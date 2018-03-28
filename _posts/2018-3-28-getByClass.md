---
layout: post
title: 封装getElementsByClassName!
---
### 由于getElementsByClassName在IE上支持不好，所以我们需要封装一个函数来解决。

```javascript
function getByClass(obj, cls){
	var result = [],
	    oEles = obj.getElementsByTagName("*");
	for (var i = 0; i < oEles.length; i++){
        if(oEles[i].className == cls){
            result.push(oEles[i]);
        }
	}
	return result;
}
```
