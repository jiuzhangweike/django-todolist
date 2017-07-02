### CSS 样式 Demo

我们在上一节中已经简单的了解了一些和 CSS Selector 相关的部分知识，接着在这一节中我们会见到一些简单的例子，通过一些简单的例子，去实践更多的 CSS 属性，我们可以学到一些和 CSS 样式设计有关系的知识。

#### 部分文字设置颜色：

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

#### 背景垂直重复：

我们经常有需要为某种背景设置背景，因为本身是使用小图进行设置，那我们就需要一种重复机制进行设置，比如让图片纵向重复平铺，或者让背景纵向平铺。我们可以通过 `background-repeat` 这个属性对它进行设置：

``` html
<html>
<head>

<style type="text/css">
body
{ 
background-image: 
url(http://img5.imgtn.bdimg.com/it/u=3894097359,3266263308&fm=26&gp=0.jpg);
background-repeat: repeat-y
}
</style>
</head>
<body>
</body>
</html>

```

我们设置为整个 body 都被一张图片在 y 轴上重复填充。

保存运行之后的效果是：

![back](chapter_3_zero_to_web_css_style/just-horizontal.png)



#### 使用滚动条来显示溢出的内容：

当我们开发带有列表的程序时，我们不希望内容的逐渐填充把页面撑得很大，而是希望我们的界面能提供一个滚动条，能让我们的内容能够滚动的浏览，就如同我们接下来要开发的这个 Todo-List 界面，我们就需要为我们的 todo 项目提供一个列表。这时候我们就为我们所想要设置滚动条的元素为固定大小，然后我们的