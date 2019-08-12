---
title: 'CSS快速入门'
abbrlink: '0'
tags: 
    CSS
categories:
    CSS
---
## 入门语法介绍

### box-sizing属性

box-sizing,可以设定元素的大小该如何计算，包括两个属性：content-box 与 border-box

``` bash
div {
    boc-sizing: content-box;
}
```

上面的代码box-sizing的默认值是content-box,对元素设置所设定的宽度会应用到该元素的内容上，而填充和边框会照常加上去
如果把值设置为border-box，则意味着设定的width值是内容、填充和边框的总宽度
![12](./assets/1.png)
示例如下：

``` bash
div {
    border: 10px solid black;
    box-sizing: border-box;
    padding: 10px;
    width: 150px;
}
```

现在150px的宽度包括了填充和边框，二者在内容两侧都占据了10px，所以div元素的内容计算宽度就是110px，即150px减去20px的填充和20px的边框
对于Firefox来说，关于它的-moz-box-sizing属性，有额外的padding-box属性，使用这个值，计算元素属性时会对它的填充和内容进行计算，不包括边框
