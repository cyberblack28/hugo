---
title: "8.Exercise2 firewalld"
date: 2017-10-17T15:26:15Z
draft: false
weight: 10
---

## 1.firewalldサービスの状態確認

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

2.firewalld サービスが実行されているかどうかを確認します。実行されていない場合は、実行してみましょう。実行されている場合は、実行する場合はどうするか考えてみましょう。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
# systemctl status firewalld
● firewalld.service - firewalld - dynamic firewall daemon
   Loaded: loaded (/usr/lib/systemd/system/firewalld.service; enabled; vendor preset: enabled)
   Active: active (running) since Thu 2020-02-06 20:37:53 EST; 1h 34min ago
     Docs: man:firewalld(1)
 Main PID: 1019 (firewalld)
    Tasks: 3 (limit: 23983)
   Memory: 34.7M
   CGroup: /system.slice/firewalld.service
           mq1019 /usr/libexec/platform-python -s /usr/sbin/firewalld --nofork --nopid

 2月 06 21:38:50 localhost.localdomain firewalld[1019]: WARNING: COMMAND_FAILED: '/usr/sbin/iptables -w10 -w --table filter --delete FORWARD --destination 1>
 2月 06 21:38:50 localhost.localdomain firewalld[1019]: WARNING: COMMAND_FAILED: '/usr/sbin/iptables -w10 -w --table filter --delete FORWARD --source 192.16>
 2月 06 21:38:50 localhost.localdomain firewalld[1019]: WARNING: COMMAND_FAILED: '/usr/sbin/iptables -w10 -w --table filter --delete FORWARD --in-interface >
 2月 06 21:38:50 localhost.localdomain firewalld[1019]: WARNING: COMMAND_FAILED: '/usr/sbin/iptables -w10 -w --table filter --delete FORWARD --out-interface>
 2月 06 21:38:50 localhost.localdomain firewalld[1019]: WARNING: COMMAND_FAILED: '/usr/sbin/iptables -w10 -w --table filter --delete FORWARD --in-interface >
 2月 06 21:38:50 localhost.localdomain firewalld[1019]: WARNING: COMMAND_FAILED: '/usr/sbin/iptables -w10 -w --table filter --delete INPUT --in-interface vi>
 2月 06 21:38:50 localhost.localdomain firewalld[1019]: WARNING: COMMAND_FAILED: '/usr/sbin/iptables -w10 -w --table filter --delete INPUT --in-interface vi>
 2月 06 21:38:50 localhost.localdomain firewalld[1019]: WARNING: COMMAND_FAILED: '/usr/sbin/iptables -w10 -w --table filter --delete OUTPUT --out-interface >
 2月 06 21:38:50 localhost.localdomain firewalld[1019]: WARNING: COMMAND_FAILED: '/usr/sbin/iptables -w10 -w --table filter --delete INPUT --in-interface vi>
 2月 06 21:38:50 localhost.localdomain firewalld[1019]: WARNING: COMMAND_FAILED: '/usr/sbin/iptables -w10 -w --table filter --delete INPUT --in-interface vi
<font color="Red">//[q]キーを入力して終了</font>
</pre>
</div>
</details>
{{< /accordion >}}

***

## 2.ファイアウォールゾーンの確認

1.デフォルトのファイアウォールゾーンが public に設定されていることを確認してみましょう。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
# firewall-cmd --get-default-zone
public
</pre>
</div>
</details>
{{< /accordion >}}

***

## 3.不要なポートの確認

1.public ゾーンに対する永続的な設定で、不要なポートが開いていないことを確認してみましょう。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
# firewall-cmd --permanent --zone=public --list-all
public
  target: default
  icmp-block-inversion: no
  interfaces:
  sources:
  services: cockpit dhcpv6-client dns http https ssh
  ports:
  protocols:
  masquerade: no
  forward-ports:
  source-ports:
  icmp-blocks:
  rich rules:
</pre>
</div>
</details>
{{< /accordion >}}

***

## 4.ポートの開放

1.ポート 8080/TCP を public ゾーンの永続的な設定に追加して、設定を確認してみましょう。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
# firewall-cmd --permanent --zone=public --add-port 8080/tcp
success
</pre>

<pre>
# firewall-cmd --permanent --zone=public --list-all
public
  target: default
  icmp-block-inversion: no
  interfaces:
  sources:
  services: cockpit dhcpv6-client dns http https ssh
  ports: 8080/tcp
  protocols:
  masquerade: no
  forward-ports:
  source-ports:
  icmp-blocks:
  rich rules:
</pre>
</div>
</details>
{{< /accordion >}}

2.studentユーザに戻りましょう。

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