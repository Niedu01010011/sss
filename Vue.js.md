# Vue

## 1. Vue基本使用

### 1.vue的基本使用步骤

1. 需要提供标签用于填充数据。

2. 引入vue.js库文件

3. 使用vue的语法做功能

4. 把vue提供的数据填充到标签里面

   ![image-20210406122909842](C:\Users\29635\AppData\Roaming\Typora\typora-user-images\image-20210406122909842.png)

   ![image-20210406123029264](C:\Users\29635\AppData\Roaming\Typora\typora-user-images\image-20210406123029264.png)

### 2. 指令

​	指令的本质就是自定义属性

​	指令的格式：以v-开始（比如v-cloak）

1. v-cloak

   + 插值表达式存在的问题：闪动。
   + 如何解决该问题： 使用v-cloak指令。
   + 解决该问题的原理：先隐藏，替换好值之后再显示最终的值。

   ![image-20210406124504057](D:\vue\Vue.js.assets\image-20210406124504057.png)

2. v-text
   + v-text指令用于将数据填充到标签中，作用与插值表达式类似，但没有闪动问题。
   + 如果数据中有HTML标签会将html标签一并输出。
   + 注意：此处为单向绑定，数据对象上的值改变，插值会发生变化；但是当插值发生变化并不会影响数据对象的值。

3. v-html
   + 用法与v-text相似，但是它可以将html片段填充到标签中
   + 可能有安全问题，一般只在可信任内容上使用v-html，永不用在用户提交的内容上。
   + 它与v-text区别在于v-text输出的是纯文本，浏览器不会对其再进行html解析，但v-html会将其当html标签解析后输出。

4. v-pre

   + 显示原始信息跳过编译过程。
   + 跳过这个元素和它的子元素的编译过程。
   + 一些静态内容不需要编译加这个指令可以加快渲染。

   ![image-20210406125652345](D:\vue\Vue.js.assets\image-20210406125652345.png)

   ```js
   <body>
       <div v-cloak id="app">
           {{msg}}
           <div v-text='msg'></div>
           <div v-text='msg1'></div>
           <div v-html='msg1'></div>
           <div v-pre='msg'>{{msg}}</div>
       </div>
       <script src="./vue.min.js"></script>
       <script>
           var vm = new Vue({
               el: '#app',
               data: {
                   msg: 'Hello Vue!',
                   msg1: '<h1>Hellp Vue!</h1>'
               }
           })
       </script>
   </body>
   ```

   ![image-20210406130344301](D:\vue\Vue.js.assets\image-20210406130344301.png)

5. 数据响应式

   ![image-20210406130512710](D:\vue\Vue.js.assets\image-20210406130512710.png)

6. 双向数据绑定

   v-model

   ![image-20210406131639728](D:\vue\Vue.js.assets\image-20210406131639728.png)

   MVVM：

   ​	![image-20210406131930951](D:\vue\Vue.js.assets\image-20210406131930951.png)

7. 事件绑定

   v-on：

   + 用来绑定事件的
   + v-on:click缩写为@click

   ![image-20210406133956841](D:\vue\Vue.js.assets\image-20210406133956841.png)

   事件绑定-参数传递

   ![image-20210406134356514](D:\vue\Vue.js.assets\image-20210406134356514.png)

   ```js
   <div id="app">
   <div>{{num}}</div>
   <div>
   <!-- 如果事件直接绑定函数名称，那么默认会传递事件对象作为事件函数的第一个参数 -->
   <button v-on:click='handle1'>点击1</button>
   <!-- 2、如果事件绑定函数调用，那么事件对象必须作为最后一个参数显示传递，
   并且事件对象的名称必须是$event
   -->
   <button v-on:click='handle2(123, 456, $event)'>点击2</button>
   </div>
   </div>
   <script type="text/javascript" src="js/vue.js"></script>
   <script type="text/javascript">
   var vm = new Vue({
   el: '#app',
   data: {
   num: 0
   },
   methods: {
   handle1: function(event) {
   console.log(event.target.innerHTML)
   },
   handle2: function(p, p1, event) {
   console.log(p, p1)
   console.log(event.target.innerHTML)
   this.num++;
   }
   }
   });
   </script>
   ```

8. 事件修饰符

   ![image-20210406134714473](D:\vue\Vue.js.assets\image-20210406134714473.png)

   使用修饰符时，顺序很重要；相应的代码会以同样的顺序产生，因此，用v-on:click.prevent.self会阻止所有的点击，而v-on:click.self.prevent只会阻止对元素自身的点击

9. 按键修饰符

   ![image-20210406145850056](D:\vue\Vue.js.assets\image-20210406145850056.png)

   自定义按键修饰符

   ![image-20210406150314496](D:\vue\Vue.js.assets\image-20210406150314496.png)

   ![image-20210406150330820](D:\vue\Vue.js.assets\image-20210406150330820.png)

10. 属性绑定

    1. v-bind

       ![image-20210406164543733](D:\vue\Vue.js.assets\image-20210406164543733.png)

    2. 绑定对象

       ![image-20210406171810686](D:\vue\Vue.js.assets\image-20210406171810686.png)

       ![image-20210406171825612](D:\vue\Vue.js.assets\image-20210406171825612.png)

    3. 绑定数组

       ![image-20210406171905046](D:\vue\Vue.js.assets\image-20210406171905046.png)

11. 分支循环结构

    1. v-if

       ![image-20210406192026878](D:\vue\Vue.js.assets\image-20210406192026878.png)

    2. v-show和v-if的区别

       ![image-20210406192101202](D:\vue\Vue.js.assets\image-20210406192101202.png)

    3. v-for

       用于循环的数组里面的值可以是对象，也可以是普通元素。

       ![image-20210406192317271](D:\vue\Vue.js.assets\image-20210406192317271.png)

       ![image-20210406195635764](D:\vue\Vue.js.assets\image-20210406195635764.png)

       ![image-20210406195746016](D:\vue\Vue.js.assets\image-20210406195746016.png)

       ​	![image-20210406200113828](D:\vue\Vue.js.assets\image-20210406200113828.png)

### 3.Vue常用特性

1. **表单操作**

   1. input单行文本 	textarea多行文本	select下拉多选	radio单选框 	checkbox多选框

   2. 通过v-model获取单选框中的值

      ![image-20210407151311567](D:\vue\Vue.js.assets\image-20210407151311567.png)

   3. 通过v-model获取复选框中的值

      复选框checkbox这种的组合时data中的hobby我们要定义成数组否则无法实现多选。

      ![image-20210407151642429](D:\vue\Vue.js.assets\image-20210407151642429.png)

      ![image-20210407151658154](D:\vue\Vue.js.assets\image-20210407151658154.png)

   4. 通过v-model获取下拉框和文本框中的值

      ![image-20210407152028539](D:\vue\Vue.js.assets\image-20210407152028539.png)

   5. 表单修饰符(添加在v-model之后)

      1. .number转换为数值
         + 当开始输入非数字的字符串时，因为Vue无法将字符串转换成数值
         +  所以属性值将实时更新成相同的字符串。即使后面输入数字，也将被视作字符串。
      2. .trim自动过滤用户输入的首尾空白字符
         + 只能去掉首尾的 不能去除中间的空格
      3. lazy将input事件切换成change事件
         + lazy 修饰符延迟了同步更新属性值的时机。即将原本绑定在 input 事件的同步逻辑转变为绑定在 change 事件上

      ```html
      <!-- 自动将用户的输入值转为数值类型 -->
      <input v-model.number="age" type="number">
      <!--自动过滤用户输入的首尾空白字符 -->
      <input v-model.trim="msg">
      <!-- 在“change”时而非“input”时更新 -->
      <input v-model.lazy="msg" >
      ```

2. **自定义指令**

   ```js
   <div id="app">
           <input type="text" v-focus>
           <input type="text" v-color='msg'>
       </div>
       <script src="./vue.min.js"></script>
       <script>
           //光标自动定位 
           //全局指令
           Vue.directive('focus', {
               inserted: function (el) {
                   el.focus();
               }
           })
   		Vue.directive('color', {
   			// bind声明周期, 只调用一次，指令第一次绑定到元素时调用。在这里可以进行一次性的初始化设置
   			// el 为当前自定义指令的DOM元素
   			// binding 为自定义的函数形参 通过自定义属性传递过来的值 存在binding.value 里面
   			bind: function(el, binding){
   				// 根据指令的参数设置背景色
   				// console.log(binding.value.color)
   				el.style.backgroundColor = binding.value.color;
   			}
   		});
   
   
           var vm = new Vue({
               el: '#app',
               data: {
                   msg: {
                       color: 'orange'
                   }
               },
               directives: {//局部指令
                   color: {//带参数的自定义指令
                       inserted: function (el, binding) {
                           el.style.backgroundColor = binding.value.color;
                       }
                   }
               }
           })
       </script>
   ```

### 3. 计算属性computed

+ 模板中放入太多的逻辑会让模板过重且难以维护 使用计算属性可以让模板更加的简洁 。

+ 计算属性是基于它们的响应式依赖进行缓存的 。

+ computed比较适合对多个变量或者对象进行处理后返回一个结果值，也就是数多个变量中的某一个值发生了变 化则我们监控的这个值也就会发生变化。

  ```js
   <div id="app">
          <div>{{msg}}</div>
          <div>{{reverseMessage}}</div>
          <div>{{reverseMessage}}</div>
          <div>{{reverseString()}}</div>
          <div>{{reverseString()}}</div>
      </div>
      <script src="./vue.min.js"></script>
      <script>
          // 计算属性与方法的区别：计算属性是基于依赖进行缓存的，而方法不缓存。
          var vm = new Vue({
              el: '#app',
              data: {
                  msg: 'nmsl'
              },
              methods: {
                  reverseString: function () {
                      console.log('methods');//控制台中methods将出现两次
                      return this.msg.split('').reverse().join('');
                  }
              },
              computed: {
                  reverseMessage: function () {
                      console.log('computed');
                      //控制台中computed将只出现一次
                      //第二次调用时将直接从缓存中取结果
                      return this.msg.split('').reverse().join('');
                  }
              }
          })
      </script>
  ```

### 4. 帧听器watch

+ 使用watch来响应数据的变化 

+ 一般用于异步或者开销较大的操作 

+ watch 中的属性 一定是data 中 已经存在的数据 

+ 当需要监听一个对象的改变时，普通的watch方法无法监听到对象内部属性的改变，只有data中的数据才能够 监听到变化，此时就需要deep属性对对象进行深度监听

  ```js
  //侦听器案例
  	<div id="app">
          <div>
              <span>用户名：</span>
              <span>
                  <input type="text" v-model.lazy='uname'>
              </span>
              <span>{{tip}}</span>
          </div>
      </div>
      <script src="./vue.min.js"></script>
      <script>
          var vm = new Vue({
              el: '#app',
              data: {
                  uname: '',
                  tip: ''
              },
              methods: {
                  check: function (uname) {
                      var that = this;
                      setTimeout(() => {
                          if (uname === 'admin') {
                              that.tip = 'change a username';
                          } else {
                              that.tip = 'ok';
                          }
                      }, 2000);
                  }
              },
              watch: {
                  uname: function (val) {
                      this.check(val);
                      this.tip = 'loading';
                  }
              }
          })
      </script>
  ```

### 5. 过滤器

+ Vue.js允许自定义过滤器，可被用于一些常见的文本格式化。 

+ 过滤器可以用在两个地方：双花括号插值和v-bind表达式。 

+ 过滤器应该被添加在JavaScript表达式的尾部，由“管道”符号指示 支持级联操作。 

+ 过滤器不改变真正的 data ，而只是改变渲染的结果，并返回过滤后的版本 

+ 全局注册时是filter，没有s的。而局部过滤器是filters，是有s的

  ```html
  <div id="app">
      <input type="text" v-model='msg'>
      <!-- upper 被定义为接收单个参数的过滤器函数，表达式 msg 的值将作为参数传入到函数中 -->
      <div>{{msg | upper}}</div>
      <!--
      支持级联操作
      upper 被定义为接收单个参数的过滤器函数，表达式msg 的值将作为参数传入到函数中。
      然后继续调用同样被定义为接收单个参数的过滤器 lower ，将upper 的结果传递到lower中
      -->
      <div>{{msg | upper | lower}}</div>
      <div :abc='msg | upper'>测试数据</div>
  </div>
  <script type="text/javascript">
      // lower 为全局过滤器
      Vue.filter('lower', function (val) {
          return val.charAt(0).toLowerCase() + val.slice(1);
      });
      var vm = new Vue({
          el: '#app',
          data: {
              msg: ''
          },
          //filters 属性 定义 和 data 已经 methods 平级
          // 定义filters 中的过滤器为局部过滤器
          filters: {
              // upper 自定义的过滤器名字
              // upper 被定义为接收单个参数的过滤器函数，表达式 msg 的值将作为参数传入到函数中
              upper: function (val) {
                  // 过滤器中一定要有返回值 这样外界使用过滤器的时候才能拿到结果
                  return val.charAt(0).toUpperCase() + val.slice(1);
              }
          }
      });
  </script>
  ```

### 6. 生命周期

​	Vue实例从创建到销毁的过程，这些过程中会伴随着一些函数的自我调用。我们称这些函数为钩子函数。

![image-20210407175128192](D:\vue\Vue.js.assets\image-20210407175128192.png)

### 7.变异数组

​	![image-20210407195605019](D:\vue\Vue.js.assets\image-20210407195605019.png)	

​	动态数组响应式数据：Vue.set(vm.item,indexOfItem,newValue)让触发视图重新更新一遍，数据动态起来。vm.item是要更改的数据、indexOfItem是数据的第几项、newValue是更改后的数据。

## 2.Vue组件

### 1.组件注册

1. 全局组件注册语法

   ```js
   Vue.component(组件名称，{
                 data:组件数据，
                 template:组件模板内容
                 })
   //例子：定义一个名为button-counter的新组件
   Vue.component('button-counter',{
       data:function(){
           return{
               count:0
           }
       },
       template:'<button v-on:click='count++'>点击了{{count}}次</button>'
   })
   ```

2. 组件注册注意事项

   ![image-20210409135401320](D:\vue\Vue.js.assets\image-20210409135401320.png)

   ![image-20210409135837950](D:\vue\Vue.js.assets\image-20210409135837950.png)

   驼峰命名法命名组件时，不能直接写到html中，可以用短横线方式写到html中，但是可以直接写到其他子组件的template中。

   ```html
     <div id="app">
        <!-- 
   		4、  组件可以重复使用多次 
   	      因为data中返回的是一个对象所以每个组件中的数据是私有的
   		  即每个实例可以维护一份被返回对象的独立的拷贝   
   	--> 
       <button-counter></button-counter>
       <button-counter></button-counter>
       <button-counter></button-counter>
         <!-- 8、必须使用短横线的方式使用组件 -->
        <hello-world></hello-world>
     </div>
   
   <script type="text/javascript">
   	//5  如果使用驼峰式命名组件，那么在使用组件的时候，只能在字符串模板中用驼峰的方式使用组件，
       // 7、但是在普通的标签模板中，必须使用短横线的方式使用组件
        Vue.component('HelloWorld', {
         data: function(){
           return {
             msg: 'HelloWorld'
           }
         },
         template: '<div>{{msg}}</div>'
       });
       
       
       
       Vue.component('button-counter', {
         // 1、组件参数的data值必须是函数 
         // 同时这个函数要求返回一个对象  
         data: function(){
           return {
             count: 0
           }
         },
         //  2、组件模板必须是单个根元素
         //  3、组件模板的内容可以是模板字符串  
         template: `
           <div>
             <button @click="handle">点击了{{count}}次</button>
             <button>测试123</button>
   			#  6 在字符串模板中可以使用驼峰的方式使用组件	
   		   <HelloWorld></HelloWorld>
           </div>
         `,
         methods: {
           handle: function(){
             this.count += 2;
           }
         }
       })
       var vm = new Vue({
         el: '#app',
         data: {
           
         }
       });
     </script>
   ```

   

2. 局部组件注册

   只能在当前注册它的Vue实例中使用

   ```html
     <div id="app">
         <my-component></my-component>
     </div>
   
   
   <script>
       // 定义组件的模板
       var Child = {
         template: '<div>A custom component!</div>'
       }
       new Vue({
         //局部注册组件  
         components: {
           // <my-component> 将只在父模板可用  一定要在实例上注册了才能在html文件中使用
           'my-component': Child
         }
       })
    </script>
   ```

### 3.Vue调试工具

### 4.组件间数据交互

1. 父组件向子组件传值

   + 父组件发送的形式是以属性的形式绑定值到子组件身上。
   + 然后子组件用属性props接收。
   + 在props中使用驼峰形式，模板中需要使用短横线的形式字符串形式的模板中没有这个限制。

   ```html
   <div id="app">
       <div>{{pmsg}}</div>
        <!--1、menu-item  在 APP中嵌套着 故 menu-item   为  子组件      -->
        <!-- 给子组件传入一个静态的值 -->
       <menu-item title='来自父组件的值'></menu-item>
       <!-- 2、 需要动态的数据的时候 需要属性绑定的形式设置 此时 ptitle  来自父组件data 中的数据 . 
   		  传的值可以是数字、对象、数组等等
   	-->
       <menu-item :title='ptitle' content='hello'></menu-item>
     </div>
   
     <script type="text/javascript">
       Vue.component('menu-item', {
         // 3、 子组件用属性props接收父组件传递过来的数据  
         props: ['title', 'content'],
         data: function() {
           return {
             msg: '子组件本身的数据'
           }
         },
         template: '<div>{{msg + "----" + title + "-----" + content}}</div>'
       });
       var vm = new Vue({
         el: '#app',
         data: {
           pmsg: '父组件中内容',
           ptitle: '动态绑定属性'
         }
       });
     </script>
   ```

2. 子组件向父组件传值

   + 子组件用`$emit()`触发事件
   + `$emit()`第一个参数为自定义的事件名称 第二个参数为需要传递的数据
   + 父组件用v-on监听子组件的事件

   ```html
    <div id="app">
       <div :style='{fontSize: fontSize + "px"}'>{{pmsg}}</div>
        <!-- 2 父组件用v-on 监听子组件的事件
   		这里 enlarge-text  是从 $emit 中的第一个参数对应   handle 为对应的事件处理函数	
   	-->	
       <menu-item :parr='parr' @enlarge-text='handle($event)'></menu-item>
     </div>
     <script type="text/javascript" src="js/vue.js"></script>
     <script type="text/javascript">
       /*
         子组件向父组件传值-携带参数
       */
       
       Vue.component('menu-item', {
         props: ['parr'],
         template: `
           <div>
             <ul>
               <li :key='index' v-for='(item,index) in parr'>{{item}}</li>
             </ul>
   			###  1、子组件用$emit()触发事件
   			### 第一个参数为 自定义的事件名称   第二个参数为需要传递的数据  
             <button @click='$emit("enlarge-text", 5)'>扩大父组件中字体大小</button>
             <button @click='$emit("enlarge-text", 10)'>扩大父组件中字体大小</button>
           </div>
         `
       });
       var vm = new Vue({
         el: '#app',
         data: {
           pmsg: '父组件中内容',
           parr: ['apple','orange','banana'],
           fontSize: 10
         },
         methods: {
           handle: function(val){
             // 扩大字体大小
             this.fontSize += val;
           }
         }
       });
     </script>
   ```

3. 兄弟之间的传递

   - 兄弟之间传递数据需要借助于事件中心，通过事件中心传递数据   

     ![image-20210409162642858](D:\vue\Vue.js.assets\image-20210409162642858.png)

     - 提供事件中心    var hub = new Vue()

   - 传递数据方，通过一个事件触发hub.$emit(方法名，传递的数据)

   - 接收数据方，通过mounted(){} 钩子中  触发hub.$on()方法名

   - 销毁事件 通过hub.$off()方法名销毁之后无法进行传递数据

### 5.组件插槽

1. 匿名插槽

   ```html
     <div id="app">
       <!-- 这里的所有组件标签中嵌套的内容会替换掉slot  如果不传值 则使用 slot 中的默认值  -->  
       <alert-box>有bug发生</alert-box>
       <alert-box>有一个警告</alert-box>
       <alert-box></alert-box>
     </div>
   
     <script type="text/javascript">
       /*
         组件插槽：父组件向子组件传递内容
       */
       Vue.component('alert-box', {
         template: `
           <div>
             <strong>ERROR:</strong>
   		# 当组件渲染的时候，这个 <slot> 元素将会被替换为“组件标签中嵌套的内容”。
   		# 插槽内可以包含任何模板代码，包括 HTML
             <slot>默认内容</slot>
           </div>
         `
       });
       var vm = new Vue({
         el: '#app',
         data: {
           
         }
       });
     </script>
   </body>
   </html>
   ```

2. 具名插槽

   使用<slot>中的“name”属性绑定元素

   ```html
    <div id="app">
       <base-layout>
          <!-- 2、 通过slot属性来指定, 这个slot的值必须和下面slot组件得name值对应上
   				如果没有匹配到 则放到匿名的插槽中   --> 
         <p slot='header'>标题信息</p>
         <p>主要内容1</p>
         <p>主要内容2</p>
         <p slot='footer'>底部信息信息</p>
       </base-layout>
   
       <base-layout>
         <!-- 注意点：template临时的包裹标签最终不会渲染到页面上     -->  
         <template slot='header'>
           <p>标题信息1</p>
           <p>标题信息2</p>
         </template>
         <p>主要内容1</p>
         <p>主要内容2</p>
         <template slot='footer'>
           <p>底部信息信息1</p>
           <p>底部信息信息2</p>
         </template>
       </base-layout>
     </div>
     <script type="text/javascript" src="js/vue.js"></script>
     <script type="text/javascript">
       /*
         具名插槽
       */
       Vue.component('base-layout', {
         template: `
           <div>
             <header>
   			###	1、 使用 <slot> 中的 "name" 属性绑定元素 指定当前插槽的名字
               <slot name='header'></slot>
             </header>
             <main>
               <slot></slot>
             </main>
             <footer>
   			###  注意点： 
   			###  具名插槽的渲染顺序，完全取决于模板，而不是取决于父组件中元素的顺序
               <slot name='footer'></slot>
             </footer>
           </div>
         `
       });
       var vm = new Vue({
         el: '#app',
         data: {
           
         }
       });
     </script>
   </body>
   </html>
   ```

3. 作用域插槽

   + 父组件对子组件加工处理
   + 既可以复用子组件的slot，又可以使slot内容不一致

   ```html
     <div id="app">
       <!-- 
   		1、当我们希望li 的样式由外部使用组件的地方定义，因为可能有多种地方要使用该组件，
   		但样式希望不一样 这个时候我们需要使用作用域插槽 
   		
   	-->  
       <fruit-list :list='list'>
          <!-- 2、 父组件中使用了<template>元素,而且包含scope="slotProps",
   			slotProps在这里只是临时变量   
   		---> 	
         <template slot-scope='slotProps'>
           <strong v-if='slotProps.info.id==3' class="current">
               {{slotProps.info.name}}		         
            </strong>
           <span v-else>{{slotProps.info.name}}</span>
         </template>
       </fruit-list>
     </div>
     <script type="text/javascript" src="js/vue.js"></script>
     <script type="text/javascript">
       /*
         作用域插槽
       */
       Vue.component('fruit-list', {
         props: ['list'],
         template: `
           <div>
             <li :key='item.id' v-for='item in list'>
   			###  3、 在子组件模板中,<slot>元素上有一个类似props传递数据给组件的写法msg="xxx",
   			###   插槽可以提供一个默认内容，如果如果父组件没有为这个插槽提供了内容，会显示默认的内容。
   					如果父组件为这个插槽提供了内容，则默认的内容会被替换掉
               <slot :info='item'>{{item.name}}</slot>
             </li>
           </div>
         `
       });
       var vm = new Vue({
         el: '#app',
         data: {
           list: [{
             id: 1,
             name: 'apple'
           },{
             id: 2,
             name: 'orange'
           },{
             id: 3,
             name: 'banana'
           }]
         }
       });
     </script>
   </body>
   </html>
   ```

## 3.Vue的前后端交互模式

### 1. URL地址格式	

1. 接口调用方式
   + 原生ajax
   + 基于jquery的ajax
   + fetch
   + axios

2. URL地址格式

   ![image-20210410151912243](D:\vue\Vue.js.assets\image-20210410151912243.png)

   ![image-20210410152157562](D:\vue\Vue.js.assets\image-20210410152157562.png)

### 2.Promise

​	使用promise是异步编程的一种解决方案，从语法上讲，Promise是一个对象，从它可以获取异步操作的消息。

​	使用promise主要有以下好处：

+ 可以避免多层异步调用的嵌套问题。
+ Promise对象提供了简洁的API，使得控制异步操作更加容易。

1. 基本用法 

   ![image-20210410155346523](D:\vue\Vue.js.assets\image-20210410155346523.png)

2. 基于promise发送Ajax请求

   ```js
   /*
         基于Promise发送Ajax请求
       */
       function queryData(url) {
        #   1.1 创建一个Promise实例
         var p = new Promise(function(resolve, reject){
           var xhr = new XMLHttpRequest();
           xhr.onreadystatechange = function(){
             if(xhr.readyState != 4) return;
             if(xhr.readyState == 4 && xhr.status == 200) {
               # 1.2 处理正常的情况
               resolve(xhr.responseText);
             }else{
               # 1.3 处理异常情况
               reject('服务器错误');
             }
           };
           xhr.open('get', url);
           xhr.send(null);
         });
         return p;
       }
   	# 注意：  这里需要开启一个服务 
       # 在then方法中，你也可以直接return数据而不是Promise对象，在后面的then中就可以接收到数据了
       queryData('http://localhost:3000/data')
         .then(function(data){
           console.log(data)
           #  1.4 想要继续链式编程下去 需要 return  
           return queryData('http://localhost:3000/data1');
         })
         .then(function(data){
           console.log(data);
           return queryData('http://localhost:3000/data2');
         })
         .then(function(data){
           console.log(data)
         });
   ```

3. then参数中的函数返回值

   1. 返回Promise实例对象

      返回的该实例对象会调用下一个then

   2. 返回普通值

      返回的普通值会直接传递给下一个then，通过then参数中函数的参数接收该值

4. Promise基本API

   + .then()：得到异步任务正确的结果
   + .catch():获取异常信息
   + .finally()：成功与否都会执行

   ```js
       /*
         Promise常用API-实例方法
       */
       // console.dir(Promise);
       function foo() {
         return new Promise(function(resolve, reject){
           setTimeout(function(){
             // resolve(123);
             reject('error');
           }, 100);
         })
       }
       // foo()
       //   .then(function(data){
       //     console.log(data)
       //   })
       //   .catch(function(data){
       //     console.log(data)
       //   })
       //   .finally(function(){
       //     console.log('finished')
       //   });
   
       // --------------------------
       // 两种写法是等效的
       foo()
         .then(function(data){
           # 得到异步任务正确的结果
           console.log(data)
         },function(data){
           # 获取异常信息
           console.log(data)
         })
         # 成功与否都会执行（不是正式标准） 
         .finally(function(){
           console.log('finished')
         });
   ```

5. 静态方法

   + **.all():**并发处理多个异步任务，所有任务都执行完成才能得到结果。

     `Promise.all`方法接受一个数组作参数，数组中的对象（p1、p2、p3）均为promise实例（如果不是一个promise，该项会被用`Promise.resolve`转换为一个promise)。它的状态由这三个promise实例决定

   + **.race():**并发处理多个异步任务，只要有一个任务完成就能得到结果。

     `Promise.race`方法同样接受一个数组作参数。当p1, p2, p3中有一个实例的状态发生改变（变为`fulfilled`或`rejected`），p的状态就跟着改变。并把第一个改变状态的promise的返回值，传给p的回调函数

   ```js
       /*
         Promise常用API-对象方法
       */
       // console.dir(Promise)
       function queryData(url) {
         return new Promise(function(resolve, reject){
           var xhr = new XMLHttpRequest();
           xhr.onreadystatechange = function(){
             if(xhr.readyState != 4) return;
             if(xhr.readyState == 4 && xhr.status == 200) {
               // 处理正常的情况
               resolve(xhr.responseText);
             }else{
               // 处理异常情况
               reject('服务器错误');
             }
           };
           xhr.open('get', url);
           xhr.send(null);
         });
       }
   
       var p1 = queryData('http://localhost:3000/a1');
       var p2 = queryData('http://localhost:3000/a2');
       var p3 = queryData('http://localhost:3000/a3');
        Promise.all([p1,p2,p3]).then(function(result){
          //   all 中的参数  [p1,p2,p3]   和 返回的结果一 一对应["HELLO TOM", "HELLO JERRY", "HELLO SPIKE"]
          console.log(result) //["HELLO TOM", "HELLO JERRY", "HELLO SPIKE"]
        })
       Promise.race([p1,p2,p3]).then(function(result){
         // 由于p1执行较快，Promise的then()将获得结果'P1'。p2,p3仍在继续执行，但执行结果将被丢弃。
         console.log(result) // "HELLO TOM"
       })
   ```

### 3.fetch

1. fetch基本用法

   + Fetch API是新的ajax解决方案 Fetch会返回Promise

   + **fetch不是ajax的进一步封装，而是原生js，没有使用XMLHttpRequest对象**。

   + fetch(url, options).then(）

   ```js
      /*
         Fetch API 基本用法
         	fetch(url).then()
        	第一个参数请求的路径   Fetch会返回Promise   所以我们可以使用then 拿到请求成功的结果 
       */
       fetch('http://localhost:3000/fdata').then(function(data){
         // text()方法属于fetchAPI的一部分，它返回一个Promise实例对象，用于获取后台返回的数据
         return data.text();
       }).then(function(data){
         //   在这个then里面我们能拿到最终的数据  
         console.log(data);
       })
   ```

2. fetch API中的HTTP请求

   + fetch(url, options).then()

   + HTTP协议，它给我们提供了很多的方法，如POST，GET, DELETE,UPDATE,PATCH和PUT

     + 默认是GET请求
     + 需要在options对象中指定对应的method         method：请求使用的方法
     + post和普通请求的时候需要在options中设置请求头headers和body

     ```js
             /*
                   Fetch API 调用接口传递参数
             */
            #1.1 GET参数传递 - 传统URL  通过url  ？ 的形式传参 
             fetch('http://localhost:3000/books?id=123', {
                 	# get 请求可以省略不写 默认的是GET 
                     method: 'get'
                 })
                 .then(function(data) {
                 	# 它返回一个Promise实例对象，用于获取后台返回的数据
                     return data.text();
                 }).then(function(data) {
                 	# 在这个then里面我们能拿到最终的数据  
                     console.log(data)
                 });
     
           #1.2  GET参数传递  restful形式的URL  通过/ 的形式传递参数  即  id = 456 和id后台的配置有关   
             fetch('http://localhost:3000/books/456', {
                 	# get 请求可以省略不写 默认的是GET 
                     method: 'get'
                 })
                 .then(function(data) {
                     return data.text();
                 }).then(function(data) {
                     console.log(data)
                 });
     
            #2.1  DELETE请求方式参数传递      删除id  是  id=789
             fetch('http://localhost:3000/books/789', {
                     method: 'delete'
                 })
                 .then(function(data) {
                     return data.text();
                 }).then(function(data) {
                     console.log(data)
                 });
     
            #3 POST请求传参
             fetch('http://localhost:3000/books', {
                     method: 'post',
                 	# 3.1  传递数据 
                     body: 'uname=lisi&pwd=123',
                 	#  3.2  设置请求头 
                     headers: {
                         'Content-Type': 'application/x-www-form-urlencoded'
                     }
                 })
                 .then(function(data) {
                     return data.text();
                 }).then(function(data) {
                     console.log(data)
                 });
     
            # POST请求传参
             fetch('http://localhost:3000/books', {
                     method: 'post',
                     body: JSON.stringify({
                         uname: '张三',
                         pwd: '456'
                     }),
                     headers: {
                         'Content-Type': 'application/json'
                     }
                 })
                 .then(function(data) {
                     return data.text();
                 }).then(function(data) {
                     console.log(data)
                 });
     
             # PUT请求传参     修改id 是 123 的 
             fetch('http://localhost:3000/books/123', {
                     method: 'put',
                     body: JSON.stringify({
                         uname: '张三',
                         pwd: '789'
                     }),
                     headers: {
                         'Content-Type': 'application/json'
                     }
                 })
                 .then(function(data) {
                     return data.text();
                 }).then(function(data) {
                     console.log(data)
                 });
     ```

3. fetchAPI中的响应格式

   + 用fetch来获取数据，如果响应正常返回，我们首先看到的是一个response对象，其中包括返回的一堆原始字节，这些字节需要在收到后，需要我们通过调用方法将其转换为相应格式的数据，比如`JSON`,`BLOB`或者`TEXT`等等

   ```js
      fetch('http://localhost:3000/json').then(function(data){
         // return data.json();   //  将获取到的数据使用 json 转换对象
         return data.text(); //  //  将获取到的数据 转换成字符串 
       }).then(function(data){
         // console.log(data.uname)
         // console.log(typeof data)
         var obj = JSON.parse(data);
         console.log(obj.uname,obj.age,obj.gender)
       })
   ```

### 4.axios

+ 基于promise用于浏览器和node.js的http客户端
+ 支持浏览器和node.js
+ 支持promise
+ 能拦截请求和响应
+ 自动转换JSON数据
+ 能转换请求和响应数据

1. axios基本用法

   + get和delete请求传递参数
     + 通过传统的url以？的形式传递参数
     + restful形式传递参数
     + 通过params形式传递参数

   + post和put请求传递参数

     + 通过选项传递参数
     + 通过URLSearchParams传递参数

     ```js
         # 1. 发送get 请求 
     	axios.get('http://localhost:3000/adata').then(function(ret){ 
           #  拿到 ret 是一个对象      所有的对象都存在 ret 的data 属性里面
           // 注意data属性是固定的用法，用于获取后台的实际数据
           // console.log(ret.data)
           console.log(ret)
         })
     	# 2.  get 请求传递参数
         # 2.1  通过传统的url  以 ? 的形式传递参数
     	axios.get('http://localhost:3000/axios?id=123').then(function(ret){
           console.log(ret.data)
         })
         # 2.2  restful 形式传递参数 
         axios.get('http://localhost:3000/axios/123').then(function(ret){
           console.log(ret.data)
         })
     	# 2.3  通过params  形式传递参数 
         axios.get('http://localhost:3000/axios', {
           params: {
             id: 789
           }
         }).then(function(ret){
           console.log(ret.data)
         })
     	#3 axios delete 请求传参     传参的形式和 get 请求一样
         axios.delete('http://localhost:3000/axios', {
           params: {
             id: 111
           }
         }).then(function(ret){
           console.log(ret.data)
         })
     
     	# 4  axios 的 post 请求
         # 4.1  通过选项传递参数
         axios.post('http://localhost:3000/axios', {
           uname: 'lisi',
           pwd: 123
         }).then(function(ret){
           console.log(ret.data)
         })
     	# 4.2  通过 URLSearchParams  传递参数 
         var params = new URLSearchParams();
         params.append('uname', 'zhangsan');
         params.append('pwd', '111');
         axios.post('http://localhost:3000/axios', params).then(function(ret){
           console.log(ret.data)
         })
     
      	#5  axios put 请求传参   和 post 请求一样 
         axios.put('http://localhost:3000/axios/123', {
           uname: 'lisi',
           pwd: 123
         }).then(function(ret){
           console.log(ret.data)
         })
     ```

2. axios全局配置

   ```js
   #  配置公共的请求头 
   axios.defaults.baseURL = 'https://api.example.com';
   #  配置 超时时间
   axios.defaults.timeout = 2500;
   #  配置公共的请求头
   axios.defaults.headers.common['Authorization'] = AUTH_TOKEN;
   # 配置公共的 post 的 Content-Type
   axios.defaults.headers.post['Content-Type'] = 'application/x-www-form-urlencoded';
   ```

3. axios拦截器

   1. 请求拦截器

      + 请求拦截器的作用是在请求发送前进行一些操作

        例如在每个请求体里加上token，统一做了处理后，以后要改也非常容易

   2. 响应拦截器

      + 响应拦截器的作用是在接收到响应后进行一些操作

        例如在服务器返回登录状态失效，需要重新登录的时候，跳转到登录页

   ```js
   	# 1. 请求拦截器 
   	axios.interceptors.request.use(function(config) {
         console.log(config.url)
         # 1.1  任何请求都会经过这一步   在发送请求之前做些什么   
         config.headers.mytoken = 'nihao';
         # 1.2  这里一定要return   否则配置不成功  
         return config;
       }, function(err){
          #1.3 对请求错误做点什么    
         console.log(err)
       })
   	#2. 响应拦截器 
       axios.interceptors.response.use(function(res) {
         #2.1  在接收响应做些什么  
         var data = res.data;
         return data;
       }, function(err){
         #2.2 对响应错误做点什么  
         console.log(err)
       })
   ```

4. async和await

   1. async作为一个关键字放到函数前面

      任何一个`async`函数都会隐式返回一个`promise`

   2. await关键字只能在使用async定义的函数中使用

      await后面可以直接跟一个Promise实例对象

      await函数不能单独使用

   3. async/await让异步代码看起来、表现起来更像同步代码

      ```js
       	# 1.  async 基础用法
          # 1.1 async作为一个关键字放到函数前面
      	async function queryData() {
            # 1.2 await关键字只能在使用async定义的函数中使用      await后面可以直接跟一个 Promise实例对象
            var ret = await new Promise(function(resolve, reject){
              setTimeout(function(){
                resolve('nihao')
              },1000);
            })
            // console.log(ret.data)
            return ret;
          }
      	# 1.3 任何一个async函数都会隐式返回一个promise   我们可以使用then 进行链式编程
          queryData().then(function(data){
            console.log(data)
          })
      
      	#2.  async    函数处理多个异步函数
          axios.defaults.baseURL = 'http://localhost:3000';
      
          async function queryData() {
            # 2.1  添加await之后 当前的await 返回结果之后才会执行后面的代码   
            var info = await axios.get('async1');
            #2.2  让异步代码看起来、表现起来更像同步代码
            var ret = await axios.get('async2?info=' + info.data);
            return ret.data;
          }
      
          queryData().then(function(data){
            console.log(data)
          })
      ```

## 4.Vue路由

### 1. 路由的概念

+ 路由的本质就是一种对应关系，比如说我们在url地址中输入我们要访问的url地址之后，浏览器要去请求这个url地址对应的资源。那么url地址和真实的资源之间就有一种对应的关系，就是路由。	

+ 路由分为前端路由和后端路由
  + 后端路由是由服务器端进行实现，并完成资源的分发	
  + 前端路由是依靠hash值(锚链接)的变化进行实现 ，前端路由主要做的事情就是监听事件并分发执行事件处理函数。

### 2.Vue Router简介

+ 它是一个Vue.js官方提供的路由管理器。是一个功能更加强大的前端路由器，推荐使用。

+ Vue Router和Vue.js非常契合，可以一起方便的实现SPA(single page web application,单页应用程序)应用程序的开发。
+ Vue Router依赖于Vue，所以需要先引入Vue，再引入Vue Router

+ Vue Router的特性
  + 支持H5历史模式或hash模式
  + 支持嵌套路由
  + 支持路由参数
  + 支持编程式路由
  + 支持命名路由
  + 支持路由导航守卫
  + 支持路由过渡动画特效
  + 支持路由懒加载
  + 支持路由滚动行为

### 3.Vue Router的使用步骤

1. 导入js文件

2. 添加路由链接:<router-link>是路由中提供的标签，默认会被渲染为a标签，to属性默认被渲染为href属性，
   to属性的值会被渲染为#开头的hash地址
   <router-link to="/user">User</router-link>
   <router-link to="/login">Login</router-link>
3. .添加路由填充位（路由占位符）
   <router-view></router-view>
4. .定义路由组件
   var User = { template:"<div>This is User</div>" }
   var Login = { template:"<div>This is Login</div>" }
5. .配置路由规则并创建路由实例
   var myRouter = new VueRouter({
       //routes是路由规则数组
       routes:[
           //每一个路由规则都是一个对象，对象中至少包含path和component两个属性
           //path表示  路由匹配的hash地址，component表示路由规则对应要展示的组件对象
           {path:"/user",component:User},
           {path:"/login",component:Login}
       ]
   })
6. .将路由挂载到Vue实例中
   new Vue({
       el:"#app",
       //通过router属性挂载路由对象
       router:myRouter
   })

### 4.路由重定向与嵌套路由

1. 路由重定向：可以通过路由重定向为页面设置默认展示的组件，在路由规则中添加一条路由规则即可。

   ```js
   var myRouter = new VueRouter({
       //routes是路由规则数组
       routes: [
           //path设置为/表示页面最初始的地址 / ,redirect表示要被重定向的新地址，设置为一个路由即可
           { path:"/",redirect:"/user"},
           { path: "/user", component: User },
           { path: "/login", component: Login }
       ]
   })
   ```

2. **嵌套路由**

   1. 嵌套路由的概念

      嵌套路由最关键的代码在于理解子级路由的概念：
      比如我们有一个/login的路由，那么/login下面还可以添加子级路由，如:
      `/login/account`,`/login/phone`。

      ```js
      var User = { template: "<div>This is User</div>" }
      //Login组件中的模板代码里面包含了子级路由链接以及子级路由的占位符
          var Login = { template: `<div>
              <h1>This is Login</h1>
              <hr>
              <router-link to="/login/account">账号密码登录</router-link>
              <router-link to="/login/phone">扫码登录</router-link>
              <!-- 子路由组件将会在router-view中显示 -->
              <router-view></router-view>
              </div>` }
      
          //定义两个子级路由组件
          var account = { template:"<div>账号：<input><br>密码：<input></div>"};
          var phone = { template:"<h1>扫我二维码</h1>"};
          var myRouter = new VueRouter({
              //routes是路由规则数组
              routes: [
                  { path:"/",redirect:"/user"},
                  { path: "/user", component: User },
                  { 
                      path: "/login", 
                      component: Login,
                      //通过children属性为/login添加子路由规则
                      children:[
                          { path: "/login/account", component: account },
                          { path: "/login/phone", component: phone },
                      ]
                  }
              ]
          })
      
          var vm = new Vue({
              el: '#app',
              data: {},
              methods: {},
              router:myRouter
          });
      ```

      ![image-20210412112727377](D:\vue\Vue.js.assets\image-20210412112727377.png)

### 5.动态路由匹配

1. 基础的动态路由匹配

   ```js
   var User = { template:"<div>用户：{{$route.params.id}}</div>"}
   
   var myRouter = new VueRouter({
       //routes是路由规则数组
       routes: [
           //通过/:参数名  的形式传递参数 
           { path: "/user/:id", component: User },
           ]
   })
   ```

2. 如果使用`$route.params.id`来获取路径传参的数据不够灵活

   + 我们可以通过props来就接受参数

     ```js
     var User = { 
         props:["id"],
         template:"<div>用户：{{id}}</div>"
         }
     
     var myRouter = new VueRouter({
         //routes是路由规则数组
         routes: [
             //通过/:参数名  的形式传递参数 
             //如果props设置为true，route.params将会被设置为组件属性
             { path: "/user/:id", component: User,props:true },
             ]
     })
     ```

   + 还有一种情况，我们可以将props设置为对象，那么就直接将对象的数据传递给组件进行使用

     ```js
     var User = { 
         props:["username","pwd"],
         template:"<div>用户：{{username}}---{{pwd}}</div>"
         }
     
     var myRouter = new VueRouter({
         //routes是路由规则数组
         routes: [
             //通过/:参数名  的形式传递参数 
             //如果props设置为对象，则传递的是对象中的数据给组件
             { path: "/user/:id", component: User,props:								{username:"jack",pwd:123} },
             ]
     })
     ```

   + 如果想要获取传递的参数值还想要获取传递的对象数据，那么props应该设置为
     函数形式。

     ```js
     var User = { 
         props:["username","pwd","id"],
         template:"<div>用户：{{id}} -> {{username}}---{{pwd}}</div>"
         }
     
     var myRouter = new VueRouter({
         //routes是路由规则数组
         routes: [
             //通过/:参数名  的形式传递参数 
             //如果props设置为函数，则通过函数的第一个参数获取路由对象
             //并可以通过路由对象的params属性获取传递的参数
             //
             { path: "/user/:id", component: User,props:(route)=>{
                 return {username:"jack",pwd:123,id:route.params.id}
                 } 
             },
     	]
     })
     ```

### 6.命名路由以及编程式导航

1. 命名路由：给路由取名字

   ```js
   var myRouter = new VueRouter({
       //routes是路由规则数组
       routes: [
           //通过name属性为路由添加一个别名
           { path: "/user/:id", component: User, name:"user"},
           ]
   })
   ```

   添加了别名之后，可以使用别名进行跳转

   <router-link to="/user">User</router-link>
   <router-link :to="{ name:'user' , params: {id:123} }">User</router-link>

2. 编程式导航

   页面导航的两种方式：

   + 声明式导航：通过点击连接的方式实现的导航
   + 编程式导航：调用js的api方法实现导航

   Vue-Router中常见的导航方式：

   + this.$router.push("hash地址");
   + this.$router.push("/login");
   + this.$router.push({ name:'user' , params: {id:123} });
   + this.$router.push({ path:"/login" });
   + this.$router.push({ path:"/login",query:{username:"jack"} });
   + this.$router.go( n );//n为数字，参考history.go
   + this.$router.go( -1 );

## 5.webpack

### 1.es6模块化规范

1. es6模块化规范是浏览器端与服务器端通用的模块化开发规范，es6模块化规范中定义

   + 每个js文件都是一个独立的模块
   + 导入模块成员使用`import`关键字
   + 暴露模块成员使用`export`关键字

2. Node.js中通过babel体验ES6模块化

   ![image-20210412145051497](D:\vue\Vue.js.assets\image-20210412145051497.png)

3. es6模块化的基本语法

   1. 默认导出与默认导入

      + 默认导出语法 ：exports default  默认导出的成员

        ```js
        //当前文件模块为m1.js
        //定义私有成员a和c
        let a = 10;
        let c = 20;
        //外界访问不到变量d，因为它没有被暴露出去
        let d = 30;
        function show(){}
        //将本模块中的私有成员暴露出去，供其他模块使用
        export default{
            a,
            c,
        }
        ```

      + 默认导入语法 ：import  接收名称  from  '模块标识符'

        ```js
        //导入模块成员
        import m1 from './m1.js'
        
        console.log(m1);
        //打印输出结果为：
        //{a:1o, c:20, show:[Function:show]}
        ```

      **注意：每个模块中，只允许使用唯一的一次export default，否则会报错**

   2. 按需导出与按需导入

      ![image-20210412150914294](D:\vue\Vue.js.assets\image-20210412150914294.png)

   3. 直接导入并执行模块代码

      ![image-20210412150950509](D:\vue\Vue.js.assets\image-20210412150950509.png)

### 2.webpack

1. webpack概述：

   webpack是一个流行的前端构建工具（打包工具），可以解决当前web开发中所面临的困境。

   webpack提供了友好的模块化支持，以及代码压缩混淆，处理js兼容问题，性能优化等强大的功能，从而让程序员把工作的中心放到具体的功能是实现上，提高了开发效率和项目的可维护性。

2. webpack的基本使用

   1. 创建列表隔行变色项目

      ![image-20210412151417763](D:\vue\Vue.js.assets\image-20210412151417763.png)

   2. 在项目中安装和配置webpack

      ![image-20210412151512947](D:\vue\Vue.js.assets\image-20210412151512947.png)

   3. 配置打包的入口和出口

      ![image-20210412151539956](D:\vue\Vue.js.assets\image-20210412151539956.png)

   4. 配置webpack自动打包功能

      ![image-20210412151608282](D:\vue\Vue.js.assets\image-20210412151608282.png)

   5. 配置html-webpack-plugin生成预览页面

      ![image-20210412151645075](D:\vue\Vue.js.assets\image-20210412151645075.png)

   6. 配置自动打包相关的参数

      ![image-20210412151711394](D:\vue\Vue.js.assets\image-20210412151711394.png)

3. webpack中的加载器

   1. 通过loader打包非js模块

      ![image-20210412151809141](D:\vue\Vue.js.assets\image-20210412151809141.png)

   2. loader的调用过程

      ![image-20210412151838450](D:\vue\Vue.js.assets\image-20210412151838450.png)

4. webpack中加载器的基本使用

   1. 打包处理css文件

      ![image-20210412151926834](D:\vue\Vue.js.assets\image-20210412151926834.png)

   2. 打包处理less文件

      ![image-20210412151948968](D:\vue\Vue.js.assets\image-20210412151948968.png)

   3. 打包处理scss文件

      ![image-20210412152013386](D:\vue\Vue.js.assets\image-20210412152013386.png)

   4. 配置postCSS自动添加css的兼容前缀

      ![image-20210412152050368](D:\vue\Vue.js.assets\image-20210412152050368.png)

   5. 打包样式表中的图片和字体文件

      ![image-20210412152133216](D:\vue\Vue.js.assets\image-20210412152133216.png)

   6. 打包处理js文件中的高级语法

      ![image-20210412152155922](D:\vue\Vue.js.assets\image-20210412152155922.png)

### 3.Vue单文件组件

1. Vue单文件组件的基本用法

   单文件组件的组成结构

   + template    组件的模板区域

   + script    业务逻辑区域

   + style    样式区域

     ![image-20210413124021444](D:\vue\Vue.js.assets\image-20210413124021444.png)

2. webpack中配置vue 组件的加载器

   ![image-20210413124108699](D:\vue\Vue.js.assets\image-20210413124108699.png)

3. webpack项目中使用vue

   ![image-20210413124147012](D:\vue\Vue.js.assets\image-20210413124147012.png)

4. webpack打包发布

   ![image-20210413125403394](D:\vue\Vue.js.assets\image-20210413125403394.png)

### 4.Vue脚手架

1. Vue脚手架的基本用法

   + 安装3.x版本的Vue脚手架

     ```
     npm install -g @vue/cli
     ```

   + 基于3.x版本的脚手架创建vue项目

     ```
     //1.基于交互式命令行的方式，创建新版vue项目
     vue create my-project
     //2.基于图形化界面的方式，创建新版vue项目
     vue ui
     //3.基于2.x的旧模板，创建旧版vue项目
     npm install -g@vue/cli-init
     vue init webpack my-project
     ```

2. Vue脚手架生成的项目结构分析

   ![image-20210413125929654](D:\vue\Vue.js.assets\image-20210413125929654.png)

3. Vue脚手架的自定义配置

   1. 通过package.json配置项目

      注意：不推荐使用这种配置方式。因为package.json主要用来管理包的配置信息；为了方便维护，推荐将vue脚手架相关的配置，单独定义到vue.config.js配置文件中。

      ```
      //必须是符合会番地json语法
      "vue":{
      	"devServer":{
      	"port":"8888",
      	"open":true
      	}
      }
      ```

   2. 通过单独的配置文件配置项目

      + 在项目的根目录中创建文件vue.config.js

      + 在该文件中进行相关配置，从而覆盖默认配置

        ```
        //vue.config.js
        moudule.exports = {
        	devServer:{
        	port:8888
        	}
        }
        ```

### 5.Element-UI的基本使用  

1. 基于命令行方式手动安装

   ![image-20210413130609501](D:\vue\Vue.js.assets\image-20210413130609501.png)

2. 基于图形化界面自动安装

   ![image-20210413130632199](D:\vue\Vue.js.assets\image-20210413130632199.png)

## 6. vue案例

### 1.前端项目初始化步骤

+ 安装Vue脚手架
+ 通过脚手架创建项目
+ 配置路由
+ 配置Element-UI:在插件中安装，搜索vue-cli-plugin-element
+ 配置Axios：在依赖中安装,搜索axios(运行依赖)
+ 初始化git仓库
+ 将本地项目托管到github或者码云中

### 2.token原理分析

![image-20210413142316681](D:\vue\Vue.js.assets\image-20210413142316681.png)

### 3. 路由导航守卫控制访问权限

![image-20210414003641718](D:\vue\Vue.js.assets\image-20210414003641718.png)

1. ![image-20210414011414372](D:\vue\Vue.js.assets\image-20210414011414372.png)

### 4.slot-scope；scope.row,this.$refs.

### 5.提交表单时先预验证再发请求

![image-20210417163244909](D:\vue\Vue.js.assets\image-20210417163244909.png)

### 6.form

+ ：model：绑定数据
+ ：rules：验证规则
+ ref：引用

### 7.table

## 7. Vuex

### 1.Vuex概述

 1. Vuex是实现组件全局状态（数据）管理的一种机制，可以方便的实现组件之间数据的共享

    ![image-20210421160732291](D:\vue\Vue.js.assets\image-20210421160732291.png)

2. 使用Vuex统一管理状态的好处
   + 能够在vuex中集中管理共享的数据，易于开发和后期维护
   + 能够高效地实现组件之间地数据共享，提高开发效率
   + 存储在vuex中的数据都是响应式的，能够实时保持数据与页面的同步

3. 一般情况下，**只有组件之间共享的数据，才有必要存储到vuex中**；对于组件中的私有数据，依旧存储在组件自身的data中即可。

### 2.Vuex的基本使用

1. 安装vuex依赖包

   ```
   npm install vuex --save
   ```

2. 导入vuex包

   ```
   import Vuex from 'vuex'
   Vue.use(Vuex)
   ```

3. 创建store对象

   ```
   const store = new Vuex.Store({
   	// state 中存放的就是全局共享的数据
   	state：{count:0}
   })
   ```

4. 将store对象挂载到vue实例中

   ```
   new Vue({
   	el:'#app',
   	render:h=>h(app),
   	router,
   	store
   })
   ```

### 3.Vuex的核心概念

1. State

   State提供唯一的公共数据源，所有共享的数据都要统一放到Store的State中进行存储。

   ```
   // 创建store数据源，提供唯一公共数据
   const store = new Vuex.Store({
   	state:{ count: 0 }
   })
   ```

   组件访问State中数据的第一种方式：

   ```
   this.$store.state.全局数据名称
   ```

   ![image-20210421173215763](D:\vue\Vue.js.assets\image-20210421173215763.png)

2. Mutation

   Mutation用于变更Store中的数据

   + 只能通过mutation变更Store数据，不可以直接操作Store中的数据

   + 通过这种方式虽然操作起来稍微繁琐一些，但是可以集中监控所有数据的变化

     ![image-20210421173409155](D:\vue\Vue.js.assets\image-20210421173409155.png)

     ![image-20210421173420394](D:\vue\Vue.js.assets\image-20210421173420394.png)

     ![image-20210421173435856](D:\vue\Vue.js.assets\image-20210421173435856.png)

3. Action

   Action用于处理异步任务

   如果通过异步操作变更数据，必须通过Action，而不能使用Mutation，但是在Action中还是要通过触发Mutation的方式间接变更数据。

   ![image-20210421173656604](D:\vue\Vue.js.assets\image-20210421173656604.png)

   ![image-20210421173718348](D:\vue\Vue.js.assets\image-20210421173718348.png)

   ![image-20210421173730540](D:\vue\Vue.js.assets\image-20210421173730540.png)

4. Getter

   ![image-20210421173747420](D:\vue\Vue.js.assets\image-20210421173747420.png)

   ![image-20210421173758243](D:\vue\Vue.js.assets\image-20210421173758243.png)

## 8.Vue补充

1. 在事件定义时，写方法时省略了小括号，但是方法本身是需要一个参数的，这个时候Vue会默认将浏览器生成的event事件对象作为参数传入到方法

   ```
   <button @click="btnClick"></button>
   ....
   methods:{
   	btnClick(e){
   		console.log(e);//MouseEvent
   	}
   }
   ```

   在方法定义时，我们需要event对象，同时又需要其他参数时

   ```
   <button @click="btnClick('abc', $event)"></button>
   ....
   methods:{
   	btnClick(str, event){
   		console.log('------',str,event);//-------abc,MouseEvent
   	}
   }
   ```

2. v-if:当条件为false时，包含v-if指令的元素不会存在在dom中 

   v-show：当条件为false时，只是给当前的元素添加一个行内样式：display：none

3. v-for:

   1. 遍历数组

   ![image-20210424192533954](D:\vue\Vue.js.assets\image-20210424192533954.png)

   2. 遍历对象

   ![image-20210424192439978](D:\vue\Vue.js.assets\image-20210424192439978.png)

4. 

