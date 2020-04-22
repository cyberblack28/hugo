---
title: "Exercise3 Networkmanager"
date: 2017-10-17T15:26:15Z
draft: false
weight: 10
---

## 1.nmcliコマンド～インターフェイス編～

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

2.nmcliコマンドを利用して、enp0s3の現在設定されているIPアドレスを表示してください。「grep IP4」を利用してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
# nmcli connection show enp0s3 | grep IP4
IP4.ADDRESS[1]:                         10.0.2.15/24
IP4.GATEWAY:                            10.0.2.2
IP4.ROUTE[1]:                           dst = 0.0.0.0/0, nh = 10.0.2.2, mt = 100
IP4.ROUTE[2]:                           dst = 10.0.2.0/24, nh = 0.0.0.0, mt = 100
IP4.DNS[1]:                             192.168.84.41
IP4.DNS[2]:                             192.168.84.1
IP4.DNS[3]:                             8.8.8.8
IP4.DNS[4]:                             192.168.230.254
IP4.DNS[5]:                             163.139.230.164
IP4.DOMAIN[1]:                          sied.local
</pre>
</div>
</details>
{{< /accordion >}}

3.nmcliコマンドを利用して、手動設定に切り替えてenp0s3のIPアドレスを「10.0.2.0/24」に変更してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
# nmcli connection modify enp0s3 ipv4.method manual ipv4.address 10.0.2.0/24
</pre>

<pre>
# nmcli connection modify enp0s3 ipv4.address 10.0.2.0/24
</pre>
</div>
</details>
{{< /accordion >}}

4.手動設定に切り替えたものを自動構成（DHCP）に戻してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
# nmcli connection modify enp0s3 ipv4.method auto
</pre>
</div>
</details>
{{< /accordion >}}

5.設定を反映するために、「systemctl restart NetworkManager」を実行し、enp0s3にIPアドレスが割り当てられているか確認してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
# systemctl restart NetworkManager
# ip address show enp0s3
2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:a3:26:3e brd ff:ff:ff:ff:ff:ff
    inet 10.0.2.15/24 brd 10.0.2.255 scope global dynamic noprefixroute enp0s3
       valid_lft 86393sec preferred_lft 86393sec
    inet6 fe80::acad:70d1:c57a:b0db/64 scope link noprefixroute
       valid_lft forever preferred_lft forever
</pre>
</div>
</details>
{{< /accordion >}}

6.nmcliコマンドを利用して、接続一覧を確認してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
# nmcli connection show
NAME    UUID                                  TYPE      DEVICE
enp0s3  dd400f88-eb57-4065-9f99-ebc71df3e564  ethernet  enp0s3
enp0s8  00cb8299-feb9-55b6-a378-3fdc720e0bc6  ethernet  enp0s8
virbr0  61f17c29-8ead-41bc-aaf7-5695636060f5  bridge    virbr0
</pre>
</div>
</details>
{{< /accordion >}}

7.nmcliコマンドを利用して、enp0s3インターフェイスを無効にしてください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
# nmcli connection down enp0s3
接続 'enp0s3' が正常に非アクティブ化されました (D-Bus アクティブパス: /org/freedesktop/NetworkManager/ActiveConnection/1)
</pre>
</div>
</details>
{{< /accordion >}}

8.nmcliコマンドを利用して、enp0s3インターフェイスを有効にしてください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
# nmcli connection up enp0s3
接続が正常にアクティベートされました (D-Bus アクティブパス: /org/freedesktop/NetworkManager/ActiveConnection/4)
</pre>

<pre>
# nmcli connection show
  NAME    UUID                                  TYPE      DEVICE
  enp0s3  dd400f88-eb57-4065-9f99-ebc71df3e564  ethernet  enp0s3
  enp0s8  00cb8299-feb9-55b6-a378-3fdc720e0bc6  ethernet  enp0s8
  virbr0  61f17c29-8ead-41bc-aaf7-5695636060f5  bridge    virbr0
</pre>
</div>
</details>
{{< /accordion >}}

9.studentユーザに戻りましょう。

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

## 2.nmcliコマンド～ホスト名編～

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

2.nmcliコマンドを利用して、ホスト名を「tokyo-ec.com」に変更してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
# nmcli general hostname tokyo-ec.com
# hostnamectl status
   Static hostname: tokyo-ec.com
Transient hostname: tokyoec.com
         Icon name: computer-vm
           Chassis: vm
        Machine ID: ec3013fcd5694968ae0536d059095897
           Boot ID: c193b869958c41588ad66301b47c88cd
    Virtualization: oracle
  Operating System: CentOS Linux 8 (Core)
       CPE OS Name: cpe:/o:centos:centos:8
            Kernel: Linux 4.18.0-147.3.1.el8_1.x86_64
      Architecture: x86-64
</pre>
</div>
</details>
{{< /accordion >}}

3.systemctlコマンドを利用してsystemd-hostnamedをrestartして、hostnamectlコマンドを利用して、ホスト名情報を確認してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
# systemctl restart systemd-hostnamed
</pre>

<pre>
# hostnamectl status
   Static hostname: tokyo-ec.com
         Icon name: computer-vm
           Chassis: vm
        Machine ID: ec3013fcd5694968ae0536d059095897
           Boot ID: c193b869958c41588ad66301b47c88cd
    Virtualization: oracle
  Operating System: CentOS Linux 8 (Core)
       CPE OS Name: cpe:/o:centos:centos:8
            Kernel: Linux 4.18.0-147.3.1.el8_1.x86_64
      Architecture: x86-64
</pre>
</div>
</details>
{{< /accordion >}}

4.catコマンドで/etc/hostnameファイルを確認してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
# cat /etc/hostname
tokyo-ec.com
</pre>
</div>
</details>
{{< /accordion >}}

5.studentユーザに戻りましょう。

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

## 3.nmtuiコマンド

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

2.nmtuiコマンドを実行して、[接続の編集]-[enp0s3]-[取り消し]-[back]-[終了]を選択して、一連の流れを確認してください。

※操作は矢印キーとEnterキーで行えます。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
# nmtui

[接続の編集]

<img src="/images/exercise3-networkmanager-01.png">

[enp0s3]

<img src="/images/exercise3-networkmanager-02.png">

[取り消し]

<img src="/images/exercise3-networkmanager-03.png">

[戻る]

<img src="/images/exercise3-networkmanager-04.png">

[終了]

<img src="/images/exercise3-networkmanager-04.png">

</pre>
</div>
</details>
{{< /accordion >}}

3.studentユーザに戻りましょう。

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