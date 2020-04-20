---
title: "1.Ansible Environment Construction - SSH"
date: 2017-10-17T15:26:15Z
draft: false
weight: 10
---

## SSH設定変更手順

ansible-host作業

1.元ファイルのバックアップ

```
# cp -p /etc/ssh/sshd_config /etc/ssh/sshd_config.org
```

2.sshd_configの設定変更

```
# vim /etc/ssh/sshd_config

---------------------以下赤字の内容に変更---------------------------
・
・省略
・
#LoginGraceTime 2m
PermitRootLogin yes <font color="Red">//←「PermitRootLogin no」変更⇒「PermitRootLogin yes」</font>
#StrictModes yes
#MaxAuthTries 6
#MaxSessions 10
・
・省略
・
# To disable tunneled clear text passwords, change to no here!
PasswordAuthentication yes <font color="Red">//←「PasswordAuthentication no」変更⇒「PasswordAuthentication yes」</font>
#PermitEmptyPasswords no
PasswordAuthentication yes <font color="Red">//←「PasswordAuthentication no」変更⇒「PasswordAuthentication yes」</font>
・
・省略
・
---------------------[Esc + :wq]で保存終了します。-------------------------
```

3.sshdの再起動

```
# systemctl restart sshd
```