# Node.js - day05

## 反馈

1. 阔以阔以
1. 感觉昨天上午学的内容 都云里雾里的呢.....
1. 谢谢老师的悉心教导,老师实在是太温柔了
1. 男人一定要慢 慢一点才好
1. mysql-ithm模块使用有点模糊，花姐可以再讲讲吗
1. 花姐，来做反馈了哦！做天的跨域JSONP和CORS还是模糊鸭！在自习回顾一下就很好了鸭！ 一到下午感觉状态下滑，学东西记不住怎么破呢？ 嘤嘤嘤，嘤嘤嘤！手动滑稽
1. 数据库很好，老师也很好，代码也很好，大家也很好，好好学习。
1. 我有一只小毛驴我从来也不骑,有一天我开开心心敲着代码骑
1. 上课就困- = ,(告诉自己不能睡). 睛乏的睁不开,(还是闭着眼睛听会儿吧). 眼睛一闭一睁,一节课过去了,与困作斗争的同时一点课都听不进去,只能等晚上1.4倍速刷一遍视频,敲一遍代码,搞到一两点(嗯..大致了解今天讲了些什么了,明天又是元气满满的一天)..............恶性循环,白天睡觉晚上敲代码,我太♂了..你看这小伙,20出头了还是那么精神.jpg,
1. 老师在终端中什么时候使用nodemon 什么时候使用node 分不清楚 越学越懵
1. 棒棒棒 你真棒
1. 花姐，什么情况下是同源
1. 讲得很好，需要自己练习，花姐棒棒哒

## 回顾

1. 运行代码
   1. `node xxx.js`: 代码如果修改了,需要重新运行`ctrl+c`,运行
   2. `nodemon xxx.js`:代码修改了,自动重新运行
   
2. 同源

   1. `http://192.168.156.88:3000`
   2. http:// 协议
   3. (192.168.156.88)(www.jd.com) ip地址,域名
   4. :3000 端口
   5. 对比:
      1. `http://192.168.156.88:3000`
      2. `http://192.168.156.88:5500`

3. 跨域:

   1. 地址1:页面的地址,浏览器地址栏中的地址
      1. `http://192.168.156.88:5500/index.html`
   2. 地址2:Ajax发送请求的`url`地址
      1. $.ajax
         1. url:`http://192.168.156.88:3000/search`

4. 跨域方案 - jsonp

   1. 和Ajax木有关系
   2. 利用的是`script`标签的src属性不受跨域限制
   3. 向不同源的服务器,发送了一个`get`
   4. url中携带了一个`callback`的参数
   5. 服务器接收到之后返回了一个 函数的调用`xxx({name:'jack'})`
   6. 返回浏览器之后解析成js,调用

   

   使用方式:

   1. 前端: $.ajax( dataType:'jsonp' ,type:'get')
   2. 后端:response.jsonp({name:'jack'})
      1. 文档中:
      2. 请求方法:get  (jsonp)
      3. 请求参数:
      4. 请求地址:

   缺点:

   1. 只能发get请求,无法进行大量数据的提交

   优点

   1. 兼容性好

5. 跨域方案 - cors

   1. `html5`中推出的,低版本浏览器不支持
   2. 前端什么都不用干
   3. 后端设置一个允许的`header`
   4. 浏览器看到了这个`header`

   优点:

   1. 支持get和post

   缺点:

   1. 兼容性不太好

6. `mysql-ithm`模块使用

   1. 数据库: 保存数据,保证数据的安全性

   2. 数据库管理员:DBA

   3. SQL语句:

      1. 增:insert
      2. 删:delete
      3. 改:update
      4. 查:select

   4. ``mysql-ithm``

      1. 提供了以一堆的`方法`
      2. 调用方法,用操纵对象的方法,
      3. 内部生成对应的`sql`语句
      4. 间接操纵数据库

      ![1572312665126](assets/1572312665126.png)

## 英雄管理 - 项目说明

1. 开发方式:
   1. 后端:
      1. 照着接口文档
      2. 写接口:接收数据,接收文件,增删改查数据库,返回结果
   2. 前端:
      1. 写静态
      2. 照着接口文档
      3. 调接口

##  英雄管理 - 接口文档

> 自己写接口，自己调用自己写的接口
>
> 素材在其他资料中

1. 文档:
   1. 项目开始之前
   2. 架构根据需求,定需要的接口

| 服务器说明            | 作用描述                     |
| --------------------- | ---------------------------- |
| http://127.0.0.1:3000 | 服务器基地址                 |
| 200                   | 请求成功 状态码              |
| 401                   | 用户名已存在 或者 用户名错误 |
| 402                   | 密码 错误  或者  验证码错误  |
| 500                   | 服务器内部错误               |
| 302                   | 服务器重定向                 |

| 接口名称     | URL          | 请求方式 | 请求参数                 | 返回值             |
| ------------ | ------------ | -------- | ------------------------ | ------------------ |
| 查询英雄列表 | /hero/list   | get      | 无                       | {heros:[英雄列表]} |
| 查询英雄详情 | /hero/info   | get      | id : 英雄id              | {data:英雄详情}    |
| 编辑英雄     | /hero/update | post     | name , skill , icon , id | {code : 200)       |
| 删除英雄     | /hero/delete | post     | id                       | {code:200}         |
| 新增英雄     | /hero/add    | post     | name , skill , icon      | {code:200}         |

```javascript
//4.设计路由（接口文档）

//(1)查询英雄列表
app.get('/hero/list', (req, res) => {
});

//(2)查询英雄详情
app.get('/hero/info', (req, res) => {
});

//(3)编辑英雄
app.post('/hero/update', (req, res) => {
});

//(4)删除英雄
app.post('/hero/delete', (req, res) => {
});

//(5)新增英雄
app.post('/hero/add', (req, res) => {
});

```



## 英雄管理 - 项目初始化

步骤

1. 新建文件夹`heroManage`
2. 在文件夹中打开终端:`npm init -y`
3. 创建`index.js`
4. 下包`npm i express`
5. `c+v`express的基本结构
6. `c+v`今天要写的路由

## 英雄管理 - 数据库初始化

![1572313078688](assets/1572313078688.png)

步骤:

1. 装包:

   1. `npm i mysql-ithm `
   2. `npm i mysql`
   3. 一行装多个`npm i mysql mysql-ithm`

2. 导包

3. 用包

   1. ```javascript
      //2.连接数据库
      //如果数据库存在则连接，不存在则会自动创建数据库
      hm.connect({
          host: 'localhost',//数据库地址
          port:'3306',
          user: 'root',//用户名，没有可不填
          password: 'root',//密码，没有可不填
          database: 'herodb'//数据库名称
      });
      
      //3.创建Model(表格模型：负责增删改查)
      //如果table表格存在则连接，不存在则自动创建
      const heroModel = hm.model('hero',{
          // 名字 字符串
          name:String,
          // 技能 字符串
          skill:String,
          // 头像 路径 用字符串存
          icon:String
      });
      ```



注意:

1. `mysql` `mysql-ithm`导入
2. `mysql-ithm`保存的变量值 是`hm`
3. `const app = express()`保留
4. 类型记住是大写
5. 端口
   1. 一个端口一次只能被一个软件使用
   2. 3306已经被数据库使用了
   3. 3000被express使用了

![1572315580719](assets/1572315580719.png)

## 英雄管理 - 查询英雄列表

> 读取并返回所有的英雄

![1572315661666](assets/1572315661666.png)

步骤:

1. 注册路由(搞定)
2. 查询所有数据:`heroModel.find((err,result)=>{})`
3. 查询完毕之后:`回调函数中`
   1. 对
      1. 返回给浏览器`response.send({heros:[英雄列表]})`
   2. 错
      1. 返回服务器内部错误,

注意:

1. 返回的格式按照接口文档的来
2. 读取成功或者失败都会返回值
3. 最下面的测试返回值,注释掉了
4. 花姐加了一条测试数据,大伙没加

## 英雄管理 - 查询英雄详情

> 根据id查询出某一个英雄

![1572317733695](assets/1572317733695.png)

实现:

1. 注册路由
2. 回调函数中
   1. 获取id:`request.query.id`
   2. 查询数据(数据库):`heroModel.find('id='+id,(err,result)=>{})`
   3. 查询的回调函数中
      1. 对
         1. 查询出了数据
            1. 返回
         2. 没有查询出数据
            1. 返回id错误
      2. 错
         1. 500



注意:

1. id的目的是精确的查询出一个
2. 文档,后端的`leader`写,`组长`,`架构`
3. find方法哪怕只有一条数据也是数组,没有数据也是数组
4. 最初的测试返回的结果,一定要注释掉

## 英雄管理 - 新增英雄

> 新增英雄数据,名字和技能是字符串,icon是文件路径,文件需要上传到服务器

![1572321007589](assets/1572321007589.png)

步骤

1. 注册路由
2. 回调函数
   1. 接收post提交的文本`body-parser`
      1. 装包,导包,用包
   2. 接收post提交的文件`express-fileupload`
      1. 装包,导包,用包
   3. 获取数据
      1. 名字:name  `request.body.name`
      2. 技能:skill``request.body.skill``
      3. icon:`request.files.icon.name`
   4. 移动文件
      1. ``request.files.icon.mv(路径,回调函数)`
   5. 保存数据到数据库:`heroModel.insert(数据,回调函数)`
   6. 回调函数中
      1. 返回结果

注意:

1. 包名,复制,`求你们了`
2. 使用包的代码顺序
   1. 在app的后面才可以
3. es6新语法使用:
   1. 老语法还是兼容的
   2. 用新看起来逼格高,日后工作时,绝大多是都是es6新语法
4. 第三方模块的使用:
   1. 新建项目
   2. c+v示例代码 没问题
   3. 迁移到项目中



## 英雄管理 - 删除英雄

> 删除某一个英雄

![1572322753416](assets/1572322753416.png)

步骤:

1. 注册路由
2. 回调函数中
   1. 接收id`request.body.id`
   2. 删除数据
   3. `heroModel.delete('id=${id}',(err,result)=>{})`
   4. 删除数据的回调函数中
      1. 没错 返回 
      2. 有错 500

## 英雄管理 - 编辑英雄

![1572331098720](assets/1572331098720.png)

步骤

1. 注册路由
2. 回调函数中
   1. 接收文本
      1. `name,skill,id`  `request.query`
   2. 接收文件名字
      1. `icon` `request.files.icon.name`
   3. 移动到`uploads`中
   4. 修改数据:`heroModel.update('id=${id}',{对象},(err,result))`
      1. 修改数据的回调函数中
         1. 对:`{code:200}`
         2. 错:500



注意:

1. 文件的上传和post文本的获取需要依赖于
   1. `body-parser`post文本
   2. `express-fileupload`post文件
2. postman测试
   1. 参数要和文档一致
3. 数据不改变
   1. 修改id存在的数据
   2. 最初新建表格的时候,和最终的表头不相同
      1. 删除表格,重新执行代码

## 前后端工作分工

1. 后端:------------------------------->写接口
2. 前端:写静态,写js效果--------->调用接口

## 整合静态页面

步骤

1. 把`其他资料/web`文件夹拷贝到`heroManage`项目的根目录
2. `index.js`中 增加`app.use(express.static('web'))`
3. 可以通过和接口同源的地址,访问`web文件夹`下面的页面
4. `http://127.0.0.1:3000/index.html` 访问到页面了
5. 调用接口时
   1. url:`/hero/list`
   2. 自动把左侧的基地址补上去

## 接口调用 - 英雄列表

步骤

1. 调用接口`/hero/list`
2. 调用成功之后渲染到页面上
   1. 定义模板
   2. 挖坑
   3. 起名字
   4. 填坑
   5. `template(模板id,数据)`
   6. 渲染到页面上

注意:

1. 图片默认访问不到
2. 去`index.js`中增加`app.use(express.static('uploads'))`
   1. 把`uploads`暴露出来,外部才可以访问的到

## 接口调用 - 英雄新增

步骤-图片预览:

1. 文本绑定`change`事件
   1. `this.files[0]`
   2. `URL.createdObjectURL()`
   3. 把生成的url设置给`img`的`src`属性

步骤 - 英雄新增

1. 点击新增
2. 创建formData
   1. 表单元素的`name`属性和接口要求的`key`要一致
3. $.ajax
   1. url:`/hero/add`
   2. type:`post`,
   3. data:formData
   4. contentType:false,
   5. processData:false
   6. success(){}

## 接口调用 - 英雄删除

步骤

1. 点击删除
   1. 事件绑定给tbody,用委托的方式指定触发的元素
   2. confirm确认
2. 调用删除接口
   1. url:`/hero/delete`,
   2. type:`post`,
   3. data:{id:id},
      1. id去找父元素获取
   4. success()
      1. 判断
      2. 重新获取数据

## 接口调用 - 英雄编辑01

> 进入编辑状态

步骤

1. `index.html`中用事件绑定的方式为编辑按钮绑定点击事件

2. 获取父元素上的`data-id`

3. 跳转到`add.html?id=具体的值`

4. `add.html`页面中

   1. 获取id

   2. 调用根据id查询数据的接口

      1. url:`/hero/info`,
      2. type:`get`,
      3. data:{id},
      4. success
         1. 把数据渲染到页面上
            1. id保存到隐藏域中`type=hidden`

      

## 接口调用 - 英雄编辑02

> 保存

步骤

1. 点击保存
2. 创建formData
3. 调用接口
   1. url:`/hero/update`,
   2. data:formData
   3. type:post,
   4. processData:false,
   5. contentType:false
   6. success
      1. backData.code==200
      2. 提示用户
      3. 去首页

## Mockjs 模拟数据生成

> Mock模拟数据

1. Mockjs的js库,可以生成随机的测试数据

    http://mockjs.com/

2. Mockjs生成随机测试数据



1. 

## 补充 - 快捷键

1. home,end:行头,行位
   1. mac: fn+左右
2. shift+home或end:选中一行
3. ctrl+左右:识别词组跳跃
4. vscode中快捷键:
   1. ctrl+enter:光标换行,文字不换行
   2. ctrl+shift+enter:光标去上一行,文字不动

 https://code.visualstudio.com/shortcuts/keyboard-shortcuts-windows.pdf 

## 补充 - typora主题

> 如何自定义typora**主题**

