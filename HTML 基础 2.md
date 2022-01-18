## HTML 标题

HTML 标题（Heading）是通过`<h1> - <h6> `标签来定义的。

## 实例

`<h1>这是一个标题</h1>` 
`<h2>这是一个标题</h2>`
`<h3>这是一个标题</h3>`

`<hr>`

hr 元素可用于分隔内容。

`<!-- 这是一个注释 -->`

浏览器会忽略注释，也不会显示它们

`<br>`

希望在不产生一个新段落的情况下进行换行（新行），请使用 `<br>`

## HTML 提示 - 如何查看源代码

右键，然后选择"查看源文件"（IE）或"查看页面源代码"（Firefox），其他浏览器的做法也是类似的。这么做会打开一个包含页面 HTML 代码的窗口。

+++

## HTML 段落

HTML 段落是通过标签 <p> 来定义的。

## 实例

`<p>这是一个段落。</p>`
` <p>这是另外一个段落。</p>`

+++

## HTML 链接

HTML 链接是通过标签` <a>` 来定义的。

## 实例

`<a href="https://www.runoob.com">这是一个链接</a>`

## HTML 链接语法

链接的 HTML 代码很简单。它类似这样：

`<a href="url">链接文本</a>`

href 属性描述了链接的目标。.

## 实例

`<a href="https://www.runoob.com/">访问菜鸟教程</a>`

## HTML 链接 - target 属性

使用 target 属性，你可以定义被链接的文档在何处显示。

下面的这行会在新窗口打开文档：

## 实例

`<a href="https://www.runoob.com/" target="_blank" rel="noopener noreferrer">访问菜鸟教程!</a>`

## HTML 链接- id 属性

id 属性可用于创建一个 HTML 文档书签。

**提示:** 书签不会以任何特殊方式显示，即在 HTML 页面中是不显示的，所以对于读者来说是隐藏的。

## 实例

在HTML文档中插入ID:

`<a id="tips">有用的提示部分</a>`

在HTML文档中创建一个链接到"有用的提示部分(id="tips"）"：

`<a href="#tips">访问有用的提示部分</a>`

或者，从另一个页面创建一个链接到"有用的提示部分(id="tips"）"：

`<a href="https://www.runoob.com/html/html-links.html#tips">访问有用的提示部分</a>`

+++

## HTML 图像

HTML 图像是通过标签 <img> 来定义的.

## 实例

`<img loading="lazy" src="/images/logo.png" width="258" height="39" />`
