[目录](README)

# JavaScript

##### -- 基于 Bibili 2022 年李立超老师最新 JavaScript 基础视频教程

![one image for JS](../Allimages/JSchaoge.png)

### 1. JS 的编写位置

```js
 <!-- 1.可以将js编写到网页内部的script标签 -->
        <script>
            alert("哈哈！")
        </script> -->

  <!-- 2.可以将js编写外部的js文件中，然后通过script标签进行引入 -->
        <script src="./script/script.js"></script>

 <!-- 3.可以将js代码编写到指定属性中 -->
        <button onclick="alert('你点我干嘛！')">点我一下</button>
```

### 2. 标识符

在 JS 中, 所有可以由我们自主命名的内容，都可以认为是一个标识符, 像 变量名 函数名 类名...

使用标识符需要遵循如下的命名规范：

1. 标识符只能含有字母、数字、下划线、$，且不能以数字开头

2. 标识符不能是 JS 中的关键字和保留字，也不建议使用内置的函数或类名作为变量名

3. 命名规范：
- 通常会使用驼峰命名法
  
  - 首字母小写，每个单词开头大写
  
  - maxlength --> maxLength
  
  - borderleftwidth --> borderLeftWidth

- 类名会使用大驼峰命名法
  
  - 首字母大写，每个单词开头大写
  
  - maxlength --> MaxLength

- 常量的字母会全部大写
  
  - MAX_LENGTH

### 3. 数值 (Number)

- 在 JS 中所有的整数和浮点数都是 Number 类型
  
  - JS 中的数值并不是无限大的，当数值超过一定范围后会显示近似值
  
  - Infinity 是一个特殊的数值表示无穷
  
  - 所以在 JS 中进行一些精度比较高的运算时要十分注意
  
  - NaN 也是一个特殊的数值，表示非法的数值

- 大整数（BigInt）
  
  - 大整数用来表示一些比较大的整数
  
  - 大整数使用 n 结尾，它可以表示的数字范围是无限大
  
  ```js
  a = 99999999999999999999999999999999999999999999999999n;
  ```

### 4. 类型检查

typeof 运算符

- typeof 用来检查不同的值的类型

- 它会根据不同的值返回不同的结果

- 返回的是数据类型，但返回值是字符串的形式

```js
let a = 10;
let b = 10n;
console.log(typeof a); // "number"
console.log(typeof b); // "bigint"
```

### 5. 字符串（String）

- 在 JS 中使用单引号或双引号来表示字符串

- 转义字符 \
  
  - \" --> "
  
  - \' --> '
  
  - \\\ --> \\\
  
  - \t --> 制表符
  
  - \n --> 换行

- 模板字符串
  
  - 使用反单引号` 来表示模板字符串
  
  - 模板字符串中可以嵌入变量

- 使用 typeof 检查一个字符串时会返回 "string"

### 6. 其他数据类型

**布尔值（Boolean）**

- 布尔值主要用来进行逻辑判断

- 布尔值只有两个 true 和 false

- 使用 typeof 检查一个布尔值时会返回 "boolean"

**空值 （Null）**

- 空值用来表示空对象

- 空值只有一个 null

- 使用 typeof 检查一个空值时会返回"object" (JS 历史原因，是个 BUG)

- 使用 typeof 无法检查 null, 检查不出来，返回的是"object"

**未定义（Undefined）**

- 当声明一个变量而没有赋值时，它的值就是 Undefined

- Undefined 类型的值只有一个就是 undefined

- 使用 typeof 检查一个 Undefined 类型的值时，会返回 "undefined"

**符号（Symbol）**

- 用来创建一个唯一的标识

- 使用 typeof 检查符号时会返回 "symbol"

**JS 中原始值一共有七种**

1.Number

2.BigInt

3.String

4.Boolean

5.Null

6.Undefined

7.Symbol

七种原始值是构成各种数据的基石

**原始值在 JS 中是不可变类型，一旦创建就不能修改**

### 7. 类型转换-字符串

类型转换指将一种数据类型转换为其他类型，将其他类型转换为字符串、数值和布尔值

转换为字符串

1.调用 toString()方法将其他类型转换为字符串

- 调用 xxx 的 yyy 方法 --> xxx.yyy()

- 由于 null 和 undefined 中没有 toString()，所以对这两个东西调用 toString()时会报错
  
  2.调用 String()函数将其他类型转换为字符串

- 调用 xxx 函数 --> xxx()

- 原理：

对于拥有 toString()方法的值调用 String()函数时，实际上就是在调用 toString()方法

对于 null，则直接转换为"null"

对于 undefined，直接转换为"undefined"

```js
let a = 10;
a = a.toString(); // "10"

let b = 33;
b = String(b);
```

### 8. 算术运算符

JS 是一门弱类型语言，当进行运算时会通过自动的类型转换来完成运算.

- 运算符可以用来对一个或多个操作数（值）进行运算

- 算术运算符：
  
  - 加法运算符
  
  - 减法运算符
  
  - \* 乘法运算符
  
  - / 除法运算符
  
  - \*\* 幂运算
  
  - % 模运算，两个数相除取余数

- 注意：
  
  - 算术运算时，除了字符串的加法，其他运算的操作数是非数值时，都会转换为数值然后再运算

```js
let a = 1 + 1;
a = 10 / 0; // Infinity

a = 10 - "5"; // 10 - 5
a = 10 + true; // 10 + 1
a = 5 + null; // 5 + 0
a = 6 - undefined; // 6 - NaN
```

当任意一个值和字符串做加法运算时，它会先将其他值转换为字符串，然后再做拼串的操作

可以利用这一特点来完成类型转换, 可以通过为任意类型 + 一个空串的形式来将其转换为字符串, 其原理和 String()函数相同，但使用起来更加简洁

```js
let a = 1;
a = "hello" + "world";
a = "1" + 2; // "1" + "2"
a = true;
a = a + "";
```

### 9. 赋值运算符

赋值运算符用来将一个值赋值给一个变量

**=**

- 将符号右侧的值赋值给左侧的变量

**??=**

- 空赋值

- 只有当变量的值为 null 或 undefined 时才会对变量进行赋值

**+=**

- a += n 等价于 a = a + n

**-=**

- a -= n 等价于 a = a - n

**\*=**

- a \*= n 等价于 a = a \_ n

**/=**

- a /= n 等价于 a = a / n

**%=**

- a %= n 等价于 a = a % n

**\*\*=**

- a **= n 等价于 a = a ** n

```js
let a = 10;
a = 5; // 将右边的值 赋值 给左边的变量
let b = a; // 一个变量只有在=左边时才是变量，在=右边时它是值

a = 66;
a = a + 11; // 大部分的运算符都不会改变变量的值，赋值运算符除外

a = 5;
a = a + 5; // 10
a += 5; // 在a原来值的基础上增加5

a = null;

a ??= 101;
```

### 10. 一元的 ±

- 正号：不会改变数值的符号
* 负号：可以对数值进行符号位取反

当我们对非数值类型进行正负运算时，会先将其转换为数值然后再运算

### 11. ++ 自增运算符

++ 使用后会使得原来的变量立刻增加 1

- 自增分为前自增(++a)和后自增(a++)

- 无论是++a 还是 a++都会使原变量立刻增加 1

- 不同的是++a 和 a++所返回的值不同

a++ 是自增前的值 旧值

++a 是自增后的值 新值

### 12. -- 自减运算符

- 使用后会使得原来的变量立刻减小 1

- 自减分为前自减(--a)和后自减(a--)

- 无论是--a 还是 a--都会使原变量立刻减少 1

- 不同的是--a 和 a--的值不同

--a 是新值

a-- 是旧值

### 13.  ! 逻辑非

! 逻辑非

- ! 可以用来对一个值进行非运算

- 它可以对一个布尔值进行取反操作

true --> false

false --> true

- 如果对一个非布尔值进行取反，它会先将其转换为布尔值然后再取反，可以利用这个特点将其他类型转换为布尔值

- 类型转换
  
  - 转换为字符串
    
    - 显式转换：String()
    
    - 隐式转换：+ ""
  
  - 转换为数值
    
    - 显式转换：Number()
    
    - 隐式转换：+
  
  - 转换为布尔值
    
    - 显式转换：Boolean()
    
    - 隐式转换：!!

### 14. && 逻辑与

- 可以对两个值进行与运算

- 当&&左右都为 true 时，则返回 true，否则返回 false

- 与运算是短路的与，如果第一个值为 false，则不看第二个值

- 与运算是找 false 的，如果找到 false 则直接返回，没有 false 才会返回 true

- 对于非布尔值进行与运算，它会转换为布尔值然后运算

- 但是最终会返回原值
  
  如果第一个值为 false，则直接返回第一个值

如果第一个值为 true，则返回第二个值

### 15. || 逻辑或

- 可以对两个值进行或运算

- 当||左右有 true 时，则返回 true，否则返回 false

- 或运算也是短路的或，如果第一个值为 true，则不看第二个值

- 或运算是找 true，如果找到 true 则直接返回，没有 true 才会返回 false

- 对于非布尔值或运算，它会转换为布尔值然后运算

- 但是最终会返回原值
  
  如果第一个值为 true，则返回第一个

如果第一个值为 false，则返回第二个

```js
let result = true && true; // true
result = true && false; // false
result = false && true; // false
result = false && false; // false

true && alert(123); // 第一个值为true，alert会执行
false && alert(123); // 第一个值为false，alert不会执行

// true && true  -> true
result = 1 && 2; // 2
// true && false -> false
result = 1 && 0; // 0
// false && false -> false
result = 0 && NaN; // 0

result = true || false; // true
result = false || true; // true
result = true || true; // true
result = false || false; // false

false || alert(123); // 第一个值为false，alert会执行
true || alert(123); // 第一个值为true，alert不会执行

result = 1 || 2; // 1
result = "hello" || NaN; // "hello"
result = NaN || 1; // 1
result = NaN || null; // null
```

### 16. 关系运算符

关系运算符用来检查两个值之间的关系是否成立, 成立返回 true，不成立返回 false

`>` 用来检查左值是否大于右值

`>=` 用来检查左值是否大于或等于右值

< 用来检查左值是否小于右值

<= 用来检查左值是否小于或等于右值

注意：

当对非数值进行关系运算时，它会先将前转换为数值然后再比较

当关系运算符的两端是两个字符串，它不会将字符串转换为数值，

而是逐位的比较字符的 Unicode 编码

利用这个特点可以对字符串按照字母排序

注意比较两个字符串格式的数字时一定要进行类型转换

```js
let result = 10 > 5; // true
result = 5 > 5; // false
result = 5 >= 5; // true

result = 5 < "10"; // true
result = "1" > false; // true

result = "a" < "b"; // true
result = "z" < "f"; // false
result = "abc" < "b"; // true

result = "12" < "2"; // true
result = +"12" < "2"; // false

// 检查num是否在5和10之间
let num = 4;
// result = 5 < num < 10 // 错误的写法
result = num > 5 && num < 10;
```

### 17. 相等运算符

**==**

- 相等运算符，用来比较两个值是否相等

- 使用相等运算符比较两个不同类型的值时，它会将其转换为相同的类型（通常转换为数值）然后再比较, 类型转换后值相同也会返回 true

- null 和 undefined 进行相等比较时会返回 true

- NaN 不和任何值相等，包括它自身

**===**

- 全等运算符，用来比较两个值是否全等

- 它不会进行自动的类型转换，如果两个值的类型不同直接返回 false

- null 和 undefined 进行全等比较时会返回 false

**!=**

- 不等，用来检查两个值是否不相等

- 会自动的进行类型转换

**!==**

- 不全等，比较两个值是否不全等

- 不和自动的类型转换

```js
let result = 1 == 1; // true
result = 1 == 2; // false
result = 1 == "1"; // true
result = true == "1"; // true

result = null == undefined; // true
result = NaN == NaN; // false

result = 1 === "1"; // false
result = null === undefined; // false

result = 1 != 1; // false
result = 1 != "1"; // false
result = 1 !== "1"; // true
```

### 18. 条件运算符

条件表达式 ? 表达式 1 : 表达式 2

执行顺序：条件运算符在执行时，会先对条件表达式进行求值判断，

如果结果为 true，则执行表达式 1

如果结果为 false，则执行表达式 2

```js
false ? alert(1) : alert(2);

let a = 100;
let b = 200;
// a > b ? alert('a大！') : alert("b大！")
let max = a > b ? a : b;
```

### 19. 运算符的优先级

和数学一样，JS 中的运算符也有优先级，比如先乘除和加减

可以通过优先级的表格来查询运算符的优先级:

[https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Operator_Precedence]()

在表格中位置越靠上的优先级越高，优先级越高越先执行，优先级一样自左向右执行

优先级我们不需要记忆，甚至表格都不需要看

因为()拥有最高的优先级，使用运算符时，如果遇到拿不准的，可以直接通过()来改变优先级即可

### 20. 代码块

使用花括号{ } 来创建代码块，代码块可以用来对代码进行分组，

同一个代码中的代码，就是同一组代码，一个代码块中的代码要么都执行要么都不执行

let 和 var

- 在 JS 中，使用 let 声明的变量具有块作用域, 在代码块中声明的变量无法在代码块的外部访问

- 使用 var 声明的变量，不具有块作用域

### 21. if 语句

**流程控制语句可以用来改变程序执行的顺序**

1. 条件判断语句

2. 条件分支语句

3. 循环语句

**if 语句**

- 语法：
  
  ```js
  if(条件表达式){
  
      语句...
  
  }
  ```

- 执行流程

if 语句在执行会先对 if 后的条件表达式进行求值判断，

如果结果为 true，则执行 if 后的语句

如果为 false 则不执行

if 语句只会控制紧随其后其后的那一行代码，如果希望可以控制多行代码，可以使用{}将语句扩起来

最佳实践：即使 if 后只有 1 行代码，我们也应该编写代码块，这样结构会更加的清晰

如果 if 后的添加表达式不是布尔值，会转换为布尔值然后再运算

**if-else 语句**

- 语法：
  
  ```js
  if(条件表达式){
      语句...
  }else{
      语句...
  }
  ```

- 执行流程：

if-else 执行时，先对条件表达式进行求值判断，

如果结果为 true 则执行 if 后的语句

如果结果为 false 则执行 else 后的语句

**if-else if-else 语句：**

- 语法：
  
  ```js
  if(条件表达式){
    语句...
  }else if(条件表达式){
      语句...
  }else if(条件表达式){
      语句...
  }else{
      语句...
  }
  ```

- 执行流程：

if-else if-else 语句，会自上向下依次对 if 后的条件表达式进行求值判断，

如果条件表达式结果为 true，则执行当前 if 后的语句，执行完毕语句结束

如果条件表达式结果为 false，则继续向下判断，直到找到 true 为止

如果所有的条件表达式都是 false，则执行 else 后的语句

**注意**：

if-else if-else 语句中只会有一个代码块被执行，一旦有执行的代码块，下边的条件都不会在继续判断了, 所以一定要注意，条件的编写顺序

### 22. switch 语句

-**语法：**

```js
switch(表达式){
  case 表达式:
    代码...
    break
  case 表达式:
    代码...
    break
  case 表达式:
    代码...
    break
  case 表达式:
    代码...
    break
  default:
    代码...
    break
}
```

- 执行的流程

switch 语句在执行时，会依次将 switch 后的表达式和 case 后的表达式进行全等比较

如果比较结果为 true，则自当前 case 处开始执行代码

如果比较结果为 false，则继续比较其他 case 后的表达式，直到找到 true 为止

如果所有的比较都是 false，则执行 default 后的语句

- 注意：

当比较结果为 true 时，会从当前 case 处开始执行代码

也就是说 case 是代码执行的起始位置

这就意味着只要是当前 case 后的代码，都会执行

可以使用 break 来避免执行其他的 case

- 总结

switch 语句和 if 语句的功能是重复，switch 能做的事 if 也能做，反之亦然。

它们最大的不同在于，switch 在多个全等判断时，结构比较清晰

### 23. 循环语句

通过循环语句可以使指定的代码反复执行

- **JS 中一共有三种循环语句:**
  
  - while 语句
  
  - do-while 语句
  
  - for 语句
1. **while 语句**

```js
while(条件表达式){
    语句...
}
```

- 执行流程：

while 语句在执行时，会先对条件表达式进行判断，

如果结果为 true，则执行循环体，执行完毕，继续判断

如果为 true，则再次执行循环体，执行完毕，继续判断，如此重复

知道条件表达式结果为 false 时，循环结束

**通常编写一个循环，要有三个要件：**

- 1.初始化表达式（初始化变量）

- 2.条件表达式（设置循环运行的条件）

- 3.更新表单式（修改初始化变量）
2. **do-while 循环**

```js
do{
  语句...
}while(条件表达式)
```

- 执行顺序：

do-while 语句在执行时，会先执行 do 后的循环体，

执行完毕后，会对 while 后的条件表达式进行判断

如果为 false，则循环终止

如果为 true，则继续执行循环体，以此类推

- **和 while 的区别**：

while 语句是先判断再执行

do-while 语句是先执行再判断

实质的区别：do-while 语句可以确保循环至少执行一次

3. **for 循环**
- for 循环和 while 没有本质区别，都是用来反复执行代码, 不同点就是语法结构，for 循环更加清晰

- 语法：

```js
for(① 初始化表达式; ② 条件表达式; ④ 更新表达式){
      ③ 语句...
}
```

- 执行流程：

① 执行初始化表达式，初始化变量

② 执行条件表达式，判断循环是否执行（true 执行，false 终止）

③ 判断结果为 true，则执行循环体

④ 执行更新表达式，对初始化变量进行修改

⑤ 重复 ②，知道判断为 false 为止

- 初始化表达式，在循环的整个的生命周期中只会执行 1 次

- for 循环中的三个表达式都可以省略

- 使用 let 在 for 循环的()中声明的变量是局部变量，只能在 for 循环内部访问

使用 var 在 for 循环的()中声明的变量可以在 for 循环的外部访问

- 创建死循环的方式：
  
  ```js
  while (1) {}
  
  for (;;) {}
  ```

\- **嵌套循环**

当循环发生嵌套时，外层循环每执行一次，内层循环就会执行一个完整的周期

-  **break 和 continue**

- break
  
  - break 用来终止 switch 和循环语句
  
  - break 执行后，当前的 switch 或循环会立刻停止
  
  - break 会终止离他最近的循环

- continue
  
  - continue 用来跳过当次循环

### 24. 对象

数据类型：

原始值：就是不可变类型，一旦创建就不能修改

1.数值 Number

2.大整数 BigInt

3.字符串 String

4.布尔值 Boolean

5.空值 Null

6.未定义 Undefined

7.符号 Symbol

对象：就是可变类型

对象是 JS 中的一种复合数据类型，它相当于一个容器，<mark>在对象中可以存储各种不同类型数据</mark>

原始值只能用来表示一些简单的数据，不能表示复杂数据, 比如：现在需要在程序中表示一个人的信息, 通过原始值来存储这个的信息就是：

let name = "孙悟空"

let age = 18

let gender = "男"

用对象来存储更合适，对象可以存储多个各种类型的数据, **对象中存储的数据，我们称为属性**

<mark>向对象中添加属性</mark>：对象.属性名 = 属性值

<mark>读取对象中的属性</mark>：对象.属性名

- 如果读取的是一个对象中没有的属性，不会报错而是返回 undefined

<mark>修改对象中的属性，和添加属性的方式一样</mark>：对象.属性名 = 属性值

- 会覆盖相同的已经存在的属性从而修改了对象的属性

<mark> 删除对象的属性：</mark> delete 对象名.属性名

### 25. 对象的属性

**属性名**

- 通常属性名就是一个字符串，所以属性名可以是任何值，没有什么特殊要求

但是如果你的属性名太特殊了，不能直接使用，需要使用[ ]来设置

虽然如此，但是我们还是强烈建议属性名也按照标识符的规范命名，

比如不能以数字开头等等

- 也可以使用符号（symbol）作为属性名，来添加属性，不通过点语法

而是直接赋值的方式：

obj[mySymbol] = "通过 symbol 添加的属性"

获取这种属性时，也必须使用 symbol 来获取

使用 symbol 添加的属性，通常是那些不希望被外界访问的属性

开发中 symbol 不常用

- 使用[]去操作属性时，可以使用变量

**属性值**

- 对象的属性值可以是任意的数据类型，也可以是一个对象

使用 typeof 检查一个对象时，会返回 object

**in 运算符**

- 用来检查对象中是否含有某个属性

- 语法：属性名 in obj

- 如果有返回 true，没有返回 false

```js
let obj = Object();
obj.name = "孙悟空";
obj.age = 18;
obj["gender"] = "男";

let str = "address";
obj[str] = "花果山"; // 等价于 obj["address"] = "花果山"
obj.str = "哈哈"; // 使用.的形式添加属性时，不能使用变量

let mySymbol = Symbol();
let newSymbol = Symbol();
// 使用symbol作为属性名
obj[mySymbol] = "通过symbol添加的属性";
console.log(obj[mySymbol]);

obj.f = Object();
obj.f.name = "猪八戒";
obj.f.age = 28;
console.log(obj.f.name);
```

### 26. 对象字面量

- 可以直接使用{ } 来创建对象

- 使用{ }所创建的对象，可以直接向对象中添加属性

- 语法：

```js
{
  属性名:属性值,
  [属性名]: 属性值,
}
```

```js
let mySymbol = Symbol();

let obj2 = {
  name: "孙悟空",
  age: 18,
  ["gender"]: "男",
  [mySymbol]: "特殊的属性",
  hello: {
    a: 1,
    b: true,
  },
};
```

### 27. 枚举属性

枚举属性，指将对象中的所有的属性全部获取

**for-in 语句**

- 语法：

```js
for(let propName in 对象){
    语句...
}
```

- for-in 的循环体会执行多次，有几个属性就会执行几次，每次执行时，都会将一个属性名赋值给我们所定义的变量

- 注意：并不是所有的属性都可以枚举，比如 使用符号添加的属性不能枚举

```js
let obj = {
  name: "孙悟空",
  age: 18,
  gender: "男",
  address: "花果山",
  [Symbol()]: "测试的属性", // 符号添加的属性是不能枚举
};

for (let propName in obj) {
  console.log(propName, obj[propName]);
  // 打印输出时不能写成obj.propName,[]里才是变量
  // obj.propName 表示obj里的有个属性propName，
  // 但obj里没有propName属性，写成obj.propName会返回undefined
}
```

### 28. 可变类型

- 原始值都属于不可变类型，一旦创建就无法修改

- 在内存中不会创建重复的原始值

```js
let a = 10;
let b = 10;
a = 12; // 当我们为一个变量重新赋值时，绝对不会影响其他变量
```

- 对象属于可变类型

- 对象创建完成后，可以任意的添加删除修改对象中的属性

- 注意：
  
  - 当对两个对象进行相等或全等比较时，比较的是对象的内存地址
  
  - 如果有两个变量同时指向一个对象，通过一个变量修改对象时，对另外一个变量也会产生影响

**修改对象**

- 修改对象时，如果有其他变量指向该对象, 则所有指向该对象的变量都会受到影响

**修改变量**

- 修改变量时，只会影响当前的变量，即只影响自己，不影响其他人

在使用变量存储对象时，很容易因为改变变量指向的对象，提高代码的复杂度, 所以通常情况下，声明存储对象的变量时会使用 const

**注意**：

const 只是禁止变量被重新赋值，对对象的修改没有任何影响

```js
 `      const obj = {
            name: "孙悟空",
        }
        const obj2 = obj
        obj2.name = "猪八戒" // 修改对象


       const obj3 = {
            name: "猪八戒"
        }
        obj3.name = "沙和尚" // 修改变量
```

### 26. 方法

方法（method）

- 当一个对象的属性指向一个函数，即对象的属性是一个函数

那么我们就称这个函数是该对象的方法

调用函数就称为调用对象的方法

```js
let obj = {};
obj.name = "孙悟空";
obj.age = 18;

// 函数也可以成为一个对象的属性
obj.sayHello = function () {
  alert("hello");
};
```

### 27. 函数

**函数（Function）**

- 函数也是一个对象

- 它具有其他对象所有的功能

- 函数是用来存储代码的，且可以在需要时调用这些代码

**语法**：

```js
function 函数名(){
    语句...
}
```

**调用函数**：

- 调用函数就是执行函数中存储的代码

- 语法：函数对象()

例如：fn()

使用 typeof 检查函数对象时会返回 function

### 28. 函数的创建方式

**函数的定义方式,有 3 种方式**：

1.**函数声明**

```js
function 函数名(){
    语句...
}
```

2.**函数表达式**

    const 变量 = function(){
      语句...
    }

3.**箭头函数**

```js
() => {
  语句...
}
```

箭头函数主要是用来替代函数表达式的，并且它不能用作构造函数

箭头函数中没有 arguments

```js
function fn() {
  console.log("函数声明所定义的函数~");
}

const fn2 = function () {
  console.log("函数表达式");
};

const fn3 = () => {
  console.log("箭头函数");
};

const fn4 = () => console.log("箭头函数");
```

在 JS 中，函数也是一个对象（一等函数，又称 JS 的 "一等公民"）

**一等函数的意思指：别的对象能做的事情，函数也可以**

### 29. 函数的参数

**形式参数**

- 在定义函数时，可以在函数中指定数量不等的形式参数（形参）

- 在函数中定义形参，就相当于在函数内部声明了对应的变量但是没有赋值

**实际参数**

- 在调用函数时，可以在函数的( )里传递数量不等的实参

- 实参会赋值给其对应的形参

- 参数的个数：
  
  1.如果实参和形参数量相同，则对应的实参赋值给对应的形参
  
  2.如果实参多余形参，则多余的实参不会使用
  
  3.如果形参多余实参，则多余的形参为 undefined

- 参数的类型
  
  - JS 中不会检查参数的类型，<mark>可以传递任何类型的值作为参数</mark>

也就是**参数可以是原始值，对象或函数**

如果将函数作为参数传递，那么我们就称这个函数为回调函数（callback）

1.函数声明

```js
function 函数名([参数]){
    语句...
}
```

2.函数表达式

```js
const 变量 = function([参数]){
    语句...
}
```

3.箭头函数

```js
([参数]) => {
    语句...
}
```

- 当箭头函数中只有一个参数时，可以省略圆括号( )
  
  ```js
  const fn = (a, b) => {
    console.log("a =", a);
    console.log("b =", b);
  };
  const fn2 = (a) => {
    console.log("a =", a);
  };
  ```

- 箭头函数定义参数时，可以为参数指定默认值. 默认值会在没有对应实参时生效
  
  ```js
  const fn3 = (a = 10, b = 20, c = 30) => {
    console.log("a =", a);
    console.log("b =", b);
    console.log("c =", c);
  };
  
  fn3(1, 2); // a=1, b=2, c的值是默认值30
  ```

### 30. 函数的返回值

在函数中，可以通过 return 关键字来指定函数的返回值

返回值就是函数的执行结果，函数调用完毕返回值便会作为结果返回

任何值都可以作为返回值使用（包括对象和函数之类）

如果 return 后不跟任何值，则相当于返回 undefined

如果不写 return，那么函数的返回值依然是 undefined

return 一执行函数立即结束

```js
function fn() {
  // return {name:"孙悟空"} // 返回一个对象
  // return ()=>alert(123) // 返回一个函数

  // return

  alert(123);
  return;
  alert(456); // 无效代码
}

let result = fn();
```

箭头函数的返回值可以直接写在箭头后

**如果直接在箭头后设置对象字面量为返回值时，对象字面量必须使用()括起来**

```js
const sum = (a, b) => a + b;

const fn = () => ({ name: "孙悟空" }); // 返回对象字面量，必须使用()包裹对象

let result = sum(123, 456);
result = fn();
```

### 31. 作用域 和 作用域链

<mark>作用域（scope）</mark>

- 作用域指的是一个变量的可见区域

- 作用域有两种：全局和局部

**全局作用域**

- 全局作用域在网页运行时创建，在网页关闭时销毁

- 所有直接编写到 script 标签中的代码都位于全局作用域中

- 全局作用域中的变量是全局变量，可以在任意位置访问

**局部作用域**

- 块作用域

- 块作用域是一种局部作用域

- 块作用域在代码块执行时创建，代码块执行完毕它就销毁

- 在块作用域中声明的变量是局部变量，只能在块内部访问，外部无法访问

**函数作用域**

- 函数作用域也是一种局部作用域

- 函数作用域在函数调用时产生，调用结束后销毁

- 函数每次调用都会产生一个全新的函数作用域

- 在函数中定义的变量是局部变量，只能在函数内部访问，外部无法访问

在开发中应该尽量减少直接在全局作用域中编写代码！所以我们的代码要尽量编写的局部作用域. 如果使用 let 声明的变量，可以使用花括号{ }来创建块作用域

<mark>作用域链</mark>

- 当我们使用一个变量时， JS 解释器会优先在当前作用域中寻找变量，

如果找到了则直接使用

如果没找到，则去上一层作用域中寻找，找到了则使用

如果没找到，则继续去上一层寻找，以此类推

如果一直到全局作用域都没找到，则报错 xxx is not defined

### 32. Window 对象

**<mark>Window 对象</mark>**

- 在浏览器中，浏览器为我们提供了一个 window 对象，可以直接访问

- window 对象代表的是浏览器窗口，通过该对象可以对浏览器窗口进行各种操作

除此之外**window 对象还负责存储 JS 中的内置对象和浏览器的宿主对象**

- window 对象的属性可以通过 window 对象访问，也可以直接访问

- 函数就可以认为是 window 对象的方法

- 向 window 对象中添加的属性会自动成为全局变量，比如：window.a = 10

**<mark>内置对象</mark>**：JS 标准已经定义好的对象，存储在 window 对象中，可以直接使用，

比如：Number(), String()

**<mark>宿主对象</mark>**：由浏览器提供的对象，也存储在 window 对象中，可以直接使用,

比如：document.write(), console.log()

备注：

var 用来声明变量，作用和 let 相同，但是 var 不具有块作用域

- 在全局中使用 var 声明的变量，都会作为 window 对象的属性保存

- 使用 function 声明的函数，都会作为 window 的方法保存

- 使用 let 声明的变量不会存储在 window 对象中，而存在一个秘密的小地方（无法访问）

- var 虽然没有块作用域，但有函数作用域

### 33. 提升

变量的提升

- 使用 var 声明的变量，它会在所有代码执行前被声明, 所以我们可以在变量声明前就访问变量

- **变量的提升毫无意义 😀😀**

函数的提升

- 使用函数声明创建的函数，会在其他代码执行前被创建, 所以我们可以在函数声明前调用函数

- 函数表达式没有函数提升，比如：let fn = function(){ ... } 不存在提升

let 声明的变量实际也会提升，但是在赋值之前解释器禁止对该变量的访问

### 34. 立即执行函数（IIFE）

IIFE: Immediately Invoked Function Expression

- 立即是一个匿名的函数，并它只会调用一次

- 可以利用 IIFE 来创建一个一次性的函数作用域，避免变量冲突的问题

- 如果有多个立即执行函数，函数之间必须加分号;

```js
(function () {
  let a = 10;
  console.log(111);
})();

(function () {
  let a = 20;
  console.log(222);
})();

(function () {
  let a = 10;
  console.log(111);
})();
```

### 35. this

- 函数在执行时，JS 解析器每次都会传递进一个隐含的参数

- 这个参数就叫做 this, 可以直接使用

- this 会指向一个对象

- this 所指向的对象会根据函数调用方式的不同而不同
  
  1.以函数形式调用时，this 指向的是 window
  
  2.以方法的形式调用时，this 指向的是调用方法的对象

...

- 通过 this 可以在方法中引用调用方法的对象

- 箭头函数没有自己的 this，它的 this 由它的外层作用域决定

**注意：箭头函数的 this 和它的调用方式无关**

<mark>**this 的使用场景**</mark>

1. 在 script 标签内 this 代表的是 window 对象

2. 在普通函数中 this 代表的是 window 对象

3. 在方法中 this 代表的是方法的调用者

4. 在构造函数中 this 代表的是实例化的那个对象, 即新建的对象

5. 在事件回调函数中 this 代表的是事件源

6. 通过 call 和 apply 调用的函数中，第一个参数就是函数的 this
   
   - 通过 call 方法调用函数，函数的实参直接在第一个参数后一个一个的列出来
   
   - 通过 apply 方法调用函数，函数的实参需要通过一个数组传递

7. 通过 bind 返回的函数，this 由 bind 第一个参数决定
   
   - bind() 是函数的方法，它的返回值是一个新函数，所以该方法可以用来创建一个新的函数
   
   - bind 可以为新函数绑定 this, 一旦绑定，无法修改 this
   
   - bind 可以为新函数绑定参数, 同样，一旦绑定，无法修改绑定的参数
   
   - 注意，无法修改是针对返回的新函数，原来的函数不受影响

8. 箭头函数没有自己的 this，它的 this 由箭头函数外层作用域决定. 也无法通过 call apply 和 bind 修改箭头函数的 this，因为它本身根本没有 this
   
   箭头函数中也没有 arguments

### 36. 严格模式

JS 运行代码的模式有两种：

- 正常模式
  
  - 默认情况下代码都运行在正常模式中，在正常模式，语法检查并不严格, 它的原则是：能不报错的地方尽量不报错
  
  - 这种处理方式导致代码的运行性能较差

- 严格模式
  
  - 在严格模式下，语法检查变得严格
    
    1.禁止一些语法
    
    2.更容易报错
    
    3.提升了性能
  
  - 在开发中，应该尽量使用严格模式，这样可以将一些隐藏的问题消灭在萌芽阶段，同时也能提升代码的运行性能

```js
"use strict"; // 全局的严格模式

let a = 10;

console.log(a);

function fn() {
  "use strict"; // 函数的严格的模式
}
```

### 37. 类 class

使用 Object 创建对象的问题：

1. 无法区分出不同类型的对象

2. 不方便批量创建对象

在 JS 中可以通过类（class）来解决使用 object 创建对象时的问题：

1. 类是对象模板，可以将对象中的属性和方法直接定义在类中, 定义后，就可以直接通过类来创建对象

2. 通过同一个类创建的对象，我们称为同类对象

可以使用 instanceof 来检查一个对象是否是由某个类创建，返回值是布尔值

如果某个对象是由某个类所创建，则我们称该对象是这个类的实例

语法：

class 类名 {} // 类名要使用大驼峰命名，即首字母大写，推荐

const 类名 = class {}  // 这么写也行，但不推荐

通过类创建对象：new 类()

```js
// Person类专门用来创建人的对象
class Person {}

// Dog类专门用来创建狗的对象
class Dog {}

const p1 = new Person(); // 调用构造函数创建对象
const p2 = new Person();

const d1 = new Dog();
const d2 = new Dog();

console.log(p1 instanceof Person); // true
console.log(d1 instanceof Person); // false
```

类的代码块默认就是严格模式, 类的代码块是用来设置对象的属性的，不是什么代码都能写

- 实例属性只能通过实例访问调用

- 静态属性(也称类属性)只能通过类本身去访问调用

```js
class Person {
  name = "孙悟空"; // Person的实例属性name p1.name
  age = 18; // 实例属性只能通过实例访问 p1.age

  // 使用static声明的属性，是静态属性（也称类属性） Person.test
  static test = "test静态属性";
  // 静态属性只能通过类去访问 Person.hh
  static hh = "静态属性";
}
const p1 = new Person();
const p2 = new Person();
```

### 38. 方法

方法也是对象的一个属性，只不过这个属性的值是一个函数

```js
class Person {
  name = "孙悟空";

  sayHello() {
    console.log("大家好，我是" + this.name);
  } // 添加方法（即实例方法） 实例方法中this就是当前实例，即就是调用方法的对象

  static test() {
    console.log("我是静态方法", this);
  } // 静态方法（类方法） 直接通过类来调用 静态方法中this指向的是当前类
}

const p1 = new Person();

// console.log(p1)

Person.test(); // 调用静态方法

p1.sayHello(); // 调用实例方法
```

### 39. 类的构造函数

在类中可以添加一个特殊的方法 constructor，该方法的名字是固定的，必须叫 constructor，该方法我们称为构造函数（或者叫构造方法）.

构造函数会在我们调用类，创建对象时执行，也就是当使用 new 关键字创建一个对象时，

就是在调用构造函数 constructor()，并且它会自动返回返回实例对象，无需 return 关键字

constructor() 方法是类的构造函数(默认方法)，用于传递参数, 返回实例对象，通过 new 命令生成对象实例时，自动调用该方法。

如果没有显示定义, 类内部会自动给我们创建一个 constructor()

一个类只能拥有一个名为 “constructor”的特殊方法，如果类包含多个 constructor 的方法，则将抛出 一个 SyntaxError 的错

```js
class Person {
  constructor(name, age, gender) {
    // console.log("构造函数执行了~", name, age, gender)
    // 可以在构造函数中，为实例属性进行赋值
    // 在构造函数中，this表示当前所创建的对象
    this.name = name;
    this.age = age;
    this.gender = gender;
  }
}

const p1 = new Person("孙悟空", 18, "男");
const p2 = new Person("猪八戒", 28, "男");
const p3 = new Person("沙和尚", 38, "男");
```

### 40. 封装

面向对象的特点：封装、继承和多态

封装 —— 安全性

继承 —— 扩展性

多态 —— 灵活性

**封装**

- 对象就是一个用来存储不同属性的容器

- 对象不仅负责存储属性，还要负责数据的安全

- 直接添加到对象中的属性，并不安全，因为它们可以被任意的修改

- 如何确保数据的安全：
  
  1.私有化数据
  
  - 将需要保护的数据设置为私有，只能在类内部使用
    
    2.提供 setter 和 getter 方法来开放对数据的操作
  
  - 属性设置私有，通过 getter setter 方法操作属性带来的好处
    
    - 可以控制属性的读写权限
    
    - 可以在方法中对属性的值进行验证

- 封装主要用来保证数据的安全，**实现封装的方式**：
  
  1.属性私有化 加#，也就是使用#开头的对象属性就变成了私有属性，它只能在类内部访问，注意加了#的私有属性一定要先声明，才能使用，否则报错
  
  2.通过 getter 和 setter 方法来操作属性
  
  ```js
  get 属性名(){
     return this.#属性
  }
  
  set 属性名(参数){
     this.#属性 = 参数
  }
  ```
3. 调用#属性时，由于#属性被定义在 setter 方法里，并有 getter 方法可以读取，

因此可以：实例对象.属性名 来读取属性，同时修改不了属性，实现数据的安全

开发中根据实际需要决定是否采取这种对象属性的封装，如果要封装对象属性，推荐下面的写法：

```js
get 属性名(){
   return this.#属性
}

set 属性名(参数){
    this.#属性 = 参数
}
```

```js
class Person {
  // #address = "花果山"
  // 实例使用#开头就变成了私有属性，私有属性只能在类内部访问

  // 私有属性要先声明才能使用
  #name;
  #age;
  #gender;

  constructor(name, age, gender) {
    this.#name = name;
    this.#age = age;
    this.#gender = gender;
  }

  sayHello() {
    console.log(this.#name);
  }

  // getter方法，用来读取属性
  getName() {
    return this.#name;
  }

  // setter方法，用来设置属性
  setName(name) {
    this.#name = name;
  }

  getAge() {
    return this.#age;
  }

  // 不推荐加if判断的写法
  setAge(age) {
    if (age >= 0) {
      this.#age = age;
    }
  }

  get gender() {
    return this.#gender;
  }

  set gender(gender) {
    this.#gender = gender;
  }
}

const p1 = new Person("孙悟空", 18, "男");

// p1.age = "hello"

// p1.getName()
p1.setAge(-11); // p1.age = 11  p1.age

// p1.setName('猪八戒')

p1.gender = "女"; // 修改不了属性gender，它是私有的#gender
console.log(p1.gender); // 男，可以实例对象.属性名来读取
```

### 41. 多态

- 在 JS 中不会检查参数的类型，所以这就意味着任何数据都可以作为参数传递

- 要调用某个函数，无需指定的类型，只要对象满足某些条件即可

- 多态就是要调用某个函数的时候，不检查函数的参数类型，而是关心参数的特点，

只要参数满足某些特点或条件，参数就是合法的，可以使用，

**即函数的参数的数据类型可以是任意类型，这就是多态！**

- 如果一个东西走路像鸭子，叫起来像鸭子，那么程序就认为它就是鸭子

- 多态为我们提供了灵活性

### 42. 继承

- 可以通过 extends 关键来完成继承

- 简单理解：当一个类继承另一个类时，就相当于将另一个类中的代码复制到了当前类中

- 继承发生时，被继承的类称为 父类（或超类），继承的类称为 子类

- 通过继承可以减少重复的代码，并且可以在不修改一个类的前提对其进行扩展

- **有了类，就不需要再用原型 prototype 继承了，可以把公共的属性和方法放在父类里**

```js
class Animal {
  constructor(name) {
    this.name = name;
  }

  sayHello() {
    console.log("动物在叫~");
  }
}

class Dog extends Animal {}

class Cat extends Animal {}

class Snake extends Animal {}

const dog = new Dog("旺财"); // 继承了父类Animal的构造函数
const cat = new Cat("汤姆");

dog.sayHello(); // 因为是继承，可以调用父类Animal的普通方法
cat.sayHello();
```

- 通过继承可以在不修改一个类的情况下对其进行扩展

- **OCP 开闭原则: 程序应该对修改关闭，对扩展开放**

- 子类可以重写父类的同名方法

- 特殊：子类重写父类的构造函数 constructor()时，子类必须在自己的 constructor()里调用 super(), 并且 super()要位于第一行

- 子类的方法中可以使用 super 来调用父类的方法

```js
class Animal {
  constructor(name) {
    this.name = name;
  }

  sayHello() {
    console.log("动物在叫~");
  }
}

class Dog extends Animal {
  // 在子类中，可以通过创建同名方法来重写父类的方法, 重写：override
  sayHello() {
    console.log("汪汪汪");
  }
}

class Cat extends Animal {
  // 重写构造函数，子类中有constructor构造函数，则必须使用调用super()
  constructor(name, age) {
    // 重写构造函数时，构造函数的第一行代码必须为super()
    super(name); // 调用父类的构造函数

    this.age = age;
  }

  sayHello() {
    // 调用一下父类的sayHello
    super.sayHello(); // 在方法中可以使用super来调用父类的方法

    console.log("喵喵喵");
  }
}

const dog = new Dog("旺财");
const cat = new Cat("汤姆", 3);

dog.sayHello();
cat.sayHello();
```

### 43. 对象的结构

对象中存储属性的区域实际有两个：

1. **对象自身**
- 直接通过对象所添加的属性，位于对象自身中，一般是点语法，
  
  例如：p.address = "花果山"

- 在类 class 中通过 x = y 的形式添加的属性，位于对象自身中，
  
  例如：age = 18
2. **原型对象（prototype）**
- 对象中还有一些内容，会存储到其他的对象里（原型对象）

- 在对象中会有一个属性用来存储原型对象 prototype，这个属性叫做**\_**proto\_\***\*（在对象自身中总会有**\_**proto\_\*\***)

- 每个函数都有 prototype，只有函数才有 prototype

- 原型对象也负责为对象存储属性，当我们访问对象中的属性时，会优先访问对象自身的属性，对象自身没有该属性时，才会去原型对象中寻找

- 属性会添加到原型对象中的情况：
1. 在类中通过 xxx(){}方式添加的方法，位于原型 prototype 中，例如：
   
   ```js
   sayHello() { // 位于原型 prototype
     console.log("Hello，我是", this.name)
   }
   ```

2. 主动向原型中添加的属性或方法, 例如：
   
   ```js
   Person.prototype.do = function(){...}
   Person.prototype.nation = 'china'
   ```

3. prototype 上的方法是给实例对象使用的

4.构造函数和原型对象 prototype 中的 this 都指向实例化的对象

```js
class Person {
  name = "孙悟空"; // 位于对象自身中
  age = 18; // 位于对象自身中

  sayHello() {
    //位于原型prototype中，有了类class就无需再使用prototype了
    console.log("Hello，我是", this.name);
  }
}

const p = new Person();

p.address = "花果山";
p.sayHello = "hello";
```

### 44. 原型对象 - 原型链

访问一个对象的原型对象，有 2 种访问方式，这 2 种方式得到的结果一模一样:

1. 对象.\_\_proto\_\_  --> 不要用等号给它赋值。即<mark>禁止写：对象.\_\_proto\_\_= xxx</mark>

2. Object.getPrototypeOf(对象)

备注：一般在编程语言中以下划线开头的属性都是隐藏属性, 隐藏属性就是不希望你直接访问的属性

**原型对象 prototype 中的数据**：

1. 对象中的数据（属性、方法等）

2. constructor（对象的构造函数）: prototype 中的 constructor 指向对象的构造函数，

就是为了识别对象的类型，看对象是由哪个类创建的

例如：为什么打印输出 Person 类的实例对象 Person {name: '孙悟空'，age:18}，

它怎么知道这个对象是 Person 对象？

就是因为在对象的 prototype 中有 constructor,通过 constructor 判断出了对象的类型，当 constructor 判断出了对象是 Person 对象，打印输出时，就可以看到 Person {name: '孙悟空'，age:18}

**注意**

原型对象也有原型，这样就构成了一条原型链，根据对象的复杂程度不同，原型链的长度也不同：

p 对象的原型链：p 对象 --> 原型 --> 原型 --> null

obj 对象的原型链：obj 对象 --> 原型 --> null

**原型链：**

读取对象属性时，会优先读取对象自身属性，

如果对象中有，则使用，没有则去对象的原型中寻找

如果原型中有，则使用，没有则去原型的原型中寻找

直到找到 Object 对象的原型（Object 的原型没有原型（为 null））

如果依然没有找到，则返回 undefined

原型链和作用域链的区别：

- 作用域链，是找变量的链，找不到会报错

- 原型链，是找属性的链，找不到会返回 undefined

```js
class Person {
  name = "孙悟空";
  age = 18;
  sayHello() {
    // 位于原型prototype中
    console.log("Hello，我是", this.name);
  }
}

const p = new Person();
console.log(p.__proto__.__proto__.__proto__);
console.log(p.constructor);
const obj = {}; // obj.__proto__
```

所有的同一个类的实例对象它们的原型对象都是同一个，也就意味着，同类型对象的原型链是一样的

**原型的作用**：

原型就相当于是一个公共的区域，可以被所有该类的实例对象访问，可以将该类实例中的所有的公共属性（方法）统一存储到原型中, 这样我们只需要创建一个属性，即可被所有实例访问

**原型继承**：

JS 中继承就是通过原型来实现的, 当继承时，子类的原型就是一个父类的实例 ！！

例如：cat.prototype = new Animal() // 子类 cat 继承了父类 Animal

在对象中有些值是对象独有的，比如属性（name，age，gender）每个对象都应该有自己值，但是有些值对于每个对象来说都是一样的，比如各种方法，对于这些一样的值没必要重复的创建，公共的属性和方法可以放到原型上

-------------- <mark>以下知识点主要用于面试 但也有利于理解 JS，只是开发中不这么做</mark> -----------------

大部分情况下，我们是不需要修改原型对象，需要修改原型的情况几乎不存在！

注意：千万不要通过类的实例去修改原型，因为：

1. 通过一个对象影响所有同一个类的对象，这么做不合适

2. 修改原型先得创建实例，麻烦

3. 危险

除了通过**proto**能访问对象的原型外，还可以通过类的 prototype 属性，来访问实例的原型, 修改原型时，最好通过类去修改，即直接用类名去修改

好处：

1. 一修改就是修改所有实例的原型

2. 无需创建实例即可完成对类的修改

原则：

1. 原型尽量不要手动改

2. 要改也不要通过实例对象去改

3. 通过 类.prototype 属性去修改

4. 最好不要直接给 prototype 去赋值，会覆盖掉 prototype，等于破坏了原来的原型链

即不要 Person.prototype = { 代码 }

**应该用点语法 Person.prototype.xxx = 新的属性或方法**

总之：虽然 JS 提供了修改原型的方法，但是不建议修改原型，修改原型会使代码变得复杂

### 45. instanceof 和 has own

instanceof 用来检查一个对象是否是一个类的实例，返回布尔值

- instanceof 检查的是对象的原型链上是否有该类实例, 只要原型链上有该类实例，就会返回 true

- Object 是所有对象的原型，所以任何对象和 Object 进行 instanceof 运算都会返回 true

```js
class Animal {}

class Dog extends Animal {}

const dog = new Dog();

console.log(dog instanceof Dog); // true
console.log(dog instanceof Animal); // true
console.log(dog instanceof Object); // true
```

读取一个实例的原型，有 2 种方式, 使用哪种都可以：

1- 实例对象.\_\_proto\_\_

2- 类名.prototype

这 2 种方式访问的都是同一个东西，比较二者的返回值，返回的是 true

```js
class Person {
  name = "孙悟空";
  age = 18;

  sayHello() {
    console.log("Hello，我是", this.name);
  }
}

const p = new Person();
//读取实例 p 的原型
console.log(p.__proto__);
console.log(Person.prototype);
console.log(Person.prototype === p.__proto__); // true
```

**in**

- 使用 in 运算符检查属性时，无论属性在对象自身还是在原型中，都会返回 true

**对象.hasOwnProperty(属性名) (不推荐使用)**

- 用来检查一个对象的自身是否含有某个属性，返回布尔值

**Object.hasOwn(对象, 属性名)**

- 用来检查一个对象的自身是否含有某个属性，返回布尔值

```js
class Person {
  name = "孙悟空";
  age = 18;

  sayHello() {
    console.log("Hello，我是", this.name);
  }
}
console.log("sayHello" in p);

console.log(p.hasOwnProperty("sayHello"));
console.log(p.__proto__.__proto__.hasOwnProperty("hasOwnProperty"));

console.log(Object.hasOwn(p, "sayHello")); // false
```

### 46. 旧类

早期 JS 中，直接通过函数来定义类

- 一个函数如果直接调用 xxx() 那么这个函数就是一个普通函数

- 一个函数如果通过 new 调用 new xxx() 那么这个函数就是一个构造函数

function Person(){

}

等价于：

class Person{

}

```js
var Person = (function () {
  function Person(name, age) {
    // 在构造函数中，this表示新建的对象
    this.name = name;
    this.age = age;

    // this.sayHello = function(){
    //     console.log(this.name)
    // }//不建议这么创建方法，这么写每次创建对象的同时都要再写方法，麻烦
  }

  // 向原型中添加属性（方法）
  Person.prototype.sayHello = function () {
    console.log(this.name);
  };

  // 静态属性，就是类自身的属性
  Person.staticProperty = "xxx";
  // 静态方法，就是类自身的方法，不是实例对象的
  Person.staticMethod = function () {};

  return Person;
})();
```

```js
var Animal = (function () {
  function Animal() {}

  return Animal;
})();

var Cat = (function () {
  function Cat() {}

  // 继承Animal，原型继承，子类的原型 = 父类的实例
  Cat.prototype = new Animal();

  return Cat;
})();

var cat = new Cat();
```

### 47. new 运算符

new 运算符是创建对象时要使用的运算符

- 使用 new 时，到底发生了哪些事情：

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/new

- 当使用 new 去调用一个函数时，这个函数将会作为构造函数调用，使用 new 调用函数时，将会发生这些事：
1. 创建一个普通的 JS 对象（Object 对象 {}）, 为了方便，称其为新对象

2. 将构造函数的 prototype 属性设置为新对象的原型

3. 使用实参来执行构造函数，并且将新对象设置为函数中的 this

4. 如果构造函数返回的是一个非原始值，则该值会作为 new 运算的返回值返回（千万不要这么做）

如果构造函数的返回值是一个原始值或者没有指定返回值，则新的对象将会作为返回值返回

通常情况不会为构造函数指定返回值，也就是构造函数里无需 return 关键字，自动会返回对象

### 48. 面向对象总结

面向对象本质就是，编写代码时所有的操作都是通过对象来进行的。

面向对象的编程的步骤：

1. 找对象

2. 搞对象

学习对象的时候怎么学：

1. 明确这个对象代表什么，有什么用

2. 如何获取到这个对象

3. 如何使用这个对象（对象中的属性和方法）

**JS 对象的分类，有 3 类**：

1.<mark>内建对象</mark>

- 由 ES 标准所定义的对象，可以直接使用

- 比如 Object Function String Number ....
2. <mark>宿主对象</mark>
- 由浏览器提供的对象，比如 document,window

- BOM(用来操作浏览器的对象)、DOM(用来操作网页的对象)

宿主就是语言运行的位置，比如：

- 现在 JS 运行在浏览器中，那浏览器就是宿主

- JS 在 Node 中运行，Node 就是宿主，

- 在 Deno 中运行，Deno 就是宿主，不同的运行环境就是不同的宿主
  
  3.<mark>自定义对象</mark>

- 由开发人员自己创建的对象

### 49. 数组 ( Array）

- 数组也是一种复合数据类型，在数组可以存储多个不同类型的数据

- 数组中存储的是有序的数据，数组中的每个数据都有一个唯一的索引, 可以通过索引来操作获取数据

- 数组中存储的数据叫做元素

- 索引（index）是一组大于 0 的整数

- 创建数组:
  
  通过 Array()来创建数组，也可以通过[]来创建字面量数组 (推荐字面量方式创建数组)

- 向数组中添加元素
  
  - 语法：数组[index] = 元素

- 读取数组中的元素
  
  - 语法：数组[index]
  
  - 如果读取了一个不存在的元素，不会报错而是返回 undefined

- length
  
  - 获取数组的长度
  
  - 获取的实际值就是数组的最大索引 + 1
  
  - 向数组最后添加元素：数组[数组.length] = 元素
  
  - length 是可以修改的
    
    - length 改大了，长度变长，数组里会增加空元素
    
    - length 改小了，长度变短，会自动删除数组尾部多余的元素

### 50. for-of 语句

for-of 语句可以用来遍历可迭代对象，比如数组，字符串

语法：

```js
for(变量 of 可迭代的对象){
    语句...
}
```

执行流程：

for-of 的循环体会执行多次，数组中有几个元素就会执行几次，每次执行时都会将一个元素赋值给变量

```js
const arr = ["孙悟空", "猪八戒", "沙和尚", "唐僧"];

for (let value of arr) {
  console.log(value);
}

for (let value of "hello") {
  console.log(value); // 可以 hello 的每个字母取出来
}
```

备注：

JavaScript 原有的 **for...in 循环，只能获得对象的键名，不能直接获取键值**

ES6 提供**for...of 循环，允许遍历获得键值**

### 51. 数组方法

**Array.isArray()**

- 用来检查一个对象是否是数组，返回值是布尔值

**at()**

- 可以根据索引获取数组中的指定元素

- at 可以接收负索引作为数组的参数

-------- <mark>以下的方法都是非破坏性方法，不会影响原数组，而是返回一个新的数组</mark> ---------

**concat()**

- 用来连接两个或多个数组

- 非破坏性方法，不会影响原数组，而是返回一个新的数组

**indexOf()**

- 获取元素在数组中第一次出现的索引

- 参数：
1. 要查询的元素

2. 查询的其实位置

**lastIndexOf()**

- 获取元素在数组中最后一次出现的位置

- 返回值：找到了则返回元素的索引，没有找到返回-1

**join()**

- 将一个数组中的元素连接为一个字符串

["孙悟空", "猪八戒", "沙和尚", "唐僧", "沙和尚"] -> "孙悟空,猪八戒,沙和尚,唐僧,沙和尚"

- 参数：

指定一个字符串作为连接符

**slice()**

- 用来截取数组（非破坏性方法）

- 参数：
1. 截取元素的起始位置（包括该位置）

2. 截取元素的结束位置（不包括该位置）
   
   - 第二个参数可以省略不写，如果省略则会一直截取到最后
   
   - 索引可以是负值

3. 如果将两个参数全都省略，则可以对数组进行浅拷贝（浅复制）

**map()**

- 可以根据原有数组返回一个新数组

- 需要一个回调函数作为参数，回调函数的返回值会成为新数组中的元素

- 回调函数中有三个参数：
  
  - 第一个参数：当前元素
  
  - 第二个参数：当前元素的索引
  
  - 第三个参数：当前数组

**forEach()**

- 用来遍历数组

- 它需要一个回调函数作为参数，这个回调函数会被调用多次

数组中有几个元素，回调函数就会调用几次

每次调用，都会将数组中的数据作为参数传递

- 回调函数中有三个参数：
  
  - element 当前的元素
  
  - index 当前元素的索引
  
  - array 被遍历的数组

**filter()**

- 可以用来对数组进行过滤, 从一个数组中获得符和条件的元素

- 将数组中符合条件的元素保存到一个新数组中返回

- 需要一个回调函数作为参数，会为每一个元素去调用回调函数，

并根据返回值来决定是否将元素添加到新数组中

- 根据回调函数的结果来决定是否保留元素，true 保留，false 不保留

**find()**

- 可以从一个数组中获得符和条件的第一个元素

**reduce()**

- 可以用来合并数组中的元素

- 需要两个参数：
  
  - 回调函数（指定运算规则）
  
  - 四个参数：
    
    - prev 上一次运算结果
    
    - curr 当前值
    
    - index 当前索引
    
    - arr 当前数组

- 初始值
  
  - 用来指定第一次运算时 prev，如果不指定则直接从第二个元素开始计算

---

--------- <mark>以下的方法都是破坏性方法，会改变原来的对象，原来的对象发生变化了</mark> -----------

**push()**

- 向数组的末尾添加一个或多个元素，并返回新的长度

**pop()**

- 删除并返回数组的最后一个元素

**unshift()**

- 向数组的开头添加一个或多个元素，并返回新的长度

**shift()**

- 删除并返回数组的第一个元素

**splice()**

- 可以删除、插入/添加、替换数组中的元素

- 参数：
  
  - 第 1 个参数 删除的起始位置
  
  - 第 2 个参数 删除的数量
  
  - 第 3 个参数 要插入的元素

- 返回值：返回被删除的元素

**reverse()**

- 反转数组

**sort()**

- sort 用来对数组进行排序（会对改变原数组）

- sort 默认会将数组升序排列

注意：sort 默认会按照 Unicode 编码进行排序，所以如果直接通过 sort 对数字进行排序

可能会得到一个不正确的结果，例如：1，2，10，4 得到的排序结果是 1，10，2，4

- 参数：
  
  - 可以传递一个回调函数作为参数，通过回调函数来指定排序规则
  
  - (a, b) => a - b 升序排列
  
  - (a, b) => b - a 降序排列

### 52. 浅拷贝 - 深拷贝 - 对象的复制

**浅拷贝（shallow copy - la copie superficielle）**

- 通常对对象的拷贝都是浅拷贝

- 浅拷贝顾名思义，只对对象的浅层进行复制（只复制一层）

- 如果对象中存储的数据是原始值，那么拷贝的深浅是不重要

- 浅拷贝只会对对象本身进行复制，不会复制对象中的属性（或元素）

**深拷贝（deep copy - la copie profonde）**

- 深拷贝指不仅复制对象本身，还复制对象中的属性和元素

- 因为性能问题，通常情况不太使用深拷贝

- **JS 中专门用来深拷贝的方法：structuredClone()**

浅拷贝只复制属性指向某个对象的指针，而不复制对象本身，新旧对象还是共享同一块内存，修改对象属性会影响原对象

但深拷贝会另外创造一个一模一样的对象，新对象跟原对象不共享内存，修改新对象不会改到原对象

开发中根据具体需求选择浅拷贝或深拷贝

```js
const obj = {
  name: "孙悟空",
  friend: {
    name: "猪八戒",
  },
};

// 对obj进行浅复制(浅拷贝)
const obj2 = Object.assign({}, obj);

// 对obj进行深复制(深拷贝)
const obj3 = structuredClone(obj);

// 利用JSON来完成深复制(深拷贝)
const str = JSON.stringify(obj);
const obj4 = JSON.parse(str);
```

**对象的浅拷贝方式**

**注意：对象的复制一定会产生新的对象**

```js
// 如何去复制一个对象 复制必须要产生新的对象才是复制
// 当调用slice时，会产生一个新的数组对象，从而完成对数组的复制
const arr3 = arr.slice();
```

**... (展开运算符)**

- 可以将一个数组中的元素展开到另一个数组中

- 或者作为函数的参数传递

- 通过它也可以对数组进行浅拷贝

```js
function sum(a, b, c) {
  return a + b + c;
}

const arr4 = [10, 20, 30];
let result = sum(...arr4); // 把数组arr4里的元素作为实参传递给了sum函数
```

```js
// 给数组添加新元素
let arr1 = ["this", "is", "an"];
arr1 = [...arr1, "apple"];
console.log(arr1); // [ 'this', 'is', 'an', 'apple' ]

//合并数组，参数排列顺序不同，结果不同
const arr1 = [1, 2, 3];
const arr2 = [4, 5, 6];

const arr3 = [...arr1, ...arr2];
console.log(arr3); // [ 1, 2, 3, 4, 5, 6 ]

const arr4 = [...arr2, ...arr1];
console.log(arr4); // [4, 5, 6, 1, 2, 3];

// 多个数组的合并
const output = [...arr1, ...arr2, ...arr3, ...arr4];
```

**对象的复制**

- Object.assign(目标对象, 被复制的对象)

- 将被复制对象中的属性复制到目标对象里，并将目标对象返回

- 也可以使用展开运算符对对象进行复制

```js
const obj = { name: "孙悟空", age: 18 };

// const obj2 = Object.assign({}, obj)
const obj2 = { address: "花果山", age: 28 };

Object.assign(obj2, obj); // 将obj中的属性在新对象中展开
// console.log(obj2)

const obj3 = { address: "高老庄", ...obj, age: 48 };
```

**通过...展开运算符合并对象**

- 对象添加时会覆盖原先数据,所以在添加时需要把原数据写上

- 注意：未添加…展开运算符时会显示添加整个数组或对象,而不是单个元素

```js
let obj = { name: "Tom", age: 18 };
let temp = { gender: "male", girlfriend: "Mary" };

//将temp添加到obj里,后面的参数添加到前面的参数里面
obj = { ...obj, ...temp };
console.log(obj); // {name:'Tom',age:18,gender:'male',girlfriend:'Mary}
```

```js
let arr = [1, 2, 3, 4, 5];
console.log(arr); // 输出整个数组[1,2,3,4,5]
console.log(...arr); // 输出数组的单个元素1 2 3 4 5
```

### 53. 高阶函数

高阶函数 (Higher-order function)

- 如果一个函数的参数或返回值是函数，则这个函数就称为高阶函数

- 为什么要将函数作为参数传递？（回调函数有什么作用？）
  
  - 作为参数或返回值的函数就是回调函数
  
  - 将函数作为参数，意味着可以对另一个函数动态的传递代码

- 通常回调函数都是匿名函数，也就是使用一次就结束了，回调函数的调用都是一次性的

```js
function someFn() {
  return "hello";
}

function outer(cb) {
  return () => {
    // 返回值是一个函数
    console.log("记录日志~~~~~");
    const result = cb();
    return result;
  };
}

let result = outer(someFn);
```

### 54. 闭包

闭包就是能访问到外部函数作用域中变量的函数

**什么时候使用**：

当我们需要隐藏一些不希望被别人访问的内容时就可以使用闭包

**构成闭包的要件**：

1. 函数的嵌套

2. 内部函数要引用外部函数中的变量

3. 内部函数要作为返回值返回

**简单理解闭包操作**：

把一个函数 x 和变量定义在另一个函数 y 里，同时一定要在 y 里 return 函数 x,

然后调用 y，这就是闭包

注意：由于 y 返回的 x 是个函数，要拿到结果，还要再调用 x，即 x()

```js
// 函数 outer前套了一个箭头函数，并且内部的箭头函数作为返回值返回
function outer() {
  let num = 0; // 位于函数作用域中

  return () => {
    //内部函数要作为返回值返回
    num++; // 内部函数引用外部函数中的变量 num
    console.log(num);
  };
}

const newFn = outer(); // 注意newFn接收的是一个函数

console.log(newFn);
newFn(); // newFn是一个函数，只有调用了才有结果
newFn();
```

函数的作用域，在函数创建时就已经确定的（也称词法作用域）, 和调用的位置无关

闭包利用的就是词法作用域, 词法作用域要看定义函数时函数的位置，函数的外层作用域取决于在哪个位置定义的函数

```js
let a = "全局变量a";

function fn() {
  // 这里定义了函数fn，fn的外层作用域就是全局作用域
  console.log(a);
}

function fn2() {
  let a = "fn2中的a";

  fn();
}

fn2(); // "全局变量a", 函数fn的外层作用域是全局

function fn3() {
  let a = "fn3中的a";

  function fn4() {
    // 这里定义了函数fn4，fn4的外层作用域就是函数fn3
    console.log(a);
  }

  return fn4;
}

let fn4 = fn3();

fn4(); // "fn3中的a"
```

闭包的生命周期：

1. 闭包在外部函数调用时产生，外部函数每次调用都会产生一个全新的闭包

2. 在内部函数丢失时销毁（也就是内部函数被垃圾回收了，闭包才会消失）

闭包的注意事项：

闭包主要用来隐藏一些不希望被外部访问的内容，这就意味着闭包需要占用一定的内存空间，相较于类来说，闭包比较浪费内存空间（类可以使用原型而闭包不能），

- 需要执行次数较少时，使用闭包，一般闭包就需要一个，最多 2，3 个，而且闭包的每个对象，每个属性，每个方法都会独立的占用一个内存，很浪费内存

- 需要大量创建实例时，使用类

根据使用 JS 的经验，一般需要隐藏的一些东西不需要创建大量实例，所以几乎我们藏东西的时候使用闭包没问题

```js
function outer2() {
  let num = 0;
  return () => {
    num++;
    console.log(num);
  };
}

let fn1 = outer2(); // fn1是独立闭包，fn2也是独立闭包，
let fn2 = outer2();
// fn1和fn2是相互独立的，因为外部函数每次调用都会产生一个全新的闭包

fn1();
fn2();

fn1 = null; // 清除内存
fn2 = null;
```

### 55. 递归

调用自身的函数称为递归函数，递归的作用和循环基本一致

递归的核心思想就是将一个大的问题拆分为一个一个小的问题，小的问题解决了，大的问题也就解决了

编写递归函数，一定要包含两个要件：

1.基线条件 ——>   递归的终止条件

2.递归条件 ——>   如何对问题进行拆分

递归的作用和循环是一致的，不同点在于，递归思路的比较清晰简洁，循环的执行性能比较好. 在开发中，一般的问题都可以通过循环解决，也是尽量去使用循环，少用递归, 递归性能不好, 只在一些使用循环解决比较麻烦的场景下，才使用递归

### 56. arguments - 可变参数

**<mark>arguments</mark>**

- arguments 是函数中又一个隐含参数

- arguments 是一个类数组对象（伪数组）

和数组相似，可以通过索引来读取元素，也可以通过 for 循环变量，但是它不是一个数组对象，**不能调用数组的方法**

- arguments 用来存储函数的实参，无论用户是否定义形参，实参都会存储到 arguments 对象中, 可以**通过 arguments 直接访问实参**

- arguments 和形参没有关系，也就是有没有形参，实参都是在 arguments 里

**<mark>可变参数(也就是剩余参数)，在定义函数时可以将参数指定为可变参数</mark>**

- 语法：...可变参数名

- 可变参数可以接收任意数量实参，并将他们统一存储到一个数组中返回

- 可变参数的作用和 arguments 基本是一致，但是也具有一些不同点：
1. 可变参数的名字可以自己指定

2. 可变参数就是一个真数组，可以直接使用数组的方法

3. 可变参数可以和其他普通参数一起使用，但要将可变参数写到最后

**<mark>arguments 和 可变参数的区别：</mark>**

- arguments 是伪数组，不能使用数组方法，...

- 可变参数 是真数组，可以使用数组方法

- 可变参数可以配合其他参数一起使用，arguments 不行

- 使用 arguments,需要结合 for 循环使用

- 可变参数不需要循环，直接使用即可

开发中一般使用可变参数，arguments 是比较老的,存在不足，现在都用可变参数代替 arguments

```js
function fn() {
  // 报错，arguments是伪数组，不能调用数组方法
  arguments.forEach((ele) => console.log(ele));
}
```

```js
// 定义一个函数，可以求任意个数值的和
function sum() {
  // 通过arguments，可以不受参数数量的限制更加灵活的创建函数
  let result = 0;

  for (let num of arguments) {
    result += num;
  }

  return result;
}

function sum2(...num) {
  return num.reduce((a, b) => a + b, 0);
}

// 当可变参数和普通参数一起使用时，需要将可变参数写到最后
function fn3(a, b, ...args) {
  console.log(args);
}

fn3(123, 456, "hello", true, "1111");
```

---

### 以下是内建对象部分

所谓的内建对象，就是 JS 标准中定义的对象，在任何的 JS 解释器中可以直接使用的对象

比如：数组，Object, Function, 原始值 等等

### 57. 解构赋值：只有数组解构和对象解构两种

解构赋值是一种快速为变量赋值的简洁语法，本质上仍然是为变量赋值，分为数组解构、对 象解构两大类型

- **数组解构赋值**

数组解构是将数组的单元值(就是数组元素的值)快速批量赋值给一系列变量的简洁语法，如下代码所示：

```html
<script>
  // 普通的数组
  let arr = [1, 2, 3];
  // 批量声明变量 a b c
  // 同时将数组单元值 1 2 3 依次赋值给变量 a b c
  let [a, b, c] = arr;
  console.log(a); // 1
  console.log(b); // 2
  console.log(c); // 3

  // 变量的数量大于单元值数量时，多余的变量将被赋值为 undefined
  const [a, b, c, d] = [1, 2, 3];
  console.log(a); // 1
  console.log(b); // 2
  console.log(c); // 3
  console.log(d); // undefined

  // 变量的数量小于单元值数量时，其余的单元值被忽略
  const [a, b] = [1, 2, 3]; // 3被忽略
  console.log(a); // 1
  console.log(b); // 2

  // 变量的数量小于单元值数量时，用剩余参数比较合适，剩余参数返回的是一个真数组
  const [a, b, ...c] = [1, 2, 3, 4];
  console.log(a); // 1
  console.log(b); // 2
  console.log(c); // [3,4] 真数组

  // 使用默认参数，防止传递undefined
  const [a = 0, b = 0] = []; // 默认参数为0
</script>
```

总结：

1. 赋值运算符 `=` 左侧的 `[]`
   
   用于批量声明变量，右侧数组的单元值将被赋值给左侧的变量

2. 变量的顺序对应数组单元值的位置依次进行赋值操作

3. 变量的数量大于单元值数量时，多余的变量将被赋值为 `undefined`

4. 变量的数量小于单元值数量时，可以通过 `...` 获取剩余单元值，但只能置于最末位

5. 允许初始化变量的默认值，且只有数组元素的值为 `undefined` 时默认值才会生效
- **对象解构赋值**

对象解构是将对象属性和方法快速批量赋值给一系列变量的简洁语法，如下代码所示：

```html
<script>
    // 普通对象
    const user = {
      name: '小明',
      age: 18
    };
    // 批量声明变量 name age
    // 同时将数组单元值 小明  18 依次赋值给变量 name  age
    // 注意：解构赋值中变量的名字必须和对象里对应的属性名字一样！
    const {name, age} = user // 解构赋值的变量名必须和对象user里的name，age一样
    console.log(name) // 小明
    console.log(age) // 18

    // 对象解构的变量名可以重新改名，通过冒号实现，语法：旧变量名：新变量名
    const {name:username,age} = {name:'小明',age:18}
    console.log(username) // 小明

    // 解构对象数组, 即数组的元素是对象
    const pig = [
      {
        name:'佩奇'，
        age:6
      }
    ]
    const [{name,age}] = pig

    // 多级对象解构
    const pig = {
      name:'佩奇'，
      family:{
        mom:'猪妈'，
        dad:'猪爸'，
        sister:'乔治'
      }
      age:6
    }
    const {name,family:{mom,dad,sister},age} = pig
    console.log(name)// 佩奇
    console.log(mom) // 猪妈
    console.log(dad) // 猪爸
    console.log(sister) // 乔治

    // 多级对象数组解构
    const person = [
      {
        name:'佩奇'，
        family:{
          mom:'猪妈'，
          dad:'猪爸'，
          sister:'乔治'
        }
        age:6
     }
   ]
    const [{name,family:{mom,dad,sister},age}] = person
    console.log(name)// 佩奇
    console.log(mom) // 猪妈
    console.log(dad) // 猪爸
    console.log(sister) // 乔治
</script>
```

总结：

1. 赋值运算符 `=` 左侧的 `{}`
   
   用于批量声明变量，右侧对象的属性值将被赋值给左侧的变量.
   
   <mark>注意：在进行对象解构赋值时，需要保证等号右侧是一个字面量对象</mark>

2. 对象属性的值将被赋值给与属性名相同的解构变量,
   
   也就是解构赋值中变量的名字必须和对象里对应的属性名字一样

3. 对象中找不到与变量名一致的属性时变量值为 `undefined`

4. 允许初始化变量的默认值，属性不存在或单元值为 `undefined` 时默认值才会生效

5. 对象解构的变量名可以重新改名，只需用冒号把新旧变量名隔开就可实现，冒号左边是旧变量名，右边是新变量名，语法：旧变量名：新变量名

### 58. 对象序列化

对象的序列化

- JS 中的对象使用时都是存在于计算机的内存中的

- 序列化指将对象转换为一个可以存储的格式

<mark>**在 JS 中对象的序列化通常是将一个对象转换为字符串（JSON 字符串）！！**</mark>

- 序列化的用途（对象转换为字符串有什么用）：
  
  - 对象转换为字符串后，可以将字符串在不同的语言之间进行传递
    
    甚至人可以直接对字符串进行读写操作，使得 JS 对象可以不同的语言之间传递
  
  - 用途：
1. 作为数据交换的格式，比如前端和后端服务器之间相互传递数据

2. 用来编写配置文字，比如 vscode 配置 settings.json 里的各项配置
- 如何进行序列化：
  
  - 在 JS 中有一个工具类 JSON （JavaScript Object Notation） JS 对象表示法
  
  - JS 对象序列化后会转换为一个字符串，这个字符串我们称其为 JSON 字符串

- 也可以手动的编写 JSON 字符串，在很多程序的配置文件就是使用 JSON 编写的

- 编写 JSON 的注意事项：
1. JSON 字符串有两种类型：
   
   - JSON 对象 {}
   
   - JSON 数组 []

2. JSON 字符串的属性名必须使用双引号引起来

3. JSON 中可以使用的属性值（元素）
   
   - 数字（Number）
   
   - 字符串（String） 必须使用双引号
   
   - 布尔值（Boolean）
   
   - 空值（Null）
   
   - 对象（Object {}）
   
   - 数组（Array []）

**JSON 中不能使用 undefined 和函数**

4. JSON 的格式和 JS 对象的格式基本上一致的，JSON 的格式更严格一点

注意：JSON 字符串如果属性是最后一个，则不要再加逗号,

正常使用 JSON 时，一般不会手动写 JSON，因为容易写错，尤其是当数据较多的时候，

因此手写 JSON，常见的场景只有编写配置文字(vscode 配置 settings.json 里的各项配置)

```js
const obj = {
  name: "孙悟空",
  age: 18,
};

// 将obj转换为JSON字符串
//JSON.stringify()可以将一个对象转换为JSON字符串
const str = JSON.stringify(obj);

// JSON.parse() 可以将一个JSON格式的字符串转换为JS对象
const obj2 = JSON.parse(str);

console.log(obj);
console.log(str); // {"name":"孙悟空","age":18}
console.log(obj2);
```

### 59. Map 对象

- Map 对象用来存储键值对结构的数据（key-value）

- Object 中存储的数据就可以认为是一种键值对结构

- Map 和 Object 的主要区别：
  
  - Object 中的属性名只能是字符串或符号，如果传递了一个其他类型的属性名，
    
    JS 解释器会自动将其转换为字符串
  
  - Map 中任何类型的值都可以称为数据的 key

- 我们主要使用的是 Object，那什么时候用 Map?
  
  当一个字符串的属性不能满足你的需要，你想使用对象作为 key 去使用的时候，Map 就是不二选择

- 创建：new Map()

- 属性和方法：
  
  - map.size() 获取 map 中键值对的数量
  
  - map.set(key, value) 向 map 中添加键值对
  
  - map.get(key) 根据键名 key 获取值
  
  - map.delete(key) 删除指定数据
  
  - map.has(key) 检查 map 中是否包含指定键，返回值是布尔值
  
  - map.clear() 删除全部的键值对

```js
const map = new Map();

map.set("name", "孙悟空");
map.set(obj2, "呵呵");
map.set(NaN, "哈哈哈");

map.delete(NaN);
// map.clear()

console.log(map);
console.log(map.get("name"));
console.log(map.has("name"));
```

- Array.from() 方法对一个类似数组或可迭代对象创建一个新的，浅拷贝的数组实例用展开...运算符也可以将 map 转换为数组，并且这种方式更简单，更推荐
  
  map.keys() - 获取 map 的所有的 key
  
  map.values() - 获取 map 的所有的 value
  
  ```js
  const map = new Map();
  
  map.set("name", "孙悟空");
  map.set("age", 18);
  map.set({}, "呵呵");
  
  // Array.from() 方法对一个类似数组或可迭代对象创建一个新的，浅拷贝的数组实例
  // 将map转换为数组
  const arr = Array.from(map); // [["name","孙悟空"],["age",18]]
  
  // 用展开...运算符也可以将map转换为数组，并且这种方式更简单，更推荐
  const arr = [...map];
  console.log(arr);
  ```

### 60. set 对象

**`Set`**  对象允许你存储任何类型的唯一值，无论是原始值或者是对象引用

`Set`对象是值的集合，你可以按照插入的顺序迭代它的元素。Set 中的元素只会**出现一次**， 即 Set 中的元素是唯一的

- Set 用来创建一个集合

- 它的功能和数组类似，不同点在于 Set 中不能存储重复的数据

也就是 Set 里只能是不同的数据，数据不能重复一样的，

重复的数据加不进 Set，而数组可以存储重复数据

- 创建方式：
  
  - new Set()
  
  - 或 new Set([...]) // 根据一个数组创建一个集合 Set

- 方法
  
  - size 获取数量
  
  - add() 添加元素
  
  - has() 检查元素
  
  - delete() 删除元素

```js
// 创建一个Set
const set = new Set();

// 向set中添加数据
set.add(10);
set.add("孙悟空");
set.add(10); // 加不进，已经有数字10

const arr = [...set];

const arr2 = [1, 2, 3, 2, 1, 3, 4, 5, 4, 6, 7, 7, 8, 9, 10];

const set2 = new Set(arr2); // 利用Set实现数组去重

console.log([...set2]); // 把Set转换为数组
```

### 61. Math

- Math 是一个工具类，实际上并不是一个真正的类，

它不能使用 new，创建不出对象

- Math 中为我们提供了数学运算相关的一些常量和方法

- Math 本身就是一个对象，直接使用即可

- 常量：Math.PI 获取圆周率

- 方法:
  
  - Math.abs() 求一个数的绝对值
  
  - Math.min() 求多个值中的最小值
  
  - Math.max() 求多个值中的最大值
  
  - Math.pow() 求 x 的 y 次幂/次方
  
  - Math.sqrt() 求一个数的平方根
  
  - Math.floor() 向下取整
  
  - Math.ceil() 向上取整
  
  - Math.round() 四舍五入取整
  
  - Math.trunc() 直接去除小数位
  
  - Math.random() 生成一个 0-1 之间的随机数，不包括 0 和 1

### 62. Date

- 在 JS 中所有的和时间相关的数据都由 Date 对象来表示

- 对象的方法：
  
  - getFullYear() 获取 4 位数年份 例如：2022
  
  - getMonth() 返当前日期的月份（0-11）
  
  - getDate() 返回当前的日期，是几日
  
  - getDay() 返回当前日期是周几（0-6） 0 表示周日

......

- getTime() 返回当前日期对象的时间戳

时间戳：自 1970 年 1 月 1 日 0 时 0 分 0 秒到当前时间所经历的毫秒数

计算机底层存储时间时，使用都是时间戳

getTime()要通过一个对象调用

Date.now() 获取当前的时间戳

```js
// 直接通过new Date()创建时间对象时，它创建的是当前的时间的对象
let d = new Date();

// 可以在Date()的构造函数中，传递一个表示时间的字符串
// 字符串的格式：月/日/年 时:分:秒
// 年-月-日T时:分:秒
d = new Date("2019-12-23T23:34:35");

// new Date(年份, 月, 日, 时, 分, 秒, 毫秒)，推荐使用
d = new Date(2016, 0, 1, 13, 45, 33);

d = new Date();

result = d.getFullYear();
result = d.getMonth();
result = d.getDate();
result = d.getDay();

result = d.getTime();
```

### 63. 包装类

在 JS 中，除了直接创建原始值外，也可以创建原始值的对象

通过 new String() 可以创建 String 类型的对象

通过 new Number() 可以创建 Number 类型的对象

通过 new Boolean() 可以创建 Boolean 类型的对象

- **但是千万不要这么做，不要用 new 对象的这种方式**

- **因为包装类不是给我们用的，是 JS 给自己用的**

<mark>包装类</mark>：

JS 中一共有 5 个包装类

String --> 字符串包装为 String 对象

Number --> 数值包装为 Number 对象

Boolean --> 布尔值包装为 Boolean 对象

BigInt --> 大整数包装为 BigInt 对象

Symbol --> 符号包装为 Symbol 对象

- 通过包装类可以将一个原始值包装为一个对象，当我们对一个原始值调用方法或属性时， JS 解释器会临时将原始值包装为对应的对象，然后调用这个对象的属性或方法

- 包装类不是给我们用的，是 JS 给自己的解释器/浏览器用的

<mark>包装类对我们的意义</mark>：

由于原始值会被临时转换为对应的对象，这就意味着对象中的方法都可以直接通过原始值来调用

### 64. 字符串的方法

- 字符串其本质就是一个字符数组

- "hello" --> 在计算机底层保存的是数组["h", "e", "l", "l", "o"]

- 字符串的很多方法都和数组是非常类似的

- 属性和方法：
  
  - length 获取字符串的长度
  
  - 字符串[索引] 获取指定位置的字符

- str.at() （实验方法）根据索引获取字符，可以接受负索引

- str.charAt() 根据索引获取字符

- str.concat() 用来连接两个或多个字符串

- str.includes() 用来检查字符串中是否包含某个内容, 有返回 true, 没有返回 false

- str.indexOf() 查询字符串中是否包含某个内容

- str.lastIndexOf() 查询字符串中是否包含某个内容

- str.startsWith() 检查一个字符串是否以指定内容开头

- str.endsWith() 检查一个字符串是否以指定内容结尾

- str.padStart() 通过添加指定的内容，使字符串保持某个长度

- str.padEnd() 通过添加指定的内容，使字符串保持某个长度

- str.replace() 使用一个新字符串替换一个指定内容

- str.replaceAll() 使用一个新字符串替换所有指定内容

- str.slice() 对字符串进行切片

- str.substring() 截取字符串

- str.split() 用来将一个字符串拆分为一个数组

- str.toLowerCase() 将字符串转换为小写

- str.toUpperCase() 将字符串转换为大写

- str.trim() 去除前后空格

- str.trimStart() 去除开始空格

- str.trimEnd() 去除结束空格

备注：

无论是字符串的属性还是字符串的方法都不是破坏性的，也就是不会影响原来的字符串，调用了方法之后，原来的字符串该什么样还是什么样，不会因为调用了方法而改变，因为字符串是不可变类型，一旦创建永远都不会改变

[目录](README)
