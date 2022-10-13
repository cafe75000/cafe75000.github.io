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

### node.js 和 JavaScript有什么区别？

- node和JS的标准是一样的，遵循的都是ECMAScript

- DOM BOM 是浏览器独有的，node没有DOM BOM

### 什么是Node.js?

- 在 Node.js 之前，JavaScript 只能运行在浏览器中，作为网页脚本使用，为网页添加一些特效，或者和服务器进行通信

- 有了 Node.js 以后，JavaScript 就可以脱离浏览器，像其它编程语言一样直接在计算机上使用，想干什么就干什么，再也不受浏览器的限制了.

- Node.js 不是一门新的编程语言，也不是一个 JavaScript 框架，它是一套 JavaScript 运行环境，用来支持 JavaScript 代码的执行. 用编程术语来讲，Node.js 是一个 JavaScript 运行时（Runtime）

- **什么是运行时？**
  
  - 所谓运行时，就是程序在运行期间需要依赖的一系列组件或者工具；把这些工具和组件打包在一起提供给程序员，程序员就能运行自己编写的代码了
  
  - 对于 JavaScript 来说，它在运行期间需要依赖以下组件：
    
    - 解释器：JavaScript 是一种脚本语言，需要一边解释一边运行，用到哪些源代码就编译哪些源代码，整个过程由解释器完成。没有解释器的话，JavaScript 只是一堆纯文本文件，不能被计算机识别
      
      V8 引擎就是 JavaScript 解释器，它负责解析和执行 JavaScript 代码
    
    - 标准库：在 JavaScript 代码中会调用一些内置函数，这些函数不是我们自己编写的，而是标准库自带的
    
    - 本地模块：就是已经被提前编译好的模块，它们是二进制文件，和可执行文件在内部结构上没有什么区别，只是不能单独运行而已.
      
      JavaScript 的很多功能都需要本地模块的支持，比如：cookie、ajax 等. JavaScript 解释器需要本地模块的支持，标准库在编写时也会调用本地模块的接口，而我们编写的 JavaScript 代码一般不会直接使用本地模块，所以 Web 前端程序员触及不到它们.
      
      本地模块是幕后英雄，它不显山露水，但是又不可或缺.
  
  - 解释器、标准库、本地模块等各种组件/工具共同支撑了 JavaScript 代码的运行，它们统称为 JavaScript 运行时

- **Node.js的诞生**
  
  -  谷歌公司在 Chrome 浏览器中集成了一种名为“V8”的 JavaScript 引擎（也即 JavaScript 解释器），它能够非常快速地解析和执行 JavaScript 代码
  
  - V8 引擎的强大，以及当年 JavaScript 的火爆，使得一名叫 Ryan Dahl 的程序员动起了“歪心思”，他希望在浏览器之外再为 JavaScript 构建一个运行时，让 JavaScript 能够直接在计算机上运行，这样 JavaScript 就能像 Python、Ruby、PHP 等其它脚本语言一样大展宏图，不必再受限于浏览器，只能做一些小事情.
    
    Ryan Dahl 和他的团队真的做到了，并且做得很好，他们将这套独立的 JavaScript 运行时命名为 Node.js

- Node.js 几乎完全抛弃了浏览器，自己从头构建了一套全新的 JavaScript 运行时.  它让 JavaScript 脱离了浏览器环境，可以直接在计算机上运行，极大地拓展了 JavaScript 用途。我们应该将 JavaScript 和 Python、Java、Ruby 等其它编程语言同等对待. 

简单的说 Node.js 就是运行在服务端的 JavaScript. Node.js 是一个基于 Chrome JavaScript 运行时建立的一个平台. 

Node.js 是一个事件驱动 I/O 服务端 JavaScript 环境，基于 Google 的 V8 引擎，V8 引擎执行 Javascript 的速度非常快，性能非常好. 

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

参考  https://www.lilichao.com/index.php/2022/10/10/%e5%bc%82%e6%ad%a5%e7%bc%96%e7%a8%8b/

Promise 就是一个用来存储数据的对象，但是由于它存取的方式的特殊，可以直接将异步调用的结果存储到Promise中.

**Promise 是解决异步的回调地狱问题的方案**

### 创建Promise

- promise有其一套特殊的存取数据的方式, 它的创建方式也很特殊

- 创建Promise时，构造函数中需要一个函数作为参数

- Promise构造函数的回调函数会在创建Promise时调用，调用时会有2个参数传递进去

- 这2个参数就是resolve, reject，它们是2个回调函数，通过resolve和reject这2个函数可以向Promise中存储数据,

- <mark>resolve和reject这2个函数都可以存储数据</mark>：
  
  - resolve在执行正常时存储数据，存储的是成功的数据
  
  - reject在执行错误时存储数据，存储的是失败的数据
  
  - 根据代码执行的情况，选择resolve或reject存储数据

- 通过函数来向Promise中添加数据，好处就是可以用来添加异步调用的数据

- 从Promise中读取数据：
  
  - <mark>可以通过Promise的实例方法then()来读取Promise中存储的数据</mark>
  
  - then也需要2个回调函数作为参数，通过这2个回调函数来获取Promise中的数据
    
    - 通过resolve存储的数据会调用then的第1个函数返回数据，可以在第1个函数中编写处理数据的代码
    
    - 通过reject存储的数据或者出现异常时，会调用then的第2个函数返回数据，可以在第2个函数中编写处理异常的代码
    
    - **注意then里的2个回调函数和promise构造函数里的resolve和reject这2个函数不一样，不是一回事！**
      
      - resolve和reject这2个函数不是我们创建的，是Promise内部创建的，用来存储数据的函数
      
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

## Promise 的链式调用解决回调地狱

```js
function sum(a,b){
  return new Promise((resolve, reject)=>{
    setTimeout(()=>{
      resolve(a+b)
    },1000)
  })
}

// 回调地狱
 sum(123,456).then(result=>{
    sum(result, 7).then(result =>{
         sum(result, 8).then(result => {
             console.log(result)
         })
     })
 })

// 链式调用解决回调地狱
sum(123, 456)
     .then(result => result + 7)
     .then(result => result + 8)
     .then(result => console.log(result))
```

- Promise 中的 <mark>then, catch, finally 这3个方法都会返回一个新的Promise</mark> 
  
  ```js
  return new Promise()
  ```

- Promise中会存储回调函数的返回值，return新Promise是为了拿到数据

- **注意：finally的返回值，不会存储到新的Promise中**

- 对Promise进行链式调用时，后边的方法(即 then and catch) 读取的是上一步的执行结果，如果上一步的执行结果不是当前想要的结果，则直接跳过当前的方法

- 当Promise出现异常时，而整个调用链中没有出现catch，则异常会向外抛出

- catch自身有异常或错误时，它的错误由后续的catch代码解决, 因此catch应该写在最后，统一处理所有的错误

```js
const promise = new Promise((resolve, reject)=>{
    resolve("第一步执行结果")
})

const promise2 = promise.then(result => {
    console.log("收到结果：", result)
    return "第二步执行结果" // 会作为新的结果存储到新Promise中
})

const promise3 = promise2.then(result => {
    console.log("收到结果：", result)
    return "第三步执行结果" // 会作为新的结果存储到新Promise中
})
```

```js
// 简化一些可以这样写
const promise = new Promise((resolve, reject)=>{
    resolve("第一步执行结果")
})

promise
    .then(result => {
        console.log("收到结果：", result)
        return "第二步执行结果" // 会作为新的结果存储到新Promise中
      })
    .then(result => {
        console.log("收到结果：", result)
        return "第三步执行结果" // 会作为新的结果存储到新Promise中
      })
```

## Promise的静态方法

参考 https://www.lilichao.com/index.php/2022/10/10/%e5%bc%82%e6%ad%a5%e7%bc%96%e7%a8%8b/

Promise的静态方法直接通过Promise类去调用，这些方法可以帮助我们完成一些更加复杂的异步操作. 

静态方法：

- Promise.reject() 创建一个立即拒绝的Promise

- Promise.all([...]) 同时返回多个Promise的执行结果，其中有一个报错，就返回错误

- Promise.allSettled([...]) 同时返回多个Promise的执行结果(无论成功或失败)
  
  - 成功：{status: 'fulfilled', value: result}
  
  - 失败：{status: 'rejected', reason: error}

- Promise.race([...]) 返回执行最快的Promise(不考虑对错), 而忽略其他未执行完的Promise

- Promise.any([...]) 返回执行第1个最快完成的Promise，如果所有的Promise都失败才会返回一个错误信息

- Promise.resolve  用来创建一个新的Promise实例，且直接通过resolve存入一个数据

- Promise.reject  用来创建一个新的Promise实例，且直接通过reject存入一个数据

```js
function sum(a, b) {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            resolve(a + b)
        }, 5000);
    })
}

Promise.all([sum(1, 1), sum(2, 2), sum(3, 3)])
    .then((result) => {
        console.log(result)
    })
```

[目录](README)
