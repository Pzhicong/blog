使用express生成了package.json，它只产生了javascript的app.js和routes/index.js。模版引擎ejs有文件index.ejs，此外还有样式表style.css。
创建工程时候一直使用jade。要求用ejs

一、app.js 工程的入口。
  分析代码：
      1.我们导入了express模块，前面我们通过npm install依赖上了，在这里就可以直接通过require获取、
      2.routes是一个文件夹形式的本地模块，即./routes/index.js，他的功能是为指定的路径组织返回内容，相对于mvc架构中的控制器。
      3.app.set是Express的参数设置工具，接受一个键(key)和一个值(value)，可以用的参数如下：
           basepath：基础机制，通常用于res.redirect()跳转
           views：视图文件的目录，存放模版文件
           port：指定的端口
           view engine:视图模块引擎(推荐使用ejs)
           view options：全局视图参数对象
           view cache：启用视图缓存
           case sensitive routes：路径区分大小写
           strict routing：严格路径，启用后不会忽略路径末尾的"/"
           jsonp callback：开启透明的jsonp支持
      4.Express依赖于connect，connect更加短小精悍，是一个偏向基础设施的框架，提供了大量的中间件，可以通过app.use启用。
         中间件：一系列的组件连接到一起，然后让http的请求依次流过这些组件。这些被connect串联起来的组件被称为中间件
         app.configure中启用了五个中间件：
            bodyParser：解析客户端请求。
            router：项目的路由支持
            static:提供静态文件支持。
            methodOverride：函数重写
            errorHandler：错误控制器
            connect详解：http://cnodejs.org/topic/4fb79b0e06f43b56112b292c
      5.app.get('/',routes.index)，是一个路由控制器，用户如果访问'/'路径，则routes.index来控制。
      6.通过express.createServer()函数创建一个应用的实例

二、routes/index.js是路由文件，相当于控制器，用于组织展示的内容。
    app.js中通过app.get('/',routes.index)将'/'路径映射到exports.index函数下，其中只有一个语句，res.render('index',{title:"pcat"})，功能是
调用模版解析引擎，并传入一个对象作为参数，这个对象只有一个属性，即title

三、index.ejs模版文件，即routes.index.js中调用的模版。
        它的基础是HTML语言(我们降低了学习难度)，其中包含了<%=title%>的标签，功能是显示引用的变量。即res.render函数的第二个参数出啊如的对象的属性.
 
