---
title: "1.WordPress Environment Construction - Nginx"
date: 2017-10-17T15:26:15Z
draft: false
weight: 10
---

## Nginxのインストール手順

1.epelリポジトリの設定

```
# yum -y install epel-release
Loaded plugins: fastestmirror
Determining fastest mirrors
epel/x86_64/metalink                                     | 8.4 kB     00:00
 * epel: ftp.jaist.ac.jp
base                                                     | 3.6 kB     00:00
epel                                                     | 5.3 kB     00:00
extras                                                   | 2.9 kB     00:00
updates                                                  | 2.9 kB     00:00
(1/7): epel/x86_64/group_gz                                |  90 kB   00:00
(2/7): epel/x86_64/updateinfo                              | 1.0 MB   00:00
(3/7): epel/x86_64/primary_db                              | 6.9 MB   00:01
(4/7): updates/7/x86_64/primary_db                         | 6.7 MB   00:01
(5/7): base/7/x86_64/group_gz                              | 165 kB   00:01
(6/7): extras/7/x86_64/primary_db                          | 159 kB   00:02
(7/7): base/7/x86_64/primary_db                            | 6.0 MB   00:05
Resolving Dependencies
--> Running transaction check
---> Package epel-release.noarch 0:7-11 will be updated
---> Package epel-release.noarch 0:7-12 will be an update
--> Finished Dependency Resolution

Dependencies Resolved

================================================================================
 Package                Arch             Version           Repository      Size
================================================================================
Updating:
 epel-release           noarch           7-12              epel            15 k

Transaction Summary
================================================================================
Upgrade  1 Package

Total download size: 15 k
Downloading packages:
Delta RPMs disabled because /usr/bin/applydeltarpm not installed.
epel-release-7-12.noarch.rpm                               |  15 kB   00:00
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  Updating   : epel-release-7-12.noarch                                     1/2
  Cleanup    : epel-release-7-11.noarch                                     2/2
  Verifying  : epel-release-7-12.noarch                                     1/2
  Verifying  : epel-release-7-11.noarch                                     2/2

Updated:
  epel-release.noarch 0:7-12

Complete!
```

```
# rpm -ivh http://rpms.famillecollet.com/enterprise/remi-release-7.rpm
Retrieving http://rpms.famillecollet.com/enterprise/remi-release-7.rpm
warning: /var/tmp/rpm-tmp.TRn9Kd: Header V4 DSA/SHA1 Signature, key ID 00f97f56: NOKEY
Preparing...                          ################################# [100%]
Updating / installing...
   1:remi-release-7.7-1.el7.remi      ################################# [100%]
```

```
# vim /etc/yum.repos.d/nginx.repo

-------------以下をコピー&ペースト---------------------------------
[nginx]
name=nginx repo
baseurl=http://nginx.org/packages/mainline/centos/7/$basearch/
gpgcheck=0
enabled=0
-------------[Esc + :wq]で保存終了します。-------------------------
```

***

2.Nginxのインストール

```
# yum -y --enablerepo=nginx install nginx
Loaded plugins: fastestmirror
Loading mirror speeds from cached hostfile
 * epel: ftp.jaist.ac.jp
 * remi-safe: ftp.riken.jp
Resolving Dependencies
--> Running transaction check
---> Package nginx.x86_64 1:1.17.8-1.el7.ngx will be installed
--> Finished Dependency Resolution

Dependencies Resolved

================================================================================
 Package       Arch           Version                       Repository     Size
================================================================================
Installing:
 nginx         x86_64         1:1.17.8-1.el7.ngx            nginx         770 k

Transaction Summary
================================================================================
Install  1 Package

Total download size: 770 k
Installed size: 2.7 M
Downloading packages:
nginx-1.17.8-1.el7.ngx.x86_64.rpm                          | 770 kB   00:03
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
Warning: RPMDB altered outside of yum.
  Installing : 1:nginx-1.17.8-1.el7.ngx.x86_64                              1/1
----------------------------------------------------------------------

Thanks for using nginx!

Please find the official documentation for nginx here:
* http://nginx.org/en/docs/

Please subscribe to nginx-announce mailing list to get
the most important news about nginx:
* http://nginx.org/en/support.html

Commercial subscriptions for nginx are available on:
* http://nginx.com/products/

----------------------------------------------------------------------
  Verifying  : 1:nginx-1.17.8-1.el7.ngx.x86_64                              1/1

Installed:
  nginx.x86_64 1:1.17.8-1.el7.ngx

Complete!
```

3.Nginxの自動起動設定

```
# systemctl enable nginx
Created symlink from /etc/systemd/system/multi-user.target.wants/nginx.service to /usr/lib/systemd/system/nginx.service.
```

```
# systemctl list-unit-files --type=service | grep nginx
nginx-debug.service                           disabled
nginx.service                                 enabled
```

4.Nginxの起動

```
# systemctl start nginx
```

```
# systemctl status nginx
● nginx.service - nginx - high performance web server
   Loaded: loaded (/usr/lib/systemd/system/nginx.service; enabled; vendor preset: disabled)
   Active: active (running) since Wed 2020-02-12 13:30:11 KST; 4min 29s ago
     Docs: http://nginx.org/en/docs/
  Process: 11471 ExecStart=/usr/sbin/nginx -c /etc/nginx/nginx.conf (code=exited, status=0/SUCCESS)
 Main PID: 11472 (nginx)
   CGroup: /system.slice/nginx.service
           tq11472 nginx: master process /usr/sbin/nginx -c /etc/nginx/nginx.conf
           mq11473 nginx: worker process

Feb 12 13:30:11 wordpress.novalocal systemd[1]: Starting nginx - high performance web server...
Feb 12 13:30:11 wordpress.novalocal systemd[1]: Started nginx - high performance web server.
```