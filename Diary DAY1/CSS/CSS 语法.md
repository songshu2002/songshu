# CSS 语法

------

## 实例

- 查看 [实例 1](https://www.runoob.com/try/try.php?filename=ex1)
- 查看 [实例 2](https://www.runoob.com/try/try.php?filename=ex2)

------

## CSS 实例

CSS 规则由两个主要的部分构成：选择器，以及一条或多条声明:

![img](https://www.runoob.com/wp-content/uploads/2013/07/632877C9-2462-41D6-BD0E-F7317E4C42AC.jpg)

选择器通常是您需要改变样式的 HTML 元素。

每条声明由一个属性和一个值组成。

属性（property）是您希望设置的样式属性（style attribute）。每个属性有一个值。属性和值被冒号分开。

------

## CSS 实例

CSS声明总是以分号(;)结束，声明总以大括号({})括起来:

```css
p {color:red;text-align:center;}
```

为了让CSS可读性更强，你可以每行只描述一个属性:

## 实例

```css
`p {    color:red;    text-align:center; }`
```


[尝试一下 »](https://www.runoob.com/try/try.php?filename=trycss_syntax1)



------

## CSS 注释

注释是用来解释你的代码，并且可以随意编辑它，浏览器会忽略它。

CSS注释以 **/\*** 开始, 以 ***/** 结束, 实例如下:

## 实例

```css
/*这是个注释*/

 p 

{    text-align:center; 

   /*这是另一个注释*/ 

   color:black;  

  font-family:arial; 

}
```

