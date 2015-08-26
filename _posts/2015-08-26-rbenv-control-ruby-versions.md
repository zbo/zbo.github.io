---
layout: post
tags: basic
date: 2015-08-26 23:31
title: rbenv usage control ruby versions
published: true
---

**rbenv** is tool to control versions
<p/>
{% highlight ruby %}
rbenv global version ＃global ruby
rbenv shell version  ＃RBENV_VERSION
rbenv local version  ＃.rbenv-version file in floder
{% endhighlight %}

<p/>
make it work by adding folloing @ bottom of your rc profile
you have to rehash everytime you change

{% highlight ruby %}
export PATH="$HOME/.rbenv/bin:$PATH"
eval "$(rbenv init -)"

plus + rbenv rehash
LMXMN031:~ bob.zhu$ ruby --version
ruby 1.9.3p545 (2014-02-24 revision 45159) [x86_64-darwin14.3.0]
{% endhighlight %}
