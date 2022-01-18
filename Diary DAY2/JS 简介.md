## 实例


[尝试一下 »](https://www.runoob.com/try/try.php?filename=tryjs_events)

## 为什么学习 JavaScript?

JavaScript 是 web 开发人员必须学习的 3 门语言中的一门：

1. **HTML** 定义了网页的内容

2. **CSS** 描述了网页的布局

3. **JavaScript** 控制了网页的行为、

   +++

   在实例页面中，可以点击 "尝试一下" 来查看 JavaScript 在线实例。

   - [JavaScript 实例](https://www.runoob.com/js/js-examples.html)

   - [JavaScript 对象实例](https://www.runoob.com/js/js-ex-objects.html)

   - [JavaScript 浏览器支持实例](https://www.runoob.com/js/js-ex-browser.html)

   - [JavaScript HTML DOM 实例](https://www.runoob.com/js/js-ex-dom.html)

   - +++

   - JavaScript 是可插入 HTML 页面的编程代码。

     JavaScript 插入 HTML 页面后，可由所有的现代浏览器执行。

     +++

     ## JavaScript：直接写入 HTML 输出流

     ## 实例

     ```javascript
     document.write("<h1>这是一个标题</h1>"); 
     
     document.write("<p>这是一个段落。</p>");
     ```


     [尝试一下 »](https://www.runoob.com/try/try.php?filename=tryjs_intro_document_write)

     

     | ![lamp](https://www.runoob.com/images/lamp.jpg) | 您只能在 HTML 输出中使用 document.write。如果您在文档加载后使用该方法，会覆盖整个文档。 |
     | ----------------------------------------------- | ------------------------------------------------------------ |
     |                                                 |                                                              |

     

     ------

     ## JavaScript：对事件的反应

     ## 实例

     ```javascript
     <button type="button" onclick="alert('欢迎!')">点我!</button>
     
     
     ```

     [尝试一下 »](https://www.runoob.com/try/try.php?filename=tryjs_intro_alert)

     alert() 函数在 JavaScript 中并不常用，但它对于代码测试非常方便。

     

     onclick 事件只是您即将在本教程中学到的众多事件之一。

     ------

     ## JavaScript：改变 HTML 内容

     使用 JavaScript 来处理 HTML 内容是非常强大的功能。

     ## 实例

     ```javascript
     x=document.getElementById("demo");  //查找元素
     
      x.innerHTML="Hello JavaScript";    //改变内容
     ```

     
     [尝试一下 »](https://www.runoob.com/try/try.php?filename=tryjs_intro_inner_html)

     您会经常看到 **document.getElementById("*****some id*****")**。这个方法是 HTML DOM 中定义的。

     DOM (**D**ocument **O**bject **M**odel)（文档对象模型）是用于访问 HTML 元素的正式 W3C 标准。

     您将在本教程的多个章节中学到有关 HTML DOM 的知识。

     ------

     ## JavaScript：改变 HTML 图像

     本例会动态地改变 HTML <image> 的来源（src）：

     ## 点亮灯泡

     <script> function changeImage() {     element=document.getElementById('myimage')     if (element.src.match("bulbon"))     {         element.src="/images/pic_bulboff.gif";     }     else     {         element.src="/images/pic_bulbon.gif";     } } </script> <img loading="lazy" id="myimage" onclick="changeImage()" src="/images/pic_bulboff.gif" width="100" height="180">

     ```javascript
     <script>
     function changeImage()
     {
         element=document.getElementById('myimage')
         if (element.src.match("bulbon"))
         {
             element.src="/images/pic_bulboff.gif";
         }
         else
         {
             element.src="/images/pic_bulbon.gif";
         }
     }
     </script>
     <img loading="lazy" id="myimage" onclick="changeImage()" src="/images/pic_bulboff.gif" width="100" height="180">
     ```

     点击以下灯泡查看效果：

     ![img](https://www.runoob.com/images/pic_bulboff.gif)

     点击灯泡就可以打开或关闭这盏灯

     
     [尝试一下 »](https://www.runoob.com/try/try.php?filename=tryjs_lightbulb)

     > 以上实例中代码 **element.src.match("bulbon")** 的作用意思是：检索 **<img id="myimage" onclick="changeImage()" src="/images/pic_bulboff.gif" width="100" height="180">** 里面 src 属性的值有没有包含 **bulbon** 这个字符串，如果存在字符串 **bulbon**，图片 **src** 更新为 **bulboff.gif**，若匹配不到 **bulbon** 字符串，**src** 则更新为 **bulbon.gif**

     JavaScript 能够改变任意 HTML 元素的大多数属性，而不仅仅是图片。

     ------

     ## JavaScript：改变 HTML 样式

     改变 HTML 元素的样式，属于改变 HTML 属性的变种。

     ## 实例

     ```javascript
     x=document.getElementById("demo") //找到元素 
     x.style.color="#ff0000";           //改变样式
     ```


     [尝试一下 »](https://www.runoob.com/try/try.php?filename=tryjs_intro_style)

     

     ------

     ## JavaScript：验证输入

     JavaScript 常用于验证用户的输入。

     ## 实例

     ```javascript
     if isNaN(x) {  
         alert("不是数字"); 
     }
     ```

     
     [尝试一下 »](https://www.runoob.com/try/try.php?filename=tryjs_intro_validate)

     以上实例只是普通的验证，如果要在生产环境中使用，需要严格判断，如果输入的空格，或者连续空格 isNaN 是判别不出来的。可以添加正则来判断（后续章节会说明）：

     ## 实例

     ```javascript
     if(isNaN(x)||x.replace(/(^\s*)|(\s*$)/g,"")==""){  
         alert("不是数字"); 
     }
     
     
     
     ```


     [尝试一下 »](https://www.runoob.com/try/try.php?filename=tryjs_intro_validate2)