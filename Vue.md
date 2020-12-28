# **Vue**

## day 01

### 1.  Vue的生命周期

### 2. 插值操作

1. Mustache
   + mustache语法中不仅仅可以直接写变量，也可以写简单的表达式。
   + mustache语法放入content中，不能作为标签的属性值。
2. v-once
   + 该指令后面不需要跟任何表达式。
   + 该指令表示元素和组件只渲染一次，不会随着数据的改变而改变。
3. v-html
   1. 该指令后面往往会跟一个string类型。
   2. 会将string的html解析出来并且进行渲染。
4. v-text
   1. 与mustache相似：都是用于数据显示在界面中。
   2. 通常接受一个string类型。
5. v-pre
   1. 用于跳过这个元素和它子元素的编译过程，用于显示原本的Mustache语法。
6. v-cloak
   1. 防止渲染时js卡住让mustache给用户看到。

### 3.绑定属性

1. v-bind

   1. 除了内容需要动态来决定外，某些属性我们也希望动态来绑定。

      + 比如动态绑定a元素的href属性。
      + 比如动态绑定img元素的src属性

   2. v-bind指令

      + 作用：动态绑定属性。

      + 缩写：：

      + 预期：any（with argument）| Object（without argument）

      + 参数：attrOrProp（optional）

      + 
      
      + ```javascript
      <a v-bind:href="ahref">百度一下</a>
                                  ......
        
                                data：{
                          ahref：“www.baidu.com”
                                }
        ```
        
      

