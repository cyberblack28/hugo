---
title: "14.Docker Compose"
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

***

## Docker Composeのインストール

1.jqのインストール

{{< accordion >}}
<div>
<pre>
# dnf -y install jq
メタデータの期限切れの最終確認: 0:00:09 時間前の 2020年02月18日 21時40分32秒 に 実施しました。
依存関係が解決しました。
================================================================================
 パッケージ        Arch           バージョン            リポジトリー      サイズ
================================================================================
インストール:
 jq                x86_64         1.5-12.el8            AppStream         161 k
依存関係のインストール:
 oniguruma         x86_64         6.8.2-1.el8           AppStream         188 k

トランザクションの概要
================================================================================
インストール  2 パッケージ

ダウンロードサイズの合計: 349 k
インストール済みのサイズ: 1.0 M
パッケージのダウンロード:
(1/2): jq-1.5-12.el8.x86_64.rpm                 1.4 MB/s | 161 kB     00:00
(2/2): oniguruma-6.8.2-1.el8.x86_64.rpm         1.6 MB/s | 188 kB     00:00
--------------------------------------------------------------------------------
合計                                            680 kB/s | 349 kB     00:00
トランザクションの確認を実行中
トランザクションの確認に成功しました。
トランザクションのテストを実行中
トランザクションのテストに成功しました。
トランザクションを実行中
  準備             :                                                        1/1
  インストール中   : oniguruma-6.8.2-1.el8.x86_64                           1/2
  scriptletの実行中: oniguruma-6.8.2-1.el8.x86_64                           1/2
  インストール中   : jq-1.5-12.el8.x86_64                                   2/2
  scriptletの実行中: jq-1.5-12.el8.x86_64                                   2/2
  検証             : jq-1.5-12.el8.x86_64                                   1/2
  検証             : oniguruma-6.8.2-1.el8.x86_64                           2/2

インストール済み:
  jq-1.5-12.el8.x86_64               oniguruma-6.8.2-1.el8.x86_64

完了しました!
</pre>
</div>
{{< /accordion >}}

2.インストールスクリプトの作成

{{< accordion >}}
<div>
<pre>
# vim docker-compose-install.sh

----------------------------------------------------以下の内容をコピー&ペースト--------------------------------------------------
#!/bin/bash
compose_version=$(curl https://api.github.com/repos/docker/compose/releases/latest | jq .name -r)
output='/usr/local/bin/docker-compose'
curl -L https://github.com/docker/compose/releases/download/$compose_version/docker-compose-$(uname -s)-$(uname -m) -o $output
chmod +x $output
echo $(docker-compose --version)
----------------------------------------------------[Esc + :wq]で保存終了します。-----------------------------------------------
</pre>

<pre>
# chmod +x docker-compose-install.sh
</pre>
</div>
{{< /accordion >}}

3.インストールスクリプトの実行

{{< accordion >}}
<div>
<pre>
# sh docker-compose-install.sh
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 19166  100 19166    0     0  67964      0 --:--:-- --:--:-- --:--:-- 67964
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   617  100   617    0     0   1742      0 --:--:-- --:--:-- --:--:--  1762
100 16.3M  100 16.3M    0     0  2621k      0  0:00:06  0:00:06 --:--:-- 3824k
docker-compose version 1.25.4, build 8d51620a
</pre>
</div>
{{< /accordion >}}

***

## docker-compose.ymlファイルの作成

1.docker-compose.ymlファイルの作成

{{< accordion >}}
<div>
<pre>
# vim docker-compose.yml

----------------------------------------------------以下の内容をコピー&ペースト--------------------------------------------------
version: '3'

services:
   db:
     image: mysql:5.7
     volumes:
       - db_data:/var/lib/mysql
     restart: always
     env_file: .env

   wordpress:
     depends_on:
       - db
     image: wordpress:latest
     ports:
       - "8080:80"
     restart: always
     environment:
       WORDPRESS_DB_HOST: db:3306
     env_file: .env

volumes:
    db_data:
     driver: local
----------------------------------------------------[Esc + :wq]で保存終了します。-----------------------------------------------
</pre>
</div>
{{< /accordion >}}

2..envファイルの作成

{{< accordion >}}
<div>
<pre>
# vim .env

----------------------------------------------------以下の内容をコピー&ペースト--------------------------------------------------
MYSQL_ROOT_PASSWORD=somewordpress
MYSQL_DATABASE=wordpress
MYSQL_USER=wordpress
MYSQL_PASSWORD=wordpress
WORDPRESS_DB_USER=wordpress
WORDPRESS_DB_PASSWORD=wordpress
----------------------------------------------------[Esc + :wq]で保存終了します。-----------------------------------------------
</pre>
</div>
{{< /accordion >}}

***

## WordPressコンテナーとMySQLコンテナーの起動

1.WordPressコンテナーとMySQLコンテナーの起動

```
# docker-compose up -d
Creating network "build_wordpress_default" with the default driver
Creating volume "build_wordpress_db_data" with local driver
Pulling db (mysql:5.7)...
5.7: Pulling from library/mysql
619014d83c02: Pull complete
9ced578c3a5f: Pull complete
731f6e13d8ea: Pull complete
3c183de42679: Pull complete
6de69b5c2f3c: Pull complete
00f0a4086406: Pull complete
84d93aea836d: Pull complete
e2dd1f3e5a3d: Pull complete
98fb37478ee6: Pull complete
57eb21662ebf: Pull complete
e95057f0a050: Pull complete
Digest: sha256:cf6899e980c38071a78ded028de40e65286bfbbb746b97617ac4c9a84c4e812d
Status: Downloaded newer image for mysql:5.7
Pulling wordpress (wordpress:latest)...
latest: Pulling from library/wordpress
bc51dd8edc1b: Pull complete
a3224e2c3a89: Pull complete
be7a066df88f: Pull complete
bfdf741d72a9: Pull complete
a9e612a5f04c: Pull complete
c026d8d0e8cb: Pull complete
d94096c4941c: Pull complete
5a16031a7587: Pull complete
0cf1daf9efc0: Pull complete
b202acb13a6c: Pull complete
907001e30880: Pull complete
2e4b329c80b2: Pull complete
cd1ec92e7164: Pull complete
8cba435f5ca6: Pull complete
42d9ff86311d: Pull complete
4907cef4e3ab: Pull complete
d9efb2f24248: Pull complete
8301b0ae2103: Pull complete
a9e295ae3552: Pull complete
cd1a22f91cdc: Pull complete
f81677d558c1: Pull complete
Digest: sha256:d9664204507998c812efc3a20d3d320724068b8ff308e99ff1329ada8ce70abc
Status: Downloaded newer image for wordpress:latest
Creating build_wordpress_db_1 ... done
Creating build_wordpress_wordpress_1 ... done
```

2.ブラウザを起動して「http://192.168.56.29:8080」にアクセス