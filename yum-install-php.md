# 概况

本文介绍一种比较便捷的安装PHP环境的方法-yum安装,这种安装方式相比源码安装PHP，更加方便快捷。
使用yum安装PHP的前提是分清本身操作系统版本和想安装的PHP版本，版本的匹配和镜像源兼容是环境安装成功的关键。

本文以centos7和PHP7.2，没有安装过PHP环境的一台服务器为例来说明。

## epel源

epel 是 Extra Packages for Enterprise Linux (EPEL)，网上相关资料提示 更新yum源，就是基于epel的。

参考网址 [https://fedoraproject.org/wiki/EPEL#Quickstart](https://fedoraproject.org/wiki/EPEL#Quickstart)

![yum源.png](https://upload-images.jianshu.io/upload_images/5651-cf65681648d54cfc.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 通过yum方式安装PHP

第一步依然是寻找适合的版本

>yum search php72

如图所示，命令会列出所有与php7.2相关的扩展，模块名称和模块说明依次罗列了出来。基本扩展fpm，pdo，mongodb，都在这里可以找到。

![yumphp72.png](https://upload-images.jianshu.io/upload_images/5651-c4428b106222ee1b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 常见扩展

以下是search php72 显示的扩展，常见扩展用不同的显示块进行了标记，全部已安装。

```
php72w-common.x86_64y
Installed:
  php72w-common.x86_64 0:7.2.21-1.w7 
```

>yum install php72w-cli.x86_64

Installed:
  php72w-cli.x86_64 0:7.2.21-1.w7                                                                                                                       

Dependency Installed:
  libargon2.x86_64 0:20161029-3.el7

>php72w-fpm.x86_64 : PHP FastCGI Process Manager


Running transaction
  Installing : php72w-fpm-7.2.21-1.w7.x86_64                                                                                                        1/1 
  Verifying  : php72w-fpm-7.2.21-1.w7.x86_64                                                                                                        1/1 

Installed:
  php72w-fpm.x86_64 0:7.2.21-1.w7

>php72w-mysql.x86_64 : A module for PHP applications that use MySQL databases

Installed:
  php72w-mysql.x86_64 0:7.2.21-1.w7                                                                                                                     

Dependency Installed:
  php72w-pdo.x86_64 0:7.2.21-1.w7  

>yum install php72w-devel.x86_64

php72w-bcmath.x86_64 : A module for PHP applications for using the bcmath library

>php72w-cli.x86_64 : Command-line interface for PHP

>php72w-common.x86_64 : Common files for PHP

php72w-dba.x86_64 : A database abstraction layer module for PHP applications
php72w-devel.x86_64 : Files needed for building PHP extensions


php72w-embedded.x86_64 : PHP library for embedding in applications

php72w-enchant.x86_64 : Enchant spelling extension for PHP applications
>php72w-fpm.x86_64 : PHP FastCGI Process Manager

>php72w-gd.x86_64 : A module for PHP applications for using the gd graphics library

php72w-imap.x86_64 : A module for PHP applications that use IMAP
php72w-interbase.x86_64 : A module for PHP applications that use Interbase/Firebird databases

php72w-intl.x86_64 : Internationalization extension for PHP applications
php72w-ldap.x86_64 : A module for PHP applications that use LDAP

php72w-mbstring.x86_64 : A module for PHP applications which need multi-byte string handling
>php72w-mysql.x86_64 : A module for PHP applications that use MySQL databases

php72w-mysqlnd.x86_64 : A module for PHP applications that use MySQL databases
php72w-odbc.x86_64 : A module for PHP applications that use ODBC databases

>php72w-opcache.x86_64 : An opcode cache Zend extension

>php72w-pdo.x86_64 : A database access abstraction module for PHP applications

>php72w-pdo_dblib.x86_64 : MSSQL database module for PHP

>php72w-pear.noarch : PHP Extension and Application Repository framework

php72w-pecl-apcu.x86_64 : APCu - APC User Cache
php72w-pecl-apcu-devel.x86_64 : APCu developer files (header)

php72w-pecl-geoip.x86_64 : Extension to map IP addresses to geographic places

>php72w-pecl-igbinary.x86_64 : Replacement for the standard PHP serializer

php72w-pecl-igbinary-devel.x86_64 : Igbinary developer files (header)

>php72w-pecl-imagick.x86_64 : Provides a wrapper to the ImageMagick library

php72w-pecl-imagick-devel.x86_64 : Imagick developer files (header)

php72w-pecl-libsodium.x86_64 : Wrapper for the Sodium cryptographic library

php72w-pecl-memcached.x86_64 : Extension to work with the Memcached caching daemon

>php72w-pecl-mongodb.x86_64 : PECL package MongoDB driver

php72w-pecl-redis.x86_64 : Extension for communicating with the Redis key-value store

php72w-pecl-xdebug.x86_64 : PECL package for debugging PHP scripts
php72w-pgsql.x86_64 : A PostgreSQL database module for PHP

php72w-phpdbg.x86_64 : Interactive PHP debugger
php72w-process.x86_64 : Modules for PHP script using system process interfaces

php72w-pspell.x86_64 : A module for PHP applications for using pspell interfaces

php72w-recode.x86_64 : A module for PHP applications for using the recode library

php72w-snmp.x86_64 : A module for PHP applications that query SNMP-managed devices

php72w-soap.x86_64 : A module for PHP applications that use the SOAP protocol


## 常见基础命令

使用yum 方式安装完成的php环境，当然是支持php 命令行常见命令的，比如

### 查看配置文件基本信息

```
php  --ini
```
php7以后主配置文件和扩展文件是分开的
```
Configuration File (php.ini) Path: /etc
Loaded Configuration File:         /etc/php.ini
Scan for additional .ini files in: /etc/php.d
Additional .ini files parsed:      /etc/php.d/bcmath.ini,
/etc/php.d/bz2.ini,
/etc/php.d/calendar.ini,
/etc/php.d/ctype.ini,
/etc/php.d/curl.ini,
/etc/php.d/dom.ini,
/etc/php.d/exif.ini,
/etc/php.d/fileinfo.ini,
/etc/php.d/ftp.ini,
/etc/php.d/gd.ini,
/etc/php.d/gettext.ini,
/etc/php.d/gmp.ini,
/etc/php.d/iconv.ini,
/etc/php.d/igbinary.ini,
/etc/php.d/imagick.ini,
```
### 查看扩展模块加载情况

grep 扩展名称

``` 
php -m  |grep mongodb

[root@10-9-77-82 ~]# php -m  |grep mongodb
mongodb

```

mongodb

### 查看PHP 扩展目录

```
php-config --extension-dir
```

### pdo_mysql.so 加载错误

在执行 php -ini 时遇到以下错误，提示未能加载mysqli.so和pdo_mysql.so.so


```
PHP Warning:  PHP Startup: Unable to load dynamic library 'mysqli.so' (tried: /usr/lib64/php/modules/mysqli.so (libmysqlclient.so.18: cannot open shared object file: No such file or directory), /usr/lib64/php/modules/mysqli.so.so (/usr/lib64/php/modules/mysqli.so.so: cannot open shared object file: No such file or directory)) in Unknown on line 0
PHP Warning:  PHP Startup: Unable to load dynamic library 'pdo_mysql.so' (tried: /usr/lib64/php/modules/pdo_mysql.so (libmysqlclient.so.18: cannot open shared object file: No such file or directory), /usr/lib64/php/modules/pdo_mysql.so.so (/usr/lib64/php/modules/pdo_mysql.so.so: cannot open shared object file: No such file or directory)) in Unknown on line 0
```

加载相关模块，解决加载 mysql.so 报错 

>yum install php72w-mysql.x86_64 

检测验证

>php -m |grep mysql

![mysql.so.png](https://upload-images.jianshu.io/upload_images/5651-f3ad4b98aeb37c02.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```
php72w-mysql.x86_64 : A module for PHP applications that use MySQL databases
php72w-mysqlnd.x86_64 : A module for PHP applications that use MySQL databases

```

## 什么是 systemctl

systemctl 是一种Linux服务管理的方式 

从CentOS 7.x开始，CentOS开始使用systemd服务来代替daemon。

![systemctl-centos7.png](https://upload-images.jianshu.io/upload_images/5651-efca4f51b42903ba.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


systemd的设计目标是，为系统的启动和管理提供一套完整的解决方案。

>systemctl是 Systemd 的主命令，用于管理系统

根据 Linux 惯例，字母d是守护进程（daemon）的缩写。 Systemd 这个名字的含义，就是它要守护整个系统

关于systemctl详细的介绍请移步这里 

Systemd 入门教程：命令篇 http://www.ruanyifeng.com/blog/2016/03/systemd-tutorial-commands.html 
Systemd 入门教程：实战篇 http://www.ruanyifeng.com/blog/2016/03/systemd-tutorial-part-two.html 

### 认识 /usr/lib/systemd/system

对于那些支持 Systemd 的软件，安装的时候，会自动在/usr/lib/systemd/system目录添加一个配置文件,我们cd 到这个目录下，找到php-fpm.service文件，看看内容如下
```
cd /usr/lib/systemd/system

[root@10-9-77-82 system]# cat php-fpm.service
[Unit]
Description=The PHP FastCGI Process Manager
After=syslog.target network.target

[Service]
Type=notify
PIDFile=/var/run/php-fpm/php-fpm.pid
EnvironmentFile=/etc/sysconfig/php-fpm
ExecStart=/usr/sbin/php-fpm --nodaemonize --fpm-config /etc/php-fpm.conf
ExecReload=/bin/kill -USR2 $MAINPID
PrivateTmp=true

[Install]
WantedBy=multi-user.target
```
以下是systemctl 常用命令

### 启动服务

```
systemctl start php-fpm
```

![chmod-php.png](https://upload-images.jianshu.io/upload_images/5651-87834d29ee621826.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![systemctl-php-fpm.png](https://upload-images.jianshu.io/upload_images/5651-6c710599238e0178.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 查看所有启动的服务

```
systemctl list-units --type=service
```
![ systemctl-list.png](https://upload-images.jianshu.io/upload_images/5651-a387e2789c8cdf2b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

如图，我们可以 看到服务名称php-fpm.service 和crond.service

### 查看服务状态 

```
systemctl status  php-fpm
```
![ systemctl-status.png](https://upload-images.jianshu.io/upload_images/5651-b0997d9dfdd91efc.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 总结

yum是一个软件包管理器，相比源码编译安装，yum安装方式更加方便，快捷。自动解决软件包之间的依赖关系。本文中的操作示例，换做不同的操作系统，和不同的php版本，或者nginx，mysql，对应的包，源，都会有变化。

yum安装软件，使用者不需要指定安装目录，也就是说没法控制yum软件包的安装目录。

而我们需要理解的是yum的使用套路，首先使用search 命令找到合适的源，然后安装，寻找配置文件，启动服务。运行过程中，有修改，再针对性的安装或者调整。

对于centos7 管理软件服务的不同，就像这篇文章中（https://blog.csdn.net/u012834750/article/details/80501440）
提到的，centos7中的命令大变样，会不会觉得之前学习的命令都用不上了，使用者总是得拥抱变化，学习新的方式，所以说命令总是记不完的，对于新东西，学习要抓住核心本质。

end 2019年9月21 
610212129@qq.com

