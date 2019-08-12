---
abbrlink: '1'
title: 'DOM选择器'
tags: 
    CSS
categories:
    CSS
---
## 属性选择器

属性选择器是在CSS2中引入的，他们能够指定一些规则，这些规则根据元素的属性（诸如href或title）以及这些属性的值对元素进行匹配

``` bash
<ul>
    <li><a href="" lang="en-GB" rel="friend net">Peter</a></li>
    <li><a href="" lang="es-ES" rel-"fiend">Pedro</a></li>
    <li><a href="" lang="es-MX" rel-"contact">Pancho</a></li>
</ul>
```

### 简单属性选择器

将规则应用到定义了指定属性的元素上，而不管属性的值是什么

``` bash
a[rel] {
    color: red;
}
```

由于所有元素都有rel属性，所以所有元素都会应用这条规则

### 精确属性值选择器

``` bash
a[rel='friend'] {
    color: red;
}
```

这个代码只会将规则标记到第二个a元素

### 部分属性选择器

``` bash
a[rel~='friend'] {
    color: red;
}
```

这个代码会选择rel属性中带有friend的值的元素，则这个规则会标记到第一与第二个

### 语言属性选择器

``` bash
a[lang|='es'] {
    color: red;
}
```

选中所有属性值以es开头的lang语言，即会选中2和3

## CSS3的新属性选择器

### 开始字串属性值选择器（开始选择器）

该选择器会选择一些元素，这些元素所选择的属性是以一个字符串为起始，该字符串会作为参数提供给选择器，这个选择器使用插入符号(^)修饰属性中的等号

``` bash
E[attr^='value'] {}
```

这行代码将在指定属性的起始处寻找指定的值
示例如下：

``` bash
<p>Lorem ipsum dolor <a href="mailto:email@example.com">email<a> sit amet.</a></p>
<style>
a[href^='mailto'] {
    background-image: url('email_go.png');
}
</style>
```

输出结果为：

``` bash
Lorem ipsum dolor email sit amet.  #这里的email是一个地址即上述href绑定的地址 email原为一图片索引，本人懒就没放图片
```

### 结束子串属性值选择器（结束选择器）

与开始选择器相反，使用该选择器去选择以指定的值结束的属性
语法差异为用($)去修饰(=)

### 任意子串属性值选择器（任意选择器）

该选择器使用规则即在指定的属性字符串的内部任意位置搜索指定的子串
该选择器使用的符号是(*)

### 多属性选择器

可以把多个选择器串接在一起，这样在选择目标的时候能够做到非常的具体，使用多选择器，可以通过定义在开始、结束以及中间任意位置的值创建应用到属性上的规则

 ``` bash
 <p><a href="http://example.com/folder1/file.pdf">Lorem ipsum</a></p>
 <p><a href="http://example.com/folder2/file.pdf">Lorem ipsum</a></p>
 ```

 如果要指定一条只应用到第二个p元素的规则，可以把一些选择器串接到一起：

 ``` bash
 a[href^='http://'][href*='/folder2/'][href$='.pdf'] {}
 ```

这行代码会寻找这样的a元素，它具有一个href属性，是以 http: // 开始，以.pdf结束，并且在中间包含了/folder2/，非常明确

### 普通兄弟连结符

``` bash
E + F {} #相邻兄弟连结符
E ~ F {} #普通兄弟连结符
```

相邻兄弟连结符选择的是文档树的同一层级，紧邻在元素(E)之后的任意元素；
普通兄弟连结符选择的是文档树的同一层级，位于元素(E)之后的任意元素。
示例如下：

``` bash
<p>Next we are going to discuss ... </p>
<h2>Ren&eacute; Descartes</h2>
<p>A highly influential French philosopher...</p>
<p>He only famously declared:</p>
<blockquote>
    <p>I think,therefore I am.</p>
</blockquote>  
<p>However,this presumes the existence of the speaker.</p>
<style>
h2 + p {
    font-weight:bolder;
}
h2 ~ p {
    font-style: italic;
}
</style>
```

输出结果如下：
