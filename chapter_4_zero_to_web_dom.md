## DOM 相关

经过前面几节中的内容的学习，我们现在已经对 JavaScript 这门语言有了一定程度的了解了，我们学到了一些基础的文法，还对 JavaScript 中比较令人纠结的动态语言特性，另外我们还在最后提供的拓展阅读之中，为大家提供了更为有深度的关于 JavaScript 中 `原型链` 相关的知识。在这节里我们主要介绍一些基础的 DOM 操作，这就是我们之前介绍了 JavaScript 的一个主要的用处，就是操作 **HTML** 中的元素，通过添加、修改、删除等一系列操作，对我们的网页进行修改，产生一定的动态的效果。

### 浏览器对象

JavaScript 作为一门语言我们有了了解，但是 JavaScript 目前主要的作用还是作为一门浏览器语言被使用，那么浏览器作为语言的外围环境，将我们能从浏览器中获取一些浏览器对象，然后我们就可以借助访问这些浏览器对象，获取当前浏览器很多的信息，这里我们可以简单的介绍一下：

* `window` 对象：window 表示了浏览器的外围窗口，我们能从 window 对象中，获得 `innerWidth` 和 `innerHeight` 获取浏览器的宽高。
* `screen` 对象：screen 对象表示了屏幕的大小，我们能拿到 `width` 和 `height` 来拿到屏幕的大小。
* `location` 对象：location 对象经常用在获取和处理当前 url 的场景中，我们能从 location 中获取很多和 url 的具体信息，例如 `host` 、`port` 等很多的信息。
* `navigator` 对象：navigator 对象中能拿到很多浏览器的详细信息，比如经常用的  **navigator.userAgent** 获取浏览器设置的 UA 信息。
* `document` 对象：document 是代表了当前网页的文档模型，比如 `document.title` 就表示了我们当前的网页的 title 文本，这就是我们要操纵的 DOM 对象。

### 操纵 DOM 树

在我们之前的文章中提到过 DOM 对象是一个树形的数据结构（联想我们讲解过的 HTML 的结构），那我们操纵 DOM 树的时候我们的操作也会紧密围绕这个树形结构去展开，比如最简单的我们可以通过一些 document 提供的 API 去从文本模型中获取出对应的节点，比如我们可以使用 `getElementById()` 和 `getElementsByTagName()` 这两个 API，第一个 API 可以获取对应的 ID 的元素，而第二个 API 可以获取到所有 Tag 为对应项目的元素集合。

``` html

```

