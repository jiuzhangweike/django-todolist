# 表单提交

我们制作一个能够和后端进行交互的网页，那我们肯定要通过一种方式能够和后端交流数据，我们不但要能接受到 Web Server 的数据，还要能把我们的数据能够提交给我们的 Web Server，因而我们需要能够理解和使用表单这种功能。

Django 中提供了一系列的 API 和工具类，帮助我们构建表单接受我们的网站的使用者输入的数据，处理后再反馈给我们的用户。

## HTML 表单

我们在 HTML 中使用的表单是形如 `<form>...</form>` 的一对的 form 标签中间包含我们想要放入表单的元素，允许我们的使用者输入文本、选择选项、操纵对象，之后我们再把这些数据返回给 Web Server。

我们举一个使用 `<input>` 标签的例子，一个表单至少要包含两个基础的元素：

* 提交到哪：我们提交数据的 url。
* 如何提交：我们使用哪种 HTTP 的方法去传送我们的数据。

举一个例子，如果我们需要在 Django 中写一个 Login 界面界面，登录界面中我们需要提供标签，这里我们包含登录名字的 `<input>` 标签里面需要设置 **type=text**，包含登录密码的 `<input>` 标签里面我们需要设置 **type=password** ，我们还可以给我们提交按钮 `<button>` 标签设置一个 **type=submit** 属性，设置我们能通过点击这个按钮提交这个表单。

另外我们还能包含一些隐藏的用户不可见的元素放在我们的表单之中。我们同样需要在 `form` 中设置属性去控制我们提交的 url 和提交的方法，比如我们可以在 `<form>` 标签中设置 action 属性为 **/admin/** ，设置我们的提交的 Url 为 **admin** ，我们也可以给它的 method 属性为 **post**，指定我们的提交方式为 POST 方法，当我们的按钮 ：

``` html
<input type="submit" value="Log in"> 
```

被按下后我们的数据会被提交到我们的 admin 的 Url 中去。

## Get 和 Post 方法

我们在处理 HTML Form 的时候只能使用两种 HTML 方法 —— **GET 和 POST** 。

### Post 方法

比如我们刚才举例子在 Django 中实现 Login 界面中，我们提交登陆账户和密码使用的就是 Post 方法。

### Get 方法

我们 Get 方法相反，就是把我们的想要提交的数据打包转成一个字符串，编码在我们的 Url 里面，我们的 Url 里面包含我们所要提交数据的地址，还包含我们提交的数据的 key 和 value：

```
https://docs.djangoproject.com/search/?q=forms&release=1.
```

我们使用 GET 方法的时候类似于这个样子。

## 使用表单提交

``` django
      {% for todo in todolist %}
        <tr>
          <td>{{ todo.title }}</td>
          <td>
            {% if todo.completed %}
              <del>已完成</del>
            {% else %}
              <form action="/complete/{{ todo.id }}/">
                <button class="btn btn-primary" type="submit">标记完成</button>
              </form>
            {% endif %}
          </td>
          <td>
            <form action="/delete/{{ todo.id }}/">
              <button class="btn btn-primary" type="submit">删除</button>
            </form>
          </td>
        </tr>
      {% endfor %}
```

比如说我们使用在我们刚才在模板文件中写的遍历展示我们的 todo-list 的地方，我们还要在每一行提供两个按钮能够将我们的这条 todo-item 标记为完成，或是将我们的 todo-item 标记为删除。这里面我们就是填写了两个 `<form>` 标签：

``` django
<form action="/complete/{{ todo.id }}/">
     <button class="btn btn-primary" type="submit">标记完成</button>
</form>
```

这里面我们就是使用了 GET 方法，将我们的 todo-item 的那条具体的 id 编码在我们的 Url 里面提交给我们的后端，对它进行响应的处理，还记得我们在 [Url 捕获](http://www.jiuzhang.com/tutorial/django-step-0-to-1/120) 的章节中进行的设计么：

``` python
urlpatterns = [
    // ...
    url(r'^delete/(?P<pk>\d+)/', views.delete),
    url(r'^complete/(?P<pk>\d+)/', views.complete),
]
```

