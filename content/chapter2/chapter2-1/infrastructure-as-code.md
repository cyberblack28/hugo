---
title: "12.Infrastructure as Code"
date: 2017-10-17T15:26:15Z
draft: false
weight: 20
---

## 事前作業

1.studentユーザでログインして、rootユーザに変更します。

```
$ su -
パスワード:tokyoec
#
```

2.Nginxアンインストール

※CentOS8_PROXY_DNSの仮想マシンで実行すること

```
# dnf -y remove nginx
モジュラーの依存に関する問題:

 問題 1: conflicting requests
  - nothing provides module(perl:5.26) needed by module perl-DBD-MySQL:4.046:8010020191114030811:073fa5fe-0.x86_64
 問題 2: conflicting requests
  - nothing provides module(perl:5.26) needed by module perl-DBD-SQLite:1.58:8010020191114033549:073fa5fe-0.x86_64
 問題 3: conflicting requests
  - nothing provides module(perl:5.26) needed by module perl-DBI:1.641:8010020191113222731:16b3ab4d-0.x86_64
依存関係が解決しました。
=============================================================================================================================================================
 パッケージ                                  アーキテクチャー       バージョン                                              リポジトリー               サイズ
=============================================================================================================================================================
削除中:
 nginx                                       x86_64                 1:1.14.1-9.module_el8.0.0+184+e34fea82                  @AppStream                 1.7 M
未使用の依存関係の削除:
 nginx-all-modules                           noarch                 1:1.14.1-9.module_el8.0.0+184+e34fea82                  @AppStream                   0
 nginx-mod-http-image-filter                 x86_64                 1:1.14.1-9.module_el8.0.0+184+e34fea82                  @AppStream                  29 k
 nginx-mod-http-perl                         x86_64                 1:1.14.1-9.module_el8.0.0+184+e34fea82                  @AppStream                  61 k
 nginx-mod-http-xslt-filter                  x86_64                 1:1.14.1-9.module_el8.0.0+184+e34fea82                  @AppStream                  25 k
 nginx-mod-mail                              x86_64                 1:1.14.1-9.module_el8.0.0+184+e34fea82                  @AppStream                 113 k
 nginx-mod-stream                            x86_64                 1:1.14.1-9.module_el8.0.0+184+e34fea82                  @AppStream                 171 k

トランザクションの概要
=============================================================================================================================================================
削除  7 パッケージ

解放された容量: 2.0 M
トランザクションの確認を実行中
トランザクションの確認に成功しました。
トランザクションのテストを実行中
トランザクションのテストに成功しました。
トランザクションを実行中
  準備             :                                                                                                                                     1/1
  scriptletの実行中: nginx-mod-http-image-filter-1:1.14.1-9.module_el8.0.0+184+e34fea82.x86_64                                                           1/1
  削除             : nginx-mod-http-image-filter-1:1.14.1-9.module_el8.0.0+184+e34fea82.x86_64                                                           1/7
  削除             : nginx-mod-http-perl-1:1.14.1-9.module_el8.0.0+184+e34fea82.x86_64                                                                   2/7
  削除             : nginx-mod-http-xslt-filter-1:1.14.1-9.module_el8.0.0+184+e34fea82.x86_64                                                            3/7
  削除             : nginx-mod-mail-1:1.14.1-9.module_el8.0.0+184+e34fea82.x86_64                                                                        4/7
  削除             : nginx-mod-stream-1:1.14.1-9.module_el8.0.0+184+e34fea82.x86_64                                                                      5/7
  scriptletの実行中: nginx-1:1.14.1-9.module_el8.0.0+184+e34fea82.x86_64                                                                                 6/7
  削除             : nginx-1:1.14.1-9.module_el8.0.0+184+e34fea82.x86_64                                                                                 6/7
  scriptletの実行中: nginx-1:1.14.1-9.module_el8.0.0+184+e34fea82.x86_64                                                                                 6/7
  削除             : nginx-all-modules-1:1.14.1-9.module_el8.0.0+184+e34fea82.noarch                                                                     7/7
  scriptletの実行中: nginx-all-modules-1:1.14.1-9.module_el8.0.0+184+e34fea82.noarch                                                                     7/7
  検証             : nginx-1:1.14.1-9.module_el8.0.0+184+e34fea82.x86_64                                                                                 1/7
  検証             : nginx-all-modules-1:1.14.1-9.module_el8.0.0+184+e34fea82.noarch                                                                     2/7
  検証             : nginx-mod-http-image-filter-1:1.14.1-9.module_el8.0.0+184+e34fea82.x86_64                                                           3/7
  検証             : nginx-mod-http-perl-1:1.14.1-9.module_el8.0.0+184+e34fea82.x86_64                                                                   4/7
  検証             : nginx-mod-http-xslt-filter-1:1.14.1-9.module_el8.0.0+184+e34fea82.x86_64                                                            5/7
  検証             : nginx-mod-mail-1:1.14.1-9.module_el8.0.0+184+e34fea82.x86_64                                                                        6/7
  検証             : nginx-mod-stream-1:1.14.1-9.module_el8.0.0+184+e34fea82.x86_64                                                                      7/7

削除しました:
  nginx-1:1.14.1-9.module_el8.0.0+184+e34fea82.x86_64                               nginx-all-modules-1:1.14.1-9.module_el8.0.0+184+e34fea82.noarch
  nginx-mod-http-image-filter-1:1.14.1-9.module_el8.0.0+184+e34fea82.x86_64         nginx-mod-http-perl-1:1.14.1-9.module_el8.0.0+184+e34fea82.x86_64
  nginx-mod-http-xslt-filter-1:1.14.1-9.module_el8.0.0+184+e34fea82.x86_64          nginx-mod-mail-1:1.14.1-9.module_el8.0.0+184+e34fea82.x86_64
  nginx-mod-stream-1:1.14.1-9.module_el8.0.0+184+e34fea82.x86_64

完了しました!
```

3.httpd,php,mariadbアンインストール

※CentOS8_WORDPRESSの仮想マシンで実行すること

```
# dnf -y remove httpd php php-devel php-pdo php-mysqlnd php-mbstring php-json php-gd mariadb mariadb-server
モジュラーの依存に関する問題:

 問題 1: conflicting requests
  - nothing provides module(perl:5.26) needed by module perl-DBD-MySQL:4.046:8010020191114030811:073fa5fe-0.x86_64
 問題 2: conflicting requests
  - nothing provides module(perl:5.26) needed by module perl-DBD-SQLite:1.58:8010020191114033549:073fa5fe-0.x86_64
 問題 3: conflicting requests
  - nothing provides module(perl:5.26) needed by module perl-DBI:1.641:8010020191113222731:16b3ab4d-0.x86_64
依存関係が解決しました。
================================================================================
 パッケージ     Arch   バージョン                              Repo       サイズ
================================================================================
削除中:
 httpd          x86_64 2.4.37-16.module_el8.1.0+256+ae790463   @AppStream 5.4 M
 mariadb        x86_64 3:10.3.17-1.module_el8.1.0+257+48736ea6 @AppStream  40 M
 mariadb-server x86_64 3:10.3.17-1.module_el8.1.0+257+48736ea6 @AppStream  88 M
 php            x86_64 7.2.11-2.module_el8.1.0+209+03b9a8ff    @AppStream 5.5 M
 php-devel      x86_64 7.2.11-2.module_el8.1.0+209+03b9a8ff    @AppStream 5.3 M
 php-gd         x86_64 7.2.11-2.module_el8.1.0+209+03b9a8ff    @AppStream 122 k
 php-json       x86_64 7.2.11-2.module_el8.1.0+209+03b9a8ff    @AppStream  53 k
 php-mbstring   x86_64 7.2.11-2.module_el8.1.0+209+03b9a8ff    @AppStream 2.0 M
 php-mysqlnd    x86_64 7.2.11-2.module_el8.1.0+209+03b9a8ff    @AppStream 545 k
 php-pdo        x86_64 7.2.11-2.module_el8.1.0+209+03b9a8ff    @AppStream 236 k
未使用の依存関係の削除:
 apr            x86_64 1.6.3-9.el8                             @AppStream 293 k
 apr-util       x86_64 1.6.1-6.el8                             @AppStream 231 k
 apr-util-bdb   x86_64 1.6.1-6.el8                             @AppStream  12 k
 apr-util-openssl
                x86_64 1.6.1-6.el8                             @AppStream  20 k
 autoconf       noarch 2.69-27.el8                             @AppStream 2.2 M
 automake       noarch 1.16.1-6.el8                            @AppStream 1.7 M
 centos-logos-httpd
                noarch 80.5-2.el8                              @AppStream 1.9 k
 cpp            x86_64 8.3.1-4.5.el8                           @AppStream  28 M
 gcc            x86_64 8.3.1-4.5.el8                           @AppStream  59 M
 gcc-c++        x86_64 8.3.1-4.5.el8                           @AppStream  31 M
 glibc-devel    x86_64 2.28-72.el8                             @BaseOS    1.2 M
 glibc-headers  x86_64 2.28-72.el8                             @BaseOS    1.9 M
 httpd-filesystem
                noarch 2.4.37-16.module_el8.1.0+256+ae790463   @AppStream 400
 httpd-tools    x86_64 2.4.37-16.module_el8.1.0+256+ae790463   @AppStream 211 k
 isl            x86_64 0.16.1-6.el8                            @AppStream 3.1 M
 kernel-headers x86_64 4.18.0-147.3.1.el8_1                    @BaseOS    4.6 M
 libstdc++-devel
                x86_64 8.3.1-4.5.el8                           @AppStream  11 M
 libtool        x86_64 2.4.6-25.el8                            @AppStream 2.6 M
 libxcrypt-devel
                x86_64 4.1.1-4.el8                             @BaseOS     24 k
 m4             x86_64 1.4.18-7.el8                            @BaseOS    370 k
 mariadb-backup x86_64 3:10.3.17-1.module_el8.1.0+257+48736ea6 @AppStream  28 M
 mariadb-common x86_64 3:10.3.17-1.module_el8.1.0+257+48736ea6 @AppStream 179 k
 mariadb-connector-c
                x86_64 3.0.7-1.el8                             @AppStream 424 k
 mariadb-connector-c-config
                noarch 3.0.7-1.el8                             @AppStream 497
 mariadb-errmsg x86_64 3:10.3.17-1.module_el8.1.0+257+48736ea6 @AppStream 2.3 M
 mariadb-gssapi-server
                x86_64 3:10.3.17-1.module_el8.1.0+257+48736ea6 @AppStream  26 k
 mariadb-server-utils
                x86_64 3:10.3.17-1.module_el8.1.0+257+48736ea6 @AppStream  11 M
 mod_http2      x86_64 1.11.3-3.module_el8.1.0+213+acce2796    @AppStream 479 k
 nginx-filesystem
                noarch 1:1.14.1-9.module_el8.0.0+184+e34fea82  @AppStream   0
 pcre-cpp       x86_64 8.42-4.el8                              @BaseOS     47 k
 pcre-devel     x86_64 8.42-4.el8                              @BaseOS    1.7 M
 pcre-utf16     x86_64 8.42-4.el8                              @BaseOS    455 k
 pcre-utf32     x86_64 8.42-4.el8                              @BaseOS    435 k
 perl-DBD-MySQL x86_64 4.046-3.module_el8.1.0+203+e45423dc     @AppStream 367 k
 perl-Thread-Queue
                noarch 3.13-1.el8                              @AppStream  29 k
 php-cli        x86_64 7.2.11-2.module_el8.1.0+209+03b9a8ff    @AppStream  11 M
 php-common     x86_64 7.2.11-2.module_el8.1.0+209+03b9a8ff    @AppStream 6.2 M
 php-fpm        x86_64 7.2.11-2.module_el8.1.0+209+03b9a8ff    @AppStream 5.7 M

トランザクションの概要
================================================================================
削除  48 パッケージ

解放された容量: 363 M
トランザクションの確認を実行中
トランザクションの確認に成功しました。
トランザクションのテストを実行中
トランザクションのテストに成功しました。
トランザクションを実行中
  準備             :                                                        1/1
  scriptletの実行中: php-devel-7.2.11-2.module_el8.1.0+209+03b9a8ff.x86_6   1/1
  削除             : php-devel-7.2.11-2.module_el8.1.0+209+03b9a8ff.x86    1/48
  削除             : pcre-devel-8.42-4.el8.x86_64                          2/48
  削除             : php-7.2.11-2.module_el8.1.0+209+03b9a8ff.x86_64       3/48
  scriptletの実行中: libtool-2.4.6-25.el8.x86_64                           4/48
  削除             : libtool-2.4.6-25.el8.x86_64                           4/48
  scriptletの実行中: httpd-2.4.37-16.module_el8.1.0+256+ae790463.x86_64    5/48
  削除             : httpd-2.4.37-16.module_el8.1.0+256+ae790463.x86_64    5/48
  scriptletの実行中: httpd-2.4.37-16.module_el8.1.0+256+ae790463.x86_64    5/48
  scriptletの実行中: php-fpm-7.2.11-2.module_el8.1.0+209+03b9a8ff.x86_6    6/48
  削除             : php-fpm-7.2.11-2.module_el8.1.0+209+03b9a8ff.x86_6    6/48
  scriptletの実行中: php-fpm-7.2.11-2.module_el8.1.0+209+03b9a8ff.x86_6    6/48
  削除             : automake-1.16.1-6.el8.noarch                          7/48
  削除             : httpd-tools-2.4.37-16.module_el8.1.0+256+ae790463.    8/48
  削除             : apr-util-1.6.1-6.el8.x86_64                           9/48
  scriptletの実行中: apr-util-1.6.1-6.el8.x86_64                           9/48
  削除             : gcc-c++-8.3.1-4.5.el8.x86_64                         10/48
  scriptletの実行中: autoconf-2.69-27.el8.noarch                          11/48
  削除             : autoconf-2.69-27.el8.noarch                          11/48
  scriptletの実行中: gcc-8.3.1-4.5.el8.x86_64                             12/48
  削除             : gcc-8.3.1-4.5.el8.x86_64                             12/48
  scriptletの実行中: glibc-devel-2.28-72.el8.x86_64                       13/48
  削除             : glibc-devel-2.28-72.el8.x86_64                       13/48
  削除             : libxcrypt-devel-4.1.1-4.el8.x86_64                   14/48
  削除             : glibc-headers-2.28-72.el8.x86_64                     15/48
  削除             : php-cli-7.2.11-2.module_el8.1.0+209+03b9a8ff.x86_6   16/48
  削除             : php-mysqlnd-7.2.11-2.module_el8.1.0+209+03b9a8ff.x   17/48
  削除             : php-pdo-7.2.11-2.module_el8.1.0+209+03b9a8ff.x86_6   18/48
  削除             : php-mbstring-7.2.11-2.module_el8.1.0+209+03b9a8ff.   19/48
  削除             : php-json-7.2.11-2.module_el8.1.0+209+03b9a8ff.x86_   20/48
  削除             : php-gd-7.2.11-2.module_el8.1.0+209+03b9a8ff.x86_64   21/48
  削除             : mariadb-gssapi-server-3:10.3.17-1.module_el8.1.0+2   22/48
  削除             : kernel-headers-4.18.0-147.3.1.el8_1.x86_64           23/48
  削除             : libstdc++-devel-8.3.1-4.5.el8.x86_64                 24/48
  削除             : perl-Thread-Queue-3.13-1.el8.noarch                  25/48
  削除             : httpd-filesystem-2.4.37-16.module_el8.1.0+256+ae79   26/48
  scriptletの実行中: httpd-filesystem-2.4.37-16.module_el8.1.0+256+ae79   26/48
  削除             : nginx-filesystem-1:1.14.1-9.module_el8.0.0+184+e34   27/48
  scriptletの実行中: nginx-filesystem-1:1.14.1-9.module_el8.0.0+184+e34   27/48
  削除             : centos-logos-httpd-80.5-2.el8.noarch                 28/48
  削除             : mariadb-backup-3:10.3.17-1.module_el8.1.0+257+4873   29/48
  scriptletの実行中: mariadb-server-3:10.3.17-1.module_el8.1.0+257+4873   30/48
  削除             : mariadb-server-3:10.3.17-1.module_el8.1.0+257+4873   30/48
  scriptletの実行中: mariadb-server-3:10.3.17-1.module_el8.1.0+257+4873   30/48
  削除             : mariadb-3:10.3.17-1.module_el8.1.0+257+48736ea6.x8   31/48
  削除             : mariadb-errmsg-3:10.3.17-1.module_el8.1.0+257+4873   32/48
  削除             : mariadb-common-3:10.3.17-1.module_el8.1.0+257+4873   33/48
  削除             : mariadb-server-utils-3:10.3.17-1.module_el8.1.0+25   34/48
  削除             : perl-DBD-MySQL-4.046-3.module_el8.1.0+203+e45423dc   35/48
  削除             : mariadb-connector-c-3.0.7-1.el8.x86_64               36/48
  削除             : mariadb-connector-c-config-3.0.7-1.el8.noarch        37/48
  削除             : php-common-7.2.11-2.module_el8.1.0+209+03b9a8ff.x8   38/48
警告: /etc/php.ini は /etc/php.ini.rpmsave として保存されました。

  scriptletの実行中: cpp-8.3.1-4.5.el8.x86_64                             39/48
  削除             : cpp-8.3.1-4.5.el8.x86_64                             39/48
  削除             : isl-0.16.1-6.el8.x86_64                              40/48
  scriptletの実行中: isl-0.16.1-6.el8.x86_64                              40/48
  scriptletの実行中: m4-1.4.18-7.el8.x86_64                               41/48
  削除             : m4-1.4.18-7.el8.x86_64                               41/48
  削除             : apr-1.6.3-9.el8.x86_64                               42/48
  scriptletの実行中: apr-1.6.3-9.el8.x86_64                               42/48
  削除             : apr-util-bdb-1.6.1-6.el8.x86_64                      43/48
  削除             : apr-util-openssl-1.6.1-6.el8.x86_64                  44/48
  削除             : mod_http2-1.11.3-3.module_el8.1.0+213+acce2796.x86   45/48
  削除             : pcre-utf16-8.42-4.el8.x86_64                         46/48
  削除             : pcre-utf32-8.42-4.el8.x86_64                         47/48
  削除             : pcre-cpp-8.42-4.el8.x86_64                           48/48
  scriptletの実行中: pcre-cpp-8.42-4.el8.x86_64                           48/48
  検証             : apr-1.6.3-9.el8.x86_64                                1/48
  検証             : apr-util-1.6.1-6.el8.x86_64                           2/48
  検証             : apr-util-bdb-1.6.1-6.el8.x86_64                       3/48
  検証             : apr-util-openssl-1.6.1-6.el8.x86_64                   4/48
  検証             : autoconf-2.69-27.el8.noarch                           5/48
  検証             : automake-1.16.1-6.el8.noarch                          6/48
  検証             : centos-logos-httpd-80.5-2.el8.noarch                  7/48
  検証             : cpp-8.3.1-4.5.el8.x86_64                              8/48
  検証             : gcc-8.3.1-4.5.el8.x86_64                              9/48
  検証             : gcc-c++-8.3.1-4.5.el8.x86_64                         10/48
  検証             : glibc-devel-2.28-72.el8.x86_64                       11/48
  検証             : glibc-headers-2.28-72.el8.x86_64                     12/48
  検証             : httpd-2.4.37-16.module_el8.1.0+256+ae790463.x86_64   13/48
  検証             : httpd-filesystem-2.4.37-16.module_el8.1.0+256+ae79   14/48
  検証             : httpd-tools-2.4.37-16.module_el8.1.0+256+ae790463.   15/48
  検証             : isl-0.16.1-6.el8.x86_64                              16/48
  検証             : kernel-headers-4.18.0-147.3.1.el8_1.x86_64           17/48
  検証             : libstdc++-devel-8.3.1-4.5.el8.x86_64                 18/48
  検証             : libtool-2.4.6-25.el8.x86_64                          19/48
  検証             : libxcrypt-devel-4.1.1-4.el8.x86_64                   20/48
  検証             : m4-1.4.18-7.el8.x86_64                               21/48
  検証             : mariadb-3:10.3.17-1.module_el8.1.0+257+48736ea6.x8   22/48
  検証             : mariadb-backup-3:10.3.17-1.module_el8.1.0+257+4873   23/48
  検証             : mariadb-common-3:10.3.17-1.module_el8.1.0+257+4873   24/48
  検証             : mariadb-connector-c-3.0.7-1.el8.x86_64               25/48
  検証             : mariadb-connector-c-config-3.0.7-1.el8.noarch        26/48
  検証             : mariadb-errmsg-3:10.3.17-1.module_el8.1.0+257+4873   27/48
  検証             : mariadb-gssapi-server-3:10.3.17-1.module_el8.1.0+2   28/48
  検証             : mariadb-server-3:10.3.17-1.module_el8.1.0+257+4873   29/48
  検証             : mariadb-server-utils-3:10.3.17-1.module_el8.1.0+25   30/48
  検証             : mod_http2-1.11.3-3.module_el8.1.0+213+acce2796.x86   31/48
  検証             : nginx-filesystem-1:1.14.1-9.module_el8.0.0+184+e34   32/48
  検証             : pcre-cpp-8.42-4.el8.x86_64                           33/48
  検証             : pcre-devel-8.42-4.el8.x86_64                         34/48
  検証             : pcre-utf16-8.42-4.el8.x86_64                         35/48
  検証             : pcre-utf32-8.42-4.el8.x86_64                         36/48
  検証             : perl-DBD-MySQL-4.046-3.module_el8.1.0+203+e45423dc   37/48
  検証             : perl-Thread-Queue-3.13-1.el8.noarch                  38/48
  検証             : php-7.2.11-2.module_el8.1.0+209+03b9a8ff.x86_64      39/48
  検証             : php-cli-7.2.11-2.module_el8.1.0+209+03b9a8ff.x86_6   40/48
  検証             : php-common-7.2.11-2.module_el8.1.0+209+03b9a8ff.x8   41/48
  検証             : php-devel-7.2.11-2.module_el8.1.0+209+03b9a8ff.x86   42/48
  検証             : php-fpm-7.2.11-2.module_el8.1.0+209+03b9a8ff.x86_6   43/48
  検証             : php-gd-7.2.11-2.module_el8.1.0+209+03b9a8ff.x86_64   44/48
  検証             : php-json-7.2.11-2.module_el8.1.0+209+03b9a8ff.x86_   45/48
  検証             : php-mbstring-7.2.11-2.module_el8.1.0+209+03b9a8ff.   46/48
  検証             : php-mysqlnd-7.2.11-2.module_el8.1.0+209+03b9a8ff.x   47/48
  検証             : php-pdo-7.2.11-2.module_el8.1.0+209+03b9a8ff.x86_6   48/48

削除しました:
  httpd-2.4.37-16.module_el8.1.0+256+ae790463.x86_64
  mariadb-3:10.3.17-1.module_el8.1.0+257+48736ea6.x86_64
  mariadb-server-3:10.3.17-1.module_el8.1.0+257+48736ea6.x86_64
  php-7.2.11-2.module_el8.1.0+209+03b9a8ff.x86_64
  php-devel-7.2.11-2.module_el8.1.0+209+03b9a8ff.x86_64
  php-gd-7.2.11-2.module_el8.1.0+209+03b9a8ff.x86_64
  php-json-7.2.11-2.module_el8.1.0+209+03b9a8ff.x86_64
  php-mbstring-7.2.11-2.module_el8.1.0+209+03b9a8ff.x86_64
  php-mysqlnd-7.2.11-2.module_el8.1.0+209+03b9a8ff.x86_64
  php-pdo-7.2.11-2.module_el8.1.0+209+03b9a8ff.x86_64
  apr-1.6.3-9.el8.x86_64
  apr-util-1.6.1-6.el8.x86_64
  apr-util-bdb-1.6.1-6.el8.x86_64
  apr-util-openssl-1.6.1-6.el8.x86_64
  autoconf-2.69-27.el8.noarch
  automake-1.16.1-6.el8.noarch
  centos-logos-httpd-80.5-2.el8.noarch
  cpp-8.3.1-4.5.el8.x86_64
  gcc-8.3.1-4.5.el8.x86_64
  gcc-c++-8.3.1-4.5.el8.x86_64
  glibc-devel-2.28-72.el8.x86_64
  glibc-headers-2.28-72.el8.x86_64
  httpd-filesystem-2.4.37-16.module_el8.1.0+256+ae790463.noarch
  httpd-tools-2.4.37-16.module_el8.1.0+256+ae790463.x86_64
  isl-0.16.1-6.el8.x86_64
  kernel-headers-4.18.0-147.3.1.el8_1.x86_64
  libstdc++-devel-8.3.1-4.5.el8.x86_64
  libtool-2.4.6-25.el8.x86_64
  libxcrypt-devel-4.1.1-4.el8.x86_64
  m4-1.4.18-7.el8.x86_64
  mariadb-backup-3:10.3.17-1.module_el8.1.0+257+48736ea6.x86_64
  mariadb-common-3:10.3.17-1.module_el8.1.0+257+48736ea6.x86_64
  mariadb-connector-c-3.0.7-1.el8.x86_64
  mariadb-connector-c-config-3.0.7-1.el8.noarch
  mariadb-errmsg-3:10.3.17-1.module_el8.1.0+257+48736ea6.x86_64
  mariadb-gssapi-server-3:10.3.17-1.module_el8.1.0+257+48736ea6.x86_64
  mariadb-server-utils-3:10.3.17-1.module_el8.1.0+257+48736ea6.x86_64
  mod_http2-1.11.3-3.module_el8.1.0+213+acce2796.x86_64
  nginx-filesystem-1:1.14.1-9.module_el8.0.0+184+e34fea82.noarch
  pcre-cpp-8.42-4.el8.x86_64
  pcre-devel-8.42-4.el8.x86_64
  pcre-utf16-8.42-4.el8.x86_64
  pcre-utf32-8.42-4.el8.x86_64
  perl-DBD-MySQL-4.046-3.module_el8.1.0+203+e45423dc.x86_64
  perl-Thread-Queue-3.13-1.el8.noarch
  php-cli-7.2.11-2.module_el8.1.0+209+03b9a8ff.x86_64
  php-common-7.2.11-2.module_el8.1.0+209+03b9a8ff.x86_64
  php-fpm-7.2.11-2.module_el8.1.0+209+03b9a8ff.x86_64

完了しました!
```

4.ドキュメントルート内データの削除

```
# rm -rf /var/www/html/*
```

5.mariadb関連ファイルの削除

```
# rm -rf /var/lib/mysql/*
```

***

## 2.Ansibleのインストール

CentOS8_PROXY_DNSの仮想マシンで実行すること

1.ansibleのインストール

{{< accordion >}}
<div>
<pre>
# pip3 install ansible
WARNING: Running pip install with root privileges is generally not a good idea. Try `pip3 install --user` instead.
Collecting ansible
  Downloading https://files.pythonhosted.org/packages/d7/d7/5afcb906038cd8a217ac57110055e27000c5cfe05ecafe969aaa119d1652/ansible-2.9.4.tar.gz (14.2MB)
    100% |????????????????????????????????| 14.2MB 111kB/s
Collecting jinja2 (from ansible)
  Downloading https://files.pythonhosted.org/packages/27/24/4f35961e5c669e96f6559760042a55b9bcfcdb82b9bdb3c8753dbe042e35/Jinja2-2.11.1-py2.py3-none-any.whl (126kB)
    100% |????????????????????????????????| 133kB 1.5MB/s
Requirement already satisfied: PyYAML in /usr/lib64/python3.6/site-packages (from ansible)
Requirement already satisfied: cryptography in /usr/lib64/python3.6/site-packages (from ansible)
Collecting MarkupSafe>=0.23 (from jinja2->ansible)
  Downloading https://files.pythonhosted.org/packages/b2/5f/23e0023be6bb885d00ffbefad2942bc51a620328ee910f64abe5a8d18dd1/MarkupSafe-1.1.1-cp36-cp36m-manylinux1_x86_64.whl
Requirement already satisfied: idna>=2.1 in /usr/lib/python3.6/site-packages (from cryptography->ansible)
Requirement already satisfied: asn1crypto>=0.21.0 in /usr/lib/python3.6/site-packages (from cryptography->ansible)
Requirement already satisfied: six>=1.4.1 in /usr/lib/python3.6/site-packages (from cryptography->ansible)
Requirement already satisfied: cffi!=1.11.3,>=1.7 in /usr/lib64/python3.6/site-packages (from cryptography->ansible)
Requirement already satisfied: pycparser in /usr/lib/python3.6/site-packages (from cffi!=1.11.3,>=1.7->cryptography->ansible)
Installing collected packages: MarkupSafe, jinja2, ansible
  Running setup.py install for ansible ... done
Successfully installed MarkupSafe-1.1.1 ansible-2.9.4 jinja2-2.11.1
</pre>

<pre>
# dnf -y install https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm
メタデータの期限切れの最終確認: 0:31:02 時間前の 2020年02月07日 01時22分47秒 に 実施しました。
epel-release-latest-8.noarch.rpm                 19 kB/s |  21 kB     00:01
依存関係が解決しました。
================================================================================
 パッケージ           Arch           バージョン      リポジトリー         サイズ
================================================================================
インストール:
 epel-release         noarch         8-7.el8         @commandline          21 k

トランザクションの概要
================================================================================
インストール  1 パッケージ

合計サイズ: 21 k
インストール済みのサイズ: 30 k
パッケージのダウンロード:
トランザクションの確認を実行中
トランザクションの確認に成功しました。
トランザクションのテストを実行中
トランザクションのテストに成功しました。
トランザクションを実行中
  準備             :                                                        1/1
  インストール中   : epel-release-8-7.el8.noarch                            1/1
  scriptletの実行中: epel-release-8-7.el8.noarch                            1/1
  検証             : epel-release-8-7.el8.noarch                            1/1

インストール済み:
  epel-release-8-7.el8.noarch

完了しました!
</pre>

<pre>
# dnf -y install sshpass
メタデータの期限切れの最終確認: 0:03:11 時間前の 2020年02月07日 01時54分09秒 に 実施しました。
依存関係が解決しました。
================================================================================
 パッケージ        アーキテクチャー バージョン             リポジトリー   サイズ
================================================================================
インストール:
 sshpass           x86_64           1.06-9.el8             epel            27 k

トランザクションの概要
================================================================================
インストール  1 パッケージ

ダウンロードサイズの合計: 27 k
インストール済みのサイズ: 40 k
パッケージのダウンロード:
sshpass-1.06-9.el8.x86_64.rpm                   186 kB/s |  27 kB     00:00
--------------------------------------------------------------------------------
合計                                             32 kB/s |  27 kB     00:00
警告: /var/cache/dnf/epel-6519ee669354a484/packages/sshpass-1.06-9.el8.x86_64.rpm: ヘッダー V3 RSA/SHA256 Signature、鍵 ID 2f86d6a1: NOKEY
Extra Packages for Enterprise Linux 8 - x86_64  1.6 MB/s | 1.6 kB     00:00
GPG 鍵 0x2F86D6A1 をインポート中:
 Userid     : "Fedora EPEL (8) <epel@fedoraproject.org>"
 Fingerprint: 94E2 79EB 8D8F 25B2 1810 ADF1 21EA 45AB 2F86 D6A1
 From       : /etc/pki/rpm-gpg/RPM-GPG-KEY-EPEL-8
鍵のインポートに成功しました
トランザクションの確認を実行中
トランザクションの確認に成功しました。
トランザクションのテストを実行中
トランザクションのテストに成功しました。
トランザクションを実行中
  準備             :                                                        1/1
  インストール中   : sshpass-1.06-9.el8.x86_64                              1/1
  scriptletの実行中: sshpass-1.06-9.el8.x86_64                              1/1
  検証             : sshpass-1.06-9.el8.x86_64                              1/1

インストール済み:
  sshpass-1.06-9.el8.x86_64

完了しました!
</pre>
</div>
{{< /accordion >}}

2.バージョン確認

{{< accordion >}}
<div>
<pre>
# ansible --version
ansible 2.9.4
  config file = None
  configured module search path = ['/root/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']
  ansible python module location = /usr/local/lib/python3.6/site-packages/ansible
  executable location = /usr/local/bin/ansible
  python version = 3.6.8 (default, Nov 21 2019, 19:31:34) [GCC 8.3.1 20190507 (Red Hat 8.3.1-4)]
</pre>
</div>
{{< /accordion >}}

3.ansibleコマンドでansible-hostへpingを実行

{{< accordion >}}
<div>
<pre>
# ansible 192.168.56.29 -m ping
[WARNING]: No inventory was parsed, only implicit localhost is available

[WARNING]: provided hosts list is empty, only localhost is available. Note that
the implicit localhost does not match 'all'

[WARNING]: Could not match supplied host pattern, ignoring: 192.168.56.29
</pre>
</div>
{{< /accordion >}}

4.ansibleのhostsファイルにansible-hostのグローバルIPを登録

{{< accordion >}}
<div>
<pre>
# mkdir /etc/ansible
</pre>

<pre>
# vim /etc/ansible/hosts

--------------以下の内容をコピー&ペースト--------------
192.168.56.29
---------------[Esc + :wq]で保存終了します。----------
</pre>
</div>
{{< /accordion >}}

5.ansibleコマンドでansible-hostへpingを実行

{{< accordion >}}
<div>
<pre>
# ansible 192.168.56.29 -m ping
The authenticity of host '192.168.56.29 (192.168.56.29)' can't be established.
ECDSA key fingerprint is SHA256:Fy2Wio1WjB5kEHWkB3LYA7SVHWHQb27BVb7/I+lUwo4.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
192.168.56.29 | UNREACHABLE! => {
    "changed": false,
    "msg": "Failed to connect to the host via ssh: Warning: Permanently added '192.168.56.29' (ECDSA) to the list of known hosts.\r\nroot@192.168.56.29: Permission denied (publickey,gssapi-keyex,gssapi-with-mic,password).",
    "unreachable": true
}
</pre>
</div>
{{< /accordion >}}

6.「/root/hostlist」ファイルを作成し、ansible-hostのグローバルIPを登録

{{< accordion >}}
<div>
<pre>
# vim /root/hostlist

--------------以下の内容をコピー&ペースト--------------
192.168.56.29
---------------[Esc + :wq]で保存終了します。----------
</pre>
</div>
{{< /accordion >}}

7.ansibleコマンドでansible-hostへpingを実行

{{< accordion >}}
<div>
<pre>
# ansible 192.168.56.29 -m ping -k
SSH password:tokyoec <font color="Red">//←パスワードを入力</font>
192.168.56.29 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/libexec/platform-python"
    },
    "changed": false,
    "ping": "pong"
}
</pre>
</div>
{{< /accordion >}}

8.鍵の作成

{{< accordion >}}
<div>
<pre>
# ssh-keygen
Generating public/private rsa key pair.
Enter file in which to save the key (/root/.ssh/id_rsa): <font color="Red">//←[Enter]キー</font>
Enter passphrase (empty for no passphrase): <font color="Red">//←[Enter]キー</font>
Enter same passphrase again: <font color="Red">//←[Enter]キー</font>
Your identification has been saved in /root/.ssh/id_rsa.
Your public key has been saved in /root/.ssh/id_rsa.pub.
The key fingerprint is:
SHA256:azyDznQNySVZHRWaOVc/FALA1wdhi49jtREA4WVBJsk root@localhost.localdomain
The key's randomart image is:
+---[RSA 3072]----+
|        o=BX*O=+o|
|        .E=.+==o.|
|        o.o.=+o..|
|       . +  +oo .|
|        S  + o   |
|       o +. .    |
|      o B .      |
|     + o o       |
|      o          |
+----[SHA256]-----+
</pre>
</div>
{{< /accordion >}}

9.ansible-hostに鍵をコピー

{{< accordion >}}
<div>
<pre>
# ssh-copy-id 192.168.56.29
/usr/bin/ssh-copy-id: INFO: Source of key(s) to be installed: "/root/.ssh/id_rsa.pub"
/usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
/usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
root@192.168.56.29's password:tokyoec //←パスワードを入力

Number of key(s) added: 1

Now try logging into the machine, with:   "ssh '192.168.56.29'"
and check to make sure that only the key(s) you wanted were added.
</pre>
</div>
{{< /accordion >}}

10.ansibleコマンドでansible-hostへpingを実行

{{< accordion >}}
<div>
<pre>
# ansible 192.168.56.29 -m ping
192.168.56.29 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/libexec/platform-python"
    },
    "changed": false,
    "ping": "pong"
}
</pre>
</div>
{{< /accordion >}}

***

## 3.Playbookの作成・WordPress環境構築

CentOS8_PROXY_DNSの仮想マシンで実行すること

1.wordpress.ymlの作成

```
# vim wordpress.yml

--------------------以下の内容をコピー&ペーストします。--------------------------------------------------

---
 - name: wordpress環境構築
   hosts: 192.168.56.29
   remote_user: root
   become: yes
   vars:
     wordpress_url: https://ja.wordpress.org/latest-ja.tar.gz
     mysql_user: wordpress
     mysql_password: wppass
     mysql_database: wordpress
     mysql_root_password: mariadb123
            
   tasks:
   - name: Apache（httpd）のインストール
     dnf: name=httpd state=latest
            
   - name: サービスの起動
     service: name=httpd state=started enabled=yes

   - name: PHPのインストール
     dnf: name="{{item}}" state=latest
     with_items:
      - php
      - php-devel
      - php-pdo
      - php-mysqlnd
      - php-mbstring
      - php-json
      - php-gd

   - name: タイムゾーンの設定
     ini_file: >
      dest=/etc/php.ini
      section=Date
      option=date.timezone
      value='"Asia/Tokyo"'

   - name: httpサービスの再起動
     service: name=httpd state=restarted enabled=yes
            
   - name: MariaDBインストール
     dnf: name="{{item}}" state=latest
     with_items:
      - mariadb
      - mariadb-server
      - python3-PyMySQL
      
   - name: サービスの起動
     service: name=mariadb state=started enabled=yes

   - name: WordPress用データベースの作成
     mysql_db: name={{ mysql_database }} state=present

   - name: WordPress用データベースユーザの作成
     mysql_user: name={{ mysql_user }} host={{ item }} password={{ mysql_password }} priv={{ mysql_database }}.*:ALL,GRANT state=present
     with_items:
       - localhost

   - name: MariaDB rootパスワード設定
     mysql_user: name=root
                 host=localhost
                 password="{{ mysql_root_password }}"
                 check_implicit_admin=yes
                 login_user="{{ mysql_user }}"
                 login_password="{{ mysql_root_password }}"
                 state=present
            
   - name: wordpressのダウンロード
     get_url:
       url="{{ wordpress_url }}"
       dest=/tmp/wordpress.tar.gz
            
   - name: wordpressの展開
     unarchive: src=/tmp/wordpress.tar.gz dest=/var/www/html/ copy=no
            
   - name: wordpressの所有権をapacheに変更
     file: path=/var/www/html/wordpress/ owner=apache group=apache recurse=yes

   - name: ディレクトリへのアクセス許可1
     command: chcon -R -t httpd_sys_content_t /var/www/html/wordpress

   - name: ディレクトリへのアクセス許可2
     command: chcon -R -t httpd_sys_rw_content_t /var/www/html/wordpress

   - name: httpサービスの起動
     service: name=httpd state=restarted

   - name: firewalld(http,https)の開放
     become: yes
     firewalld:
       zone: public
       service: "{{ item }}"
       permanent: yes
       state: enabled
     with_items:
       - http
       - https

   - name: 設定の反映
     become: yes
     systemd:
       state: restarted
       name: firewalld
--------------------[Esc + :wq]で保存終了します。-------------------------------------------------------
```

2.ansibleの実行

```
# ansible-playbook wordpress.yml
  PLAY [wordpress環境構築] ****************************************************************************************************************************************

  TASK [Gathering Facts] **************************************************************************************************************************************
  ok: [192.168.56.29]
  
  TASK [Apache（httpd）のインストール] *********************************************************************************************************************************
  changed: [192.168.56.29]
  
  TASK [サービスの起動] **********************************************************************************************************************************************
  changed: [192.168.56.29]
  
  TASK [PHPのインストール] *******************************************************************************************************************************************
  [DEPRECATION WARNING]: Invoking "dnf" only once while using a loop via squash_actions is deprecated. Instead of using a loop to supply multiple items and
  specifying `name: "{{item}}"`, please use `name: ['php', 'php-devel', 'php-pdo', 'php-mysqlnd', 'php-mbstring', 'php-json', 'php-gd']` and remove the loop.
  This feature will be removed in version 2.11. Deprecation warnings can be disabled by setting deprecation_warnings=False in ansible.cfg.
  changed: [192.168.56.29] => (item=['php', 'php-devel', 'php-pdo', 'php-mysqlnd', 'php-mbstring', 'php-json', 'php-gd'])
  
  TASK [タイムゾーンの設定] ********************************************************************************************************************************************
  changed: [192.168.56.29]
  
  TASK [httpサービスの再起動] *****************************************************************************************************************************************
  changed: [192.168.56.29]
  
  TASK [MariaDBインストール] ****************************************************************************************************************************************
  [DEPRECATION WARNING]: Invoking "dnf" only once while using a loop via squash_actions is deprecated. Instead of using a loop to supply multiple items and
  specifying `name: "{{item}}"`, please use `name: ['mariadb', 'mariadb-server', 'python3-PyMySQL']` and remove the loop. This feature will be removed in
  version 2.11. Deprecation warnings can be disabled by setting deprecation_warnings=False in ansible.cfg.
  changed: [192.168.56.29] => (item=['mariadb', 'mariadb-server', 'python3-PyMySQL'])
  
  TASK [サービスの起動] **********************************************************************************************************************************************
  changed: [192.168.56.29]
  
  TASK [WordPress用データベースの作成] **********************************************************************************************************************************
  changed: [192.168.56.29]
  
  TASK [WordPress用データベースユーザの作成] *******************************************************************************************************************************
  changed: [192.168.56.29] => (item=localhost)
  
  TASK [MariaDB rootパスワード設定] **********************************************************************************************************************************
  changed: [192.168.56.29]
  
  TASK [wordpressのダウンロード] *************************************************************************************************************************************
  changed: [192.168.56.29]
  
  TASK [wordpressの展開] *****************************************************************************************************************************************
  changed: [192.168.56.29]
  
  TASK [wordpressの所有権をapacheに変更] ******************************************************************************************************************************
  changed: [192.168.56.29]
  
  TASK [ディレクトリへのアクセス許可1] **************************************************************************************************************************************
  changed: [192.168.56.29]
  
  TASK [ディレクトリへのアクセス許可2] **************************************************************************************************************************************
  changed: [192.168.56.29]
  
  TASK [httpサービスの起動] ******************************************************************************************************************************************
  changed: [192.168.56.29]
  
  TASK [firewalld(http,https)の開放] *****************************************************************************************************************************
  changed: [192.168.56.29] => (item=http)
  changed: [192.168.56.29] => (item=https)
  
  TASK [設定の反映] ************************************************************************************************************************************************
  changed: [192.168.56.29]
  
  PLAY RECAP **************************************************************************************************************************************************
  192.168.56.29              : ok=19   changed=18   unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

3.http://192.168.56.29/wordpress/にアクセス


























***