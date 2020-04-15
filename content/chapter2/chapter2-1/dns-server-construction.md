---
title: "2.DNS Server Construction"
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

## DNSサーバの構築テキスト

CentOS8_PROXY_DNSの仮想マシンで実行すること

1.dnsmasqの稼働確認

{{< accordion >}}
<div>
<pre>
# systemctl status dnsmasq.service
● dnsmasq.service - DNS caching server.
   Loaded: loaded (/usr/lib/systemd/system/dnsmasq.service; disabled; vendor pr>
   Active: inactive (dead)
<font color="Red">//[SPACE]キーでスクロール、[q]キーを入力して終了</font>
</pre>
</div>
{{< /accordion >}}

2.dnsmasqの無効化

{{< accordion >}}
<div>
<pre>
# systemctl mask dnsmasq.service
Created symlink /etc/systemd/system/dnsmasq.service → /dev/null.
</pre>

<pre>
# systemctl status dnsmasq.service
● dnsmasq.service
   Loaded: masked (Reason: Unit dnsmasq.service is masked.)
</pre>
</div>
{{< /accordion >}}

3.BINDをインストール

{{< accordion >}}
<div>
<pre>
# dnf install -y bind bind-utils
メタデータの期限切れの最終確認: 0:36:10 時間前の 2020年02月06日 20時47分42秒 に 実施しました。
パッケージ bind-utils-32:9.11.4-26.P2.el8.x86_64 は既にインストールされています 。
依存関係が解決しました。
================================================================================
 パッケージ  Arch          バージョン                    リポジトリー     サイズ
================================================================================
インストール:
 bind        x86_64        32:9.11.4-26.P2.el8           AppStream        2.1 M

トランザクションの概要
================================================================================
インストール  1 パッケージ

ダウンロードサイズの合計: 2.1 M
インストール済みのサイズ: 4.8 M
パッケージのダウンロード:
bind-9.11.4-26.P2.el8.x86_64.rpm                3.5 MB/s | 2.1 MB     00:00
--------------------------------------------------------------------------------
合計                                            1.8 MB/s | 2.1 MB     00:01
トランザクションの確認を実行中
トランザクションの確認に成功しました。
トランザクションのテストを実行中
トランザクションのテストに成功しました。
トランザクションを実行中
  準備             :                                                        1/1
  scriptletの実行中: bind-32:9.11.4-26.P2.el8.x86_64                        1/1
  インストール中   : bind-32:9.11.4-26.P2.el8.x86_64                        1/1
  scriptletの実行中: bind-32:9.11.4-26.P2.el8.x86_64                        1/1
  検証             : bind-32:9.11.4-26.P2.el8.x86_64                        1/1

インストール済み:
  bind-32:9.11.4-26.P2.el8.x86_64

完了しました!
</pre>
</div>
{{< /accordion >}}

4.BINDの自動起動設定

{{< accordion >}}
<div>
<pre>
# systemctl enable named.service
Created symlink /etc/systemd/system/multi-user.target.wants/named.service → /usr/lib/systemd/system/named.service.
</pre>

<pre>
# systemctl is-enabled named.service
enabled
</pre>
</div>
{{< /accordion >}}

5.BINDの起動

{{< accordion >}}
<div>
<pre>
# systemctl start named.service
</pre>

<pre>
# systemctl status named.service
● named.service - Berkeley Internet Name Domain (DNS)
   Loaded: loaded (/usr/lib/systemd/system/named.service; enabled; vendor preset: disabled)
   Active: active (running) since Thu 2020-02-06 21:24:42 EST; 8s ago
  Process: 12136 ExecStart=/usr/sbin/named -u named -c ${NAMEDCONF} $OPTIONS (code=exited, status=0/SUCCESS)
  Process: 12133 ExecStartPre=/bin/bash -c if [ ! "$DISABLE_ZONE_CHECKING" == "yes" ]; then /usr/sbin/named-checkconf -z "$NAMEDCONF"; else echo "Checking o>
 Main PID: 12138 (named)
    Tasks: 4 (limit: 23983)
   Memory: 54.1M
   CGroup: /system.slice/named.service
           mq12138 /usr/sbin/named -u named -c /etc/named.conf

 2月 06 21:24:42 localhost.localdomain named[12138]: network unreachable resolving './DNSKEY/IN': 2001:500:2f::f#53
 2月 06 21:24:42 localhost.localdomain named[12138]: network unreachable resolving './NS/IN': 2001:500:2f::f#53
 2月 06 21:24:42 localhost.localdomain named[12138]: network unreachable resolving './DNSKEY/IN': 2001:7fd::1#53
 2月 06 21:24:42 localhost.localdomain named[12138]: network unreachable resolving './NS/IN': 2001:7fd::1#53
 2月 06 21:24:42 localhost.localdomain named[12138]: network unreachable resolving './DNSKEY/IN': 2001:500:a8::e#53
 2月 06 21:24:42 localhost.localdomain named[12138]: network unreachable resolving './NS/IN': 2001:500:a8::e#53
 2月 06 21:24:42 localhost.localdomain named[12138]: network unreachable resolving './DNSKEY/IN': 2001:500:9f::42#53
 2月 06 21:24:42 localhost.localdomain named[12138]: network unreachable resolving './NS/IN': 2001:500:9f::42#53
 2月 06 21:24:42 localhost.localdomain named[12138]: managed-keys-zone: Key 20326 for zone . acceptance timer complete: key now trusted
 2月 06 21:24:42 localhost.localdomain named[12138]: resolver priming query complete
 <font color="Red">//[q]キーを入力して終了</font>
</pre>
</div>
{{< /accordion >}}

6.「/etc/named.conf」を設定

{{< accordion >}}
<div>
<pre>
# cp -p /etc/named.conf /etc/named.conf.org
</pre>

<pre>
# vim /etc/named.conf

--------opsions設定の前に、以下の設定を行い、ネットワークグループの作成します。127.0.0.1と192.168.56.0/24を追加します。-----------------
//
// named.conf
//
// Provided by Red Hat bind package to configure the ISC BIND named(8) DNS
// server as a caching only nameserver (as a localhost DNS resolver only).
//
// See /usr/share/doc/bind*/sample/ for example named configuration files.
//

 <font color="Red">//↓追記箇所</font>
acl localnet {
  127.0.0.1;
  192.168.56.0/24;
};
 <font color="Red">//↑追記箇所</font>

options {
  listen-on port 53 { 127.0.0.1; };
  listen-on-v6 port 53 { ::1; };
  directory       "/var/named";
  dump-file       "/var/named/data/cache_dump.db";
  statistics-file "/var/named/data/named_stats.txt";
  memstatistics-file "/var/named/data/named_mem_stats.txt";
  secroots-file   "/var/named/data/named.secroots";
  recursing-file  "/var/named/data/named.recursing";
  allow-query     { localhost; };

・
・省略
・
・
--------------------------------------------------------------------------------------------------------------------------------
</pre>

<pre>
--------optionsのlisten-on portとallow-queryの設定を変更します。------------------------------------------------------------------
//
// named.conf
//
// Provided by Red Hat bind package to configure the ISC BIND named(8) DNS
// server as a caching only nameserver (as a localhost DNS resolver only).
//
// See /usr/share/doc/bind*/sample/ for example named configuration files.
//

 <font color="Red">//↓追記箇所</font>
acl localnet {
  127.0.0.1;
  192.168.56.0/24;
};
 <font color="Red">//↑追記箇所</font>

options {
  listen-on port 53 { 127.0.0.1; 192.168.56.28; };　//←変更箇所
  listen-on-v6 port 53 { ::1; };
  directory       "/var/named";
  dump-file       "/var/named/data/cache_dump.db";
  statistics-file "/var/named/data/named_stats.txt";
  memstatistics-file "/var/named/data/named_mem_stats.txt";
  secroots-file   "/var/named/data/named.secroots";
  recursing-file  "/var/named/data/named.recursing";
  allow-query     { localnet; }; //←変更箇所

・
・省略
・
・
--------------------------------------------------------------------------------------------------------------------------------
</pre>

<pre>
--------最終行に以下、ゾーンファイルの設定を追加します。------------------------------------------------------------------
・
・省略
・
・
include "/etc/named.rfc1912.zones";
include "/etc/named.root.key";

 <font color="Red">//↓追記箇所</font>
zone "example.com" {
  type master;
  file "internal.zone";
};

zone "56.168.192.in-addr.arpa" {
  type master;
  file "internal.rev";
};
 <font color="Red">//↑追記箇所</font>
--------------------[Esc + :wq]で保存終了します。-------------------------------------------------------------------------
</pre>
</div>
{{< /accordion >}}

7.nmcliコマンドで「/etc/resolv.conf」に自身のIPアドレスを設定

{{< accordion >}}
<div>
<pre>
# nmcli con mod enp0s8 ipv4.dns 192.168.56.28
</pre>
</div>
{{< /accordion >}}

8.NetworkManagerを再起動して、設定を反映します。

{{< accordion >}}
<div>
<pre>
# systemctl restart NetworkManager
</pre>

<pre>
# systemctl status NetworkManager
● NetworkManager.service - Network Manager
   Loaded: loaded (/usr/lib/systemd/system/NetworkManager.service; enabled; vendor preset: enabled)
   Active: active (running) since Thu 2020-02-06 21:27:29 EST; 8s ago
     Docs: man:NetworkManager(8)
 Main PID: 12198 (NetworkManager)
    Tasks: 4 (limit: 23983)
   Memory: 6.5M
   CGroup: /system.slice/NetworkManager.service
           mq12198 /usr/sbin/NetworkManager --no-daemon

 2月 06 21:27:29 localhost.localdomain NetworkManager[12198]: <info>  [1581042449.9974] device (enp0s3): state change: secondaries -> activated (reason 'non>
 2月 06 21:27:29 localhost.localdomain NetworkManager[12198]: <info>  [1581042449.9980] manager: NetworkManager state is now CONNECTED_SITE
 2月 06 21:27:30 localhost.localdomain NetworkManager[12198]: <info>  [1581042450.0315] device (enp0s3): Activation: successful, device activated.
 2月 06 21:27:30 localhost.localdomain NetworkManager[12198]: <info>  [1581042450.0322] manager: NetworkManager state is now CONNECTED_GLOBAL
 2月 06 21:27:30 localhost.localdomain NetworkManager[12198]: <info>  [1581042450.0327] device (enp0s8): state change: config -> ip-config (reason 'none', s>
 2月 06 21:27:30 localhost.localdomain NetworkManager[12198]: <info>  [1581042450.0337] device (enp0s8): state change: ip-config -> ip-check (reason 'none',>
 2月 06 21:27:30 localhost.localdomain NetworkManager[12198]: <info>  [1581042450.0821] device (enp0s8): state change: ip-check -> secondaries (reason 'none>
 2月 06 21:27:30 localhost.localdomain NetworkManager[12198]: <info>  [1581042450.0823] device (enp0s8): state change: secondaries -> activated (reason 'non>
 2月 06 21:27:30 localhost.localdomain NetworkManager[12198]: <info>  [1581042450.0874] device (enp0s8): Activation: successful, device activated.
 2月 06 21:27:30 localhost.localdomain NetworkManager[12198]: <info>  [1581042450.0880] manager: startup complete
<font color="Red">//[q]キーを入力して終了</font>
</pre>
</div>
{{< /accordion >}}

9.「/etc/resolv.conf」を確認

{{< accordion >}}
<div>
<pre>
# cat /etc/resolv.conf
# Generated by NetworkManager
search sied.local com
nameserver 192.168.84.41
nameserver 192.168.84.1
nameserver 8.8.8.8
# NOTE: the libc resolver may not support more than 3 nameservers.
# The nameservers listed below may not be recognized.
nameserver 192.168.230.254
nameserver 163.139.230.164
nameserver 192.168.56.28
</pre>
</div>
{{< /accordion >}}

10.192.168.56.28以外のIPアドレスがある場合はコメントアウト

{{< accordion >}}
<div>
<pre>
# vim /etc/resolv.conf

--------------------192.168.56.28以外のIPアドレスがある場合はコメントアウト-------------------------------------------------
# Generated by NetworkManager
search sied.local com
#nameserver 192.168.84.41 <font color="Red">//←#を付けてコメントアウト</font>
#nameserver 192.168.84.1 <font color="Red">//←#を付けてコメントアウト</font>
#nameserver 8.8.8.8 <font color="Red">//←#を付けてコメントアウト</font>
# NOTE: the libc resolver may not support more than 3 nameservers.
# The nameservers listed below may not be recognized.
#nameserver 192.168.230.254 <font color="Red">//←#を付けてコメントアウト</font>
#nameserver 163.139.230.164 <font color="Red">//←#を付けてコメントアウト</font>
nameserver 192.168.56.28
--------------------[Esc + :wq]で保存終了します。-------------------------------------------------------------------------
</pre>
</div>
{{< /accordion >}}

11.ゾーンファイルの作成

{{< accordion >}}
<div>
<pre>
# vim /var/named/internal.zone

------------------------------------------------------------------------------------------------------------------------
$TTL 86400
@       IN  SOA  ns.example.com.  root.example.com.( 
          2016072601  ; serial              
          21600       ; refresh after 6 hours
          3600        ; retry after 1 hour
          604800      ; expire after 1 week
          86400 )     ; minimum TTL of 1 day
;
        IN  NS    ns
;
ns      IN  A     192.168.56.28
www     IN  A     192.168.56.28
ftp     IN  A     192.168.56.29
--------------------[Esc + :wq]で保存終了します。-------------------------------------------------------------------------
</pre>
</div>
{{< /accordion >}}

12.ゾーンファイル(逆引き)の作成

{{< accordion >}}
<div>
<pre>
# vim /var/named/internal.rev

-------------------------------------------------------------------------------------------------------------------------
$TTL 86400
@         IN  SOA  ns.example.com.  root.example.com. (
            2016072601  ; serial
            21600       ; refresh after 6 hours
            3600        ; retry after 1 hour
            604800      ; expire after 1 week
            86400 )     ; minimum TTL of 1 day
; 
    IN  NS    ns.example.com.
28	IN  PTR  www.example.com.
29	IN  PTR  ftp.example.com.
--------------------[Esc + :wq]で保存終了します。-------------------------------------------------------------------------
</pre>
</div>
{{< /accordion >}}

13.BINDの再起動

{{< accordion >}}
<div>
<pre>
# systemctl restart named.service
</pre>

<pre>
# systemctl status named.service
● named.service - Berkeley Internet Name Domain (DNS)
   Loaded: loaded (/usr/lib/systemd/system/named.service; enabled; vendor preset: disabled)
   Active: active (running) since Thu 2020-02-06 21:29:51 EST; 7s ago
  Process: 12319 ExecStop=/bin/sh -c /usr/sbin/rndc stop > /dev/null 2>&1 || /bin/kill -TERM $MAINPID (code=exited, status=0/SUCCESS)
  Process: 12334 ExecStart=/usr/sbin/named -u named -c ${NAMEDCONF} $OPTIONS (code=exited, status=0/SUCCESS)
  Process: 12331 ExecStartPre=/bin/bash -c if [ ! "$DISABLE_ZONE_CHECKING" == "yes" ]; then /usr/sbin/named-checkconf -z "$NAMEDCONF"; else echo "Checking o>
 Main PID: 12336 (named)
    Tasks: 4 (limit: 23983)
   Memory: 53.7M
   CGroup: /system.slice/named.service
           mq12336 /usr/sbin/named -u named -c /etc/named.conf

 2月 06 21:29:51 localhost.localdomain named[12336]: network unreachable resolving './DNSKEY/IN': 2001:500:2f::f#53
 2月 06 21:29:51 localhost.localdomain named[12336]: network unreachable resolving './NS/IN': 2001:500:2f::f#53
 2月 06 21:29:51 localhost.localdomain named[12336]: network unreachable resolving './DNSKEY/IN': 2001:500:1::53#53
 2月 06 21:29:51 localhost.localdomain named[12336]: network unreachable resolving './NS/IN': 2001:500:1::53#53
 2月 06 21:29:51 localhost.localdomain named[12336]: network unreachable resolving './DNSKEY/IN': 2001:503:c27::2:30#53
 2月 06 21:29:51 localhost.localdomain named[12336]: network unreachable resolving './NS/IN': 2001:503:c27::2:30#53
 2月 06 21:29:51 localhost.localdomain named[12336]: network unreachable resolving './DNSKEY/IN': 2001:503:ba3e::2:30#53
 2月 06 21:29:51 localhost.localdomain named[12336]: network unreachable resolving './NS/IN': 2001:503:ba3e::2:30#53
 2月 06 21:29:51 localhost.localdomain named[12336]: managed-keys-zone: Key 20326 for zone . acceptance timer complete: key now trusted
 2月 06 21:29:51 localhost.localdomain named[12336]: resolver priming query complete
<font color="Red">//[q]キーを入力して終了</font>
</pre>
</div>
{{< /accordion >}}

14.nslookupコマンドで確認（正引）

{{< accordion >}}
<div>
<pre>
# nslookup
> server 192.168.56.28
Default server: 192.168.56.28
Address: 192.168.56.28#53
> www.example.com
Server:         192.168.56.18
Address:        192.168.56.18#53

Name:   www.example.com
Address: 192.168.56.28
> exit
</pre>
</div>
{{< /accordion >}}

15.nslookupコマンドで確認（逆引）

{{< accordion >}}
<div>
<pre>
# nslookup
> server 192.168.56.28
Default server: 192.168.56.28
Address: 192.168.56.28#53
> 192.168.56.28
28.56.168.192.in-addr.arpa      name = www.example.com.
> 192.168.56.29
29.56.168.192.in-addr.arpa      name = ftp.example.com.
> exit
</pre>
</div>
{{< /accordion >}}

16.外部からも名前解決できるようにfirewalldでdnsを解放

{{< accordion >}}
<div>
<pre>
# firewall-cmd --add-service=dns --zone=public --permanent
success
</pre>
</div>
{{< /accordion >}}

17.設定を反映

{{< accordion >}}
<div>
<pre>
# firewall-cmd --reload
success
</pre>
</div>
{{< /accordion >}}