---
title: "Update PHP version on MacOS Mojave and Catalina"
date: "2019-11-21"
cover:
  image: "/images/blog/php.jpeg"
summary: "I've decided to share some tips regarding the upgrade process of the default PHP version that comes bundled with MacOS Mojave."
---


Hello folks,

Since this is my first post in a long time, I've decided to share some tips regarding the upgrade process of the default PHP version that comes bundled with MacOS Mojave.

By default on Mojave we are running:

> php -v PHP 7.1.23 (cli) (built: Feb 22 2019 22:19:32) ( NTS ) Copyright (c) 1997-2018 The PHP Group Zend Engine v3.1.0, Copyright (c) 1998-2018 Zend Technologies

Some web apps like [Laravel](https://laravel.com/) require a more update version of PHP. Here's how you can update it via the command line:

### PHP 7.3 (Next stable) - 10.10 and later

curl -s https://php-osx.liip.ch/install.sh | bash -s 7.3

### PHP 7.2 (Current stable) - 10.10 and later

curl -s https://php-osx.liip.ch/install.sh | bash -s 7.2

### PHP 7.1 (Old stable) - 10.10 and later

curl -s https://php-osx.liip.ch/install.sh | bash -s 7.1

### PHP 7.0 (Old stable) - 10.10 and later

curl -s https://php-osx.liip.ch/install.sh | bash -s 7.0

### PHP 5.6 (Old stable) - 10.8 and later

curl -s https://php-osx.liip.ch/install.sh | bash -s 5.6

### PHP 5.5 (End of life) - All OS X versions

curl -s https://php-osx.liip.ch/install.sh | bash -s 5.5

### PHP 5.4 (End of life) - All OS X versions

curl -s https://php-osx.liip.ch/install.sh | bash -s 5.4

### PHP 5.3 (End of life) - All OS X versions

curl -s https://php-osx.liip.ch/install.sh | bash -s 5.3

After the installation is done, you should add the binary to your path in **~/.bash\_profile**:

> export PATH=/usr/local/php5/bin:$PATH

Next up, reload your terminal and type **php -v** and you should see the latest and greatest php version in action:

> php -v PHP 7.3.8 (cli) (built: Aug 11 2019 20:50:16) ( NTS ) Copyright (c) 1997-2018 The PHP Group Zend Engine v3.3.8, Copyright (c) 1998-2018 Zend Technologies with Zend OPcache v7.3.8, Copyright (c) 1999-2018, by Zend Technologies with Xdebug v2.7.2, Copyright (c) 2002-2019, by Derick Rethans
