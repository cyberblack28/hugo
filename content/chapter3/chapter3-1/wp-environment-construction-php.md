---
title: "2.WordPress Environment Construction - PHP"
date: 2017-10-17T15:26:15Z
draft: false
weight: 10
---

## PHPのインストール手順

1.PHP7系のインストール

```
# yum -y install --enablerepo=epel,remi-php72 php php-mbstring php-pear php-fpm php-mcrypt php-mysql
Loaded plugins: fastestmirror
Loading mirror speeds from cached hostfile
 * epel: ftp.jaist.ac.jp
 * remi-php72: ftp.riken.jp
 * remi-safe: ftp.riken.jp
Package php-mcrypt is obsoleted by php-pecl-mcrypt, trying to install php-pecl-mcrypt-1.0.3-1.el7.remi.7.2.x86_64 instead
Package php-mysql is obsoleted by php-mysqlnd, trying to install php-mysqlnd-7.2.27-1.el7.remi.x86_64 instead
Resolving Dependencies
--> Running transaction check
---> Package php.x86_64 0:7.2.27-1.el7.remi will be installed
--> Processing Dependency: httpd-mmn = 20120211x8664 for package: php-7.2.27-1.el7.remi.x86_64
--> Processing Dependency: php-cli(x86-64) = 7.2.27-1.el7.remi for package: php-7.2.27-1.el7.remi.x86_64
--> Processing Dependency: php-common(x86-64) = 7.2.27-1.el7.remi for package: php-7.2.27-1.el7.remi.x86_64
--> Processing Dependency: httpd for package: php-7.2.27-1.el7.remi.x86_64
--> Processing Dependency: libargon2.so.0()(64bit) for package: php-7.2.27-1.el7.remi.x86_64
---> Package php-fpm.x86_64 0:7.2.27-1.el7.remi will be installed
---> Package php-mbstring.x86_64 0:7.2.27-1.el7.remi will be installed
--> Processing Dependency: libonig.so.5()(64bit) for package: php-mbstring-7.2.27-1.el7.remi.x86_64
---> Package php-mysqlnd.x86_64 0:7.2.27-1.el7.remi will be installed
--> Processing Dependency: php-pdo(x86-64) = 7.2.27-1.el7.remi for package: php-mysqlnd-7.2.27-1.el7.remi.x86_64
---> Package php-pear.noarch 1:1.10.10-4.el7.remi will be installed
--> Processing Dependency: php-composer(fedora/autoloader) for package: 1:php-pear-1.10.10-4.el7.remi.noarch
--> Processing Dependency: php-posix for package: 1:php-pear-1.10.10-4.el7.remi.noarch
--> Processing Dependency: php-xml for package: 1:php-pear-1.10.10-4.el7.remi.noarch
---> Package php-pecl-mcrypt.x86_64 0:1.0.3-1.el7.remi.7.2 will be installed
--> Processing Dependency: libmcrypt.so.4()(64bit) for package: php-pecl-mcrypt-1.0.3-1.el7.remi.7.2.x86_64
--> Running transaction check
---> Package httpd.x86_64 0:2.4.6-90.el7.centos will be installed
--> Processing Dependency: httpd-tools = 2.4.6-90.el7.centos for package: httpd-2.4.6-90.el7.centos.x86_64
--> Processing Dependency: system-logos >= 7.92.1-1 for package: httpd-2.4.6-90.el7.centos.x86_64
--> Processing Dependency: /etc/mime.types for package: httpd-2.4.6-90.el7.centos.x86_64
--> Processing Dependency: libaprutil-1.so.0()(64bit) for package: httpd-2.4.6-90.el7.centos.x86_64
--> Processing Dependency: libapr-1.so.0()(64bit) for package: httpd-2.4.6-90.el7.centos.x86_64
---> Package libargon2.x86_64 0:20161029-3.el7 will be installed
---> Package libmcrypt.x86_64 0:2.5.8-13.el7 will be installed
---> Package oniguruma5.x86_64 0:6.9.4-1.el7.remi will be installed
---> Package php-cli.x86_64 0:7.2.27-1.el7.remi will be installed
---> Package php-common.x86_64 0:7.2.27-1.el7.remi will be installed
--> Processing Dependency: php-json(x86-64) = 7.2.27-1.el7.remi for package: php-common-7.2.27-1.el7.remi.x86_64
---> Package php-fedora-autoloader.noarch 0:1.0.0-1.el7 will be installed
---> Package php-pdo.x86_64 0:7.2.27-1.el7.remi will be installed
---> Package php-process.x86_64 0:7.2.27-1.el7.remi will be installed
---> Package php-xml.x86_64 0:7.2.27-1.el7.remi will be installed
--> Processing Dependency: libxslt.so.1(LIBXML2_1.0.11)(64bit) for package: php-xml-7.2.27-1.el7.remi.x86_64
--> Processing Dependency: libxslt.so.1(LIBXML2_1.0.13)(64bit) for package: php-xml-7.2.27-1.el7.remi.x86_64
--> Processing Dependency: libxslt.so.1(LIBXML2_1.0.18)(64bit) for package: php-xml-7.2.27-1.el7.remi.x86_64
--> Processing Dependency: libxslt.so.1(LIBXML2_1.0.22)(64bit) for package: php-xml-7.2.27-1.el7.remi.x86_64
--> Processing Dependency: libxslt.so.1(LIBXML2_1.0.24)(64bit) for package: php-xml-7.2.27-1.el7.remi.x86_64
--> Processing Dependency: libexslt.so.0()(64bit) for package: php-xml-7.2.27-1.el7.remi.x86_64
--> Processing Dependency: libxslt.so.1()(64bit) for package: php-xml-7.2.27-1.el7.remi.x86_64
--> Running transaction check
---> Package apr.x86_64 0:1.4.8-5.el7 will be installed
---> Package apr-util.x86_64 0:1.5.2-6.el7 will be installed
---> Package centos-logos.noarch 0:70.0.6-3.el7.centos will be installed
---> Package httpd-tools.x86_64 0:2.4.6-90.el7.centos will be installed
---> Package libxslt.x86_64 0:1.1.28-5.el7 will be installed
---> Package mailcap.noarch 0:2.1.41-2.el7 will be installed
---> Package php-json.x86_64 0:7.2.27-1.el7.remi will be installed
--> Finished Dependency Resolution

Dependencies Resolved

=============================================================================================================================================================
 Package                                     Arch                         Version                                     Repository                        Size
=============================================================================================================================================================
Installing:
 php                                         x86_64                       7.2.27-1.el7.remi                           remi-php72                       3.2 M
 php-fpm                                     x86_64                       7.2.27-1.el7.remi                           remi-php72                       1.7 M
 php-mbstring                                x86_64                       7.2.27-1.el7.remi                           remi-php72                       496 k
 php-mysqlnd                                 x86_64                       7.2.27-1.el7.remi                           remi-php72                       236 k
 php-pear                                    noarch                       1:1.10.10-4.el7.remi                        remi-php72                       361 k
 php-pecl-mcrypt                             x86_64                       1.0.3-1.el7.remi.7.2                        remi-php72                        30 k
Installing for dependencies:
 apr                                         x86_64                       1.4.8-5.el7                                 base                             103 k
 apr-util                                    x86_64                       1.5.2-6.el7                                 base                              92 k
 centos-logos                                noarch                       70.0.6-3.el7.centos                         base                              21 M
 httpd                                       x86_64                       2.4.6-90.el7.centos                         base                             2.7 M
 httpd-tools                                 x86_64                       2.4.6-90.el7.centos                         base                              91 k
 libargon2                                   x86_64                       20161029-3.el7                              epel                              23 k
 libmcrypt                                   x86_64                       2.5.8-13.el7                                epel                              99 k
 libxslt                                     x86_64                       1.1.28-5.el7                                base                             242 k
 mailcap                                     noarch                       2.1.41-2.el7                                base                              31 k
 oniguruma5                                  x86_64                       6.9.4-1.el7.remi                            remi-safe                        197 k
 php-cli                                     x86_64                       7.2.27-1.el7.remi                           remi-php72                       4.8 M
 php-common                                  x86_64                       7.2.27-1.el7.remi                           remi-php72                       1.1 M
 php-fedora-autoloader                       noarch                       1.0.0-1.el7                                 epel                             9.6 k
 php-json                                    x86_64                       7.2.27-1.el7.remi                           remi-php72                        66 k
 php-pdo                                     x86_64                       7.2.27-1.el7.remi                           remi-php72                       128 k
 php-process                                 x86_64                       7.2.27-1.el7.remi                           remi-php72                        83 k
 php-xml                                     x86_64                       7.2.27-1.el7.remi                           remi-php72                       209 k

Transaction Summary
=============================================================================================================================================================
Install  6 Packages (+17 Dependent packages)

Total download size: 37 M
Installed size: 82 M
Downloading packages:
(1/23): apr-1.4.8-5.el7.x86_64.rpm                                                                                                    | 103 kB  00:00:00
(2/23): centos-logos-70.0.6-3.el7.centos.noarch.rpm                                                                                   |  21 MB  00:00:00
(3/23): apr-util-1.5.2-6.el7.x86_64.rpm                                                                                               |  92 kB  00:00:01
(4/23): httpd-2.4.6-90.el7.centos.x86_64.rpm                                                                                          | 2.7 MB  00:00:00
(5/23): libxslt-1.1.28-5.el7.x86_64.rpm                                                                                               | 242 kB  00:00:00
(6/23): mailcap-2.1.41-2.el7.noarch.rpm                                                                                               |  31 kB  00:00:00
(7/23): httpd-tools-2.4.6-90.el7.centos.x86_64.rpm                                                                                    |  91 kB  00:00:00
(8/23): libargon2-20161029-3.el7.x86_64.rpm                                                                                           |  23 kB  00:00:00
(9/23): libmcrypt-2.5.8-13.el7.x86_64.rpm                                                                                             |  99 kB  00:00:00
warning: /var/cache/yum/x86_64/7/remi-safe/packages/oniguruma5-6.9.4-1.el7.remi.x86_64.rpm: Header V4 DSA/SHA1 Signature, key ID 00f97f56: NOKEY
Public key for oniguruma5-6.9.4-1.el7.remi.x86_64.rpm is not installed
(10/23): oniguruma5-6.9.4-1.el7.remi.x86_64.rpm                                                                                       | 197 kB  00:00:00
Public key for php-cli-7.2.27-1.el7.remi.x86_64.rpm is not installed[=========================================             ]  12 MB/s |  28 MB  00:00:00 ETA
(11/23): php-cli-7.2.27-1.el7.remi.x86_64.rpm                                                                                         | 4.8 MB  00:00:00
(12/23): php-7.2.27-1.el7.remi.x86_64.rpm                                                                                             | 3.2 MB  00:00:00
(13/23): php-fedora-autoloader-1.0.0-1.el7.noarch.rpm                                                                                 | 9.6 kB  00:00:00
(14/23): php-common-7.2.27-1.el7.remi.x86_64.rpm                                                                                      | 1.1 MB  00:00:00
(15/23): php-json-7.2.27-1.el7.remi.x86_64.rpm                                                                                        |  66 kB  00:00:00
(16/23): php-mbstring-7.2.27-1.el7.remi.x86_64.rpm                                                                                    | 496 kB  00:00:00
(17/23): php-fpm-7.2.27-1.el7.remi.x86_64.rpm                                                                                         | 1.7 MB  00:00:00
(18/23): php-mysqlnd-7.2.27-1.el7.remi.x86_64.rpm                                                                                     | 236 kB  00:00:00
(19/23): php-pdo-7.2.27-1.el7.remi.x86_64.rpm                                                                                         | 128 kB  00:00:00
(20/23): php-pear-1.10.10-4.el7.remi.noarch.rpm                                                                                       | 361 kB  00:00:00
(21/23): php-process-7.2.27-1.el7.remi.x86_64.rpm                                                                                     |  83 kB  00:00:00
(22/23): php-pecl-mcrypt-1.0.3-1.el7.remi.7.2.x86_64.rpm                                                                              |  30 kB  00:00:00
(23/23): php-xml-7.2.27-1.el7.remi.x86_64.rpm                                                                                         | 209 kB  00:00:00
-------------------------------------------------------------------------------------------------------------------------------------------------------------
Total                                                                                                                         16 MB/s |  37 MB  00:00:02
Retrieving key from file:///etc/pki/rpm-gpg/RPM-GPG-KEY-remi
Importing GPG key 0x00F97F56:
 Userid     : "Remi Collet <RPMS@FamilleCollet.com>"
 Fingerprint: 1ee0 4cce 88a4 ae4a a29a 5df5 004e 6f47 00f9 7f56
 Package    : remi-release-7.7-1.el7.remi.noarch (installed)
 From       : /etc/pki/rpm-gpg/RPM-GPG-KEY-remi
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  Installing : libargon2-20161029-3.el7.x86_64                                                                                                          1/23
  Installing : apr-1.4.8-5.el7.x86_64                                                                                                                   2/23
  Installing : apr-util-1.5.2-6.el7.x86_64                                                                                                              3/23
  Installing : httpd-tools-2.4.6-90.el7.centos.x86_64                                                                                                   4/23
  Installing : php-common-7.2.27-1.el7.remi.x86_64                                                                                                      5/23
  Installing : php-json-7.2.27-1.el7.remi.x86_64                                                                                                        6/23
  Installing : php-cli-7.2.27-1.el7.remi.x86_64                                                                                                         7/23
  Installing : php-fedora-autoloader-1.0.0-1.el7.noarch                                                                                                 8/23
  Installing : php-pdo-7.2.27-1.el7.remi.x86_64                                                                                                         9/23
  Installing : php-process-7.2.27-1.el7.remi.x86_64                                                                                                    10/23
  Installing : oniguruma5-6.9.4-1.el7.remi.x86_64                                                                                                      11/23
  Installing : libxslt-1.1.28-5.el7.x86_64                                                                                                             12/23
  Installing : php-xml-7.2.27-1.el7.remi.x86_64                                                                                                        13/23
  Installing : centos-logos-70.0.6-3.el7.centos.noarch                                                                                                 14/23
  Installing : libmcrypt-2.5.8-13.el7.x86_64                                                                                                           15/23
  Installing : mailcap-2.1.41-2.el7.noarch                                                                                                             16/23
  Installing : httpd-2.4.6-90.el7.centos.x86_64                                                                                                        17/23
  Installing : php-7.2.27-1.el7.remi.x86_64                                                                                                            18/23
  Installing : php-pecl-mcrypt-1.0.3-1.el7.remi.7.2.x86_64                                                                                             19/23
  Installing : 1:php-pear-1.10.10-4.el7.remi.noarch                                                                                                    20/23
  Installing : php-mbstring-7.2.27-1.el7.remi.x86_64                                                                                                   21/23
  Installing : php-mysqlnd-7.2.27-1.el7.remi.x86_64                                                                                                    22/23
  Installing : php-fpm-7.2.27-1.el7.remi.x86_64                                                                                                        23/23
  Verifying  : mailcap-2.1.41-2.el7.noarch                                                                                                              1/23
  Verifying  : httpd-tools-2.4.6-90.el7.centos.x86_64                                                                                                   2/23
  Verifying  : php-fedora-autoloader-1.0.0-1.el7.noarch                                                                                                 3/23
  Verifying  : httpd-2.4.6-90.el7.centos.x86_64                                                                                                         4/23
  Verifying  : apr-1.4.8-5.el7.x86_64                                                                                                                   5/23
  Verifying  : libargon2-20161029-3.el7.x86_64                                                                                                          6/23
  Verifying  : php-fpm-7.2.27-1.el7.remi.x86_64                                                                                                         7/23
  Verifying  : libmcrypt-2.5.8-13.el7.x86_64                                                                                                            8/23
  Verifying  : centos-logos-70.0.6-3.el7.centos.noarch                                                                                                  9/23
  Verifying  : php-mbstring-7.2.27-1.el7.remi.x86_64                                                                                                   10/23
  Verifying  : php-pdo-7.2.27-1.el7.remi.x86_64                                                                                                        11/23
  Verifying  : php-json-7.2.27-1.el7.remi.x86_64                                                                                                       12/23
  Verifying  : php-process-7.2.27-1.el7.remi.x86_64                                                                                                    13/23
  Verifying  : php-common-7.2.27-1.el7.remi.x86_64                                                                                                     14/23
  Verifying  : php-cli-7.2.27-1.el7.remi.x86_64                                                                                                        15/23
  Verifying  : libxslt-1.1.28-5.el7.x86_64                                                                                                             16/23
  Verifying  : apr-util-1.5.2-6.el7.x86_64                                                                                                             17/23
  Verifying  : php-pecl-mcrypt-1.0.3-1.el7.remi.7.2.x86_64                                                                                             18/23
  Verifying  : php-mysqlnd-7.2.27-1.el7.remi.x86_64                                                                                                    19/23
  Verifying  : php-xml-7.2.27-1.el7.remi.x86_64                                                                                                        20/23
  Verifying  : oniguruma5-6.9.4-1.el7.remi.x86_64                                                                                                      21/23
  Verifying  : php-7.2.27-1.el7.remi.x86_64                                                                                                            22/23
  Verifying  : 1:php-pear-1.10.10-4.el7.remi.noarch                                                                                                    23/23

Installed:
  php.x86_64 0:7.2.27-1.el7.remi                    php-fpm.x86_64 0:7.2.27-1.el7.remi              php-mbstring.x86_64 0:7.2.27-1.el7.remi
  php-mysqlnd.x86_64 0:7.2.27-1.el7.remi            php-pear.noarch 1:1.10.10-4.el7.remi            php-pecl-mcrypt.x86_64 0:1.0.3-1.el7.remi.7.2

Dependency Installed:
  apr.x86_64 0:1.4.8-5.el7                             apr-util.x86_64 0:1.5.2-6.el7                      centos-logos.noarch 0:70.0.6-3.el7.centos
  httpd.x86_64 0:2.4.6-90.el7.centos                   httpd-tools.x86_64 0:2.4.6-90.el7.centos           libargon2.x86_64 0:20161029-3.el7
  libmcrypt.x86_64 0:2.5.8-13.el7                      libxslt.x86_64 0:1.1.28-5.el7                      mailcap.noarch 0:2.1.41-2.el7
  oniguruma5.x86_64 0:6.9.4-1.el7.remi                 php-cli.x86_64 0:7.2.27-1.el7.remi                 php-common.x86_64 0:7.2.27-1.el7.remi
  php-fedora-autoloader.noarch 0:1.0.0-1.el7           php-json.x86_64 0:7.2.27-1.el7.remi                php-pdo.x86_64 0:7.2.27-1.el7.remi
  php-process.x86_64 0:7.2.27-1.el7.remi               php-xml.x86_64 0:7.2.27-1.el7.remi

Complete!
```

2.phpのバージョン確認

```
# php -v
PHP 7.2.27 (cli) (built: Jan 22 2020 09:31:55) ( NTS )
Copyright (c) 1997-2018 The PHP Group
Zend Engine v3.2.0, Copyright (c) 1998-2018 Zend Technologies
```

3.php-fpm設定

{{< accordion >}}
<div>
<pre>
# cp -p /etc/php-fpm.d/www.conf /etc/php-fpm.d/www.conf.org
</pre>

<pre>
# vim /etc/php-fpm.d/www.conf

---------------------以下赤字の内容に設定変更-------------------------------
・
・省略
・
; Unix user/group of processes
; Note: The user is mandatory. If the group is not set, the default user's group
;       will be used.
; RPM: apache user chosen to provide access to the same directories as httpd
user = nginx <font color="Red">//←「apache」変更⇒「nginx」</font>
; RPM: Keep a group allowed to write in log dir.
group = nginx <font color="Red">//←「apache」変更⇒「nginx」</font>
・
・省略
・
---------------------[Esc + :wq]で保存終了します。-------------------------
</pre>
</div>
{{< /accordion >}}

4.php-fpmの自動起動設定

```
# systemctl enable php-fpm
Created symlink from /etc/systemd/system/multi-user.target.wants/php-fpm.service
```

```
# systemctl list-unit-files --type=service | grep php-fpm
php-fpm.service                               enabled    
```

5.php-fpmの起動

```
# systemctl start php-fpm
```

```
# systemctl status php-fpm
● php-fpm.service - The PHP FastCGI Process Manager
   Loaded: loaded (/usr/lib/systemd/system/php-fpm.service; enabled; vendor preset: disabled)
   Active: active (running) since Wed 2020-02-12 14:23:59 KST; 31s ago
 Main PID: 25222 (php-fpm)
   Status: "Processes active: 0, idle: 5, Requests: 0, slow: 0, Traffic: 0req/sec"
   CGroup: /system.slice/php-fpm.service
           tq25222 php-fpm: master process (/etc/php-fpm.conf)
           tq25223 php-fpm: pool www
           tq25224 php-fpm: pool www
           tq25225 php-fpm: pool www
           tq25226 php-fpm: pool www
           mq25227 php-fpm: pool www
```