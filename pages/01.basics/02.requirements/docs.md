---
title: Требования
taxonomy:
    category: docs
---

Grav специально разработан, чтобы не быть требовательным. Вы запросто можете запустить Grav на вашем компьютере, а так же на 99% веб-хостингах. Если у вас под рукой ручка, запишите системные требования для Grav:

1. Веб-сервер (Apache, Nginx, LiteSpeed, Lightly, IIS и т. Д.)
2. PHP 5.6.3 или выше
3. Хм... этого хватит, (но, пожалуйста, посмотрите на требования к PHP чтобы не обламываться)

Grav использует обычные текстовые файлы для работы с контентом. Нет необходимости использовать базы данных. 

!! Для оптимальной производительности настоятельно рекомендуется использовать пользовательский кеш PHP, такой как APC, APCu, XCache, Memcached или Redis. Не волнуйтесь, это, как правило, уже входит есть на хостинге!

## Веб-серверы

Grav настолько прост и универсален, что вам даже не нужен веб-сервер для его запуска. Вы можете запустить его непосредственно из встроенного инструмента `router.php` PHP, если вы используете PHP 5.6.3 или новее.

This is a useful way to check a Grav install and perform some brief development, but it is **not** recommended for a live site or even for advanced development tasks. We've outlined how in our [Installation guide](../installation#running-grav-with-the-built-in-php-webserver-using-routerphp).

Even though technically you do not need a standalone web server, it is better to run one, even for local development. There are many great options available:

### Mac

* OS X 10.13 High Sierra уже поставляется с веб-сервером Apache и PHP 7.2, поэтому работа выполнена!
* [MAMP/MAMP Pro](http://mamp.info) поставляется с Apache, MySQL и, конечно, PHP. Это отличный способ получить больше контроля над версией PHP, которую вы запускаете, настройкой виртуальных хостов и другими полезными функциями, такими как автоматическая обработка динамического DNS.
* [AMPPS](http://www.ampps.com/downloads) это программный стек от Softaculous, включащий Apache, PHP, Perl, Python, .. Это включает в себя все, что вам нужно (и многое другое) для разработки GRAV.

### Windows

* [Open Server](https://ospanel.io/) это портативная серверная платформа в которой есть всё что вам нужно.
* [XAMPP](https://www.apachefriends.org/index.html) предоставляет Apache, PHP и MySQL в одном простом пакете.
* [EasyPHP](http://www.easyphp.org/) provides a personal Web hosting package as well as a more powerful developer version.
* [MAMP for Windows](http://mamp.info) долгое время был популярным на MAC, но теперь доступен и на Windows.
* [IIS with PHP](http://php.iis.net/) это быстрый способ запуска PHP на Windows.
* [AMPPS](http://www.ampps.com/downloads) это программный стек от Softaculous, включащий Apache, PHP, Perl, Python, .. Это включает в себя все, что вам нужно (и многое другое) для разработки GRAV.

### Linux

* Многие дистрибутивы Linux уже поставляются с встроенным Apache и PHP. Если это не так, дистрибутив обычно предоставляет менеджер пакетов, через который вы можете установить их без особых проблем. Более продвинутые конфигурации поможет иследовать хорошая поисковая система.

### Требования к Apache

Несмотря на то, что большинство дистрибутивов Apache поставляются со всем необходимым, для полноты, вот список необходимых модулей Apache:

* `mod_rewrite`
* `mod_ssl` (если вы хотите запустить Grav с SSL)

You should also ensure you have `AllowOverride All` set in the `<Directory>` and/or `<VirtualHost>` blocks so that the `.htaccess` file processes correctly, and rewrite rules take effect.

### Требования к IIS

Although IIS is considered a web server ready to run 'out-of-the-box', some changes need to be made.

To get **Grav** running on an IIS server, you need to install **URL Rewrite**. This can be accomplished using **Microsoft Web Platform Installer** from within IIS. You can also install URL Rewrite by going to [iis.net](https://www.iis.net/downloads/microsoft/url-rewrite).

### Требования к PHP

Most hosting providers and even local LAMP setups have PHP pre-configured with everything you need for Grav to run 'out-of-the-box'. However, some Windows setups, and even Linux distributions local or on VPS (I'm looking at you Debian!) - ship with a very minimal PHP compile. Therefore, you may need to install or enable these PHP modules:

* `curl` (client for URL handling used by GPM)
* `ctype` (used by symfony/yaml/Inline)
* `dom` (used by grav/admin newsfeed)
* `gd` (a graphics library used to manipulate images)
* `json` (used by Symfony/Composer/GPM)
* `mbstring` (multibyte string support)
* `openssl` (secure sockets library used by GPM)
* `session` (used by toolbox)
* `simplexml` (used by grav/admin newsfeed)
* `xml` (XML support)
* `zip` extension support (used by GPM)

For enabling `openssl` and (un)zip support you will need to find in the `php.ini` file of your Linux distribution for lines like:

  - `;extension=openssl.so`.
  - `;extension=zip.so`.

and remove the leading semicolon.

##### Optional Modules

* `apcu` for increased cache performance
* `opcache` for increased PHP performance
* `xcache` alternative to *apcu*, not as fast, but still pretty good
* `yaml` PECL Yaml provides native yaml processing and can dramatically increase performance
* `xdebug` useful for debugging in a development environment

### Permissions

For Grav to function correctly, your web server needs to have the appropriate **file permissions** to write logs, caches, etc. When using either the [CLI](/advanced/grav-cli) (Command Line Interface) or [GPM](/advanced/grav-gpm) (Grav Package Manager), the user running PHP from the command line also needs to have the appropriate permissions to modify files.

By default, Grav will install with `644` and `755` permissions for files and folders, respectively. Most hosting providers have configurations that ensure that a web server running PHP will allow you to create and modify files within your user account. This means that Grav runs **out-of-the-box** on the vast majority of hosting providers.

However, if you are running on a dedicated server or even your local environment, you may need to adjust permissions to ensure your **user** and your **web server** can modify files as needed. There are a couple of approaches you can take.

1. In a **local development environment**, you can usually configure your web server to run under your user profile. This way the web server will always allow you to create and modify files.

2. Change the **group permissions** on all files and folders so that the web server's group has write access to files and folders while keeping the standard permissions. This requires a few commands to make this work.

First, find out which user Apache runs with by running the following command:
```
ps aux | grep -v root | grep apache | cut -d\  -f1 | sort | uniq 
```
Now, find out which group this user belongs to by running this command (note: adjust USERNAME with the apache username you found in the previous command)
```
groups USERNAME
```
(note: adjust `GROUP` to be the group your apache runs under, found in the previous command. [`www-data`, `apache`, `nobody`, etc.]):

```
chgrp -R GROUP .
find . -type f | xargs chmod 664
find ./bin -type f | xargs chmod 775
find . -type d | xargs chmod 775
find . -type d | xargs chmod +s
umask 0002
```

If you need to invoke superuser permissions, you would run `find … | sudo xargs chmod …` instead.

## Recommended Tools

### Text Editors

Although you can get away with Notepad, Textedit, Vi, or whatever default text editor comes with your platform, we recommend using a good text editor with syntax highlighting to make things easier. Here are some recommended options:

1. [SublimeText](http://www.sublimetext.com/) - OS X/Windows/Linux - A commercial developer's editor, but well worth the price. Very powerful especially combined with plugins such as [Markdown Extended](https://sublime.wbond.net/packages/Markdown%20Extended), [Pretty YAML](https://sublime.wbond.net/packages/Pretty%20YAML), and [PHP-Twig](https://sublime.wbond.net/packages/PHP-Twig).
2. [Atom](http://atom.io) - OS X/Windows/Linux - A new editor developed by Github. It's free and open source. It is similar to Sublime, but does not have the sheer depth of plugins available yet.
3. [Notepad++](http://notepad-plus-plus.org/) - Windows - A free and very popular developer's editor for Windows.
4. [Bluefish](http://bluefish.openoffice.nl/index.html) - OS X/Windows/Linux - A free, open source text editor geared towards programmers and web developers.
5. [Visual Studio Code](https://code.visualstudio.com/) - A lightweight but powerful source code editor which runs on your desktop and is available for Windows, macOS and Linux.

### Markdown Editors

Another option if you primarily work with just creating content, is to use a **Markdown Editor**. These often are very content-centric and usually provide a **live-preview** of your content rendered as HTML. There are literally hundreds of these, but some good options include:

1. [MacDown](http://macdown.uranusjr.com/) - OS X - Free, a simple, lightweight open source Markdown editor.
2. [LightPaper](http://lightpaper.42squares.in/) - OS X - $9.99, clean, powerful. Our markdown editor of choice on the Mac. **Get 25% OFF with Discount Code: GET_GRAV_25**
3. [MarkDrop](http://culturezoo.com/markdrop/) - OS X - $5, but super clean and Droplr support built-in.
4. [MarkdownPad](http://markdownpad.com/) - Windows - Free and Pro versions. Even has YAML front-matter support. An excellent solution for Windows users.
5. [Mark Text](https://marktext.github.io/website/) - Free, open source Markdown editor for Windows / Linux / OS X. 

### FTP Clients

Although there are many ways to deploy **Grav**, the simplest is to copy your local site to your hosting provider. The easiest way to accomplish this is with an [FTP Client](http://en.wikipedia.org/wiki/File_Transfer_Protocol). There are many available, but some recommended ones include:

1. [Transmit](http://panic.com/transmit/) - OS X - The de facto FTP/SFTP client on OS X. Easy to use, fast, folder-syncing and pretty much anything else you could ask for.
2. [FileZilla](https://filezilla-project.org/) - OS X/Windows/Linux - Probably the best option for Windows and Linux users. Free and very powerful (but very ugly on the Mac!).
3. [Cyberduck](http://cyberduck.io/) - OS X/Windows - A decent free option for both OS X and Windows users. Not as full-featured as the others.
4. [ForkLift](http://www.binarynights.com/forklift/) - OS X - A solid alternative to Transmit, and slightly cheaper to boot.


