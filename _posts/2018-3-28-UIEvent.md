---
layout: post
title: ui event
---
### 13.4.1 UI事件

load事件：最常用的一个事件，当页面加载完成后(包括所有image、javascript文件、CSS文件等外部资源)，就会触发windows上面的load事件。

第一种定义onload事件处理程序的方式：
```javascript
EventUtil.addHandler(window, "load", function(event) {
    alert("loaded!");
});
```
第二种方式是：

```html
<body onload="alert('loaded!')"></body>
```
但是尽可能的使用javascript方式。根据"DOM2级事件"规范，应该在document而非window上面触发load事件。但是，所有路南器都在window上面实现了该事件，以确保向后兼容。

图像上面也可以触发load事件，例如：

```html
<img src="smile.gif" onload="alert('Image loaded.')">
```
也可以使用javascript来实现，例如：

```javascript
var image = document.getElementById("myImage");
EventUtil.addHandler(image, "load", function(event) {
    event = EventUtil.getEvent(event);
    alert(EventUtil.getTarget(event).src);
});
```
在创建新的<img>元素时，可以为其制定一个事件处理程序，以便图像加载完毕后给出提示。此时，最重要的是要在制定src属性之前先指定事件，例子：

```javascript
//首先为window指定了onload事件处理程序，因为要添加一个新元素，必须确定页面已经加载完毕---在页面加载前操作document.body会导致错误。
EventUtil.addHandler(window, "load", function() {  
    var image = document.createElement("img");
    EventUtil.addHandler(image, "load", function(event) {
        event = EventUtil.getEvent(event);
        alert(EventUtil.getTarget(event).src);
    });
    document.body.appendChild(image);
    image.src = "smile.gif";
});
```

在DOM出现之前，开发人员经常使用Image对象在客户端预先加载图像。可以像使用<img>元素一样使用Image对象，只不过无法添加到DOM树中。例子：

```javascript
EventUtil.addHandler(window, "load" , function() {
    var image = new Image();    //使用Image构造函数创建了一个新图像的实例
    EventUtil.addHandler(image, "load", function(event) {
        alert("Image loaded!");
    });
    image.src = "smile.gif";
});
```
在IE9+、Firefox、Opera、Chrome 和Safari 3+及更高版本中,<script>元素也会触发load事件，以便开发人员确定动态加载的JavaScript文件是否加载完毕。

```javascript
EventUtil.addHandler(window, "load", function(){
    var script = document.createElement("script");
    EventUtil.addHandler(script, "load", function(event){
        alert("Loaded");
    });
    script.src = "example.js";
    document.body.appendChild(script);
});
```
IE和Opera 还支持<link>元素上的load事件，以便开发人员确定样式表是否加载完毕。例如：

```javascript
EventUtil.addHandler(window, "load", function(){
    var link = document.createElement("link");
    link.type = "text/css";
    link.rel= "stylesheet";

    EventUtil.addHandler(link, "load", function(event){
        alert("css loaded");
    });
    link.href = "example.css";
    document.getElementsByTagName("head")[0].appendChild(link);
});
```
