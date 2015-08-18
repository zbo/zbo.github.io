---
layout: post
tags: basic
date: 2015-08-14 13:06
title: Singleton creation
published: true
---

this is the code I use to create singleton, but missing one volatile,
[this article] point out: java byte code might be rearranged to improve performance.
so if no volatile keywords, the instance could be not none, but memory still not allocated.

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