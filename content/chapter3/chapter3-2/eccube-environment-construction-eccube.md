---
title: "4.ECCUBE Environment Construction - ECCUBE"
date: 2017-10-17T15:26:15Z
draft: false
weight: 10
---

## EC-CUBEのインストール手順

1.EC-CUBEのダウンロード

```
# cd /var/www/html
```

```
# wget http://downloads.ec-cube.net/src/eccube-4.0.3.zip
--2020-03-31 14:56:31--  http://downloads.ec-cube.net/src/eccube-4.0.3.zip
Resolving downloads.ec-cube.net (downloads.ec-cube.net)... 52.219.68.82
Connecting to downloads.ec-cube.net (downloads.ec-cube.net)|52.219.68.82|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 43604415 (42M) [application/zip]
Saving to: ‘eccube-4.0.3.zip’

100%[======================================>] 43,604,415  18.0MB/s   in 2.3s

2020-03-31 14:56:33 (18.0 MB/s) - ‘eccube-4.0.3.zip’ saved [43604415/43604415]
```

2.unzipコマンドのインストール、解凍、httpdの再起動

```
# yum -y install unzip
Loaded plugins: fastestmirror
Loading mirror speeds from cached hostfile
 * epel: nrt.edge.kernel.org
 * remi-safe: ftp.riken.jp
Resolving Dependencies
--> Running transaction check
---> Package unzip.x86_64 0:6.0-20.el7 will be installed
--> Finished Dependency Resolution

Dependencies Resolved

================================================================================
 Package          Arch              Version               Repository       Size
================================================================================
Installing:
 unzip            x86_64            6.0-20.el7            base            170 k

Transaction Summary
================================================================================
Install  1 Package

Total download size: 170 k
Installed size: 365 k
Downloading packages:
unzip-6.0-20.el7.x86_64.rpm                                | 170 kB   00:02
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  Installing : unzip-6.0-20.el7.x86_64                                      1/1
  Verifying  : unzip-6.0-20.el7.x86_64                                      1/1

Installed:
  unzip.x86_64 0:6.0-20.el7

Complete!
```

```
# unzip eccube-4.0.3.zip
・
・省略
・
  eccube-4.0.3/vendor/zendframework/zend-code/doc/book/index.md -> ../../README.md
#
```

```
# systemctl restart httpd
```

3.ブラウザを起動して「http://グローバルIPアドレス/eccube-4.0.3」にアクセス