---
layout: default
title: mediaqueries
category: CSS
---

#学习media query

##背景

让页面在不同的使用情景下应用不同的css在 HTML4 CSS2 时就已支持,比如，在屏幕查看和打印采用不同的样式表：

    <link rel="stylesheet" type="text/css" media="screen" href="sans-serif.css">
    <link rel="stylesheet" type="text/css" media="print" href="serif.css">

在css文件内，可按如下区分：

    @media screen {
      * { font-family: sans-serif }
    }

在HTML4中可支持的全部媒体类型有
- `<del>aural</del>`, 被speech取代
- `braille`, 用于盲文触觉反馈设备
- `handheld`, 手持设备（小屏，有限带宽）
- `print`, 用于分页材料，或在文档的打印预览模式
- `projection`, 用于投影的汇报
- `screen`, 主要用于彩色电脑屏幕
- `tty`, 用于 fixed-pitch character grid，tty中不支持像素单位px
- `tv`，用于电视设备（低分辨率，彩色，屏幕限制滚动，有声）。
CSS2里支持的类型列表略有不同，除去了`aural`, 并增加了 `embossed:盲文打印` 和 `speech：语音合成`, 另外`all`表示该样式表适用于所有的媒体。

HTML5引入了Media Queries规范。

***

##Media Queries

媒体查询是一个逻辑表达式，当用户代理运行的设备能匹配媒体查询的媒体类型时为真。

媒体查询拥有速记语法，介绍关键字如下：

`all`：可用来表示所有未被明确指出的类型。`@media all and (min-width:500px) { … }`是完全等同于`@media (min-width:500px) { … }`的。  

`and`：逻辑与  

`,`：逻辑或，当用逗号分隔开的媒体查询列表中只要有一项匹配，则采用样式。如`@media screen and (color), projection and (color) { … }`  

`not`：逻辑非  

`only`：The keyword ‘only’ can also be used to hide style sheets from older user agents. User agents must process media queries starting with ‘only’ as if the ‘only’ keyword was not present.

NOTE：用户代理被期望能重新评估和布局页面来响应用户环境的变化,例如设备从横向模式倾斜至纵向模式，但并非必须的。

***

##语法

***

##特性

媒体特性与一般的css属性类似，但略有不同：
- css属性用于声明文档的呈现，而媒体特性用于描述输出设备的要求。
- 绝大多数的媒体特性接受可选的 `min-` 与 `max-` 前缀。
- css属性总是需要一个值来形成声明，而媒体特性，可以不需要值。
- css属性接受复杂的赋值方式，如 `calc()`表达式， 而媒体属性只简单的值。

### width

适用于：视觉与触觉媒体类型  
min/max前缀可用

### height

适用于：视觉与触觉媒体类型  
min/max前缀可用

    <link rel="stylesheet" media="print and (min-width: 25cm)" href="http://…" />

    @media screen and (min-width: 400px) and (max-width: 700px) { … }

###device-width

适用于：视觉与触觉媒体类型  
min/max前缀可用  
描述输出设备的显示区域宽度；若为连续媒体，表示屏幕宽度，若为分页媒体，表示页表宽度。

###device-height

适用于：视觉与触觉媒体类型  
min/max前缀可用  
描述输出设备的显示区域高度；若为连续媒体，表示屏幕高度，若为分页媒体，表示页表高度。

    @media screen and (device-width: 800px) { … }
    <link rel="stylesheet" media="screen and (device-height: 600px)" />

###orientation

value: portrait (竖屏模式)| landscape (横屏模式)  
适用于位图媒体形式   
min/max前缀不适用  

    @media all and (orientation:portrait) { … }
    @media all and (orientation:landscape) { … }

###aspect-ratio

适用于位图媒体形式  
min/max前缀可用  
定义为'height'与'width'的比率

###device-aspect-ratio

适用于位图媒体形式  
min/max前缀可用  
定义为'device-height'与'device-width'的比率

###color

适用于视觉媒体形式  
min/max前缀可用  
描述输出设备每色彩分量所用的比特数，若设备不是'color device'，则为0。

###color-index

适用于视觉媒体形式  
min/max前缀可用  
描述输出设备颜色查找表的条目数，若设备不采用颜色查找表，则为0。

###monochrome

适用于视觉媒体形式
min/max前缀可用
描述单色帧缓冲中每像素所用比特数，若设备不是单色设备，则为0。

    @media all and (monochrome) { … }
    @media all and (min-monochrome: 1) { … }

    <!-- 打印时彩色设备与单色设备分别采用不同样式表 -->
    <link rel="stylesheet" media="print and (color)" href="http://…" />
    <link rel="stylesheet" media="print and (monochrome)" href="http://…" />

###resolution

适用于位图媒体形式  
min/max前缀可用  
描述输出设备的精度，如像素的密度。当查询设备为非方形像素时，'max-resolution'将与密度最大的维度相比，'min-resolution'将与密度最小的维度比较，而'resolution'匹配不了非方形像素的设备。

    <!-- resolution的单位为dpi或dpcm -->
    @media print and (min-resolution: 300dpi) { … }
    @media print and (min-resolution: 118dpcm) { … }

###scan

value: progressive | interlace  
适用于'tv' 媒体类型  
不支持min/max前缀

###grid

适用于视觉与触觉媒体类型  
不支持min/max前缀  
用来查询输出设备基于位图还是基于网格；若基于网格，则为1，若基于位图，则为0。

***

#参考

[media query文档](http://www.w3.org/TR/css3-mediaqueries/)
