---
title: "7.WordPress Environment Construction"
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

## 1.WordPress用のデータベース作成

CentOS8_WORDPRESSの仮想マシンで実行すること

1.WordPress用のデータベース作成

{{< accordion >}}
<div>
<pre>
# mysql -u root -p
Enter password:mariadb123 <font color="Red">//←パスワード入力</font>
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 9
Server version: 10.3.17-MariaDB MariaDB Server

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]>
</pre>

<pre>
MariaDB [(none)]> )]> CREATE DATABASE wordpress;
Query OK, 1 row affected (0.000 sec)
</pre>

<pre>
MariaDB [(none)]> GRANT ALL PRIVILEGES ON wordpress.*TO 'wordpress'@'localhost' IDENTIFIED BY 'wppass';
Query OK, 0 rows affected (0.000 sec)
</pre>

<pre>
MariaDB [(none)]> FLUSH PRIVILEGES;
Query OK, 0 rows affected (0.000 sec)
</pre>

<pre>
MariaDB [(none)]> exit
Bye
#
</pre>

</div>
{{< /accordion >}}

***

## 2.WordPressのインストール

CentOS8_WORDPRESSの仮想マシンで実行すること

1.WordPressのダウンロード

{{< accordion >}}
<div>
<pre>
# wget https://ja.wordpress.org/latest-ja.tar.gz
--2020-02-06 04:17:22--  https://ja.wordpress.org/latest-ja.tar.gz
ja.wordpress.org (ja.wordpress.org) をDNSに問いあわせています... 198.143.164.252
ja.wordpress.org (ja.wordpress.org)|198.143.164.252|:443 に接続しています... 接続しました。
HTTP による接続要求を送信しました、応答を待っています... 200 OK
長さ: 12479892 (12M) [application/octet-stream]
`latest-ja.tar.gz' に保存中

latest-ja.tar.gz                        100%[============================================================================>]  11.90M  2.03MB/s 時間 6.4s

2020-02-06 04:17:29 (1.87 MB/s) - `latest-ja.tar.gz' へ保存完了 [12479892/12479892]
</pre>
</div>
{{< /accordion >}}

2.tarコマンドで展開

{{< accordion >}}
<div>
<pre>
# tar xvzf latest-ja.tar.gz
wordpress/
・
・省略
・
wordpress/wp-links-opml.php
</pre>
</div>
{{< /accordion >}}

3.WordPressデータをドキュメントルートに移動

{{< accordion >}}
<div>
<pre>
# mv wordpress /var/www/html
</pre>
</div>
{{< /accordion >}}

4.「/var/www/html/wordpress」ディレクトリの所有者変更

{{< accordion >}}
<div>
<pre>
# chown -R apache:apache /var/www/html/wordpress/
</pre>

<pre>
# ls -la /var/www/html/wordpress/
合計 212
drwxr-xr-x.  5 apache apache  4096  1月  2 00:00 .
drwxr-xr-x.  3 root   root      23  2月 17 02:08 ..
-rw-r--r--.  1 apache apache   420 11月 30  2017 index.php
-rw-r--r--.  1 apache apache 19935  1月  1  2019 license.txt
-rw-r--r--.  1 apache apache 10180  1月  2 00:00 readme.html
-rw-r--r--.  1 apache apache  6939  9月  2 20:41 wp-activate.php
drwxr-xr-x.  9 apache apache  4096  1月  2 00:00 wp-admin
-rw-r--r--.  1 apache apache   369 11月 30  2017 wp-blog-header.php
-rw-r--r--.  1 apache apache  2283  1月 20  2019 wp-comments-post.php
-rw-r--r--.  1 apache apache  3944  1月  2 00:00 wp-config-sample.php
drwxr-xr-x.  5 apache apache    69  1月  2 00:00 wp-content
-rw-r--r--.  1 apache apache  3955 10月 10 18:52 wp-cron.php
drwxr-xr-x. 20 apache apache  8192  1月  2 00:00 wp-includes
-rw-r--r--.  1 apache apache  2504  9月  2 20:41 wp-links-opml.php
-rw-r--r--.  1 apache apache  3326  9月  2 20:41 wp-load.php
-rw-r--r--.  1 apache apache 47597 12月  9 08:30 wp-login.php
-rw-r--r--.  1 apache apache  8483  9月  2 20:41 wp-mail.php
-rw-r--r--.  1 apache apache 19120 10月 15 11:37 wp-settings.php
-rw-r--r--.  1 apache apache 31112  9月  2 20:41 wp-signup.php
-rw-r--r--.  1 apache apache  4764 11月 30  2017 wp-trackback.php
-rw-r--r--.  1 apache apache  3150  7月  1  2019 xmlrpc.php
</pre>
</div>
{{< /accordion >}}

5.ディレクトリにSELinuxのコンテキストを設定

{{< accordion >}}
<div>
<pre>
# chcon -R -t httpd_sys_content_t /var/www/html/wordpress
</pre>

<pre>
# chcon -R -t httpd_sys_rw_content_t /var/www/html/wordpress
</pre>
</div>
{{< /accordion >}}

6.ブラウザでhttp://192.168.56.28/wordpress/にアクセス