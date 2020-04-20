---
title: "1.ECCUBE Environment Construction - Apache Web Server"
date: 2017-10-17T15:26:15Z
draft: false
weight: 10
---

## Apache Web Serverのインストール手順

1.httpdのインストール

```
# yum -y install httpd
Loaded plugins: fastestmirror
Determining fastest mirrors
epel/x86_64/metalink                                     | 5.9 kB     00:00
 * epel: nrt.edge.kernel.org
base                                                     | 3.6 kB     00:00
epel                                                     | 4.7 kB     00:00
extras                                                   | 2.9 kB     00:00
updates                                                  | 2.9 kB     00:00
(1/7): epel/x86_64/updateinfo                              | 1.0 MB   00:00
(2/7): epel/x86_64/group_gz                                |  95 kB   00:00
(3/7): epel/x86_64/primary_db                              | 6.8 MB   00:00
(4/7): base/7/x86_64/group_gz                              | 165 kB   00:00
(5/7): extras/7/x86_64/primary_db                          | 164 kB   00:01
(6/7): base/7/x86_64/primary_db                            | 6.0 MB   00:03
(7/7): updates/7/x86_64/primary_db                         | 7.6 MB   00:06
Resolving Dependencies
--> Running transaction check
---> Package httpd.x86_64 0:2.4.6-90.el7.centos will be installed
--> Processing Dependency: httpd-tools = 2.4.6-90.el7.centos for package: httpd-2.4.6-90.el7.centos.x86_64
--> Processing Dependency: system-logos >= 7.92.1-1 for package: httpd-2.4.6-90.el7.centos.x86_64
--> Processing Dependency: /etc/mime.types for package: httpd-2.4.6-90.el7.centos.x86_64
--> Processing Dependency: libaprutil-1.so.0()(64bit) for package: httpd-2.4.6-90.el7.centos.x86_64
--> Processing Dependency: libapr-1.so.0()(64bit) for package: httpd-2.4.6-90.el7.centos.x86_64
--> Running transaction check
---> Package apr.x86_64 0:1.4.8-5.el7 will be installed
---> Package apr-util.x86_64 0:1.5.2-6.el7 will be installed
---> Package centos-logos.noarch 0:70.0.6-3.el7.centos will be installed
---> Package httpd-tools.x86_64 0:2.4.6-90.el7.centos will be installed
---> Package mailcap.noarch 0:2.1.41-2.el7 will be installed
--> Finished Dependency Resolution

Dependencies Resolved

================================================================================
 Package             Arch          Version                    Repository   Size
================================================================================
Installing:
 httpd               x86_64        2.4.6-90.el7.centos        base        2.7 M
Installing for dependencies:
 apr                 x86_64        1.4.8-5.el7                base        103 k
 apr-util            x86_64        1.5.2-6.el7                base         92 k
 centos-logos        noarch        70.0.6-3.el7.centos        base         21 M
 httpd-tools         x86_64        2.4.6-90.el7.centos        base         91 k
 mailcap             noarch        2.1.41-2.el7               base         31 k

Transaction Summary
================================================================================
Install  1 Package (+5 Dependent packages)

Total download size: 24 M
Installed size: 31 M
Downloading packages:
(1/6): apr-util-1.5.2-6.el7.x86_64.rpm                     |  92 kB   00:00
(2/6): apr-1.4.8-5.el7.x86_64.rpm                          | 103 kB   00:00
(3/6): httpd-2.4.6-90.el7.centos.x86_64.rpm                | 2.7 MB   00:03
(4/6): httpd-tools-2.4.6-90.el7.centos.x86_64.rpm          |  91 kB   00:00
(5/6): mailcap-2.1.41-2.el7.noarch.rpm                     |  31 kB   00:00
(6/6): centos-logos-70.0.6-3.el7.centos.noarch.rpm         |  21 MB   00:36
--------------------------------------------------------------------------------
Total                                              679 kB/s |  24 MB  00:36
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  Installing : apr-1.4.8-5.el7.x86_64                                       1/6
  Installing : apr-util-1.5.2-6.el7.x86_64                                  2/6
  Installing : httpd-tools-2.4.6-90.el7.centos.x86_64                       3/6
  Installing : centos-logos-70.0.6-3.el7.centos.noarch                      4/6
  Installing : mailcap-2.1.41-2.el7.noarch                                  5/6
  Installing : httpd-2.4.6-90.el7.centos.x86_64                             6/6
  Verifying  : mailcap-2.1.41-2.el7.noarch                                  1/6
  Verifying  : httpd-tools-2.4.6-90.el7.centos.x86_64                       2/6
  Verifying  : apr-util-1.5.2-6.el7.x86_64                                  3/6
  Verifying  : httpd-2.4.6-90.el7.centos.x86_64                             4/6
  Verifying  : apr-1.4.8-5.el7.x86_64                                       5/6
  Verifying  : centos-logos-70.0.6-3.el7.centos.noarch                      6/6

Installed:
  httpd.x86_64 0:2.4.6-90.el7.centos

Dependency Installed:
  apr.x86_64 0:1.4.8-5.el7
  apr-util.x86_64 0:1.5.2-6.el7
  centos-logos.noarch 0:70.0.6-3.el7.centos
  httpd-tools.x86_64 0:2.4.6-90.el7.centos
  mailcap.noarch 0:2.1.41-2.el7

Complete!
```

2.httpdのバージョン確認

```
# httpd -v
Server version: Apache/2.4.6 (CentOS)
Server built:   Aug  8 2019 11:41:18
```

3.httpdの自動起動設定

```
# systemctl enable httpd
Created symlink from /etc/systemd/system/multi-user.target.wants/httpd.service to /usr/lib/systemd/system/httpd.service.
```

```
# systemctl list-unit-files --type=service | grep httpd
  httpd.service                                 enabled
```

4.httpdの起動

```
# systemctl start httpd
```

```
# systemctl status httpd
  ● httpd.service - The Apache HTTP Server
  Loaded: loaded (/usr/lib/systemd/system/httpd.service; enabled; vendor preset: disabled)
  Active: active (running) since Tue 2020-03-31 14:25:09 JST; 9s ago
    Docs: man:httpd(8)
          man:apachectl(8)
Main PID: 10671 (httpd)
  Status: "Total requests: 0; Current requests/sec: 0; Current traffic:   0 B/sec"
  CGroup: /system.slice/httpd.service
          tq10671 /usr/sbin/httpd -DFOREGROUND
          tq10672 /usr/sbin/httpd -DFOREGROUND
          tq10673 /usr/sbin/httpd -DFOREGROUND
          tq10674 /usr/sbin/httpd -DFOREGROUND
          tq10675 /usr/sbin/httpd -DFOREGROUND
          mq10676 /usr/sbin/httpd -DFOREGROUND

Mar 31 14:25:09 centos.novalocal systemd[1]: Starting The Apache HTTP Server...
Mar 31 14:25:09 centos.novalocal systemd[1]: Started The Apache HTTP Server.
Hint: Some lines were ellipsized, use -l to show in full.
```

5.Apacheの設定変更

{{< accordion >}}
<div>
<pre>
# cp -p /etc/httpd/conf/httpd.conf /etc/httpd/conf/httpd.conf.org
</pre>

<pre>
# vim /etc/httpd/conf/httpd.conf

-----------------------------以下赤字の内容に設定変更-------------------------------
・
・省略
・
#
# AllowOverride controls what directives may be placed in .htaccess files.
# It can be "All", "None", or any combination of the keywords:
#   Options FileInfo AuthConfig Limit
#
AllowOverride All <font color="Red">//←「AllowOverride None」変更⇒「AllowOverride All」</font>
・
・省略
・
-----------------------------[Esc + :wq]で保存終了します。-------------------------
</pre>

<pre>
# systemctl reload httpd
</pre>
</div>
{{< /accordion >}}

