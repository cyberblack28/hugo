---
title: "Exercise2 DNS Command"
date: 2017-10-17T15:26:15Z
draft: false
weight: 10
---

## 1.whoisコマンド

1.rootユーザに変更してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ su -
パスワード:tokyoec
#
</pre>
</div>
</details>
{{< /accordion >}}

2.以下の手順に従ってwhoisコマンドをインストールします。

```
# yum install epel-release
メタデータの期限切れの最終確認: 0:06:17 時間前の 2020年02月03日 20時19分21秒 に 実施しました。
依存関係が解決しました。
================================================================================
 パッケージ            Arch            バージョン         リポジトリー    サイズ
================================================================================
インストール:
 epel-release          noarch          8-5.el8            extras           22 k

トランザクションの概要
================================================================================
インストール  1 パッケージ

ダウンロードサイズの合計: 22 k
インストール済みのサイズ: 30 k
これでよろしいですか? [y/N]: y
パッケージのダウンロード:
epel-release-8-5.el8.noarch.rpm                  88 kB/s |  22 kB     00:00
--------------------------------------------------------------------------------
合計                                             25 kB/s |  22 kB     00:00
トランザクションの確認を実行中
トランザクションの確認に成功しました。
トランザクションのテストを実行中
トランザクションのテストに成功しました。
トランザクションを実行中
  準備             :                                                        1/1
  インストール中   : epel-release-8-5.el8.noarch                            1/1
  scriptletの実行中: epel-release-8-5.el8.noarch                            1/1
  検証             : epel-release-8-5.el8.noarch                            1/1

インストール済み:
  epel-release-8-5.el8.noarch

完了しました!
```

```
# yum config-manager --set-enabled PowerTools
# yum repolist
CentOS-8 - AppStream                            9.3 kB/s | 4.3 kB     00:00
CentOS-8 - Base                                 5.1 kB/s | 3.8 kB     00:00
CentOS-8 - Extras                               2.9 kB/s | 1.5 kB     00:00
CentOS-8 - PowerTools                           198 kB/s | 2.0 MB     00:10
Extra Packages for Enterprise Linux 8 - x86_64  184 kB/s | 5.5 MB     00:30
repo id            repo の名前                                             状態
AppStream          CentOS-8 - AppStream                                    5,001
BaseOS             CentOS-8 - Base                                         1,784
PowerTools         CentOS-8 - PowerTools                                   1,499
*epel              Extra Packages for Enterprise Linux 8 - x86_64          4,643
extras             CentOS-8 - Extras                                           3
```

```
# yum search whois
メタデータの期限切れの最終確認: 0:00:39 時間前の 2020年02月03日 20時26分35秒 に 実施しました。
=========================== 名前 & 概要 一致: whois ============================
whois.x86_64 : Improved WHOIS client
whois-nls.noarch : Gettext catalogs for whois tools
```

```
# yum info whois
メタデータの期限切れの最終確認: 0:00:50 時間前の 2020年02月03日 20時26分35秒 に 実施しました。
利用可能なパッケージ
名前         : whois
バージョン   : 5.5.1
リリース     : 1.el8
Arch         : x86_64
サイズ       : 77 k
ソース       : whois-5.5.1-1.el8.src.rpm
リポジトリー : epel
概要         : Improved WHOIS client
URL          : http://www.linux.it/~md/software/
ライセンス   : GPLv2+
説明         : Searches for an object in a RFC 3912 database.
             :
             : This version of the WHOIS client tries to guess the right server
             : to ask for the specified object. If no guess can be made it will
             : connect to whois.networksolutions.com for NIC handles or
             : whois.arin.net for IPv4 addresses and network names.
```

```
# yum -y install whois
メタデータの期限切れの最終確認: 0:01:13 時間前の 2020年02月03日 20時26分35秒 に 実施しました。
依存関係が解決しました。
================================================================================
 パッケージ         Arch            バージョン              リポジトリー  サイズ
================================================================================
インストール:
 whois              x86_64          5.5.1-1.el8             epel           77 k
依存関係のインストール:
 whois-nls          noarch          5.5.1-1.el8             epel           37 k

トランザクションの概要
================================================================================
インストール  2 パッケージ

ダウンロードサイズの合計: 114 k
インストール済みのサイズ: 343 k
パッケージのダウンロード:
(1/2): whois-nls-5.5.1-1.el8.noarch.rpm         120 kB/s |  37 kB     00:00
(2/2): whois-5.5.1-1.el8.x86_64.rpm             202 kB/s |  77 kB     00:00
--------------------------------------------------------------------------------
合計                                             59 kB/s | 114 kB     00:01
警告: /var/cache/dnf/epel-6519ee669354a484/packages/whois-5.5.1-1.el8.x86_64.rpm: ヘッダー V3 RSA/SHA256 Signature、鍵 ID 2f86d6a1: NOKEY
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
  インストール中   : whois-nls-5.5.1-1.el8.noarch                           1/2
  インストール中   : whois-5.5.1-1.el8.x86_64                               2/2
  scriptletの実行中: whois-5.5.1-1.el8.x86_64                               2/2
  検証             : whois-5.5.1-1.el8.x86_64                               1/2
  検証             : whois-nls-5.5.1-1.el8.noarch                           2/2

インストール済み:
  whois-5.5.1-1.el8.x86_64             whois-nls-5.5.1-1.el8.noarch

完了しました!
```

```
# rpm -qa | grep whois
whois-nls-5.5.1-1.el8.noarch
whois-5.5.1-1.el8.x86_64
```

3.whoisコマンドでtokyo-ec.ac.jpドメインを確認してください。

```
# whois tokyo-ec.ac.jp
  [ JPRS database provides information on network administration. Its use is    ]
  [ restricted to network administration purposes. For further information,     ]
  [ use 'whois -h whois.jprs.jp help'. To suppress Japanese output, add'/e'     ]
  [ at the end of command, e.g. 'whois -h whois.jprs.jp xxx/e'.                 ]
  
  Domain Information: [ドメイン情報]
  a. [ドメイン名]                 TOKYO-EC.AC.JP
  e. [そしきめい]                 がっこうほうじん でんぱがくえん
  f. [組織名]                     学校法人 電波学園
  g. [Organization]               EDUCATIONAL FOUNDATION DENPA GAKUEN
  k. [組織種別]                   学校法人
  l. [Organization Type]          EDUCATIONAL FOUNDATION
  m. [登録担当者]                 MY54761JP
  n. [技術連絡担当者]             MA27235JP
  p. [ネームサーバ]               dns-b.iij.ad.jp
  p. [ネームサーバ]               dns-c.iij.ad.jp
  s. [署名鍵]
  [状態]                          Connected (2021/01/31)
  [登録年月日]                    1997/01/24
  [接続年月日]                    1997/01/24
  [最終更新]                      2020/02/01 01:01:34 (JST)
```

4.studentユーザに戻ってください。

```
# exit
ログアウト
$
```

***

## 2.nslookupコマンド

1.nslookupコマンドを利用して、tokyo-ec.ac.jpのグローバルIPアドレスを調べてください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ nslookup tokyo-ec.ac.jp
Server:         192.168.84.41
Address:        192.168.84.41#53

Non-authoritative answer:
Name:   tokyo-ec.ac.jp
Address: 103.4.43.184
</pre>
</div>
</details>
{{< /accordion >}}

2.nslookupコマンドの対話形式で、tokyo-ec.ac.jpのグローバルIPアドレスを調べてください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ nslookup //[Enter]キー
> tokyo-ec.ac.jp
Server:         192.168.84.41
Address:        192.168.84.41#53

Non-authoritative answer:
Name:   tokyo-ec.ac.jp
Address: 103.4.43.184
> exit
$
</pre>
</div>
</details>
{{< /accordion >}}

***

## 3.digコマンド

1.digコマンドを利用して、tokyo-ec.ac.jpのaレコード情報を調べてください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ dig tokyo-ec.ac.jp a

; <<>> DiG 9.11.4-P2-RedHat-9.11.4-26.P2.el8 <<>> tokyo-ec.ac.jp a
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 58746
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 4000
;; QUESTION SECTION:
;tokyo-ec.ac.jp.                        IN      A

;; ANSWER SECTION:
tokyo-ec.ac.jp.         21288   IN      A       103.4.43.184

;; Query time: 4 msec
;; SERVER: 192.168.84.41#53(192.168.84.41)
;; WHEN: 月  2月 03 21:00:27 EST 2020
;; MSG SIZE  rcvd: 59
</pre>
</div>
</details>
{{< /accordion >}}

2.digコマンドを利用して、tokyo-ec.ac.jpのmxレコード情報を調べてください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ dig tokyo-ec.ac.jp mx

; <<>> DiG 9.11.4-P2-RedHat-9.11.4-26.P2.el8 <<>> tokyo-ec.ac.jp mx
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 21880
;; flags: qr rd ra; QUERY: 1, ANSWER: 2, AUTHORITY: 0, ADDITIONAL: 9
  
;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 4000
;; QUESTION SECTION:
;tokyo-ec.ac.jp.                        IN      MX
  
;; ANSWER SECTION:
tokyo-ec.ac.jp.         21599   IN      MX      120 mx6.securemx.jp.
tokyo-ec.ac.jp.         21599   IN      MX      100 mx.securemx.jp.
  
;; ADDITIONAL SECTION:
mx6.securemx.jp.        18      IN      AAAA    2001:240:bb81::4:501
mx6.securemx.jp.        18      IN      AAAA    2001:240:bb81::4:521
mx6.securemx.jp.        18      IN      AAAA    2001:240:bb81::4:500
mx6.securemx.jp.        18      IN      AAAA    2001:240:bb81::4:520
mx.securemx.jp.         348     IN      A       210.130.202.98
mx.securemx.jp.         348     IN      A       210.130.202.123
mx.securemx.jp.         348     IN      A       210.130.202.122
mx.securemx.jp.         348     IN      A       210.130.202.97
  
;; Query time: 29 msec
;; SERVER: 192.168.84.41#53(192.168.84.41)
;; WHEN: 月  2月 03 21:02:50 EST 2020
;; MSG SIZE  rcvd: 267
</pre>
</div>
</details>
{{< /accordion >}}

3.digコマンドを利用して、tokyo-ec.ac.jpのnsレコード情報を調べてください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ dig tokyo-ec.ac.jp ns

; <<>> DiG 9.11.4-P2-RedHat-9.11.4-26.P2.el8 <<>> tokyo-ec.ac.jp ns
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 10797
;; flags: qr rd ra; QUERY: 1, ANSWER: 2, AUTHORITY: 0, ADDITIONAL: 5

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 4000
;; QUESTION SECTION:
;tokyo-ec.ac.jp.                        IN      NS

;; ANSWER SECTION:
tokyo-ec.ac.jp.         21599   IN      NS      dns-c.iij.ad.jp.
tokyo-ec.ac.jp.         21599   IN      NS      dns-b.iij.ad.jp.

;; ADDITIONAL SECTION:
dns-c.iij.ad.jp.        19795   IN      A       210.130.1.15
dns-c.iij.ad.jp.        8239    IN      AAAA    2001:240:bb81::2:15
dns-b.iij.ad.jp.        21303   IN      A       202.232.2.14
dns-b.iij.ad.jp.        21433   IN      AAAA    2001:240:bb81::2:14

;; Query time: 28 msec
;; SERVER: 192.168.84.41#53(192.168.84.41)
;; WHEN: 月  2月 03 21:07:20 EST 2020
;; MSG SIZE  rcvd: 178
</pre>
</div>
</details>
{{< /accordion >}}

4.digコマンドを利用して、tokyo-ec.ac.jpのsoaレコード情報を調べてください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
# ip r
default via 10.0.2.2 dev enp0s3 proto dhcp metric 102
10.0.2.0/24 dev enp0s3 proto kernel scope link src 10.0.2.15 metric 102
192.168.56.0/24 dev enp0s8 proto kernel scope link src 192.168.56.18 metric 101
192.168.122.0/24 dev virbr0 proto kernel scope link src 192.168.122.1 linkdown
</pre>

<pre>
# ip route
default via 10.0.2.2 dev enp0s3 proto dhcp metric 102
10.0.2.0/24 dev enp0s3 proto kernel scope link src 10.0.2.15 metric 102
192.168.56.0/24 dev enp0s8 proto kernel scope link src 192.168.56.18 metric 101
192.168.122.0/24 dev virbr0 proto kernel scope link src 192.168.122.1 linkdown
</pre>

<pre>
# ip route show
default via 10.0.2.2 dev enp0s3 proto dhcp metric 102
10.0.2.0/24 dev enp0s3 proto kernel scope link src 10.0.2.15 metric 102
192.168.56.0/24 dev enp0s8 proto kernel scope link src 192.168.56.18 metric 101
192.168.122.0/24 dev virbr0 proto kernel scope link src 192.168.122.1 linkdown
</pre>

<pre>
# ip route list
default via 10.0.2.2 dev enp0s3 proto dhcp metric 102
10.0.2.0/24 dev enp0s3 proto kernel scope link src 10.0.2.15 metric 102
192.168.56.0/24 dev enp0s8 proto kernel scope link src 192.168.56.18 metric 101
192.168.122.0/24 dev virbr0 proto kernel scope link src 192.168.122.1 linkdown
</pre>
</div>
</details>
{{< /accordion >}}

5.routeコマンドを使って、ルーティングテーブルを確認してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
# route
Kernel IP routing table
Destination     Gateway         Genmask         Flags Metric Ref    Use Iface
default         _gateway        0.0.0.0         UG    102    0        0 enp0s3
10.0.2.0        0.0.0.0         255.255.255.0   U     102    0        0 enp0s3
192.168.56.0    0.0.0.0         255.255.255.0   U     101    0        0 enp0s8
192.168.122.0   0.0.0.0         255.255.255.0   U     0      0        0 virbr0
</pre>
</div>
</details>
{{< /accordion >}}

6.studentユーザに戻ってください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
# exit
ログアウト
$
</pre>
</div>
</details>
{{< /accordion >}}

***

## 4.hostコマンド

1.hostコマンドを利用して、tokyo-ec.ac.jpのグローバルIPアドレスを調べてください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ host tokyo-ec.ac.jp
tokyo-ec.ac.jp has address 103.4.43.184
tokyo-ec.ac.jp mail is handled by 100 mx.securemx.jp.
tokyo-ec.ac.jp mail is handled by 120 mx6.securemx.jp.
</pre>
</div>
</details>
{{< /accordion >}}

2.hostコマンドを利用して、tokyo-ec.ac.jpのaレコード情報を調べてください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ host -t a tokyo-ec.ac.jp
host -t a tokyo-ec.ac.jp
tokyo-ec.ac.jp has address 103.4.43.184
</pre>
</div>
</details>
{{< /accordion >}}

3.hostコマンドを利用して、tokyo-ec.ac.jpのmxレコード情報を調べてください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ host -t mx tokyo-ec.ac.jp
tokyo-ec.ac.jp mail is handled by 120 mx6.securemx.jp.
tokyo-ec.ac.jp mail is handled by 100 mx.securemx.jp.
</pre>
</div>
</details>
{{< /accordion >}}

4.hostコマンドを利用して、tokyo-ec.ac.jpのnsレコード情報を調べてください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ host -t ns tokyo-ec.ac.jp
tokyo-ec.ac.jp name server dns-b.iij.ad.jp.
tokyo-ec.ac.jp name server dns-c.iij.ad.jp.
</pre>
</div>
</details>
{{< /accordion >}}

5.hostコマンドを利用して、tokyo-ec.ac.jpのsoaレコード情報を調べてください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ host -t soa tokyo-ec.ac.jp
tokyo-ec.ac.jp has SOA record dns-b.iij.ad.jp. dns-managers.iij.ad.jp. 1553222258 3600 1800 3600000 900
</pre>
</div>
</details>
{{< /accordion >}}

6.hostコマンドを利用して、103.4.43.184のptrレコード情報を調べてください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ host -t ptr 103.4.43.184
184.43.4.103.in-addr.arpa domain name pointer h103004043184.mediagalaxy.ne.jp.
</pre>
</div>
</details>
{{< /accordion >}}