---
title: "socket.io初探"
date: 2019-02-23
permalink: "/javascript/socket.io初探/"
---

#### 安装 socket.io 库,我这里使用了 express 框架(没有使用原生 node),所以在这里一并安装了

```bash
npm install socket.io express --save-dev
```

#### 安装完成以后我们新建一个 index.js,然后再`index.js`里面编写:

#####  服务端使用

```javascript
创建http服务和io服务
const express = require("express");
const app=express();
const http = require("http").Server(app);               
const socket= require("socket.io")(http);                              

//访问根路径返回index.html               
app.get("/", (req, res) => {                 
    res.sendfile(__dirname+'/index.html')                 
    });                              
    
//建立连接               
socket.on('connection',function(socket){               
    /.../               
}  

```

 - 客户端使用 

 ```               javascript
 <script src="http://localhost:8080/socket.io/socket.io.js"></script>                              
 
 //建立连接               
 const socket = io.connect("ws://192.168.1.120:8080");   

 ```
  - > 当服务端和客户端连接成功时，服务端会监听到connection和connect事件，客户端会监听到connect事件，断开连接时服务端对应到客户端的socket与客户端均会监听到disconcect事件。                              

  #### 推送消息                              

  - > socket.emit('[定义的接口名字]',data);例如:                              

  ```               javascript
  socket.emit('test','我是个测试');              
  ```

  #### 接收消息                              
  - > socket.on('[定义的接口名字]',data=>{}) 例如:                              
  ```               javascript
  socket.on('test',data=>{                 
      //接收到数据做一些事情               
})               

  ```
#### 服务端广播消息                              
```               javascript
//需要广播除自己外的其他人,只需要加一个broadcast              
socket.broadcast.emit('[接口]',data)  
```
