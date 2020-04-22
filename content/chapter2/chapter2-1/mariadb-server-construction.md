---
title: "6.MariaDB Environment Construction"
date: 2017-10-17T15:26:15Z
draft: false
weight: 10
---

## 事前作業

1.studentユーザでログインして、rootユーザに変更します。

```
$ su -
パスワード:tokyoec
#
```

***

## 1.mariadbのインストール

CentOS8_WORDPRESSの仮想マシンで実行すること

1.mariadbのインストール

{{< accordion >}}
<div>
<pre>
# dnf -y install mariadb mariadb-server
メタデータの期限切れの最終確認: 0:27:42 時間前の 2020年02月06日 03時08分52秒 に 実施しました。
依存関係が解決しました。
================================================================================
 パッケージ      Arch   バージョン                              Repo      サイズ
================================================================================
インストール:
 mariadb         x86_64 3:10.3.17-1.module_el8.1.0+257+48736ea6 AppStream 6.1 M
 mariadb-server  x86_64 3:10.3.17-1.module_el8.1.0+257+48736ea6 AppStream  16 M
依存関係のインストール:
 mariadb-common  x86_64 3:10.3.17-1.module_el8.1.0+257+48736ea6 AppStream  62 k
 mariadb-connector-c
                 x86_64 3.0.7-1.el8                             AppStream 148 k
 mariadb-connector-c-config
                 noarch 3.0.7-1.el8                             AppStream  13 k
 mariadb-errmsg  x86_64 3:10.3.17-1.module_el8.1.0+257+48736ea6 AppStream 232 k
 perl-DBD-MySQL  x86_64 4.046-3.module_el8.1.0+203+e45423dc     AppStream 156 k
弱い依存関係のインストール:
 mariadb-backup  x86_64 3:10.3.17-1.module_el8.1.0+257+48736ea6 AppStream 6.0 M
 mariadb-gssapi-server
                 x86_64 3:10.3.17-1.module_el8.1.0+257+48736ea6 AppStream  49 k
 mariadb-server-utils
                 x86_64 3:10.3.17-1.module_el8.1.0+257+48736ea6 AppStream 1.6 M
モジュールストリームの有効化:
 mariadb                10.3
 perl-DBD-MySQL         4.046

トランザクションの概要
================================================================================
インストール  10 パッケージ

ダウンロードサイズの合計: 30 M
インストール済みのサイズ: 171 M
パッケージのダウンロード:
(1/10): mariadb-common-10.3.17-1.module_el8.1.0 438 kB/s |  62 kB     00:00
(2/10): mariadb-connector-c-3.0.7-1.el8.x86_64. 528 kB/s | 148 kB     00:00
(3/10): mariadb-connector-c-config-3.0.7-1.el8. 165 kB/s |  13 kB     00:00
(4/10): mariadb-backup-10.3.17-1.module_el8.1.0 4.5 MB/s | 6.0 MB     00:01
(5/10): mariadb-errmsg-10.3.17-1.module_el8.1.0 279 kB/s | 232 kB     00:00
(6/10): mariadb-gssapi-server-10.3.17-1.module_ 243 kB/s |  49 kB     00:00
(7/10): mariadb-10.3.17-1.module_el8.1.0+257+48 1.9 MB/s | 6.1 MB     00:03
(8/10): perl-DBD-MySQL-4.046-3.module_el8.1.0+2 638 kB/s | 156 kB     00:00
(9/10): mariadb-server-utils-10.3.17-1.module_e 545 kB/s | 1.6 MB     00:03
(10/10): mariadb-server-10.3.17-1.module_el8.1. 475 kB/s |  16 MB     00:34
--------------------------------------------------------------------------------
合計                                            853 kB/s |  30 MB     00:36
トランザクションの確認を実行中
トランザクションの確認に成功しました。
トランザクションのテストを実行中
トランザクションのテストに成功しました。
トランザクションを実行中
  scriptletの実行中: mariadb-connector-c-3.0.7-1.el8.x86_64                 1/1
  準備             :                                                        1/1
  インストール中   : mariadb-connector-c-config-3.0.7-1.el8.noarch         1/10
  インストール中   : mariadb-common-3:10.3.17-1.module_el8.1.0+257+4873    2/10
  インストール中   : mariadb-connector-c-3.0.7-1.el8.x86_64                3/10
  インストール中   : perl-DBD-MySQL-4.046-3.module_el8.1.0+203+e45423dc    4/10
  インストール中   : mariadb-errmsg-3:10.3.17-1.module_el8.1.0+257+4873    5/10
  インストール中   : mariadb-backup-3:10.3.17-1.module_el8.1.0+257+4873    6/10
  インストール中   : mariadb-gssapi-server-3:10.3.17-1.module_el8.1.0+2    7/10
  インストール中   : mariadb-server-utils-3:10.3.17-1.module_el8.1.0+25    8/10
  scriptletの実行中: mariadb-server-3:10.3.17-1.module_el8.1.0+257+4873    9/10
  インストール中   : mariadb-server-3:10.3.17-1.module_el8.1.0+257+4873    9/10
  scriptletの実行中: mariadb-server-3:10.3.17-1.module_el8.1.0+257+4873    9/10
  インストール中   : mariadb-3:10.3.17-1.module_el8.1.0+257+48736ea6.x8   10/10
  scriptletの実行中: mariadb-3:10.3.17-1.module_el8.1.0+257+48736ea6.x8   10/10
  検証             : mariadb-3:10.3.17-1.module_el8.1.0+257+48736ea6.x8    1/10
  検証             : mariadb-backup-3:10.3.17-1.module_el8.1.0+257+4873    2/10
  検証             : mariadb-common-3:10.3.17-1.module_el8.1.0+257+4873    3/10
  検証             : mariadb-connector-c-3.0.7-1.el8.x86_64                4/10
  検証             : mariadb-connector-c-config-3.0.7-1.el8.noarch         5/10
  検証             : mariadb-errmsg-3:10.3.17-1.module_el8.1.0+257+4873    6/10
  検証             : mariadb-gssapi-server-3:10.3.17-1.module_el8.1.0+2    7/10
  検証             : mariadb-server-3:10.3.17-1.module_el8.1.0+257+4873    8/10
  検証             : mariadb-server-utils-3:10.3.17-1.module_el8.1.0+25    9/10
  検証             : perl-DBD-MySQL-4.046-3.module_el8.1.0+203+e45423dc   10/10

インストール済み:
  mariadb-3:10.3.17-1.module_el8.1.0+257+48736ea6.x86_64
  mariadb-server-3:10.3.17-1.module_el8.1.0+257+48736ea6.x86_64
  mariadb-backup-3:10.3.17-1.module_el8.1.0+257+48736ea6.x86_64
  mariadb-gssapi-server-3:10.3.17-1.module_el8.1.0+257+48736ea6.x86_64
  mariadb-server-utils-3:10.3.17-1.module_el8.1.0+257+48736ea6.x86_64
  mariadb-common-3:10.3.17-1.module_el8.1.0+257+48736ea6.x86_64
  mariadb-connector-c-3.0.7-1.el8.x86_64
  mariadb-connector-c-config-3.0.7-1.el8.noarch
  mariadb-errmsg-3:10.3.17-1.module_el8.1.0+257+48736ea6.x86_64
  perl-DBD-MySQL-4.046-3.module_el8.1.0+203+e45423dc.x86_64

完了しました!
</pre>
</div>
{{< /accordion >}}

2.mariadbの自動起動設定

{{< accordion >}}
<div>
<pre>
# systemctl enable mariadb
Created symlink /etc/systemd/system/mysql.service → /usr/lib/systemd/system/mariadb.service.
Created symlink /etc/systemd/system/mysqld.service → /usr/lib/systemd/system/mariadb.service.
Created symlink /etc/systemd/system/multi-user.target.wants/mariadb.service → /usr/lib/systemd/system/mariadb.service.
</pre>
</div>
{{< /accordion >}}

3.mariadbの起動

{{< accordion >}}
<div>
<pre>
# systemctl start mariadb
</pre>

<pre>
# systemctl status mariadb
● mariadb.service - MariaDB 10.3 database server
   Loaded: loaded (/usr/lib/systemd/system/mariadb.service; enabled; vendor preset: disabled)
   Active: active (running) since Thu 2020-02-06 03:44:50 EST; 56s ago
     Docs: man:mysqld(8)
           https://mariadb.com/kb/en/library/systemd/
  Process: 4903 ExecStartPost=/usr/libexec/mysql-check-upgrade (code=exited, status=0/SUCCESS)
  Process: 4768 ExecStartPre=/usr/libexec/mysql-prepare-db-dir mariadb.service (code=exited, status=0/SUCCESS)
  Process: 4744 ExecStartPre=/usr/libexec/mysql-check-socket (code=exited, status=0/SUCCESS)
 Main PID: 4871 (mysqld)
   Status: "Taking your SQL requests now..."
    Tasks: 30 (limit: 23983)
   Memory: 85.9M
   CGroup: /system.slice/mariadb.service
           mq4871 /usr/libexec/mysqld --basedir=/usr

 2月 06 03:44:50 tokyo-ec.com mysql-prepare-db-dir[4768]: Please report any problems at http://mariadb.org/jira
 2月 06 03:44:50 tokyo-ec.com mysql-prepare-db-dir[4768]: The latest information about MariaDB is available at http://mariadb.org/.
 2月 06 03:44:50 tokyo-ec.com mysql-prepare-db-dir[4768]: You can find additional information about the MySQL part at:
 2月 06 03:44:50 tokyo-ec.com mysql-prepare-db-dir[4768]: http://dev.mysql.com
 2月 06 03:44:50 tokyo-ec.com mysql-prepare-db-dir[4768]: Consider joining MariaDB's strong and vibrant community:
 2月 06 03:44:50 tokyo-ec.com mysql-prepare-db-dir[4768]: https://mariadb.org/get-involved/
 2月 06 03:44:50 tokyo-ec.com mysqld[4871]: 2020-02-06  3:44:50 0 [Note] /usr/libexec/mysqld (mysqld 10.3.17-MariaDB) starting as process 4871 ...
 2月 06 03:44:50 tokyo-ec.com mysqld[4871]: 2020-02-06  3:44:50 0 [Warning] Could not increase number of max_open_files to more than 1024 (request: 4183)
 2月 06 03:44:50 tokyo-ec.com mysqld[4871]: 2020-02-06  3:44:50 0 [Warning] Changed limits: max_open_files: 1024  max_connections: 151 (was 151)  table_cach>
 2月 06 03:44:50 tokyo-ec.com systemd[1]: Started MariaDB 10.3 database server.
 <font color="Red">//[SPACE]キーでスクロールして、[q]キーを入力して終了</font>
</pre>
</div>
{{< /accordion >}}

4.mariadbのrootユーザのパスワード設定

{{< accordion >}}
<div>
<pre>
# mysql -u root
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 8
Server version: 10.3.17-MariaDB MariaDB Server

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]>
</pre>

<pre>
MariaDB [(none)]> update mysql.user set password=password('mariadb123') where user = 'root';
Query OK, 4 rows affected (0.001 sec)
Rows matched: 4  Changed: 4  Warnings: 0
</pre>

<pre>
MariaDB [(none)]> FLUSH PRIVILEGES;
Query OK, 0 rows affected (0.001 sec)
</pre>

<pre>
MariaDB [(none)]> exit
Bye
#
</pre>
</div>
{{< /accordion >}}