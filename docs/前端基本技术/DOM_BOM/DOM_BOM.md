[目录](README)

# DOM - BOM

##### -- 基于 2022 年李立超老师最新 JavaScript 基础视频教程

### 1. document 对象

- document 对象表示的是整个网页

- document 对象的原型链

HTMLDocument -> Document -> Node -> EventTarget -> Object.prototype -> null

- 凡是在原型链上存在的对象的属性和方法都可以通过 Document 去调用

- 部分属性：
  
  - document.documentElement --> html 根元素
  
  - document.head --> head 元素
  
  - document.title --> title 元素
  
  - document.body --> body 元素
  
  - document.links --> 获取页面中所有的超链接

...

### 2. 元素节点

元素节点对象（element）

- 在网页中，每一个标签都是一个元素节点

- 如何获取元素节点对象？
1. 通过 document 对象来<mark>获取</mark>元素节点

2. 通过 document 对象来<mark>创建</mark>元素节点
- 通过 document 来获取已有的元素节点：
  
  - **document.getElementById()** 根据 id 获取一个元素节点对象
  
  - **document.getElementsByClassName()**
    
    - 根据元素的 class 属性值获取一组元素节点对象
    
    - 返回的是一个类数组对象
    
    - 该方法返回的结果是一个实时更新的集合, 也就是说，当网页中新添加元素时，集合也会实时的刷新
  
  - **document.getElementsByTagName()**
    
    - 根据标签名获取一组元素节点对象
    
    - 返回的结果是可以实时更新的集合
    
    - document.getElementsByTagName("\*") 获取页面中所有的元素
  
  - **document.getElementsByName()**
    
    - 根据标签的 name 属性获取一组元素节点对象
    
    - 返回一个实时更新的集合
    
    - 主要用于表单项 form，因为 form 表单控件 input 等有 name 属性
  
  - **document.querySelectorAll()**
    
    - 根据选择器去页面中查询元素
    
    - 会返回一个类数组（不会实时更新）
  
  - **document.querySelector()** 根据选择器去页面中查询第一个符合条件的元素

- 创建一个元素节点:
  
  - **document.createElement()** 根据标签名创建一个元素节点对象

- 通过元素节点对象获取其他节点的方法:
  
  - **element.children** 获取当前元素的子元素，开发中常用
  
  - **element.firstElementChild** 获取当前元素的第一个子元素
  
  - **element.lastElementChild** 获取当前元素的最后一个子元素
  
  - **element.nextElementSibling** 获取当前元素的下一个兄弟元素
  
  - **element.previousElementSibling** 获取当前元素的前一个兄弟元素
  
  - **element.parentNode** 获取当前元素的父节点
  
  - **element.tagName** 获取当前元素的标签名

### 3. 文本节点

在 DOM 中，网页中所有的文本内容都是文本节点对象,可以通过元素来获取其中的文本节点对象，但是我们通常不会这么做

我们可以直接通过元素去修改其中的文本

- 修改文本的三个属性
1. element.textContent 获取或修改元素中的文本内容
   
   - 获取的是标签中的内容，不会考虑 css 样式, 也就是标签里有什么，就获取什么，不管 css 样式

2. element.innerText 获取或修改元素中的文本内容
   
   - innerText 获取内容时，会考虑 css 样式
   
   - 通过 innerText 去读取 CSS 样式，会触发网页的重排（即重新计算 CSS 样式）
   
   - 当字符串中有标签时，会自动对标签进行转义, 只识别文本内容，不能解析标签，同时空格和换行也会去掉, 比如：
     
     ```js
     <li> --> <li>
     ```

3. element.innerHTML 获取或修改元素中的 html 代码
   
   - 可以直接向元素中添加 html 代码, 也就是既识别文本内容，也能够解析标签，同时保留空格和换行
   
   - innerHTML 插入内容时，有被 xss（恶意代码）注入的风险

### 4. 属性节点 (Attr）

- 属性节点在 DOM 中也是一个对象，通常不需要获取对象，而是直接通过元素即可完成对其的各种操作

- 如何操作属性节点：
  
  - 方式一：
    
    - 读取：元素.属性名（注意，class 属性需要使用 className 来读取）
    
    - 读取一个布尔值时，会返回 true 或 false(比如属性 disabled)
    
    - 修改：元素.属性名 = 属性值
  
  - 方式二：
    
    - 读取：元素.getAttribute(属性名)
    
    - 修改：元素.setAttribute(属性名, 属性值)
    
    - 删除：元素.removeAttribute(属性名)

### 5. 事件 （event）

- 事件就是用户和页面之间发生的交互行为, 比如：点击按钮、鼠标移动、双击按钮、敲击键盘、松开按键...

- 可以通过为事件绑定响应函数（即回调函数），来完成和用户之间的交互，我们定义回调函数但不调用，而是当事件发生的时候浏览器自己调用回调函数

- 绑定响应函数的方式：
  
  1. 可以直接在元素的属性中设置
  
  2. 可以通过为元素的指定属性设置回调函数的形式来绑定事件
     
     - 这种方式不能重复绑定，一个事件只能绑定一个响应函数
     
     - 如果再绑定的话，后面绑定的事件回覆盖前面的事件
  
  3. 可以通过元素 addEventListener()方法来绑定事件, 这种方式可以绑定多次，按绑定的顺序依次执行

### 6. 文档的加载

网页是自上向下加载的，如果将 js 代码编写到网页的上边，js 代码在执行时，网页还没有加载完毕，这时会出现无法获取到 DOM 对象的情况, window.onload 事件会在窗口中的内容加载完毕之后才触发, document 的 DOMContentLoaded 事件会在当前文档加载完毕之后触发

如何解决这个问题：

- 方法 1. 将 script 标签编写到 body 标签里面的最后位置

- 方法 2. 将代码编写到 window.onload 的回调函数中

- 方法 3. 将代码编写到 document 对象的 DOMContentLoaded 的回调函数中（执行时机更早）.
  
  DOMContentLoaded 只能通过 document.addEventListener 使用

- 方法 4. 将代码编写到外部的 js 文件中，然后以 defer 的形式进行引入（执行时机更早，早于 DOMContentLoaded）

### 7. 节点的复制

使用 cloneNode() 方法对节点进行复制时，它会复制节点的所有特点包括各种属性

这个方法默认只会复制当前节点，而不会复制节点的子节点，比如里面的文本不会被复制

可以传递一个 true 作为参数，这样该方法也会将元素的子节点一起进行复制

```js
/* 点击按钮后，将id为l1的元素添加list2中 */
const list2 = document.getElementById("list2");
const l1 = document.getElementById("l1");
const btn01 = document.getElementById("btn01");
btn01.onclick = function () {
  const newL1 = l1.cloneNode(true); // 用来对节点进行复制的
  newL1.id = "newL1";
  list2.appendChild(newL1);
};
```

### 8. 读取和修改 CSS 样式

- 读取 CSS 样式可通过方法 getComputedStyle()
  
  - 它会返回一个对象，这个对象中包含了当前元素所有的生效的样式
  
  - 参数：
    
    1. 要获取样式的对象
    
    2. 要获取的伪元素，可选项
  
  - 返回值：
    
    - 返回的一个对象，对象中存储了当前元素的样式
    
    - 获取的是只读性质的，不能修改值
  
  - 注意：
    
    - 样式对象中返回的样式值，不一定能来拿来直接计算
    
    - 所以使用时，一定要确保值是可以计算的才去计算

- 其他读取 CSS 样式的方法
  
  **元素.clientHeight / 元素.clientWidth**
  
  - 获取元素内部的宽度和高度（包括内容区 content 和内边距 padding）
  
  - 只读
  
  **元素.offsetHeight / 元素.offsetWidth**
  
  - 获取元素的可见框的大小（包括内容区 content、内边距 padding 和边框 border）
  
  - 只读
  
  **元素.scrollHeight / 元素.scrollWidth**
  
  - 获取元素滚动区域的大小
  
  - 只读
  
  **元素.offsetParent**
  
  - 获取元素的定位父元素
  
  - 定位父元素：离当前元素最近的开启了定位的祖先元素，
  
  如果所有的元素都没有开启定位则返回 body
  
  - 只读
  
  **元素.offsetTop / 元素.offsetLeft**
  
  - 获取元素相对于其定位父元素的偏移量
  
  - 只读
  
  **元素.scrollTop / 元素.scrollLeft**
  
  - 获取或设置元素滚动条的偏移量
  
  - 可读可改写

- 修改 CSS 样式
  
  - 修改样式的方式：元素.style.样式名 = 样式值
  
  - 如果样式名中含有符号-，则需要将样式表修改为驼峰命名法
    
    例如：background-color --> backgroundColor

- 其他修改 CSS 样式的方法
  
  - 除了可以通过 元素.style.样式名 = 样式值 的方式直接修改样式外，也可以通过修改 class 属性来间接的修改样式，通过 class 修改样式的好处：
    
    1. 可以一次性修改多个样式
    
    2. 对 JS 和 CSS 进行解耦
  
  ```js
  const btn = document.getElementById("btn");
  const box1 = document.querySelector(".box1");
  btn.onclick = function () {
    box1.className += " box2";
  };
  ```
  
  - 元素.classList 是一个对象，对象中提供了对当前元素的类的各种操作方法:
    
    1. **元素.classList.add()** 向元素中添加一个或多个 class
    
    2. **元素.classList.remove()** 移除元素中的一个或多个 class
    
    3. **元素.classList.toggle()** 切换元素中的 class
    
    4. **元素.classList.replace()** 替换 class
    
    5. **元素.classList.contains()** 检查 class

```js
const btn = document.getElementById("btn");
const box1 = document.querySelector(".box1");

btn.onclick = function () {
  let result = box1.classList.contains("box3");
  console.log(result);
};
```

### 9. 事件对象

- 事件对象是由浏览器在事件触发时所创建的对象， 在这个对象中封装了事件相关的各种信息

- 通过事件对象可以获取到事件的详细信息, 比如：鼠标的坐标、键盘的按键..

- 浏览器在创建事件对象后，会将事件对象作为响应函数的参数进行传递，所以我们可以在事件的回调函数中定义一个形参来接收事件对象

```js
const box1 = document.getElementById("box1");
box1.addEventListener("mousemove", (event) => {
  console.log(event.clientX, event.clientY); // 得到鼠标移动时的坐标值
  box1.textContent = event.clientX + "," + event.clientY;
});
```

- 在 DOM 中存在着多种不同类型的事件对象, 多种事件对象有一个共同的祖先就是 Event
  
  - event.target 触发事件的对象
    
    - 在事件的响应函数中：event.target 表示的是触发事件的对象
    
    - this 绑定事件的对象，谁绑定事件，谁就是 this
  
  - event.currentTarget 绑定事件的对象（等同 this）
  
  - event.stopPropagation() 停止事件的传导，可以用来取消冒泡
  
  - event.preventDefault() 取消默认行为

### 10. 事件的冒泡

事件的冒泡就是指事件的向上传导

- 当元素上的某个事件被触发后，其祖先元素上的相同事件也会同时被触发

- 事件的冒泡是默认的，和绑定事件无关，绑不绑定事件都会有事件的冒泡

- 冒泡的存在大大的简化了代码的编写，大部分情况需要冒泡，但是在一些场景下我们并不希望冒泡存在，不希望事件冒泡时，可以通过事件对象来取消冒泡

- <mark>事件的冒泡和元素的样式无关，只和结构相关</mark>

```js
<body>
    <div id="box1"></div>

    <div id="box2"></div>

    <div id="box3" onclick="alert(3)">
        <div id="box4" onclick="alert(4)"></div>
    </div>

    <script>
        /*
            使小绿球可以跟随鼠标一起移动
            事件的冒泡和元素的样式无关，只和结构相关
        */

        const box1 = document.getElementById("box1")
        const box2 = document.getElementById("box2")

        document.addEventListener("mousemove", (event) => {
            box1.style.left = event.x + "px"
            box1.style.top = event.y + "px"
        })

        box2.addEventListener("mousemove", event => {
            event.stopPropagation()
        })
    </script>
```

### 11. 事件的委派

**委派就是将本该绑定给多个元素的事件，统一绑定给父元素或祖先元素**，

**一般绑定给 document,有时会绑定给 ul，这样可以降低代码复杂度方便维护**

```js
<body>
    <button id="btn">点我一下</button>

    <hr />

    <ul id="list">
        <li><a href="javascript:;">链接一</a></li>
        <li><a href="javascript:;">链接二</a></li>
        <li><a href="javascript:;">链接三</a></li>
        <li><a href="javascript:;">链接四</a></li>
    </ul>

    <script>
        /*
            我一个希望：
                只绑定一次事件，就可以让所有的超链接，
                    包括当前的和未来新建的超链接都具有这些事件

            思路：
                可以将事件统一绑定给document，这样点击超链接时由于事件的冒泡，
                    会导致document上的点击事件被触发，这样只绑定一次，
                        所有的超链接都会具有这些事件

            委派就是将本该绑定给多个元素的事件，统一绑定给父元素或祖先元素，
                一般绑定给document,有时会绑定给ul，这样可以降低代码复杂度方便维护
        */

        const list = document.getElementById("list")
        const btn = document.getElementById("btn")

        // 获取list中的所有链接
        const links = list.getElementsByTagName("a")


        document.addEventListener("click", (event) => {
            // 在执行代码前，先来判断一下事件是由谁触发
            // 检查event.target 是否在 links 中存在

            // 通过静态方法 Array.from()把类数组links转化为真正的数组
            // console.log(Array.from(links))

            // 也可以通过[...links]把类数组links转化为真正的数组
            // 通过includes()方法检查event.target 是否在 links 中存在
            if ([...links].includes(event.target)) {
                alert(event.target.textContent)
            }
        })

        // 点击按钮后，在ul中添加一个新的li
        btn.addEventListener("click", () => {
            list.insertAdjacentHTML(
                "beforeend",
                "<li><a href='javascript:;'>新超链接</a></li>"
            )
        })
    </script>
```

### 12. 事件的捕获

事件的传播机制：

- 在 DOM 中，事件的传播可以分为三个阶段：
  
  1. 捕获阶段：由祖先元素向目标元素进行事件的捕获（注意：默认情况下，事件不会在捕获阶段触发）
  
  2. 目标阶段：触发事件的对象
  
  3. 冒泡阶段：由目标元素向祖先元素进行事件的冒泡

- 事件的捕获，指事件从外向内的传导，当前元素触发事件以后，会先从当前元素最大的祖先元素开始向当前元素进行事件的捕获

- 如果希望在捕获阶段触发事件，可以将 addEventListener 的第三个参数设置为 true，一般情况下我们不希望事件在捕获阶段触发，所有通常都不需要设置第三个参数

```js
const box1 = document.getElementById("box1");
const box2 = document.getElementById("box2");
const box3 = document.getElementById("box3");

box1.addEventListener("click", (event) => {
  // eventPhase 表示事件触发的阶段，开发中不用，但学习阶段可用来查看事件触发的阶段
  alert("1" + event.eventPhase);
  // 返回数字1表示是捕获阶段 返回数字2表示是目标阶段 返回数字3表示是冒泡阶段
});

box2.addEventListener("click", (event) => {
  alert("2" + event.eventPhase);
});

box3.addEventListener("click", (event) => {
  alert("3" + event.eventPhase);
});
```

### 13. BOM 浏览器对象模型

- BOM 为我们提供了一组对象，通过这组对象可以完成对浏览器的各种操作

- BOM 对象：
  
  - Window —— 代表浏览器窗口（全局对象）
  
  - Location —— 浏览器的地址栏信息
    
    - 可以直接将 location 的值修改为一个新的地址，这样会使得网页发生跳
    
    - location.assign() 跳转到一个新的地址
    
    - location.replace() 跳转到一个新的地址（因为是替换跳转，无法通过回退按钮回退）
    
    - location.reload() 刷新页面，可以传递一个 true 来强制清缓存刷新
    
    - location.href 获取当前页面地址
  
  - History —— 浏览器的历史记录（控制浏览器前进后退）
    
    - history.length: 历史记录的数量，访问了几个网址，就有几条记
    
    - history.back(): 回退按钮
    
    - history.forward(): 前进按钮
    
    - history.go()
    
    - 可以向前跳转也可以向后跳转
    
    - 正值往前跳，负值往后跳，且可以指定跳转的数量
  
  - Screen —— 屏幕的信息
  
  - Navigator —— 浏览器的对象（可以用来识别浏览器，是 chrome,IE 还是 firefox）

userAgent 返回一个用来描述浏览器信息的字符串,可通过 userAgent 对浏览器进行判断，看看用户使用的是哪个浏览器（chrome,firefox 等）

但现在在开发中不常用这种手动的判断来识别浏览器，因为有更强大的打包工具， 比如 webpack，在打包的时候可自动对代码进行处理，使得代码可以兼容不同的浏览器

- BOM 对象都是作为 window 对象的属性保存的，所以可以直接在 JS 中访问这些对象

### 14. 定时器

通过定时器，可以使代码在指定的时间后执行，设置定时器的方式有两种：

1. **setTimeout()** 到了指定的时间只会执行一次
   
   - 有 2 个参数：
     
     - 回调函数（要执行的代码）
     
     - 间隔的时间（毫秒）
   
   - 关闭定时器 clearTimeout()

2. **setInterval()** 每隔一段时间代码就会执行一次，会反复执行
   
   - 有 2 个参数：
     
     - 回调函数（要执行的代码）
     
     - 间隔的时间（毫秒）
   
   - 关闭定时器 clearInterval()

定时器的本质，就是在指定时间后将函数添加到消息队列中，并不是到达指定时间后立即执行函数

setInterval() 每隔一段时间就将函数添加到消息队列中，但是如果函数执行的速度比较慢，它无法确保每次执行的间隔都是一样的

解决：那就不能使用 setInterval()，而要使用 setTimeout()，在 setTimeout()里面再设置一个 setTimeout()，模拟成 setInterval()

开发中使用更多的是 setTimeout()，可以保证有相同的间隔时间

### 15. 事件循环（event loop）

函数在每次执行时，都会产生一个执行环境

- 执行环境负责存储函数执行时产生的一切数据

- 问题：函数的执行环境要存储到哪里呢？

- 函数的执行环境存储到了一个叫做调用栈的地方

- 栈，是一种数据结构，特点 后进先出

- 队列，也是一种数据结构，特点 先进先出

调用栈（call stack）

- 调用栈负责存储函数的执行环境

- 当一个函数被调用时，它的执行环境会作为一个栈帧. 插入到调用栈的栈顶，函数执行完毕,其栈帧会自动从栈中弹出

消息队列

- 消息队列负责存储将要执行的函数

- 当我们触发一个事件时，其响应函数并不是直接就添加到调用栈中的, 因为调用栈中有可能会存在一些还没有执行完的代码

- 事件触发后，JS 引擎是将事件响应函数插入到消息队列中排队
  
  

![eventloop](C:\Users\lei\Desktop\cafe75000.github.io\docs\前端基本技术\DOM_BOM\eventLoop.gif)

[目录](README)
