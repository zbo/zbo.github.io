---
layout: post
tags: basic
date: 2015-08-14 13:06
title: Singleton creation
published: true
---

this is the code I use to create singleton, but missing one volatile,
[this article] point out: java byte code might be rearranged to improve performance.
so if no volatile keywords, the instance could be not none, but memory still not initialized.

{% highlight java %}
public class DoubleCheckedLocking {                      //1
    private static Instance instance;                    //2
    public static Instance getInstance() {               //3
        if (instance == null) {                          //4:first check
            synchronized (DoubleCheckedLocking.class) {  //5:lock
                if (instance == null)                    //6:second check
                    instance = new Instance();           //7:problem here
            }                                            //8
        }                                                //9
        return instance;                                 //10
    }                                                    //11
}
{% endhighlight %}

<br/>
instance initialize contains three major steps:
{% highlight java %}
memory = allocate();   //1：分配对象的内存空间
ctorInstance(memory);  //2：初始化对象
instance = memory;     //3：设置instance指向刚分配的内存地址
{% endhighlight %}

<br/>
{% highlight java %}
memory = allocate();   //1：分配对象的内存空间
instance = memory;     //3：设置instance指向刚分配的内存地址
                       //注意，此时对象还没有被初始化！
ctorInstance(memory);  //2：初始化对象
{% endhighlight %}

which means, following two statement could be both true.
{% highlight java %}
instance!=null
instance have no memory connected
{% endhighlight %}
<p></p>
this could mess your plate.

the right code should include volatile.

{% highlight java %}
public class SafeDoubleCheckedLocking {
private volatile static Instance instance;
    public static Instance getInstance() {
        if (instance == null) {
            synchronized (SafeDoubleCheckedLocking.class) {
        if (instance == null)
            instance = new Instance();
            //instance volatile，resolve the problem
        }
        }
        return instance;
        }
}
{% endhighlight %}


[this article]: http://www.infoq.com/cn/articles/double-checked-locking-with-delay-initialization/