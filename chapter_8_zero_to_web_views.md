# 其余的一些实现

我们在前面的几个小节中介绍中，我们已经介绍完了至少了大半的程序的内容了，包含了 Url 的捕获、简单的模板引擎的使用、简单的表单提交的知识，并且在这些知识点中我们穿插的介绍了我们的 todo-list 的 Demo 中是如何使用这些知识点进行了相关的实现，其中我们在 `template` 的模板和 `views.py` 的部分的还有一些实现和细节我们还没有完全的介绍清楚，我们在这节里面做一些简要的介绍。

## 使用模态框添加 todo-item

我们在 **todo-list** 的主界面使用弹出模态框的方式添加了 **todo-item**：

![model](chapter_8_zero_to_web_views/model.png)

如上图所示，我们通过点击弹出一个模态框，我们在模态框里面添写信息，再点击确认上传我们的 **todo-item** ：

``` django
    <div>
      <button class="btn btn-primary" data-toggle="modal" data-target="#modal-add">添加</button>
    </div>
```

我们在界面中放着这样的一个弹出模态框的按钮，能打开一个这样的模态框：

``` django
<div class="modal fade" id="modal-add">
     <form method="post">
        {% csrf_token %}
        <div class="modal-dialog">
          <div class="modal-content">
            <div class="modal-header">
              <h4>ADD TODO</h4>
            </div>
            <div class="modal-body">
              <div class="input-group">
                <span class="input-group-addon">title</span>
                <input type="text" class="form-control" name="title" />
              </div>
            </div>
            <input type="hidden" name="action" value="add" />
            <div class="modal-footer">
              <button class="btn btn-primary" type="submit">确定</button>
            </div>
          </div>
        </div>
     </form>
</div>
```

我们在模态框中包含了一个表单，我们把确定的按钮设置为了 `submit` 我们又通过了设置了一个隐藏的 `<input>` 设置 `action` 为 `add` ，来区分我们的 action，我们点击确定，就能向本页面发送一个表单。

``` python

def todolist(request):
    if request.method == 'POST':
        action = request.POST.get('action')
        if action == 'add':
            title = request.POST.get('title')
            Todo.objects.create(title=title)

    todolist = Todo.objects.all()
    return render(request, 'index.html', locals())

```

我们在本页面的 `Views.py` 界面中检测向本界面提交的表单，并且检测到我们的 `action == 'add'` 然后我们以获取到的数据，向数据库创建新的对象。

然后我们再获取全部的数据库的对象，渲染到我们的页面上面，这就是我们不依赖其他手段，仅通过重新刷新界面的方式进行我们的更新。

## 其余的 Views 中的简单实现 

![views](chapter_8_zero_to_web_views/usage.png)

我们通过对点击完成或是删除都会调用 Views.py 中对应的程序：

``` python
def delete(request, pk):
    todo = get_object_or_404(Todo, id=pk)
    todo.delete()
    return HttpResponseRedirect('/')


def complete(request, pk):
    todo = get_object_or_404(Todo, id=pk)
    todo.completed = True
    todo.save()
    return HttpResponseRedirect('/')
```

这部分的实现也都很是简单，删除或是完成，我们不过是修改状态，或是找到对应的 item 直接删除掉。

## 总结

到这部分位置我们终于几乎仅依赖于 Django 的相关的知识构建了我们自己的 Todo-List 程序，麻雀虽小五脏俱全。但是我们在开发方面的追求是永无止步的，这门微课只是提供一个指南式的入门课程，希望能够成为一个对初学者入门起到一个指引的作用的课程。在这门课程中我们窥见了 Django 开发的一角，在接下来的学习中我们会为大家推荐一些书籍：

* 《Python编程：从入门到实践》：不要被这个 “接地气” 的中文译名骗了，其实这是一本特别适合 Python 入门的教材，这本书和其余 Python 的入门教程有些区别，你可以根据这本书的讲解一步步的学习 Python 的各个细节，讲解顺序和那种像是字典一样的书籍不一样，而是从注重和读者的交互的角度进行一步步的讲解，而且其中包含了很多的实例还有和 Django 相关的部分。
* 《流畅的 Python》：对 Python 已经有一些熟悉的同学可以来阅读这本书，涉及到了很多的有趣而有深度的 Python 知识点，但是读起来并不枯燥和繁杂，反而像是书名里的一样，读起来非常的流畅，很多同学表示一次性读下来让人受益匪浅。
* 《九章微课：Python 入门》：除了这个 Django 的微课之外，九章算法还为同学们提供了一个 Python 入门的微课，这个微课内容比较翔实并且带有对一些特性的启发和思考，还包含了很多的 best practice 的部分，其中的 CookBook 时间也可以为初学者的在入门的同时打下更好的基础和产生深远的影响。
* Django 官方文档：谈到对 Django 这种具体到某个框架的学习和实现，书籍的作用就不会那么显著了，和之前推荐的一样，即查即用的 Django 官方文档是最好的选择里面不但有对各个 API 的详细解读还有很多 best practice 的参考范例可以参考。
* 《CSS 设计指南》：CSS 可能是三件套中写起来比较困扰的一个了，因为不同的设计元素之间会互相产生影响，不过 《CSS 设计指南》在相关的教学书籍之中做出了一个好的典范，仔细阅读之后会有一种拔冗见日的感觉，除此以外 MDN 的 CSS tutorial 也是一个不错的在线教程。
* 《Head First JavaScript》：挑选 JavaScript 的入门书，Head-First 系列总是一个不能跳过的、不会有错的选项，作为一本针对初学者的书，Head-First 用这个系列一贯的灵活、轻松地讲课方式为我们讲解了 JavaScript 很多的特性和使用。
* 《JavaScript 高级编程》：在对 JavaScript 有了一定的了解时候，如果想对这门有趣的语言有更多的了解之外，《JavaScript 高级编程》是我们无法错过的一本经典教材，其中的内容虽然仍以 ES5 为蓝本但是涵盖范围的广度和深度都不仅是在使用一门语言的层次上面，读了这本书甚至对程序理论、语言设计都会有一定的益处，是一本不可多得进阶书籍。

上面推荐的这些书籍、微课、文档都考虑到了不同的层次、水平的开发者阅读，仔细的学习一些好书能让我们在对很多程序、理论的认知上达到一个新的层次上去。

这个微课中简单的 TodoList 虽然完成了，但是这个东西本身的可拓展的空间还有很多：

* 请求：这里我们的请求都是通过提交表单刷新页面的方式进行的，虽然简单但是效果并不好，在这方面我们可以尝试通过发送请求动态的刷新某些部分的显示。
* 模板：这个 todolist 我们使用了 Django 自带的模板和相应的模板语法进行开发，但是使用模板语法毕竟有些繁杂并且表达能力并不强，这里我们也可以使用一些流行的前端的渲染框架来完成这个部分的工作如 Vue.js、React.js。
* 界面：我们这里仅仅展示了样式最为简单的一个 todolist ，但是一个好的应用程序还是要拥有美观的界面才能吸引到用户的，大家可以通过学习更多编写界面的知识对我们的界面进行修改。
* 功能：功能现在只有增删改查的功能，但是本身 todolist 可能还需要有一些分组啊、设定完成时间之类的功能，大家也可以思考一下有哪些功能可以加在自己的 todolist 上面。

说了这么多可拓展的内容，大家是不是觉得有点头大？没关系的就像我们完成的这个 TodoList 一样，千里之行始于足下，从现在的一点一滴开始慢慢的我们就会成为一个出色的软件工程师了！

这个结束，只是一个开始，加油！





















