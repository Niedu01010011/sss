## javascript

1. ### WebApi

   1. ![image-20201116164050242](C:\Users\29635\AppData\Roaming\Typora\typora-user-images\image-20201116164050242.png)

   2. document.querySelector()

      ![image-20201116164440653](C:\Users\29635\AppData\Roaming\Typora\typora-user-images\image-20201116164440653.png)

   3. document.querySelectorAll()

      

      ![image-20201116164856522](C:\Users\29635\AppData\Roaming\Typora\typora-user-images\image-20201116164856522.png)

   4. innerText和innerHTML的区别	![image-20201116180342693](C:\Users\29635\AppData\Roaming\Typora\typora-user-images\image-20201116180342693.png)

   

事件委派（利用事件的冒泡）

![image-20201116153956897](C:\Users\29635\AppData\Roaming\Typora\typora-user-images\image-20201116153956897.png)

5. 定时器
   1. window.setTimeout(调用函数，[延迟的毫秒数])
      
      1. setTimeout()方法用于设置一个定时器，该定时器到期后执行调用函数。
      
   2. setInterval（调用函数，延迟毫秒数）

      1. 可以在设置定时器之前调用一次函数，防止刚开始刷新页面有空白问题。

      2. clearInterval（setInterval的名字）停止定时器

         ![image-20201210233529625](C:\Users\29635\AppData\Roaming\Typora\typora-user-images\image-20201210233529625.png)


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
   
      