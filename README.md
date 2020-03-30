# Hexo-ReedSpace
personal blog website

## 1 介绍
- 基于Hexo搭建的个人博客网站
- 使用了主题[hexo-theme-huhu](https://github.com/shixiaohu2206/hexo-theme-huhu.git)

## 2 运行项目
关于hexo项目怎么跑起来，官方文档已经比较清晰，这里就直接描述最简单的几个关键的命令

### 2.1 拷贝项目到本地
```bash
$ git clone git@github.com:shixiliufanglzh/hexo-reed-space.git
```

### 2.2 安装依赖
在项目根目录下运行命令：
```bash
$ npm install
```

### 2.3 启动
安装完成后，输入以下命令以启动服务器，网站会在 http://localhost:4000 下启动。
```bash
$ hexo server
```
可以简写
```bash
$ hexo s
```
使用 -p 选项指定其他端口
```bash
$ hexo server -p 5000
```

### 2.4 生成静态文件
```bash
$ hexo generate
```
可以简写
```bash
$ hexo g
```
静态文件会生成到 `public` 目录下。

## 3 搭建历程
这一块主要介绍这个项目从开始到完成的搭建过程，虽然整个项目基本都是拿来主义，但其中也遇到一些挫折，描述一下克服的过程，也许可以为后面搭建类似项目提供经验参考。

### 3.1 安装前提
- Node.js (尽量使用 Node.js 10.0 及以上版本)
- git

### 3.2 安装Hexo
```bash
$ npm install -g hexo-cli
```
### 3.3 初始化Hexo项目
执行下列命令，Hexo 将会在指定文件夹中新建所需要的文件。
```bash
$ hexo init <folder>
$ cd <folder>
$ npm install
```
新建完成后，指定文件夹的目录如下：
```bash
.
├── _config.yml
├── package.json
├── scaffolds
├── source
|   ├── _drafts
|   └── _posts
└── themes
```
### 3.4 安装主题
这里选择了主题[hexo-theme-huhu](https://github.com/shixiaohu2206/hexo-theme-huhu.git)，其他主题也是一样的操作方式。
在项目根目录下运行以下命令：
```bash
git clone https://github.com/shixiaohu2206/hexo-theme-huhu.git themes/hexo-theme-huhu
```
然后修改根目录下的 `_config.yml` 中的 theme 为 `hexo-theme-huhu`。
本主题需要安装`shelljs`，因为 requiresJS 打包时，需要执行 bash 命令

```bash
npm install --save shelljs
```

### 3.5 站内搜索
目前主题只支持自生成搜索文件的方式，因为依赖第三方站内搜索，始终不是很稳定的赶脚，而且会加载许多第三方的服务文件，导致博客首屏加载慢。
安装`hexo-generator-json-content`插件，用于生成站内搜索生成文件

```bash
npm install --save hexo-generator-json-content
```

在根目录下的 `_config.yml` 中新增配置，如下:

```yml
#https://github.com/alexbruno/hexo-generator-json-content
jsonContent:
  dateFormat: YYYY/MM/DD
  pages: false
  posts:
    tags: true
    title: true
    date: true
    text: true
    permalink: true
    photos: true
  file: content.json
```

### 3.6 新建 about 页面

about 页面没有单独 layout，直接以 markdown 渲染

```bash
hexo new page "about"
```

### 3.7 新建 tags、categories、friends 页面

```bash
hexo new page "tags"
hexo new page "friends"
hexo new page "categories"
```
tags、categories、friends 有单独的 layout，所以新增命令后，需要在 `/source/` 下对应的文件中新增 layout 参数，例如：
```markdown
---
title: categories
date: 2020-03-29 10:59:55
layout: categories
---
```

### 3.8 外围配置
该主题提供了 `友链`、`GTM 统计`、`Goole 站点`、`Google 广告`、`百度站点`、`百度联盟`、`百度统计`等等其他丰富的功能，我这里暂时并没有使用，主题的[相关文档](https://github.com/shixiaohu2206/)有介绍如何配置，这里就不介绍了。


### 3.9 代码高亮
主题[hexo-theme-huhu](https://github.com/shixiaohu2206/)支持 highlight.js 官方的 css，[highlight.js 官网](https://highlightjs.org/static/demo/)看中哪个颜色搭配，复制 css 样式替换`themes\huhu\source\style\highlight.styl`，这里使用的主题是`“Night Owl”`。

在根目录下的 `_config.yml` 中修改 *Writing* 部分配置，如下:

```yml
highlight:
  enable: true #开启代码块高亮
  line_number: true #显示行号
  auto_detect: true #如果未指定语言，则启用自动检测
  tab_replace: '' # 用 n 个空格替换 tabs；如果值为空，则不会替换 tabs
  wrap: true #Wrap the code block in <table>
  hljs: true #默认为false,新增hljs参数，并设为true，不然无法使用highlight.js 官方的 css
```

### 3.10 文章评论
主题支持两种方案：
1. valine (依赖LeanCloud)
2. 畅言

我这里选择的是valine
- tbd

遇到报错
```
Code -1: undefined [410 GET https://avoscloud.com/1.1/classes/Comment]
```

```yml
#valine评论
valine:
  API_ID: ''
  API_KEY: ''
```


### 3.11 RSS
- tbd
<!-- 安装插件`hexo-generator-feed`

```bash
npm install --save hexo-generator-feed
```

在根目录配置 `_config.yml` 中添加

```yml
#rss
feed:
  type: atom
  path: atom.xml
  limit: 20
  hub:
  content:
  content_limit: 140
  content_limit_delim: ''
  order_by: -date
  icon: icon.png
``` -->

### 3.12 置顶
- tbd
<!-- 
```bash
#卸载官方插件
npm uninstall hexo-generator-index --save

#安装插件
npm install hexo-generator-index-pin-top --save
```

在 markdown 文件的 `Front-matter`，新增 `top: 1`即可，top 值越大，越靠前展示

主题在列表页增加了置顶的小图标，具体样式查看[虎虎博客](https://blog.utone.xyz/) -->


### 3.13 自定义follow
- tbd
- iconfont 补充图标库

