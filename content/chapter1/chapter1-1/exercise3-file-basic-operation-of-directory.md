---
title: "Exercise3 File & Basic operation of directory"
date: 2017-10-17T15:26:15Z
draft: false
weight: 10
---

## 1.ディレクトリの作成と削除

次の図を参照しながら、同じディレクトリ構成を作成してみましょう。

![sample directory](/images/exercise3-file-basic-operation-of-directory.png)

1.ホームディレクトリ（/home/student）に移動して、カレントディレクトリを確認してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ cd
$ pwd
/home/student
</pre>
</div>
</details>
{{< /accordion >}}

2.trainingディレクトリを作成して、できていることを確認してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ mkdir training
$ ls
training      テンプレート  ドキュメント  音楽  公開
ダウンロード  デスクトップ  ビデオ        画像
</pre>
</div>
</details>
{{< /accordion >}}

3.カレントディレクトリをtrainingディレクトリに変更して、linuxディレクトリを作成してできていることを確認してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ cd training
$ mkdir linux
$ ls
linux
</pre>
</div>
</details>
{{< /accordion >}}

4.unixディレクトリとwindowsディレクトリを作成して、できていることを確認してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ mkdir unix windows
$ ls
linux  unix  windows
</pre>
</div>
</details>
{{< /accordion >}}

5.ホームディレクトリ（/home/student）に移動して、trainingディレクトリを削除して、削除できたことを確認してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ cd
$ rm -r training
$ ls
ダウンロード  デスクトップ  ビデオ  画像
テンプレート  ドキュメント  音楽    公開
</pre>
</div>
</details>
{{< /accordion >}}

6.1回のコマンド実行で画像のディレクトリ構造を作成してください。lsコマンドで「-R」オプションを利用してディレクトリ構造を確認してみましょう。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ mkdir -p training/linux training/unix training/windows
$ ls training/
linux  unix  windows
</pre>
</div>
</details>
{{< /accordion >}}

***

## 2.ファイルのコピー

1.「su -」コマンドを実行して、rootユーザのパスワードを入力してrootユーザに変更してください。

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

2.studentユーザのホームディレクトリ（/home/student）に移動して、「/etc/hosts」ファイルを「/etc/hosts.bak」というファイル名にしてコピーしてください。コピーファイルができたことを確認してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
# cd /home/student
# cp -p /etc/hosts /etc/hosts.bak
# ls /etc
DIR_COLORS               cron.deny                   gconf          libblockdev               nsswitch.conf      rc3.d              sudo-ldap.conf
DIR_COLORS.256color      cron.hourly                 gcrypt         libibverbs.d              nsswitch.conf.bak  rc4.d              sudo.conf
DIR_COLORS.lightbgcolor  cron.monthly                gdm            libnl                     oddjob             rc5.d              sudoers
GREP_COLORS              cron.weekly                 geoclue        libpaper.d                oddjobd.conf       rc6.d              sudoers.d
NetworkManager           crontab                     glvnd          libreport                 oddjobd.conf.d     rdma               sysconfig
PackageKit               crypto-policies             gnupg          libssh                    openldap           redhat-release     sysctl.conf
UPower                   crypttab                    groff          libuser.conf              opt                request-key.conf   sysctl.d
X11                      csh.cshrc                   group          libvirt                   os-release         request-key.d      system-release
adjtime                  csh.login                   group-         locale.conf               ostree             resolv.conf        system-release-cpe
aliases                  cups                        grub.d         localtime                 pam.d              rhsm               systemd
alsa                     cupshelpers                 grub2.cfg      login.defs                papersize          rpc                tcsd.conf
alternatives             dbus-1                      gshadow        logrotate.conf            passwd             rpm                terminfo
anacrontab               dconf                       gshadow-       logrotate.d               passwd-            rsyslog.conf       tmpfiles.d
asound.conf              default                     gss            lsm                       pbm2ppa.conf       rsyslog.d          trusted-key.key
at.deny                  depmod.d                    gssproxy       lvm                       pinforc            rwtab.d            tuned
audit                    dhcp                        host.conf      machine-id                pipewire           samba              udev
authselect               dleyna-server-service.conf  hostname       magic                     pkcs11             sane.d             udisks2
avahi                    dnf                         hosts          mailcap                   pki                sasl2              unbound
bash_completion.d        dnsmasq.conf                hosts.bak      makedumpfile.conf.sample  plymouth           security           updatedb.conf
bashrc                   dnsmasq.d                   hp             man_db.conf               pm                 selinux            usb_modeswitch.conf
bindresvport.blacklist   dracut.conf                 idmapd.conf    mcelog                    pnm2ppa.conf       services           vconsole.conf
binfmt.d                 dracut.conf.d               init.d         microcode_ctl             polkit-1           sestatus.conf      vimrc
bluetooth                egl                         inittab        mime.types                popt.d             setroubleshoot     virc
brlapi.key               enscript.cfg                inputrc        mke2fs.conf               prelink.conf.d     sgml               vmware-tools
brltty                   environment                 iproute2       modprobe.d                printcap           shadow             wgetrc
brltty.conf              ethertypes                  iscsi          modules-load.d            profile            shadow-            wpa_supplicant
centos-release           exports                     issue          motd                      profile.d          shells             xattr.conf
centos-release-upstream  exports.d                   issue.d        motd.d                    protocols          skel               xdg
chkconfig.d              favicon.png                 issue.net      mtab                      pulse              smartmontools      xinetd.d
chromium                 filesystems                 kdump.conf     mtools.conf               qemu-ga            sos.conf           xml
chrony.conf              firefox                     kernel         multipath                 qemu-kvm           speech-dispatcher  yum
chrony.keys              firewalld                   krb5.conf      nanorc                    radvd.conf         ssh                yum.conf
cifs-utils               flatpak                     krb5.conf.d    ndctl                     ras                ssl                yum.repos.d
cni                      fonts                       ksmtuned.conf  netconfig                 rc.d               sssd
cockpit                  fprintd.conf                ld.so.cache    networks                  rc.local           subgid
containers               fstab                       ld.so.conf     nfs.conf                  rc0.d              subgid-
cron.d                   fuse.conf                   ld.so.conf.d   nfsmount.conf             rc1.d              subuid
cron.daily               fwupd                       libaudit.conf  nftables                  rc2.d              subuid-
</pre>
</div>
</details>
{{< /accordion >}}

3.「exit」コマンドを実行して、studentユーザに変更してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
# exit
$
</pre>
</div>
</details>
{{< /accordion >}}

＜参考＞
ファイルのコピーは、別の言い方をすると、ファイルのバックアップになります。設定ファイル等を更新する際は、必ず、元ファイルを別ファイル名でコピーして、バックアップファイルを作成した上で、元ファイルの更新を行います。もし設定ファイルの更新ミスがあり、システムが動かくなくなったりした場合に、更新前のファイルにすぐ戻せるようにして、迅速なトラブル回避を行えるよう備えておきます。

***

## 3.ファイルの移動

1.「su -」コマンドを実行して、rootユーザのパスワードを入力してrootユーザに変更してください。

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

2.studentユーザのホームディレクトリ（/home/student）に移動して、training/linuxの下にbackupディレクトリを作成して、できたことを確認してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
# cd /home/student
# mkdir training/linux/backup
# ls -R
.:
training  ダウンロード  テンプレート  デスクトップ  ドキュメント  ビデオ  音楽  画像  公開

./training:
linux  unix  windows

./training/linux:
backup

./training/linux/backup:

./training/unix:

./training/windows:

./ダウンロード:

./テンプレート:

./デスクトップ:

./ドキュメント:

./ビデオ:

./音楽:

./画像:

./公開:
</pre>
</div>
</details>
{{< /accordion >}}

3.「/etc/hosts.bak」ファイルをホームディレクトリにあるtraining/linux/backupに移動してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
# mv /etc/hosts.bak training/linux/backup
# ls training/linux/backup/
hosts.bak
</pre>
</div>
</details>
{{< /accordion >}}

4.rmコマンドの「-rf」オプションを利用して、「training」ディレクトリを削除します。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
# rm -rf training
# ls
ダウンロード  デスクトップ  ビデオ  画像
テンプレート  ドキュメント  音楽    公開
</pre>
</div>
</details>
{{< /accordion >}}

5.「exit」コマンドを実行して、studentユーザに変更してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
# exit
$
</pre>
</div>
</details>
{{< /accordion >}}

***

## 4.長文テキストの表示および閲覧

1.「su -」コマンドを実行して、rootユーザのパスワードを入力してrootユーザに変更してください。

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

2.studentユーザのホームディレクトリ（/home/student）に移動して、「/etc/bashrc」ファイルをlessコマンドを実行して先頭から末尾まで見てみましょう。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
# cd /home/student
# less /etc/bashrc
//spaceキーで末尾までスクロール、(END)と表示されたらqキーを押して終了する。
# /etc/bashrc

# System wide functions and aliases
# Environment stuff goes in /etc/profile

# It's NOT a good idea to change this file unless you know what you
# are doing. It's much better to create a custom.sh shell script in
# /etc/profile.d/ to make custom changes to your environment, as this
# will prevent the need for merging in future updates.

# Prevent doublesourcing
if [ -z "$BASHRCSOURCED" ]; then
  BASHRCSOURCED="Y"

  # are we an interactive shell?
  if [ "$PS1" ]; then
    if [ -z "$PROMPT_COMMAND" ]; then
      case $TERM in
      xterm*|vte*)
        if [ -e /etc/sysconfig/bash-prompt-xterm ]; then
            PROMPT_COMMAND=/etc/sysconfig/bash-prompt-xterm
        elif [ "${VTE_VERSION:-0}" -ge 3405 ]; then
            PROMPT_COMMAND="__vte_prompt_command"
        else
            PROMPT_COMMAND='printf "\033]0;%s@%s:%s\007" "${USER}" "${HOSTNAME%%.*}" "${PWD/#$HOME/\~}"'
        fi
        ;;
      screen*)
        if [ -e /etc/sysconfig/bash-prompt-screen ]; then
            PROMPT_COMMAND=/etc/sysconfig/bash-prompt-screen
        else
            PROMPT_COMMAND='printf "\033k%s@%s:%s\033\\" "${USER}" "${HOSTNAME%%.*}" "${PWD/#$HOME/\~}"'
        fi
        ;;
# /etc/bashrc

# System wide functions and aliases
# Environment stuff goes in /etc/profile

# It's NOT a good idea to change this file unless you know what you
# are doing. It's much better to create a custom.sh shell script in
# /etc/profile.d/ to make custom changes to your environment, as this
# will prevent the need for merging in future updates.

# Prevent doublesourcing
if [ -z "$BASHRCSOURCED" ]; then
  BASHRCSOURCED="Y"

  # are we an interactive shell?
  if [ "$PS1" ]; then
    if [ -z "$PROMPT_COMMAND" ]; then
      case $TERM in
      xterm*|vte*)
        if [ -e /etc/sysconfig/bash-prompt-xterm ]; then
            PROMPT_COMMAND=/etc/sysconfig/bash-prompt-xterm
        elif [ "${VTE_VERSION:-0}" -ge 3405 ]; then
            PROMPT_COMMAND="__vte_prompt_command"
        else
            PROMPT_COMMAND='printf "\033]0;%s@%s:%s\007" "${USER}" "${HOSTNAME%%.*}" "${PWD/#$HOME/\~}"'
        fi
        ;;
      screen*)
        if [ -e /etc/sysconfig/bash-prompt-screen ]; then
            PROMPT_COMMAND=/etc/sysconfig/bash-prompt-screen
        else
            PROMPT_COMMAND='printf "\033k%s@%s:%s\033\\" "${USER}" "${HOSTNAME%%.*}" "${PWD/#$HOME/\~}"'
        fi
        ;;
      *)
        [ -e /etc/sysconfig/bash-prompt-default ] && PROMPT_COMMAND=/etc/sysconfig/bash-prompt-default
        ;;
      esac
    fi
    # Turn on parallel history
    shopt -s histappend
    history -a
    # Turn on checkwinsize
    shopt -s checkwinsize
    [ "$PS1" = "\\s-\\v\\\$ " ] && PS1="[\u@\h \W]\\$ "
    # You might want to have e.g. tty in prompt (e.g. more virtual machines)
    # and console windows
    # If you want to do so, just add e.g.
    # if [ "$PS1" ]; then
    #   PS1="[\u@\h:\l \W]\\$ "
    # fi
    # to your custom modification shell script in /etc/profile.d/ directory
  fi

  if ! shopt -q login_shell ; then # We're not a login shell
    # Need to redefine pathmunge, it gets undefined at the end of /etc/profile
    pathmunge () {
        case ":${PATH}:" in
            *:"$1":*)
                ;;
            *)
                if [ "$2" = "after" ] ; then
                    PATH=$PATH:$1
                else
                    PATH=$1:$PATH
                fi
        esac
    }

    # By default, we want umask to get set. This sets it for non-login shell.
    # Current threshold for system reserved uid/gids is 200
    # You could check uidgid reservation validity in
    # /usr/share/doc/setup-*/uidgid file
    if [ $UID -gt 199 ] && [ "`id -gn`" = "`id -un`" ]; then
       umask 002
    else
       umask 022
    fi

    SHELL=/bin/bash
    # Only display echos from profile.d scripts if we are no login shell
    # and interactive - otherwise just process them to set envvars
    for i in /etc/profile.d/*.sh; do
        if [ -r "$i" ]; then
            if [ "$PS1" ]; then
                . "$i"
            else
                . "$i" >/dev/null
            fi
        fi
    done

    unset i
    unset -f pathmunge
  fi

fi
# vim:ts=4:sw=4
(END)
q
</pre>
</div>
</details>
{{< /accordion >}}

3.ホームディレクトリ（/home/student）に移動して、「/etc/bashrc」ファイルをlessコマンドを実行して先「else」という文字列を検索してみましょう。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
# less /etc/bashrc
//(スラッシュ)elseと入力してnキーを「Pattern not found (press RETURN)」と表示されるまで押し、表示されたらqキーを押して終了する。
</pre>
</div>
</details>
{{< /accordion >}}

4.「exit」コマンドを実行して、studentユーザに変更してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
# exit
$
</pre>
</div>
</details>
{{< /accordion >}}

***

## 5.シンボリックリンク

1.「su -」コマンドを実行して、rootユーザのパスワードを入力してrootユーザに変更してください。

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

2.studentユーザのホームディレクトリ（/home/student）に移動して、「/sys/dev/block」のシンボリックリンクとして「block」ファイル作成して、シンボリックリンクが貼られていること確認してください。

※ls -laコマンド結果でblockの箇所がblock -> /sys/dev/blockとなっていることを確認しましょう。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
# cd /home/student
# ln -s /sys/dev/block block
# ls -la
合計 40
drwx------. 15 student student  4096  1月 29 01:34 .
drwxr-xr-x.  3 root    root       21  1月 21 00:23 ..
-rw-------.  1 student student   620  1月 21 00:26 .ICEauthority
-rw-------.  1 student student  3610  1月 28 04:47 .bash_history
-rw-r--r--.  1 student student    18 11月  8 11:21 .bash_logout
-rw-r--r--.  1 student student   141 11月  8 11:21 .bash_profile
-rw-r--r--.  1 student student   337  1月 28 01:55 .bashrc
drwx------. 10 student student   232  1月 21 00:24 .cache
drwx------. 11 student student   215  1月 21 00:24 .config
-rw-------.  1 student student    16  1月 21 00:23 .esd_auth
drwx------.  3 student student    19  1月 21 00:23 .local
drwxr-xr-x.  4 student student    39  1月 21 00:11 .mozilla
drwxrw----.  3 student student    19  1月 21 00:23 .pki
-rw-------.  1 student student 10007  1月 28 01:55 .viminfo
lrwxrwxrwx.  1 root    root       14  1月 29 01:34 block -> /sys/dev/block
drwxr-xr-x.  2 student student     6  1月 21 00:23 ダウンロード
drwxr-xr-x.  2 student student     6  1月 21 00:23 テンプレート
drwxr-xr-x.  2 student student     6  1月 21 00:23 デスクトップ
drwxr-xr-x.  2 student student     6  1月 21 00:23 ドキュメント
drwxr-xr-x.  2 student student     6  1月 21 00:23 ビデオ
drwxr-xr-x.  2 student student     6  1月 21 00:23 音楽
drwxr-xr-x.  2 student student     6  1月 21 00:23 画像
drwxr-xr-x.  2 student student     6  1月 21 00:23 公開
</pre>
</div>
</details>
{{< /accordion >}}

3.「cd /sys/dev/block」と入力せず、作成したシンボリックリンクを利用して、「/sys/dev/block」ディレクトリまで移動してみましょう。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
# cd block
# ls
11:0  253:0  253:1  8:0  8:1  8:2
</pre>

<pre>
$ cd /sys/dev/block
# ls
11:0  253:0  253:1  8:0  8:1  8:2
</pre>
</div>
</details>
{{< /accordion >}}

4.「/home/student」ディレクトリに戻って、blockファイルを削除してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
# cd /home/student
# rm block
rm: シンボリックリンク 'block' を削除しますか? y //yと入力
# ls
ダウンロード  デスクトップ  ビデオ  画像
テンプレート  ドキュメント  音楽    公開
</pre>
</div>
</details>
{{< /accordion >}}

5.「exit」コマンドを実行して、studentユーザに変更してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
# exit
$
</pre>
</div>
</details>
{{< /accordion >}}