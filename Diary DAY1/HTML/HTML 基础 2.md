## HTML 表格

表格由 <table> 标签来定义。每个表格均有若干行（由 <tr> 标签定义），每行被分割为若干单元格（由 <td> 标签定义）。字母 td 指表格数据（table data），即数据单元格的内容。数据单元格可以包含文本、图片、列表、段落、表单、水平线、表格等等。

## 表格实例

## 实例

`<table border="1"> `

​    `<tr>      `

   `<td>row 1, cell 1</td>  `   

   ` <td>row 1, cell 2</td>`  

   `</tr>   `

  `<tr>   ` 

​    ` <td>row 2, cell 1</td>  `  

​    ` <td>row 2, cell 2</td>  `

   `</tr> `

`</table>`

在浏览器显示如下：:

![img](https://www.runoob.com/wp-content/uploads/2013/07/4AEE0F4B-669C-4BBC-BEC4-6953E1B0E278.jpg)

+++

表格的表头使用 `<th> `标签进行定义。

大多数浏览器会把表头显示为粗体居中的文本：

## 实例

`<table border="1">  
    <tr>  
        <th>Header 1</th>   
        <th>Header 2</th>  
    </tr>  
    <tr>     
        <td>row 1, cell 1</td>  
        <td>row 1, cell 2</td>   
    </tr>
    </table>`

在浏览器显示如下：

![img](https://www.runoob.com/wp-content/uploads/2013/07/CB476DA7-7279-4892-A424-657772E385BA.jpg)

+++

+++

[没有边框的表格](https://www.runoob.com/try/try.php?filename=tryhtml_tables3)
本例演示一个没有边框的表格。

[表格中的表头(Heading)](https://www.runoob.com/try/try.php?filename=tryhtml_table_headers)
本例演示如何显示表格表头。

[带有标题的表格](https://www.runoob.com/try/try.php?filename=tryhtml_tables2)
本例演示一个带标题 (caption) 的表格

[跨行或跨列的表格单元格](https://www.runoob.com/try/try.php?filename=tryhtml_table_span)
本例演示如何定义跨行或跨列的表格单元格。

[表格内的标签](https://www.runoob.com/try/try.php?filename=tryhtml_table_elements)
本例演示如何在不同的元素内显示元素。

[单元格边距(Cell padding)](https://www.runoob.com/try/try.php?filename=tryhtml_table_cellpadding)
本例演示如何使用 Cell padding 来创建单元格内容与其边框之间的空白。

[单元格间距(Cell spacing)](https://www.runoob.com/try/try.php?filename=tryhtml_table_cellspacing)
本例演示如何使用 Cell spacing 增加单元格之间的距离。

[漂亮的表格](https://c.runoob.com/codedemo/3187)

## 

<caption> 标题

<colgroup>格列的组

<col>列属性

<thead>页眉

<tbody>主体

<tfoot>页脚