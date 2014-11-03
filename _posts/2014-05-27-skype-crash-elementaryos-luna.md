---
layout:     post
title:      Skype падает на ElementaryOS Luna
date:       2013-10-15 20:00:00
summary:	Как починить падение скайпа на ElementaryOS Luna.
---

После установки последней версии [elementaryOS](http://elementaryos.org/) скайп категорически отказывался принимать, или совершать, любые звонки.
При этом в логе можно было наблюдать следующие ошибки:

{% highlight bash %}
ALSA lib conf.c:3314:sad:snd_config_hooks_call) Cannot open shared library libasound_module_conf_pulse.so
ALSA lib control.c:951:sad:snd_ctl_open_noupdate) Invalid CTL default
skype: hcontrol.c:326: _snd_hctl_find_elem: Assertion `hctl failed.
Aborted
{% endhighlight %}

Все дело в том что Microsoft по прежнему забывает прописывать корректные зависимости для 64-х битного пакета. На Debian-based системе лечится с помощью следующей команды:

{% highlight bash %}
sudo apt-get install libasound2-plugings:i386
{% endhighlight %}
