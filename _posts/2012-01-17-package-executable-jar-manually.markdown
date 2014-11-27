---
title: Java文件打包成可执行Jar的方法
layout: post
tags: jar
category: java
date: 2012-01-07
---

首先，这个东西呢说难也很容易，但是在不知道的情况下还是无从下手的噶。呵呵，废话不多说，进入正题。
假定你已经配置好环境变量了，如果未配置，请google。
首先：假定我们有一个工作目录是 `d:\java` , 在工作目录下存放了我们的java文件和我们的依赖jar包。假定是如下的两个文件：`HelloWorld.java` 和 `common-lang.jar`,
其中HelloWorld.java的内容如下：

{% highlight java %}
package org.tony.hello;

import java.util.Date; 
import org.apache.commons.lang.time.DateFormatUtils;
 
public class HelloWorld
{
   public static void main(String[] args) 
   {
       String curDate = DateFormatUtils.format(new Date(),"yyyy-MM-DD HH:mm:ss");
       System.out.println("curDate:" + curDate);
   }
}
{% endhighlight %}

准备工作做好了，我们需要编写我们的manifest文件 `hello.mf` :
{% highlight python %}
Manifest-Version: 1.0 
Created-By: tony example
Class-Path: test.jar commons-lang-2.4.jar
Main-Class: org.tony.hello.HelloWorld
{% endhighlight %}
接着编译我们的 `HelloWorld.java` :

{% highlight python %}
javac -cp ./common-lang.jar -d . HelloWorld.java
{% endhighlight %}
在没有出现错误的情况下，我们就需要将编译好的class文件打包到我们的jar中，同时为了携带方便，我们也将common-lang.jar打包入test.jar中，当然通常是不这样做的，使用如下命令:
`
jar -cvfm test.jar test.mf -C ./ .
`
这样就在当前目录下生成了 test.jar.在命令行下执行 `jar -jar test.jar` 就可以运行我们的程序产生结果了。