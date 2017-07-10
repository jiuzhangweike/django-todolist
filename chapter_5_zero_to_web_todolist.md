# 来做我们的 Todo-List

太好了，我们终于走到了这一步，不知道我们有多少同学成功的坚持下来了。前面我们分别的学习了 **Django入门开发** 的相关的知识，和 **Web前端开发** 相关的 HTML、CSS以及一些 JavaScript 相关的知识，这些知识虽然看起来较为繁杂，但是在我们一步步的不断地学习之后，大家都对这些部分的知识和内容有了一定的了解，接下来我们终于要开始设计和实现我们所想要制作的 `Todo-List` 程序了。



## 了解数据库

在具体的设计开发之前，我们还应该了解一些与数据库相关的知识，并且这里我们也会把这部分的知识侧重在 Django 中的数据库的使用。在进入我们的介绍之前，我们先提出这样的一个问题，那就是我们常说的数据库到底是什么东西？我们在 [Wikipedia](https://zh.wikipedia.org/wiki/%E6%95%B0%E6%8D%AE%E5%BA%93) 能看到这样的解释：

> [数据库管理系统](https://zh.wikipedia.org/wiki/%E6%95%B0%E6%8D%AE%E5%BA%93%E7%AE%A1%E7%90%86%E7%B3%BB%E7%BB%9F)（英语：Database Management System，简称DBMS）是为管理[数据库](https://zh.wikipedia.org/wiki/%E8%B3%87%E6%96%99%E5%BA%AB)而设计的电脑[软件](https://zh.wikipedia.org/wiki/%E8%BB%9F%E9%AB%94)系统，一般具有存储、截取、安全保障、备份等基础功能。数据库管理系统可以依据它所支持的[数据库模型](https://zh.wikipedia.org/w/index.php?title=%E8%B3%87%E6%96%99%E5%BA%AB%E6%A8%A1%E5%9E%8B&action=edit&redlink=1)来作分类，例如[关系式](https://zh.wikipedia.org/wiki/%E9%97%9C%E8%81%AF%E6%A8%A1%E5%9E%8B)、[XML](https://zh.wikipedia.org/w/index.php?title=XML%E8%B3%87%E6%96%99%E5%BA%AB&action=edit&redlink=1)；或依据所支持的电脑类型来作分类，例如服务器群集、移动电话；或依据所用查询语言来作分类，例如[SQL](https://zh.wikipedia.org/wiki/SQL)、[XQuery](https://zh.wikipedia.org/w/index.php?title=XQuery&action=edit&redlink=1)；或依据性能冲量重点来作分类，例如最大规模、最高运行速度；亦或其他的分类方式。不论使用哪种分类方式，一些DBMS能够跨类别，例如，同时支持多种查询语言。

无论我们作为什么方向的软件开发者，我们都或多或少的会用到各种形式上的数据库，但是这种细分领域的东西是很容易让人困惑和畏惧的东西，比如数据库、编译器和操作系统等等的大型系统，都会让人有望而生畏的情绪，但是我们这里应该暂时放下这种情绪，让我们简单的来考虑我们的数据库的本质到底是什么。

我们这里可以给出一种简单的结论——**数据库本质上是一系列文件的集合** 。如果我们从这个角度来考虑，数据库就不是什么复杂的东西了，我们可以简单地使用这样的一副图片来表示我们的理解：

![database](chapter_5_zero_to_web_todolist/database.png)

这里我们看到我把数据库分成了两堆，一部分是 `FileSet` 用于数据库实际内容的存储，另一部分是



## 数据库设计

我们在开发实际的程序之前我们应该简单的设计一下我们的程序，首先是数据设计，我们只是为了实现一个简单的能够存储 每个 Todo-Item 数据而已，因而我们所需要的数据也不过是几种数据：

* 我们需要每个 Item 的 Title 作为每个 Todo-Item 的标题，我们还应该需要一个 description 值来对我们的每个 Item 进行更为详细的描述。
* 另外我们的每一个 Item 还需要用一个 Flag 来记录我们当前条目的状态，就是说我们的这条 todo 是不是已经完成了，通过区分这个我们可以提供一些视觉上的区分方法，来区分我们的 todo 是否完成（比如说给已经完成的条目添加删除线）。
* 紧接着我们应该提供一个 createAt 时间戳来记录我们的本条 todo 的创建时间，还有我们还需要一个 updateAt 的时间戳来记录我们