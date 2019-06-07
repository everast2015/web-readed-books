# 《精妙绝伦的css》

## 第二部分 选择器

### 伪类和伪元素

`css2.1` 中伪类有：  
- `:link`未访问过的链接
- `:visited` --访问过的链接
- `:hover` --鼠标悬停的元素
- `:focus` --获取焦点的元素
- `:active` --激活的元素
- `:first-child` --作为其他元素第一个元素的子元素
- `:lang()` 根据元素的`lang` 属性确定的元素

`css3` 中添加的伪类有：
- `:target`
- `:root`
- `:nth-child`
- `:nth-of-type`
- `:nth-last-of-type`
- `:first-of-type`
- `:last-of-type`
- `:only-of-type`
- `:last-child`
- `:empty`
- `:not`
- `:enabled`
- `:disabled`
- `:checked`

`css2.1` 中的伪元素有：
- `::first-line`
- `::first-letter`
- `::before`
- `::after`

他们主要的区别就是影响文档的方式不同，伪类的表现有点儿像给文档添加类，而伪元素的效果好像有元素被插入到文档中。

### 特殊性

特殊性是一个选择器“特殊程度”的数字代表，有三样东西经常被用来确定选择器的特殊性

- 每个元素描述符贡献为：0,0,0,1
- 每个类、伪类或者属性描述符贡献为：0,0,1,0
- 每个ID描述符贡献为：0,1,0,0

先不要抓狂，先来看几个小例子


标签 | 权重 | 描述
---------|----------|---------
 div ul ul li | 0,0,0,4 | 4个元素描述符
 div.aside ul li | 0,0,1,3 | 1个类描述符，3个元素描述符
 #title | em |  一个ID描述符，1个元素描述符


 ## 第三部分提示

 尽量避免的情况：

 1. 尽量避免无单位的行高值，行高是可以继承的，不写单位的话，后代是不可以继承父亲的行高值的。
 2. 避免缺少样式的边框值，这里的边框值指的是`border-style` 的属性
 ```
 form {
   border: 2px skyblue;
 }
 ```

  这里的边框的样式是不会出来的，主要的原因就是缺少了`border-style` 的属性，所以使用默认的属性的值，默认的属性的是`border-style: none;` 所以边框的效果是不出来的。

3. 使用颜色控制边框外观

主要的原因的就是使用内外阴影的来控制的话，例如`inset` 或者 `outset` 的话，各个浏览器的厂商的渲染的效果是不一样的，这样的话，我们就需要考虑兼容性的问题，所以建议的话，还是使用颜色值进行替换。

4. 控制元素的显示

`display: none;` 两个不好的地方。

1. 一个是潜在的
2. 一个是固有的


## 打印样式

打印的图片和输出的样式一致的解决的方案：

```
<style type="text/css" media="print"></style>

<link media="print" href="print.css">

@import url(print.css) print;
```

打印的时候不打印背景的解决方案：

```
* {
    background: transparent;
    color: black;
}
```

或者说是可以列出全部需要调整的样式，像这样。

body,#navbar,.warning,.blockquote {
    background: transparent;
    color: black;
}

## 通过背景实现列表标记

```
ul.stars {
    list-style: none;
}
ul.stars li {
    background: url(star.gif) 0 0 .1em no-repeat;
    padding-left: 16px;
}
```

## 不可不知的容器

```
<div class="wrapper">
</div>
```


```
body {
  backgorund: #ABACAB;
  text-align: center;
}

.wrapper {
  width: 800px;
  margin: 0 auto;
  text-align: center;
}
```

这是个兼容老版本的`IE`的居中设计技术，老版本的`IE` 并不识别靠左右外边距实现自动居中，但却认为文本居中`text-align: center`可以用来居中显示快元素。

我们也可以把之前的规则稍微修改一下：

```
html {
  background: #ABACAB;
  text-align: center;
}

body {
  width: 800px;
  margin: 0 auto;
  text-align: left;
}
```


## 第四章 居中块状框

1. 定宽 + margin

```
div#main {
    width: 1200px;
    margin: 0 auto;
}
```
之所以能这样做是因为`css` 规范中说明，当一个元素有特定的宽度，并且左右外边距都是自动确定时，浏览器会取元素和容器的宽度之差，除以二后分别应用在元素的左外边距和右外边距上，因此，元素就居中了。

当然，这不会使那个框中的文字也跟着居中，如果需要文字进行居中，就需要添加一个属性
`text-align: center`

## 遏制浮动的方法

1. 通过溢出遏制浮动
2. 通过浮动遏制浮动
3. 清除浮动

代码：

```css
    .clearfix {
        display: block;
        clear: left;
        font-size: 0;
        height: 0;
        visibility: hidden;
        margin: -0.66em 0;
    }
```

## 简单的两栏布局

1. 浮动 + 宽度

```html
    <div class="columns left">
        左边内容
    </div>
    <div class="columns right">
        右边内容
    </div>

```

```css
    .columns {
        float: right;
        width: 50%;
    }
```