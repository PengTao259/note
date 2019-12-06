## Ajax的补充

### 是什么

- 字面意思
    - Ajax 即“Asynchronous  Javascript  And  XML”（异步的 JavaScript 和 XML）
- 深层意思
    - 是一种通过JS代码完成客户端和服务器端交互的技术

### 典型应用场景

在`不更新页面`的情况下（页面有没有更新就检查后退按钮），浏览器要从web服务器获取数据，此时就可以使用ajax技术。

先来对比更新和不更新页面，以分页为例

- 大学的公告页，没有使用AJAX：http://www.whut.edu.cn/tzgg/
- 博客园的主页,   使用了AJAX：<https://www.cnblogs.com/>

经典应用

- 博客页的注册页：<https://account.cnblogs.com/signup>
- 购物网站：http://www.smzdm.com

### AJAX技术的好处

总结如下两点好处：

1. 局部更新，提升用户体验，提升性能。
2. 分离开发，提高开发效率。
    1. 前端 调用接口
    2. 后端 开发接口

## jQuery中的ajax补充

- $.ajax();

    ```js
    $.ajax({
        type: '请求方式',
        url: '接口地址',
        data: '请求参数',
        dataType: '响应数据格式',
        success: function (res) {
            // res就是服务器返回的结果
        },
        beforeSend: function () {},
        complete: function () {},
        contentType: '设置请求头中的content-type的值',
        processData: '是否处理请求参数'
    });
    ```

    

- $.get()

    ```js
    $.get('url', [请求参数], [请求成功后的回调函数], [服务器返回数据的类型]);
    ```

    

- $.post()

    ```js
    $.post('url', [请求参数], [请求成功后的回调函数], [服务器返回数据的类型]);
    ```

    

## 其他封装库 axios （了解）

### axios库

jquery中封装了ajax功能，但是它的体积比较大。如果我们只希望使用ajax功能，而不需要dom操作的话，我们可以选择使用axios库。(fetch)

应用：

```
- 它只专注于处理http请求，比jquery的体积小的多，适用于只需要ajax请求的业务场景；
- 后期学习三大前端框架时也会用到；
```

#### 使用示例

通过官网查看其使用方法。

与jquery一样，要使用它，必须先引入这个文件。然后就可以按如下的格式去使用了。

中文网站：<http://www.axios-js.com/zh-cn/docs/

```javascript
// 获取服务器的返回值
axios.get('/common/get?id=123').then(function(res) {
    // res 就是本次请求的信息
    console.info(res);
    // 获取 从服务器返回的数据
    console.info(res.data);
});

axios.get('/common/get', { params: { id: 123, name: 'jake' } }).then(function(res) {
    // res 就是本次请求的信息
    console.info(res);
    // 获取 从服务器返回的数据
    console.info(res.data);
});

// post请求，不带参数
axios.post('/common/post').then(function(res) {
    console.info(res.data);
});
// post请求，带参数
axios.post('/common/post', { id: 123, name: 'jake' }).then(function(res) {
    console.info(res.data);
});
```



## 模板引擎

### 模板引擎介绍

客户端中拿到请求的数据过后最常见的就是把这些数据呈现到界面上。

如果数据结构简单，可以直接通过字符串操作（拼接）的方式处理，但是如果数据过于复杂，字符串拼接维护成本太大，就不推荐了。

> 模板引擎：
>
> - artTemplate：https://aui.github.io/art-template/

模板引擎实际上就是一个 API，模板引擎有很多种，使用方式大同小异，目的为了可以更容易更高效的将数据渲染到HTML字符串中。==通俗的说，模板引擎的目的就是将服务器返回的数据显示到HTML页面中==。

### 使用模板引擎步骤

1. 准备一个存放数据的盒子（不是必须的，使用body也可以）

2. 引入template-web.js文件

3. 定义模板（具体语法可以去官网查看），一定要指定script的id和type属性

4. 调用template函数，为模板分配数据，template函数有两个参数一个返回值

    1. 参数1：模板的id
    2. 参数2：分配的数据，必须是一个JS对象的形式
    3. 一个返回值：是数据和模板标签组合好的结果

5. 将 “拼接” 好的结果放到准备好的盒子中（不是必须的，console出来也可以看结果）

    ![1566443384929](Ajax补充.assets/1566443384929.png)

```html
<script src="./assets/template-web.js"></script>

<script type="text/html" id="test">
        <h2>{{title}}</h2>
        <p>{{age}}</p>
        <ul>
            <li>{{heroes[0]}}</li>
            <li>{{heroes[1]}}</li>
            <li>{{heroes[2]}}</li>
    </ul>
</script>

<script>
    // 下面的数据是模拟的，相当于ajax请求之后，服务器返回的数据
    var data = {
        title: '模板引擎练习',
        age: 20,
        heroes: ['曹操', '刘备', '李逵', '张飞']
    };
    // 调用template函数
    /*
        var str = template(模板的id, 数据); // 数据必须是JS对象格式
        */
    var str = template('test', data);
    console.log(str);
</script>
```

> 定义模板时的script标签一定好指定id和type
>
> tempalte函数语法：var html = template(模板id,  Object);

### 模板语法

- 输出普通数据（字符串、数值等）

    ```
    // 模板写法
    {{var}}
    
    // template函数写法
    var html = template('id', {
        var: 'hello world'
    });
    ```

- 条件

    ```
    // 模板写法
    {{if age > 18}}
    	大于18
    {{else}}
    	小于18
    {{/if}}
    
    // template函数写法
    var html = template('id', {
        age: 20
    });
    ```

- 循环

    ```
    // 模板写法
    {{each arr}}
    	{{$index}} -- 数组的下标
    	{{$value}} -- 数组的值
    {{/each}}
    
    // template函数写法
    var html = template('id', {
        arr: ['apple', 'banana', 'orange']
    });
    ```

完整的代码：

```html
<script src="./assets/template-web.js"></script>

    <!-- 1. 定义模板 -->
    <script id="abc" type="text/html">
        <h1>{{name}}</h1>
        <p>我是{{nickname}}，我有一辆{{car}}，我今年{{age}}岁了</p>
        {{if age >= 18}}
            <p>欢迎来玩~</p>
        {{else}}
            <p>未成年人禁止进入</p>
        {{/if}}
        <p>我有好几个女朋友，分别是：</p>
        <ul>
            {{each girls}}
            <li>{{$index}} -- {{$value}}</li>
            {{/each}}
        </ul>
    </script>


    <script>
        // 2. 调用template函数
        var str = template('abc', {
            name: '狗哥',
            nickname: '北狗最光阴',
            car: '宝马',
            age: 31,
            girls: ['王婆', '金莲', '西门大官人', '李师师', '赛金花']
        });

        console.log(str);
        document.body.innerHTML = str;
    </script>
```



### 案例中使用模板引擎处理响应数据

下面以留言板案例为例。

```html
<!-- 引入template-web.js -->
<script src="./assets/template-web.js"></script>

<!-- 定义模板 -->
<script id="moban" type="text/html">
    {{each girls}}
    <li class="media">
      <img class="mr-3" src="avatar.png" alt="">
      <div class="media-body">
        <h4>{{$value.name}}</h4>
        <p>{{$value.content}}</p>
    </div>
    </li>
    {{/each}}
</script>
```

```js
xhr.onload = function () {
    // console.log(this.response);
    var data = JSON.parse(this.response);
    console.log(data);
    // 拼接字符串
    var str = template('moban', {
        girls: data
    });
    // 把变量后，拼接好的str放到 id为 messages 的ul中
    document.getElementById('messages').innerHTML = str;
}
```

