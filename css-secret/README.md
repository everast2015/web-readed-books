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

1. 自适应的椭圆
```
border-radius: 50%;
```
* 四分之一椭圆

> 要创建一个4/1 椭圆，其中一个角的水平和垂直半径都需要是100%，而其他三个角都不能设置为圆角。

```
border-radius: 100% 0 0 0;
```
![四分之一椭圆](https://github.com/yjn2015/web-readed-books/blob/master/css-secret/img/border-radius.png)


2. 平行四边形

问题描述：

对于平行四边形的问题，有没有办法只让容器的形状倾斜，而保持其内容不变呢？

- 方法一、嵌套解决方案

我们可以在应用一次反向的`skew()`变形，从而抵消容器的变形效果。

```html
<a href="#" class="button">
      <div> Click me </div>
</a>
```

```css
      .button {
            transform: skewX(skewX(-45deg));
      }
      .button > div {
            transform: skewX(45deg);
      }
```

最终的效果图：

![平行四边形](https://github.com/yjn2015/web-readed-books/blob/master/css-secret/img/sbx.png)

- 方法二、伪元素方案

实现的思路：

另一种思路是把所有样式（背景、边框）都应用到伪元素上，然后在对伪元素进行变形，因为我们的伪元素不是包含在伪元素内的，所以内容并不会收到影响。

```css
.button {
      position: relative;
      /* 其他文字颜色，内边距等样式 */
} 
.button::before {
      /* 用伪元素来生成一个矩形 */
      content:'';
      position: absolute;
      top: 0;
      right: 0;
      bottom: 0;
      left: 0;
      z-index: -1;
      background: #58a;
      transform: skewX(-45deg);
}
```
![伪元素方案效果图](https://github.com/yjn2015/web-readed-books/blob/master/css-secret/img/other-sbx.png)

3. 菱形图片

- 基于变形的解决方案

需要把图片把一个`<div>` 包裹起来，然后对其应用相反的`rotate()`变形样式;

```html
      <div class="picture">
            <img src="./img/bg-position.jpg" alt="icon">
      </div>
```

```css
      .picture {
            width: 200px;
            transform: rotate(45deg);
            overflow: hidden;
      }
      .picture > img {
            max-width: 100%;
            transform: rotate(-45deg) scale(1.42);
      }
```
![伪元素方案效果图](https://github.com/yjn2015/web-readed-books/blob/master/css-secret/img/lingxing.png)

4. 切角效果

解决方案：

`css` 渐变，我们只需要一个线性渐变就可以达到目标，这个渐变需要把一个透明色标放在切角处，然后在相同位置设置另一个色标，并把其颜色设置为我们需要的背景色

```css
      background: #58a;
      background: linear-gradient(-45deg, transparent 15px, #58a 0);

```

最终效果：

![切角方案效果图](https://github.com/yjn2015/web-readed-books/blob/master/css-secret/img/qiejiao.png)

- 两个切角的效果

两个切角的效果的话，主要在多加一层渐变，默认情况下，这两层渐变都会填充满整个元素，因此他们会互相覆盖，需要把他们的背景图都缩小一半，分别占据整个元素的一半的面积。

相关代码：

```css
background: #58a;
background: linear-gradient(-45deg, transparent 15px, #58a 0) right,linear-gradient(45deg, transparent 15px, #655 0) left;
background-size: 50% 100%;
background-repeat: no-repeat;

```

最终的效果：

![切角方案效果图](https://github.com/yjn2015/web-readed-books/blob/master/css-secret/img/fourqiejiao.png)


- 弧形切角（内凹圆角）

实现的原理：

主要使用的方法就是径向渐变代替线性渐变。


上代码:

```css
background: #58a;
background: radial-gradient(circle at top left, transparent 15px, #58a 0 ) top left,radial-gradient(circle at top right, transparent 15px, #58a 0 ) top right,radial-gradient(circle at bottom left, transparent 15px, #58a 0 ) bottom left,radial-gradient(circle at bottom right, transparent 15px, #58a 0 ) bottom right;
background-size: 50% 50%;
background-repeat: no-repeat;
```

最终效果：

![切角方案效果图](https://github.com/yjn2015/web-readed-books/blob/master/css-secret/img/circlefour.png)



5. 梯形标签页

解决方案：

可以利用2D变形属性可以生成一个梯形

对元素使用了3D变形之后，其内部的变形效果是“不可逆转的”，这一点跟2D变形不同，唯一可行的途径就是把变形效果作用在伪元素上。这有些类似与我们在“平行四边形”一节中生成的平行四边形的方法。

上代码：

```css
      .tab {
            position: relative;
            display: inline-block;
            padding: .5em 1em .35em;
            color: white;
      }
      .tab::before {
            content: '';
            position: absolute;
            top: 0;
            right: 0;
            bottom: 0;
            left: 0;
            background: #58a;
            transform: perspective(.5em) rotateX(5deg);
      }

```

梯形效果图：

![梯形方案效果图](https://github.com/yjn2015/web-readed-books/blob/master/css-secret/img/tx.png)

6. 简单的拼图

- 基于`transform` 的解决方案

上代码：

```html
      <div class="pie"></div>

```

```css
      .pie {
            width: 100px;
            height: 100px;
            border-radius: 50%;
            background: yellowgreen;
            background-image: linear-gradient(to right, transparent 50%, #650 0);
      }
      .pie::before {
            content: '';
            display: block;
            margin-left: 50%;
            height: 100%;
            border-radius: 0 100% 100% 0 / 50%;
            background: #655;
            transform-origin: left;
            transform: rotate(.1turn);
      }
```

拼图效果图：

![梯形方案效果图](https://github.com/yjn2015/web-readed-books/blob/master/css-secret/img/pie.png)

## 第四章 视觉效果

1. 单侧阴影

最终的解决方案是来自`box-shadow` 鲜为人知的第四个长度参数，它排在模糊半径之后，称为扩展半径。这个参数会根据你指定的值扩大（当指定负值时）缩小投影的尺寸。举例来说，一个-5px的扩张半径会把投影的宽度和高度各减少10px（即每边减少5px）

如果我们给投影一个正的垂直偏移量，我们就会在元素的底部看到一道投影，而元素的另外三侧是没有投影的。

```css
      box-shadow: 0 5px 4px -4px black;
```
最终效果图：

![梯形方案效果图](https://github.com/yjn2015/web-readed-books/blob/master/css-secret/img/shadow.png)

 1.2. 邻边投影

 如何在元素的两条边上设置投影。如果这两条边是相邻的，就比较容易一些。

 - 扩展半径不应该设为模糊半径的相反值，而应该是这个相反值的一半。
 - 需要指定两个偏移量，我们希望投影在水平和垂直方法上同时有移动。他们的值需要大于等于模糊半径的一半，因为我们希望把投影藏进另外两条边之内。

 具体的实现的代码：

 ```css
      box-shadow: 3px 3px 6px -3px black;
 ```

 最终效果：

![梯形方案效果图](https://github.com/yjn2015/web-readed-books/blob/master/css-secret/img/single-shadow.png)

1.3. 双侧投影

背景：

当我们想把投影设置在两条对边上时（比如左侧和右侧）时，事情就变得非常棘手，因为扩张半径在四个方向上的作用是均等的（也就是说，我们无法指定投影在水平方法上扩大，而在垂直方向上缩小），唯一的方法就是用两块投影（每边各一块）来达到目的。然后基本上就是把“单侧阴影”中的技巧运用两次。

具体的实现的代码;

```css
      box-shadow: 5px 0 5px -5px black,-5px 0 5px -5px black;
```

最终效果：

![梯形方案效果图](https://github.com/yjn2015/web-readed-books/blob/master/css-secret/img/side-shadow.png)

2. 不规则阴影 

不规则阴影目前采用的方法是滤镜的效果

3. 染色阴影

背景：

使用纯`css` 的方法实现图片染色效果

方法：

基于滤镜的解决方案：

- 第一个滤镜是`sepia()` ，它会给图片添加一种降饱和度的橙黄色染色效果，几乎所有的像素的色相值会被收敛到35-40
- `saturate()` 滤镜来给每个像素添加饱和度
- `hue-rotate()` 滤镜，把每个像素的色相以指定的度数进行偏移。

具体的实现的代码：

```
filter: sepia(1) saturate(4) hue-rotate(295deg);
```

4. 毛玻璃效果

背景：

如果我们在半透明背景颜色的上方添加文字的话，这样文字的可读性将会变色很低

解决的方案：

可以采用滤镜的方式模糊背景

具体的实现的代码：

```css
body(,main::before {
      background: url(tiger.jpg) 0 / cover fixed;
}
.main {
      position: relative;
      background: hsla(0,0%,100%, .3);
      overflow: hidden;
}
.main::before {
      content: '';
      position: absolute;
      top: 0;
      right: 0;
      bottom: 0;
      left: 0;
      filter: blur(20px);
      margin: -30px;
}

```
5. 折角效果

- 方法一、45度折角的解决方案

主要的思路：
  就是使用渐变的方案实现的：
  ```css
    background: #58a;
    background: linear-gradient(-135deg, transparent 2em, #58a 0);
  
  ```

  # 第六章用户体验

  ## 选用合适的鼠标光标

  1. 提示禁用状态

  ```css
      :disabled,[disabled],[aria-disabled="true"] {
            cursor: not-allowed;
      }
  ```

  2. 隐藏鼠标光标

  在`css2.1` 中，隐藏光标也是有可能的，但需要用到一张1x1的透明GIF图片，然后这样做：

  ```css
      video {
            cursor: url(transparent.gif);
      }
  
  ```

  但是现在不需要这样做的了，可以直接使用`cursor: none`;不过为了回退版本，向下兼容，我们可以使用层叠机制来实现这一点。

  ```css
     cursor: url(transparent.gif);
     cursor: none;
  ```

## 扩大可点击的范围

1. 方法一

设置一圈透明边框

```css
      border: 10px solid transparent;
```

但是效果却不是很好，它同时让按钮变大了，原因在于背景在默认情况下回蔓延到边框的下层，简单好用的`background-clip`属性可以把背景限制在原本的区域之内。

```css
      border: 10px solid transparent;
      background-clip: padding-box;
```

但是还存在一个问题就是，当你需要给按钮加上真正的边框的时候，会发现按钮的真正边框被我们挪作他用了，怎么办？很简单，可以用内嵌投影来模拟出一道边框


```css
      border: 10px solid transparent;
      background-clip: padding-box;
      box-shadow: 0 0 0 1px rgba(0,0,0,.3) inset;
```

## 自定义复选框

```html
<input type="checkbox" id="awesome"/>
<label for="awesome">Awesome!</label>
```

```css
input[type="checkbox"] + lable::before {
      content: '\a0;'; /* 不换行空格 */
      display: inline-block;
      width: .8em;
      height: .8em;
      margin-right: .2em;
      border-radius: .2em;
      background: silver;
      text-indent: .15em;
      line-height: .65;

}

/* 设置选中的颜色值 */
input[type="checkbox"]:checked + label::before {
      content: '\2713';
      background: yellowgreen;
}

/* 隐藏原有的元素 */
input[type="checkbox"] {
      position: absolute;
      clip: rect(0,0,0,0);
}
```

## 通过阴影来弱化背景

我们需要一层半透明的遮罩层来把后面的一切整体调暗，最常见的方法是添加一个额外的html元素用于遮罩内容，然后为其添加以下样式。

```css
/* 用于遮罩背景 */
.overlay {
      position: fixed;
      top: 0;
      right: 0； 
      bottom: 0;
      left: 0;
      background: rgba(0,0,0,.8);
}
```



