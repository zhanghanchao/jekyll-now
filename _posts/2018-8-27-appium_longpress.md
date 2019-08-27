---
layout: post
title: appium longPress
---

## appium长按操作方法的实现

```java
  public void longPress(WebElement element) {
        TouchAction action = new TouchAction(driver);
        int x = element.getLocation().getX();
        int y = element.getLocation().getY();
        action.longPress(PointOption.point(x,y)).release().perform();
    }
```
