---
layout: post
title: lexical scope
---
### 今天刷了几个题蛮有意思的，分享一下。
* 第一题

```javascript
var foo = 1;
function bar() {
  	foo = 10;
	return;
	function foo() {}
}
bar(); 
alert(foo); //1
```
* 第二题

```javascript
var x = 3;
var foo = {
    x: 2,
    baz: {
        x: 1,
        bar: function() {
            return this.x;
        }
    }
}

var go = foo.baz.bar;

alert(go()); //3
alert(foo.baz.bar()); //1
```
* 第三题

```javascript
var x   = 4,
    obj = {
        x: 3,
        bar: function() {
            var x = 2;
            setTimeout(function() {
                var x = 1;
                alert(this.x);
            }, 1000);
        }
    };
obj.bar(); //4
```
* 第四题

```javascript
var arr = [];
arr[0]  = 'a';
arr[1]  = 'b';
arr.foo = 'c';
alert(arr.length); //2
```
* 第五题

```javascript
function foo(a) {
    arguments[0] = 2;
    alert(a);
}
foo(1); //2
```
