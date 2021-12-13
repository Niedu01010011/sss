# JQUERY

## 1.  JQuery基本使用

1. **jquery的入口函数**

   ```js
   // 第一种: 简单易用。
   $(function () {   
       ...  // 此处是页面 DOM 加载完成的入口
   }) ; 
   
   // 第二种: 繁琐，但是也可以实现
   $(document).ready(function(){
      ...  //  此处是页面DOM加载完成的入口
   });
   ```

   1. 等着DOM结构渲染完毕即可执行内部代码，不必等到所有外部资源加载完成，jquery帮我们完成了封装。
   2. 相当于原生js中的DOMContentLoaded。
   3. 不同于原生js中的load事件是等页面文档、外部的js文件、css文件、图片加载完毕才执行内部代码。
   4. 更推荐使用第一种方式。

2. **jquery中的顶级对象$**

   1. $是jquery的别称，在代码中可以使用jquery代替，但一般为了方便，通常都直接使用$。
   2. $是jquery的顶级对象，相当于原生js中的window。把元素利用$包装成jquery对象，就可以调用jquery的方法。

3. **jquery对象和dom对象**

   使用jquery方法和原生js获取的元素是不一样的，总结如下：

   1. 用原生js获取来的对象就是dom对象。
   2. jquery方法获取的元素就是jquery对象。
   3. jquery对象的本质是：利用$对dom对象包装后产生的对象（伪数组形式存储）。
   4. ![image-20210124211907950](C:\Users\29635\AppData\Roaming\Typora\typora-user-images\image-20210124211907950.png)

4. **jquery对象和dom对象转换**

   ​	dom对象与jquery对象之间是可以相互转换的。因为原生js比jquery更大，原生的一些属性和方法jquery没有给我们封装，要想使用这些属性方法需要把jquery对象转换成dom对象才能使用。

   ```js
   // 1.DOM对象转换成jQuery对象，方法只有一种
   var box = document.getElementById('box');  // 获取DOM对象
   var jQueryObject = $(box);  // 把DOM对象转换为 jQuery 对象
   
   // 2.jQuery 对象转换为 DOM 对象有两种方法：
   //   2.1 jQuery对象[索引值]
   var domObject1 = $('div')[0]
   
   //   2.2 jQuery对象.get(索引值)
   var domObject2 = $('div').get(0)
   ```

## 2. jquery选择器

原生js获取元素的方式很多，很杂，而且兼容性情况不一致，因此jquery给我们做了封装，使获取元素统一标准。

1. **基础选择器**

​			![image-20210124234301696](JQUERY.assets\image-20210124234301696.png)

2. **层级选择器（后代选择器和子代选择器）**

   ![image-20210124234413935](JQUERY.assets\image-20210124234413935.png)

3. **筛选选择器**

   ![image-20210124234746039](JQUERY.assets\image-20210124234746039.png)

4. **jquery中还有一些筛选方法，类似dom中的通过一个节点找另外一个节点，父、子、兄以外有所加强。**

   ![image-20210124234909944](JQUERY.assets\image-20210124234909944.png)

5. **隐式迭代**

   1. 遍历内部dom元素（伪数组形式存储）的过程就叫做隐式迭代。

   2. 简单理解：给匹配刀的所有元素进行循环遍历，执行相应的方法，而不用我们再进行循环，简化我们的操作，方便我们调用。

      ```js
      $('div').hide();//页面中所有的div全部隐藏，不用循环操作
      ```

6. **jquery的排他思想**

   ```js
   // 想要多选一的效果，排他思想：当前元素设置样式，其余的兄弟元素清除样式。
   $(this).css(“color”,”red”);
   $(this).siblings(). css(“color”,””);
   ```


## 3. jquery样式操作

jquery中常用的样式操作有两种：css（）和设置类样式方法

1. **操作css方法**

   ```js
   // 1.参数只写属性名，则是返回属性值
   var strColor = $(this).css('color');
   
   // 2.  参数是属性名，属性值，逗号分隔，是设置一组样式，属性必须加引号，值如果是数字可以不用跟单位和引号
   $(this).css(''color'', ''red'');
   
   // 3.  参数可以是对象形式，方便设置多组样式。属性名和属性值用冒号隔开， 属性可以不用加引号
   $(this).css({ 
       width: 400,
       height: 400,
       backgroundColor: 'red'
       //如果是复合属性则必须采取驼峰命名法，如果值不是数字，则需要加引号
   });
   ```

   注意：css() 多用于样式少时操作，多了则不太方便。

2. **设置类样式方法**

   作用等同于以前的classList，可以操作类样式，注意操作类里面的参数不要加点。

   常用的三种设置类样式的方法：

   ```
   //1.添加类
   $('div').addClass('current');
   //2.删除类
   $('div').removeClass('current');
   //3.切换类
   $('div').toggleClass('current');
   ```

   注意：

   1.设置类样式方法比较适合样式多时操作，可以弥补css()的不足。

   2.原生js中className会覆盖元素原先里面的类名，jquery里面类操作知识对指定类进行操作，不影响原先的类名。

## 4. Jquery效果

​	jquery给我们封装了很多动画效果，最常见的如下：

```js
1. 显示隐藏：show()/hide()/toggle();
2. 滑入滑出：slideDown()/slideUp()/slideToggle(); 
3. 淡入淡出： fadeIn()/fadeOut()/fadeToggle()/fadeTo();
4. 自定义动画： animate();
```

注意：

动画或者效果一旦触发就会执行，如果多次触发，就造成多个动画或者效果排队执行。

jQuery为我们提供另一个方法，可以停止动画排队：stop() ;

1. **显示隐藏**

   显示隐藏动画，常见有三个方法：show() / hide() / toggle() ;

   ​	语法规范如下:

   ![image-20210129164640430](JQUERY.assets\image-20210129164640430.png)

   ![image-20210129164657977](JQUERY.assets\image-20210129164657977.png)

   ![image-20210129164717509](JQUERY.assets\image-20210129164717509.png)

2. **滑入滑出**

   ![image-20210129164755425](JQUERY.assets\image-20210129164755425.png)

   ![image-20210129164836276](JQUERY.assets\image-20210129164836276.png)

3. **淡入淡出**

   ![image-20210129164923192](JQUERY.assets\image-20210129164923192.png)

   ![image-20210129164941901](JQUERY.assets\image-20210129164941901.png)

4. **自定义动画**

   ![image-20210129165004660](JQUERY.assets\image-20210129165004660.png)

```js
//代码演示
<body>
    <button>动起来</button>
    <div></div>
    <script>
        $(function() {
            $("button").click(function() {
                $("div").animate({
                    left: 500,
                    top: 300,
                    opacity: .4,
                    width: 500
                }, 500);
            })
        })
    </script>
</body>
```

5. **停止动画排队**

   动画或者效果一旦触发就会执行，如果多次触发，就造成多个动画或者效果排队执行。

   ​	停止动画排队的方法为：stop() ; 

   - stop() 方法用于停止动画或效果。
   - stop() 写到动画或者效果的前面， 相当于停止结束上一次的动画。

   ​        总结: 每次使用动画之前，先调用 stop() ,在调用动画。

6. **事件切换**

   ​	jQuery中为我们添加了一个新事件 hover() ; 功能类似 css 中的伪类 :hover 。介绍如下

   **语法**

   ```javascript
   hover([over,]out)     // 其中over和out为两个函数
   ```

   - over:鼠标移到元素上要触发的函数（相当于mouseenter）
   - out:鼠标移出元素要触发的函数（相当于mouseleave）
   - 如果只写一个函数，则鼠标经过和离开都会触发它

## 5. 今日总结

![image-20210129165334951](JQUERY.assets\image-20210129165334951.png)

## 6.jquery属性操作

​	jquery常用属性操作有三种：prop()/attr()/data();

1. **元素固有属性值prop()**

   所谓元素固有属性就是元素本身自带的属性，比如<a>元素里面的href，比如<input>元素里面的type。

   ![image-20210131101534074](JQUERY.assets\image-20210131101534074.png)

2. **元素自定义属性值attr()**

   用户自己给元素添加的属性，我们称为自定义属性。比如给div添加index=“1"。

   ![image-20210131101720494](JQUERY.assets\image-20210131101720494.png)

3. **数据缓存data()**

   data()方法可以在指定元素上存取数据，并不会修改dom元素结构。一旦页面刷新，之前存放的数据都将被移除。

   ![image-20210131101836970](JQUERY.assets\image-20210131101836970.png)

   演示代码

   ```js
   <body>
       <a href="http://www.itcast.cn" title="都挺好">都挺好</a>
       <input type="checkbox" name="" id="" checked>
       <div index="1" data-index="2">我是div</div>
       <span>123</span>
       <script>
           $(function() {
               //1. element.prop("属性名") 获取元素固有的属性值
               console.log($("a").prop("href"));
               $("a").prop("title", "我们都挺好");
               $("input").change(function() {
                   console.log($(this).prop("checked"));
               });
               // console.log($("div").prop("index"));
               // 2. 元素的自定义属性 我们通过 attr()
               console.log($("div").attr("index"));
               $("div").attr("index", 4);
               console.log($("div").attr("data-index"));
               // 3. 数据缓存 data() 这个里面的数据是存放在元素的内存里面
               $("span").data("uname", "andy");
               console.log($("span").data("uname"));
               // 这个方法获取data-index h5自定义属性 第一个 不用写data-  而且返回的是数字型
               console.log($("div").data("index"));
           })
       </script>
   </body>
   ```

## 7.jquery文本属性值

​	jquery的文本属性值常见操作有三种：html()/text()/val();分别对应js中的innerHTML、innerText和value属性。

1. **jquery内容的文本值**

   ![image-20210131105720434](JQUERY.assets\image-20210131105720434.png)

   ​	

   ```js
   //演示代码
   <body>
   	<div>
       	<span>我是内容</span>
       </div>
   	<input type="text" value="请输入内容">
       <script>
            // 1. 获取设置元素内容 html()
           console.log($("div").html());
           // $("div").html("123");
           // 2. 获取设置元素文本内容 text()
           console.log($("div").text());
           $("div").text("123");
           // 3. 获取设置表单值 val()
           console.log($("input").val());
           $("input").val("123");
       </script>
   </body>
   ```

##  8.jquery 元素操作

​	jquery元素操作主要讲的是用jquery方法，操作标签的 遍历、创建、添加、删除等操作。

1. **遍历元素**

   jquery隐式迭代是对同一类元素做了同样的操作。如果想给同一类元素做不同的操作，就需要用到遍历。

   ![image-20210131110315876](JQUERY.assets\image-20210131110315876.png)

   ```js
   //演示代码
   <body>
       <div>1</div>
       <div>2</div>
       <div>3</div>
       <script>
           $(function() {
               // 如果针对于同一类元素做不同操作，需要用到遍历元素（类似for，但是比for强大）
               var sum = 0;
               var arr = ["red", "green", "blue"];
               // 1. each() 方法遍历元素 
               $("div").each(function(i, domEle) {
                   // 回调函数第一个参数一定是索引号  可以自己指定索引号号名称
                   // console.log(i);
                   // 回调函数第二个参数一定是 dom 元素对象，也是自己命名
                   // console.log(domEle);  // 使用jQuery方法需要转换 $(domEle)
                   $(domEle).css("color", arr[i]);
                   sum += parseInt($(domEle).text());
               })
               console.log(sum);
               // 2. $.each() 方法遍历元素 主要用于遍历数据，处理数据
               // $.each($("div"), function(i, ele) {
               //     console.log(i);
               //     console.log(ele);
               // });
               // $.each(arr, function(i, ele) {
               //     console.log(i);
               //     console.log(ele);
               // })
               $.each({
                   name: "andy",
                   age: 18
               }, function(i, ele) {
                   console.log(i); // 输出的是 name age 属性名
                   console.log(ele); // 输出的是 andy  18 属性值
               })
           })
       </script>
   </body>
   ```

2. **创建，添加，删除**

   jquery方法操作元素的创建，添加，删除方法很多，则重点使用部分，如下：

   ![image-20210131111337961](JQUERY.assets\image-20210131111337961.png)

   ​	![image-20210131111354171](JQUERY.assets\image-20210131111354171.png)

   ​	

   ```js
   //案例代码
   <body>
       <ul>
           <li>原先的li</li>
       </ul>
       <div class="test">我是原先的div</div>
       <script>
           $(function() {
               // 1. 创建元素
               var li = $("<li>我是后来创建的li</li>");
         
               // 2. 添加元素
               // 	2.1 内部添加
               // $("ul").append(li);  内部添加并且放到内容的最后面 
               $("ul").prepend(li); // 内部添加并且放到内容的最前面
               //  2.2 外部添加
               var div = $("<div>我是后妈生的</div>");
               // $(".test").after(div);
               $(".test").before(div);
         
               // 3. 删除元素
               // $("ul").remove(); 可以删除匹配的元素 自杀
               // $("ul").empty(); // 可以删除匹配的元素里面的子节点 孩子
               $("ul").html(""); // 可以删除匹配的元素里面的子节点 孩子
           })
       </script>
   </body>
   ```

3. **jquery尺寸、位置操作**

   jquery中分别为我们提供了两套快速获取和设置元素尺寸和位置的api，方便易用，内容如下。

   1. **jquery尺寸操作**

      ![image-20210131113955506](JQUERY.assets\image-20210131113955506.png)

   2. **jquery位置操作**

      ![

      ```
      image-20210131114019542
      ```
      
      ](JQUERY.assets\image-20210131114019542.png)
      
      **代码演示**
      
      ```js
      <body>
          <div class="father">
              <div class="son"></div>
          </div>
              
          <div class="back">返回顶部</div>
          <div class="container"></div>
         
          <script>
              $(function() {
                  // 1. 获取设置距离文档的位置（偏移） offset
                  console.log($(".son").offset());
                  console.log($(".son").offset().top);
                  // $(".son").offset({
                  //     top: 200,
                  //     left: 200
                  // });
            
                  // 2. 获取距离带有定位父级位置（偏移） position   如果没有带有定位的父级，则以文档为准
                  // 这个方法只能获取不能设置偏移
                  console.log($(".son").position());
                  // $(".son").position({
                  //     top: 200,
                  //     left: 200
                  // });
            
            		// 3. 被卷去的头部
            		$(document).scrollTop(100);
                  // 被卷去的头部 scrollTop()  / 被卷去的左侧 scrollLeft()
                  // 页面滚动事件
                  var boxTop = $(".container").offset().top;
                  $(window).scroll(function() {
                      // console.log(11);
                      console.log($(document).scrollTop());
                      if ($(document).scrollTop() >= boxTop) {
                          $(".back").fadeIn();
                      } else {
                          $(".back").fadeOut();
                      }
                  });
                  // 返回顶部
                  $(".back").click(function() {
                      // $(document).scrollTop(0);
                      $("body, html").stop().animate({
                          scrollTop: 0
                      });
                      // $(document).stop().animate({
                      //     scrollTop: 0
                      // }); 不能是文档而是 html和body元素做动画
                  })
              })
          </script>
      </body>
      ```

9. **今日总结**

   ![image-20210201000736408](JQUERY.assets\image-20210201000736408.png)

## 9.jquery事件注册

​	jquery为我们提供了方便的事件注册机制，操作优缺点如下：

+ 优点：操作简单，且不用担心事件覆盖等问题。
+ 缺点普通的事件注册不能做事件委托，且无法实现事件解绑，需要借助其他方法。

![image-20210201001047158](JQUERY.assets\image-20210201001047158.png)

**演示代码**

```js
<body>
    <div></div>
    <script>
        $(function() {
            // 1. 单个事件注册
            $("div").click(function() {
                $(this).css("background", "purple");
            });
            $("div").mouseenter(function() {
                $(this).css("background", "skyblue");
            });
        })
    </script>
</body>
```

## 10.jquery事件处理

​	因为普通注册事件方法的不足，jquery又开发了多个处理方法，重点讲解如下：
+ on()：用于事件绑定，是目前最好用的事件绑定方法。
+ off()：事件解绑。
+ trigger()/triggerHandle():事件触发。

2. **事件处理on()绑定事件**

   因为普通注册事件方法的不足，jquery又创建了多个新的事件绑定方法bind()/live()/delegate()/on()等，

   其中最好用的是：on()

   ![image-20210201001559438](JQUERY.assets\image-20210201001559438.png)

   ![image-20210201002316273](JQUERY.assets\image-20210201002316273.png)

```js
<body>
    <div></div>
    <ul>
        <li>我们都是好孩子</li>
        <li>我们都是好孩子</li>
        <li>我们都是好孩子</li>
    </ul>
    <ol></ol>

    <script>
        $(function() {
            // (1) on可以绑定1个或者多个事件处理程序
            // $("div").on({
            //     mouseenter: function() {
            //         $(this).css("background", "skyblue");
            //     },
            //     click: function() {
            //         $(this).css("background", "purple");
            //     }
            // });
            $("div").on("mouseenter mouseleave", function() {
                $(this).toggleClass("current");
            });
  
            // (2) on可以实现事件委托（委派）
            // click 是绑定在ul 身上的，但是 触发的对象是 ul 里面的小li
            // $("ul li").click();
            $("ul").on("click", "li", function() {
                alert(11);
            });

            // (3) on可以给未来动态创建的元素绑定事件
            $("ol").on("click", "li", function() {
                alert(11);
            })
            var li = $("<li>我是后来创建的</li>");
            $("ol").append(li);
        })
    </script>
</body>

```

2. **事件处理off()解绑事件**

   ​		当某个事件上面的逻辑，在特定 需求下不需要的时候，可以把该事件上的逻辑移除，这个过程我们成为事件解绑。jquery为我们提供了多种事件解绑方法：die()/undelegate()/off()等，甚至还有只触发一次的事件绑定方法one()，在这里我们重点讲解一下off();

   ![image-20210201003343684](JQUERY.assets\image-20210201003343684.png)

   ​		**演示代码**

```js
<body>
    <div></div>
<ul>
    <li>我们都是好孩子</li>
<li>我们都是好孩子</li>
<li>我们都是好孩子</li>
</ul>
<p>我是一个P标签</p>
<script>
    $(function() {
    // 事件绑定
    $("div").on({
        click: function() {
            console.log("我点击了");
        },
        mouseover: function() {
            console.log('我鼠标经过了');
        }
    });
    $("ul").on("click", "li", function() {
        alert(11);
    });

    // 1. 事件解绑 off 
    // $("div").off();  // 这个是解除了div身上的所有事件
    $("div").off("click"); // 这个是解除了div身上的点击事件
    $("ul").off("click", "li");

    // 2. one() 但是它只能触发事件一次
    $("p").one("click", function() {
        alert(11);
    })
})
</script>
</body>
```

3. **事件处理trigger()自动触发事件**

   有些时候，在某些特定条件下，我们希望某些事件能够自动触发，比如轮播图自动播放功能跟点击右侧按钮一致。可以利用定时器自动触发右侧按钮点击事件，不必鼠标点击触发。由此jquery为我们提供了两个自动触发事件trigger()和triggerHandle();

   ![image-20210205111404339](JQUERY.assets\image-20210205111404339.png)

   演示代码

   ```js
   <body>
       <div></div>
       <input type="text">
         
       <script>
       $(function() {
         // 绑定事件
         $("div").on("click", function() {
           alert(11);
         });
   
         // 自动触发事件
         // 1. 元素.事件()
         // $("div").click();会触发元素的默认行为
         
         // 2. 元素.trigger("事件")
         // $("div").trigger("click");会触发元素的默认行为
         $("input").trigger("focus");
         
         // 3. 元素.triggerHandler("事件") 就是不会触发元素的默认行为
         $("input").on("focus", function() {
           $(this).val("你好吗");
         });
         // 一个会获取焦点，一个不会
         $("div").triggerHandler("click");
         // $("input").triggerHandler("focus");
       });
       </script>
   </body>
   ```

   