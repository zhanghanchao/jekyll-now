---
layout: post
title: CSS三种基本的布局模型
---
## CSS包含3种基本的布局模型，用英文概括为：Flow、Layer 和 Float。

## 在网页中，元素有三种布局模型：

* 1、流动模型（Flow）
* 2、浮动模型 (Float)
* 3、层模型（Layer）

## 层模型有三种形式：
* If the element has 'position: absolute', the containing block is established bythe nearest ancestor with a 'position' of 'absolute', 'relative' or 'fixed', in the following way:
* In the case that the ancestor is an inline element, the containing block is the bounding box around the padding boxes of the first and the last inline boxes generated for that element. In CSS 2.1, if the inline element is split across multiple lines, the containing block is undefined.
* Otherwise, the containing block is formed by the padding edge of the ancestor.If there is no such ancestor, the containing block is the initial containing block.

## 1、绝对定位(position: absolute)

 如果想为元素设置层模型中的绝对定位，需要设置position:absolute(表示绝对定位)，这条语句的作用将元素从

文档流中拖出来，然后使用left、right、top、bottom属性相对于其最接近的一个具有定位属性的父包含块进行绝对

定位。如果不存在这样的包含块，则相对于body元素，即相对于浏览器窗口.

## 2、相对定位(position: relative)

 如果想为元素设置层模型中的相对定位，需要设置position:relative（表示相对定位），它通过left、right、

top、bottom属性确定元素在正常文档流中的偏移位置。相对定位完成的过程是首先按static(float)方式生成一个元

素(并且元素像层一样浮动了起来)，然后相对于以前的位置移动，移动的方向和幅度由left、right、top、bottom属

性确定，偏移前的位置保留不动。

## 3、固定定位(position: fixed)

fixed：表示固定定位，与absolute定位类型类似，但它的相对移动的坐标是视图（屏幕内的网页窗口）本身。由于视

图本身是固定的，它不会随浏览器窗口的滚动条滚动而变化，除非你在屏幕中移动浏览器窗口的屏幕位置，或改变浏

览器窗口的显示大小，因此固定定位的元素会始终位于浏览器窗口内视图的某个位置，不会受文档流动影响，这与

background-attachment:fixed;属性功能相同。以下代码可以实现相对于浏览器视图向右移动100px，向下移动50px

。并且拖动滚动条时位置固定不变。

## Relative与Absolute组合使用

1、参照定位的元素必须是相对定位元素的前辈元素：
2、参照定位的元素必须加入position:relative;
3、定位元素加入position:absolute，便可以使用top、bottom、left、right来进行偏移定位了。
