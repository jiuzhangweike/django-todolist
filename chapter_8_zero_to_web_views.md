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
* Django 官方文档：谈到对 Django 这种具体到某个框架的学习和实现，书籍的作用就不会那么显著了，和之前推荐的一样，即查即用的 Django 官方文档是最好的选择里面不但有对各个 API 的详细解读还有很多 best practice 的参考范例可以参考。
* ​





















