---
title: Установка
taxonomy:
    category: docs
---

Установка Gravc это тривиальный процесс. По факту это не настоящая установка. У вас есть **три** варианта как установить Grav. Первый - самый простой - скачать **zip** архив и распоковать его. Второй варианта - установка с помощью **Composer**. Третий вариант это сделать копию исходного проекта из **GitHub**, и затем запустить встроенный скрипт для установки необходимых зависимостей:

## Проверьте версию PHP

Grav невероятно прост в настройке и запуске. Убедитесь, что ваша версия PHP выше 5.5.9, перейдя в терминал и набрав:

```bash
$ php -v
```
В ответ вы получите информацию о версии и сборке. Например:

```bash
PHP 7.2.7 (cli) (built: Jun 19 2018 23:13:48) ( NTS MSVC15 (Visual C++ 2017) x64 )
Copyright (c) 1997-2018 The PHP Group
Zend Engine v3.2.0, Copyright (c) 1998-2018 Zend Technologies
```

## Вариант 1: установить из ZIP-пакета

Самый простой способ установить Grav - загрузить ZIP-пакет и извлечь его:

1. Загрузите самую последнюю версию **[Grav](https://getgrav.org/download/core/grav/latest)** или сборку **[Grav + Панель администрировнания](https://getgrav.org/download/core/grav-admin/latest)**.
2. Извлеките ZIP-файл в [корневой каталог](https://www.wordnik.com/words/webroot) вашего веб-сервера, например `~/webroot/grav`

!!! Есть [Skeleton](https://getgrav.org/downloads/skeletons)-сборки, которые включают в себя основную систему Grav, образцы страниц, плагины и конфигурацию. Это отличный способ начать работу; все, что вам нужно сделать, это [скачать Skeleton](https://getgrav.org/downloads/skeletons)-сборку, которая подходит вам, и сдедовать инструкциям.

!!!! If you downloaded the ZIP file and then plan to move it to your webroot, please move the **ENTIRE FOLDER** because it contains several hidden files (such as .htaccess) that will not be selected by default. The omission of these hidden files can cause problems when running Grav.


## Вариант 2: установка через Composer

Альтернативный метод - это установить Grav с [Composer](https://getcomposer.org/doc/00-intro.md#installation-linux-unix-osx):

```
$ composer create-project getgrav/grav ~/webroot/grav
```

Если вы хотите поробовать новейшую версию Grav, добавьте `1.x-dev` в качестве дополнительного параметра:

```
$ composer create-project getgrav/grav ~/webroot/grav 1.x-dev
```

## Вариант 3: установить через GitHub

Другой метод - клонировать Grav из репозитория GitHub, а затем запустить простой скрипт установки зависимостей:

1. Clone the Grav repository from [GitHub](https://github.com/getgrav/grav) to a folder in the webroot of your server, e.g. `~/webroot/grav`. Launch a **terminal** or **console** and navigate to the webroot folder:
   ```
   $ cd ~/webroot
   $ git clone -b master https://github.com/getgrav/grav.git
   ```

2. Install **vendor dependencies** via [composer](https://getcomposer.org/doc/00-intro.md#installation-linux-unix-osx):
   ```
   $ cd ~/webroot/grav
   $ composer install --no-dev -o
   ```

3. Install the **plugin** and **theme dependencies** by using the [Grav CLI application](../../advanced/grav-cli) `bin/grav`:
   ```
   $ cd ~/webroot/grav
   $ bin/grav install
   ```

   This will automatically **clone** the required dependencies from GitHub directly into this Grav installation.

## Веб сервер

#### Apache/IIS/Nginx

Использование Grav с веб-сервером, таким как Apache, IIS или Nginx, так же просто, как извлечение Grav в папку под [webroot](https://www.wordnik.com/words/webroot). Все, что требуется для работы, это PHP 5.5.9 или выше, поэтому вы должны убедиться, что ваш экземпляр сервера отвечает этому требованию. Более подробную информацию о требованиях Grav можно найти в главе [требования](../requirements) этого руководства.


Using Grav with a web server such as Apache, IIS, or Nginx is as simple as extracting Grav into a folder under the [webroot](https://www.wordnik.com/words/webroot). All it requires to function is PHP 5.5.9 or higher, so you should make sure that your server instance meets that requirement. More information about Grav requirements can be found in the [requirements](../requirements) chapter of this guide.

If your web root is, for example, `~/public_html` then you could extract it into this folder and reach it via `http://localhost`. If you extracted it into `~/public_html/grav` you would reach it via `http://localhost/grav`.

!!! Every web server must be configured. Grav ships with .htaccess by default, for Apache, and comes with some [default server configuration files](https://github.com/getgrav/grav/tree/master/webserver-configs), for `nginx`, `caddy server`, `iis`, and `lighttpd`. Use them accordingly when needed.

#### Running Grav with the Built-in PHP Webserver Using `router.php`

You can run Grav using a simple command from Terminal / Command Prompt using the built-in PHP server available to any system with PHP 5.5+ installed. All you need to do is navigate to the root of your Grav install using the Terminal or Command Prompt and enter `php -S localhost:8000 system/router.php`. You can replace the port number (in our example it's `8000`) with any port you prefer.

Entering this command will present you with output similar to the following:

```bash
$ php -S localhost:8000 system/router.php
PHP 7.0.14 Development Server started at Thu Jan 26 17:19:50 2017
Listening on http://localhost:8000
Document root is /Users/example/sites/grav/
Press Ctrl-C to quit.
```

Your terminal will also give you real-time updates of any activity on this ad hoc-style server. You can copy the URL provided in the `Listening on` line and paste that into your browser of choice to access your site, including the administrator.

!!!! This is a useful tool for quick development, and should **not** be used in place of a dedicated web server such as Apache.


## Successful Installation

The first time it loads, Grav pre-compiles some files. If you now refresh your browser, you will get a faster, cached version.

![Grav Installed](install.png?cropResize=600,600)  {.border}

!! In the previous examples, **$** represents the command prompt. This may look different on various platforms.

By default, Grav comes with some sample pages to give you something to get started with. Your site is already fully functional and you can configure it, add content, extend it, or customize it as much as you like.

## Installation & Setup Problems

If any issues are discovered during the initial page load (or after a cache-flush event) you may see an error page:

![Grav with Problems](problems.png?cropResize=600,600)  {.border}

Please consult the [Troubleshooting](../../troubleshooting) section for help regarding specific issues.

! If you have issues with file permissions, please check the [Permissions Troubleshooting documentation](/troubleshooting/permissions). Also, you could look at the [Hosting Guides documentation](/webservers-hosting) that has specific instructions for various hosting environments

## Grav Updates

### Automatic Updates

The preferred method for updating Grav (from v0.9.3 onwards) is to use the **Grav Package Manager (GPM)**. All you need to do  is to navigate to the root of your Grav site and type:

```
bin/gpm selfupgrade -f
```

Full information can be found in the [Grav GPM Documentation](../../advanced/grav-gpm). We also have GPM integrated into our [Admin Panel](../../admin-panel) plugin which will check, prompt, and automatically install any updates.
