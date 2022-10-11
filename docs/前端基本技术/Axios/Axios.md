[目录](README)

# Axios

## axios 的理解和使用

## 1. axios 是什么？

1). 前端最流行的 ajax 请求库.

​ axios 借助 async await 解决了回调地狱的问题，提供了拦截器，还提供批量发送请求，因此得到程序员和市场的认可.

2). react / vue 官方都推荐使用 axios 发 ajax 请求

( 因为原生的 XHR 太麻烦，而 jQuery 有回调地狱问题, 因此 axios 是最佳选择 )

3). 文档：`https://github.com/axios/axios`

## 2. axios 特点

1). 基于 promise 的异步 ajax 请求库

2). 浏览器端 或 node 端(node.js 里)都可以使用

3). 支持请求 和响应拦截器

4). 支持请求取消

5). 请求 / 响应数据转换

6). 批量发送多个请求

## 3. 使用 axios 发 ajax 请求

```js
/* 1.GET请求：从服务器端获取数据 */
function testGet() {
  axios({
    url: "http://localhost:3000/posts",
    // url:'http://localhost:3000/posts2',
    method: "GET",
    params: {
      id: 1,
      xxx: "abc",
    },
  });
}
```

备注：要启动 axios 对应的服务器(假如服务器名为：myserver.js), 在 cmd 使用的命令是：node myserver.js 服务器启动成功后，就可以开始写 axios 发送的各种请求了

## 4. 测试访问: 使用 axios

```js
/* 先把axios模块引入到项目中 */
<script src="https://cdn.bootcss.com/axios/0.19.0/axios.js"></script>

<script>
  // 30分钟内不再发预检请求
  // axios.defaults.headers["Access-Control-Max-Age"] = "1800"

  /* 1. GET请求: 从服务器端获取数据*/
  function testGet() {
    // axios.get('http://localhost:3000/posts') // 获取所有posts的数组
    // axios.get('http://localhost:3000/posts/1') // 获取id为1的数组
    // axios.get('http://localhost:3000/posts?id=1&id=2') // 获取id为1或2的数组
    // axios.get('http://localhost:3000/posts?title=json-server&author=typicode')
  }
  testGet()

  /* 2. POST请求: 向服务器端添加新数据*/
  function testPost() {
    // axios.post('http://localhost:3000/comments', {body: 'xxx', postId: 1}) // 保存数据
  }
  testPost()

  /* 3. PUT请求: 更新服务器端已经数据 */
  function testPut() {
    // axios.put('http://localhost:3000/comments/4', {body: 'yyy', postId: 1})
  }
  testPut()

  /* 4. DELETE请求: 删除服务器端数据 */
  function testDelete() {
    // axios.delete('http://localhost:3000/comments/4')
  }
  testDelete()
</script>
```

## 5.axios 的基本使用：

先启动这个 html 文件的接口服务器(命令：node 服务器名称)，启动成功后可以开始写 axios 各种请求，服务器用来做请求数据交互

或者使用 json-server 搭建的服务器，命令：json-server --watch db.json --> 前提是先创建一个文件名为 db.json 的 json 数据用来做请求数据交互

```html
<head>
  <meta charset="UTF-8" />
  <title>axios的基本使用</title>
  // 先引入axios模块(可从官网把axios模块下到本地再引入)
  <script type="text/javascript" src="./js/axios.min.js"></script>
</head>

<body>
  <button id="btn1">点击获取所有人的信息</button>

  <script type="text/javascript">
       //获取按钮
       const btn1 = document.getElementById('btn1')
       // 绑定onclick事件
       // 获取所有人的信息--发送GET请求--不携带参数
       btn1.onclick = ()=>{
           // 完整版
           axios({
               method: 'GET',
               //请求地址
               url: 'http://localhost:3000/posts',
           }).then(
               response => {console.log('请求成功',response.data)}，
               error = {console.log('请求失败', error)}
           )

           //精简版
           axios.get('http://localhost:3000/posts').then(
               response => {console.log('请求成功',response.data)}，
               error = {console.log('请求失败', error)}
           )
       }
    /* 总结：
      1. axios调用的返回值是promise实例. 即axios.get('http://localhost:3000/posts/1')返回一个promise实例
      2. 成功的值叫response, 失败的值叫error
      3. axios成功的值是一个axios封装的response对象，服务器返回的真正数据在response.data中
      4. 携带query参数时，编写的配置项叫做params.注意！！
      5. 携带params参数时，就需要自己手动拼在url地址后面.注意！！
    */
  </script>
</body>
```

如果只想获取成功的值 response, 使用 async await 结构会更加优化，就不用.then 去指定成功/失败的回调, 如果请求成功，async await 结构会直接返回成功的值 (react, vue 中使用 async await 会方便很多)

```js
<head>
  <meta charset="UTF-8">
  <title>axios的基本使用</title>
    // 先引入axios模块(可从官网把axios模块下到本地再引入)
  <script type="text/javascript" src="./js/axios.min.js"></script>
</head>

<body>
  <button id="btn1">点击获取所有人的信息</button>

  <script type="text/javascript">
      //获取按钮
      const btn1 = document.getElementById('btn1')

     // async await结构，如果请求成功，直接返回成功的值
      btn1.onclick = async ()=>{
          //精简版
        const result = await axios.get('http://localhost:3000/posts/1')
      }

  </script>
</body>
```

### - 关于 GET 请求：

<font color="red">**注意 params，写的是 params，但携带的是 query 查询参数**</font>，**因为这里的 params 取的是该英文单词本身的原文意思，指的就是“参数”的意思，和包含在 url 地址中 `http://localhost:3000/add_person/tom/18的params参数 /add_person/tom/18` 是完全 2 个意思，二者之间完全没关系.**

那如果要配置真正的 params 参数，该如何写呢？

**如果真想带 params 参数，axios 没有设置 params 配置项，没有对应的配置项可以写，只能直接在 url 地址后面直接写上 params 参数，即在 `http://localhost:3000` 后面直接加上 /add_person/tom/18 这部分 params 参数.**

意思就是说 axios 只设置了 query 配置项，query 配置时写的 key 却是单词 params，而 axios 根本没有设置 url 地址的 params 参数部分的配置项，要配置 url 地址的 params 参数只能手动在 url 地址后面添加.

```js
<head>
  <meta charset="UTF-8">
  <title>axios的基本使用</title>
    // 先引入axios模块(可从官网把axios模块下到本地再引入)
  <script type="text/javascript" src="./js/axios.min.js"></script>
</head>

<body>
  <button id="btn1">点击获取所有人的信息</button>
  <button id="btn2">点击获取某个人的信息</button>
  <input id="person_id" type="text" placeholder="输入个人id">

  <script type="text/javascript">
      //获取按钮和input节点
     const btn1 = document.getElementById('btn1')
     const btn2 = document.getElementById('btn2')
     const personId = document.getElementById('person_id')

     // 完整版，获取某个人的信息--发送GET请求--携带query参数
     // 点击按钮2，获取input框用户输入的内容
    btn2.onclick = ()=>{
        axios({
            method: 'GET',
            //请求地址
            url: 'http://localhost:3000/posts',
          // 此处写的是params，但携带的是query查询参数
          // personId.value 是input框里用户输入的内容
            params:{id:personId.value}
        }).then(
            response => {console.log('请求成功',response.data)}，
            error = {console.log('请求失败', error)}
    )

        // 精简版，带query参数
       // params:{id:personId.value} --》这是query参数
        axios.get('http://localhost:3000/posts',{params:{id:personId.value}}).then(
            response => {console.log('请求成功',response.data)}，
            error = {console.log('请求失败', error)}
    )

 }

  </script>
</body>
```

##### 常见的 GET 请求：

- 浏览器地址栏输入网址时，即浏览器请求页面时，且无法手动更改

- 可以请求外部资源的 html 标签，例如 `<img>` `<a>` `<link>` `<script>`, 且无法手动更改

- 发送 Ajax 请求时如果没有指定发送请求的方式，默认就是 GET 请求

- form 表单提交时，如果没有指定方式，默认也是 GET 请求

### - 关于 POST 请求：

POST 请求带请求体，POST 请求的参数是放在请求体里，有 2 种编码格式：

1. json
2. urlencoded

<font color="red">**POST 请求体的参数配置格式：**</font>

1. **默认是 json 编码格式 data:{ key:value, key:value... },** 例如：

   ```js
   data:{
      name:psersonName.value,
      age:personAge.value
   }
   ```

   在开发者工具里可看到请求头那里自动就是:
   Content-Type:application/json

   备注：现在前后端数据交互，如果使用 axios，post 请求一般携带 json 编码，如果接口文档中没有指明清楚，意味着后端可以解析 json 和 urlencoded 两种编码格式.

2. **urlencoded 编码格式要使用模板字符串进行配置,** 例如：

```js
data: `name=${personName.value}&age=${personAge.value}`;
```

​ 在开发者工具里可看到请求头那里自动就是:
​ Content-Type:application/x-www-form-urlencoded

```js
<head>
  <meta charset="UTF-8">
  <title>axios的基本使用</title>
    // 先引入axios模块(可从官网把axios模块下到本地再引入)
  <script type="text/javascript" src="./js/axios.min.js"></script>
</head>

<body>
  <button id="btn1">点击获取所有人的信息</button>
  <button id="btn2">点击获取某个人的信息</button>
  <input id="person_id" type="text" placeholder="输入个人id">
  <button id="btn3">点击添加某个人的信息</button>
  <input id="person_name" type="text" placeholder="输入名字">
  <input id="person_age" type="text" placeholder="输入年龄">

  <script type="text/javascript">
      //获取按钮和input节点
     const btn1 = document.getElementById('btn1')
     const btn2 = document.getElementById('btn2')
     const btn3 = document.getElementById('btn3')
     const personId = document.getElementById('person_id')
   const personName = document.getElementById('person_name')
   const personAge = document.getElementById('person_age')

//完整版添加某个人的信息--发送POST请求--携带json或urlencoded编码参数 // 点击按钮3，获取input框用户输入的内容
    btn3.onclick = ()=>{
        axios({
            method: 'POST',
            //请求地址
            url: 'http://localhost:3000/posts',
          // 携带post请求体参数，默认是json编码
            data:{
                name:psersonName.value,
                age:personAge.value}
        }).then(
            response => {console.log('请求成功',response.data)}，
            error = {console.log('请求失败', error)}
    )

    // 携带post请求体参数, urlencoded编码
     axios({
      data:`name=${personName.value}&age=${personAge.value}`
     }).then(
            response => {console.log('请求成功',response.data)}，
            error = {console.log('请求失败', error)}
    )

  // 精简版，post请求体直接写参数对象，不要写data，就是json编码的参数
  // 参数对象{name:personName.value, age:personAge.value}
        axios.post('http://localhost:3000/posts',{name:personName.value, age:personAge.value}).then(
            response => {console.log('请求成功',response.data)}，
            error = {console.log('请求失败', error)}
    )

 //精简版,post请求体用模块字符串写参数，不写data，就是urlencoded编码
    // `name=${personName.value}&age=${personAge.value}`
     axios.post('http://localhost:3000/posts',`name=${personName.value}&age=${personAge.value}`).then(
            response => {console.log('请求成功',response.data)}，
            error = {console.log('请求失败', error)}
    )

 }

  </script>
</body>
```

##### 常见的 POST 请求

- 发送 Ajax 请求时明确指定使用 POST 方式

- 使用第三方发送请求库时明确指定使用 POST 方式

- form 表单提交时明确指定使用 POST 方式

### - 关于 PUT 请求

PUT 请求也带请求体, 请求体里的参数编码格式和 POST 请求一样

```js
<head>
  <meta charset="UTF-8">
  <title>axios的基本使用</title>
    // 先引入axios模块(可从官网把axios模块下到本地再引入)
  <script type="text/javascript" src="./js/axios.min.js"></script>
</head>

<body>
  <button id="btn1">点击获取所有人的信息</button>
  <button id="btn2">点击获取某个人的信息</button>
  <input id="person_id" type="text" placeholder="输入个人id">
  <button id="btn3">点击添加某个人的信息</button>
  <input id="person_name" type="text" placeholder="输入名字">
  <input id="person_age" type="text" placeholder="输入年龄">
  <button id="btn4">点击更新某个人的信息</button>
<input id="person_update-id" type="text" placeholder="输入id">
<input id="person_update-name" type="text" placeholder="输入名字">
<input id="person_update-age" type="text" placeholder="输入年龄">

  <script type="text/javascript">
      //获取按钮和input节点
     const btn1 = document.getElementById('btn1')
     const btn2 = document.getElementById('btn2')
     const btn3 = document.getElementById('btn3')
     const btn4 = document.getElementById('btn4')
     const personId = document.getElementById('person_id')
   const personName = document.getElementById('person_name')
   const personAge = document.getElementById('person_age')
   const personUpdateId = document.getElementById('person_update-id')
  const personUpdateName = document.getElementById('person_update-name')
  const personUpdateAge = document.getElementById('person_update-age')

//完整版更新某个人的信息--发送POT请求--携带json或urlencoded编码参数 // 点击按钮4，获取input框用户输入的内容
    btn4.onclick = ()=>{
        axios({
            method: 'PUT',
            //请求地址
            url: 'http://localhost:3000/posts',
          // 携带put请求体参数，默认是json编码
            data:{
                id:psersonUpdateId.value,
                name:psersonUpdateName.value,
                age:personUpdateAge.value}
        }).then(
            response => {console.log('请求成功',response.data)}，
            error = {console.log('请求失败', error)}
    )

         // 精简版
        axios.put('http://localhost:3000/posts',{
            id:psersonUpdateId.value,
            name:psersonUpdateName.value,
            age:personUpdateAge.value
        }).then(
            response => {console.log('请求成功',response.data)}，
            error = {console.log('请求失败', error)}
    )
 }

  </script>
</body>
```

### - 关于 DELETE 请求

1. 如果服务端将参数当做 url query 参数 接收，则格式为：

   **{params: param}，这样发送的 url 将变为`http:www.XXX.com?a=…&b=…`**

2. 如果是服务端将参数当作 Java 对象来封装接收则 参数格式为：

   **{data: param}**

```js
<head>
  <meta charset="UTF-8">
  <title>axios的基本使用</title>
    // 先引入axios模块(可从官网把axios模块下到本地再引入)
  <script type="text/javascript" src="./js/axios.min.js"></script>
</head>

<body>
  <button id="btn1">点击获取所有人的信息</button>
  <button id="btn2">点击获取某个人的信息</button>
  <input id="person_id" type="text" placeholder="输入个人id">
  <button id="btn3">点击添加某个人的信息</button>
  <input id="person_name" type="text" placeholder="输入名字">
  <input id="person_age" type="text" placeholder="输入年龄">
  <button id="btn4">点击更新某个人的信息</button>
<input id="person_update-id" type="text" placeholder="输入更新的id">
<input id="person_update-name" type="text" placeholder="输入名字">
<input id="person_update-age" type="text" placeholder="输入年龄">
    <button id="btn5">点击删除某个人的信息</button>
<input id="person_delete-id" type="text" placeholder="输入删除的id">

  <script type="text/javascript">
      //获取按钮和input节点
     const btn1 = document.getElementById('btn1')
     const btn2 = document.getElementById('btn2')
     const btn3 = document.getElementById('btn3')
     const btn4 = document.getElementById('btn4')
     const personId = document.getElementById('person_id')
   const personName = document.getElementById('person_name')
   const personAge = document.getElementById('person_age')
   const personUpdateId = document.getElementById('person_update-id')
  const personUpdateName = document.getElementById('person_update-name')
  const personUpdateAge = document.getElementById('person_update-age')
  const personDeleteId = document.getElementById('person_delete-id')

//完整删除某个人的信息--发送DELETE请求-携带params参数
  // 点击按钮5，获取input框用户输入的内容
    btn5.onclick = ()=>{
        axios({
            method: 'DELETE',
        //地址携带params参数,手动在地址后面添加params参数
        // params参数就是对应的删除框input输入的内容
            url: `http://localhost:3000/post/${personDeleteId.value}`,
           ).then(
            response => {console.log('请求成功',response.data)}，
            error = {console.log('请求失败', error)}
    )

 }

  </script>
</body>
```

## 6. 前端常用的 axios 配置项，根据不同的请求及后端提供的接口文档，选择的使用需要的配置项

```js
// 请求方式: 有 GET, POST, PUT, DELETE
 method: 'GET',

//请求地址
 url: 'http://localhost:3000/posts'',

 //配置query参数
 params:{a:1,b:2},

 //配置请求体参数，参数是json编码
 data:{c:3,d:4}，

 // 配置请求体参数，参数是urlencoded编码, 使用模板字符串
 data:`e=5&f=6`,

 // 配置超时的时间
 timeout:2000

 // 配置请求头
 headers:{school:atguigu}

 // 配置响应数据的格式(json是默认值)
 responseType:'json'
```

- 可以把每个请求都会使用的配置项写成全局配置，这样就不用每个请求分别写这些配置，可优化代码.

- 全局配置项也就是 axios 的配置默认属性，格式：**axios.defaults.具体配置项， 注意 defaults 是带 s 的复数**, 例如:

  ```js
  axios.defaults.baseUrl = "http://localhost:5000";
  axios.defaults.timeout = 2000;
  axios.defaults.headers = { token: "687dhuisud235dysuucsukuysgy456" };
  ```

```js
<head>
  <meta charset="UTF-8">
  <title>axios的常用配置项</title>
    // 先引入axios模块(可从官网把axios模块下到本地再引入)
  <script type="text/javascript" src="./js/axios.min.js"></script>
</head>

<body>
  <button id="btn1">点击获取所有人的信息</button>

  <script type="text/javascript">
      //获取按钮和input节点
     const btn1 = document.getElementById('btn1')

    btn1.onclick = ()=>{
        axios({
            // 请求方式
            method: 'GET',
            //请求地址
            url: 'http://localhost:3000/posts'',
            //配置query参数
            params:{a:1,b:2},
            //配置请求体参数，参数是json编码
            data:{c:3,d:4}，
            // 配置请求体参数，参数是urlencoded编码
            data:`e=5&f=6`,
            // 配置超时的时间
            timeout:2000
           // 配置请求头
            headers:{school:atguigu}
           // 配置响应数据的格式(json是默认值)
           responseType:'json'
           ).then(
            response => {console.log('请求成功',response.data)}，
            error = {console.log('请求失败', error)}
    )

 }

  </script>
</body>
```

## 7. axios.create(config 配置项) 方法

1. 根据指定配置创建一个新的 axios, 也就是每个新创建的 axios 都有自己的配置. 方法参数 config 配置项是 key:value 的格式
2. 新创建的 axios 只是没有取消请求和批量发请求的方法, 其它所有语法和原生的 axios(即 axios 模块自带的 axios 实例)都是一致的
3. 为什么要设计这个语法?
   因为有需求: 项目中有部分接口需要的配置与另一部分接口需要的配置不太一样

```js
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8" />
        <title>axios.create方法</title>
        <script type="text/javascript" src="./js/axios.min.js"></script>
    </head>
    <body>
        <button id="btn">点我获取所有人</button><br/><br/>
        <button id="btn2">点我获取测试数据</button><br/><br/>
        <button id="btn3">点我获取笑话信息</button><br/><br/>
        <script type="text/javascript" >
            const btn = document.getElementById('btn')
            const btn2 = document.getElementById('btn2')
            const btn3 = document.getElementById('btn3')

             // 使用axios.create方法创建一个axios实例
            // 方法参数config配置项是 key:value 的格式
            const axios2 = axios.create({
                timeout:3000,
                // 有的服务器不认可配置请求头，会报错
                //headers:{name:'tom'},
                baseURL:'https://api.apiopen.top'
            })

        //给axios配置默认属性，注意是赋值，所以不是key:value形式
            axios.defaults.timeout = 2000
            axios.defaults.headers = {school:'atguigu'}
            axios.defaults.baseURL = 'http://localhost:5000'

            btn.onclick = ()=>{
                axios({
                    url:'/persons', //请求地址
                    method:'GET',//请求方式
                }).then(
                    response => {console.log('成功了',response.data);},
                    error => {console.log('失败了',error);}
                )
            }

            btn2.onclick = ()=>{
                axios({
                    url:'/test1', //请求地址
                    method:'GET',//请求方式
                }).then(
                    response => {console.log('成功了',response.data);},
                    error => {console.log('失败了',error);}
                )
            }

            btn3.onclick = ()=>{
                axios2({
                    url:'/getJoke',
                    method:'GET'
                }).then(
                    response => {console.log('成功了',response.data);},
                    error => {console.log('失败了',error);}
                )
            }
        </script>
    </body>
</html>
```

## 8. axios 中的拦截器：请求拦截器和响应拦截器

1. **axios 请求拦截器 axios.interceptors.request**

   1)- 是什么？

   在真正发请求前执行的**一个回调函数**

   2)- 作用：

   对所有的请求做统一的处理：追加请求头、追加参数、界面 loading 提示等等

   3）请求拦截器必须要接收一个配置项 config,而且必须将它返回

```js
 axios.interceptors.request.use((config)=>{
       return config
 }
```

​

2. **axios 响应拦截器 axios.interceptors.response**

   1)- 是什么？

   得到响应之后执行的**一组回调函数**

   2)- 作用：
   若请求成功，对成功的数据进行处理
   若请求失败，对失败进行统一的操作

   ​ 3)- **响应拦截器无论是是成功响应还是失败响应都必须有返回值.**
   ​ 成功响应里根据项目需要返回需要的数据
   ​ 失败响应里一般返回一个新的 promise 对象--> return new Promise(()=>{})

```js
<!DOCTYPE html>
<html>
    <head>
    <meta charset="UTF-8" />
        <title>axios中的拦截器</title>
<script type="text/javascript" src="./js/axios.min.js"></script>
</head>
<body>
    <button id="btn">点我获取所有人</button><br/><br/>

   <script type="text/javascript" >
        const btn = document.getElementById('btn')

       //请求拦截器
       axios.interceptors.request.use((config)=>{
          console.log('请求拦截器1执行了');
          if(Date.now() % 2 === 0){
              config.headers.token = 'atguigu'
          }
          return config
       })

     //响应拦截器
     axios.interceptors.response.use(
       response => {
          console.log('响应拦截器成功的回调执行了',response);
          if(Date.now() % 2 === 0) return response.data
          else return '时间戳不是偶数，不能给你数据'
      },
      error => {
          console.log('响应拦截器失败的回调执行了');
          alert(error);
          return new Promise(()=>{})
      }
    )

    btn.onclick = async()=>{
       const result = await axios.get('http://localhost:5000/persons21')
       console.log(result);
   }
    </script>
  </body>
</html>
```

## 9. axios 中取消请求，也叫中断请求

通过 axios.CalcelToken 来取消请求

1. 取消的基本使用

```js
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8" />
        <title>axios中取消请求1</title>
        <script type="text/javascript" src="./js/axios.min.js"></script>
    </head>
    <body>
        <button id="btn">点我获取测试数据</button><br/><br/>
        <button id="btn2">取消请求</button><br/><br/>
        <script type="text/javascript" >
            const btn = document.getElementById('btn')
            const btn2 = document.getElementById('btn2')
            // 通过结构赋值从axios上取得CancelToken, CancelToken能为一次请求“打标识”
            // CancelToken是一个内置的构造函数
            const {CancelToken} = axios
            let cancel

            btn.onclick = async()=>{
                 axios({
                    url:'http://localhost:5000/test1?delay=3000',
                    // key键名必须写成cancelToken，否则无效，axios规定
                    cancelToken:new CancelToken((c)=>{ //c是一个函数，调用c就可以关闭本次请求
                        cancel = c
                    })
                }).then(
                    response => {console.log('成功了',response.data);},
                    error => {console.log('失败了',error);}
                )
            }

            btn2.onclick = ()=>{
                cancel()
            }


        </script>
    </body>
</html>
```

2. 请求中的判断

   axios 的方法 isCancel() 专门用来判断错误 error 是真的错误还是因为用户取消请求导致的错误.

```js
<head>
    <meta charset="UTF-8" />
    <title>axios中取消请求2</title>
<script type="text/javascript" src="./js/axios.min.js"></script>
</head>
<body>
    <button id="btn">点我获取测试数据</button><br/><br/>
    <button id="btn2">取消请求</button><br/><br/>
    <script type="text/javascript" >
        const btn = document.getElementById('btn')
        const btn2 = document.getElementById('btn2')
        const {CancelToken,isCancel} = axios //CancelToken能为一次请求“打标识”
        let cancel

        btn.onclick = async()=>{
            // 判断之前有没有cancel，如果有cancel，说明已经发了请求，那就取消请求
            // 如果没有cancel，说明是第1次发请求
            if(cancel) cancel()
             axios({
                url:'http://localhost:5000/test1?delay=3000',
                cancelToken:new CancelToken((c)=>{ //c是一个函数，调用c就可以关闭本次请求
                cancel = c
                })
        }).then(
                response => {console.log('成功了',response.data);},
            error => {
                if(isCancel(error)){
                //如果进入判断，证明：是用户取消了请求
                console.log('用户取消了请求，原因是：',error.message);
            }else{
                console.log('失败了',error);
            }
        }
    )
}

        btn2.onclick = ()=>{
            cancel('任性，就是不要了')
        }

</script>
</body>
```

3. 取消请求和拦截器配合使用

```js
<head>
    <meta charset="UTF-8" />
    <title>axios中取消请求3</title>
   <script type="text/javascript" src="./js/axios.min.js"></script>
</head>
<body>
    <button id="btn">点我获取测试数据</button><br/><br/>
    <button id="btn2">取消请求</button><br/><br/>
    <script type="text/javascript" >
        const btn = document.getElementById('btn')
        const btn2 = document.getElementById('btn2')
        const {CancelToken,isCancel} = axios //CancelToken能为一次请求“打标识”
        let cancel

        // 请求拦截器
        axios.interceptors.request.use((config)=>{
            if(cancel) cancel('取消了')
            // cancelToken是config 的一个属性
            config.cancelToken = new CancelToken((c)=> cancel= c)
            return config
        })
        //响应拦截器
        axios.interceptors.response.use(
            response => {return response.data},
            error => {
                if(isCancel(error)){
                    //如果进入判断，证明：是用户取消了请求
                    console.log('用户取消了请求，原因是：',error.message);
                }else{
                    console.log('失败了',error);
                }
                return new Promise(()=>{})
            }
        )

        btn.onclick = async()=>{
            const result = await axios.get('http://localhost:5000/test1?delay=3000')
            console.log(result);
        }

        btn2.onclick = ()=>{
            cancel('任性，就是不要了')
        }

    </script>
</body>
```

## 10. axios 批量发送请求

通过 axios.all(参数是数组) 批量发送请求

```js
<head>
    <meta charset="UTF-8" />
    <title>8_axios批量发送请求</title>
    <script type="text/javascript" src="./js/axios.min.js"></script>
</head>
<body>
    <button id="btn">点我批量发送请求</button><br/><br/>

    <script type="text/javascript" >
        const btn = document.getElementById('btn')

    btn.onclick = async()=>{
        // 3个 GET 请求同时发送，就不要await了
        axios.all([
            axios.get('http://localhost:5000/test1'),
            axios.get('http://localhost:5000/test2?delay=3000'),
            axios.get('http://localhost:5000/test3'),
        ]).then(
            response => {console.log(response);},
            error => {console.log(error);}
        )
    }
   </script>
</body>
```

[目录](README)
