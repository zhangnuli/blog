---
title: "Fetch API"
date: 2019-02-23
permalink: "/javascript/Fetch-API"
meta:
  - name: description
    content: 一个热爱文学的伪程序猿，张努力，Node，webpack，JavaScript，爱好者，博客
  - name: keywords
    content: 一个热爱文学的伪程序猿，张努力，Node，webpack，JavaScript，爱好者，博客
---

# Fetch API

- 提供了一个 JavaScript 接口，用于访问和操纵 HTTP 管道的部分，例如请求和响应。它还提供了一个全局 fetch()方法，该方法提供了一种简单，合理的方式来跨网络异步获取资源。

- 已经作为现代浏览器中异步网络请求的标准方法，其使用 Promise 作为基本构造要素。

* 不兼容 IE 浏览器

## 使用 fetch 进行请求

```javascript
//这段代码表示，fetch 创建了一个 HTTP 请求，去本域下请求 file.json 资源。
fetch('/file.json')

//请求数据返回的只是一个 HTTP 响应而不是真的JSON。为了获取JSON的内容，我们需要使用  json()方法
fetch('https://api.zhangnuli.xyz/fetch')
  .then(function(response) {
    返回promise
    return response.json();
  })
  .then(function(myJson) {
    //获取到的数据
    console.log(myJson);
  })
  //捕获错误
 .catch(err=>console.error(err))

```

## 参数

- fetch 可以接收到第二个参数

```javascript
fetch(url, {
    body: JSON.stringify(data),
    cache: 'no-cache',
    credentials: 'same-origin',
    headers: {
      'user-agent': 'Mozilla/4.0 MDN Example',
      'content-type': 'application/json'
    },
    method: 'POST',
    mode: 'cors'
  })

```

### body：需要传送的数据体

### cache：处理缓存

- default: 表示 fetch 请求之前将检查下 http 的缓存.
-
- no-store: 表示 fetch 请求将完全忽略 http 缓存的存在. 这意味着请求之前将不再检查下

- http 的缓存, 拿到响应后, 它也不会更新 http 缓存.

- no-cache: 如果存在缓存, 那么 fetch 将发送一个条件查询 request 和一个正常的 request, 拿到响应后, 它会更新 http 缓存.

- reload: 表示 fetch 请求之前将忽略 http 缓存的存在, 但是请求拿到响应后, 它将主动更新 http 缓存.

* force-cache: 表示 fetch 请求不顾一切的依赖缓存, 即使缓存过期了, 它依然从缓存中读取. 除非没有任何缓存, 那么它将发送一个正常的 request.

- only-if-cached: 表示 fetch 请求不顾一切的依赖缓存, 即使缓存过期了, 它依然从缓存中读取. 如果没有缓存, 它将抛出网络错误(该设置只在 mode 为”same-origin”时有效)

### credentials：跨域请求中需要带有 cookie 时, 可在 fetch 方法的第二个参数对象中添加 credentials 属性, 并将值设置为”include

### headers：请求头

### method：请求方法（post,get,put, delete）

### mode：可以设置不同的模式使得请求有效

- same-origin: 表示同域下可请求成功; 反之, 浏览器将拒绝发送本次 fetch, 同时抛出错误 “TypeError: Failed to fetch(…)”.

* cors: 表示同域和带有 CORS 响应头的跨域下可请求成功. 其他请求将被拒绝.

- cors-with-forced-preflight: 表示在发出请求前, 将执行 preflight 检查.

* no-cors: 常用于跨域请求不带 CORS 响应头场景, 此时响应类型为 “opaque”
