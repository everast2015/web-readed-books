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
 A1 | B1 | C1
 A2 | B2 | C2
 A3 | B3 | C3