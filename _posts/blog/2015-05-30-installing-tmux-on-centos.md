---
layout: post
title: "Install tmux on Centos 6.x"
share: true
modified:
categories: blog
excerpt: no idea why there is no rpm for this...
tags: []
image:
  feature:
date: 2015-05-30T22:32:00+01:00
---

I've been trying to get a consistant enviornment working for work and home and thought that it might be useful to setup a vagrant development box using Centos 6.x with puppet to see if I achieve this. Mostly it's been okay but there is no `tmux` for Centos... so you can't just type in:

`yum install tmux`

and expect it to work.

I have managed to get this to build from source and here are the list of things that I think you need to follow. I'd be grateful if someone else could give this a shot to see if there anything that I'm missing.

Firstly you need to install the depedencies that are available as rpms:

{% highlight bash %}
yum install nurses-devel
yum install automake.noarch
{% endhighlight %}

Next thing is to install `libevent` which is needed for tmux to function:

{% highlight bash %}
wget http://iweb.dl.sourceforge.net/project/levent/libevent/libevent-2.0/libevent-2.0.22-stable.tar.gz
tar zxvf ./libevent-2.0.22-stable.tar.gz
cd ./libevent-2.0.22-stable
./configure && make
sudo make install
{% endhighlight %}

You will then need to make sure that you've addded this to your `LD_LIBRARY_PATH`. I added this additional line to my `.bash_profile`:

`export LD_LIBRARY_PATH=/usr/local/lib`

Next... download and install tmux. You'll be doing this from source. I used the following commands to download from github and compile. Once you've done this you should be done:

{% highlight bash %}
git clone git://git.code.sf.net/p/tmux/tmux-code tmux-tmux-code
cd tmux-tmux-code
chmod +x ./autogen.sh
./autogen.sh
./configure && make
sudo make install
{% endhighlight %}

You can test your install by typing in `tmux -V` which should give you the latest version number.

Enjoy.
