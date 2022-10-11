# <font color="blue">**API 相关**</font>

## 1. API 的分类

- 1). REST API（ restful 风格的 API）--> 现在大部分项目都是这个风格

  - 发送请求进行增删改查 CRUD 哪个操作由请求方式来决定

  - 同一个请求路径可以进行多个操作

  - 请求方式会用到 GET/POST/PUT/DELETE

- 2). 非 REST API (restless 风格的 API）

  - 请求方式不决定请求的增删改查 CRUD 操作

  - 一个请求路径只对应一个操作

  - 一般只有 GET/POST

## 2. 使用 json-server 搭建 REST API 用来模拟和服务器数据交互

1). json-server 是什么? 用来快速搭建 REST API 的工具包

2). 使用 json-server

​ ① 在线文档：https://github.com/typicode/json-server

​ ② 下载： npm install -g json-server

​ ③ 目标根目录下创建数据库 json 文件：db.json

​ ④ 执行命令: json-server --watch db.json --> --watch 可省略不写

```json
## 目标根目录下创建数据库json文件: db.json, 如下：
{
 "posts": [
   {"id": 1, "title": "json-server", "author": "typicode" }
 ],
  "comments": [
   {"id": 1, "body": "some comment", "postId": 1 }
 ],
   "profile": {"name": "typicode" }
}

## 启动服务器
  执行命令: json-server --watch db.json  -->  --watch可省略不写
```

**备注：**

学过 express 可以自己创建接口，如果不懂 express，可以通过 json-server 帮助创建一个接口

## 3. 使用浏览器访问测试

```js
 http://localhost:3000/posts
 http://localhost:3000/posts/1
```

## 4. 使用 postman 测试接口

测试 GET/POST/PUT/DELETE 请求

![Utiliser Postman pour concevoir une API](https://cdn.sanity.io/images/kjg6yd05/production/f2c5a50f886bf471c6f5261121c9e2ac6647e68a-800x565.jpg?w=3840&fit=clip)

## 5.一般 http 请求与 ajax 请求

1). ajax 请求是一种特别的 http 请求

2). 对服务器端来说，没有任何区别，区别在浏览器端

3). 浏览器端发请求：只有 XHR 或 fetch 发出的才是 ajax 请求，其他所有的都是非 ajax 请求

4). 浏览器端接收到响应

​ ① 一般请求：浏览器一般会直接显示响应体数据，也就是我们常说的自动刷新 / 跳转页面

​ ② ajax 请求：浏览器不会对界面进行任何更新操作，只是调用监视的回调函数并传入响应相关数据

[目录](README)
