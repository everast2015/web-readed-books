# 《javascript 权威指南》

## 对象

创建对象的几种方式：
1. 对象直接量
2. 关键字new
3. `ES5`的`Object.create()` 函数

- 对象直接量

创建对象直接量最简单的方法就是使用一个花括号进行创建。
```js
var empty = {}; // 创建一个空的对象
```

对象直接量是由若干名/值对组成的映射表，名/值对中间用冒号隔开，整个映射表用花括号括起来。

- 通过 `new` 创建对象。

```js
var object = new Object();

```

这里的函数称为构造函数`constructor`，构造函数用以初始化一个新创建的对象。

- `Object.create()` 

`ES5` 定义了一个名为`Object.create()` 的方法，它创建了一个新对象，其中第一个参数是这个对象的原型，第二个可选参数，用以对对象的属性进行进一步的描述。

```js
var o1 = Object.create({
    x:1,
    y:1
});
```

### 属性的设置和查询
在`js` 中可以通过点`(.)`或方括号`[]` 运算符来获取对象的属性的值。
获取属性的值：
```js
var author = book.author;
var title = book['main title'];
```
设置属性的值：
```js
book.author = "you name";
book['main title'] = "ECMASCRIPT";
```

### 删除属性
`delete` 运算符可以删除对象的属性。
```js
delete book.author; // book 不再有属性 author
delete book["main title"]
```
`delete` 运算符只能删除自有属性，不能删除继承属性（要删除继承属性必须是从定义这个属性的原型对象是哪个删除它，而已这会影响到所有继承自这个原型的对象）。

### 检查属性
判断某个属性是否存在与对象中，可以通过`in` 运算符、`hasOwnPreperty()` 和 `propertyIsEnumerable()` 方法来完成这个工作。

```js
var o = {x: 1}
o.hasOwnProperty("x"); // true 0有一个自有属性x
o.hasOwnproperty("y"); // false o 不存在自有属性 y
```
![对象](https://github.com/yjn2015/web-readed-books/blob/master/js-anthoritative/object.png)

## 作用域

作用域指一个变量的作用的范围

在`js` 中一共有两种作用域：

1. 全局作用域
- 直接写在`<script></script>` 标签中的`JS`代码，都在全局作用域。
- 全局作用域在页面打开时创建，在页面关闭时销毁。
- 在全局作用域中有一个全局对象`window`
> 它代表的是一个浏览器的窗口，它由浏览器创建，我们可以直接使用

- 在全局作用域中

1. 创建的变量都会作为`window`的属性保存起来
2. 创建的函数都将作为`window`对象的方法保存起来。

### 变量的声明提前
