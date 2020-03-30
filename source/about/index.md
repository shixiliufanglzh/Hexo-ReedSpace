---
title: about
date: 2020-03-29 10:53:11
---


```typescript
/**
 * get blog list of some user
 * @param {string} userName
 * @param {number} [pageIndex=0]
 * @return {Promise<IResData<any>>}
 */
export async function getProfileBlogs(
    userName: string,
    pageIndex: number = 0,
): Promise<IResData<any>> {
    const result = await getBlogsByUser(userName, pageIndex, PAGE_SIZE);
    if (result) {
        const blogList = result.blogs;
        return new SuccessModel({
            isEmpty: blogList.length <= 0,
            count: result.count,
            pageSize: PAGE_SIZE,
            pageIndex,
            blogList,
        });
    }
    return new ErrorModel(apiErrInfo.getBlogFail);
}

/**
 * get blog list of some user
 * @param {string} userName
 * @param {number} [pageIndex=0]
 * @return {Promise<IResData<any>>}
 */
export async function getProfileBlogs(
    userName: string,
    pageIndex: number = 0,
): Promise<IResData<any>> {
    const result = await getBlogsByUser(userName, pageIndex, PAGE_SIZE);
    if (result) {
        const blogList = result.blogs;
        return new SuccessModel({
            isEmpty: blogList.length <= 0,
            count: result.count,
            pageSize: PAGE_SIZE,
            pageIndex,
            blogList,
        });
    }
    return new ErrorModel(apiErrInfo.getBlogFail);
}

/**
 * get blog list of some user
 * @param {string} userName
 * @param {number} [pageIndex=0]
 * @return {Promise<IResData<any>>}
 */
export async function getProfileBlogs(
    userName: string,
    pageIndex: number = 0,
): Promise<IResData<any>> {
    const result = await getBlogsByUser(userName, pageIndex, PAGE_SIZE);
    if (result) {
        const blogList = result.blogs;
        return new SuccessModel({
            isEmpty: blogList.length <= 0,
            count: result.count,
            pageSize: PAGE_SIZE,
            pageIndex,
            blogList,
        });
    }
    return new ErrorModel(apiErrInfo.getBlogFail);
}

/**
 * get blog list of some user
 * @param {string} userName
 * @param {number} [pageIndex=0]
 * @return {Promise<IResData<any>>}
 */
export async function getProfileBlogs(
    userName: string,
    pageIndex: number = 0,
): Promise<IResData<any>> {
    const result = await getBlogsByUser(userName, pageIndex, PAGE_SIZE);
    if (result) {
        const blogList = result.blogs;
        return new SuccessModel({
            isEmpty: blogList.length <= 0,
            count: result.count,
            pageSize: PAGE_SIZE,
            pageIndex,
            blogList,
        });
    }
    return new ErrorModel(apiErrInfo.getBlogFail);
}

/**
 * get blog list of some user
 * @param {string} userName
 * @param {number} [pageIndex=0]
 * @return {Promise<IResData<any>>}
 */
export async function getProfileBlogs(
    userName: string,
    pageIndex: number = 0,
): Promise<IResData<any>> {
    const result = await getBlogsByUser(userName, pageIndex, PAGE_SIZE);
    if (result) {
        const blogList = result.blogs;
        return new SuccessModel({
            isEmpty: blogList.length <= 0,
            count: result.count,
            pageSize: PAGE_SIZE,
            pageIndex,
            blogList,
        });
    }
    return new ErrorModel(apiErrInfo.getBlogFail);
}
```