---
layout:		post
comments:	true
title:		Рецепты SSH	
date:		2015-04-29
categories:
- recipes
---

Полезная замена Putty - [Putty Tray](https://puttytray.goeswhere.com/).

Генерируем новый ключ, и заливаем на таргет(ответ на вопрс - "Как передавать пароль в ssh?"):
{% highlight bash %}
ssh-keygen -t rsa
ssh-copy-id username@host
{% endhighlight %}

Рекурсивно копируем папку на локальный таргет(используется шифрование `arcfour` для ускорения процесса, когда сохраннность данных не является не важна), если на последней отсутствует [rsync](http://en.wikipedia.org/wiki/Rsync):
{% highlight bash %}
scp -r -o Ciphers=arcfour src_folder username@host:dest_folder
{% endhighlight %}
