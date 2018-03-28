---
title: 'ECMAScript数据类型'
date: 2018-03-27 10:48:48
categories: JavaScript高级程序设计笔记
toc: true
tags: JavaScript
---
## 基本介绍

ECMAScirpt 5.1 中定义了6种数据类型，其中有5中简单数据类型（基本数据类型）:

 1. **Undefined：**只有一个值，为undefined，意味着“空值(no value)”，适用于所有数据类型。
 2. **Null：**只有一个值，为null，意味着“空对象(no object)”，只适用于对象类型。（literal）
 3. **Boolean：**有两个值，为true与false 
 4. **Number：**值遵循IEEE 754标准的64位浮点数的集合，没有整型数据结构。此外还包含三个特殊的值：NaN、Infinity、Infinity
 5. **String：**值是有穷个Unicode字符的集合。必须用'或"括起来。
 6. 还有一种复杂数据类型： **Object**
 7. 最新的ECMAScript 6 又加了一种类型：**Symbol** (ECMAScript 6 新定义)


----------


## typeof操作符
用来检测给定变量的数据类型。
对一个值使用typeof操作符可能返回下列某个字符：

 1. “undefined”值未定义 
 2. “boolean”布尔值 
 3. “string”字符串 
 4. “number”数值 
 5. “object”对象或null
 6. “function”函数

使用：typeof 操作数  /  typeof(操作数)  ——>圆括号不是必须的，因为typeof不是函数


----------


## Undefine类型
首字母大写的Undefined表示的是一种数据类型，小写的undefined表示的是属于这种数据类型的唯一的一个值。
使用var声明变量但未进行初始化时，这个变量的值就是undefined，例如：

```
var message;
alert(message == undefined); // true
```

一个未初始化的变量的值为undefined，一个没有传入实参的形参变量的值为undefined，如果一个函数什么都不返回，则该函数默认返回undefined。

> 注意： 对未声明的变量执行typeof操作符同样会返回undefined。

```
var message; //这个变量声明之后默认为undefined
// 下面这个变量未声明
// var age
alert(typeof message); // "undefined"
alert(typeof age); // "undefined"

```


----------


## Null类型
首字母大写的Null表示的是一种数据类型，小写的null表示的是属于这种数据类型的唯一的一个值。
null值表示一个空对象指针：

```
var car = null;
alert(typeof car); //"object"
```

如果定义的变量准备用于保存对象，那么最好将该变量初始化为null。

undefined 值派生自 null，因此规定相等性测试返回 true。
```
null  == undefined // true
null === undefined // false
```



null 是一个字面量 (而不是全局对象的一个属性，undefined 是 )

```
console.log(null);             //null
console.log(undefined);        //undefined

console.log(window.null);      //undefined
console.log(window.undefined); //undefined
```

**null与undefined的区别**

```
console.log(foot); // Uncaught ReferenceError: foot is not defined

var foo;
console.log(foo);  // undefined

var bar = null;
console.log(bar);  // null

typeof null        // object (bug in ECMAScript, should be null)
typeof undefined   // undefined
```


----------


## Boolean类型

1、如果 Boolean 构造函数的参数不是一个布尔值，则该参数会被转换成一个布尔值。
2、**转换规则:**

|数据类型|true|false|
|---|---|---|
|Boolean|true|false|
|String|任何非空字符串|""（空字符串）|
|Number|任何非零数字值（包括无穷大）|0 和 NaN|
|Object|任何对象|null|
|Undefined|（不适用）|undefined|

```
//初始化的时候
//false
var bfalse = new Boolean(false);
var bEmptyString = new Boolean("");
var bZero = new Boolean(0);
var bNaN = new Boolean(NaN);
var bNull = new Boolean(null);
var bNoParam = new Boolean(); //相当于传入undefined

//true
var btrue = new Boolean(true);
var btrueString = new Boolean("true");
var bfalseString = new Boolean("false");
var bSuLin = new Boolean("Su Lin");
```

> 不要通过新建 Boolean 对象的方法来将一个非布尔值转化成布尔值。 直接使用 Boolean 函数才是正确的

```
var x = Boolean(expression);     // 这样用
var x = new Boolean(expression); // 而不要这样!
```



## Number类型

根据 ECMAScript 标准，JavaScript 中只有一种数字类型：基于 IEEE 754 标准的双精度 64 位二进制格式的值（-(253 -1) 到 253 -1）。它并没有为整数给出一种特定的类型。除了能够表示浮点数外，还有一些带符号的值：+Infinity，-Infinity 和 NaN (非数值，Not-a-Number)
### 1.数值字面量格式：

```
var intNum = 55; //十进制整数

var octalNum1 = 070; //八进制 56
var octalNum1 = 079; //无效，解析为79
var octalNum1 = 08;  //无效，解析为8

var hexNum1 = 0xA;  //十六进制 10
var hexNum1 = 0x1f; //十六进制31

var floatNum1 = 1.1;
var floatNum2 = 0.1;
var floatNum3 = .1; //有效但不推荐
var floatNum4 = 1.0; //小数点后面没有数字，转换为整数 解析为1
var floatNum5 = 10.0; //整数 解析为10
var floatNum6 = 3.125e7; //等于31250000
```

数字类型只有一个整数，它有两种表示方法： 0 可表示为 -0 和 +0（"0" 是 +0 的简写）。 在实践中，这也几乎没有影响。 例如 +0 === -0 为真。 但是，你可能要注意除以0的时候：

```
42 / +0; // Infinity
42 / -0; // -Infinity
```

### 2.数值范围
|表示|描述|
|--|--|
|Number.MIN_VALUE|最小数值，一般为5e-324|
|Number.MAX_VALUE|最大数值，一般为1.7976931348623157e+308|
|Infinity|正无穷，是不能参与计算的数值|
|-Infinity|负无穷，是不能参与计算的数值|

### 3.NAN
如果参数无法被转换为数字，则返回 NaN。

 - 任何涉及NaN的操作（例如NaN/10）都会返回NaN。
 - NaN与任何值都不相等，包括NaN本身。

ECMAScript定义了isNaN()函数来确定某个参数是否“不是数值”。isNaN()在接收到一个值之后，会尝试将这个值转换为数值。某些不是数值的值会直接转换为数值，而任何不能被转换为数值的值都会导致这个函数返回true。

```
isNaN(NaN);        // true
isNaN(Number.NaN); // true
isNaN(0 / 0)       // true

// e.g. these would have been true with global isNaN()
Number.isNaN("NaN");      // false
Number.isNaN(undefined);  // false
Number.isNaN({});         // false
Number.isNaN("blabla");   // false

// These all return false
Number.isNaN(true);
Number.isNaN(null);
Number.isNaN(37);
Number.isNaN("37");
Number.isNaN("37.37");
Number.isNaN("");
Number.isNaN(" ");
```

将非数值转换为数值：Number()、parseInt()、parseFloat()

**Number() 可用于任何数据类型**
### 转换规则：

 - Boolean值：true false分别转换为1 0
 - 数字值：简单的传入和返回
 - null值：0
 - undefined值：返回NaN
 - 字符串：
	 - 只包含数字（包括前面带正、负号）则转换为十进制数值
	 - 包含有效的浮点格式，如“1.1”，则转换为对应的浮点数
	 - 包含有效的十六进制格式，如“0xf”，则转换为相同大小的十进制整数
	 - 字符串为空，则转换为0
	 - 字符串中包含除上述格式之外的字符，则转换为NaN
 - 若为对象，则调用对象的valueof()方法，然后依照前面的规则转换返回值。若转换的结果是NaN，则调用对象的toString()方法，然后再次依照前面的规则转换返回值。

```
var num1 = Number("hello world!"); //NaN
var num2 = Number("");             //0
var num3 = Number("000011");       //11
var num4 = Number(true);           //1

//处理整数常用parseInt()函数
var num1 = parseInt("1234blue"); //1234
var num2 = parseInt("");         //NaN
var num3 = parseInt("0xA");      //10
var num4 = parseInt(22.5);       //22
var num5 = parseInt("070");      //ECMAScript 3 认为是56 八进制，ECMAScript 5 认为是70 十进制
var num6 = parseInt("70");       //70 十进制
var num7 = parseInt("0xf");      //15

//处理浮点数常用parseFloat()函数
var num1 = parseFloat("1234blue"); //1234
var num3 = parseFloat("0xA");      //0
var num4 = parseFloat("22.5");     //22.5
var num5 = parseFloat("22.34.5");  //22.34
var num6 = parseFloat("0908.5");   //908.5
var num7 = parseFloat("3.125e7");  //31250000
```

----------


## String类型

1、JavaScript的字符串类型用于表示文本数据。它是一组16位的无符号整数值的“元素”。
2、在字符串中的每个元素占据了字符串的位置。第一个元素的索引为0，下一个是索引1，依此类推。字符串的长度是它的元素的数量
3、与 C 语言不同，JavaScript 中字符串是不可变的（译注：如，JavaScript 中对字符串的操作一定返回了一个新字符串，原始字符串并没有被改变）
Javascript中一切都是object-based。

### 创建string，也有两种类型

 1. 使用字面量方式创建的字符串，为基本类型的 string              
	 - 实际上保存就是的值，是一个基本类型 
 2. 使用String()创建的字符串，为基本类型的 string     
 3. 使用构造函数 new String()的方式创建的字符串，为对象类型的 string  
	 - 实际上保存的是一个指向字符串对象的指针

### 转换为字符串

 - 第一种方法：toString() 返回相应值的字符串表现（null与undefined值没有这个方法）
 - 第二种方法：在不知道转换的值是不是null或undefined情况下，可以用转型函数String()，能将任何类型的值转换为字符串。

----------


## Object类型

数据和功能的集合。是所有对象的基础，所有对象都具有Object的基本属性和方法。

```
var o = new Object();

var o = new Object; // 有效，但不推荐省略圆括号
```

### ①constructor属性
构造函数属性,可确定当前对象的构造函数。

```
var o = new Object();
console.log(o.constructor == Object);//true
var arr = new Array();
console.log(arr.constructor == Array);//true
```

### ②hasOwnProperty(propertyName)
判断属性是否存在于当前对象实例中（而不是在实例的原型中）。
### ③isPrototypeOf(object)
判断传入的对象是否是当前对象的原型
### ④propertyIsEnumerable(propertyName)
判断给定的属性是否能使用for-in语句来枚举
### ⑤toLocaleString()
返回对象的字符串表示，该字符串与执行环境的地区对应
### ⑥toString()
返回对象的字符串表示
### ⑦valueOf()
返回对象的字符串、数值或布尔值表示


----------


## Symbol类型

ES6引入了一种新的原始数据类型Symbol，表示独一无二的值。 可以从根本上防止属性名的冲突。

Symbol值通过Symbol函数生成。这就是说，对象的属性名现在可以有两种类型，一种是原来就有的字符串，另一种就是新增的Symbol类型。凡是属性名属于Symbol类型，就都是独一无二的，可以保证不会与其他属性名产生冲突。

```
let s = Symbol();
typeof s            // "symbol"
```

上面代码中，变量s就是一个独一无二的值。typeof运算符的结果，表明变量s是 Symbol 数据类型，而不是字符串之类的其他类型。

> 注意， Symbol 函数前不能使用 new 命令，否则会报错。这是因为生成的  Symbol 是一个原始类型的值，不是对象。也就是说，由于 Symbol  值不是对象，所以不能添加属性。基本上，它是一种类似于字符串的数据类型。

Symbol函数可以接受一个字符串作为参数，表示对 Symbol 实例的描述，主要是为了在控制台显示，或者转为字符串时，比较容易区分。

```
var s1 = Symbol('foo');
var s2 = Symbol('bar');
s1 // Symbol(foo)
s2 // Symbol(bar)
s1.toString() // "Symbol(foo)"
s2.toString() // "Symbol(bar)"
```

上面代码中，s1和s2是两个 Symbol 值。如果不加参数，它们在控制台的输出都是Symbol()，不利于区分。有了参数以后，就等于为它们加上了描述，输出的时候就能够分清，到底是哪一个值。

> 注意，Symbol 函数的参数只是表示对当前 Symbol 值的描述，因此相同参数的 Symbol 函数的返回值是不相等的。

```
//  没有参数的情况
var s1 = Symbol();
var s2 = Symbol();
s1 === s2 // false

//  有参数的情况
var s1 = Symbol("foo");
var s2 = Symbol("foo");
s1 === s2 // false
```

上面代码中，s1和s2都是Symbol函数的返回值，而且参数相同，但是它们是不相等的。

由于每一个Symbol值都是不相等的，这意味着Symbol值可以作为标识符，用于对象的属性名，就能保证不会出现同名的属性。这对于一个对象由多个模块构成的情况非常有用，能防止某一个键被不小心改写或覆盖。Symbol值作为对象属性名时，不能用点运算符。在对象的内部，使用Symbol值定义属性时，Symbol值必须放在方括号之中。

```
var mySymbol = Symbol();
//  第一种写法
var a = {};
a[mySymbol] = 'Hello!';
//  第二种写法
var a = {
[mySymbol]: 'Hello!'
};
//  第三种写法
var a = {};
Object.defineProperty(a, mySymbol, { value: 'Hello!' });
//  以上写法都得到同样结果
a[mySymbol] // "Hello!"
```

**Symbol 值不能与其他类型的值进行运算，会报错。**

```
var sym = Symbol('My symbol');
"your symbol is " + sym
// TypeError: can't convert symbol to string
`your symbol is ${sym}`
// TypeError: can't convert symbol to string
```

但是， Symbol 值可以显式转为字符串。

```
var sym = Symbol('My symbol');
String(sym) // 'Symbol(My symbol)'
sym.toString() // 'Symbol(My symbol)'
```

### Symbol.for() ， Symbol.keyFor()

有时，我们希望重新使用同一个 Symbol 值，Symbol.for方法可以做到这一点。它接受一个字符串作为参数，然后搜索有没有以该参数作为名称的Symbol 值。如果有，就返回这个 Symbol 值，否则就新建并返回一个以该字符串为名称的 Symbol 值。

```
var s1 = Symbol.for('foo');
var s2 = Symbol.for('foo');
s1 === s2 // true
```

上面代码中， s1 和 s2 都是 Symbol 值，但是它们都是同样参数的Symbol.for方法生成的，所以实际上是同一个值。

Symbol.for()与Symbol()这两种写法，都会生成新的 Symbol 。
**区别：**
前者会被登记在全局环境中供搜索，后者不会。

 - Symbol.for()不会每次调用就返回一个新的 Symbol 类型的值，而是会先检查给定的 key 是否已经存在，如果不存在才会新建一个值。比如，如果你调用

```
Symbol.for("cat") 30次，每次都会返回同一个 Symbol 值，但是调用Symbol("cat") 30 次，会返回 30 个不同的 Symbol 值。
Symbol.for("bar") === Symbol.for("bar")
// true
Symbol("bar") === Symbol("bar")
// false
```

上面代码中，由于Symbol()写法没有登记机制，所以每次调用都会返回一个不同的值。

 - Symbol.keyFor 方法返回一个已登记的 Symbol 类型值的 key 。

```
var s1 = Symbol.for("foo");
Symbol.keyFor(s1) // "foo"
var s2 = Symbol("foo");
Symbol.keyFor(s2) // undefined
```

上面代码中，变量s2属于未登记的 Symbol 值，所以返回undefined。

> 需要注意的是，Symbol.for为 Symbol 值登记的名字，是全局环境的，可以在不同的 iframe 或 service worker中取到同一个值。
