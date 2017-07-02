### CSS 样式 Demo

我们在上一节中已经简单的了解了一些和 CSS Selector 相关的部分知识，接着在这一节中我们会见到一些简单的例子，通过一些简单的例子，去实践更多的 CSS 属性，我们可以学到一些和 CSS 样式设计有关系的知识。

* 部分文字设置颜色：

在一群文字同时排列的时候，我们可能只需要其中的一部分文字拥有高亮的效果，就像我们经常在代码段中见到的那样部分的关键字和符号有高亮而其余的文字高亮。

``` html
<p><span class="highlight"> lfkdsk </span> jiuzhang </p>
```

我们通过 span 作为行内元素，再为这个行内元素设置自己的 class ，然后设置 CSS 样式就能实现行内的颜色高亮。

``` css
span.highlight {
  color:rgb(0,0,255) 
}
```

最后显示的样式是这样子：

![highlight](chapter_3_zero_to_web_css_style/highlight.png)

我们全部的代码是这个样子的：

``` html
<html>
<head>
<style type="text/css">
span.highlight {color:rgb(0,0,255)}
</style>
</head>

<body>
<p><span class="highlight"> lfkdsk </span> jiuzhang </p>
</body>
</html>
```

* 背景垂直重复：

