1. **Please verify that the package.json has a valid "main" entry**  重新下载包 或者删除package-lock.json文件并重新执行npm install命令

   [解决]: https://stackoverflow.com/questions/66207737/please-verify-that-the-package-json-has-a-valid-main-entry

   

2. **net::ERR_CONNECTION_REFUSED** 

   + 没有运行服务器
   + 代码错误

3. let与const都是块级作用域

   ```js
   (function a(){
       const a = 10;
   })();
   (function b(){
       const a = 20;
   })();
   
   //控制台输出10，20.说明两个块级作用域内用const定义互不影响。
   ```

4. 子页面调父页面的函数

   ```js
   window.parent.function()
   ```

5. jquery为input赋值

   ```js
   $('input[name="input中name属性值"]').val(想要赋的值)
   ```

6. layui表单赋值

   ```js
   //给表单赋值
   form.val("formTest", { //formTest 即 class="layui-form" 所在元素属性 lay-filter="" 对应的值
     "username": "贤心" // "name": "value"
     ,"sex": "女"
     ,"auth": 3
     ,"check[write]": true
     ,"open": false
     ,"desc": "我爱layui"
   });
    
   //获取表单区域所有值
   var data1 = form.val("formTest");
   ```

7. ajax请求体的名称要一致。报错...is required就是名称不一致

8. 代理事件的绑定

   ![image-20210404184716228](D:\vue\node报错.assets\image-20210404184716228.png)