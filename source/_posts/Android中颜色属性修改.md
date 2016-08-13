---
title: Android中颜色属性修改
tags:
  - Android
  - Color
date: 2016-08-13 12:31:21
categories:
	- Android
---

颜色设置有这样几种方式

1. 使用`Color`类的常量来创建或者表示一个颜色。

```
int color = Color.BLACK;
```

2. 根据ARGB或者RGB值来取值。

```
int color = Color.argb(127,255,0,255);
int color1 = Color.rgb(255,0,255);
```

3. 在xml文件中通过十六进制来设置颜色。下面的格式分别是AARRGGBB、RRGGBB、ARGB、RGB
```
<color name=”mycolor”>#7fff00ff</color>
<color name=”mycolor”>#7fff00</color>
<color name=”mycolor”>#7fff</color>
<color name=”mycolor”>#7ff</color>
```

## 代码修改颜色的**色调**、**饱和度**和**亮度**

源码中，在包`android.graphics.Color`下有`Color`类，该类中提供了很多关于颜色操作的静态方法，其中需要用到的主要有两个

> 方法1 `public static void colorToHSV(int color, float hsv[]) `

> 方法2 `public static int HSVToColor(float hsv[])`

首先看一下这两个方法的注释
方法1：

> Convert the argb color to its HSV components. hsv[0] is Hue [0 .. 360) hsv[1] is Saturation [0...1] hsv[2] is Value [0...1]

> Parameters:
color the argb color to convert. The alpha component is ignored.
hsv 3 element array which holds the resulting HSV components.

将argb颜色值用HSV形式来进行表现，数组hsv的第一个元素表示色调，取值为0~360，第二个元素表示饱和度，取值为0~1，第三个元素表示亮度，取值也是0~1。
方法2：

> Convert HSV components to an ARGB color. Alpha set to 0xFF. hsv[0] is Hue [0 .. 360) hsv[1] is Saturation [0...1] hsv[2] is Value [0...1] If hsv values are out of range, they are pinned.

> Parameters:
hsv 3 element array which holds the input HSV components.
Returns:
the resulting argb color

与上面方法的功能相反，将HSV形式的颜色转换为argb颜色值进行返回。

有关更多HSV的信息可以参考[百度百科-HSV颜色模型](http://baike.baidu.com/link?url=r1BaevhGhOhAfq0e1BBZCp8ddt5FNH89BtOWJogp0z4OuFIAtZ-kxKthWYTXimuzTQbisE9uLy_Cug662nLZEelIwme3lYw4mhnetkI76zm)。

这样就可以不需要直接对颜色值进行拆分、修改相关色值的参数了。直接调用原生方法即可对颜色的色调、饱和度、亮度进行修改。

