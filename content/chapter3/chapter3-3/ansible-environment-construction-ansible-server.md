---
title: "2.Ansible Environment Construction - Ansible-Server"
date: 2017-10-17T15:26:15Z
draft: false
weight: 10
---

## ansible-serverの作成手順

ansible-server作業

1.ansibleのインストール

```
# yum -y install ansible
Loaded plugins: fastestmirror
Determining fastest mirrors
epel/x86_64/metalink                                     | 8.8 kB     00:00
 * epel: ftp.iij.ad.jp
base                                                     | 3.6 kB     00:00
epel                                                     | 5.3 kB     00:00
extras                                                   | 2.9 kB     00:00
updates                                                  | 2.9 kB     00:00
(1/7): epel/x86_64/group_gz                                |  90 kB   00:00
(2/7): epel/x86_64/updateinfo                              | 1.0 MB   00:00
(3/7): epel/x86_64/primary_db                              | 6.9 MB   00:00
(4/7): updates/7/x86_64/primary_db                         | 6.7 MB   00:01
(5/7): extras/7/x86_64/primary_db                          | 159 kB   00:02
(6/7): base/7/x86_64/primary_db                            | 6.0 MB   00:03
(7/7): base/7/x86_64/group_gz                              | 165 kB   00:07
Resolving Dependencies
--> Running transaction check
---> Package ansible.noarch 0:2.9.3-1.el7 will be installed
--> Processing Dependency: python-httplib2 for package: ansible-2.9.3-1.el7.noarch
--> Processing Dependency: python-paramiko for package: ansible-2.9.3-1.el7.noarch
--> Processing Dependency: python2-cryptography for package: ansible-2.9.3-1.el7.noarch
--> Processing Dependency: python2-jmespath for package: ansible-2.9.3-1.el7.noarch
--> Processing Dependency: sshpass for package: ansible-2.9.3-1.el7.noarch
--> Running transaction check
---> Package python-httplib2.noarch 0:0.9.2-1.el7 will be installed
---> Package python-paramiko.noarch 0:2.1.1-9.el7 will be installed
--> Processing Dependency: python2-pyasn1 for package: python-paramiko-2.1.1-9.el7.noarch
---> Package python2-cryptography.x86_64 0:1.7.2-2.el7 will be installed
--> Processing Dependency: python-idna >= 2.0 for package: python2-cryptography-1.7.2-2.el7.x86_64
--> Processing Dependency: python-cffi >= 1.4.1 for package: python2-cryptography-1.7.2-2.el7.x86_64
--> Processing Dependency: python-enum34 for package: python2-cryptography-1.7.2-2.el7.x86_64
---> Package python2-jmespath.noarch 0:0.9.0-3.el7 will be installed
---> Package sshpass.x86_64 0:1.06-2.el7 will be installed
--> Running transaction check
---> Package python-cffi.x86_64 0:1.6.0-5.el7 will be installed
--> Processing Dependency: python-pycparser for package: python-cffi-1.6.0-5.el7.x86_64
---> Package python-enum34.noarch 0:1.0.4-1.el7 will be installed
---> Package python-idna.noarch 0:2.4-1.el7 will be installed
---> Package python2-pyasn1.noarch 0:0.1.9-7.el7 will be installed
--> Running transaction check
---> Package python-pycparser.noarch 0:2.14-1.el7 will be installed
--> Processing Dependency: python-ply for package: python-pycparser-2.14-1.el7.noarch
--> Running transaction check
---> Package python-ply.noarch 0:3.4-11.el7 will be installed
--> Finished Dependency Resolution

Dependencies Resolved

================================================================================
 Package                    Arch         Version             Repository    Size
================================================================================
Installing:
 ansible                    noarch       2.9.3-1.el7         epel          17 M
Installing for dependencies:
 python-cffi                x86_64       1.6.0-5.el7         base         218 k
 python-enum34              noarch       1.0.4-1.el7         base          52 k
 python-httplib2            noarch       0.9.2-1.el7         extras       115 k
 python-idna                noarch       2.4-1.el7           base          94 k
 python-paramiko            noarch       2.1.1-9.el7         base         269 k
 python-ply                 noarch       3.4-11.el7          base         123 k
 python-pycparser           noarch       2.14-1.el7          base         104 k
 python2-cryptography       x86_64       1.7.2-2.el7         base         502 k
 python2-jmespath           noarch       0.9.0-3.el7         extras        39 k
 python2-pyasn1             noarch       0.1.9-7.el7         base         100 k
 sshpass                    x86_64       1.06-2.el7          extras        21 k

Transaction Summary
================================================================================
Install  1 Package (+11 Dependent packages)

Total download size: 19 M
Installed size: 112 M
Downloading packages:
(1/12): ansible-2.9.3-1.el7.noarch.rpm                     |  17 MB   00:01
(2/12): python-enum34-1.0.4-1.el7.noarch.rpm               |  52 kB   00:01
(3/12): python-cffi-1.6.0-5.el7.x86_64.rpm                 | 218 kB   00:02
(4/12): python-idna-2.4-1.el7.noarch.rpm                   |  94 kB   00:00
(5/12): python-ply-3.4-11.el7.noarch.rpm                   | 123 kB   00:00
(6/12): python-paramiko-2.1.1-9.el7.noarch.rpm             | 269 kB   00:00
(7/12): python-httplib2-0.9.2-1.el7.noarch.rpm             | 115 kB   00:03
(8/12): python-pycparser-2.14-1.el7.noarch.rpm             | 104 kB   00:00
(9/12): python2-pyasn1-0.1.9-7.el7.noarch.rpm              | 100 kB   00:00
(10/12): python2-cryptography-1.7.2-2.el7.x86_64.rpm       | 502 kB   00:00
(11/12): python2-jmespath-0.9.0-3.el7.noarch.rpm           |  39 kB   00:01
(12/12): sshpass-1.06-2.el7.x86_64.rpm                     |  21 kB   00:01
--------------------------------------------------------------------------------
Total                                              4.0 MB/s |  19 MB  00:04
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  Installing : python2-pyasn1-0.1.9-7.el7.noarch                           1/12
  Installing : python-enum34-1.0.4-1.el7.noarch                            2/12
  Installing : python-httplib2-0.9.2-1.el7.noarch                          3/12
  Installing : sshpass-1.06-2.el7.x86_64                                   4/12
  Installing : python2-jmespath-0.9.0-3.el7.noarch                         5/12
  Installing : python-ply-3.4-11.el7.noarch                                6/12
  Installing : python-pycparser-2.14-1.el7.noarch                          7/12
  Installing : python-cffi-1.6.0-5.el7.x86_64                              8/12
  Installing : python-idna-2.4-1.el7.noarch                                9/12
  Installing : python2-cryptography-1.7.2-2.el7.x86_64                    10/12
  Installing : python-paramiko-2.1.1-9.el7.noarch                         11/12
  Installing : ansible-2.9.3-1.el7.noarch                                 12/12
  Verifying  : python-idna-2.4-1.el7.noarch                                1/12
  Verifying  : python-pycparser-2.14-1.el7.noarch                          2/12
  Verifying  : python-ply-3.4-11.el7.noarch                                3/12
  Verifying  : python2-jmespath-0.9.0-3.el7.noarch                         4/12
  Verifying  : python-paramiko-2.1.1-9.el7.noarch                          5/12
  Verifying  : python-cffi-1.6.0-5.el7.x86_64                              6/12
  Verifying  : sshpass-1.06-2.el7.x86_64                                   7/12
  Verifying  : python-httplib2-0.9.2-1.el7.noarch                          8/12
  Verifying  : python2-pyasn1-0.1.9-7.el7.noarch                           9/12
  Verifying  : python-enum34-1.0.4-1.el7.noarch                           10/12
  Verifying  : python2-cryptography-1.7.2-2.el7.x86_64                    11/12
  Verifying  : ansible-2.9.3-1.el7.noarch                                 12/12

Installed:
  ansible.noarch 0:2.9.3-1.el7

Dependency Installed:
  python-cffi.x86_64 0:1.6.0-5.el7
  python-enum34.noarch 0:1.0.4-1.el7
  python-httplib2.noarch 0:0.9.2-1.el7
  python-idna.noarch 0:2.4-1.el7
  python-paramiko.noarch 0:2.1.1-9.el7
  python-ply.noarch 0:3.4-11.el7
  python-pycparser.noarch 0:2.14-1.el7
  python2-cryptography.x86_64 0:1.7.2-2.el7
  python2-jmespath.noarch 0:0.9.0-3.el7
  python2-pyasn1.noarch 0:0.1.9-7.el7
  sshpass.x86_64 0:1.06-2.el7

Complete!
```

2.バージョン確認

```
# ansible --version
ansible 2.9.3
  config file = /etc/ansible/ansible.cfg
  configured module search path = [u'/root/.ansible/plugins/modules', u'/usr/share/ansible/plugins/modules']
  ansible python module location = /usr/lib/python2.7/site-packages/ansible
  executable location = /bin/ansible
  python version = 2.7.5 (default, Jul 13 2018, 13:06:57) [GCC 4.8.5 20150623 (Red Hat 4.8.5-28)]
```

3.ansibleコマンドでansible-hostへpingを実行

```
# ansible ansible-hostのグローバルIP -m ping
[WARNING]: provided hosts list is empty, only localhost is available. Note that
the implicit localhost does not match 'all'

[WARNING]: Could not match supplied host pattern, ignoring: 133.186.208.195
```

4.ansibleのhostsファイルにansible-hostのグローバルIPを登録

```
# vim /etc/ansible/hosts

-------------------------------------------------------------------------
ansible-hostのグローバルIPアドレスを最終行に追記
---------------------[Esc + :wq]で保存終了します。-------------------------
```

5.ansibleコマンドでansible-hostへpingを実行

{{< accordion >}}
<div>
<pre>
# ansible ansible-hostのグローバルIP -m ping
The authenticity of host '133.186.208.195 (133.186.208.195)' can't be established.
ECDSA key fingerprint is SHA256:Tgv/XzC7dZ9c2cpdGPBlVNiXkyZHbRsz0PAJtrRZ/9M.
ECDSA key fingerprint is MD5:af:fd:3a:14:a9:42:2c:6c:f9:f2:e1:73:17:4d:a3:b8.
Are you sure you want to continue connecting (yes/no)? yes <font color="Red">//←「yes」と入力</font>
133.186.208.195 | UNREACHABLE! => {
    "changed": false,
    "msg": "Failed to connect to the host via ssh: Warning: Permanently added '133.186.208.195' (ECDSA) to the list of known hosts.\r\nPlease login as the user \"centos\" rather than the user \"root\".\nPermission denied (publickey,gssapi-keyex,gssapi-with-mic,password).",
    "unreachable": true
}
</pre>
</div>
{{< /accordion >}}

6.「/root/hostlist」ファイルを作成し、ansible-hostのグローバルIPを登録

```
# vim /root/hostlist

-------------------------------------------------------------------------
ansible-hostのグローバルIPアドレスを記述
---------------------[Esc + :wq]で保存終了します。-------------------------
```

7.ansibleコマンドでansible-hostへpingを実行

```
# ansible ansible-hostのグローバルIP -m ping -k
SSH password:tokyoec //←「tokyoec」と入力
133.186.208.195 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python"
    },
    "changed": false,
    "ping": "pong"
}
```

8.鍵の作成

{{< accordion >}}
<div>
<pre>
# ssh-keygen
Generating public/private rsa key pair.
Enter file in which to save the key (/root/.ssh/id_rsa): <font color="Red">//← Enterキー</font>
Enter passphrase (empty for no passphrase): <font color="Red">//← Enterキー</font>
Enter same passphrase again: <font color="Red">//← Enterキー</font>
Your identification has been saved in /root/.ssh/id_rsa.
Your public key has been saved in /root/.ssh/id_rsa.pub.
The key fingerprint is:
SHA256:cLaYnQZSwwRp9cV3uN4tuhuRbSToxYVOGcXW5/RWnas root@ansible-server.novalocal
The key's randomart image is:
+---[RSA 2048]----+
|    .*=  .. .Bo.o|
|    o..o ..o*.+.*|
|   .. o + .+++.o=|
|     . O + .o= .+|
|      o S ..o.+o |
|       .    .Eo .|
|            .. . |
|            ..   |
|            oo   |
+----[SHA256]-----+
</pre>
</div>
{{< /accordion >}}

9.ansible-hostに鍵をコピー

{{< accordion >}}
<div>
<pre>
# ssh-copy-id 133.186.208.195
/bin/ssh-copy-id: INFO: Source of key(s) to be installed: "/root/.ssh/id_rsa.pub"
/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
Please login as the user "centos" rather than the user "root".
root@133.186.208.195's password:tokyoec <font color="Red">//←「tokyoec」と入力</font>

Number of key(s) added: 1

Now try logging into the machine, with:   "ssh '133.186.208.195'"
and check to make sure that only the key(s) you wanted were added.
</pre>
</div>
{{< /accordion >}}

10.ansibleコマンドでansible-hostへpingを実行

```
# ansible ansible-hostのグローバルIP -m ping
133.186.208.195 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python"
    },
    "changed": false,
    "ping": "pong"
}
```