## frame - 设置高度与宽度

height 和 width 属性用来定义iframe标签的高度与宽度。

属性默认以像素为单位, 但是你可以指定其按比例显示 (如："80%")。

## 实例

```html
`<iframe loading="lazy" src="demo_iframe.htm" width="200" height="200"></iframe>`
```


[尝试一下 »](https://www.runoob.com/try/try.php?filename=tryhtml_iframe_height_width)



------

## iframe - 移除边框

frameborder 属性用于定义iframe表示是否显示边框。

设置属性值为 "0" 移除iframe的边框:

## 实例

```html
`<iframe src="demo_iframe.htm" frameborder="0"></iframe>`
```


[尝试一下 »](https://www.runoob.com/try/try.php?filename=tryhtml_iframe_frameborder)



------

## 使用 iframe 来显示目标链接页面

iframe 可以显示一个目标链接的页面

目标链接的属性必须使用 iframe 的属性，如下实例:

## 实例

```html
<iframe src="demo_iframe.htm" name="iframe_a"></iframe>`

` <p><a href="https://www.runoob.com" target="iframe_a" rel="noopener">RUNOOB.COM</a></p>
```


[尝试一下 »](https://www.runoob.com/try/try.php?filename=tryhtml_iframe_target)