---
title: "5.PHP Environment Construction"
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

## 1.phpのインストール

CentOS8_WORDPRESSの仮想マシンで実行すること

1.phpのインストール

{{< accordion >}}
<div>
<pre>
# dnf -y install php php-devel php-pdo php-mysqlnd php-mbstring php-json php-gd
メタデータの期限切れの最終確認: 0:07:41 時間前の 2020年02月06日 20時47分42秒 に 実施しました。
依存関係が解決しました。
================================================================================
 パッケージ       Arch   バージョン                             Repo      サイズ
================================================================================
インストール:
 php              x86_64 7.2.11-2.module_el8.1.0+209+03b9a8ff   AppStream 1.5 M
 php-devel        x86_64 7.2.11-2.module_el8.1.0+209+03b9a8ff   AppStream 712 k
 php-gd           x86_64 7.2.11-2.module_el8.1.0+209+03b9a8ff   AppStream  84 k
 php-json         x86_64 7.2.11-2.module_el8.1.0+209+03b9a8ff   AppStream  73 k
 php-mbstring     x86_64 7.2.11-2.module_el8.1.0+209+03b9a8ff   AppStream 581 k
 php-mysqlnd      x86_64 7.2.11-2.module_el8.1.0+209+03b9a8ff   AppStream 190 k
 php-pdo          x86_64 7.2.11-2.module_el8.1.0+209+03b9a8ff   AppStream 122 k
依存関係のインストール:
 autoconf         noarch 2.69-27.el8                            AppStream 710 k
 automake         noarch 1.16.1-6.el8                           AppStream 713 k
 cpp              x86_64 8.3.1-4.5.el8                          AppStream  10 M
 gcc              x86_64 8.3.1-4.5.el8                          AppStream  23 M
 gcc-c++          x86_64 8.3.1-4.5.el8                          AppStream  12 M
 isl              x86_64 0.16.1-6.el8                           AppStream 841 k
 libstdc++-devel  x86_64 8.3.1-4.5.el8                          AppStream 2.0 M
 libtool          x86_64 2.4.6-25.el8                           AppStream 709 k
 nginx-filesystem noarch 1:1.14.1-9.module_el8.0.0+184+e34fea82 AppStream  24 k
 perl-Thread-Queue
                  noarch 3.13-1.el8                             AppStream  24 k
 php-cli          x86_64 7.2.11-2.module_el8.1.0+209+03b9a8ff   AppStream 3.1 M
 php-common       x86_64 7.2.11-2.module_el8.1.0+209+03b9a8ff   AppStream 655 k
 glibc-devel      x86_64 2.28-72.el8                            BaseOS    1.0 M
 glibc-headers    x86_64 2.28-72.el8                            BaseOS    469 k
 kernel-headers   x86_64 4.18.0-147.3.1.el8_1                   BaseOS    2.7 M
 libxcrypt-devel  x86_64 4.1.1-4.el8                            BaseOS     25 k
 m4               x86_64 1.4.18-7.el8                           BaseOS    223 k
 pcre-cpp         x86_64 8.42-4.el8                             BaseOS     47 k
 pcre-devel       x86_64 8.42-4.el8                             BaseOS    551 k
 pcre-utf16       x86_64 8.42-4.el8                             BaseOS    195 k
 pcre-utf32       x86_64 8.42-4.el8                             BaseOS    186 k
弱い依存関係のインストール:
 php-fpm          x86_64 7.2.11-2.module_el8.1.0+209+03b9a8ff   AppStream 1.6 M
モジュールストリームの有効化:
 nginx                   1.14
 php                     7.2

トランザクションの概要
================================================================================
インストール  29 パッケージ

ダウンロードサイズの合計: 65 M
インストール済みのサイズ: 186 M
パッケージのダウンロード:
(1/29): automake-1.16.1-6.el8.noarch.rpm        6.4 MB/s | 713 kB     00:00
(2/29): autoconf-2.69-27.el8.noarch.rpm         4.5 MB/s | 710 kB     00:00
(3/29): cpp-8.3.1-4.5.el8.x86_64.rpm            8.5 MB/s |  10 MB     00:01
(4/29): isl-0.16.1-6.el8.x86_64.rpm             6.1 MB/s | 841 kB     00:00
(5/29): libstdc++-devel-8.3.1-4.5.el8.x86_64.rp  11 MB/s | 2.0 MB     00:00
(6/29): libtool-2.4.6-25.el8.x86_64.rpm         7.1 MB/s | 709 kB     00:00
(7/29): nginx-filesystem-1.14.1-9.module_el8.0. 1.9 MB/s |  24 kB     00:00
(8/29): perl-Thread-Queue-3.13-1.el8.noarch.rpm 835 kB/s |  24 kB     00:00
(9/29): php-7.2.11-2.module_el8.1.0+209+03b9a8f 8.3 MB/s | 1.5 MB     00:00
(10/29): php-cli-7.2.11-2.module_el8.1.0+209+03 9.2 MB/s | 3.1 MB     00:00
(11/29): php-common-7.2.11-2.module_el8.1.0+209 8.3 MB/s | 655 kB     00:00
(12/29): php-devel-7.2.11-2.module_el8.1.0+209+ 5.5 MB/s | 712 kB     00:00
(13/29): php-fpm-7.2.11-2.module_el8.1.0+209+03 3.7 MB/s | 1.6 MB     00:00
(14/29): php-gd-7.2.11-2.module_el8.1.0+209+03b 1.7 MB/s |  84 kB     00:00
(15/29): gcc-c++-8.3.1-4.5.el8.x86_64.rpm       4.4 MB/s |  12 MB     00:02
(16/29): php-json-7.2.11-2.module_el8.1.0+209+0 1.2 MB/s |  73 kB     00:00
(17/29): php-mysqlnd-7.2.11-2.module_el8.1.0+20 3.0 MB/s | 190 kB     00:00
(18/29): php-pdo-7.2.11-2.module_el8.1.0+209+03 2.9 MB/s | 122 kB     00:00
(19/29): gcc-8.3.1-4.5.el8.x86_64.rpm           7.6 MB/s |  23 MB     00:03
(20/29): php-mbstring-7.2.11-2.module_el8.1.0+2 2.7 MB/s | 581 kB     00:00
(21/29): glibc-headers-2.28-72.el8.x86_64.rpm   2.5 MB/s | 469 kB     00:00
(22/29): libxcrypt-devel-4.1.1-4.el8.x86_64.rpm 1.1 MB/s |  25 kB     00:00
(23/29): glibc-devel-2.28-72.el8.x86_64.rpm     2.9 MB/s | 1.0 MB     00:00
(24/29): m4-1.4.18-7.el8.x86_64.rpm             5.4 MB/s | 223 kB     00:00
(25/29): pcre-cpp-8.42-4.el8.x86_64.rpm         1.3 MB/s |  47 kB     00:00
(26/29): kernel-headers-4.18.0-147.3.1.el8_1.x8 8.2 MB/s | 2.7 MB     00:00
(27/29): pcre-utf16-8.42-4.el8.x86_64.rpm       3.4 MB/s | 195 kB     00:00
(28/29): pcre-devel-8.42-4.el8.x86_64.rpm       3.0 MB/s | 551 kB     00:00
(29/29): pcre-utf32-8.42-4.el8.x86_64.rpm       650 kB/s | 186 kB     00:00
--------------------------------------------------------------------------------
合計                                             13 MB/s |  65 MB     00:04
トランザクションの確認を実行中
トランザクションの確認に成功しました。
トランザクションのテストを実行中
トランザクションのテストに成功しました。
トランザクションを実行中
  準備             :                                                        1/1
  インストール中   : php-common-7.2.11-2.module_el8.1.0+209+03b9a8ff.x8    1/29
  インストール中   : php-cli-7.2.11-2.module_el8.1.0+209+03b9a8ff.x86_6    2/29
  インストール中   : php-pdo-7.2.11-2.module_el8.1.0+209+03b9a8ff.x86_6    3/29
  インストール中   : pcre-utf32-8.42-4.el8.x86_64                          4/29
  インストール中   : pcre-utf16-8.42-4.el8.x86_64                          5/29
  インストール中   : pcre-cpp-8.42-4.el8.x86_64                            6/29
  インストール中   : pcre-devel-8.42-4.el8.x86_64                          7/29
  インストール中   : m4-1.4.18-7.el8.x86_64                                8/29
  scriptletの実行中: m4-1.4.18-7.el8.x86_64                                8/29
  インストール中   : autoconf-2.69-27.el8.noarch                           9/29
  scriptletの実行中: autoconf-2.69-27.el8.noarch                           9/29
  インストール中   : kernel-headers-4.18.0-147.3.1.el8_1.x86_64           10/29
  scriptletの実行中: glibc-headers-2.28-72.el8.x86_64                     11/29
  インストール中   : glibc-headers-2.28-72.el8.x86_64                     11/29
  インストール中   : libxcrypt-devel-4.1.1-4.el8.x86_64                   12/29
  インストール中   : glibc-devel-2.28-72.el8.x86_64                       13/29
  scriptletの実行中: glibc-devel-2.28-72.el8.x86_64                       13/29
  インストール中   : perl-Thread-Queue-3.13-1.el8.noarch                  14/29
  インストール中   : automake-1.16.1-6.el8.noarch                         15/29
  scriptletの実行中: nginx-filesystem-1:1.14.1-9.module_el8.0.0+184+e34   16/29
  インストール中   : nginx-filesystem-1:1.14.1-9.module_el8.0.0+184+e34   16/29
  インストール中   : php-fpm-7.2.11-2.module_el8.1.0+209+03b9a8ff.x86_6   17/29
  scriptletの実行中: php-fpm-7.2.11-2.module_el8.1.0+209+03b9a8ff.x86_6   17/29
  インストール中   : libstdc++-devel-8.3.1-4.5.el8.x86_64                 18/29
  インストール中   : isl-0.16.1-6.el8.x86_64                              19/29
  scriptletの実行中: isl-0.16.1-6.el8.x86_64                              19/29
  インストール中   : cpp-8.3.1-4.5.el8.x86_64                             20/29
  scriptletの実行中: cpp-8.3.1-4.5.el8.x86_64                             20/29
  インストール中   : gcc-8.3.1-4.5.el8.x86_64                             21/29
  scriptletの実行中: gcc-8.3.1-4.5.el8.x86_64                             21/29
  インストール中   : gcc-c++-8.3.1-4.5.el8.x86_64                         22/29
  インストール中   : libtool-2.4.6-25.el8.x86_64                          23/29
  scriptletの実行中: libtool-2.4.6-25.el8.x86_64                          23/29
  インストール中   : php-devel-7.2.11-2.module_el8.1.0+209+03b9a8ff.x86   24/29
  インストール中   : php-7.2.11-2.module_el8.1.0+209+03b9a8ff.x86_64      25/29
  インストール中   : php-mysqlnd-7.2.11-2.module_el8.1.0+209+03b9a8ff.x   26/29
  インストール中   : php-gd-7.2.11-2.module_el8.1.0+209+03b9a8ff.x86_64   27/29
  インストール中   : php-json-7.2.11-2.module_el8.1.0+209+03b9a8ff.x86_   28/29
  インストール中   : php-mbstring-7.2.11-2.module_el8.1.0+209+03b9a8ff.   29/29
  scriptletの実行中: php-mbstring-7.2.11-2.module_el8.1.0+209+03b9a8ff.   29/29
  scriptletの実行中: php-fpm-7.2.11-2.module_el8.1.0+209+03b9a8ff.x86_6   29/29
  検証             : autoconf-2.69-27.el8.noarch                           1/29
  検証             : automake-1.16.1-6.el8.noarch                          2/29
  検証             : cpp-8.3.1-4.5.el8.x86_64                              3/29
  検証             : gcc-8.3.1-4.5.el8.x86_64                              4/29
  検証             : gcc-c++-8.3.1-4.5.el8.x86_64                          5/29
  検証             : isl-0.16.1-6.el8.x86_64                               6/29
  検証             : libstdc++-devel-8.3.1-4.5.el8.x86_64                  7/29
  検証             : libtool-2.4.6-25.el8.x86_64                           8/29
  検証             : nginx-filesystem-1:1.14.1-9.module_el8.0.0+184+e34    9/29
  検証             : perl-Thread-Queue-3.13-1.el8.noarch                  10/29
  検証             : php-7.2.11-2.module_el8.1.0+209+03b9a8ff.x86_64      11/29
  検証             : php-cli-7.2.11-2.module_el8.1.0+209+03b9a8ff.x86_6   12/29
  検証             : php-common-7.2.11-2.module_el8.1.0+209+03b9a8ff.x8   13/29
  検証             : php-devel-7.2.11-2.module_el8.1.0+209+03b9a8ff.x86   14/29
  検証             : php-fpm-7.2.11-2.module_el8.1.0+209+03b9a8ff.x86_6   15/29
  検証             : php-gd-7.2.11-2.module_el8.1.0+209+03b9a8ff.x86_64   16/29
  検証             : php-json-7.2.11-2.module_el8.1.0+209+03b9a8ff.x86_   17/29
  検証             : php-mbstring-7.2.11-2.module_el8.1.0+209+03b9a8ff.   18/29
  検証             : php-mysqlnd-7.2.11-2.module_el8.1.0+209+03b9a8ff.x   19/29
  検証             : php-pdo-7.2.11-2.module_el8.1.0+209+03b9a8ff.x86_6   20/29
  検証             : glibc-devel-2.28-72.el8.x86_64                       21/29
  検証             : glibc-headers-2.28-72.el8.x86_64                     22/29
  検証             : kernel-headers-4.18.0-147.3.1.el8_1.x86_64           23/29
  検証             : libxcrypt-devel-4.1.1-4.el8.x86_64                   24/29
  検証             : m4-1.4.18-7.el8.x86_64                               25/29
  検証             : pcre-cpp-8.42-4.el8.x86_64                           26/29
  検証             : pcre-devel-8.42-4.el8.x86_64                         27/29
  検証             : pcre-utf16-8.42-4.el8.x86_64                         28/29
  検証             : pcre-utf32-8.42-4.el8.x86_64                         29/29

インストール済み:
  php-7.2.11-2.module_el8.1.0+209+03b9a8ff.x86_64
  php-devel-7.2.11-2.module_el8.1.0+209+03b9a8ff.x86_64
  php-gd-7.2.11-2.module_el8.1.0+209+03b9a8ff.x86_64
  php-json-7.2.11-2.module_el8.1.0+209+03b9a8ff.x86_64
  php-mbstring-7.2.11-2.module_el8.1.0+209+03b9a8ff.x86_64
  php-mysqlnd-7.2.11-2.module_el8.1.0+209+03b9a8ff.x86_64
  php-pdo-7.2.11-2.module_el8.1.0+209+03b9a8ff.x86_64
  php-fpm-7.2.11-2.module_el8.1.0+209+03b9a8ff.x86_64
  autoconf-2.69-27.el8.noarch
  automake-1.16.1-6.el8.noarch
  cpp-8.3.1-4.5.el8.x86_64
  gcc-8.3.1-4.5.el8.x86_64
  gcc-c++-8.3.1-4.5.el8.x86_64
  isl-0.16.1-6.el8.x86_64
  libstdc++-devel-8.3.1-4.5.el8.x86_64
  libtool-2.4.6-25.el8.x86_64
  nginx-filesystem-1:1.14.1-9.module_el8.0.0+184+e34fea82.noarch
  perl-Thread-Queue-3.13-1.el8.noarch
  php-cli-7.2.11-2.module_el8.1.0+209+03b9a8ff.x86_64
  php-common-7.2.11-2.module_el8.1.0+209+03b9a8ff.x86_64
  glibc-devel-2.28-72.el8.x86_64
  glibc-headers-2.28-72.el8.x86_64
  kernel-headers-4.18.0-147.3.1.el8_1.x86_64
  libxcrypt-devel-4.1.1-4.el8.x86_64
  m4-1.4.18-7.el8.x86_64
  pcre-cpp-8.42-4.el8.x86_64
  pcre-devel-8.42-4.el8.x86_64
  pcre-utf16-8.42-4.el8.x86_64
  pcre-utf32-8.42-4.el8.x86_64

完了しました!
</pre>
</div>
{{< /accordion >}}

2.phpのバージョン確認

{{< accordion >}}
<div>
<pre>
# php -v
PHP 7.2.11 (cli) (built: Oct  9 2018 15:09:36) ( NTS )
Copyright (c) 1997-2018 The PHP Group
Zend Engine v3.2.0, Copyright (c) 1998-2018 Zend Technologies
</pre>
</div>
{{< /accordion >}}

3.phpの設定情報をブラウザに表示するためのコードを記述

{{< accordion >}}
<div>
<pre>
# cd /var/www/html
</pre>

<pre>
# vim phpinfo.php

--------------以下の内容をコピー&ペーストします。-------
<?php
phpinfo();
---------------[Esc + :wq]で保存終了します。----------
</pre>

<pre>
# systemctl restart httpd
</pre>
</div>
{{< /accordion >}}

4.ブラウザを起動して、設定情報を確認

http://192.168.56.28/phpinfo.php

{{< accordion >}}
<div>

<img src="/hugo/images/php-environment-construction-01.png">

</div>
{{< /accordion >}}