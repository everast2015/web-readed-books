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