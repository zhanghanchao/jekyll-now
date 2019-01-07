---
layout: post
title: java interface
---

### java interface
## 直接看例子,Example 1
```java
/*接口也是一种引用类型，可以等同做类。
        1.如何定义接口，语法：
        修饰符 interface 接口名{}
        2.接口中只能出现常量和抽象方法；
        3.接口其实是一个特殊的抽象类，特殊在接口是完全抽象的
        4.接口中没有构造方法，接口也无法被实例化
        5.接口和接口之间可以多继承
        6.一个类可以实现多个接口（这里的实现可以等同看做“继承”）
        7.一个非抽象的类实现接口，需要将接口中所有的方法“实现/重写/覆盖”*/
public interface A {
    //常量
    public static final String SUCCESS = "success";
    public static final String PI = "3.14";
    public static final byte MAX_VALUE=127;
    //抽象方法
    public abstract void m1();
    void m2();
    interface B {
        void m1();
    }
    interface C {
        void m2();
    }
    interface D {
        void m3();
    }
    interface E extends B,C,D{
        void m4();
    }
    //extends只能单继承，所以引入implements实现
    class MyClass implements B,C{
        public void m1(){}
        public void m2(){}
    }
    class F implements E{
        public void m1(){}
        public void m2(){}
        public void m3(){}
        public void m4(){}
    }
}
```
```java
/*
客户业务接口
接口的作用：
1.可以使项目分层，所以层都要面向接口开发，开发效率提高了。
2.接口使代码和代码之间耦合度降低，变得“可插拔”可以随意切换。
3.接口和抽象类都能完成某个功能，优先是选择接口。
因为接口可以多实现，多继承，并且一个类除了接口之外，还可以去继承其他类（保留了其他类）
*/
public interface CustomerService {
    //定义一个退出系统的方法
    void logout();
}
```
```java
//编写接口实现类
public class CostomerServiceImpl implements CustomerService {
    public void logout() {
        System.out.println("系统成功退出！");
    }
}
```
```java
public class Test01 {
    public static void main(String[] args) {
//        以下面向接口调用
        CustomerService cs = new CostomerServiceImpl(); //多态
        cs.logout();
    }
}
```
## Example 2
```java
package Car;
/*
* 汽车和发动机之间的接口
* 生产汽车的厂家面向接口生产
* 生产发动机的厂家面向接口生产
* */
public interface Engine {
//    所有发动机都可以启动
    void start();
}
```
```java
package Car;
//生产汽车
public class Car {
//    引擎
//    面向接口编程
    Engine e;
//    constructor
    Car(Engine e) {
        this.e = e;
    }
//    汽车应该能够测试引擎
    public void testEngin() {
        e.start();
    }
}
```
```java
package Car;

public class HONDA implements Engine {
    public void start() {
        System.out.println("HONDA启动");
    }
}
```
```java
package Car;

public class YAMAHA implements Engine {
    public void start() {
        System.out.println("YAMAHA启动");
    }
}
```
```java
package Car;

public class Test {
    public static void main(String[] args) {
//        生产引擎
        Engine e1 = new YAMAHA();
//        生产汽车
        Car c = new Car(e1);
//        测试引擎
        c.testEngin();
    }
}
```
