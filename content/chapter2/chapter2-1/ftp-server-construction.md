---
title: "9.FTP Server Construction"
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

## 1.vsftpdのインストール

CentOS8_WORDPRESSの仮想マシンで実行すること

1.FTP専用ユーザの作成

{{< accordion >}}
<div>
<pre>
# useradd ftpuser
nginx version: nginx/1.14.1
</pre>

<pre>
# passwd ftpuser
ユーザー ftpuser のパスワードを変更。
新しいパスワード:tokyoecftp
新しいパスワードを再入力してください:tokyoecftp
passwd: すべての認証トークンが正しく更新できました。
</pre>
</div>
{{< /accordion >}}

2.新ドキュメントルートの作成

{{< accordion >}}
<div>
<pre>
# mkdir -p /home/ftpuser/htdocs/public_html
</pre>

<pre>
# chown -R ftpuser.ftpuser /home/ftpuser/htdocs
</pre>

<pre>
# chmod 755 -R /home/ftpuser
</pre>
</div>
{{< /accordion >}}

3.vsftpdをインストール

{{< accordion >}}
<div>
<pre>
# dnf -y install vsftpd
CentOS-8 - AppStream                            8.8 kB/s | 4.3 kB     00:00
CentOS-8 - Base                                 8.6 kB/s | 3.8 kB     00:00
CentOS-8 - Extras                               2.6 kB/s | 1.5 kB     00:00
依存関係が解決しました。
================================================================================
 パッケージ      Arch            バージョン            リポジトリー       サイズ
================================================================================
インストール:
 vsftpd          x86_64          3.0.3-28.el8          AppStream          180 k

トランザクションの概要
================================================================================
インストール  1 パッケージ

ダウンロードサイズの合計: 180 k
インストール済みのサイズ: 359 k
パッケージのダウンロード:
vsftpd-3.0.3-28.el8.x86_64.rpm                  1.8 MB/s | 180 kB     00:00
--------------------------------------------------------------------------------
合計                                            409 kB/s | 180 kB     00:00
トランザクションの確認を実行中
トランザクションの確認に成功しました。
トランザクションのテストを実行中
トランザクションのテストに成功しました。
トランザクションを実行中
  準備             :                                                        1/1
  インストール中   : vsftpd-3.0.3-28.el8.x86_64                             1/1
  scriptletの実行中: vsftpd-3.0.3-28.el8.x86_64                             1/1
  検証             : vsftpd-3.0.3-28.el8.x86_64                             1/1

インストール済み:
  vsftpd-3.0.3-28.el8.x86_64

完了しました!
</pre>
</div>
{{< /accordion >}}

4.vsftpd設定ファイルの変更

{{< accordion >}}
<div>
<pre>
# cd /etc/vsftpd
</pre>

<pre>
# cp -p vsftpd.conf vsftpd.org
</pre>

<pre>
# vim vsftpd.conf
# Example config file /etc/vsftpd/vsftpd.conf
#
# The default compiled in settings are fairly paranoid. This sample file
# loosens things up a bit, to make the ftp daemon more usable.
# Please see vsftpd.conf.5 for all compiled in defaults.
#
# READ THIS: This example file is NOT an exhaustive list of vsftpd options.
# Please read the vsftpd.conf.5 manual page to get a full idea of vsftpd's
# capabilities.
#
# Allow anonymous FTP? (Beware - allowed by default if you comment this out).
anonymous_enable=NO
#
# Uncomment this to allow local users to log in.
# When SELinux is enforcing check for SE bool ftp_home_dir
local_enable=YES
#
# Uncomment this to enable any form of FTP write command.
write_enable=YES
#
# Default umask for local users is 077. You may wish to change this to 022,
# if your users expect that (022 is used by most other ftpd's)
local_umask=022
#
# Uncomment this to allow the anonymous FTP user to upload files. This only
# has an effect if the above global write enable is activated. Also, you will
# obviously need to create a directory writable by the FTP user.
# When SELinux is enforcing check for SE bool allow_ftpd_anon_write, allow_ftpd_full_access
#anon_upload_enable=YES
#
# Uncomment this if you want the anonymous FTP user to be able to create
# new directories.
#anon_mkdir_write_enable=YES
#
# Activate directory messages - messages given to remote users when they
# go into a certain directory.
dirmessage_enable=YES
#
# Activate logging of uploads/downloads.
xferlog_enable=YES
#
# Make sure PORT transfer connections originate from port 20 (ftp-data).
connect_from_port_20=YES
#
# If you want, you can arrange for uploaded anonymous files to be owned by
# a different user. Note! Using "root" for uploaded files is not
# recommended!
#chown_uploads=YES
#chown_username=whoever
#
# You may override where the log file goes if you like. The default is shown
# below.
#xferlog_file=/var/log/xferlog
#
# If you want, you can have your log file in standard ftpd xferlog format.
# Note that the default log file location is /var/log/xferlog in this case.
xferlog_std_format=YES
#
# You may change the default value for timing out an idle session.
#idle_session_timeout=600
#
# You may change the default value for timing out a data connection.
#data_connection_timeout=120
#
# It is recommended that you define on your system a unique user which the
# ftp server can use as a totally isolated and unprivileged user.
#nopriv_user=ftpsecure
#
# Enable this and the server will recognise asynchronous ABOR requests. Not
# recommended for security (the code is non-trivial). Not enabling it,
# however, may confuse older FTP clients.
#async_abor_enable=YES
#
# By default the server will pretend to allow ASCII mode but in fact ignore
# the request. Turn on the below options to have the server actually do ASCII
# mangling on files when in ASCII mode. The vsftpd.conf(5) man page explains
# the behaviour when these options are disabled.
# Beware that on some FTP servers, ASCII support allows a denial of service
# attack (DoS) via the command "SIZE /big/file" in ASCII mode. vsftpd
# predicted this attack and has always been safe, reporting the size of the
# raw file.
# ASCII mangling is a horrible feature of the protocol.
ascii_upload_enable=YES  <font color="Red">//←「#ascii_upload_enable=YES 変更⇒ ascii_upload_enable=YES」</font>
ascii_download_enable=YES <font color="Red">//←「#ascii_download_enable=YES 変更⇒ ascii_download_enable=YES」</font>
#
# You may fully customise the login banner string:
#ftpd_banner=Welcome to blah FTP service.
#
# You may specify a file of disallowed anonymous e-mail addresses. Apparently
# useful for combatting certain DoS attacks.
#deny_email_enable=YES
# (default follows)
#banned_email_file=/etc/vsftpd/banned_emails
#
# You may specify an explicit list of local users to chroot() to their home
# directory. If chroot_local_user is YES, then this list becomes a list of
# users to NOT chroot().
# (Warning! chroot'ing can be very dangerous. If using chroot, make sure that
# the user does not have write access to the top level directory within the
# chroot)
#chroot_local_user=YES <font color="Red">//←「#chroot_local_user=YES 変更⇒ chroot_local_user=YES」</font>
#chroot_list_enable=YES <font color="Red">//←「#chroot_list_enable=YES 変更⇒ chroot_list_enable=YES」</font>
# (default follows)
#chroot_list_file=/etc/vsftpd/chroot_list <font color="Red">//←「#chroot_list_file=/etc/vsftpd/chroot_list 変更⇒ chroot_list_file=/etc/vsftpd/chroot_list」</font>
#
# You may activate the "-R" option to the builtin ls. This is disabled by
# default to avoid remote users being able to cause excessive I/O on large
# sites. However, some broken FTP clients such as "ncftp" and "mirror" assume
# the presence of the "-R" option, so there is a strong case for enabling it.
ls_recurse_enable=YES <font color="Red">//←「#ls_recurse_enable=YES 変更⇒ ls_recurse_enable=YES」</font>
#
# When "listen" directive is enabled, vsftpd runs in standalone mode and
# listens on IPv4 sockets. This directive cannot be used in conjunction
# with the listen_ipv6 directive.
listen=NO
#
# This directive enables listening on IPv6 sockets. By default, listening
# on the IPv6 "any" address (::) will accept connections from both IPv6
# and IPv4 clients. It is not necessary to listen on *both* IPv4 and IPv6
# sockets. If you want that (perhaps because you want to listen on specific
# addresses) then you must run two copies of vsftpd with two configuration
# files.
# Make sure, that one of the listen options is commented !!
listen_ipv6=YES

pam_service_name=vsftpd
userlist_enable=YES
<font color="Red">//↓追記</font>
userlist_deny=NO
userlist_file=/etc/vsftpd/ftpuser_list
user_config_dir=/etc/vsftpd/vsftpd_user_conf
allow_writeable_chroot=YES
</pre>
</div>
{{< /accordion >}}

5.chroot_listファイルの作成

{{< accordion >}}
<div>
<pre>
# touch chroot_list
</pre>
</div>
{{< /accordion >}}

6.ftpuser_listファイルの作成

{{< accordion >}}
<div>
<pre>
# vim ftpuser_list

-----------------以下をコピー&ペースト-----------------
ftpuser
-----------------[Esc + :wq]で保存終了します。---------
</pre>
</div>
{{< /accordion >}}

7.初期ディレクトリの設定

{{< accordion >}}
<div>
<pre>
# mkdir vsftpd_user_conf
</pre>

<pre>
# vim vsftpd_user_conf/ftpuser

-----------------以下をコピー&ペースト-----------------
local_root=/home/ftpuser/htdocs
-----------------[Esc + :wq]で保存終了します。---------
</pre>
</div>
{{< /accordion >}}

8.SELinuxの設定

{{< accordion >}}
<div>
<pre>
# setsebool -P allow_ftpd_full_access on
</pre>
</div>
{{< /accordion >}}

9.vsftpdサービスの自動起動設定

{{< accordion >}}
<div>
<pre>
# systemctl enable vsftpd
Created symlink /etc/systemd/system/multi-user.target.wants/vsftpd.service → /usr/lib/systemd/system/vsftpd.service.
</pre>

<pre>
# systemctl list-unit-files --type=service | grep vsftpd
vsftpd.service                             enabled
vsftpd@.service                            indirect
</pre>
</div>
{{< /accordion >}}

10.vsftpdの起動

{{< accordion >}}
<div>
<pre>
# systemctl start vsftpd
</pre>

<pre>
# systemctl status vsftpd
● vsftpd.service - Vsftpd ftp daemon
   Loaded: loaded (/usr/lib/systemd/system/vsftpd.service; enabled; vendor preset: disabled)
   Active: active (running) since Fri 2020-02-07 00:24:43 EST; 32s ago
  Process: 15123 ExecStart=/usr/sbin/vsftpd /etc/vsftpd/vsftpd.conf (code=exited, status=0/SUCCESS)
 Main PID: 15124 (vsftpd)
    Tasks: 1 (limit: 23983)
   Memory: 536.0K
   CGroup: /system.slice/vsftpd.service
           mq15124 /usr/sbin/vsftpd /etc/vsftpd/vsftpd.conf

 2月 07 00:24:43 localhost.localdomain systemd[1]: Starting Vsftpd ftp daemon...
 2月 07 00:24:43 localhost.localdomain systemd[1]: Started Vsftpd ftp daemon.
</pre>
</div>
{{< /accordion >}}

11.外部からアクセスできるようにfirewalldでftpを解放

{{< accordion >}}
<div>
<pre>
# firewall-cmd --add-service=ftp --zone=public --permanent
success
</pre>
</div>
{{< /accordion >}}

12.設定を反映

{{< accordion >}}
<div>
<pre>
# firewall-cmd --reload
success
</pre>
</div>
{{< /accordion >}}

13.httpdの設定

{{< accordion >}}
<div>
<pre>
# vim /etc/httpd/conf/httpd.conf

-----------------------以下赤字の内容に変更します。-------------------------------------
・
・省略
・
#
# DocumentRoot: The directory out of which you will serve your
# documents. By default, all requests are taken from this directory, but
# symbolic links and aliases may be used to point to other locations.
#
DocumentRoot "/home/ftpuser/htdocs/public_html" <font color="Red">//←「DocumentRoot "/var/www/html" 変更⇒ DocumentRoot "/home/ftpuser/htdocs/public_html"」</font>

#
# Relax access to content within /var/www.
#
&lt;Directory "/var/www"&gt;
    AllowOverride None
    # Allow open access:
    Require all granted
    &lt;/Directory&gt;

# Further relax access to the default document root:
&lt;Directory "/home/ftpuser/htdocs/public_html"&gt; <font color="Red">//←「&lt;Directory "/var/www/html"&gt; 変更⇒ &lt;Directory "/home/ftpuser/htdocs/public_html"&gt;」</font>
    #
    # Possible values for the Options directive are "None", "All",
    # or any combination of:
    #   Indexes Includes FollowSymLinks SymLinksifOwnerMatch ExecCGI MultiViews
    #
・
・省略
・
-----------------[Esc + :wq]で保存終了します。------------------------------------------
</pre>
</div>
{{< /accordion >}}

14.SELinuxの設定

{{< accordion >}}
<div>
<pre>
# semanage fcontext -a -t httpd_sys_content_t '/home/ftpuser/htdocs/public_html(/.*)?'
</pre>

<pre>
# restorecon -Rv /home/ftpuser/htdocs/public_html
Relabeled /home/ftpuser/htdocs/public_html from unconfined_u:object_r:user_home_t:s0 to unconfined_u:object_r:httpd_sys_content_t:s0
</pre>
</div>
{{< /accordion >}}

15.httpdの再起動

{{< accordion >}}
<div>
<pre>
# systemctl restart httpd
</pre>
</div>
{{< /accordion >}}