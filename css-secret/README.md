# 《css揭秘》

## 第二章 半透明边框
1. 半透明边框代码的实现：

```css
div {
      border: 10px solid hsla(0, 0%, 100%, .5);
      background: white;
      background-clip: padding-box;
}

```
`background-clip` 设置元素的背景是否延伸到边框下面

2. 多重边框

- `box-shadow` 解决方案

```css
      background: yellowgreen;
      box-shadow: 0 0 0 10px #655;
```

不过`box-shadow` 的好处在于，它支持逗号分隔语法，我们可以创建任意数量的投影，因此我们可以非常轻松地在上面的示例中再加上一道`deeppink` 颜色的“边框”：

```css
      background: yellowgreen;
      box-shadow: 0 0 0 10px #655, 0 0 0 15px deeppink;
```

![box-shadow](https://github.com/yjn2015/web-readed-books/blob/master/css-secret/img/box-shadow.png)

- `outline` 解决方案

```css
      background: yellowgreen;
      border: 10px solid #655;
      outline: 5px solid deeppink;
```

最后的效果：

![outline](https://github.com/yjn2015/web-readed-books/blob/master/css-secret/img/outline.png)

3. 灵活的背景定位

- `background-position` 扩展语法方案

`background-position` 属性已经得到扩展，它允许我们指定背景图片距离任意角的偏移量，只要我们在偏移量前面指定关键字。

举个栗子，我们想要背景图片距离右边缘保持`20px` 的偏移量，同时跟底边保持`10px`的偏移量，可以这样做。

```css
      background: url(code-pirate.svg) no-repeat #58a;
      background-position: right 20px bottom 10px;
```

效果图：

![outline](https://github.com/yjn2015/web-readed-books/blob/master/css-secret/img/background-position.png)

- `calc() 方案`

* 注意：请不要在`calc()` 函数内部的 `-` 和 `+` 运算符的两侧各加一个空白符，否则会产生解析错误！这个规则如此怪异，是为了向前兼容：未来，在`calc()` 内部可能会允许使用关键词，而这些关键词可能会含有连字符（即减号）

4. 边框内圆角

```html
      <div class="something-meaningful">
            <div>
                  内部有圆角，是不是看起来很棒。
            </div>
      </div>
```

```css
      .something-meaningful {
            padding: .8em;
            background: #655;
      }
      .something-meaningful > div {
            padding: 1em;
            border-radius: .8em;
            background: tan;
      }
```

## 第三章 形状