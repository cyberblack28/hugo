---
title: "1.Exercise1 systemd"
date: 2017-10-17T15:26:15Z
draft: false
weight: 10
---

## 1.サービスステータスの確認

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

2.chronydのサービスのステータスを確認してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
# systemctl status chronyd
  ● chronyd.service - NTP client/server
  Loaded: loaded (/usr/lib/systemd/system/chronyd.service; enabled; vendor pre>
  Active: active (running) since Mon 2020-02-03 20:17:49 EST; 5h 36min ago
    Docs: man:chronyd(8)
          man:chrony.conf(5)
Main PID: 1001 (chronyd)
   Tasks: 1 (limit: 23983)
  Memory: 1.6M
  CGroup: /system.slice/chronyd.service
          mq1001 /usr/sbin/chronyd

2月 04 00:36:05 tokyoec.com chronyd[1001]: Source 133.18.174.255 online
2月 04 00:36:29 tokyoec.com chronyd[1001]: Source 133.243.238.243 offline
2月 04 00:36:29 tokyoec.com chronyd[1001]: Source 129.250.35.251 offline
2月 04 00:36:29 tokyoec.com chronyd[1001]: Source 162.159.200.123 offline
2月 04 00:36:29 tokyoec.com chronyd[1001]: Source 133.18.174.255 offline
2月 04 00:46:05 tokyoec.com chronyd[1001]: Source 133.243.238.243 online
2月 04 00:46:05 tokyoec.com chronyd[1001]: Source 129.250.35.251 online
2月 04 00:46:05 tokyoec.com chronyd[1001]: Source 162.159.200.123 online
2月 04 00:46:05 tokyoec.com chronyd[1001]: Source 133.18.174.255 online
2月 04 01:37:49 tokyo-ec.com chronyd[1001]: Selected source 133.243.238.243
<font color="Red">//[SPACE]キーでスクロール、[q]キーを入力して終了</font>
</pre>
</div>
</details>
{{< /accordion >}}

***

## 2.サービスの停止、開始、再起動

1.chronydのサービスを停止して、ステータス(inactive)を確認してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
# systemctl stop chronyd
# systemctl status chronyd
● chronyd.service - NTP client/server
   Loaded: loaded (/usr/lib/systemd/system/chronyd.service; enabled; vendor pre>
   Active: inactive (dead) since Tue 2020-02-04 01:56:50 EST; 7s ago
     Docs: man:chronyd(8)
           man:chrony.conf(5)
 Main PID: 1001 (code=exited, status=0/SUCCESS)

 2月 04 00:36:29 tokyoec.com chronyd[1001]: Source 129.250.35.251 offline
 2月 04 00:36:29 tokyoec.com chronyd[1001]: Source 162.159.200.123 offline
 2月 04 00:36:29 tokyoec.com chronyd[1001]: Source 133.18.174.255 offline
 2月 04 00:46:05 tokyoec.com chronyd[1001]: Source 133.243.238.243 online
 2月 04 00:46:05 tokyoec.com chronyd[1001]: Source 129.250.35.251 online
 2月 04 00:46:05 tokyoec.com chronyd[1001]: Source 162.159.200.123 online
 2月 04 00:46:05 tokyoec.com chronyd[1001]: Source 133.18.174.255 online
 2月 04 01:37:49 tokyo-ec.com chronyd[1001]: Selected source 133.243.238.243
 2月 04 01:56:50 tokyo-ec.com systemd[1]: Stopping NTP client/server...
 2月 04 01:56:50 tokyo-ec.com systemd[1]: Stopped NTP client/server.
<font color="Red">//[SPACE]キーでスクロール、[q]キーを入力して終了</font>
</pre>
</div>
</details>
{{< /accordion >}}

2.chronydのサービスを開始して、ステータス(active)を確認してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
# systemctl start chronyd
# systemctl status chronyd
● chronyd.service - NTP client/server
   Loaded: loaded (/usr/lib/systemd/system/chronyd.service; enabled; vendor pre>
   Active: active (running) since Tue 2020-02-04 02:00:09 EST; 3s ago
     Docs: man:chronyd(8)
           man:chrony.conf(5)
  Process: 6233 ExecStartPost=/usr/libexec/chrony-helper update-daemon (code=ex>
  Process: 6229 ExecStart=/usr/sbin/chronyd $OPTIONS (code=exited, status=0/SUC>
 Main PID: 6231 (chronyd)
    Tasks: 1 (limit: 23983)
   Memory: 844.0K
   CGroup: /system.slice/chronyd.service
           mq6231 /usr/sbin/chronyd

 2月 04 02:00:09 tokyo-ec.com systemd[1]: Starting NTP client/server...
 2月 04 02:00:09 tokyo-ec.com chronyd[6231]: chronyd version 3.5 starting (+CMD>
 2月 04 02:00:09 tokyo-ec.com chronyd[6231]: Frequency -9.200 +/- 0.715 ppm rea>
 2月 04 02:00:09 tokyo-ec.com chronyd[6231]: Using right/UTC timezone to obtain>
 2月 04 02:00:09 tokyo-ec.com systemd[1]: Started NTP client/server.
<font color="Red">//[SPACE]キーでスクロール、[q]キーを入力して終了</font>
</pre>
</div>
</details>
{{< /accordion >}}

3.chronydのサービスを再起動して、ステータス(active)を確認してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
# systemctl restart chronyd
# systemctl status chronyd
● chronyd.service - NTP client/server
   Loaded: loaded (/usr/lib/systemd/system/chronyd.service; enabled; vendor pre>
   Active: active (running) since Tue 2020-02-04 02:02:01 EST; 2s ago
     Docs: man:chronyd(8)
           man:chrony.conf(5)
  Process: 6277 ExecStartPost=/usr/libexec/chrony-helper update-daemon (code=ex>
  Process: 6273 ExecStart=/usr/sbin/chronyd $OPTIONS (code=exited, status=0/SUC>
 Main PID: 6275 (chronyd)
    Tasks: 1 (limit: 23983)
   Memory: 832.0K
   CGroup: /system.slice/chronyd.service
           mq6275 /usr/sbin/chronyd

 2月 04 02:02:01 tokyo-ec.com systemd[1]: Stopped NTP client/server.
 2月 04 02:02:01 tokyo-ec.com systemd[1]: Starting NTP client/server...
 2月 04 02:02:01 tokyo-ec.com chronyd[6275]: chronyd version 3.5 starting (+CMD>
 2月 04 02:02:01 tokyo-ec.com chronyd[6275]: Frequency -9.200 +/- 0.803 ppm rea>
 2月 04 02:02:01 tokyo-ec.com chronyd[6275]: Using right/UTC timezone to obtain>
 2月 04 02:02:01 tokyo-ec.com systemd[1]: Started NTP client/server.
<font color="Red">//[SPACE]キーでスクロール、[q]キーを入力して終了</font>
</pre>
</div>
</details>
{{< /accordion >}}

***

## 3.サービスの自動起動設定

1.chronydサービスが自動起動設定になっているか確認してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
# systemctl is-enabled chronyd
enabled
</pre>
</div>
</details>
{{< /accordion >}}

2.chronydサービスが自動起動設定を無効にして、確認してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
# systemctl disable chronyd
Removed /etc/systemd/system/multi-user.target.wants/chronyd.service.
</pre>

<pre>
# systemctl is-enabled chronyd
disabled
</pre>
</div>
</details>
{{< /accordion >}}

3.chronydサービスが自動起動設定を有効にして、確認してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
# systemctl enable chronyd
Created symlink /etc/systemd/system/multi-user.target.wants/chronyd.service → /usr/lib/systemd/system/chronyd.service.
</pre>

<pre>
# systemctl is-enabled chronyd
enabled
</pre>
</div>
</details>
{{< /accordion >}}

***

## 4.全サービスの確認

1.システム上のすべてのサービスユニットを一覧表示してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
# systemctl list-units --type=service
UNIT                            LOAD   ACTIVE SUB     DESCRIPTION
accounts-daemon.service         loaded active running Accounts Service
alsa-state.service              loaded active running Manage Sound Card State (>
atd.service                     loaded active running Job spooling tools
auditd.service                  loaded active running Security Auditing Service
avahi-daemon.service            loaded active running Avahi mDNS/DNS-SD Stack
chronyd.service                 loaded active running NTP client/server
colord.service                  loaded active running Manage, Install and Gener>
crond.service                   loaded active running Command Scheduler
cups.service                    loaded active running CUPS Scheduler
dbus.service                    loaded active running D-Bus System Message Bus
dracut-shutdown.service         loaded active exited  Restore /run/initramfs on>
firewalld.service               loaded active running firewalld - dynamic firew>
gdm.service                     loaded active running GNOME Display Manager
gssproxy.service                loaded active running GSSAPI Proxy Daemon
import-state.service            loaded active exited  Import network configurat>
iscsi-shutdown.service          loaded active exited  Logout off all iSCSI sess>
kdump.service                   loaded active exited  Crash recovery kernel arm>
kmod-static-nodes.service       loaded active exited  Create list of required s>
ksm.service                     loaded active exited  Kernel Samepage Merging
ksmtuned.service                loaded active running Kernel Samepage Merging (>
libstoragemgmt.service          loaded active running libstoragemgmt plug-in se>
libvirtd.service                loaded active running Virtualization daemon
lvm2-monitor.service            loaded active exited  Monitoring of LVM2 mirror>
lvm2-pvscan@8:2.service         loaded active exited  LVM event activation on d>
mcelog.service                  loaded active running Machine Check Exception L>
ModemManager.service            loaded active running Modem Manager
NetworkManager-wait-online.service loaded active exited  Network Manager Wait O>
NetworkManager.service          loaded active running Network Manager
nis-domainname.service          loaded active exited  Read and set NIS domainna>
polkit.service                  loaded active running Authorization Manager
rngd.service                    loaded active running Hardware RNG Entropy Gath>
rpc-statd-notify.service        loaded active exited  Notify NFS peers of a res>
rpcbind.service                 loaded active running RPC Bind
rsyslog.service                 loaded active running System Logging Service
rtkit-daemon.service            loaded active running RealtimeKit Scheduling Po>
smartd.service                  loaded active running Self Monitoring and Repor>
sshd.service                    loaded active running OpenSSH server daemon
sssd.service                    loaded active running System Security Services >
systemd-fsck@dev-disk-by\x2duuid-21594ec9\x2d7285\x2d4136\x2d9255\x2d2b7cee472e>
systemd-journal-flush.service   loaded active exited  Flush Journal to Persiste>
systemd-journald.service        loaded active running Journal Service
systemd-logind.service          loaded active running Login Service
systemd-machined.service        loaded active running Virtual Machine and Conta>
systemd-random-seed.service     loaded active exited  Load/Save Random Seed
systemd-remount-fs.service      loaded active exited  Remount Root and Kernel F>
systemd-resolved.service        loaded active running Network Name Resolution
systemd-sysctl.service          loaded active exited  Apply Kernel Variables
UNIT                            LOAD   ACTIVE SUB     DESCRIPTION
accounts-daemon.service         loaded active running Accounts Service
alsa-state.service              loaded active running Manage Sound Card State (>
atd.service                     loaded active running Job spooling tools
auditd.service                  loaded active running Security Auditing Service
avahi-daemon.service            loaded active running Avahi mDNS/DNS-SD Stack
chronyd.service                 loaded active running NTP client/server
colord.service                  loaded active running Manage, Install and Gener>
crond.service                   loaded active running Command Scheduler
cups.service                    loaded active running CUPS Scheduler
dbus.service                    loaded active running D-Bus System Message Bus
dracut-shutdown.service         loaded active exited  Restore /run/initramfs on>
firewalld.service               loaded active running firewalld - dynamic firew>
gdm.service                     loaded active running GNOME Display Manager
gssproxy.service                loaded active running GSSAPI Proxy Daemon
import-state.service            loaded active exited  Import network configurat>
iscsi-shutdown.service          loaded active exited  Logout off all iSCSI sess>
kdump.service                   loaded active exited  Crash recovery kernel arm>
kmod-static-nodes.service       loaded active exited  Create list of required s>
ksm.service                     loaded active exited  Kernel Samepage Merging
ksmtuned.service                loaded active running Kernel Samepage Merging (>
libstoragemgmt.service          loaded active running libstoragemgmt plug-in se>
libvirtd.service                loaded active running Virtualization daemon
lvm2-monitor.service            loaded active exited  Monitoring of LVM2 mirror>
lvm2-pvscan@8:2.service         loaded active exited  LVM event activation on d>
mcelog.service                  loaded active running Machine Check Exception L>
ModemManager.service            loaded active running Modem Manager
NetworkManager-wait-online.service loaded active exited  Network Manager Wait O>
NetworkManager.service          loaded active running Network Manager
nis-domainname.service          loaded active exited  Read and set NIS domainna>
polkit.service                  loaded active running Authorization Manager
rngd.service                    loaded active running Hardware RNG Entropy Gath>
rpc-statd-notify.service        loaded active exited  Notify NFS peers of a res>
rpcbind.service                 loaded active running RPC Bind
rsyslog.service                 loaded active running System Logging Service
rtkit-daemon.service            loaded active running RealtimeKit Scheduling Po>
smartd.service                  loaded active running Self Monitoring and Repor>
sshd.service                    loaded active running OpenSSH server daemon
sssd.service                    loaded active running System Security Services >
systemd-fsck@dev-disk-by\x2duuid-21594ec9\x2d7285\x2d4136\x2d9255\x2d2b7cee472e>
systemd-journal-flush.service   loaded active exited  Flush Journal to Persiste>
systemd-journald.service        loaded active running Journal Service
systemd-logind.service          loaded active running Login Service
systemd-machined.service        loaded active running Virtual Machine and Conta>
systemd-random-seed.service     loaded active exited  Load/Save Random Seed
systemd-remount-fs.service      loaded active exited  Remount Root and Kernel F>
systemd-resolved.service        loaded active running Network Name Resolution
systemd-sysctl.service          loaded active exited  Apply Kernel Variables
systemd-tmpfiles-setup-dev.service loaded active exited  Create Static Device N>
systemd-tmpfiles-setup.service  loaded active exited  Create Volatile Files and>
systemd-udev-settle.service     loaded active exited  udev Wait for Complete De>
systemd-udev-trigger.service    loaded active exited  udev Coldplug all Devices
systemd-udevd.service           loaded active running udev Kernel Device Manager
systemd-update-utmp.service     loaded active exited  Update UTMP about System >
systemd-user-sessions.service   loaded active exited  Permit User Sessions
tuned.service                   loaded active running Dynamic System Tuning Dae>
udisks2.service                 loaded active running Disk Manager
upower.service                  loaded active running Daemon for power manageme>
user-runtime-dir@1000.service   loaded active exited  /run/user/1000 mount wrap>
user-runtime-dir@42.service     loaded active exited  /run/user/42 mount wrapper
user@1000.service               loaded active running User Manager for UID 1000
user@42.service                 loaded active running User Manager for UID 42
vdo.service                     loaded active exited  VDO volume services
wpa_supplicant.service          loaded active running WPA supplicant

LOAD   = Reflects whether the unit definition was properly loaded.
ACTIVE = The high-level unit activation state, i.e. generalization of SUB.
SUB    = The low-level unit activation state, values depend on unit type.

63 loaded units listed. Pass --all to see loaded but inactive units, too.
To show all installed unit files use 'systemctl list-unit-files'.
<font color="Red">//[SPACE]キーでスクロール、[q]キーを入力して終了</font>
</pre>
</div>
</details>
{{< /accordion >}}

2.一覧表示からchronydのみ表示してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
# systemctl list-units --type=service | grep chronyd
chronyd.service                                                                           loaded active running NTP client/server
</pre>
</div>
</details>
{{< /accordion >}}

***

## 5.サービスユニットの有効化または無効化状態の確認

1.すべてのサービスユニットの有効化または無効化状態を一覧表示してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
# systemctl list-unit-files --type=service
UNIT FILE                                  STATE
accounts-daemon.service                    enabled
alsa-restore.service                       static
alsa-state.service                         static
anaconda-direct.service                    static
anaconda-nm-config.service                 static
anaconda-noshell.service                   static
anaconda-pre.service                       static
anaconda-shell@.service                    static
anaconda-sshd.service                      static
anaconda-tmux@.service                     static
anaconda.service                           static
arp-ethers.service                         disabled
atd.service                                enabled
auditd.service                             enabled
auth-rpcgss-module.service                 static
autovt@.service                            enabled
avahi-daemon.service                       enabled
blivet.service                             static
blk-availability.service                   disabled
bluetooth.service                          enabled
bolt.service                               static
brltty.service                             disabled
btattach-bcm@.service                      static
canberra-system-bootup.service             disabled
canberra-system-shutdown-reboot.service    disabled
canberra-system-shutdown.service           disabled
chrony-dnssrv@.service                     static
chrony-wait.service                        disabled
chronyd.service                            enabled
clean-mount-point@.service                 static
cockpit-motd.service                       static
cockpit.service                            static
colord.service                             static
configure-printer@.service                 static
console-getty.service                      disabled
container-getty@.service                   static
cpupower.service                           disabled
crond.service                              enabled
cups-browsed.service                       disabled
cups.service                               enabled
dbus-org.bluez.service                     enabled
dbus-org.fedoraproject.FirewallD1.service  enabled
dbus-org.freedesktop.Avahi.service         enabled
dbus-org.freedesktop.hostname1.service     static
dbus-org.freedesktop.import1.service       static
dbus-org.freedesktop.locale1.service       static
dbus-org.freedesktop.login1.service        static
dbus-org.freedesktop.machine1.service      static
dbus-org.freedesktop.ModemManager1.service enabled
dbus-org.freedesktop.nm-dispatcher.service enabled
dbus-org.freedesktop.portable1.service     static
dbus-org.freedesktop.resolve1.service      enabled
dbus-org.freedesktop.timedate1.service     enabled
dbus.service                               static
debug-shell.service                        disabled
display-manager.service                    enabled
dm-event.service                           static
dnf-makecache.service                      static
dnsmasq.service                            disabled
dracut-cmdline.service                     static
dracut-initqueue.service                   static
dracut-mount.service                       static
dracut-pre-mount.service                   static
dracut-pre-pivot.service                   static
dracut-pre-trigger.service                 static
dracut-pre-udev.service                    static
dracut-shutdown.service                    static
ebtables.service                           disabled
emergency.service                          static
firewalld.service                          enabled
flatpak-system-helper.service              static
fprintd.service                            static
fstrim.service                             static
fwupd-offline-update.service               static
fwupd.service                              static
gdm.service                                enabled
geoclue.service                            static
getty@.service                             enabled
grub-boot-indeterminate.service            static
gssproxy.service                           disabled
halt-local.service                         static
hypervfcopyd.service                       static
hypervkvpd.service                         static
hypervvssd.service                         static
iio-sensor-proxy.service                   static
import-state.service                       enabled
initial-setup-reconfiguration.service      disabled
initial-setup.service                      disabled
initrd-cleanup.service                     static
initrd-parse-etc.service                   static
initrd-switch-root.service                 static
initrd-udevadm-cleanup-db.service          static
instperf.service                           static
io.podman.service                          disabled
iprdump.service                            disabled
iprinit.service                            disabled
iprupdate.service                          disabled
irqbalance.service                         enabled
iscsi-shutdown.service                     static
iscsi.service                              enabled
iscsid.service                             disabled
iscsiuio.service                           disabled
kdump.service                              enabled
kmod-static-nodes.service                  static
kpatch.service                             disabled
ksm.service                                enabled
ksmtuned.service                           enabled
ldconfig.service                           static
libstoragemgmt.service                     enabled
libvirtd.service                           enabled
loadmodules.service                        enabled
lvm2-lvmpolld.service                      static
lvm2-monitor.service                       enabled
lvm2-pvscan@.service                       static
man-db-cache-update.service                static
mcelog.service                             enabled
mdadm-grow-continue@.service               static
mdadm-last-resort@.service                 static
mdcheck_continue.service                   static
mdcheck_start.service                      static
mdmon@.service                             static
mdmonitor-oneshot.service                  static
mdmonitor.service                          enabled
messagebus.service                         static
microcode.service                          enabled
mlocate-updatedb.service                   static
ModemManager.service                       enabled
multipathd.service                         enabled
ndctl-monitor.service                      disabled
netcf-transaction.service                  disabled
NetworkManager-dispatcher.service          enabled
NetworkManager-wait-online.service         enabled
NetworkManager.service                     enabled
nfs-blkmap.service                         disabled
nfs-convert.service                        enabled
nfs-idmapd.service                         static
nfs-mountd.service                         static
nfs-server.service                         disabled
nfs-utils.service                          static
nftables.service                           disabled
nis-domainname.service                     enabled
numad.service                              disabled
oddjobd.service                            disabled
ostree-finalize-staged.service             static
ostree-prepare-root.service                static
ostree-remount.service                     disabled
packagekit-offline-update.service          static
packagekit.service                         static
plymouth-halt.service                      static
plymouth-kexec.service                     static
plymouth-poweroff.service                  static
plymouth-quit-wait.service                 static
plymouth-quit.service                      static
plymouth-read-write.service                static
plymouth-reboot.service                    static
plymouth-start.service                     static
plymouth-switch-root.service               static
polkit.service                             static
psacct.service                             disabled
qemu-guest-agent.service                   disabled
qemu-pr-helper.service                     static
quotaon.service                            static
radvd.service                              disabled
ras-mc-ctl.service                         disabled
rasdaemon.service                          disabled
rc-local.service                           static
rdisc.service                              disabled
rdma-load-modules@.service                 static
rdma-ndd.service                           static
rdma.service                               disabled
realmd.service                             static
rescue.service                             static
rngd.service                               enabled
rpc-gssd.service                           static
rpc-statd-notify.service                   static
rpc-statd.service                          static
rpcbind.service                            enabled
rsyslog.service                            enabled
rtkit-daemon.service                       enabled
saslauthd.service                          disabled
selinux-autorelabel-mark.service           enabled
selinux-autorelabel.service                static
serial-getty@.service                      disabled
smartd.service                             enabled
speech-dispatcherd.service                 disabled
spice-vdagentd.service                     indirect
sshd-keygen@.service                       disabled
sshd.service                               enabled
sshd@.service                              static
sssd-autofs.service                        indirect
sssd-kcm.service                           indirect
sssd-nss.service                           indirect
sssd-pac.service                           indirect
sssd-pam.service                           indirect
sssd-ssh.service                           indirect
sssd-sudo.service                          indirect
sssd.service                               enabled
switcheroo-control.service                 disabled
syslog.service                             enabled
system-update-cleanup.service              static
systemd-ask-password-console.service       static
systemd-ask-password-plymouth.service      static
systemd-ask-password-wall.service          static
systemd-backlight@.service                 static
systemd-binfmt.service                     static
systemd-coredump@.service                  static
systemd-exit.service                       static
systemd-firstboot.service                  static
systemd-fsck-root.service                  static
systemd-fsck@.service                      static
systemd-halt.service                       static
systemd-hibernate-resume@.service          static
systemd-hibernate.service                  static
systemd-hostnamed.service                  static
systemd-hwdb-update.service                static
systemd-hybrid-sleep.service               static
systemd-importd.service                    static
systemd-initctl.service                    static
systemd-journal-catalog-update.service     static
systemd-journal-flush.service              static
systemd-journald.service                   static
systemd-kexec.service                      static
systemd-localed.service                    static
systemd-logind.service                     static
systemd-machine-id-commit.service          static
systemd-machined.service                   static
systemd-modules-load.service               static
systemd-nspawn@.service                    disabled
systemd-portabled.service                  static
systemd-poweroff.service                   static
systemd-quotacheck.service                 static
systemd-random-seed.service                static
systemd-reboot.service                     static
systemd-remount-fs.service                 static
systemd-resolved.service                   enabled
systemd-rfkill.service                     static
systemd-suspend-then-hibernate.service     static
systemd-suspend.service                    static
systemd-sysctl.service                     static
systemd-sysusers.service                   static
systemd-timedated.service                  masked
systemd-tmpfiles-clean.service             static
systemd-tmpfiles-setup-dev.service         static
systemd-tmpfiles-setup.service             static
systemd-udev-settle.service                static
systemd-udev-trigger.service               static
systemd-udevd.service                      static
systemd-update-done.service                static
systemd-update-utmp-runlevel.service       static
systemd-update-utmp.service                static
systemd-user-sessions.service              static
systemd-vconsole-setup.service             static
systemd-volatile-root.service              static
tcsd.service                               disabled
teamd@.service                             static
timedatex.service                          enabled
tuned.service                              enabled
udisks2.service                            enabled
unbound-anchor.service                     static
upower.service                             disabled
usb_modeswitch@.service                    static
usbmuxd.service                            static
user-runtime-dir@.service                  static
user@.service                              static
vdo.service                                enabled
vgauthd.service                            enabled
virtlockd.service                          indirect
virtlogd.service                           indirect
vmtoolsd-init.service                      disabled
vmtoolsd.service                           enabled
wacom-inputattach@.service                 static
wpa_supplicant.service                     disabled
zram.service                               static

273 unit files listed.                                                                         loaded active running NTP client/server
<font color="Red">//[SPACE]キーでスクロール、[q]キーを入力して終了</font>
</pre>
</div>
</details>
{{< /accordion >}}

2.一覧表示からchronydのみ表示してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
# systemctl list-unit-files --type=service | grep chronyd
chronyd.service                            enabled
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
</div>
</details>
{{< /accordion >}}