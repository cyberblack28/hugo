---
title: "1.ECCUBE Environment Construction - MariaDB"
date: 2017-10-17T15:26:15Z
draft: false
weight: 10
---

## MariaDBのインストール手順

1.mariadbのインストール

```
# yum -y install mariadb mariadb-server
Loaded plugins: fastestmirror
Loading mirror speeds from cached hostfile
 * epel: nrt.edge.kernel.org
 * remi-safe: ftp.riken.jp
Resolving Dependencies
--> Running transaction check
---> Package mariadb.x86_64 1:5.5.64-1.el7 will be installed
--> Processing Dependency: mariadb-libs(x86-64) = 1:5.5.64-1.el7 for package: 1:mariadb-5.5.64-1.el7.x86_64
---> Package mariadb-server.x86_64 1:5.5.64-1.el7 will be installed
--> Processing Dependency: perl-DBI for package: 1:mariadb-server-5.5.64-1.el7.x86_64
--> Processing Dependency: perl-DBD-MySQL for package: 1:mariadb-server-5.5.64-1.el7.x86_64
--> Processing Dependency: perl(DBI) for package: 1:mariadb-server-5.5.64-1.el7.x86_64
--> Processing Dependency: libaio.so.1(LIBAIO_0.4)(64bit) for package: 1:mariadb-server-5.5.64-1.el7.x86_64
--> Processing Dependency: libaio.so.1(LIBAIO_0.1)(64bit) for package: 1:mariadb-server-5.5.64-1.el7.x86_64
--> Processing Dependency: libaio.so.1()(64bit) for package: 1:mariadb-server-5.5.64-1.el7.x86_64
--> Running transaction check
---> Package libaio.x86_64 0:0.3.109-13.el7 will be installed
---> Package mariadb-libs.x86_64 1:5.5.60-1.el7_5 will be updated
---> Package mariadb-libs.x86_64 1:5.5.64-1.el7 will be an update
---> Package perl-DBD-MySQL.x86_64 0:4.023-6.el7 will be installed
---> Package perl-DBI.x86_64 0:1.627-4.el7 will be installed
--> Processing Dependency: perl(RPC::PlServer) >= 0.2001 for package: perl-DBI-1.627-4.el7.x86_64
--> Processing Dependency: perl(RPC::PlClient) >= 0.2000 for package: perl-DBI-1.627-4.el7.x86_64
--> Running transaction check
---> Package perl-PlRPC.noarch 0:0.2020-14.el7 will be installed
--> Processing Dependency: perl(Net::Daemon) >= 0.13 for package: perl-PlRPC-0.2020-14.el7.noarch
--> Processing Dependency: perl(Net::Daemon::Test) for package: perl-PlRPC-0.2020-14.el7.noarch
--> Processing Dependency: perl(Net::Daemon::Log) for package: perl-PlRPC-0.2020-14.el7.noarch
--> Processing Dependency: perl(Compress::Zlib) for package: perl-PlRPC-0.2020-14.el7.noarch
--> Running transaction check
---> Package perl-IO-Compress.noarch 0:2.061-2.el7 will be installed
--> Processing Dependency: perl(Compress::Raw::Zlib) >= 2.061 for package: perl-IO-Compress-2.061-2.el7.noarch
--> Processing Dependency: perl(Compress::Raw::Bzip2) >= 2.061 for package: perl-IO-Compress-2.061-2.el7.noarch
---> Package perl-Net-Daemon.noarch 0:0.48-5.el7 will be installed
--> Running transaction check
---> Package perl-Compress-Raw-Bzip2.x86_64 0:2.061-3.el7 will be installed
---> Package perl-Compress-Raw-Zlib.x86_64 1:2.061-4.el7 will be installed
--> Finished Dependency Resolution

Dependencies Resolved

================================================================================
 Package                      Arch        Version               Repository
                                                                           Size
================================================================================
Installing:
 mariadb                      x86_64      1:5.5.64-1.el7        base      8.7 M
 mariadb-server               x86_64      1:5.5.64-1.el7        base       11 M
Installing for dependencies:
 libaio                       x86_64      0.3.109-13.el7        base       24 k
 perl-Compress-Raw-Bzip2      x86_64      2.061-3.el7           base       32 k
 perl-Compress-Raw-Zlib       x86_64      1:2.061-4.el7         base       57 k
 perl-DBD-MySQL               x86_64      4.023-6.el7           base      140 k
 perl-DBI                     x86_64      1.627-4.el7           base      802 k
 perl-IO-Compress             noarch      2.061-2.el7           base      260 k
 perl-Net-Daemon              noarch      0.48-5.el7            base       51 k
 perl-PlRPC                   noarch      0.2020-14.el7         base       36 k
Updating for dependencies:
 mariadb-libs                 x86_64      1:5.5.64-1.el7        base      759 k

Transaction Summary
================================================================================
Install  2 Packages (+8 Dependent packages)
Upgrade             ( 1 Dependent package)

Total download size: 22 M
Downloading packages:
Delta RPMs disabled because /usr/bin/applydeltarpm not installed.
(1/11): libaio-0.3.109-13.el7.x86_64.rpm                   |  24 kB   00:01
(2/11): mariadb-libs-5.5.64-1.el7.x86_64.rpm               | 759 kB   00:00
(3/11): mariadb-server-5.5.64-1.el7.x86_64.rpm             |  11 MB   00:00
(4/11): perl-Compress-Raw-Bzip2-2.061-3.el7.x86_64.rpm     |  32 kB   00:00
(5/11): perl-Compress-Raw-Zlib-2.061-4.el7.x86_64.rpm      |  57 kB   00:00
(6/11): perl-DBD-MySQL-4.023-6.el7.x86_64.rpm              | 140 kB   00:00
(7/11): perl-DBI-1.627-4.el7.x86_64.rpm                    | 802 kB   00:00
(8/11): perl-IO-Compress-2.061-2.el7.noarch.rpm            | 260 kB   00:00
(9/11): perl-Net-Daemon-0.48-5.el7.noarch.rpm              |  51 kB   00:00
(10/11): perl-PlRPC-0.2020-14.el7.noarch.rpm               |  36 kB   00:00
(11/11): mariadb-5.5.64-1.el7.x86_64.rpm                   | 8.7 MB   07:16
--------------------------------------------------------------------------------
Total                                               52 kB/s |  22 MB  07:16
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  Updating   : 1:mariadb-libs-5.5.64-1.el7.x86_64                          1/12
  Installing : 1:mariadb-5.5.64-1.el7.x86_64                               2/12
  Installing : libaio-0.3.109-13.el7.x86_64                                3/12
  Installing : 1:perl-Compress-Raw-Zlib-2.061-4.el7.x86_64                 4/12
  Installing : perl-Net-Daemon-0.48-5.el7.noarch                           5/12
  Installing : perl-Compress-Raw-Bzip2-2.061-3.el7.x86_64                  6/12
  Installing : perl-IO-Compress-2.061-2.el7.noarch                         7/12
  Installing : perl-PlRPC-0.2020-14.el7.noarch                             8/12
  Installing : perl-DBI-1.627-4.el7.x86_64                                 9/12
  Installing : perl-DBD-MySQL-4.023-6.el7.x86_64                          10/12
  Installing : 1:mariadb-server-5.5.64-1.el7.x86_64                       11/12
  Cleanup    : 1:mariadb-libs-5.5.60-1.el7_5.x86_64                       12/12
  Verifying  : 1:mariadb-libs-5.5.64-1.el7.x86_64                          1/12
  Verifying  : perl-Compress-Raw-Bzip2-2.061-3.el7.x86_64                  2/12
  Verifying  : perl-Net-Daemon-0.48-5.el7.noarch                           3/12
  Verifying  : 1:mariadb-5.5.64-1.el7.x86_64                               4/12
  Verifying  : perl-DBD-MySQL-4.023-6.el7.x86_64                           5/12
  Verifying  : 1:perl-Compress-Raw-Zlib-2.061-4.el7.x86_64                 6/12
  Verifying  : 1:mariadb-server-5.5.64-1.el7.x86_64                        7/12
  Verifying  : perl-DBI-1.627-4.el7.x86_64                                 8/12
  Verifying  : libaio-0.3.109-13.el7.x86_64                                9/12
  Verifying  : perl-PlRPC-0.2020-14.el7.noarch                            10/12
  Verifying  : perl-IO-Compress-2.061-2.el7.noarch                        11/12
  Verifying  : 1:mariadb-libs-5.5.60-1.el7_5.x86_64                       12/12

Installed:
  mariadb.x86_64 1:5.5.64-1.el7       mariadb-server.x86_64 1:5.5.64-1.el7

Dependency Installed:
  libaio.x86_64 0:0.3.109-13.el7
  perl-Compress-Raw-Bzip2.x86_64 0:2.061-3.el7
  perl-Compress-Raw-Zlib.x86_64 1:2.061-4.el7
  perl-DBD-MySQL.x86_64 0:4.023-6.el7
  perl-DBI.x86_64 0:1.627-4.el7
  perl-IO-Compress.noarch 0:2.061-2.el7
  perl-Net-Daemon.noarch 0:0.48-5.el7
  perl-PlRPC.noarch 0:0.2020-14.el7

Dependency Updated:
  mariadb-libs.x86_64 1:5.5.64-1.el7

Complete!
```

2.mariadbの自動起動設定

```
# systemctl enable mariadb
Created symlink from /etc/systemd/system/multi-user.target.wants/mariadb.service to /usr/lib/systemd/system/mariadb.service.
```

```
# systemctl list-unit-files --type=service | grep mariadb
mariadb.service                               enabled
```

3.mariadbの起動

```
# systemctl start mariadb
```

```
# systemctl status mariadb
● mariadb.service - MariaDB database server
   Loaded: loaded (/usr/lib/systemd/system/mariadb.service; enabled; vendor preset: disabled)
   Active: active (running) since Tue 2020-03-31 14:50:05 JST; 9s ago
  Process: 12212 ExecStartPost=/usr/libexec/mariadb-wait-ready $MAINPID (code=exited, status=0/SUCCESS)
  Process: 12121 ExecStartPre=/usr/libexec/mariadb-prepare-db-dir %n (code=exited, status=0/SUCCESS)
 Main PID: 12209 (mysqld_safe)
   CGroup: /system.slice/mariadb.service
           tq12209 /bin/sh /usr/bin/mysqld_safe --basedir=/usr
           mq12372 /usr/libexec/mysqld --basedir=/usr --datadir=/var/lib/mysq...

Mar 31 14:50:03 centos.novalocal mariadb-prepare-db-dir[12121]: See the Maria...
Mar 31 14:50:03 centos.novalocal mariadb-prepare-db-dir[12121]: MySQL manual ...
Mar 31 14:50:03 centos.novalocal mariadb-prepare-db-dir[12121]: Please report...
Mar 31 14:50:03 centos.novalocal mariadb-prepare-db-dir[12121]: The latest in...
Mar 31 14:50:03 centos.novalocal mariadb-prepare-db-dir[12121]: You can find ...
Mar 31 14:50:03 centos.novalocal mariadb-prepare-db-dir[12121]: http://dev.my...
Mar 31 14:50:03 centos.novalocal mariadb-prepare-db-dir[12121]: Consider join...
Mar 31 14:50:03 centos.novalocal mysqld_safe[12209]: 200331 14:50:03 mysqld_s...
Mar 31 14:50:03 centos.novalocal mysqld_safe[12209]: 200331 14:50:03 mysqld_s...
Mar 31 14:50:05 centos.novalocal systemd[1]: Started MariaDB database server.
Hint: Some lines were ellipsized, use -l to show in full.
```

4.mariadbのrootユーザのパスワード設定

```
# mysql -u root
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 2
Server version: 5.5.64-MariaDB MariaDB Server

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]>
```

```
MariaDB [(none)]> update mysql.user set password=password('mariadb123') where user = 'root';
Query OK, 4 rows affected (0.00 sec)
Rows matched: 4  Changed: 4  Warnings: 0
```

```
MariaDB [(none)]> FLUSH PRIVILEGES;
Query OK, 0 rows affected (0.00 sec)
```

```
MariaDB [(none)]> exit
Bye
```

5.EC-CUBE用データベース作成

{{< accordion >}}
<div>
<pre>
# mysql -u root -p
Enter password:mariadb123 <font color="">//←パスワード入力
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 3
Server version: 5.5.64-MariaDB MariaDB Server

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]>
</pre>

<pre>
# MariaDB [(none)]> CREATE DATABASE eccube;
Query OK, 1 row affected (0.00 sec)
</pre>

<pre>
# MariaDB [(none)]> GRANT ALL PRIVILEGES ON eccube.*TO 'eccube'@'localhost' IDENTIFIED BY 'eccube';
Query OK, 0 rows affected (0.01 sec)
</pre>

<pre>
# MariaDB [(none)]> FLUSH PRIVILEGES;
Query OK, 0 rows affected (0.00 sec)
</pre>

<pre>
# MariaDB [(none)]> exit
Bye
</pre>
</div>
{{< /accordion >}}
