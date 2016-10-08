不管你写什么语言，都应该保持良好、一致的代码风格;写CSS的时候，你可以遵循下面的规范：

* 用两个空格来代替制表符（tab）
>这是唯一能保证所有环境下表现一致的方法
* 一行最多允许80个字符
* 多行书写CSS
* 利用空白符分割模块

上边的这几条规范可能并不适合每一个人，真正关键的是，你能够严格遵循某一套规范，保持代码的一致性。

### 拆分成多个文件

现在随着预处理器的流行，将CSS拆分到多个不同的文件来组织也越来越普遍。

即使不使用预处理器，拆分CSS，而不是把所有代码写到一个文件里边也是一个好习惯。


### 维护一个目录

维护目录其实需要花费大量的时间，写完代码，你还要回来更新目录；额，不得不说，原作者肯定是个很勤奋的人，维护目录也确实还是有很多好处，直接看目录，你就知道这个CSS是干嘛的，有哪些内容，以及代码的顺序是怎样的。给你一份很长的css代码，看了目录你就明白有哪些模块功能，每个模块大概在什么位置。（各位自行权衡利弊吧，小型项目可能帮助不是很大，大型项目确实是个好方法）

```
/**
 * CONTENTS
 *
 * SETTINGS
 * Global...............Globally-available variables and config.
 *
 * TOOLS
 * Mixins...............Useful mixins.
 *
 * GENERIC
 * Normalize.css........A level playing field.
 * Box-sizing...........Better default `box-sizing`.
 *
 * BASE
 * Headings.............H1–H6 styles.
 *
 * OBJECTS
 * Wrappers.............Wrapping and constraining elements.
 *
 * COMPONENTS
 * Page-head............The main page header.
 * Page-foot............The main page footer.
 * Buttons..............Button elements.
 *
 * TRUMPS
 * Text.................Text helpers.
 */
  
```

### 一行最多允许80个字符

之所以限制宽度在80个字符，主要有以下几个原因：

* 方便你在分屏的时候编写、查看代码
* 在github或者终端中查看（这个需求其实没那么重要。。。）
* 让你的注释更易阅读

> **译者注：**好吧，其实上边的理由对我来说说服力不够，但是平时写代码，确实是设置在每行最多80个字符，主要是为了防止有时候代码太长（但是对CSS来说，貌似只有常见的只有三种情况会出现，1. 设置`font` 2. 图片链接 3. 注释），要是写代码的时候还需要左右拖动滚动条就太不爽了。

``` 
/**
 * I am a long-form comment. I describe, in detail, the CSS that follows. I am
 * such a long comment that I easily break the 80 character limit, so I am
 * broken across several lines.
 */
```


### 标题

为每一个新的模块（section）添加标题

``` 
/*------------------------------------*\ 
 #SECTION-TITLE
\*------------------------------------*/

.selector { }
```

每个标题前加上(`#`)作为前缀，方便精确查找。

标题（注释）和代码之间用一个回车换行分隔，表明这是一个注释。

如果我们将每一个模块都写在单独的CSS文件中，那在文件开头就是注释标题；如果一个文件中包含多个模块，模块之间用5个回车换行分隔。通过回车换行以及注释标题，方便查找定位。

```
/*------------------------------------*\
 #A-SECTION
\*------------------------------------*/

.selector { }




/*------------------------------------*\
 #ANOTHER-SECTION
\*------------------------------------*/

/**

 * Comment

 */

.another-selector { }
```

### 语法

在讨论我们的语法规范之前，先看一下一些术语的定义：

```
[selector] {
 [property]: [value];
 [<--declaration--->]
}
```

例如：

```
.foo, .foo--bar,
.baz {
 display: block;
 background-color: green;
 color: red;
}

```

你可以看到：

* 有关联的选择器放在一行；而不相关的选择器在新的一行
* `{`前有一个空格
* 属性以及属性值在同一行
* `:`和属性值之间用一个空格分隔
* 每条声明单独占一行
* `{`和最后一个选择器处于同一行，不换行
* 第一条声明语句在`{`的下一行
* `}`单独占一行
* 每条声明语句缩进2个空格
* 在声明语句后添加`;`

根据上面的规范，下面的写法存在很多问题：

```
.foo, .foo--bar, .baz
{
   display:block;
   background-color:green;
   color:red }
```

* 用的是`tabs`而不是空格
* 不相关的选择器也放在了同一行
* `{`单独在一行
* `}`没有单独占一行
* 结尾的';'没有（当然，这并不是硬性要求）
* `:`后没有空格

### 多行编写

除了一些特殊场景，我们都应该在多行编写CSS，每一行写一条规则。

好处在于：

* 每一行都是一个单独的规则，减少样式规则之间的冲突（译者注：考虑对同一个属性设置多次的情况）
* diffs更加清楚，一行对应一个规则的改动

但是，在遇到只有一条规则的情况下，我们直接写在一行：

```
.icon {
 display: inline-block;
 width: 16px;
 height: 16px;
 background-image: url(/img/sprite.svg);
}

.icon--home { background-position: 0 0 ; }
.icon--person { background-position: -16px 0 ; }
.icon--files { background-position: 0 -16px; }
.icon--settings { background-position: -16px -16px; }
```

这样写的好处是因为：

* 因为只有一条规则，所以仍然保证了一行对应一条规则的原则
* 这些规则很相似，没必要像普通样式那样一行一行读，这个时候选择器更值得关注。

### 缩进

这里强调的缩进是指有相互关系的选择器之间的缩进，通过缩进来表明他们之间的联系，比如：

```
.foo {}
  .foo__bar {}
    .foo__baz {}
```

这样的缩进反应出`HTML`的结构，不需要查看`HTML`代码段，开发人员马上就能知道如何使用CSS类，`.foo__baz{}`在`.foo__bar`内，`.foo__bar`在`.foo{}`中。

#### Sass中的缩进

Sass支持嵌套，我们直接这样写：

```
.foo {
 color: red;

 .bar {
 color: blue;
 }

}
```

编译后的结果：

```
.foo { color: red; }
.foo .bar { color: blue; }
```

在Sass中，我们的缩进仍然采用两个空格，并且在嵌套的样式前后都留有一个空行。

**注意**：在Sass中避免非必要的嵌套

#### 对齐

当使用特定厂商带有前缀的属性时，利用缩进让属性保持对齐：

```
.foo {
  -webkit-border-radius: 3px;
  -moz-border-radius: 3px;
      border-radius: 3px;
}

.bar {
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  margin-right: -10px;
  margin-left: -10px;
  padding-right: 10px;
  padding-left: 10px;
}
```

这样在进行多行编辑的时候将非常方便（如果你的编辑器支持多行编辑）。

### 有意义的空行

和缩进一样，空行也能表达有用的信息：

* 1个空行：紧密相关的样式集之间
* 2个空行：弱相关的样式集之间
* 5个空行：不同模块之间

例子：

```
/*------------------------------------*\
 #FOO
\*------------------------------------*/

.foo { }

  .foo__bar { }


.foo--baz { }





/*------------------------------------*\
 #BAR
\*------------------------------------*/

.bar { }

  .bar__baz { }

  .bar__foo { }

```

在所有的样式集之间都要用空行分隔；错误写法：

```
.foo { }
  .foo__bar { }
.foo--baz { }

```

### HTML

考虑到`HTML`和`CSS`的紧密联系，讲了`CSS`的格式规范，`HTML`的规范也是必可不少的：

> 译者注：原文这部分内容实用性以及参考价值不是很大，这里直接放上原文，不感兴趣的同学可以直接跳过

Given HTML and CSS’ inherently interconnected nature, it would be remiss of me to not cover some syntax and formatting guidelines for markup.

Always quote attributes, even if they would work without. This reduces the chance of accidents, and is a more familiar format to the majority of developers. For all this would work (and is valid):

```
<div class=box>
```

…this format is preferred:

```
<div class="box">
```

The quotes are not required here, but err on the safe side and include them.

When writing multiple values in a class attribute, separate them with two spaces, thus:

```
<div class="foo bar">
```

When multiple classes are related to each other, consider grouping them in square brackets ([ and ]), like so:

```
<div class="[ box box--highlight ] [ bio bio--long ]">
```

This is not a firm recommendation, and is something I am still trialling myself, but it does carry a number of benefits. Read more in Grouping related classes in your markup.

As with our rulesets, it is possible to use meaningful whitespace in your HTML. You can denote thematic breaks in content with five (5) empty lines, for example:

```
<header class="page-head">
 ...
</header>





<main class="page-content">
 ...
</main>





<footer class="page-foot">
 ...
</footer>
```

Separate independent but loosely related snippets of markup with a single empty line, for example:

```
<ul class="primary-nav">

 <li class="primary-nav__item"> <a href="/" class="primary-nav__link">Home</a> </li>

 <li class="primary-nav__item primary-nav__trigger"> <a href="/about" class="primary-nav__link">About</a>

 <ul class="primary-nav__sub-nav"> <li><a href="/about/products">Products</a></li> <li><a href="/about/company">Company</a></li> </ul>

 </li>

 <li class="primary-nav__item"> <a href="/contact" class="primary-nav__link">Contact</a> </li>

</ul>
```

This allows developers to spot separate parts of the DOM at a glance, and also allows certain text editors—like Vim, for example—to manipulate empty-line-delimited blocks of markup.

#### Further Reading

[Grouping related classes in your markup]()











