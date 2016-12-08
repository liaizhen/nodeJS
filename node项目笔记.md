# 项目流程
 ## 公司部门
    1.开发部门
       后台  java php .net
       前端   ios  android   web前端
         结合UI设计稿一交互稿作为参考，最终利用相关技术完成静态的页面展示。
         前端开发的工作职责：
           1.交互稿+ui设计稿完成静态页面，就要考虑到整个前端系统的优化（gulp，grun,webpack,里面的包其实是需要js去做技术支撑的），还要掌握流行框架
           2.前端不只是实现静态页面，还需要利用ajax去动态化其中的数据，并且，这个数据也有肯是后台提供的，也可能是前端开发人员自己需要提供的，必须要掌握nodejs
       ui部门  出平面图 --ui设计稿
    2.产品部（自己系统）/需求部门（外包）
      和客户去交流，你要将这个系统做出什么样子，里面的功能。最终出一个需求文档，完成交互稿
    3.测试部门
    4.运维和维护部门
    5.运营部门
  ## 项目流程
    成员构成：
      主管（技术经理/项目经理）1
      高级工程师   1
      中级工程师   2
      初级工程师   4
      主管：根据业务分配模块和功能（项目框架的准备），将来所有的开发者在这个项目上开发属于自己的那块功能，主管也会每天检查开发者的进度（svn,git）
      高级与中级工程师：负责这个系统的核心模块
      初级工程师：参考人家的demo去写自己的模块
  ## 项目的模块构成：后台管理系统，移动端播放网站，微信推广系统
  ### 项目模块一：后台管理系统
    1.设计数据库（设计表和字段）
        userinfo
       uid-整型/长整型  主键，自增
       uname--varchar(50)
       upwd---varchar(50)
       ustatus---int  1:离职 0：正常
       videoinfo
      vid  int ,pk 自增
      title   varchar(50)
      vsortnum  int
      vvideoID varchar(50)
      vsummary   varchar(255)
      vremark    text
      vimg       varchar(255)
    2.搭建后台管理系统的框架（ 设计数据库与搭建后台管理系统的框架都是项目经理的职责。）
      a.确定mvc这种结构
      b.确定好整个项目结构的文件夹结构
      c.利用MVC和express来将整个系统的结构分离跑通，作为一个基本的结构开发人员使用
      d.将这个结构利用git进行版面管理
    3.公司针对src与dist目录做法
    src是开发文件
    dist是正式发布以后的运行文件（生成环境）
    但是在开发过程中,有可能也需要运行dist,所以dist与src被express被监听的端口一定是不一样的，不然就会有冲突。
    4.express开启网站步骤
       1.安装express   npm i express --save
       2.导入express
      3.实例一个app
      4.设定路由规则
      5.监听端口
    5.index.js的职责：项目的统一入口
       1. 进行一个判断，判断当前的环境
      env=process.env
       2.端口：问题是在src,因为dist是src的副本，所以要将端口配置成变量
    6.package.json文件中的scripts中的作用,在script中配置的代码可以使用npm run,配置的key即可自动执行。
       "dev":" cross-env PORT=8876 NODE_EVN=dev nodemon ./index.js" ,
       "dist":" cross-env PORT=8878 NODE_EVN=dist nodemon ./index.js"
    在外面开发系统的时候,一般会在scripts中配置两个key。
    'dev':只要执行npm run dev就可以去执行src下面的代码
    'dist':要执行npm run dist就可以去执行dist下面的代码
    注意：由于package.json中scripts是通过set PORT进行夸平台来设置环境变量,其他的操作系统是不兼容的set指令，所有要通过第三方包：cross-env来进行夸平台设置环境变量
    app.js的职责：仅仅是开启一个web服务器,而不需要管其他的（路由等）
    7. xtpl.renderFile('相对路径')
     自动根据web服务器的启动路径目录当做相对路径前面的绝对路径+相对路径作为test.html的绝对路径。
     项目工程自动化（脚手架）
    8.gulp
     项目中我们要利用gulp做的事情就是网站的优化
     1.js压缩
     2.css压缩
     3.img压缩
     4.css文件添加md5的后缀  site-css-->site-sddd.css:原因：我们系统中的css和js和图片被浏览器访问过一次之后就可能不会被浏览器重新加载过来，会导致功能看不到，这个时候一般是通过ctrl+f5在浏览器请求缓存数据。只要这个静态文件的内容发生改变，md5字符串就会发生改变，从而导致url发生改变
     css文件添加md5的后缀作用：
      a.防止浏览器对于这个 文件缓存
      b.cdn也是用来做静态资源缓存的,与浏览器的缓存原理一致。
     浏览器缓存原理：如果请求的静态资源url不改变的话，则会缓存这个数据
     5.利用gulp实现文件拷贝
     6利用gulp的插件实现自动将html的css的引用路径进行替换。

    9.gulp的使用回顾
     入口文件  gulpfile.js
     gulp的API
        task
        src
        pipe
        dest
    使用步骤
       1.在项目的根目录下建立一个gulpfile.js文件
       2.安装gulp
          全局安装  npm i  gulp -g
          本地安装  npm i gulp --save-dev
       3.导包  gulpfile.js导入gulp包
       4.根据需求来导包
    10.执行
     gulp 指定任务名称
    js代码的压缩必须要保证语法时候es5语法，不是不是则要用gulp-babel进行转换。
# 总结：
   ## 数据库的设计
   ## 搭建框架
      1.分析确定框架的目录结构
          src:用于开发
          dist:用于生产环境，所有的dist文件都是用gulp进行了压缩，真正在互联网的请求的静态资源的大小一定要远远小于开发环境中的资源的大小，那么服务器的响应速度会快很多，达到了网站额优化的目的
          复习gulp的使用
          学习gulp-babel的使用，将es6语法转换成es5语法
      2.controller：业务逻辑处理
          数据库的操作（orm）
          页面的渲染(xtpl)
      3.routers：负责设定路由对象，并且在路由对象上设定路由规则，同时调用controller中控制器js进行业务逻辑的 处理。
      4.view
      5.app.js作用：利用express开启web服务器
          a.在app.js要初始化对象中的模型数据
          b.在app.js中通过app.use(express.static());将statics文件夹当做项目的静态资源文件夹。
      6.index.js-->整个系统的入口，是执行了 npm run dev 或npm run dist指令
          a.在package.json的scripts加入了dev与dist指令
          b.设定了环境变量：NODE_EVN ,PORT
          c.set PORT=7788 由于set指令是不能实现跨平台的设置环境变量，所以我们用cross-env带代替set来设置环境变量。
    ## 自己动手做的步骤：
     1.将node_modules这个文件夹放到自己要开发的这个项目的父级目录中
     2.创建文件夹：src和dist
     3.利用npm init -y生成一个package.json的文件
     4.package.json文件中的scripts节点中增加如下指令
      "dev":cross-env PORT=8878 NODE_ENV=dev nodemon ./index.js
      "dist":cross-env PORT=8877 NODE_ENV=dist nodemon ./index.js
      nodemon:用来自动重启服务器，一旦js中的文件内容发生改变，服务器就会自动重启。安装的时候也必须要全局安装  npm i cross-env -g
      cross-env是一个三方包，安装的时候是在cmd中运行，多有必须要全局安装
         npm i nodemon -g
     5.在项目的根目录下建一个index.js文件
     6.在src下创建一个app.js，app.js文件的作用
      a. 开启服务器
      b.路由规则与控制器的分离
      c.初始化orm
      d.将statics目录当做静态文件的目录
     7.利用gulp进行自动化工作（将src中的代码通过压缩以后拷贝到dist目录文件中）
    8.补充内容：
      npm i express --save / npm i express  / npm i express --save-dev  三者的区别
     通过npm i express --save下载的文件是存放在 "dependencies": {}这个对象中
     通过npm i express --save-dev下载的express安装的包存放"devDependencies": {}这个对象中
     当一个项目中没有node_modules的时候，我们只要执行npm install 它就会指向package  .json文件中的devDependencies和dependencies中所有所有的包并且下载好
    如果只想下载dependencies中的所有包，应该使用npm install -production
 *****************************************************************************
  # 第二天笔记
  ## 补充知识：
      1.渲染过程：就是将浏览器不认识的代码转换成浏览器认识的代码（html.css.js）
      2.url中和路由规则中参数的获取
       a: http://127.0.0.1:8989/test?id=10&name=abc
        获取参数中id的方法
        req.query.参数名   let id=req.query.id
       b. http://127.0.0.1:8989/test/10
       在路由中带参数 'adminRouter.get('/admin/edit/:id',adminCtrl.getedit);
         获取路由中的参数：req.params['id1'] 或者id=req.params.id
         let id=req.params['id1']; 或者id=req.params.id
  ## 不支持MySQL驱动
    npm i mysql orm ,npm link mysql
  ## 内容简介
    a.后台管理页面(videoinfo)
       视频列表
       视频的新增
       视频的编辑
       视频的删除（ajax）
       富文本编辑器
     b.登录
  ## 开发步骤
     利用git管理我们的代码，利用生成nodejs的 .gitignore文件放在项目的根目录。
     利用git执行文本的版本管理步骤
       1.git init  初始化仓库  生成.git文件
       2.git add * 添加所有的文件
       3.git commit -m '' 文件提交
       4.git remote origin  仓库名  为仓库取一个别名，可以随意取
       5.git push -u origin master 这里的origin要和第四步的origin保持一致
    2.使用.editorconfig来统一各个开发工具的代码风格
       在项目团队中如果每个程序员对于代码风格的设置不一样的话，是不被允许的（比如空格的设置），所以在项目中的根目录中增加.editorconfig来统一固定的好所有的代码风格。
       sublime中如果能够正常读取和应用.editorconfig，需要装一个插件
    3.后台管理页面的静态实现（bootstrap）
    4.富文本编辑器
    1.作用：帮助我们的文字或者图片进行样式的控制，比如加粗
    2.ueditor for nodejs
       a.如何将富文本编辑器在html页面上自动生成，（这个编辑器本身与js没有关系，只要用css就可以实现，但是由于有图片上传，所以要用到js）
       b.步骤:
         1：引入三个js脚本
         ueditor.config.js
         ueditor.all.min.js
         ueditor/lang/zh-cn/zh-cn.js
         注意：  注意点：一定要将node_modules\ueditor\example\public\ueditor这个文件夹拷贝到 项目的statics文件夹中
         2：将id='editor'的script标签放在需要生成富文本编辑器的地方
          <script id="editor" type="text/plain" style="width:1024px;height:500px;"></script>
         3.调用UE.getEditeor('editor'),来生成富文本编辑器
       c.上传图片（一定要借助nodejs的web服务器的某个路由规则才行）
         获取请求体中的数据的方式
           第一种方式：route.post('/admin/add',(req,res)=>{
             req.on('data',(data)={
              console.log(data);
             }
           });
           第二种方式，通过bodyParser,这是个第三方包作用：用来接收浏览器通过post请求时候的请求报文体中的数据
             使用步骤：
               1.现在app.js使用app.use(require('body-parse'){});
               2.通过req.body.vtitle来获取post中请求体中是数据
         a.bodyParser,这是个第三方包作用：用来接收浏览器通过post请求时候的请求报文体中的数据
         bodyParser使用步骤：
           1.导包
            const bodyParser = require('body-parser');
            const ueditor = require('ueditor');
           2.将bodyParser这个包加载在express
             app.use(bodyParser());
           3.设置上传图片的路由规则代码（app.js）
           1.将ueditor(path.join(__dirname, 'statics')中的statics修改成自己静态文件夹名称
              ueditor路径
               ueditor这个文件夹放入statics中
              重定向的路径
              res.redirect('/ueditor/nodejs/config.json');
           4.我们上传到服务器的图片保存地址statics/images/ueditor/图片
           5.在express中使用中间键（body-parsers）的注意点，最好写在所有路由加载之前
           富文本内容的填充时机：
             在富文本编辑器加载完成之后，在执行富文本内容的填充。
    *****************************************************************************************
  # 第三天笔记
   ## 请求数据的方式：
        $.get(url,参数对象，成功的回调函数，服务器响应回来的数据格式)
        $.post(url，参数的对象，成功回调函数，服务器响应回来的数据格式)
        $.json(url,参数对象，成功的回调函数)
        $.ajax()最全的
   ## session和cookie(原因是http协议是无状态的,所以需要session和cookie用来维持服务端的状态,以及来标识浏览器的身份)
   ### set-cookie:标记浏览器的身份id，当浏览器获取到set-cookie指令之后，就会将这个身份id保存在内存中或者磁盘中,当下一次发送该页面的其他请求是,就会带上这个cookie,这个时候服务器就是识别该请求 是来自于那个浏览器.
        浏览器会将cookie存储在本地
         cookie:
          1.定义：cookie是客户端的一种能够存储少量(4k)文本的技术，类似于sessionStorage和localstorage
          2. 作用：一般就是用在登录以后的状态维持的浏览器身份id的保存（express-session用的就是这种技术）
         session:定义：是一种服务器端的技术,一般结合cookie来使用,用来维持服务端的状态,session的本质上就是再浏览器中开辟了一块空间
         ,这个空间的存储方式是通过键值的方式进行存储,键存储的是浏览器的身份id,而值(value)其实又是一个对象,这个对象中存储形式又是键值对的
         形式存储,这里面的键是用户自定的键,比如值对应就是我们登录中图片验证码之类的信息.
   ## 密码加密（MD5加密）
       加密的方式：
        SHA1
        SHA128
        SHA256
        MD5
        1.对称加密：可逆
        2.非对称加密：
          公钥：负责加密，通常是在互联网上流通
          私钥：负责解密，一般存储在服务器上的
          应用：https,加密
          http：所有的数据 都 是以明文的方式在互联上流通，而HTTPS是通过加密（通过公钥加密）， 以后将 数据在互联网流通的
         解密：都是私钥来进行解密
        行业规则：MD5加密的密码是不可逆转（简单的密码可以被一些网站暴力破解）
   ## 分页功能
         在公司里面，通常一页显示10条
         orm.models.videinfo.find({}{
            offset:跳过到少条
            limit:取得多少条
         })
        确实这个分页的总页数：
        算法：分页的总页数=videoinfo表的数据总条数/页容量
        req.models.cideinfo.count({},(err,count)={
          count代表数据库中的数据总条数
        })
        思路：1.
   ## 完善gulp打包到dist
   ## mysql的语句语法
 ****************************************************************************************
   # 第四天笔记
   ## session和cookie
      session是一种服务端的技术，它通过key-value形式存储在服务器端
       express-session
       cookie:是客户端（浏览器）的一种技术，用来存储少量的文本数据（4k）
   ## mysql的语句
      sql语句的：就是为了能够将数据查询出来，数据库提供了一套指令
      sql分为：
       0.use dbname :表示使用哪个数据库
       1，插入：
       语法：insert into 表名称（字段1，字段2,...）values
       (字段1的值，字段2的值)
       insert into userinfo(uname,upwd,ustatus) values ('admin','123',0)
      mysql的客服工具
      2.查询
         select * from 表名称
         select 字段名1，字段名2，...from 表名称
         select * from 表名称 limit 逃过多少条数据,拿多少条
         select * from 表名称 where 字端='值
         select * from 表名称 where like='%条件值%'
         select * from 表名称 where like='条件值%'
         select * from 表名称 where like='%条件值'
         select * from 表名称 字段的值>条件值
         select * from 表名称 where 主键值 in（1,2）
         select * from 表名称 where 主键值=1 or 主键值=2
          select * from 表名称 where 字段值='条件1' and 字段值='条件2'
          统计一个表中的数据的总条数
          select count(*) from userinfo
       3.需改
            update 表名称 set 字段1=更新的值，字段2=更新的值，...
            update 表名称 set 字段1=更新的值 where 条件
        4.删除
            delete from 表名称 清空表的数据
            delete from 表名称 where 条件
        5.连表查询
            内联
            select * from 表名称1 as t1，表名2 as t2 where t1.外建值=t2.主键值
           左连接
           右连接
         6.删除整个表
          drop table 表名称
       作用：将客户端语法语句
   ## 在mysql如何利用orm包去直接发送SQL语句到数据库服务执行
      db.driver.execQuery('带有业务的sql语句'，function(err,data){
      data:参数的值
      //1.如果是select的语句返回的data是一个对象
     //2.如果是非select语句返回的data是一个数组
      })
   ## 实现移动站点进行播放视频
        a.和后台API进行对接
          后台接口的API内容
            1.决定请求的地址api(url),如果API中有参数，要说明参数代表额意义
            2.决定请求的方式，post、get,或者两者都有
            3.决定通过ajax返回回来的数据格式json，XML
            4.返回数据格式中的每个字段的表示的意义
        b.子系统：
          i:利用nodejs开启后台的API（使用orm+MySQL语句的形式去获取数据）
          ii:利用MUI这个前端框架来实现移动站点
  ## 利用HBULider这个开发工具的云服务将移动站点打包成apk
  ## 跨域
  ## videoApp
     移动站点：一般是类似于m.jd.com m.taobao.com  在浏览器打开的，要放在服务器上进行托管（目前使用express）
     移动APP：这种类似于原生的app,直接将打包安装到手机上，将来手机就会自动利用HBlukder的基座打开一个内置的浏览器，
 ********************************************************************************************
  # 项目第五天学习内容---微信开发模块
  ## 学习微信的开发
     注册号微信公众平台之后,利用它的后天可以直接发布(无需开发经验)
     a.
  ## 学习微信的API的使用
     订阅以后自动发送消息到手机上
     当用户发送一条消息的时候,我们的服务器主动回复内容
  ## 用户自定义微信开发步骤
    1.关闭微信本身的自动回复功能
    2.把资料补全,进入到基本配置菜单--基本配置
    3.填写相关的信息
      参数说明:
       url:自己开发的微信服务器的对外的地址
       token:随意写,密码加密
       消息加密方式:在开发过程中使用明文,方便调试
    4.如何生成url
     用来给微信服务器向我们自己的开发的服务上进行消息推送,这个地址要想写成功,需要自己在开发的服务器端写代码
    5.url的验证过程
     1.服务
     将我们自己开发好的url填充到微信公众平台的修改配置中的url以后,微信服务器会自动发送一条请求到达我们服务器.由于我们的服务器设备内有给微信服务器响应一个它的要求的合法的字符串,所以微信服务器此时认为我们填写的url是一个不合法的url,所以拒绝通信
    6.如果验证成功指挥员,将来微信服务器
    1.用户关注后,响应回去
      1.0解析xml (xml2js),将xml解析成对象
      2.0分析里面的msgtype是一个event类型,event的节点中一定是一个subscribe(表示已关注公众号)
      3.0处理之后将对象以xml的格式响应回去
        响应回去数据格式可以是图文的,也可以是纯文本的
    7.SVM的使用
     1.A第一次向一个空仓库提交文件,称之为导入,没有.SVN文件,所以不能与服务器进行通信
     2.B所有的成员要将文件拉下来做开发,称之为检出(迁出)
     3.B对于一个新文件,所以要将新文件增加再签入(checkin)
    4.A当一个用户修改了原有的文件,只需要提交(checkin)即可
    5.B当使用A修改的文件,只需要更新就可以update
    6.冲突:是多个用户修改了同一个文件导致的,最后一个要update的那个用户就会发现冲突,发现冲突,就点击冲突字眼那一行就可查看
    解决方法:如果文件前面是等号,随便使用哪个即可,如果不是等号的就先使用其他用户更新的代码或者使用自己更新的代码就可以解决该冲突,然后在进行提交就可以.
    8.mongodb
     mysql oracle sqlsever  关系型数据
     noSQL(非关系数据)
     mongodb(文档型数据库),resis(缓存)
    1.组成mongodb的几种服务软件
     mongodb的监听端口号时候27017
    2.mongodb客户端软件
    3.mongodb可以建立 数据库,但是不可以建表,可以通过mongoose这个第三包来建表
     步骤:  1.安装mongoose  npm imongoose --save
            2.根据mongoose去操作数据库
            代码编写步骤
              1.导包
              2.定义一个数据库连接的字符串
               mongodb://数据库服务器ip/你的数据库名
             3.通过connect（）连接
             4.定义表的结构mongodb.Schema()
             5.通过mongoose.models(表名,表的结构)定义模型,返回一个模型
             6. 通过第五步返回 的模型进行增删查改
               create(一个表结构的对象,回调函数(err,data));
               find({查询条件},回调函数(err,data))
               update(条件,更新的字段js对象,回调函数(err))
               remove(条件,回调函数(err));
       ```
       'use strict';
       const dbConnStr='mongodb://127.0.0.1/test';
       mongoose.connect(dbConnStr);
       let Schema=mongoose.Schema,
       ObjectId=Schema.ObjectId;//代表自动生成的主键
        let userinfoSchema=new Schema({
        uid:ObjectId,//表示的是一个对象
        uname:String,
        upwd:String,
       });
       let userinfoModel=mongoose.model('userinfo',useeinfoSchema);
         userinfoModel.find({查询条件},callback(err,data))
         userinfoModel.creat(对象，callback(err, res))
         userinfoModel.update(where,set，callback(err))
         userinfoModel.remove(where,callback(err))
   ```












