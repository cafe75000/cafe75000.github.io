[目录](README) 

# 超老师Node直播

## 第一周计划：

- 周一：Node简介和安装

- 周二~周四：异步和promise

- 周五：模块化

## Node.js

- 运行在服务器的JS

- 用来编写服务器

- 特点：
  
  - 单线程、异步、非阻塞
  
  - 统一API

## 第一周

### Node.Js简介和安装

参考： https://www.lilichao.com/index.php/2022/10/08/node-js%e7%ae%80%e4%bb%8b%e5%ae%89%e8%a3%85/

#### nvm: 用来管理node的, 可以切换不同版本的node

- 命令：
  
  - nvm list  --> 显示已经安装的node版本
  
  - nvm install 版本  --> 安装指定版本的node
  
  - 查看版本：nvm version
  
  - 配置nvm的镜像服务器
    
    ```bash
    nvm node_mirror https://npmmirror.com/mirrors/node/
    ```
  
  - nvm use 版本   --> 指定要使用的node版本

#### node.js 和 JavaScript有什么区别？

- node和JS的标准是一样的，遵循的都是ECMAScript

- DOM BOM 是浏览器独有的，node没有DOM BOM

### 进程和线程

- 进程就是一个内存空间，是程序运行的环境，程序运行需要进程

- 线程是实际进行运算的东西，也就是程序要真正运行起来需要线程

- 线程会进入到进程里运行

### 同步和同步的问题解决

参考： https://www.lilichao.com/index.php/2022/10/10/%e5%bc%82%e6%ad%a5%e7%bc%96%e7%a8%8b/

- 什么是同步:
  
  - 通常情况代码都是自下而上一行一行按顺序执行的，执行完第一行再执行第二行依次执行，如果前面的代码不执行，后面的代码也不会执行，这就是同步.
  
  - 同步的代码执行会出现阻塞的情况，一行代码执行得慢会影响整个程序的执行
  
  ```js
  console.log("哈哈")
  console.log("嘻嘻")
  console.log("嘿嘿")
  ```

- 同步阻塞问题的解决:
  
  - Java 和 python: 通过多线程来解决阻塞问题，对计算机和编程的要求较高
  
  - node.js：通过异步方式来解决这一问题. 执行速度慢的代码不影响整个程序.

### 异步

- 什么是异步？可理解为一段代码的执行不会影响到其他的程序

- 异步的问题：异步代码的执行结果无法通过return获得

- 异步的特点：
  
  - 不会阻塞其他代码的执行
  
  - **需要通过回调函数来返回代码执行的结果**

- 基于回调函数的异步带来的问题：
  
  - 代码的可读性差
  
  - 代码的可调试性差
  
  - 产生回调地狱的问题

- 解决回调地狱的问题
  
  - 需要一个可以代替回调函数来给我们返回结果的东西
  
  - 这个东西就是promise
    
    - promise是一个可以用来存储数据的对象，它存储数据的方式比较特殊，取数据的方式也比较特殊
    
    - 这种特殊方式使得promise可以用来存储异步调用的数据
    
    - promise就是可以存储异步代码的对象

```js
// cb(callback),第3个参数是回调函数
function sum(a,b,cb){ 
  setTimeout(()=>{ // 异步
    cb(a + b) // a+b的结果作为回调函数的参数进行传递
   },1000)
}
console.log("1111111") // 同步

sum(123, 456,(result)=>{
  console.log(result)
})
```

```js
function sum(a, b, cb) {
    setTimeout(() => {
        cb(a + b)
    }, 1000)

}

console.log("111111")

// 回调地狱
sum(123, 456, (result)=>{
    sum(result, 7, (result)=>{
        sum(result, 8, result => {
            sum(result, 9, result => {
                sum(result, 10, result => {
                    console.log(result)
                })
            })
        })
    })
})
```

### 回调函数的作用

- 回调函数是JS中非常重要的特点. JS 中使用了大量的异步代码

- 因为异步代码没有办法直接return结果，它是通过回调函数获得代码执行后的返回结果.

- 也就是说，异步调用必须通过回调函数来返回结果，但是当我们进行一些复杂的调用时，会出现“回调地狱”，回调函数一多就很痛苦.

- 因此要使用promise来解决异步中回调函数的回调地狱的问题

- promise有其一套特殊的存取数据的方式，这个方式使得promise里面可以存储异步调用的结果

```js
function sum(a,b,callback){
  callback()
}

// function 是 callback 的实参
sum(123,456,function(result){
  console.log(result)
})
```

## Promise

### 创建Promise

- promise有其一套特殊的存取数据的方式, 它的创建方式也很特殊

- 创建Promise时，构造函数中需要一个函数作为参数

- Promise构造函数的回调函数会在创建Promise时调用，调用时会有2个参数传递进去

- 这2个参数就是resolve, reject，它们是2个回调函数，通过resolve和reject这2个函数可以向Promise中存储数据,

- <mark>resolve和reject这2个函数都可以存储数据</mark>：
  
  - resolve在执行正常时存储数据，
  
  - reject在执行错误时存储数据
  
  - 根据代码执行的情况，选择resolve或reject存储数据

- 通过函数来向Promise中添加数据，好处就是可以用来添加异步调用的数据

- 从Promise中读取数据：
  
  - <mark>可以通过Promise的实例方法then()来读取Promise中存储的数据</mark>
  
  - then也需要2个回调函数作为参数，通过这2个回调函数来获取Promise中的数据
    
    - 通过resolve存储的数据会调用then的第1个函数返回数据，可以在第1个函数中编写处理数据的代码
    
    - 通过reject存储的数据或者出现异常时，会调用then的第2个函数返回数据，可以在第2个函数中编写处理异常的代码
    
    - **注意then里的2个回调函数和promise构造函数里的resolve和reject这2个函数不一样，不是一回事！**
      
      - resolve和reject这2个函数不是我们创建的，是Promise创建的，用来存储数据的函数
      
      - then里的2个函数是我们创建的，用来读取数据的

```js
// resolve, reject 是 promise传递给回调函数的，是promise创建的
const promise = new Promise((resolve, reject)=>{
    resolve("哈哈")    
})

// result, reason 是我们创建的，用来读取存储在 promise 中的数据
promise.then((result) =>{
  console.log("promise中的数据",result)
},(reason)=>{
  console.log("数据",reason)
})
```

- **Promise中维护了2个隐藏属性：PromiseResult、PromiseState**
  
  - **PromiseResult:** 
    
    - 用来存储数据，是真正用来存储数据的属性
    
    - 无论是通过resolve还是通过reject存储的数据，最终都在PromiseResult里面
  
  - **PromiseState:** 
    
    - 用来记录Promise的状态，有3种状态
      
      - pending  进行中，无论是正确的数据还是错误的数据都还没存储进去
      
      - fulfilled  完成，通过resolve存储数据时的状态
      
      - rejected  拒绝， 出错了，通过reject存储数据或出错时的状态
    
    - <mark>state只能修改一次，修改以后永远不会再变</mark>

- **流程(Promise的原理)：**
  
  - 当Promise创建时，PromiseState的初始值为pending
  
  - 当通过resolve存储数据时，PromiseState 变为 fullfilled(完成)， PromiseResult变为存储的数据
  
  - 当通过reject存储数据时或出错时，PromiseState 变为 rejected(拒绝，出错了)， PromiseResult变为存储的数据 或 异常对象
  
  - 当我们通过then读取数据时，相当于为Promise设置了2个回调函数：
    
    - 如果PromiseState变为fulfilled，则调用then的第1个回调函数来返回数据
    
    - 如果PromiseState变为rejected，则调用then的第2个回调函数来返回数据
    
    - 也就是then会根据PromiseState的不同状态去调用不同的函数来读取数据

- **catch()**
  
  - catch()用法和then类似，但是catch只需要一个回调函数作为参数
  
  - <mark>catch()中的回调函数只会在Promise被拒绝时才会调用</mark>
  
  - catch()相当于then(null, reason=>{ } )
  
  - catch() 就是一个<mark>专门处理Promise异常</mark>的方法

- **finally()**
  
  - 无论是正常存储数据还是出现异常了，finally总会执行
  
  - 但是finally的回调函数中不会接收到数据，无论是成功的数据还是失败的数据都接收不到
  
  - finally()通常用来编写一些无论成功与否都会执行的代码

[目录](README)
