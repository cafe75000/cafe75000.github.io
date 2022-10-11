[目录](README)

# JavaScript 模块化

# 模块化入门

## 1. 理解什么是模块

1. 将一个复杂的程序依据一定的规则<font color="red">**拆**</font>分成单个文件，并最终组<font color="red">**合**</font>在一起
2. 这些拆分的文件就是模块，模块内部数据是私有的，只是向外暴露一些方法与外部其他模块通信

## 2. 为什么要模块化？

1. 降低复杂度
2. 避免命名冲突
3. 更好的分离，按需加载
4. 更高复用性，高可维护性

## 3. 模块化概念带来的问题

1. 请求过多，每写一个 script 标签就会发出一次请求，导致请求过多
2. 依赖模糊，比如模块的引入顺序该把谁放前面，谁放后面
3. 难以维护，模块太多会不好维护

# 模块化规范

前言：一个大的项目必定会使用模块化技术，使用模块化就会使用响应的模块化规范，现在比较流行的模块化规范有以下 2 种：

- **CommonJs : 服务器端, 即 Node 环境下和浏览器端都可以用**
- **ES6: 只能用在浏览器端**

## 1. CommonJS

##### 1.1 CommonJS 的规范

a. 官网：http://wiki.commonjs.org/wiki/Modules --> 参考性不大，只是概念

b. 每个文件都是一个模块

c. CommonJS 模块化的代码既可以在服务端运行，也可以在浏览器端运行，

也就是说 CommonJS 既可以写服务器端的代码(Node), 也可以写浏览器端的代码(browser)

d. **服务器端：模块化的代码可直接运行**

e. **浏览器端：模块化的代码要经过 Browserify 编译 (http://browserify.org)**

**在浏览器环境下运行，需要以下操作：**

- 全局安装 Browserify

```js
npm install browserify -g
```

- 编译指定文件, 例如编译 a.js 文件，-o 指 output

```js
browserify a.js -o build.js
```

##### 1.2 CommonJS 的基本语法

a. 暴露模块，即暴露语法：

- 第 1 种方式：**module.exports = value**, value 就是暴露的内容
- 第 2 种方式：**exports.xxx = value**, value 就是暴露的内容, xxx 是它的名字
- module.exports 和 exports 不能混用，若混用了，以 module.exports 为主, exports 则无效. 因此<mark>暴露模块要么用 module.exports, 要么用 exports，不要同时使用它们</mark>.

b. 引入模块，即引入语法:

- **引入第三方模块：require(xxx), xxx 为模块名**
- **引入自定义模块：require(xxx), xxx 为模块文件路径**

c. 备注：在内存中 exports 和 module.exports 指向同一个对象

```js
### module1.js模块里的代码如下：

/*
module1使用module.exports = value 进行暴露，value就是暴露的内容
module.exports和exports不能混用，若混用了，以module.exports为主
*/
//没有暴露的data和msg(被保护了)
const data = 'atguigu'
const msg = 'hello'

module.exports = {
    showData (){
        console.log(data);
    },
    showMsg(){
        console.log(msg);
    }
}

exports.x = 100 //此行代码不起作用。因为上方写了module.exports
```

```js
### module2.js模块里的代码如下：

/*
module2使用exports.xxxxx = value 进行暴露，value就是暴露的内容,xxxxx是他的名字
*/

exports.data  = 'atguigu2'
exports.msg = 'hello2'

exports.sum = function (a,b){
    console.log(a+b);
}

exports.sub = function (a,b){
    console.log(a-b);
}
```

```js
### app.js

// 暴露的本质是module.exports的内容
// 引入的内容是什么，取决于其他文件露的是什么

const m1 = require("./module1"); //引入自定义模块
const m2 = require("./module2"); //引入自定义模块
const uniq = require("uniq");

m1.showData();
m1.showMsg();
console.log(m2.data);
console.log(m2.msg);
m2.sum(1, 2);
m2.sub(3, 4);
const arr = [1, 3, 3, 4, 2, 5];
console.log(uniq(arr));
```

## 2. ES6 模块化

##### 1. 什么是 ES6 模块化规范

模块化的好处：大家都遵守同样的模块化规范写代码，降低了沟通的成本，极大方便了各个模块之间的相互调用，利人利己

在 ES6 模块化规范诞生之前，JS 社区已经尝试并提出了 AMD、CMD、CommonJS 等模块化规范，但是这些不是官方的规范，只是由社区提出的模块化标准，存在一定的差异性与局限性，并不是浏览器与服务器通用的模块化标准，例如：

- AMD 和 CMD 适用于浏览器端的 JS 模块化

- CommonJS 适用于服务器端的 JS 模块化

太多的模块化规范给开发者增加了学习的难度和开发的成本，因此官方的大一统的 ES6 模块化规范诞生了！

无论是浏览器端还是服务器端都可以使用 ES6 模块化规范.

ES6 模块化规范是浏览器与服务器端通用的模块化开发规范，它的出现降低了学习成本，开发者不需要再额外学习其 AMD、CMD 或 CommonJS 等模块化规范.

##### ES6 模块化规范中的定义：

- **每个 js 文件都是一个独立的模块，<mark>一个 js 文件就是一个模块</mark>**

- **导入其他模块成员使用 import 关键字**

- **向外共享模块成员使用 export 关键字**

##### 2. 在 node.js 中体验 ES6 模块化

**node.js 默认遵循了 CommonJS 的模块化规范**，其中：

- **导入其他模块使用 require()方法**

- **模块对外共享成员使用 module.exports 对象**

node.js 中默认仅支持 CommonJS 模块化规范，如果想基于 node.js 体验与学习 ES6 的模块化语法，可以按照以下 2 个步骤进行配置：

1. 确保电脑里安装了 V14.15.1 或更高版本的 node.js，因为低版本的 node.js 不支持 ES6 语法

2. 在包管理配置文件 package.json 的根节点中添加"type":"module"节点

   ```js
   {
     "type":"module", // 添加到package.json的根节点中
     "name": "0826_modular",
     "version": "1.0.0",
     "description": "",
     "main": "index.js",
     "scripts": {
       "test": "echo \"Error: no test specified\" && exit 1"
     },
     "keywords": [],
     "author": "",
     "license": "ISC",
     "dependencies": {
       "babel-preset-es2015": "^6.24.1",
       "uniq": "^1.0.1"
     }
   }
   ```

##### 3. ES6 模块化的基本语法

**ES6 的模块化主要包含如下 3 种用法：**

1. <font color='red'>**默认导出与默认导入**</font>

   - 默认导出的语法：**export default 导出成员**

   - 默认导入的语法：**import 接收名称 from '模块标识符‘，其中接收名称可以任意命名，模块标识符包裹在引号里面，可以是模块的路径，也可以是模块或包的名字**

     ```js
     *** 默认导出模块 A.js 文件
     let n1 = 10 // 模块A.js的私有成员n1
     let n2 = 20 // 模块A.js的私有成员n2，外界访问不到n2，因为它没有被默认导出
     function show(){} // 模块A.js的私有方法show

     // 用export default默认导出，向外共享了n1和show方法2个成员
     export default{
       n1,
       show
     }

     *** 默认导入模块 A.js 文件向外共享的成员
     import A from './A.js'
     console.log(A) // {n1:10, show:[Function:show]}
     ```

   - **默认导出的注意事项：**

     <font color='red'>每个模块中，只允许使用唯一的一次 export default，否则会报错！</font>

   - **默认导入的注意事项：**

     <font color='red'>默认导入时的接收名称可以是任意名称，只要是合法的成员名称即可, 以数字开头的命名就是非法的</font>

2. <font color='red'>**按需导出与按需导入**</font>

   - 按需导出的语法：**export 按需导出成员**

   - 按需导入的语法: **import {s1} from '模块标识符‘，其中花括号{}里是模块的成员，需要哪个成员，就把哪个成员放在花括号里，需要的 1 个或多个成员，若多个成员，成员之间用逗号隔开，模块标识符包裹在引号里面，可以是模块的路径，也可以是模块或包的名字**

     ```js
     *** 按需导出模块 B.js 文件
     export let s1 = 'aaa' // 向外按需导出变量s1
     export let s2 = 'ccc'// 向外按需导出变量s2
     export function say(){} // 向外按需导出方法say
     export default{ // 向外默认导出一个对象
       a:20
     }

     *** 按需导入模块 B.js的成员
     import {s1,s2,say} from './B.js'
     console.log(s1) // 打印输出 aaa
     console.log(s2) // 打印输出 ccc
     console.log(say) // 打印输出 [Function: say]

     *** 按需导入模块并重命名成员
     import {s1,s2 as str2,say} from './B.js'
     console.log(str2) // 使用重命名后的名称，打印输出 ccc

     *** 按需导入可以和默认导入一起使用
     // 默认导入了info，info指向上面默认导出的对象
     // 按需导入了变量s1,s2，方法say
     import info,{s1,s2 as str2,say} from './B.js'
     console.log(info) // 打印输出{a:20}
     ```

   - **按需导出与按需导入的注意事项：**

     - <font color='red'>每个模块中可以使用**多次**按需导出</font>

     - <font color='red'>按需导入的成员名称**必须和按需导出的名称保持一致**</font>

     - <font color='red'>按需导入时，可以使用 **as 关键字进行重命名**, 模块成员重命名后要使用重新命名的名称</font>

     - <font color='red'>按需导入可以和默认导入一起使用</font>

   - **按需导入和默认导入的语法区别**

     - 按需导入的成员都要**写在花括号里面，并且成员名称要和按需导出的成员名称一样.**

     - 默认导入的成员**不需要写在花括号里面，只需给它一个任意的名称即可**

     - 当按需导入和默认导入同时使用时，按需导入的成员和默认导入的成员之间**用逗号隔开**

3. <font color='red'>**直接导入并执行模块中的代码**</font>

   如果<font color='red'>只想单纯地执行某个模块中的代码</font>,并不需要得到模块中向外共享的成员，此时，可以直接导入并执行模块代码，导入时直接写模块的路径即可，示例如下：

   ```js
   *** 当前文件模块是 C.js
   // 在当前模块中执行一个for循环操作
   // 没有向外导出任何成员
   for(let i=0; i<3;i++){
     console.log(i)
   }

   //------------分割线--------------------

   // 直接导入并执行模块代码，不需要得到模块向外共享的成员
   // 不需要import xxx from, 导入模块的路径即可
   import '/.C.js'

   在node环境中执行模块C.js中的代码，只需在终端输入命令：node C.js, 会发现在
   终端打印输出了for循环里i的值，分别是：0 1 2
   ```

   [目录](README)
