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

之所以限制宽度在80个字符，主要有一下几个原因：

* 方便你在分屏的时候编写、查看代码
* 在github或者终端中查看（这个需求其实没那么重要。。。）
* 让你的注释好看点

> **译者注：**好吧，其实上边的理由对我来说说服力不够，但是平时写代码，确实是设置在每行最多80个字符，主要是为了防止有时候代码太长（但是对CSS来说，貌似只有三种特殊情况才会出现一行内容太长的情况，1. 设置`font` 2. 图片链接 3. 注释），要是写代码的时候还需要左右拖动滚动条就太不爽了。

``` 
/**
 * I am a long-form comment. I describe, in detail, the CSS that follows. I am
 * such a long comment that I easily break the 80 character limit, so I am
 * broken across several lines.
 */
```


### 标题

CSS中每一个主要的部分都开始于一个标题

 /*------------------------------------*\ #SECTION-TITLE \*------------------------------------*/

 .selector { } 每一部分都标题都是以“`＃`”为前缀，以使我们能够进行更有针对性的搜索（如`grep`等等），而不是只搜索标题名(`SECTION-TITLE`)，那样可能会产生许多搜索结果。在大范围中搜索带“＃”号的标题(`#SECTION-TITLE`)，应该只返回一个所需标题的结果。

在标题和下一行代码之间敲一个回车（中间可以写一写注释或者SASS或者CSS）。

如果你正在的项目里,每一个部分都有自己的文件,那么标题就应该出现在每一个部分的顶部。如果你正在做的项目每个文件包含多个部分,那么每个标题后面最好敲5个回车，这样标题再加上后面多出来的空白区域将会使新的部分在一个大的文件中滚动的时候更容易被发现。

 /*------------------------------------*\ #A-SECTION \*------------------------------------*/

 .selector { }

 /*------------------------------------*\ #ANOTHER-SECTION \*------------------------------------*/

 /** * Comment */

 .another-selector { } ### rulesets的剖析

在我们讨论我们如何书写我们的rulesets之前，让我们先熟悉一下相关术语：

 [selector] { [property]: [value]; [<--declaration--->] }

比如：

 .foo, .foo--bar, .baz { display: block; background-color: green; color: red; }

在这里，你可以看到：

* 相关的选择器写在同一行，不相关的选择器另起一行书写；* 在起始大括号（`{`）之前有一个空格；* 属性名和属性值放在同一行；* 在属性名的冒号（`:`）后，留有一个空格，再接着写属性值；* 每一个声明都开始于新的一行；* 和起始大括号（`{`）同一行的是最后一个选择器；* 第一个声明在起始大括号（`{`）后新的一行；* 结束大括号（`}`）独占新的一行；* 每个声明都缩进两个空格；* 每个声明都以一个分号（`;`）结束；

这种格式似乎是目前通用的标准（除了在空格数量上的变化，许多开发者还是喜欢两个空格）。

像下面代码这样的书写就是不正确的：

 .foo, .foo--bar, .baz { display:block; background-color:green; color:red } 问题点包括：

* 用制表符代替空格；* 不相关的选择器写在了同一行；* 起始大括号（`{`）独占一行；* 结束大括号（`}`）没有独占一行；* 最后的结束的（`;`）丢失（当然，分号是可选的，为了保持一个好习惯，最好还是写上）；* 在冒号（`:`）后面没有空格；

### 多行CSS

CSS应该多行书写，除了在某些非常特殊的情况下，这样写有许多好处：

* 降低代码合并引发冲突的几率，因为每一条样式声明都存在于它独自的一行。* 更“真实”，差异更可靠，因为一行只有一个变化。

这一规则的特殊情况应该很明显，比如类似的rulesets，只带一个声明：

 .icon { display: inline-block; width: 16px; height: 16px; background-image: url(/img/sprite.svg); }

 .icon--home { background-position: 0 0 ; } .icon--person { background-position: -16px 0 ; } .icon--files { background-position: 0 -16px; } .icon--settings { background-position: -16px -16px; } 这些类型的规则受益于单行是因为：

* 他们仍然符合one-reason-to-change-per-line规则;* 它们分享了足够多的相似之处，而这些在其他rulesets下不需要被彻底解读，这样书写使得我们浏览选择器更加直观方便。

### 缩进

除了缩进单独声明外，整个rulesets中的缩进都和它们相互之间的关系相关联，例如：

 .foo { }

 .foo__bar { }

 .foo__baz { }

通过这样做，开发者可以一眼就看到它们的结构关系是`.foo__baz {}`在`.foo__bar {}`内部，且它们都在`.foo {}`内部。

这样对DOM节点的准复制能让开发人员不用查看HTML片段就知道这些类是在怎样的结构中被使用的。

#### 缩进SASS

Sass提供嵌套功能。也就是说,通过编写下面这样的代码:

 .foo { color: red;

 .bar { color: blue; }

 } 编译成CSS就是这样：

 .foo { color: red; } .foo .bar { color: blue; } 在缩进sass的时候，我们坚持同样的两个空格，在嵌套规则的前后我们还留下一个空行。

注意：在sass缩进的时候尽量避免嵌套，更多细节请看**特异性**那一章。

#### 对齐

尝试对齐相关声明中相同的字符串，例如：

 .foo { -webkit-border-radius: 3px; -moz-border-radius: 3px; border-radius: 3px; }

 .bar { position: absolute; top: 0; right: 0; bottom: 0; left: 0; margin-right: -10px; margin-left: -10px; padding-right: 10px; padding-left: 10px; } 这使生活变得更容易一些，对开发人员来说，如果他们的代码编辑器支持多列编辑，这样就可以一次性编辑多列对齐的相同内容。

### 有意义的空白

除了缩进，我们可以通过自由和明智地使用rulesets之间的空白提供大量的信息。我们使用：

* 密切相关的rulesets之间留一个空行。* 关联性不大的rulesets之间使用两个空行。* 全新的部分板块之间留5个空行。

例如：

 /*------------------------------------*\ #FOO \*------------------------------------*/

 .foo { }

 .foo__bar { }

 .foo--baz { }

 /*------------------------------------*\ #BAR \*------------------------------------*/

 .bar { }

 .bar__baz { }

 .bar__foo { }

不应该出现两个rulesets之间没有空行的情况，比如下面这样就是错误的：

 .foo { } .foo__bar { } .foo--baz { } ### HTML

由于HTML和CSS本质上的相互关联性，这里我将疏忽一些我不介绍的语法和格式标记指南。

永远记着给属性打上引号，尽管没有引号也能正常工作。这将减少发生意外的可能性，而且这是大部分开发者更熟悉的格式。下面这行代码是有效的：

 <div class=box> 但更受欢迎的格式应该是这样的：

 <div class="box"> 这里的引号不是必须的，但从安全的角度考虑，我们应该将类名“box”用引号包起来。

当同时有多个类的值时，用两个空格将它们分隔开，像这样：

 <div class="foo bar"> 当有多个类的值是相关联的时候，用中括号把它们分别括起来，像这样：

 <div class="[ box box--highlight ] [ bio bio--long ]"> 这不是一个坚定的推荐，我自己现在还在试验这样的写法，但它确实给我带来了许多好处，更多细节请看**分组相关类的标记**。

正如我们的rulesets一样，您可以在HTML中使用有意义的空白。您可以用5个空行来隔断主题和内容部分，例如：

 <header class="page-head"> ... </header>

 <main class="page-content"> ... </main>

 <footer class="page-foot"> ... </footer>

用一个空行分隔标记相互独立且关联度不高的相关片段，例如：

 <ul class="primary-nav">

 <li class="primary-nav__item"> <a href="/" class="primary-nav__link">Home</a> </li>

 <li class="primary-nav__item primary-nav__trigger"> <a href="/about" class="primary-nav__link">About</a>

 <ul class="primary-nav__sub-nav"> <li><a href="/about/products">Products</a></li> <li><a href="/about/company">Company</a></li> </ul>

 </li>

 <li class="primary-nav__item"> <a href="/contact" class="primary-nav__link">Contact</a> </li>

 </ul> 这使得开发人员能够对DOM的不同部分一目了然，也让像Vim这样的文本编辑器使用起来更加方便，例如，操纵用空行分隔标记的代码块。

### 更多阅读

* *<a href="http://csswizardry.com/2014/05/grouping-related-classes-in-your-markup/">分组相关类的标记</a>*







当然，在大多数项目中这部分将变的大得多，但我希望我们可以看到这一节在主样式表中，为开发人员提供一个项目范围视图。我们可以清晰的看到被渲染的样式代码目的是什么，在什么位置等等。

### 宽度为80个字符

在可能的情况下，将CSS文件的宽度限制到80个字符，原因包括：

* 能够使得打开多个文件并排放置，方便浏览；
* 像GitHub网站或者终端一样查看CSS；
* 为注释提供一个舒适的长度；

 /** * I am a long-form comment. I describe, in detail, the CSS that follows. I am * such a long comment that I easily break the 80 character limit, so I am * broken across several lines. */

这里将会有不可避免的例外规则，比如URL或者梯度语法，这些都不用担心。

### 标题

CSS中每一个主要的部分都开始于一个标题

 /*------------------------------------*\ #SECTION-TITLE \*------------------------------------*/

 .selector { } 每一部分都标题都是以“`＃`”为前缀，以使我们能够进行更有针对性的搜索（如`grep`等等），而不是只搜索标题名(`SECTION-TITLE`)，那样可能会产生许多搜索结果。在大范围中搜索带“＃”号的标题(`#SECTION-TITLE`)，应该只返回一个所需标题的结果。

在标题和下一行代码之间敲一个回车（中间可以写一写注释或者SASS或者CSS）。

如果你正在的项目里,每一个部分都有自己的文件,那么标题就应该出现在每一个部分的顶部。如果你正在做的项目每个文件包含多个部分,那么每个标题后面最好敲5个回车，这样标题再加上后面多出来的空白区域将会使新的部分在一个大的文件中滚动的时候更容易被发现。

 /*------------------------------------*\ #A-SECTION \*------------------------------------*/

 .selector { }

 /*------------------------------------*\ #ANOTHER-SECTION \*------------------------------------*/

 /** * Comment */

 .another-selector { } ### rulesets的剖析

在我们讨论我们如何书写我们的rulesets之前，让我们先熟悉一下相关术语：

 [selector] { [property]: [value]; [<--declaration--->] }

比如：

 .foo, .foo--bar, .baz { display: block; background-color: green; color: red; }

在这里，你可以看到：

* 相关的选择器写在同一行，不相关的选择器另起一行书写；* 在起始大括号（`{`）之前有一个空格；* 属性名和属性值放在同一行；* 在属性名的冒号（`:`）后，留有一个空格，再接着写属性值；* 每一个声明都开始于新的一行；* 和起始大括号（`{`）同一行的是最后一个选择器；* 第一个声明在起始大括号（`{`）后新的一行；* 结束大括号（`}`）独占新的一行；* 每个声明都缩进两个空格；* 每个声明都以一个分号（`;`）结束；

这种格式似乎是目前通用的标准（除了在空格数量上的变化，许多开发者还是喜欢两个空格）。

像下面代码这样的书写就是不正确的：

 .foo, .foo--bar, .baz { display:block; background-color:green; color:red } 问题点包括：

* 用制表符代替空格；* 不相关的选择器写在了同一行；* 起始大括号（`{`）独占一行；* 结束大括号（`}`）没有独占一行；* 最后的结束的（`;`）丢失（当然，分号是可选的，为了保持一个好习惯，最好还是写上）；* 在冒号（`:`）后面没有空格；

### 多行CSS

CSS应该多行书写，除了在某些非常特殊的情况下，这样写有许多好处：

* 降低代码合并引发冲突的几率，因为每一条样式声明都存在于它独自的一行。* 更“真实”，差异更可靠，因为一行只有一个变化。

这一规则的特殊情况应该很明显，比如类似的rulesets，只带一个声明：

 .icon { display: inline-block; width: 16px; height: 16px; background-image: url(/img/sprite.svg); }

 .icon--home { background-position: 0 0 ; } .icon--person { background-position: -16px 0 ; } .icon--files { background-position: 0 -16px; } .icon--settings { background-position: -16px -16px; } 这些类型的规则受益于单行是因为：

* 他们仍然符合one-reason-to-change-per-line规则;* 它们分享了足够多的相似之处，而这些在其他rulesets下不需要被彻底解读，这样书写使得我们浏览选择器更加直观方便。

### 缩进

除了缩进单独声明外，整个rulesets中的缩进都和它们相互之间的关系相关联，例如：

 .foo { }

 .foo__bar { }

 .foo__baz { }

通过这样做，开发者可以一眼就看到它们的结构关系是`.foo__baz {}`在`.foo__bar {}`内部，且它们都在`.foo {}`内部。

这样对DOM节点的准复制能让开发人员不用查看HTML片段就知道这些类是在怎样的结构中被使用的。

#### 缩进SASS

Sass提供嵌套功能。也就是说,通过编写下面这样的代码:

 .foo { color: red;

 .bar { color: blue; }

 } 编译成CSS就是这样：

 .foo { color: red; } .foo .bar { color: blue; } 在缩进sass的时候，我们坚持同样的两个空格，在嵌套规则的前后我们还留下一个空行。

注意：在sass缩进的时候尽量避免嵌套，更多细节请看**特异性**那一章。

#### 对齐

尝试对齐相关声明中相同的字符串，例如：

 .foo { -webkit-border-radius: 3px; -moz-border-radius: 3px; border-radius: 3px; }

 .bar { position: absolute; top: 0; right: 0; bottom: 0; left: 0; margin-right: -10px; margin-left: -10px; padding-right: 10px; padding-left: 10px; } 这使生活变得更容易一些，对开发人员来说，如果他们的代码编辑器支持多列编辑，这样就可以一次性编辑多列对齐的相同内容。

### 有意义的空白

除了缩进，我们可以通过自由和明智地使用rulesets之间的空白提供大量的信息。我们使用：

* 密切相关的rulesets之间留一个空行。* 关联性不大的rulesets之间使用两个空行。* 全新的部分板块之间留5个空行。

例如：

 /*------------------------------------*\ #FOO \*------------------------------------*/

 .foo { }

 .foo__bar { }

 .foo--baz { }

 /*------------------------------------*\ #BAR \*------------------------------------*/

 .bar { }

 .bar__baz { }

 .bar__foo { }

不应该出现两个rulesets之间没有空行的情况，比如下面这样就是错误的：

 .foo { } .foo__bar { } .foo--baz { } ### HTML

由于HTML和CSS本质上的相互关联性，这里我将疏忽一些我不介绍的语法和格式标记指南。

永远记着给属性打上引号，尽管没有引号也能正常工作。这将减少发生意外的可能性，而且这是大部分开发者更熟悉的格式。下面这行代码是有效的：

 <div class=box> 但更受欢迎的格式应该是这样的：

 <div class="box"> 这里的引号不是必须的，但从安全的角度考虑，我们应该将类名“box”用引号包起来。

当同时有多个类的值时，用两个空格将它们分隔开，像这样：

 <div class="foo bar"> 当有多个类的值是相关联的时候，用中括号把它们分别括起来，像这样：

 <div class="[ box box--highlight ] [ bio bio--long ]"> 这不是一个坚定的推荐，我自己现在还在试验这样的写法，但它确实给我带来了许多好处，更多细节请看**分组相关类的标记**。

正如我们的rulesets一样，您可以在HTML中使用有意义的空白。您可以用5个空行来隔断主题和内容部分，例如：

 <header class="page-head"> ... </header>

 <main class="page-content"> ... </main>

 <footer class="page-foot"> ... </footer>

用一个空行分隔标记相互独立且关联度不高的相关片段，例如：

 <ul class="primary-nav">

 <li class="primary-nav__item"> <a href="/" class="primary-nav__link">Home</a> </li>

 <li class="primary-nav__item primary-nav__trigger"> <a href="/about" class="primary-nav__link">About</a>

 <ul class="primary-nav__sub-nav"> <li><a href="/about/products">Products</a></li> <li><a href="/about/company">Company</a></li> </ul>

 </li>

 <li class="primary-nav__item"> <a href="/contact" class="primary-nav__link">Contact</a> </li>

 </ul> 这使得开发人员能够对DOM的不同部分一目了然，也让像Vim这样的文本编辑器使用起来更加方便，例如，操纵用空行分隔标记的代码块。

### 更多阅读

* *<a href="http://csswizardry.com/2014/05/grouping-related-classes-in-your-markup/">分组相关类的标记</a>*
