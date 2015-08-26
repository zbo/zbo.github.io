---
layout: post
tags: basic
date: 2015-08-26 14:10
title: Virtual box and extension kernel source
published: true
---

virtual box is so common tool we setup parasitic system of multiple platform. extension is something you canot live without. it offer you possibility of full screen, darg drop sharing and many cool features too. which I believe everyone with virtual box should install by a simple click.<br/>
but on the way, you may meet missing kernel source missing errors. you normally find this from **/var/log/vboxinstall.log**
<p/>

{% highlight python %}
$ sudo yum update

$ sudo yum install kernel-devel gcc
$ export KERN_DIR=/usr/src/kernels/

{% endhighlight %}
<p/>
you need `reboot` to load updated kernel to match kernel source code.
afterwards, run the VBoxLinux***Install.sh again.<br/> 
it still not work. openGL build modules failed.

{% highlight python %}

$ cd /usr/src/kernels/2.6.32-431.el6.i686/include/drm/  
$ ln -s /usr/include/drm/drm.h drm.h  
$ ln -s /usr/include/drm/drm_sarea.h drm_sarea.h  
$ ln -s /usr/include/drm/drm_mode.h drm_mode.h  
$ ln -s /usr/include/drm/drm_fourcc.h drm_fourcc.h

export MAKE='/usr/bin/gmake -i'
 

{% endhighlight %}

<p/>
reboot again.<br/>
try install again.<br/>
finally works #_#!



