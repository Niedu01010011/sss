

## javascript

## 一、WebApi

1. ![image-20201116164050242](C:\Users\29635\AppData\Roaming\Typora\typora-user-images\image-20201116164050242.png)

2. document.querySelector()

   ![image-20201116164440653](C:\Users\29635\AppData\Roaming\Typora\typora-user-images\image-20201116164440653.png)

3. document.querySelectorAll()

   

   ![image-20201116164856522](C:\Users\29635\AppData\Roaming\Typora\typora-user-images\image-20201116164856522.png)

4. innerText和innerHTML的区别	![image-20201116180342693](C:\Users\29635\AppData\Roaming\Typora\typora-user-images\image-20201116180342693.png)



5. 定时器
   1. window.setTimeout(调用函数，[延迟的毫秒数])
      
      1. setTimeout()方法用于设置一个定时器，该定时器到期后执行调用函数。
      
   2. setInterval（调用函数，延迟毫秒数）

      1. 可以在设置定时器之前调用一次函数，防止刚开始刷新页面有空白问题。

      2. clearInterval（setInterval的名字）停止定时器



6. 节流阀
   1. 防止轮播图按钮连续点击造成播放过快。
   2. 节流阀的目的：当上一个函数动画内容执行完毕，再去执行下一个函数动画，让事件无法连续触发。
   3. 核心实现思路：利用回调函数，添加一个变量来控制，锁住函数和解锁函数。
      1. 开始设置一个变量 var flag = true；
      2. if （flag）{flag = false；do something}    关闭水龙头
      3. 利用回调函数动画执行完毕，flag = true     打开水龙头

7. 本地存储

   1. 数据存储在浏览器中，设置读取方便，甚至页面刷新不丢失数据。

   2. sessionStorage

      1. 生命周期为关闭浏览器窗口。

      2. 在同一窗口下数据可以共享。

      3. 以键值对形式存储使用。

      4. sessionStorage.setItem(key, value)  =>存储

         sessionStorage.getItem(key,)  =>获取

         sessionStorage.removeItem(key)  =>删除

         sessionStorage.clear()  =>清空

   3. localStorage

      1. 生命周期永久生效，除非手动删除，否则关闭页面也会存在。

      2. 可以多窗口（页面）共享（同意浏览器可以共享）。

      3. 以键值对的形式存储使用。

      4. localStorage.setItem(key, value)  =>存储

         localStorage.getItem(key,)  =>获取

         localStorage.removeItem(key)  =>删除

         localStorage.clear()  =>清空

## 二、面向对象编程

### 一、类和对象

 1. 创建类

     1. 语法：

        ```js
        //步骤1 使用class关键字
        class name {
          // class body
        }     
        //步骤2使用定义的类创建实例  注意new关键字
        var xx = new name(); 
        ```

    2. 示例：

       ```js
        // 1. 创建类 class  创建一个 明星类
        class Star {
          // 类的共有属性放到 constructor 里面
          constructor(name, age) {
          this.name = name;
          this.age = age;
          }
        }
          // 2. 利用类创建对象 new
          var ldh = new Star('刘德华', 18);
          console.log(ldh);
       ```

2. 类的继承：
   1. 继承中,如果实例化子类输出一个方法,先看子类有没有这个方法,如果有就先执行子类的。

   2. 继承中,如果子类里面没有,就去查找父类有没有这个方法,如果有,就执行父类的这个方法(就近原则)

   3. 如果子类想要继承父类的方法,同时在自己内部扩展自己的方法,利用super 调用父类的构造函数,super 必须在子类this之前调用。

      ```js
      // 父类有加法方法
       class Father {
         constructor(x, y) {
         this.x = x;
         this.y = y;
         }
         sum() {
         console.log(this.x + this.y);
         }
       }
       // 子类继承父类加法方法 同时 扩展减法方法
       class Son extends Father {
         constructor(x, y) {
         // 利用super 调用父类的构造函数 super 必须在子类this之前调用,放到this之后会报错
         super(x, y);
         this.x = x;
         this.y = y;
      
        }
        subtract() {
        console.log(this.x - this.y);
        }
      }
      var son = new Son(5, 3);
      son.subtract(); //2
      son.sum();//8
      ```
      
   4. 时刻注意this的指向问题，类里面的共有的属性和方法一定要加this使用。

      1. constructor中的this指向的是new出来的实例对象。
      2. 自定义的方法，一般也指向的new出来的实例对象。
      3. 绑定事件之后this指向的就是触发事件的事件源。
      
   5. 在es6中类没有变量提升，所以必须先定义类，才能通过类实例化对象。

### 二、构造函数和原型

1. 构造函数是一种特殊的函数，主要用来初始化对象，即为对象成员变量赋初始值，它总与new一起使用。我们可以把对象中一些公共的属性和方法抽取出来，封装到这个函数里面。

2. new在执行的时候会做四件事情：
   1. 在内存中创建一个新的空对象。
   2. 让this指向这个新的对象。
   3. 执行构造函数里面的代码，给这个新对象添加属性和方法。
   4. 返回这个新对象（所以构造函数里不需要return）。 

3. 构造函数原型prototype

   1. 构造函数通过原型分配的函数是所有对象所共享的。
   2. js规定，每个构造函数都有一个prototype属性，指向另一个对象。注意这个prototype就是一个对象，这个对象的所有属性和方法，都会被构造函数所拥有。
   3. 公共的方法直接定义在prototype对象上，这样所有对象的实例就可以共享这些方法；公共属性定义到构造函数里面。

4. 对象原型__ proto__ ：对象都会有一个属性  __ proto__ 指向构造函数的prototype原型对象。

   1.  __ proto__ 对象原型和原型对象prototype是等价的。

   2. 此实际开发中，不可以使用这个属性，它只是内部指向原型对象 prototype。

   ##### 3. 原型链

   1. 原型链和成员的查找机制：

      任何对象都有原型对象，也就是prototype属性，任何原型对象也是一个对象，该对象就有 __ proto __ 属性，这样一层一层往上找，就形成了一条链，我们成为原型链。

      当访问一个对象的属性（包括方法）时，首先查找这个对象自身有没有该属性。
      如果没有就查找它的原型（也就是 __proto__指向的 prototype 原型对象）。
      如果还没有就查找原型对象的原型（Object的原型对象）。
      依此类推一直找到 Object 为止（null）。
      __proto__对象原型的意义就在于为对象成员查找机制提供一个方向，或者说一条路线。
   
   2. 原型对象中的this指向
   
      构造函数中的this和原型对象的this，都指向我们new出来的实例对象。

      ```js
      function Star(uname, age) {
          this.uname = uname;
          this.age = age;
      }
      var that;
      Star.prototype.sing = function() {
          console.log('我会唱歌');
          that = this;
      }
      var ldh = new Star('刘德华', 18);
      // 1. 在构造函数中,里面this指向的是对象实例 ldh
      console.log(that === ldh);//true
      // 2.原型对象函数里面的this 指向的是 实例对象 ldh
      ```
   
   3. 通过原型为数组扩展内置方法
   
      ```js
       Array.prototype.sum = function() {
         var sum = 0;
         for (var i = 0; i < this.length; i++) {
         sum += this[i];
         }
         return sum;
       };
       //此时数组对象中已经存在sum()方法了  可以始终 数组.sum()进行数据的求和。
      ```

### 三、继承

1. call（）

   1. call() 可以调用函数

   2. call() 可以修改this的指向，使用call（）的时候 参数一是修改后的this指向，参数2，参数3...使用逗号隔开连接。

      ```js
       function fn(x, y) {
           console.log(this);
           console.log(x + y);
      }
        var o = {
        	name: 'andy'
        };
        fn.call(o, 1, 2);//调用了函数此时的this指向了对象o,
      ```

2. 子构造函数继承父构造函数中的属性

   1. 先定义一个父构造函数。

   2. 在定义一个子构造函数。

   3. 子构造函数继承父构造函数的属性（使用call方法）。

      ```js
       // 1. 父构造函数
       function Father(uname, age) {
         // this 指向父构造函数的对象实例
         this.uname = uname;
         this.age = age;
       }
        // 2 .子构造函数 
      function Son(uname, age, score) {
        // this 指向子构造函数的对象实例
        // 3.使用call方式实现子继承父的属性
        Father.call(this, uname, age);
        this.score = score;
      }
      var son = new Son('刘德华', 18, 100);
      console.log(son);
      ```

      ![image-20210103153126153](javascript.assets\image-20210103153126153.png)

3. 借用原型对象继承方法	

   ```js
   // 1. 父构造函数
   function Father(uname, age) {
     // this 指向父构造函数的对象实例
     this.uname = uname;
     this.age = age;
   }
   Father.prototype.money = function() {
     console.log(100000);
    };
    // 2 .子构造函数 
     function Son(uname, age, score) {
         // this 指向子构造函数的对象实例
         Father.call(this, uname, age);
         this.score = score;
     }
   // Son.prototype = Father.prototype;  这样直接赋值会有问题,如果修改了子原型对象,父原型对象也会跟着一起变化
     Son.prototype = new Father();
     // 如果利用对象的形式修改了原型对象,别忘了利用constructor 指回原来的构造函数
     Son.prototype.constructor = Son;
     // 这个是子构造函数专门的方法
     Son.prototype.exam = function() {
       console.log('孩子要考试');
   
     }
     var son = new Son('刘德华', 18, 100);
     console.log(son);
   ```

   代码运行结果：

   ![image-20210103153547794](javascript.assets\image-20210103153547794.png)

### 四、ES5新增方法

1. 数组方法forEach遍历数组

   ```js
    arr.forEach(function(value, index, array) {
          //参数一是:数组元素
          //参数二是:数组元素的索引
          //参数三是:当前的数组
    })
     //相当于数组遍历的 for循环 没有返回值
   ```

2. 数组方法filter过滤数组

   ```js
     var arr = [12, 66, 4, 88, 3, 7];
     var newArr = arr.filter(function(value, index,array) {
     	 //参数一是:数组元素
        //参数二是:数组元素的索引
        //参数三是:当前的数组
        return value >= 20;
     });
     console.log(newArr);//[66,88] //返回值是一个新数组
   ```

3. 数组方法some

   ```js
   var arr = [10, 30, 4];
    var flag = arr.some(function(value,index,array) {
       //参数一是:数组元素
        //参数二是:数组元素的索引
        //参数三是:当前的数组
        return value < 3;
     });
   console.log(flag);//false返回值是布尔值,只要查找到满足条件的一个元素就立马终止循环
   ```

4. 数组方法map 映射 一个对一个

   数组方法reduce 汇总 一堆出来一个

   ```js
   //map
   let arr = [12, 5, 8]
   let result = arr.map(function (item) {
       return item*2
   })
   let result2 = arr.map(item=>item*2) // 简写
   console.log(result)
   console.log(result2)
   
   let score = [18, 86, 88, 24]
   let result3 = score.map(item => item >= 60 ? '及格' : '不及格')
   console.log(result3)
   
   // 结果
   [ 24, 10, 16 ]
   [ 24, 10, 16 ]
   [ '不及格', '及格', '及格', '不及格' ]
   //-----------------------------------------------------------------
   //reduce
   
   ```

5. 筛选商品案例
   1. 定义数组对象数据

   ```js
   var data = [{
   			id: 1,
   			pname: '小米',
   			price: 3699
   		}, {
   			 id: 2,
               pname: 'oppo',
               price: 999
           }, {
               id: 3,
               pname: '荣耀',
               price: 1299
           }, {
               id: 4,
               pname: '华为',
               price: 1999
   			}, ];
   ```

   1. 使用forEach便利数据并渲染到页面中

   ```js
   data.forEach(function(value){
   	var tr = document.createElement('tr');
   	tr.innerHTML = '<td>' + value.id + '</td><td>' + value.pname + '</td><td>' + value.price + '</td>';
     tbody.appendChild(tr);
   });
   ```

   1. 根据价格筛选数据

   2. 获取到搜索按钮并为其绑定点击事件

   3. 使用filter将用户输入的价格信息筛选出来

      ```js
      search_price.addEventListener('click', function(){
      	var newData = data.filter(function(value){
      	//start.value是开始区间
      	//end.value是结束区间
      	return value.price >= start.value && value.price <= end.price;
      	});
      	console.log(newData);
      })
      ```

   4. 将筛选出来的数据重新渲染到表格中

      1. 将渲染数据的逻辑封装到一个函数中

         ```js
         function setData(mydata){
         	//先清空原来tbody里面的数据
         	tbody.innerHTML = '';
         	mydata.forEach(function(value){
         	var tr = document.createElement('tr');
         	tr.innerHTML = '<td>' + value.id + '</td><td>' + value.pname + '</td><td>' + value.price + '</td>';
               tbody.appendChild(tr);
         	});
         }
         ```

      2. 将筛选之后的数据重新渲染

         ```js
          search_price.addEventListener('click', function() {
              var newDate = data.filter(function(value) {
              return value.price >= start.value && value.price <= end.value;
              });
              console.log(newDate);
              // 把筛选完之后的对象渲染到页面中
              setDate(newDate);
         });
         ```

   5. 根据商品名称筛选

      1. 获取用户输入的商品名称

      2. 为查询按钮绑定点击事件,将输入的商品名称与这个数据进行筛选

         ```js
          search_pro.addEventListener('click', function() {
              var arr = [];
              data.some(function(value) {
                if (value.pname === product.value) {
                  // console.log(value);
                  arr.push(value);
                  return true; // return 后面必须写true  
                }
              });
              // 把拿到的数据渲染到页面中
              setDate(arr);
         })
         ```

6. 获取对象的属性名

   Object.keys(对象) 获取到当前对象中的属性名 ，返回值是一个数组

   ```js
    var obj = {
        id: 1,
        pname: '小米',
        price: 1999,
        num: 2000
   };
   var result = Object.keys(obj)
   console.log(result)//[id，pname,price,num]
   ```

7. Object.defineProperty

   Object.defineProperty设置或修改对象中的属性

   ```js
   Object.defineProperty(对象，修改或新增的属性名，{
   		value:修改或新增的属性的值,
   		writable:true/false,//如果值为false 不允许修改这个属性值
   		enumerable: false,//enumerable 如果值为false 则不允许遍历
           configurable: false  //configurable 如果为false 则不允许删除这个属性 属性是否可以被删除或是否可以再次修改特性
   })	
   ```

### 五、函数的定义和调用

1. 函数定义的方式
   1. 方式一：函数声明方式 function 关键字（命名函数）

   ```js
   function fn(){}
   ```
   2. 方式二：函数表达式（匿名函数）

   ```js
   var fn = function(){}
   ```

   3. 方式三：new Function()

   ```js
   var f = new Function('a', 'b', 'console.log(a + b)');
   f(1, 2);
   
   var fn = new Function('参数1','参数2'..., '函数体')
   注意
   /*Function 里面参数都必须是字符串格式
   第三种方式执行效率低，也不方便书写，因此较少使用
   所有函数都是 Function 的实例(对象)  
   函数也属于对象
   */
   ```

2. 函数的调用
   ```js
   /* 1. 普通函数 */
   function fn() {
   	console.log('人生的巅峰');
   }
    fn(); 
   /* 2. 对象的方法 */
   var o = {
     sayHi: function() {
     	console.log('人生的巅峰');
     }
   }
   o.sayHi();
   /* 3. 构造函数*/
   function Star() {};
   new Star();
   /* 4. 绑定事件函数*/
    btn.onclick = function() {};   // 点击了按钮就可以调用这个函数
   /* 5. 定时器函数*/
   setInterval(function() {}, 1000);  这个函数是定时器自动1秒钟调用一次
   /* 6. 立即执行函数(自调用函数)*/
   (function() {
   	console.log('人生的巅峰');
   })();
   ```

3. this

   1. 函数内部的this指向

      ![image-20210103213731331](javascript.assets\image-20210103213731331.png)

   2. 改变函数内部this指向

      1. call()

         call()方法调用一个对象，简单理解为调用函数的方式，但是它可以改变函数的this指向

         应用场景：经常在继承中使用

         ```js
         var o = {
         	name: 'andy'
         }
          function fn(a, b) {
               console.log(this);
               console.log(a+b)
         };
         fn(1,2)// 此时的this指向的是window 运行结果为3
         fn.call(o,1,2)//此时的this指向的是对象o,参数使用逗号隔开,运行结果为3
         ```

      2. apply()

         apply() 方法调用一个函数。简单理解为调用函数的方式，但是它可以改变函数的 this 指向。

         应用场景:  经常跟数组有关系

         ```js
         var o = {
         	name: 'andy'
         }
          function fn(a, b) {
               console.log(this);
               console.log(a+b)
         };
         fn()// 此时的this指向的是window 运行结果为3
         fn.apply(o,[1,2])//此时的this指向的是对象o,参数使用数组传递 运行结果为3
         ```

      3. bind()

         bind() 方法不会调用函数,但是能改变函数内部this 指向,返回的是原函数改变this之后产生的新函数

         如果只是想改变 this 指向，并且不想调用这个函数的时候，可以使用bind

         应用场景:不调用函数,但是还想改变this指向

         ```js
          var o = {
          name: 'andy'
          };
         
         function fn(a, b) {
         	console.log(this);
         	console.log(a + b);
         };
         var f = fn.bind(o, 1, 2); //此处的f是bind返回的新函数
         f();//调用新函数  this指向的是对象o 参数使用逗号隔开
         ```

4. call()、apply()、bind()三者异同

   1. 共同点 : 都可以改变this指向
   2. 不同点:
      - call 和 apply  会调用函数, 并且改变函数内部this指向.
      - call 和 apply传递的参数不一样,call传递参数使用逗号隔开,apply使用数组传递
      - bind  不会调用函数, 可以改变函数内部this指向.
      
   3. 应用场景

   ​		1. call 经常用做继承. 

   ​		2. apply经常跟数组有关系.  比如借助于数学对象实现数组最大值最小值

   ​		3. bind  不调用函数,但是还想改变this指向. 比如改变定时器内部的this指向.

### 六、严格模式

1. 开启严格模式

   1. 为脚本开启严格模式

      1. 有的script脚本是严格模式，有的script脚本是正常模式，这样不利于文件合并，所以可以将整个脚本文件放在一个立即执行的匿名函数之中。这样独立创建一个作用域而不影响其他script脚本。

         ```js
         (function (){
           //在当前的这个自调用函数中有开启严格模式，当前函数之外还是普通模式
         　　　　"use strict";
                var num = 10;
         　　　　function fn() {}
         })();
         //或者 
         <script>
           　"use strict"; //当前script标签开启了严格模式
         </script>
         <script>
           			//当前script标签未开启严格模式
         </script>
         ```

      2. 为函数开启严格模式

         1. 要给某个函数开启严格模式，需要把“use strict”；声明放在函数体所有语句之前。

            ```js
            function fn(){
            	"use strict";
            	return "123"
            }//当前fn函数开启了严格模式
            ```

   2. 严格模式中的变化

      ```js
      'use strict'
      num = 10 
      console.log(num)//严格模式后使用未声明的变量
      --------------------------------------------------------------------------------
      var num2 = 1;
      delete num2;//严格模式不允许删除变量
      --------------------------------------------------------------------------------
      function fn() {
       console.log(this); // 严格模式下全局作用域中函数中的 this 是 undefined
      }
      fn();  
      ---------------------------------------------------------------------------------
      function Star() {
      	 this.sex = '男';
      }
      // Star();严格模式下,如果 构造函数不加new调用, this 指向的是undefined 如果给他赋值则 会报错.
      var ldh = new Star();
      console.log(ldh.sex);
      ----------------------------------------------------------------------------------
      setTimeout(function() {
        console.log(this); //严格模式下，定时器 this 还是指向 window
      }, 2000);  
      ```

      https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Strict_mode

### 七、高阶函数

​	高阶函数是对其他函数进行操作的函数，它接收函数作为参数或将函数作为返回值输出。

​	函数也是一种数据类型，同样可以作为参数，传递给另外一个参数使用。最典型的就是作为回调函数。

### 八、闭包

1. 变量的作用域

   分为全局变量和局部变量

   1. 函数内部可以使用全局变量。
   2. 函数外部不可以使用局部变量。
   3. 当函数执行完毕，本作用域内的局部变量会销毁。

2. 什么是闭包

   1. 闭包指有权访问另一个函数作用域中的变量的函数。简单理解就是，一个作用域可以访问另外一个函数内部的局部变量。

      ```js
      function fn1(){  //fn1就是闭包函数
      	var num = 10;
      	function fn2(){
      		console.log(num);//10
      	}
      	fn2();
      }
      fn1();
      ```

   2. 闭包的作用

      延伸变量的作用范围。

      ```js
      function fn(){
      	var num = 10;
      	function fun(){
      		console.log(num);
      	}
      	return fun;
      }
      var f = fn();
      f();
      ```

3. 案例

   1. 利用闭包得到当前li的索引号

      ```js
      for (var i = 0; i < lis.length; i++) {
      // 利用for循环创建了4个立即执行函数
      // 立即执行函数也成为小闭包因为立即执行函数里面的任何一个函数都可以使用它的i这变量
      	(function(i) {    
      		lis[i].onclick = function() {      
      			console.log(i);    
      		} 
          })(i);
      }
      ```

   2. 闭包应用3秒钟之后，打印所有li元素的内容

      ```js
      for(var i = 0; i < lis.length; i++){
      	(function(i){
      		setTimeout(function(){
      		console.log(lis[i].innerHTML);
      		}, 3000)
      	})(i);
      }
      ```

   3. 闭包应用-计算打车价格

      ```js
      /*需求分析
      打车起步价13(3公里内),  之后每多一公里增加 5块钱.  用户输入公里数就可以计算打车价格
      如果有拥堵情况,总价格多收取10块钱拥堵费*/
      
       var car = (function() {
           var start = 13; // 起步价  局部变量
           var total = 0; // 总价  局部变量
           return {
             // 正常的总价
             price: function(n) {
               if (n <= 3) {
                 total = start;
               } else {
                 total = start + (n - 3) * 5
               }
               return total;
             },
             // 拥堵之后的费用
             yd: function(flag) {
               return flag ? total + 10 : total;
             }
      	}
       })();
      console.log(car.price(5)); // 23
      console.log(car.yd(true)); // 33
      ```

   4. ```js
       var name = "The Window";
         var object = {
           name: "My Object",
           getNameFunc: function() {
           return function() {
           return this.name;
           };
         }
       };
      console.log(object.getNameFunc()())
      -----------------------------------------------------------------------------------
      var name = "The Window";　　
        var object = {　　　　
          name: "My Object",
          getNameFunc: function() {
          var that = this;
          return function() {
          return that.name;
          };
        }
      };
      console.log(object.getNameFunc()())
      ```

### 九、浅拷贝和深拷贝

1. 浅拷贝知识拷贝一层，更深层次对象级别的只拷贝引用。

   深拷贝拷贝多层，每一级别的数据都会拷贝。

### 十、正则表达式

1. 正则表达式的创建

   1. 通过调用RegExp对象的构造函数创建

      ```js
      var regexp = new RegExp(/123/);//只能输入123
      console.log(regexp);
      ```

   2. 利用字面量创建 正则表达式

      ```js
      var rg = /123/;
      ```

2. 测试正则表达式

   1. test（）正则对象方法，用于检测字符串是否符合该规则，该对象会返回true或false，其参数是测试字符串。

      ```js
      var rg = /123/;
      console.log(rg.test(123));//匹配字符中是否出现123 出现结果为true
      console.log(rg.test('abc'));//匹配字符中是否出现123 未出现结果为false
      ```

3. 正则表达式中的特殊字符

   1. 正则表达式的组成

      一个正则表达式可以由简单的字符构成，比如 /abc/，也可以是简单和特殊字符的组合，比如 /ab*c/ 。其中特殊字符也被称为元字符，在正则表达式中是具有特殊意义的专用符号，如 ^ 、$ 、+ 等。

      特殊字符非常多，可以参考： 

      [MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions)

   2. 边界符

      | 边界符 | 说明                           |
      | ------ | ------------------------------ |
      | ^      | 表示匹配行首的文本（以谁开始） |
      | $      | 表示匹配行尾的文本（以谁结束） |

      如果^和$在一起，标事必须是精确匹配。

      ```js
      var rg = /abc/; // 正则表达式里面不需要加引号 不管是数字型还是字符串型
      // /abc/ 只要包含有abc这个字符串返回的都是true
      console.log(rg.test('abc'));
      console.log(rg.test('abcd'));
      console.log(rg.test('aabcd'));
      console.log('---------------------------');
      var reg = /^abc/;
      console.log(reg.test('abc')); // true
      console.log(reg.test('abcd')); // true
      console.log(reg.test('aabcd')); // false
      console.log('---------------------------');
      var reg1 = /^abc$/; // 精确匹配 要求必须是 abc字符串才符合规范
      console.log(reg1.test('abc')); // true
      console.log(reg1.test('abcd')); // false
      console.log(reg1.test('aabcd')); // false
      console.log(reg1.test('abcabc')); // false
      ```

   3. 字符类

      字符类表示有一系列字符可供选择，只要匹配其中一个就可以了。所有可供选择的字符都放在方括号内。

      1. []方括号

         ```js
         var rg = /[abc]/; // 只要包含有a 或者 包含有b 或者包含有c 都返回为true
         console.log(rg.test('andy'));//true
         console.log(rg.test('baby'));//true
         console.log(rg.test('color'));//true
         console.log(rg.test('red'));//false
         var rg1 = /^[abc]$/; // 三选一 只有是a 或者是 b  或者是c 这三个字母才返回 true
         console.log(rg1.test('aa'));//false
         console.log(rg1.test('a'));//true
         console.log(rg1.test('b'));//true
         console.log(rg1.test('c'));//true
         console.log(rg1.test('abc'));//true
         ----------------------------------------------------------------------------------
         var reg = /^[a-z]$/ //26个英文字母任何一个字母返回 true  - 表示的是a 到z 的范围  
         console.log(reg.test('a'));//true
         console.log(reg.test('z'));//true
         console.log(reg.test('A'));//false
         -----------------------------------------------------------------------------------
         //字符组合
         var reg1 = /^[a-zA-Z0-9]$/; // 26个英文字母(大写和小写都可以)任何一个字母返回 true  
         ------------------------------------------------------------------------------------
         //取反 方括号内部加上 ^ 表示取反，只要包含方括号内的字符，都返回 false 。
         var reg2 = /^[^a-zA-Z0-9]$/;
         console.log(reg2.test('a'));//false
         console.log(reg2.test('B'));//false
         console.log(reg2.test(8));//false
         console.log(reg2.test('!'));//true
         ```

      2. 量词符

         | 量词  |      说明       |
         | :---: | :-------------: |
         |   *   | 重复0次或更多次 |
         |   +   | 重复1次或更多次 |
         |   ?   |  重复0次或1次   |
         |  {n}  |     重复n次     |
         | {n,}  | 重复n次或更多次 |
         | {n,m} |   重复n到m次    |
         注意：{n,m}中间不得有空格。

      3. 用户名表单验证

         功能需求：

         1. 如果用户名输入合法, 则后面提示信息为:  用户名合法,并且颜色为绿色

         2. 如果用户名输入不合法, 则后面提示信息为:  用户名不符合规范, 并且颜色为红色

            ```js
            <input type="text" class="uname"> <span>请输入用户名</span>
             <script>
             //  量词是设定某个模式出现的次数
             var reg = /^[a-zA-Z0-9_-]{6,16}$/; // 这个模式用户只能输入英文字母 数字 下划线 中划线
             var uname = document.querySelector('.uname');
             var span = document.querySelector('span');
             uname.onblur = function() {
               if (reg.test(this.value)) {
               console.log('正确的');
               span.className = 'right';
               span.innerHTML = '用户名格式输入正确';
               } else {
               console.log('错误的');
               span.className = 'wrong';
               span.innerHTML = '用户名格式输入不正确';
               }
             }
            </script>
            ```

      4. 括号总结

         1.大括号  量词符.  里面表示重复次数

         2.中括号 字符集合。匹配方括号中的任意字符. 

         3.小括号表示优先级

      5. 预定义类

         ![image-20210112160922200](javascript.assets\image-20210112160922200.png)

      6. 手机号码案例

         ```js
          //手机号验证:/^1[3|4|5|7|8][0-9]{9}$/;
         //验证通过与不通过更换元素的类名与元素中的内容 
          if (reg.test(this.value)) {
             // console.log('正确的');
             this.nextElementSibling.className = 'success';
             this.nextElementSibling.innerHTML = '<i class="success_icon"></i> 恭喜您输入正确';
            } else {
                // console.log('不正确');
               this.nextElementSibling.className = 'error';
               this.nextElementSibling.innerHTML = '<i class="error_icon"></i>格式不正确,请从新输入 ';
          }
         ```

      7. 正则替换replace

         1. replace（）方法可以实现替换字符串操作，用来替换的参数可以是一个字符串或是一个正则表达式。

         2. 案例 过滤敏感词

            ```js
            <textarea name="" id="message"></textarea> <button>提交</button>
            <div></div>
            <script>
                var text = document.querySelector('textarea');
                var btn = document.querySelector('button');
                var div = document.querySelector('div');
                btn.onclick = function() {
                	div.innerHTML = text.value.replace(/激情|gay/g, '**');
                }
            </script>
            ```

### 十一、es6

1. let

   1. let声明的变量只在所处于的块级有效

      ```js
      if(true) {
      let a = 10;
      }
      console.log(a); // a is not defined
      ```

      **注意：**使用let关键字声明的变量才具有块级作用域，使用var声明的变量不具备块级作用域特性。

   2. 不存在变量提升

      ```js
      console.log(a); // a is not defined 
      let a = 20;
      ```

   3. 暂时性死区

      利用let声明的变量会绑定在这个块级作用域，不会受外界的影响

      ```js
      var tmp = 123；
      if (true) {
      	tmp = 'abc';
      	let tmp;
      }
      ```

      #### 经典面试题

      ```javascript
       var arr = [];
       for (var i = 0; i < 2; i++) {
           arr[i] = function () {
               console.log(i); 
           }
       }
       arr[0]();
       arr[1]();
      
      ```

      ![](javascript.assets\let面试题.png)

      **经典面试题图解：**此题的关键点在于变量i是全局的，函数执行时输出的都是全局作用域下的i值。

      ```javascript
       let arr = [];
       for (let i = 0; i < 2; i++) {
           arr[i] = function () {
               console.log(i); 
           }
       }
       arr[0]();
       arr[1]();
      
      ```

      ![](javascript.assets\let面试题2.png)

      **经典面试题图解：**此题的关键点在于每次循环都会产生一个块级作用域，每个块级作用域中的变量都是不同的，函数执行时输出的是自己上一级（循环产生的块级作用域）作用域下的i值.

      #### 小结

      - let关键字就是用来声明变量的
      - 使用let关键字声明的变量具有块级作用域
      - 在一个大括号中 使用let关键字声明的变量才具有块级作用域 var关键字是不具备这个特点的
      - 防止循环变量变成全局变量
      - 使用let关键字声明的变量没有变量提升
      - 使用let关键字声明的变量具有暂时性死区特性

2. const

   1. 具有块级作用域

      ```js
       if (true) { 
           const a = 10;
       }
      console.log(a) // a is not defined
      ```

   2. 声明常量时必须赋值

      ```js
      const PI; //Missing initializer in const declaration
      ```

      ```js
      const PI = 3.14;
      ```

   3. 常量赋值后值不能修改（如果是基本数据类型，不能更改值，如果是复杂数据类型，不能更改地址值。）

      ```js
      const PI = 3.14;
      PI = 100;//Assignment to constant variable.
      
      const ary[100, 200];
      ary[0] = 'a';
      ary[1] = 'b';
      console.log(ary);//['a', 'b']
      ary = ['a', 'b']; //Assignment to constant variable;
      ```

   #### 小结

   - const声明的变量是一个常量
   - 既然是常量不能重新进行赋值，如果是基本数据类型，不能更改值，如果是复杂数据类型，不能更改地址值
   - 声明 const时候必须要给定值

   ### let、const、var 的区别

   - 使用 var 声明的变量，其作用域为该语句所在的函数内，且存在变量提升现象
   - 使用 let 声明的变量，其作用域为该语句所在的代码块内，不存在变量提升
   - 使用 const 声明的是常量，在后面出现的代码中不能再修改该常量的值

   ![](javascript.assets\var&let&const区别.png)

3. 解构赋值

   1. 数组解构

      ```js
      let [a, b, c, d] = [1, 2, 3];
      console.log(a);//1
      console.log(b);//2
      console.log(c);//3
      console.log(d);//undefined
      ```

   2. 对象解构

      ```js
       let person = { name: 'zhangsan', age: 20 }; 
       let { name, age } = person;
       console.log(name); // 'zhangsan' 
       console.log(age); // 20
      
       let {name: myName, age: myAge} = person; // myName myAge 属于别名
       console.log(myName); // 'zhangsan' 
       console.log(myAge); // 20
      ```

      #### 小结

      - 解构赋值就是把数据结构分解，然后给变量进行赋值
      - 如果结构不成功，变量跟数值个数不匹配的时候，变量的值为undefined
      - 数组解构用中括号包裹，多个变量用逗号隔开，对象解构用花括号包裹，多个变量用逗号隔开
      - 利用解构赋值能够让我们方便的去取对象中的属性跟方法
      - 左右两边的结构必须一样，右边必须是个东西（合法）
      - 声明和赋值不能分开

4. 箭头函数

   1. es6中新增的定义函数的方式

      ```js
      () => {} //()：代表是函数； =>：必须要的符号，指向哪一个代码块；{}：函数体
      const fn = () => {}//代表把一个函数赋值给fn
      ```

   2. 函数体中只有一句代码，且代码的执行结果就是返回值，可以省略大括号；

   3. 如果形参只有一个，可以省略小括号

      ```js
       function sum(num1, num2) { 
           return num1 + num2; 
       }
       //es6写法
       const sum = (num1, num2) => num1 + num2; 
       
       
        function fn (v) {
           return v;
       } 
      //es6写法
       const fn = v => v;
      ```

   4. 箭头函数不绑定this关键字，箭头函数中的this，指向的是函数定义位置的上下文this

      ```javascript
      const obj = { name: '张三'} 
       function fn () { 
           console.log(this);//this 指向 是obj对象
           return () => { 
               console.log(this);//this 指向 的是箭头函数定义的位置，那么这个箭头函数定义在fn里面，而这个fn指向是的obj对象，所以这个this也指向是obj对象
           } 
       } 
       const resFn = fn.call(obj); 
       resFn();
      
      ```

      #### 小结

      - 箭头函数中不绑定this，箭头函数中的this指向是它所定义的位置，可以简单理解成，定义箭头函数中的作用域的this指向谁，它就指向谁
      - 箭头函数的优点在于解决了this执行环境所造成的一些问题。比如：解决了匿名函数this指向的问题（匿名函数的执行环境具有全局性），包括setTimeout和setInterval中使用this所造成的问题

      #### 面试题

      ```javascript
      var age = 100;
      
      var obj = {
      	age: 20,
      	say: () => {
      		alert(this.age)
      	}
      }
      
      obj.say();//箭头函数this指向的是被声明的作用域里面，而对象没有作用域的，所以箭头函数虽然在对象中被定义，但是this指向的是全局作用域
      ```

      ### 剩余参数

      剩余参数语法允许我们将一个不定数量的参数表示为一个数组，不定参数定义方式，这种方式很方便的去声明不知道参数情况下的一个函数

      ```javascript
      function sum (first, ...args) {
           console.log(first); // 10
           console.log(args); // [20, 30] 
       }
       sum(10, 20, 30)
      //rest parameter（剩余参数）必须是最后一个形参
      ```

      #### 剩余参数和解构配合使用

      ```javascript
      let students = ['wangwu', 'zhangsan', 'lisi'];
      let [s1, ...s2] = students; 
      console.log(s1);  // 'wangwu' 
      console.log(s2);  // ['zhangsan', 'lisi']
      
      ```

5. **es6的内置对象扩展**

   1. Array的扩展方法

      + 扩展运算符可以将数组或者对象转为用逗号分隔的参数序列

      ```javascript
       let ary = [1, 2, 3];
       ...ary  // 1, 2, 3
       console.log(...ary);    // 1 2 3,相当于下面的代码
       console.log(1,2,3);
      ```

      + 扩展运算符可以应用于合并数组

      ```js
      //方法一
      let ary1 = [1, 2, 3];
      let ary2 = [3, 4, 5];
      let ary3 = [...ary1, ...ary2];
      //方法二
      ary1.push(...ary2);
      ```

      + 将类数组或可遍历对象转化为真正的数组

      ```js
      let oDivs = document.getElementsByTagName('div');
      oDivs = [...oDivs];
      ```

      + 构造函数方法：Array.from()

        将伪数组或可遍历对象转换为真正的数组

      ```js
      //定义一个集合
      let arrayLike = {
      	'0': 'a',
      	'1': 'b',
      	'2': 'c',
      	length: 3
      };
      //转换成数组
      let arr2 = Array.from(arrayLike);//['a', 'b', 'c']
      ```

      ​		该方法还可以接受第二个参数，作用类似于数组的map方法，用来对每个元素进行处理，将处理后的值放入返回的数组。

      ```js
      let arrayLike = {
      	"0": 1,
      	"1": 2,
      	"length": 2
      }
      let newAry = Array.from(arrayLike,item =>item *2)//[2, 4]
      ```

      ​		如果是对象，那么属性需要写对应的索引

      + 实例方法： find()

        用于找出第一个符合条件的数组成员，如果没有找到返回undefined

      ```js
      let ary = [{
           id: 1,
           name: '张三'
       }, { 
           id: 2,
           name: '李四'
       }]; 
       let target = ary.find((item, index) => item.id == 2);//找数组里面符合条件的值，当数组中元素id等于2的查找出来，注意，只会匹配第一个
      
      ```

      + 实例方法：includes()

        判断某个数组是否包含给定的值，返回布尔值。

      ```javascript
      [1, 2, 3].includes(2) // true 
      [1, 2, 3].includes(4) // false
      ```

   2. String 的扩展方法

      + 模板字符串：

        ES6新增的创建字符串的方式，使用反引号定义

      ```js
      let name = `zhangsan`;
      ```

      ​		模板字符串中可以解析变量

      ```js
          let name = '张三'; 
          let sayHello = `hello,my name is ${name}`; // hello, my name is zhangsan
      ```

      ​		模板字符串中可以换行

      ```js
       let result = { 
           name: 'zhangsan', 
           age: 20,
           sex: '男' 
       } 
       let html = ` <div>
           <span>${result.name}</span>
           <span>${result.age}</span>
           <span>${result.sex}</span>
       </div> `;
      ```

      ​		在模板字符串中可以调用函数

   ```javascript
   const sayHello = function () { 
       return '哈哈哈哈 追不到我吧 我就是这么强大';
    }; 
    let greet = `${sayHello()} 哈哈哈哈`;
    console.log(greet); // 哈哈哈哈 追不到我吧 我就是这么强大 哈哈哈哈
   
   ```

   实例方法：startsWith() 和 endsWith()

   startsWith()：表示参数字符串是否在原字符串的头部，返回布尔值

   endsWith()：表示参数字符串是否在原字符串的尾部，返回布尔值

   ```javascript
   let str = 'Hello world!';
   str.startsWith('Hello') // true 
   str.endsWith('!')       // true
   
   ```

   ​	实例方法：repeat()

   ​	repeat方法表示将原字符串重复n次，返回一个新字符串

   ```javascript
   'x'.repeat(3)      // "xxx" 
   'hello'.repeat(2)  // "hellohello"
   ```

6. **Set 数据结构**

   ES6 提供了新的数据结构  Set。它类似于数组，但是成员的值都是唯一的，没有重复的值。

   Set本身是一个构造函数，用来生成  Set  数据结构			

   ```javascript
   const s = new Set();
   ```

   ​	Set函数可以接受一个数组作为参数，用来初始化。

   ```javascript
   const set = new Set([1, 2, 3, 4, 4]);//{1, 2, 3, 4}实例方法
   ```

   + add(value)：添加某个值，返回 Set 结构本身

   + delete(value)：删除某个值，返回一个布尔值，表示删除是否成功

   + has(value)：返回一个布尔值，表示该值是否为 Set 的成员

   + clear()：清除所有成员，没有返回值

     ```js
     const s = new Set();
     s.add(1).add(2).add(3); // 向 set 结构中添加值 
     s.delete(2)             // 删除 set 结构中的2值   
     s.has(1)                // 表示 set 结构中是否有1这个值 返回布尔值 
     s.clear()               // 清除 set 结构中的所有值
     //注意：删除的是元素的值，不是代表的索引
     ```

   + 遍历Set 结构的实例与数组一样，也拥有forEach方法，用于对每个成员执行某种操作，没有返回值。

     ```js
     s.foreach(value=>console.log(value))
     ```

   + 去除数组重复成员的方法

     ```js
     [...new Set(array)]//剩余参数将set数据结构转换为数组
     ```

     

1. **map数据结构**
   
   1. 

## 三、js补充

1. 堆栈底层机制

   ![image-20210424155849413](javascript.assets\image-20210424155849413.png)

   **面试题**

   ![image-20210424163645490](javascript.assets\image-20210424163645490.png)

