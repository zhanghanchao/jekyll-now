---
layout: post
title: selenium验证码识别
---
### selenium 验证码识别功能。

### 在我们做登录注册自动化时，验证码一直是许多人比较头疼的一块，找不到好的解决办法。放狗搜有以下三种方式。
### 1,webdriver + ruokuai的方式,这种方法是我推荐的做法，因为验证码识别正确率很高。这是ruokuai的开发者文档：http://wiki.ruokuai.com/, 下面贴代码:

```java
package com.kanjian.selenium;
import org.testng.annotations.Test;
import com.google.gson.JsonObject;
import com.google.gson.JsonParser;
import org.testng.annotations.BeforeMethod;
import java.awt.image.BufferedImage;
import java.io.File;
import java.io.IOException;
import javax.imageio.ImageIO;
import org.apache.commons.io.FileUtils;
import org.openqa.selenium.By;
import org.openqa.selenium.Dimension;
import org.openqa.selenium.OutputType;
import org.openqa.selenium.Point;
import org.openqa.selenium.TakesScreenshot;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.chrome.ChromeDriver;
import org.testng.annotations.AfterMethod;

public class CopyrightCodeLoginTest {
	
	WebDriver driver;
	String baseUrl = "http://copyright.default.kanjian.com";
	
	@BeforeMethod
	public void beforeMethod() {
		System.setProperty("webdriver.chrome.driver", "D:\\selenium tools\\chromedriver_win32\\chromedriver.exe");
		driver = new ChromeDriver();
	}

	@Test
	public void CopyrightLoginTest() throws IOException, InterruptedException {
		driver.get(baseUrl);
		driver.manage().window().maximize();
		Thread.sleep(500);
		driver.findElement(By.cssSelector(".top-bar__no-logining--button")).click();
		driver.findElement(By.cssSelector(".signup__to-up")).click();
		driver.findElement(By.cssSelector(".login__email")).sendKeys("copyright@kanjian.com");
		driver.findElement(By.cssSelector(".login__password")).sendKeys("123456");
		Thread.sleep(3000);
		File screenshot = ((TakesScreenshot)driver).getScreenshotAs(OutputType.FILE);
//保存截取的页面图片。

		FileUtils.copyFile(screenshot, new File("D:\\seleniumpic\\screen.jpg"));


		WebElement captcha = driver.findElement(By.cssSelector(".login__captcha--button"));
		Point location = captcha.getLocation();
		Dimension size = captcha.getSize();
		BufferedImage originalImage = ImageIO.read(screenshot);

//截取二维码图片

		BufferedImage captchadest = originalImage.getSubimage(
		location.getX(),
		location.getY(),
		size.getWidth(),
		size.getHeight());

		ImageIO.write(captchadest, "png", screenshot);
		Thread.sleep(1000);
		File captchadestImage = new File("D:\\seleniumpic\\captcha.png");

		FileUtils.copyFile(screenshot, captchadestImage);
		Thread.sleep(1000);

//调用ruokuai接口

		String captcharesult="";
		String result = RuoKuai.createByPost("用户名", "密码", "2040", "10", "79555", 
			"5ca9e6fe4d9e40169af307ebbe5b68ef", "D:\\seleniumpic\\captcha.png");  
//		System.out.println(result);

//解析json.

		JsonParser jp = new JsonParser();
		JsonObject jo = jp.parse(result).getAsJsonObject();
		if(jo.has("Result")) {
		  captcharesult = jo.get("Result").getAsString();
		  System.out.println(captcharesult);
		}else {
		  System.out.println("has wrong");
		}

		Thread.sleep(1000);
		driver.findElement(By.cssSelector(".login__captcha")).sendKeys(captcharesult);
		driver.findElement(By.cssSelector(".login__action--button")).click();
	}

	
	@AfterMethod
	public void afterMethod() {
		driver.quit();
	}
}
```
### 2,通过塞入cookie方式;这种方式还是可行的，绕过登录页面，直接进入到想要的测试页面。但是这种方式是有局限性的，比如在用户注册过程中，我们就无法使用这种方式。

下面是代码部分:

```java
package com.kanjian.selenium;
import org.testng.annotations.Test;
import java.util.Set;
import org.testng.annotations.BeforeMethod;
import org.openqa.selenium.Cookie;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;
import org.testng.annotations.AfterMethod;

public class CopyrightLoginTest {
	
	WebDriver driver;
	String baseUrl = "http://copyright.default.kanjian.com";

	@BeforeMethod
	public void beforeMethod() {
	  
		System.setProperty("webdriver.chrome.driver", "D:\\selenium tools\\chromedriver_win32\\chromedriver.exe");
		driver = new ChromeDriver();
	}
	@Test
	public void TestLogin() {
		driver.get(baseUrl);
		driver.manage().window().maximize();

//实现添加cookie绕过验证码登录功能。

		Cookie ck1 = new Cookie("sid", "ZmZhYjQyYmZiNTNiNGVhYmIxMGRkNGYxNzVlOGYzZGY=|1492048768|3d4304c2118657588927641e9020ff790e7873e0");
		Cookie ck2 = new Cookie("copyright_sid", "2|1:0|10:1492067293|13:copyright_sid|44:MjlkMzVhYjUzODljNDNmZDliOGFmNjI1OTU4MDJlYTQ=|6503fae4d16e35cc4567f4ac1f7e11a0a69e9a5d937d88205e7af2dbea8d9963");
		driver.manage().addCookie(ck1);
		driver.manage().addCookie(ck2);
		driver.get(baseUrl);
		
		try {
		Thread.sleep(2000);
		} catch (InterruptedException e) {
		
		e.printStackTrace();
		}
		Set<Cookie> cookies = driver.manage().getCookies();

    	System.out.println(String.format("Domain -> name -> value -> expiry -> path"));

		for (Cookie c : cookies)

    		System.out.println(String.format("%s -> %s -> %s -> %s -> %s", 
    		c.getDomain(), c.getName(), c.getValue(), c.getExpiry(), c.getPath()));
	}
	@AfterMethod
	public void afterMethod() {
		driver.quit();
	}

}
```
## 3，tesseract ORC

### 个人不推荐，因为识别错误率太高了。
