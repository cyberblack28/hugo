---
title: "3.Proxy Server Construction"
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

## PROXYサーバの構築テキスト

CentOS8_PROXY_DNSの仮想マシンで実行すること

1.Nginxのインストール

{{< accordion >}}
<div>
<pre>
# dnf -y install nginx
メタデータの期限切れの最終確認: 0:00:19 時間前の 2020年02月05日 00時09分34秒 に 実施しました。
依存関係が解決しました。
================================================================================
 パッケージ       Arch   バージョン                             Repo      サイズ
================================================================================
インストール:
 nginx            x86_64 1:1.14.1-9.module_el8.0.0+184+e34fea82 AppStream 570 k
依存関係のインストール:
 nginx-all-modules
                  noarch 1:1.14.1-9.module_el8.0.0+184+e34fea82 AppStream  23 k
 nginx-filesystem noarch 1:1.14.1-9.module_el8.0.0+184+e34fea82 AppStream  24 k
 nginx-mod-http-image-filter
                  x86_64 1:1.14.1-9.module_el8.0.0+184+e34fea82 AppStream  35 k
 nginx-mod-http-perl
                  x86_64 1:1.14.1-9.module_el8.0.0+184+e34fea82 AppStream  45 k
 nginx-mod-http-xslt-filter
                  x86_64 1:1.14.1-9.module_el8.0.0+184+e34fea82 AppStream  33 k
 nginx-mod-mail   x86_64 1:1.14.1-9.module_el8.0.0+184+e34fea82 AppStream  64 k
 nginx-mod-stream x86_64 1:1.14.1-9.module_el8.0.0+184+e34fea82 AppStream  85 k
モジュールストリームの有効化:
 nginx                   1.14

トランザクションの概要
================================================================================
インストール  8 パッケージ

ダウンロードサイズの合計: 881 k
インストール済みのサイズ: 2.0 M
パッケージのダウンロード:
(1/8): nginx-all-modules-1.14.1-9.module_el8.0. 174 kB/s |  23 kB     00:00
(2/8): nginx-filesystem-1.14.1-9.module_el8.0.0 180 kB/s |  24 kB     00:00
(3/8): nginx-mod-http-image-filter-1.14.1-9.mod 604 kB/s |  35 kB     00:00
(4/8): nginx-mod-http-perl-1.14.1-9.module_el8. 504 kB/s |  45 kB     00:00
(5/8): nginx-mod-http-xslt-filter-1.14.1-9.modu 677 kB/s |  33 kB     00:00
(6/8): nginx-mod-mail-1.14.1-9.module_el8.0.0+1 1.0 MB/s |  64 kB     00:00
(7/8): nginx-1.14.1-9.module_el8.0.0+184+e34fea 1.8 MB/s | 570 kB     00:00
(8/8): nginx-mod-stream-1.14.1-9.module_el8.0.0 984 kB/s |  85 kB     00:00
--------------------------------------------------------------------------------
合計                                            1.2 MB/s | 881 kB     00:00
トランザクションの確認を実行中
トランザクションの確認に成功しました。
トランザクションのテストを実行中
トランザクションのテストに成功しました。
トランザクションを実行中
  準備             :                                                        1/1
  scriptletの実行中: nginx-filesystem-1:1.14.1-9.module_el8.0.0+184+e34fe   1/8
  インストール中   : nginx-filesystem-1:1.14.1-9.module_el8.0.0+184+e34fe   1/8
  インストール中   : nginx-mod-http-image-filter-1:1.14.1-9.module_el8.0.   2/8
  scriptletの実行中: nginx-mod-http-image-filter-1:1.14.1-9.module_el8.0.   2/8
  インストール中   : nginx-mod-http-perl-1:1.14.1-9.module_el8.0.0+184+e3   3/8
  scriptletの実行中: nginx-mod-http-perl-1:1.14.1-9.module_el8.0.0+184+e3   3/8
  インストール中   : nginx-mod-http-xslt-filter-1:1.14.1-9.module_el8.0.0   4/8
  scriptletの実行中: nginx-mod-http-xslt-filter-1:1.14.1-9.module_el8.0.0   4/8
  インストール中   : nginx-mod-mail-1:1.14.1-9.module_el8.0.0+184+e34fea8   5/8
  scriptletの実行中: nginx-mod-mail-1:1.14.1-9.module_el8.0.0+184+e34fea8   5/8
  インストール中   : nginx-all-modules-1:1.14.1-9.module_el8.0.0+184+e34f   6/8
  インストール中   : nginx-1:1.14.1-9.module_el8.0.0+184+e34fea82.x86_64    7/8
  scriptletの実行中: nginx-1:1.14.1-9.module_el8.0.0+184+e34fea82.x86_64    7/8
  インストール中   : nginx-mod-stream-1:1.14.1-9.module_el8.0.0+184+e34fe   8/8
  scriptletの実行中: nginx-mod-stream-1:1.14.1-9.module_el8.0.0+184+e34fe   8/8
  検証             : nginx-1:1.14.1-9.module_el8.0.0+184+e34fea82.x86_64    1/8
  検証             : nginx-all-modules-1:1.14.1-9.module_el8.0.0+184+e34f   2/8
  検証             : nginx-filesystem-1:1.14.1-9.module_el8.0.0+184+e34fe   3/8
  検証             : nginx-mod-http-image-filter-1:1.14.1-9.module_el8.0.   4/8
  検証             : nginx-mod-http-perl-1:1.14.1-9.module_el8.0.0+184+e3   5/8
  検証             : nginx-mod-http-xslt-filter-1:1.14.1-9.module_el8.0.0   6/8
  検証             : nginx-mod-mail-1:1.14.1-9.module_el8.0.0+184+e34fea8   7/8
  検証             : nginx-mod-stream-1:1.14.1-9.module_el8.0.0+184+e34fe   8/8

インストール済み:
  nginx-1:1.14.1-9.module_el8.0.0+184+e34fea82.x86_64
  nginx-all-modules-1:1.14.1-9.module_el8.0.0+184+e34fea82.noarch
  nginx-filesystem-1:1.14.1-9.module_el8.0.0+184+e34fea82.noarch
  nginx-mod-http-image-filter-1:1.14.1-9.module_el8.0.0+184+e34fea82.x86_64
  nginx-mod-http-perl-1:1.14.1-9.module_el8.0.0+184+e34fea82.x86_64
  nginx-mod-http-xslt-filter-1:1.14.1-9.module_el8.0.0+184+e34fea82.x86_64
  nginx-mod-mail-1:1.14.1-9.module_el8.0.0+184+e34fea82.x86_64
  nginx-mod-stream-1:1.14.1-9.module_el8.0.0+184+e34fea82.x86_64

完了しました!
</pre>
</div>
{{< /accordion >}}

2.Nginxのバージョン確認

{{< accordion >}}
<div>
<pre>
# nginx -v
nginx version: nginx/1.14.1
</pre>
</div>
{{< /accordion >}}

3.Nginxの自動起動設定

{{< accordion >}}
<div>
<pre>
# systemctl enable nginx
Created symlink /etc/systemd/system/multi-user.target.wants/nginx.service → /usr/lib/systemd/system/nginx.service.
</pre>

<pre>
# systemctl list-unit-files --type=service | grep nginx
nginx.service                              enabled
</pre>
</div>
{{< /accordion >}}

4.Nginxの起動

{{< accordion >}}
<div>
<pre>
# systemctl start nginx
</pre>

<pre>
# systemctl status nginx
  ● nginx.service - The nginx HTTP and reverse proxy server
  Loaded: loaded (/usr/lib/systemd/system/nginx.service; enabled; vendor preset: disabled)
 Drop-In: /usr/lib/systemd/system/nginx.service.d
          mqphp-fpm.conf
  Active: active (running) since Thu 2020-02-06 21:37:01 EST; 9s ago
 Process: 13132 ExecStart=/usr/sbin/nginx (code=exited, status=0/SUCCESS)
 Process: 13130 ExecStartPre=/usr/sbin/nginx -t (code=exited, status=0/SUCCESS)
 Process: 13129 ExecStartPre=/usr/bin/rm -f /run/nginx.pid (code=exited, status=0/SUCCESS)
Main PID: 13134 (nginx)
   Tasks: 2 (limit: 23983)
  Memory: 4.0M
  CGroup: /system.slice/nginx.service
          tq13134 nginx: master process /usr/sbin/nginx
          mq13135 nginx: worker process

2月 06 21:37:01 localhost.localdomain systemd[1]: Starting The nginx HTTP and reverse proxy server...
2月 06 21:37:01 localhost.localdomain nginx[13130]: nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
2月 06 21:37:01 localhost.localdomain nginx[13130]: nginx: configuration file /etc/nginx/nginx.conf test is successful
2月 06 21:37:01 localhost.localdomain systemd[1]: nginx.service: Failed to parse PID from file /run/nginx.pid: Invalid argument
2月 06 21:37:01 localhost.localdomain systemd[1]: Started The nginx HTTP and reverse proxy server.
 <font color="Red">//[q]キーを入力して終了</font>
</pre>
</div>
{{< /accordion >}}

5.リバースプロキシの設定

{{< accordion >}}
<div>
<pre>
# vim /etc/nginx/conf.d/proxy.conf

----------------------------------------------------------------------------------------
server{
  server_name    *.example.com;
  server_name    192.168.56.29;
  server_tokens off;
            
  proxy_set_header    Host    $host;
  proxy_set_header    X-Real-IP    $remote_addr;
  proxy_set_header    X-Forwarded-Host       $host;
  proxy_set_header    X-Forwarded-Server    $host;
  proxy_set_header    X-Forwarded-For    $proxy_add_x_forwarded_for;
            
  location / {
    proxy_pass    http://192.168.56.29/;
  }
}
-----------------------[Esc + :wq]で保存終了します。--------------------------------------
</pre>
</div>
{{< /accordion >}}

6.Nginxを再起動

{{< accordion >}}
<div>
<pre>
# systemctl restart nginx
</pre>
</div>
{{< /accordion >}}

7.外部からアクセスできるようにfirewalldでhttpを解放

{{< accordion >}}
<div>
<pre>
# firewall-cmd --add-service=http --zone=public --permanent
success
</pre>
</div>
{{< /accordion >}}

8.設定を反映

{{< accordion >}}
<div>
<pre>
# firewall-cmd --reload
success
</pre>
</div>
{{< /accordion >}}