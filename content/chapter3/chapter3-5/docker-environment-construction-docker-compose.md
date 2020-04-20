---
title: "1.Docker Environment Construction - Docker Compose"
date: 2017-10-17T15:26:15Z
draft: false
weight: 10
---

## Docker Composeのインストール

1.jqのインストール

```
# apt -y install jq
Reading package lists... Done
Building dependency tree
Reading state information... Done
The following additional packages will be installed:
  libjq1 libonig4
The following NEW packages will be installed:
  jq libjq1 libonig4
0 upgraded, 3 newly installed, 0 to remove and 102 not upgraded.
Need to get 276 kB of archives.
After this operation, 930 kB of additional disk space will be used.
Get:1 http://mirror.kakao.com/ubuntu bionic/universe amd64 libonig4 amd64 6.7.0-1 [119 kB]
Get:2 http://mirror.kakao.com/ubuntu bionic/universe amd64 libjq1 amd64 1.5+dfsg-2 [111 kB]
Get:3 http://mirror.kakao.com/ubuntu bionic/universe amd64 jq amd64 1.5+dfsg-2 [45.6 kB]
Fetched 276 kB in 0s (571 kB/s)
Selecting previously unselected package libonig4:amd64.
(Reading database ... 65920 files and directories currently installed.)
Preparing to unpack .../libonig4_6.7.0-1_amd64.deb ...
Unpacking libonig4:amd64 (6.7.0-1) ...
Selecting previously unselected package libjq1:amd64.
Preparing to unpack .../libjq1_1.5+dfsg-2_amd64.deb ...
Unpacking libjq1:amd64 (1.5+dfsg-2) ...
Selecting previously unselected package jq.
Preparing to unpack .../jq_1.5+dfsg-2_amd64.deb ...
Unpacking jq (1.5+dfsg-2) ...
Setting up libonig4:amd64 (6.7.0-1) ...
Setting up libjq1:amd64 (1.5+dfsg-2) ...
Processing triggers for libc-bin (2.27-3ubuntu1) ...
Processing triggers for man-db (2.8.3-2ubuntu0.1) ...
Setting up jq (1.5+dfsg-2) ...
```

2.Docker Composeインストールスクリプトの作成

```
# vim docker-compose-install.sh
----------------------------------------------------------------------------------------------------------------------------------
#!/bin/bash
compose_version=$(curl https://api.github.com/repos/docker/compose/releases/latest | jq .name -r)
output='/usr/local/bin/docker-compose'
curl -L https://github.com/docker/compose/releases/download/$compose_version/docker-compose-$(uname -s)-$(uname -m) -o $output
chmod +x $output
echo $(docker-compose --version)
----------------------------------------------------------------------------------------------------------------------------------
Esc + :wq
```

3.権限付与

```
# chmod +x docker-compose-install.sh
```

4.スクリプト実行

```
# sh docker-compose-install.sh
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 19171    0 19171    0     0  73734      0 --:--:-- --:--:-- --:--:-- 73734
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   617  100   617    0     0  17628      0 --:--:-- --:--:-- --:--:-- 17628
100 16.3M  100 16.3M    0     0  2763k      0  0:00:06  0:00:06 --:--:-- 3178k
docker-compose version 1.25.4, build 8d51620a
```

***

## docker-compose.ymlの作成

1.docker-compose.ymlの作成

```
# vim docker-compose.yml
```

```YAML
version: '3.7'

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
```

***

## .envファイルの作成

1.docker-compose.ymlの作成

```
# vim .env
----------------------------------------------------------------
MYSQL_ROOT_PASSWORD=somewordpress
MYSQL_DATABASE=wordpress
MYSQL_USER=wordpress
MYSQL_PASSWORD=wordpress
WORDPRESS_DB_USER=wordpress
WORDPRESS_DB_PASSWORD=wordpress
----------------------------------------------------------------
Esc + :wq
```

## WordPressコンテナーの一括起動

1.コンテナー一括起動

```
# docker-compose up -d
Creating network "root_default" with the default driver
Creating volume "root_db_data" with local driver
Pulling db (mysql:5.7)...
5.7: Pulling from library/mysql
c499e6d256d6: Pull complete
22c4cdf4ea75: Pull complete
6ff5091a5a30: Pull complete
2fd3d1af9403: Pull complete
0d9d26127d1d: Pull complete
54a67d4e7579: Pull complete
fe989230d866: Pull complete
466a91a95e2f: Pull complete
3e4554c238f1: Pull complete
603b48ead88c: Pull complete
1e86a9aa7171: Pull complete
Digest: sha256:fbaeced79cfdae5d3c8d4a8c41e883f254f72ed7428c6b93a498824b76d97121
Status: Downloaded newer image for mysql:5.7
Pulling wordpress (wordpress:latest)...
latest: Pulling from library/wordpress
c499e6d256d6: Already exists
3a635b94b3b9: Pull complete
cf28be682a33: Pull complete
b7118ab6e551: Pull complete
925f628a16b8: Pull complete
a77cff9973b5: Pull complete
9b4f44173a15: Pull complete
c9bd6c436ae3: Pull complete
399316af3112: Pull complete
3cea11f54c61: Pull complete
1ebb66998d8f: Pull complete
ac288a1a6e08: Pull complete
776d750cfd59: Pull complete
a997f5c2f033: Pull complete
a41091590f04: Pull complete
6b1397000eb2: Pull complete
7b387d8d3957: Pull complete
04673b988ee3: Pull complete
0e2da6305da6: Pull complete
f0224352bc00: Pull complete
d5e8b4e26a84: Pull complete
Digest: sha256:191d5caf4ef5b8c57721ade777820f3267654325f7902b2ccd377ceeba1c3fe2
Status: Downloaded newer image for wordpress:latest
Creating root_db_1 ... done
Creating root_wordpress_1 ... done
```

2.ブラウザアクセス

```
「http://グローバルIPアドレス:8080/」
```

***

## Volumeについて

1.volume名の確認

```
# docker volume ls
DRIVER              VOLUME NAME
local               a7ed8567fa175dd6ea30bd45688d10fbb732e9739c186d5828595df75b329e86
local               build_wordpress_db_data
```

2.Linuxホストの以下ディレクトリでtestという空ファイルを作成

```
# touch /var/lib/docker/volumes/build_wordpress_db_data/_data/test
```

```
# ls /var/lib/docker/volumes/build_wordpress_db_data/_data/
auto.cnf         client-key.pem  ib_logfile1         private_key.pem  sys
ca-key.pem       ib_buffer_pool  ibtmp1              public_key.pem   test
ca.pem           ibdata1         mysql               server-cert.pem  wordpress
client-cert.pem  ib_logfile0     performance_schema  server-key.pem
```

3.MySQLのコンテナーID確認

```
# docker container ls
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                  NAMES
2be1b85662fc        wordpress:latest    "docker-entrypoint.s…"   2 minutes ago       Up 2 minutes        0.0.0.0:8080->80/tcp   build_wordpress_wordpress_1
2f9a12197ea0        mysql:5.7           "docker-entrypoint.s…"   2 minutes ago       Up 2 minutes        3306/tcp, 33060/tcp    build_wordpress_db_1
```

4.MySQLコンテナーの中からも確認

```
# docker container exec -it 2f9a12197ea0 /bin/bash
```

5.コンテナーでもtest2という空ファイルを作成して、Linuxホストから確認

```
root@2f9a12197ea0:/# touch /var/lib/mysql/test2
```

```
root@2f9a12197ea0:/# ls /var/lib/mysql
auto.cnf         client-key.pem  ibdata1             private_key.pem  sys
ca-key.pem       ib_buffer_pool  ibtmp1              public_key.pem   test
ca.pem           ib_logfile0     mysql               server-cert.pem  test2
client-cert.pem  ib_logfile1     performance_schema  server-key.pem   wordpress
```

```
root@2f9a12197ea0:/# exit
exit
```

6.Linuxホストで確認

```
# ls /var/lib/docker/volumes/build_wordpress_db_data/_data/
auto.cnf         client-key.pem  ib_logfile1         private_key.pem  sys
ca-key.pem       ib_buffer_pool  ibtmp1              public_key.pem   test
ca.pem           ibdata1         mysql               server-cert.pem  test2
client-cert.pem  ib_logfile0     performance_schema  server-key.pem   wordpress
```