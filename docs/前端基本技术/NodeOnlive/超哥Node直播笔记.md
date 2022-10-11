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
  setTimeout(()=>{
    cb(a + b) // a+b的结果作为回调函数的参数进行传递
   },1000)
}
console.log("1111111") // 同步

// 异步
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

[目录](README)
