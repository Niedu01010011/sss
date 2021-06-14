# Node.js

## 1.初识Node.js

1. **什么是node.js**

   Node.js是一个基于chrome V8引擎的JavaScript运行环境。

   + 浏览器是javaScript的前端运行环境

   + Node.js是JavaScript的后端运行环境

   + node.js中无法调用DOM和BOM等浏览器内置API

     ![image-20210322220139130](C:\Users\29635\AppData\Roaming\Typora\typora-user-images\image-20210322220139130.png)

2. **终端快捷键**

   ![image-20210322222027349](C:\Users\29635\AppData\Roaming\Typora\typora-user-images\image-20210322222027349.png)

## 2. fs文件系统模块

1. **什么是fs文件系统模块**	

   fs模块是Node.js官方提供的、用来操作问价男的模块。它提供了一系列的方法和属性，用来满足用户对文件的操作需求。

   ![image-20210322235621753](C:\Users\29635\AppData\Roaming\Typora\typora-user-images\image-20210322235621753.png)

2. **fs.readFile()**

   1. 语法格式

      ```js
      fs.readFile(path[,options],callback)
      ```

      

      ![image-20210322235820868](C:\Users\29635\AppData\Roaming\Typora\typora-user-images\image-20210322235820868.png)

      示例：

      ​	![image-20210322235930979](C:\Users\29635\AppData\Roaming\Typora\typora-user-images\image-20210322235930979.png)

   2. 判断是否读取文件成功

      ![image-20210323002036768](C:\Users\29635\AppData\Roaming\Typora\typora-user-images\image-20210323002036768.png)

3. **fs.writeFile()**

   1. 语法格式

      ![image-20210323003038522](C:\Users\29635\AppData\Roaming\Typora\typora-user-images\image-20210323003038522.png)

   2. 示例代码

      ![image-20210323003049525](C:\Users\29635\AppData\Roaming\Typora\typora-user-images\image-20210323003049525.png)

4. **案例：成绩整理**

   1. ![image-20210323010149129](C:\Users\29635\AppData\Roaming\Typora\typora-user-images\image-20210323010149129.png)

   2. ![image-20210323010205181](C:\Users\29635\AppData\Roaming\Typora\typora-user-images\image-20210323010205181.png)

      ```js
      const fs = require('fs');
      //__dirname表示当前文件所处的目录
      fs.readFile(__dirname + '/file/grade.txt', 'utf8', function (err, dataStr) {
          if (err) {
              return console.log(err.message);
          }
          const arr1 = dataStr.split(' ');//数组转换为字符串
          
          //arr1.forEach(item => {
          // item.replace(/=/g, ":");
          //});
          
          for (let i = arr1.length - 1; i >= 0; i--) {
              arr1[i] = arr1[i].replace(/=/g, ":");
          }
          const str = arr1.join('\r\n');//字符串转换为数组
          console.log(str);
          fs.writeFile(__dirname + '/file/gradeok.txt', str, function (err) {
              if (err) {
                  console.log('fail' + err.message);
              }
              console.log("sucess!");
          })
      })
      ```

      + __dirname表示当前文件所处的目录

## 3.path路径模块

1. **什么是path路径模块** 

   path模块是Node.js官方提供的、用来处理路径的模块。它提供了一系列的方法和属性，用来满足用户对路径的处理需求。

   ![image-20210323142602165](D:\vue\Node.js.assets\image-20210323142602165.png)

2. **路径拼接path.join()**

   1. 语法格式：

      ```
      path.join([...paths])
      ```

      ...paths<string>路径片段的序列

      返回值<string>

   2. 代码示例：

      ![image-20210323142951243](D:\vue\Node.js.assets\image-20210323142951243.png)

      + ../会抵消一个路径

3. **获取路径中的文件名path.basename()**

   1. 语法格式：

      ![image-20210323143730541](D:\vue\Node.js.assets\image-20210323143730541.png)

   2. 代码示例：

      ![image-20210323143744850](D:\vue\Node.js.assets\image-20210323143744850.png)

4. **获取路径中文件的扩展名path.extname()**

   1. 语法格式：

      ![image-20210323144022862](D:\vue\Node.js.assets\image-20210323144022862.png)

   2. 代码示例：

      ![image-20210323144038032](D:\vue\Node.js.assets\image-20210323144038032.png)

## 4.http模块

1. 什么是http模块

   在网络节点中，负责消费资源的电脑，叫做客户端；负责对外提供网络资源的电脑，叫做服务器。

   http模块是Node.js官方提供的、用来创建web服务器的模块。通过http模块提供的http.createServer()方法，就能方便地把一台普通的电脑，变成一台Web服务器，从而对外提供Web资源服务。

2. IP地址

   ![image-20210324125301276](D:\vue\Node.js.assets\image-20210324125301276.png)

3. 域名和域名服务器

   ![image-20210324125416476](D:\vue\Node.js.assets\image-20210324125416476.png)

4. 端口号

   ![image-20210324125457552](D:\vue\Node.js.assets\image-20210324125457552.png)

5. **创建最基本的web服务器**

   1. 创建web服务器的基本步骤

      + 导入http模块
      + 创建web服务器实例
      + 为服务器实例绑定request事件，监听客户端的请求
      + 启动服务器

      ```js
      //1.导入http模块
      const http = require('http');
      //2.创建web服务器实例
      const server = http.createServer();
      //3.为服务器实例绑定request事件
      server.on('request',(req,res)=>{
      	//只要有客户端来请求我们自己的服务器，就会触发request事件，从而调用这个事件处理函数
      	console.log('Someone visit our web server');
      })
      //4.启动服务器
      server.listen(80,()=>{
      	consloe.log('http server running at http://127.0.0.1')
      })
      ```

   2. req请求对象

      只要服务器接收到了客户端请求，就会调用通过server.on()为服务器绑定的request事件处理函数。

      ![image-20210324150234164](D:\vue\Node.js.assets\image-20210324150234164.png)

   3. res响应对象

      在服务器的request事件处理函数中，如果想访问与服务器相关的数据或属性，可以使用如下方式

      ```js
      server.on('request',(req, res)=>{
      	//res是响应对象，它包含了与服务器相关的数据和属性，例如：
      	//要发送到客户端的字符串
      	const str = 'Your request url is ${req.url}, and request method is ${req.method}';
      	//res.end()方法的作用：
      	//向客户端发送指定的内容，并结束这次请求的处理过程
      	res.end(str);
      })
      ```

   4. 解决中文乱码

      ```js
      res.setHeader('Content-Type', 'text/html; charset=utf-8')
      ```

## 5. 模块化

1. **什么是模块化**

   模块化是指解决一个复杂问题时，自顶向下逐层把系统划分成若干模块的过程。对于整个系统来说，模块是可组合、分解和更换的单元。

   把代码进行模块化拆分的好处：

   + 提高了代码的复用性
   + 提高了代码的可维护性
   + 可以实现按需加载

2. **模块化规范**

   ![image-20210324173522605](D:\vue\Node.js.assets\image-20210324173522605.png)

3. **node.js中模块化的分类**

   Node.js中根据模块化来源的不同，将模块分为了三大类，分别是：

   + 内置模块（由Node.js官方提供，例如fs、path、http等）

     ```js
     const fs = require('fs');
     ```

   + 自定义模块（为用户创建的每个.js文件，都是自定义模块）

     ```js
     const custom = require('./custom.js')
     ```

   + 第三方模块（由第三方开发出来的模块，并非官方提供的内置模块，也不是用户创建的自定义模块，使用前需要先下载。）

     ```js
     const moment = require('moment');
     ```

   注意：当使用require（）加载其他模块的时，会执行被加载模块中的代码。

4. **模块作用域**

   和函数作用域类似，在自定义模块中定义的变量、方法等成员，只能在当前模块内被访问，这种模块级别的访问限制，叫做模块作用域。

5. **向外共享模块作用域的成员**

   1. module对象

      在每个.js自定义模块中都有一个module对象，它里面存储了和当前模块有关的信息。

   2. module.exports对象

      在自定义模块中，可以使用module.exports对象，将模块内的成员共享出去，供外界使用。外界用require（）方法导入自定义模块时，得到的就是module.exports所指的对象。

   3. 使用require()方法导入模块时，导入的结果，永远以moudle.exports指向的对象为准。exports和moudle.exports指向同一个对象。

   4. 为了防止混乱，建议在同一个模块不要同时使用exports和moudle.exports

      ![image-20210324220152486](D:\vue\Node.js.assets\image-20210324220152486.png)

6. **Node.js中的模块化规范**

   ![image-20210324220232978](D:\vue\Node.js.assets\image-20210324220232978.png)

## 6.npm与包

1. ![image-20210324232145842](D:\vue\Node.js.assets\image-20210324232145842.png)

2. **包管理配置文件**

   ![image-20210325135511590](D:\vue\Node.js.assets\image-20210325135511590.png)

3. **快速创建package.json**

   ![image-20210325140011796](D:\vue\Node.js.assets\image-20210325140011796.png)

4. **dependencies节点**

   package.json文件中，有一个dependencies节点，专门用来记录使用npm install命令安装了哪些包。

5. **一次性安装所有的包**

   + 当我们拿到一个剔除了node_modules的项目之后，需要先把所有的包下载到项目中，才能将项目运行起来。

   + 可以运行npm install命令一次性安装所有的依赖包

   + 运行npm uninstall命令，卸载指定的包，命令执行成功后，会把卸载的包，自动从package.json的dependencies中移除。

6. **devDependencies节点**

   ![image-20210325140543530](D:\vue\Node.js.assets\image-20210325140543530.png)

7. **解决下包速度慢的问题**

   1. 切换npm的下包镜像源

      ```
      npm config set registry=https://registry.npm.taobao.org/
      ```

   2. nrm

      ![image-20210325143223872](D:\vue\Node.js.assets\image-20210325143223872.png)

8. **包的分类**

   1. 项目包

      ![image-20210325143401417](D:\vue\Node.js.assets\image-20210325143401417.png)

   2. 全局包

      ![image-20210325143542875](D:\vue\Node.js.assets\image-20210325143542875.png)

9. **规范的包结构**

   ![image-20210325145115502](D:\vue\Node.js.assets\image-20210325145115502.png)

10. **开发属于自己的包**

    1. 初始化包的基本结构

       ![image-20210325170322470](D:\vue\Node.js.assets\image-20210325170322470.png)

    2. 将不同的功能进行模块化拆分

       ![image-20210325170359372](D:\vue\Node.js.assets\image-20210325170359372.png)

    3. 终端中：

       1. npm login 登录

       2. npm publish 发布

       3. npm unpublish 包名 --force，删除

          ![image-20210325170526276](D:\vue\Node.js.assets\image-20210325170526276.png)

11. **模块化加载机制**

    1. 优先从缓存加载

       ![image-20210325170823621](D:\vue\Node.js.assets\image-20210325170823621.png)

    2. 内置模块的加载机制

       ![image-20210325170813750](D:\vue\Node.js.assets\image-20210325170813750.png)

    3. 自定义模块的加载机制

       ![image-20210325170803708](D:\vue\Node.js.assets\image-20210325170803708.png)

    4. 第三方模块的加载机制

       ![image-20210325170753737](D:\vue\Node.js.assets\image-20210325170753737.png)

    5. 目录作为模块

       ![image-20210325170740370](D:\vue\Node.js.assets\image-20210325170740370.png)

## 7.Express

1. **Express简介**

   1. 什么是Express

      官方给出的概念：Express是基于Node.js平台，快速、开放、极简的Web开发框架。

      通俗的理解：Express的作用和Node.js内置的http模块类似，是专门用来创建Web服务器的。

      Express的本质：就是一个npm上的第三方包，提供了快速创建Web服务器的便捷方法。

   2. Express能做什么

      对于前端程序员来说，最常见两种服务器，分别是：

      + Web网站服务器：专门对外提供Web网页资源的服务器。
      + API接口服务器：专门对外提供API接口的服务器。

      使用Express，我们可以方便、快速的创建Web网站的服务器或API接口的服务器。

2. **Express的基本使用**

   1. Express安装

      在项目所处的目录中，运行如下终端命令，即可将express安装到项目中使用

      ```
      npm i express@4.17.1
      ```

   2. 创建基本的Web服务器

      ```js
      const express = require('express');
      const app = express();
      app.listen(80,()=>{
      	console.log('express server running at http://127.0.0.1')
      })
      ```

   3. 监听GET请求

      ```js
      //参数1：客户端请求的URL地址
      //参数2：请求对应的处理函数
      //		req：请求对象（包含了与请求相关的属性与方法）
      //		res：响应对象（包含了与响应相关的属性与方法）
      app.get('请求URL'，function(req, res){/*处理函数*/})
      ```

   4. 监听post请求

      ```js
      //参数1：客户端请求的URL地址
      //参数2：请求对应的处理函数
      //		req：请求对象（包含了与请求相关的属性与方法）
      //		res：响应对象（包含了与响应相关的属性与方法）
      app.post('请求URL'，function(req, res){/*处理函数*/})
      ```

   5. 把内容响应给客户端

      通过res.send()方法，可以把处理好的内容，发送给客户端：

      ```js
      app.get('/user', (req, res)=>{
          //向客户端发送json对象
          res.send({
              name: 'zs',
              age: '20',
              gender: '男'
          });
      })
      
      app.post('/user', (req,res) => {
          //向客户端发送文本内容
          res.send('请求成功');
      })
      ```

   6. 获取URL中携带的查询参数

      通过req.query对象，可以访问到客户端通过查询字符串的形式，发送到服务器的参数：

      ```js
      app.get('/', (req, res)=>{
          //req.query默认是一个空对象
          //客户端使用？name=zs&age=20这种查询字符串形式，发送到服务器的参数
          //可以通过 req.query 对象访问到，例如：
          //req.query.name  req.query.age
          console.log(req.query);
      })
      ```

   7. 获取URL中的动态参数

      ```js
      app.get('/user/:id',(req,res)=>{
          //req.params默认是一个空对象
          //里面存放着通过 : 动态匹配到的参数值
          console.log(req.params)
      })
      ```

3. **托管静态资源**

   1. express.static()

      通过express.static()，我们可以非常方便地创建一个静态资源服务器，例如，通过如下代码就可以将public目录下的图片、CSS文件、JavaScript文件对外开放访问了：

      ```js
      app.use(express.static('public'))
      ```

      注意：Express在指定地静态目录中查找文件，并对外提供资源的访问路径。因此，存放静态文件的目录名不会出现在URL中。

      ![image-20210326142938948](D:\vue\Node.js.assets\image-20210326142938948.png)

   2. 托管多个静态资源目录，多次调用express.static()函数

      ```js
      app.use(express.static('public'));
      app.use(express.static('files'));
      ```

      访问静态资源文件时express.static()函数会根据目录的添加顺序查找所需的文件。

   3. 挂载路径前缀

      如果希望在托管的静态资源访问路径之前，挂载路径前缀，则可以使用如下方式：

      ```js
      app.use('/public', express.static('public'))
      ```

      现在，就可以通过带有/public前缀地址来访问public目录中的文件了

      ![image-20210326143336969](D:\vue\Node.js.assets\image-20210326143336969.png)

4. **nodemon**

   1. 为什么要使用nodemon

      ![image-20210326142631218](D:\vue\Node.js.assets\image-20210326142631218.png)

   2. 安装nodemon

      ```
      npm install -g nodemon
      ```

   3. 使用nodemon

      ![image-20210326142728590](D:\vue\Node.js.assets\image-20210326142728590.png)

5. **Express路由**

   1. 路由的概念

      1. 路由就是映射关系。

      2. 现实生活中的路由

         ![image-20210326144515470](D:\vue\Node.js.assets\image-20210326144515470.png)

      3. Express中的路由

         ![image-20210326144737759](D:\vue\Node.js.assets\image-20210326144737759.png)

      4. 路由匹配的过程

         每当一个请求到达服务器之后，需要先经过路由的匹配，只有匹配成功之后，才会调用对应的处理函数。

         在匹配时，会按照路由的顺序进行匹配，如果请求类型和请求的URL同时匹配成功，则Express会将这次请求，转交给对应的function函数进行处理。

         ![image-20210326145308666](D:\vue\Node.js.assets\image-20210326145308666.png)

6. **路由的使用**

   1. 最简单的用法

      在Express中使用路由最简单的方式，就是把路由挂载到app上

      ![image-20210326145452922](D:\vue\Node.js.assets\image-20210326145452922.png)

   2. 模块化路由

      ![image-20210326151610976](D:\vue\Node.js.assets\image-20210326151610976.png)

   3. 创建路由

      ![image-20210326151652889](D:\vue\Node.js.assets\image-20210326151652889.png)

   4. 使用app.use()函数注册路由模块

      ![image-20210326155848881](D:\vue\Node.js.assets\image-20210326155848881.png)

   5. 为路由模块添加前缀

      ![image-20210326151823906](D:\vue\Node.js.assets\image-20210326151823906.png)

7. **Express中间件**

   1. Express中间件的格式

      Express中间件，本质上就是一个function处理函数，Express中间件的格式如下：

      ![image-20210326161933244](D:\vue\Node.js.assets\image-20210326161933244.png)

      注意：中间件函数的形参列表中，必须包含next参数。而路由器处理函数中只包含req和res。

   2. next函数的作用

      next函数是实现多个中间件连续调用的关键，它表示把流转关系转交给下一个中间件或路由。

      ![image-20210326162140373](D:\vue\Node.js.assets\image-20210326162140373.png)

   3. **Express中间件初步了解**

      1. 定义中间件函数

         ![image-20210326162755466](D:\vue\Node.js.assets\image-20210326162755466.png)

      2. 全局生效的中间件

         客户端发起的任何请求，到达服务器之后，**都会触发的中间件**，叫做全局生效的中间件。

         通过调用app.use(中间件函数，即可定义一个全局生效的中间件)

         ![image-20210326162924673](D:\vue\Node.js.assets\image-20210326162924673.png)

      3. 定义全局中间件的简化形式

         直接在app.use(中间件函数)写中间件函数

         ![image-20210326163431084](D:\vue\Node.js.assets\image-20210326163431084.png)

      4. 中间件的作用

         多个中间件之间，共享一份req和res。基于这样的特性，我们可以在上游的中间件中，统一为req或res对象添加自定义的属性或方法，供下游的中间件或路由进行使用。

         ![image-20210326163628291](D:\vue\Node.js.assets\image-20210326163628291.png)

      5. 定义多个全局中间件

         可以使用app.use()连续定义多个全局中间件。客户端请求到达服务器之后，会按照中间件定义的先后顺序依次进行调用。

         ![image-20210326163744547](D:\vue\Node.js.assets\image-20210326163744547.png)

      6. 局部生效的中间件

         不使用app.use()定义的中间件，叫做局部生效的中间件

         ![image-20210326163834711](D:\vue\Node.js.assets\image-20210326163834711.png)

      7. 定义多个局部中间件

         可以在路由中，通过如下两种等价的方式，使用多个局部中间件：

         ![image-20210326164741801](D:\vue\Node.js.assets\image-20210326164741801.png)

      8. 中间件的注意事项

         ![image-20210326164814271](D:\vue\Node.js.assets\image-20210326164814271.png)

   4. **中间件的分类**

      ![image-20210326164926370](D:\vue\Node.js.assets\image-20210326164926370.png)

      1. 应用级别的中间件

         ![image-20210326165059105](D:\vue\Node.js.assets\image-20210326165059105.png)

      2. 路由级别的中间件

         ![image-20210326165119457](D:\vue\Node.js.assets\image-20210326165119457.png)

      3. 错误级别的中间件

         ![image-20210326165218237](D:\vue\Node.js.assets\image-20210326165218237.png)

      4. Express内置的中间件

         ![image-20210326165253173](D:\vue\Node.js.assets\image-20210326165253173.png)

         ​	req.body()使用之前先配置express.json()和express.urlencoded()，(直接在中间件函数之前加此代码)才能解析json和URL-encoded格式的请求体数据，不然默认undefined。

      5. 第三方中间件

         ![image-20210326165328975](D:\vue\Node.js.assets\image-20210326165328975.png)

8. **使用Express写接口**

9. **cors跨域资源共享**

   1. 使用cors中间件解决跨域问题

      cors是Express的一个第三方中间件。通过安装和配置cors中间件，可以很方便地解决跨域问题

      + 运行npm install cors 安装中间件
      + 使用const cors = require('cors')导入中间件
      + 在路由之前调用app.use(cors())配置中间件

   2. 什么是cors

      cors由一系列HTTP响应头组成，这些HTTP响应头决定浏览器是否阻止前端JS代码跨域获取资源。

      浏览器的同源安全策略默认会阻止网页跨域获取资源。但如果接口服务器配置了CORS相关的HTTP响应头，就可以解除浏览器端的跨域访问限制。

      ![image-20210326224513509](D:\vue\Node.js.assets\image-20210326224513509.png)

   3. cors注意事项

      ![image-20210326224554284](D:\vue\Node.js.assets\image-20210326224554284.png)

   4. cors响应头部- Access-Control-Allow-Origin

      + ![image-20210326224732540](D:\vue\Node.js.assets\image-20210326224732540.png)

      + ![image-20210326224741771](D:\vue\Node.js.assets\image-20210326224741771.png)

   5. cors响应头部- Access-Control-Allow-Headers

      ![image-20210326225544315](D:\vue\Node.js.assets\image-20210326225544315.png)

   6. cors响应头部- Access-Control-Allow-Methods

      ![image-20210326233417174](D:\vue\Node.js.assets\image-20210326233417174.png)

   7. 简单请求与预检请求

      + 简单：

        ![image-20210326233448260](D:\vue\Node.js.assets\image-20210326233448260.png)

      + 预检

        ![image-20210326233522231](D:\vue\Node.js.assets\image-20210326233522231.png)

      + 区别

        ![image-20210326233537977](D:\vue\Node.js.assets\image-20210326233537977.png)

## 8.MySQL数据库

1. 在项目中安装mysql模块

   ```
   npm install mysql
   ```

2. 配置mysql模块

   ![image-20210327154041224](D:\vue\Node.js.assets\image-20210327154041224.png)

3. 测试mysql模块能否正常工作

   ![image-20210327154107201](D:\vue\Node.js.assets\image-20210327154107201.png)

4. 查询，添加，更新，删除操作

   ```js
   //查询
   db.query('SELECT * from message', (err, results) => {
       if (err) return console.log(err.message);
       console.log(results);
   })
   
   // 插入数据
   const user = { username: 'ls', password: 'nmsl', status: 0 };
   const sqlStr = 'insert into message set ?';
   db.query(sqlStr, user, (err, results) => {
       if (err) return console.log(err.message);
       if (results.affectedRows === 1) { console.log('插入数据成功') };
   })
   
   // 更新
   const user = { id: 4, username: 'aaa', password: 'fxxk', status: 0 };
   const sqlStr = 'update message set username=?,password=?where id=?';
   db.query(sqlStr, [user.username, user.password, user.id], (err, results) => {
       if (err) return console.log(err.message);
       if (results.affectedRows === 1) { console.log('更新数据成功') };
   })
   
   // 删除
   const sqlStr = 'delete from message where id =?';
   db.query(sqlStr, 4, (err, results) => {
       if (err) return console.log(err.message);
       if (results.affectedRows === 1) { console.log('删除数据成功') };
   })
   ```

5. 标记删除

   使用delete语句，会真正的把数据从表中删除掉。为了保险起见，推荐使用标记删除的形式，来模拟删除的动作。所谓标记删除，就是在表中设置类似于status这样的状态字段，来标记当前这条数据是否被删除。

   当用户执行了删除动作时，我们并没有执行delete语句把数据删除掉，而实执行了update语句，将这条数据对应的status字段标记为删除即可。

   ![image-20210327154610335](D:\vue\Node.js.assets\image-20210327154610335.png)

## 9.前后端的身份认证

1. Web开发模式

   目前主流的Web开发模式有两种，分别是：

   + 基于服务端渲染的传统Web开发模式

     服务器发送客户端的HTML页面，是在服务器通过字符串的拼接，动态生成的。因此客户端不需要使用Ajax这样的技术额外请求页面的数据。

   + 基于前后端分离的新型Web开发模式

     依赖于Ajax技术的广泛应用。简而言之，前后端分离的Web开发模式，就是后端只负责提供API接口，前端使用Ajax调用接口的开发模式。

2. 身份认证

   服务端渲染推荐使用Session认证机制。

   前后端分离推荐使用JWT认证机制。

3. Session认证机制

   1. Http协议的无状态性

      ![image-20210327162600120](D:\vue\Node.js.assets\image-20210327162600120.png)

   2. 如何突破HTTP无状态的限制

      ![image-20210327162635634](D:\vue\Node.js.assets\image-20210327162635634.png)

   3. Cookie

      ![image-20210327162719040](D:\vue\Node.js.assets\image-20210327162719040.png)

   4. Cookie在身份认证中的作用

      ![image-20210327162758774](D:\vue\Node.js.assets\image-20210327162758774.png)

   5. Cookie不具有安全性

      ![image-20210327162837480](D:\vue\Node.js.assets\image-20210327162837480.png)

   6. 提高身份认证的安全性

      ![image-20210327162904587](D:\vue\Node.js.assets\image-20210327162904587.png)

   7. session的工作原理

      ![image-20210327162929404](D:\vue\Node.js.assets\image-20210327162929404.png)

4. 在Express中使用Session认证

   1. 安装express-session中间件

      ```
      npm install express-session
      ```

   2. 配置express-session中间件

      ```js
      var session = require('express-session');
      app.use(session({
      	secret: 'keyboard cat',
      	resave: false,
      	saveUninitialized: true
      }))
      //session存数据
      app.post('/api/login', (req, res) => {
      	if(req.body.username !== 'admin' || req.body.password !== '000000'){
      	return res.send({status: 1, msg:'登陆失败'})
      	}
      	req.session.user = req.body;
      	req.session.islogin = true;
      	
      	res.send({ status: 0, msg:'登录成功'})
      })
      //session取数据
      app.get('/api/username', (req, res) => {
          if (!req.session.islogin) {
              return res.send({
                  status: 1,
                  msg: 'fail'
              });
          }
          res.send({
              status: 0,
              msg: 'success',
              username: req.session.user.username
          })
      })
      //清空session
      app.post('/api/logout', (req, res) => {
          req.session.destroy();
          res.send({
              status: 0,
              msg: '退出登录成功'
          })
      })
      ```

5. JWT身份认证

   1. Session认证的局限性

      Session认证机制需要配合Cookie才能实现。由于Cookie默认不支持跨域访问，所以当涉及到前端跨域请求后端接口时，需要做很多额外的配置，才能实现跨域Session认证。

      注意：

      + 当前端请求后端接口不存在跨域问题的时候，推荐使用Session身份认证机制。
      + 当前端需要跨域请求后端接口的时候，不推荐使用Session身份认证机制，推荐使用JWT认证机制。

   2. JWT工作原理

      JWT是目前最流行的跨域认证解决方案。

      ![image-20210328155554457](D:\vue\Node.js.assets\image-20210328155554457.png)

   3. JWT组成部分

      JWT通常由三部分组成，分别是header(头部)、Payload（有效荷载）、Signature（签名）。三者之间使用英文的“.”分隔

      ```js
      Header.Payload.Signature
      ```

      ![image-20210328184046881](D:\vue\Node.js.assets\image-20210328184046881.png)

   4. JWT的三个部分各自代表的含义

      ![image-20210328184135569](D:\vue\Node.js.assets\image-20210328184135569.png)

   5. JWT的使用方式

      客户端收到服务器返回的JWT之后，通常会将它存储在localStorage或sessionStorage中。

      此后，客户端每次与服务器通信，都要带上这个JWT字符串，从而进行身份认证。推荐的做法是把JWT放在HTTP请求头的Authorization字段中

      ```js
      Authorization: Bearer <token>
      ```

   6. 安装JWT相关的包

      ```
      npm install jsonwebtoken express-jwt
      ```

      + jsonwebtoken用于生成JWT字符串

      + express-jwt用于将JWT字符串解析还原成JSON对象

   7. 定义secret密钥

      ![image-20210328201150160](D:\vue\Node.js.assets\image-20210328201150160.png)

   8. 在登录成功后生成JWT字符串

      ![image-20210328201230612](D:\vue\Node.js.assets\image-20210328201230612.png)

   9. 将JWT字符串还原成JSON对象

      ![image-20210328201303932](D:\vue\Node.js.assets\image-20210328201303932.png)

   10. 捕获解析JWT失败后产生的错误

       ![image-20210328201502962](D:\vue\Node.js.assets\image-20210328201502962.png)