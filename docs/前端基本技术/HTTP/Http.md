# <font color="blue">**HTTP**</font>

## 1. MDN 文档

https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Overview

## 2. HTTP 请求交互的基本过程

1. 浏览器端向服务器发送 HTTP 请求(请求报文)

2. 后台服务器接收到请求后, 处理请求, 向浏览器端返回 HTTP 响应(响应报文)

3. 浏览器端接收到响应, 解析显示响应体或调用监视回调

## 3. HTTP 请求报文

1). 请求行:
格式：method url
例如：GET /product_detail?id=2 或 POST /login

2). 请求头 headers(一般有多个请求头)
Host: www.baidu.com
Cookie: BAIDUID=AD3B0FA706E; BIDUPSID=AD3B0FA706;
Content-Type: application/x-www-form-urlencoded 或者 application/json

3). 请求体 body
username=tom&pwd=123
{"username": "tom", "pwd": 123}

**PS：GET 请求没有请求体 body**

## 4. HTTP 响应报文

1). 响应行：
格式：status statusText
例如：200 OK 或 404Not Found

2). 响应头(一般有多个响应头)
Content-Type: text/html;charset=utf-8
Set-Cookie: BD_CK_SAM=1;path=/

3). 响应体
html 文本/json 文本/js/css/图片...

## 5. 常见响应状态码

- 200 OK 请求成功。一般用于 GET 与 POST 请求

- 201 Created 已创建。成功请求并创建了新的资源

- 401 Unauthorized 未授权/请求要求用户的身份认证

- 404 Not Found 服务器无法根据客户端的请求找到资源

- 500 Internal Server Error 服务器内部错误，无法完成请求

## 6. 请求方式与请求参数

1- **请求方式**

1. GET: 从服务器端读取数据 ---> 查(R)
2. POST：向服务器端添加或提交新数据 --> 增(C)
3. PUT: 更新服务器端已存在的数据 --> 改(U)
4. DELETE: 删除服务器端数据 --> 删(D)

2- **请求参数**

1. **query 参数：查询字符串参数**

   ​ a. 参数包含在请求地址中，格式为：/xxxx?name=tom&age=18

   ​ b. 敏感数据不要用 query 参数，因为参数是地址的一部分，比较危险

   备注：query 参数又称查询字符串参数，编码方式为 urlencoded,因为 name=tom&age=18 这一形式就叫 urlencoded

2. **params 参数**

   ​ a. 参数包含在请求地址中，格式如下：

   `http://localhost:3000/add_person/tom/18`

   ​ b. 敏感数据不要用 params 参数，因为参数是地址的一部分, 比较危险

3. **body 请求体参数**

   ​ a. 参数包含在请求体中，在 url 地址中根本看不见，可通过浏览器开发者工具查看

   ​ b. 常用的两种编码格式：

   ​ -格式 1: **urlencoded 格式，即 key-value&key=value...的编码形式**

   ​ 例如：name=tom&age=18

   **请求地址里携带 urlencoded 编码形式的参数，叫做<mark>查询字符串参数</mark>**

   ​ **对应请求头：Content-Type: application/x-www-form-urlencoded**

   ​ <mark> 备注：如果请求体中带有 urlencoded 格式的参数，就必须得写上对应的请求头 </mark> <mark>Content-Type: application/x-www-form-urlencoded</mark>

   ​

   -格式 2：**json 格式，即 {key:value, key:value...} 的编码形式**

   ​ 例如：{"name":"tom", "age": 12}

   ​ **对应请求头：Content-Type: application/json**

   <mark>备注：如果请求体中带有 json 格式的参数，就必须得写上对应的请求头</mark> <mark>Content-Type: application/json</mark>

   ​ c. 还有一种不常用的编码格式：

   ​ Content-Type: multipart/form-data 用于文件上传请求

**特别注意：**

1. GET 请求不能携带请求体参数，因为 GET 请求没有请求体

2. 理论上任何请求可以随意使用上述 3 种类型参数中的任何一种，也就是理论上讲，4 种请求方式和 3 种参数形式之间可以任意组合，除了 GET 请求不能携带请求体 body 参数以外，甚至一次请求的 3 个参数可以用 3 种形式携带，但一般不这样做

3. 一般来说我们有一些约定俗成的规矩：

   a. 例如 form 表单发送 post 请求时：自动使用请求体参数，用 urlencoded 编码

   ​ b. 例如 jQuery 发送 ajax post 请求时：自动使用请求体参数，用 urlencoded 编码 (jQuery 有回调地狱问题)

4. **开发中请求到底发给谁？用什么请求方式？携带什么参数？**

   **要参考项目的 API 接口文档**

   [目录](README)
