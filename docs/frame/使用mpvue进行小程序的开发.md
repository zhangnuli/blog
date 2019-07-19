---
title: "使用mpvue进行小程序的开发"
date: 2019-05-11
permalink: "/frame/使用mpvue进行小程序的开发"
meta:
  - name: description
    content: 一个热爱文学的伪程序猿，张努力，Node，webpack，JavaScript，爱好者，博客
  - name: keywords
    content: 一个热爱文学的伪程序猿，张努力，Node，webpack，JavaScript，爱好者，博客
---


## 记录一次使用 mpvue

- mpvue 是基于 vue-cli@2.x 的脚手架的

* 如果安装的的是@vue/cli 3.x 可以安装一个

```bash
npm install -g @vue/cli-init

//然后

vue init mpvue/mpvue-quickstart my-project

//进入目录

npm install 安装依赖

//启动

npm run dev

```

### 开发的时候没有使用小程序的 http.request,而是使用了 flyio 库来进行 http 请求

```javascript
//安装 npm install flyio -D

在和pages同级目录下新建了一个apis文件夹

//在apis文件夹下新建index.js

//对flyio简单的封装

const Fly = require('flyio/dist/npm/wx')
const fly = new Fly()
fly.config.baseURL = 'https://tencentads.event.com.cn'
// 添加响应拦截器，响应拦截器会在then/catch处理之前执行
fly.interceptors.response.use(
  (response) => {
    // 只将请求结果的data字段返回
    return response.data
  }
)
export default fly

```

- 然后就可以愉快的使用 Promise 来进行 http 请求了

### mpvue 可以使用 vue 的生命周期也可以使用小程序的生命周期

- 在 onLoad 或者 created 进行 http 请求时,一打开小程序即使没有进入到对应的页面也会进行 http 请求,查了一下文档,如果不想一打开小程序就进行数据的请求那么可以在 onShow 的时候进行请求

* 有的时候数据更新了,但是页面却没有发生对应的变化,可以爱 nextTick 函数里进行数据的更新



###  跳转页面的时候携带参数

- 页面onLoad的时候可以通过 `this.$root.$mp.query`来获取带参数
- 页面onShow的时候可以通过`this.$root.$mp.appOptions` 来获取参数