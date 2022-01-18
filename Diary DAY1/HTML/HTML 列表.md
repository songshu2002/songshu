## HTML无序列表

无序列表是一个项目的列表，此列项目使用粗体圆点（典型的小黑圆圈）进行标记。

无序列表使用` <ul>` 标签

```html
`<ul>
<li>Coffee</li>
<li>Milk</li>
</ul>`
```

浏览器显示如下：

- Coffee

- Milk

  +++

  ## HTML 有序列表

  同样，有序列表也是一列项目，列表项目使用数字进行标记。 有序列表始于 `<ol>` 标签。每个列表项始于` <li>`标签。

  列表项使用数字来标记。

  ```html
  `<ol>
  <li>Coffee</li>
  <li>Milk</li>
  </ol>`
  ```

  浏览器中显示如下：

  1. Coffee

  2. Milk

     +++

     ## HTML 自定义列表

     自定义列表不仅仅是一列项目，而是项目及其注释的组合。

     自定义列表以 `<dl>` 标签开始。每个自定义列表项以 `<dt>` 开始。每个自定义列表项的描述以 `<dd> `开始。
  
     ```html
     `<dl>
     <dt>Coffee</dt>
     <dd>- black hot drink</dd>
     <dt>Milk</dt>
     <dd>- white cold drink</dd>
     </dl>`
     ```
  
     浏览器显示如下：
     
     - Coffee
       - black hot drink
     - Milk
       - white cold drink

**提示:** 列表项内部可以使用段落、换行符、图片、链接以及其他列表等等。

## 更多实例

[不同类型的有序列表](https://www.runoob.com/try/try.php?filename=tryhtml_lists_ordered)
本例演示不同类型的有序列表。

[不同类型的无序列表](https://www.runoob.com/try/try.php?filename=tryhtml_lists_unordered)
本例演示不同类型的无序列表。

[嵌套列表](https://www.runoob.com/try/try.php?filename=tryhtml_lists2)
本例演示如何嵌套列表。

[嵌套列表 2](https://www.runoob.com/try/try.php?filename=tryhtml_nestedlists2)
本例演示更复杂的嵌套列表。

[自定义列表](https://www.runoob.com/try/try.php?filename=tryhtml_lists3)
本例演示一个定义列表。