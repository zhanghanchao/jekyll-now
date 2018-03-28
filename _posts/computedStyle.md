---
layout: post
title: computed style!
---
### DOM2计算的样式(层叠之后的最终样式)

"DOM2级样式"增强了document.defaultView,提供了getComputedStyle()方法。这个方法接受两个参数：要去的计算
样式的元素和一个伪元素字符串(例如":after")。如果不需要伪元素信息，第二个参数可以是null。例如下面的例子：

```html
<!DOCTYPE html>
<html>
<head>
    <title>Computed Styles Example</title>
    <style type="text/css">
        #myDiv {
            background-color: blue;
            width: 100px;
            height: 200px;
        }
    </style>
</head>
<body>
    <div id="myDiv" style="background-color: red; border: 1px solid black"></div>
</body>
</html>
```

下列代码可以取得元素计算后的样式：

```javascript
var myDiv = document.getElementById("myDiv");
var computedStyle = document.defaultView.getComputedStyle(myDiv, null);
alert(computedStyle.backgroundColor); // "red"
alert(computedStyle.width); // "100px"
alert(computedStyle.height); // "200px"
alert(computedStyle.border); // 在某些浏览器中是"1px solid black"
```
得到的backgroundColor是red而不是blue是因为这个样式在自身的style特性中被覆盖了。边框属性可能会也可能不会返回样式表中实际的border 规则（Opera会返回，但其他浏览器不会）。存在这个差别的原因是不同浏览器解释综合（rollup）属性（如border）的方式不同，因为设置这种属性实际上会涉及很多其他属性。在设置border时， 实际上是设置了四个边的边框宽度、颜色、样式属性（ border-left-width 、border-top-color 、border-bottom-style ，等等）。因此，即使computedStyle.border 不会在所有浏览器中都返回值，但computedStyle.borderLeftWidth 会返回值。

IE不支持getComputedStyle()方法，但它有一种类似的概念。在IE中，每个具有style属性的元素还有一个currentStyle 属性。这个属性是CSSStyleDeclaration的实例包含当前元素全部计算后的样式。取得这些样式的方式也差不多，如下面的例子所示。

```javascript
var myDiv = document.getElementById("myDiv");
var computedStyle = myDiv.currentStyle;
alert(computedStyle.backgroundColor); //"red"
alert(computedStyle.width); //"100px"
alert(computedStyle.height); //"200px"
alert(computedStyle.border); //undefined
```
我们，不能指望某个CSS 属性的默认值在不同浏览器中是相同的。如果你需要元素具有某个特定的默认值，应该手工在样式表中指定该值。
