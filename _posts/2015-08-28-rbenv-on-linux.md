---
layout: post
tags: basic
date: 2015-08-28 10:10
title: rbenv setup on linux
published: true
---

**ubuntu** and steps install rbenv
refer to [article]

<p/>
clone rbenv and setup path:
{% highlight ruby %}
git clone git://github.com/sstephenson/rbenv.git ~/.rbenv
echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bashrc
echo 'eval "$(rbenv init -)"' >> ~/.bashrc
{% endhighlight %}

<p/>
clone rb build plugin
{% highlight ruby %}
mkdir -p ~/.rbenv/plugins
cd ~/.rbenv/plugins
git clone git://github.com/sstephenson/ruby-build.git
{% endhighlight %}

[article]: http://about.ac/2012/04/install-ruby-with-rbenv.html
