---
layout: post
title: Java Summary
categories:  [blog ]
tags: [Java ]
comments: true
published: true


---
## Java Summary

Java面试相关问题：

1. **JVM**

JVM是Java虚拟机，JVM会把Java code编译为byte code，然后执行这些byte code。所有的系统都能够安装Java虚拟机，这体现了Java程序的多平台执行优势。

2. **OOPS**

面向对象编程，具有四个概念；

- Abstraction 抽象性；
- Polymorphism 多态；
- Inheritance 继承；
- Encapsulation 封装；

3. **Overloadding VS Overriding**

- Overloadding 发生在compile阶段，Overriding发生在runtime阶段；
- Overloading是在同一个类中写同一个函数，只是参数的类型不同。而overriding一般会在子类中出现，并且重写的时候函数名字和参数类型是一样的。
- 返回类型，overloading可以自由定义，但是overriding必须和继承的父类保持一致。
- 可以overloading一个static类，但是不能overriding一个static类。

4. **Static 和 Instance**

**static** method 是一个类级别的方法，可以直接调用。**instance**是一个对象级别的方法，需要首先创建一个引用指向它，然后再进行调用。

5. **Stringbuilder, Stringbuffer, string的区别**

- String是immutable的，不可改变的。Stringbuilder和Stringbuffer都是mutable的。
- Stringbuffer是synchronized(同步的)，Stringbuilder不是。
- Stringbuilder比Stringbuffer快。
- Stringbuffer线程安全，且保证同步。Stringbuilder不保证线程同步。String也是线程安全的，因为它不改变。

6. **Java是值传递还是引用传递**

在写函数的过程中，如果参数是基本类，如int或者double，那么java是值传递。在Java中对象作为参数传递时，把对象在内存中的地址拷贝了一份传给了参数。所以总体来说都是pass by value。

7. **Serialization and Desearialziation**

Serialization将对象转化为数据流，方便对象可以在网络中进行传递。Desearialziation将数据流转化为对象。

8. **Final, Finally, FInalize**

- Final可以修饰变量，方法和类。修饰变量，说明该变量不能再改变。修饰method，说明该方法不能被overridden。修饰class，说明改类不能被继承。
- Finally是用在异常处理的情况。代码如果被写入了finally的模块中，不管该代码是否抛出异常，到最后finally块中的代码都必须执行，这个修饰一般用在关闭网络流，数据流或者输入输出流一类的处理。

9. **Java创建多线程**

一般在java中,创建多线程有两种方法:

* 继承Thread类；
* 重写run() 函数,然后调用start()函数.
* Code

- ```java
  public class simpleThread extends Thread {
  	public void run() {
  		// 写上你的task
  		System.out.println("Hello");
  	}
  }

  public class simple {
  	public static void main(String[] agrs) {
  		simpleThread t = new simpleThread();
  		t.start();
  	}
  }

  **实现Runnable接口.
  方法和上面差不多,不过是实现接口,重写的函数还是run方法.

  public class simpleThread implements Runnable {
  	public void run() {
  		// 写上你的task
  		System.out.println("Hello");
  	}
  }

  public class simple {
  	public static void main(String[] agrs) {
  		Thread t = new Thread( new simpleThread() );
  		t.start();
  	}
  }
  ```


10. **Java HashMap**

HashMap是基于Map接口的实现，储存键值对时，可以接收null的键值，是非同步的。HashMap储存着Entry(hash, key, value, next)对象。

11. **HashMap的get和put函数**

在使用put函数的时候，会把key和value传入，hashmap会使用hashcood函数计算出key的hash value，通过计算出的hash value找到对应的bucket，如果当前的bucket已经满了，HashMap会根据情况对容量进行扩容，一般是当前capacity的两倍。使用get函数的时候传入key的值，计算出对应的hash value，找到对应的bucket，然后在bucket中使用equals函数找到相应的key。如果出现碰撞的情况，会使用linked list解决冲突。

12. **创建私有的构造函数**

私有构造函数和一般的私有函数没有区别，只是能够类内部进行调用，外部无法进行访问。创建私有函数的原因有两个：（1）不想让除了类之外的其他类构造访问这个类（2）只希望该对象在类的内部构造。

13. **Singleton Design(单例模式)**

设计singleton的关键是不能让其他类随便构造该类对象，即控制该类的构造函数。将构造函数变为私有是一个关键的步骤。

- Code



```java
// 以 singleton 的模式实现该类
public class Logging {
	// 创建一个实例，有且只有一个
	private static final Logging singletonInstance = new Logging();

	// 私有构造函数
	private Logging() {}

	// 返回实例，保证了有且只有一个实例
	public static Logging getSingleton() {
		return singletonInstance;
	}
}
```
如果将上面的singleton实例只有在被需要的时候再创建从而节省资源：

```java

private static Logging singletonInstance = null;
public static Logging getSingleton() {
	if(singletonInstance == null)
		singletonInstance = new Loging();
	reutrn singletonInstance;
}
```
在设计singleton的时候保证线程安全：基于单线程时上面的设计没有问题，若有多个线程，并且这些线程同时调用上面的getSingleton函数来对实例进行初始化，因为同一时间满足了条件，则会创建两个或者以上的实例。可以通过**synchronized**关键字来解决问题。**synchronized**可以保证该函数只有一个线程可以进行访问，从而避免了上述冲突情况的出现。

```java
private static Logging singletonInstance = null;
public synchronized static Logging getSingleton() {
	if(singletonInstance == null)
		singletonInstance = new Loging();
	reutrn singletonInstance;
}
```
14.**用最少的code写一个函数，要求会把栈用光**

一般说，所有的对象都是存放在堆中的，而指向对象的reference是存在栈里面的，函数调用，一开始也会放进栈中。所以用光栈最快的方法是进行递归调用。

- **Code**:

```java
public class Useupstack {
	public static void main(String[] args) {
		help();
	}
	
	public static help() {
		help();
	}
}
```
- 用完堆里面的函数：java不方便对内存直接调用，所以用C++。C++可以任意对内存进行控制，可以使用malloc函数进行内存操作：

  ```c++

  #include <stdlib.h>
  #include <unistd.h>

  void main(int argc, char** argv)
  {
      while(1)
      {
          malloc(1);
      }
  }
  ```

