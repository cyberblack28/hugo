---
title: "Exercise1 rpm & dnf"
date: 2017-10-17T15:26:15Z
draft: false
weight: 10
---

## 1.rpmコマンド

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

2.lsコマンドで以前ダウンロードしたstressパッケージがあるかどうか確認してください。無い場合は、「wget https://www.cyberblack.net/practice/linux/zip/stress-1.0.4-23.el8.x86_64.rpm」で再度ダウンロードしてください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
# ls
anaconda-ks.cfg  initial-setup-ks.cfg  stress-1.0.4-23.el8.x86_64.rpm
</pre>

<pre>
# wget https://www.cyberblack.net/pracice/linux/zip/stress-1.0.4-23.el8.x86_64.rpm
--2020-02-02 23:23:04--  https://www.cyberblack.net/practice/linux/zip/stress-1.0.4-23.el8.x86_64.rpm
www.cyberblack.net (www.cyberblack.net) をDNSに問いあわせています... 185.199.110.153, 185.199.108.153, 185.199.109.153, ...
www.cyberblack.net (www.cyberblack.net)|185.199.110.153|:443 に接続しています... 接続しました。
HTTP による接続要求を送信しました、応答を待っています... 200 OK
長さ: 39652 (39K) [application/x-redhat-package-manager]
`stress-1.0.4-23.el8.x86_64.rpm.1' に保存中
  
stress-1.0.4-23.el8.x86_64.rpm.1        100%[============================================================================>]  38.72K  --.-KB/s 時間 0.02s
  
2020-02-02 23:23:05 (1.57 MB/s) - `stress-1.0.4-23.el8.x86_64.rpm.1' へ保存完了 [39652/39652]
</pre>
</div>
</details>
{{< /accordion >}}

3.一度、インストールしたstressパッケージを削除してください。パッケージが削除されたことを確認してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
# rpm -e stress
# rpm -qa | grep stress
</pre>
</div>
</details>
{{< /accordion >}}

4.再度、stressパッケージをインストールしてください。インストールされたことを確認してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
# rpm -ivh stress-1.0.4-23.el8.x86_64.rpm
警告: stress-1.0.4-23.el8.x86_64.rpm: ヘッダー V4 RSA/SHA256 Signature、鍵 ID e755cc63: NOKEY
Verifying...                          ################################# [100%]
準備しています...              ################################# [100%]
更新中 / インストール中...
   1:stress-1.0.4-23.el8              ################################# [100%]
# rpm -qa | grep stress
stress-1.0.4-23.el8.x86_64
</pre>
</div>
</details>
{{< /accordion >}}

5.stressパッケージの詳細情報を確認してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
# rpm -qi stress
Name        : stress
Version     : 1.0.4
Release     : 23.el8
Architecture: x86_64
Install Date: 2020年02月02日 23時31分35秒
Group       : Unspecified
Size        : 81677
License     : GPLv2+
Signature   : RSA/SHA256, 2019年08月26日 11時59分22秒, Key ID 7a517b82e755cc63
Source RPM  : stress-1.0.4-23.el8.src.rpm
Build Date  : 2019年08月26日 11時59分18秒
Build Host  : r2d2.marmotte.net
Relocations : (not relocatable)
URL         : http://people.seas.harvard.edu/~apw/stress/
Summary     : A tool to put given subsystems under a specified load
Description :
stress is not a benchmark, but is rather a tool designed to put given
subsytems under a specified load. Instances in which this is useful
include those in which a system administrator wishes to perform tuning
activities, a kernel or libc programmer wishes to evaluate denial of
service possibilities, etc.
</pre>
</div>
</details>
{{< /accordion >}}

6.stressパッケージに含まれるファイルの一覧を確認してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
# rpm -ql stress
/usr/bin/stress
/usr/lib/.build-id
/usr/lib/.build-id/94
/usr/lib/.build-id/94/a6cb123d1a5ba9215ea96ded1d27076ebd85a3
/usr/share/doc/stress
/usr/share/doc/stress/AUTHORS
/usr/share/doc/stress/COPYING
/usr/share/doc/stress/ChangeLog
/usr/share/doc/stress/NEWS
/usr/share/doc/stress/README
/usr/share/doc/stress/TODO
/usr/share/doc/stress/stress.html
/usr/share/info/stress.info.gz
/usr/share/man/man1/stress.1.gz
</pre>
</div>
</details>
{{< /accordion >}}

7.rpmコマンドでOS内にインストールされているパッケージを確認してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
# rpm -qa
iproute-tc-4.18.0-15.el8.x86_64
boost-iostreams-1.66.0-6.el8.x86_64
openssl-libs-1.1.1c-2.el8.x86_64
gnu-free-mono-fonts-20120503-18.el8.noarch
liberation-fonts-common-2.00.3-4.el8.noarch
glusterfs-cli-6.0-15.el8.x86_64
libksba-1.3.5-7.el8.x86_64
cockpit-ws-196.3-1.el8.x86_64
dbus-1.12.8-9.el8.x86_64
lohit-bengali-fonts-2.91.5-3.el8.noarch
yelp-xsl-3.28.0-2.el8.noarch
policycoreutils-python-utils-2.9-3.el8.noarch
hunspell-1.6.2-1.el8.x86_64
rhsm-gtk-1.25.17-1.el8.x86_64
cairo-gobject-1.15.12-3.el8.x86_64
paktype-naskh-basic-fonts-4.1-9.el8.noarch
python3-setuptools-wheel-39.2.0-5.el8.noarch
fprintd-0.8.1-2.el8.x86_64
ethtool-5.0-2.el8.x86_64
sssd-ldap-2.2.0-19.el8.x86_64
gstreamer1-1.14.0-3.el8.x86_64
rootfiles-8.1-22.el8.noarch
urw-base35-fonts-common-20170801-10.el8.noarch
brlapi-0.6.7-28.el8.x86_64
libini_config-1.3.1-39.el8.x86_64
cryptsetup-2.2.0-2.el8.x86_64
alsa-lib-1.1.9-4.el8.x86_64
iwl5150-firmware-8.24.2.2-94.el8.1.noarch
google-droid-sans-fonts-20120715-13.el8.noarch
speech-dispatcher-espeak-ng-0.8.8-6.el8.x86_64
gsm-1.0.17-5.el8.x86_64
perl-podlators-4.11-1.el8.noarch
python3-gobject-base-3.28.3-1.el8.x86_64
iwl105-firmware-18.168.6.1-94.el8.1.noarch
seavgabios-bin-1.11.1-4.module_el8.1.0+248+298dec18.noarch
usb_modeswitch-data-20170806-2.el8.noarch
speex-1.2.0-1.el8.x86_64
perl-DBD-SQLite-1.58-2.module_el8.1.0+207+bdacd7b7.x86_64
libreport-2.9.5-9.el8.x86_64
systemd-239-18.el8_1.1.x86_64
ipxe-roms-qemu-20181214-3.git133f4c47.el8.noarch
python3-pyyaml-3.12-12.el8.x86_64
glx-utils-8.3.0-9.el8.x86_64
harfbuzz-1.7.5-3.el8.x86_64
libwbclient-4.10.4-101.el8_1.x86_64
adobe-mappings-pdf-20180407-1.el8.noarch
python3-newt-0.52.20-9.el8.x86_64
libXvMC-1.0.10-6.el8.x86_64
libosinfo-1.5.0-3.el8.x86_64
glibmm24-2.56.0-1.el8.x86_64
systemd-udev-239-18.el8_1.1.x86_64
glibc-langpack-en-2.28-72.el8.x86_64
python3-pysocks-1.6.8-3.el8.noarch
libXxf86dga-1.1.4-12.el8.x86_64
cockpit-storaged-197.3-1.el8.noarch
dracut-squash-049-27.git20190906.el8_1.1.x86_64
libcom_err-1.44.6-3.el8.x86_64
python36-3.6.8-2.module_el8.1.0+245+c39af44f.x86_64
lua-lpeg-1.0.1-6.el8.x86_64
gnome-bluetooth-libs-3.28.2-2.el8.x86_64
plymouth-scripts-0.9.3-15.el8.x86_64
libvirt-daemon-driver-storage-mpath-4.5.0-35.1.module_el8.1.0+258+1d2a1d58.x86_64
perl-Carp-1.42-396.el8.noarch
python3-pid-2.1.1-7.el8.noarch
mtools-4.0.18-14.el8.x86_64
gnome-settings-daemon-3.32.0-4.el8.x86_64
poppler-0.66.0-26.el8.x86_64
libcacard-2.7.0-2.el8_1.x86_64
audit-libs-3.0-0.10.20180831git0047a6c.el8.x86_64
pango-1.42.4-6.el8.x86_64
perl-Text-Tabs+Wrap-2013.0523-395.el8.noarch
gnome-shell-extension-launch-new-instance-3.32.1-10.el8.noarch
geoclue2-2.4.10-1.el8.x86_64
libvirt-daemon-driver-nodedev-4.5.0-35.1.module_el8.1.0+258+1d2a1d58.x86_64
yajl-2.1.0-10.el8.x86_64
clutter-gtk-1.8.4-3.el8.x86_64
perl-interpreter-5.26.3-416.el8.x86_64
initial-setup-0.3.62.1-1.el8.x86_64
python3-dnf-4.2.7-7.el8_1.noarch
p11-kit-0.23.14-5.el8_0.x86_64
zenity-3.28.1-1.el8.x86_64
perl-File-Temp-0.230.600-1.el8.noarch
libuser-0.62-23.el8.x86_64
yum-4.2.7-7.el8_1.noarch
libwayland-egl-1.15.0-1.el8.x86_64
gspell-1.8.1-1.el8.x86_64
libmodman-2.0.1-17.el8.x86_64
gnome-boxes-3.28.5-7.el8.x86_64
gupnp-1.0.3-2.el8.x86_64
gnome-session-xsession-3.28.1-7.el8_1.x86_64
pcre-8.42-4.el8.x86_64
adwaita-gtk2-theme-3.22.3-4.el8.x86_64
libpaper-1.1.24-22.el8.x86_64
gnome-screenshot-3.26.0-3.el8.x86_64
libqmi-1.22.4-4.el8.x86_64
sos-3.7-8.el8_1.noarch
gmp-6.1.2-10.el8.x86_64
fuse3-libs-3.2.1-12.el8.x86_64
gedit-3.28.1-3.el8.x86_64
libblockdev-fs-2.19-9.el8.x86_64
wget-1.19.5-8.el8_1.1.x86_64
libX11-1.6.7-1.el8.x86_64
yelp-libs-3.28.1-3.el8.x86_64
libpkgconf-1.4.2-1.el8.x86_64
gnome-software-3.30.6-2.el8.x86_64
pinentry-1.1.0-2.el8.x86_64
stress-1.0.4-23.el8.x86_64
libXtst-1.2.3-7.el8.x86_64
gnome-autoar-0.2.3-1.el8.x86_64
libsmbios-2.4.1-2.el8.x86_64
grub2-pc-2.02-78.el8.x86_64
libtar-1.2.20-15.el8.x86_64
paps-libs-0.6.8-41.el8.x86_64
lzo-minilzo-2.08-14.el8.x86_64
eog-3.28.4-1.el8.x86_64
python3-ordered-set-2.0.2-4.el8.noarch
libunistring-0.9.9-3.el8.x86_64
urw-base35-gothic-fonts-20170801-10.el8.noarch
libtiff-4.0.9-15.el8.x86_64
PackageKit-gtk3-module-1.1.12-3.el8.x86_64
switcheroo-control-1.1-5.el8.x86_64
libsss_idmap-2.2.0-19.el8.x86_64
libfastjson-0.99.8-2.el8.x86_64
pulseaudio-module-x11-11.1-23.el8.x86_64
ima-evm-utils-1.1-5.el8.x86_64
boost-system-1.66.0-6.el8.x86_64
libmediaart-1.9.4-4.el8.x86_64
mcpp-2.7.2-20.el8.x86_64
xorg-x11-drv-evdev-2.10.6-2.el8.x86_64
librdmacm-22.3-1.el8.x86_64
opus-1.3-0.4.beta.el8.x86_64
libgphoto2-2.5.16-3.el8.x86_64
ncompress-4.2.4.4-12.el8.x86_64
PackageKit-command-not-found-1.1.12-3.el8.x86_64
NetworkManager-team-1.20.0-3.el8.x86_64
lzo-2.08-14.el8.x86_64
numad-0.5-26.20150602git.el8.x86_64
libssh-config-0.9.0-4.el8.noarch
spice-vdagent-0.19.0-3.el8.x86_64
celt051-0.5.1.3-15.el8.x86_64
oddjob-0.34.4-7.el8.x86_64
cyrus-sasl-lib-2.1.27-1.el8.x86_64
net-tools-2.0-0.51.20160912git.el8.x86_64
python3-simpleline-1.1-2.el8.noarch
exiv2-libs-0.26-10.el8.x86_64
tigervnc-server-minimal-1.9.0-10.el8.x86_64
curl-7.61.1-11.el8.x86_64
rpm-ostree-libs-2019.3-3.el8.x86_64
psmisc-23.1-3.el8.x86_64
grilo-0.3.6-2.el8.x86_64
krb5-libs-1.17-9.el8.x86_64
enscript-1.6.6-17.el8.x86_64
libreport-anaconda-2.9.5-9.el8.x86_64
speexdsp-1.2-0.13.rc3.el8.x86_64
gnome-keyring-pam-3.28.2-1.el8.x86_64
gettext-libs-0.19.8.1-17.el8.x86_64
lshw-B.02.18-21.el8.x86_64
libgovirt-0.3.4-9.el8.x86_64
libXmu-1.1.2-12.el8.x86_64
python3-meh-0.47.2-1.el8.noarch
shadow-utils-4.6-8.el8.x86_64
google-noto-sans-sinhala-fonts-20161022-7.el8.noarch
lvm2-2.03.05-5.el8.0.1.x86_64
xcb-util-0.4.0-10.el8.x86_64
tpm2-tools-3.1.4-5.el8.x86_64
kbd-2.0.4-8.el8.x86_64
mtr-0.92-3.el8.x86_64
libmbim-utils-1.18.2-3.el8.x86_64
exempi-2.4.5-2.el8.x86_64
libdb-5.3.28-37.el8.x86_64
khmeros-base-fonts-5.0-25.el8.noarch
glusterfs-client-xlators-6.0-15.el8.x86_64
xml-common-0.6.3-50.el8.noarch
gettext-0.19.8.1-17.el8.x86_64
hyperv-daemons-license-0-0.27.20180415git.el8.noarch
jomolhari-fonts-0.003-24.el8.noarch
python3-libsemanage-2.9-1.el8.x86_64
xorg-x11-server-Xwayland-1.20.3-8.el8.x86_64
boost-date-time-1.66.0-6.el8.x86_64
trousers-0.3.14-4.el8.x86_64
langtable-data-0.0.38-5.el8.noarch
lohit-odia-fonts-2.91.2-3.el8.noarch
python3-firewall-0.7.0-5.el8.noarch
sssd-krb5-common-2.2.0-19.el8.x86_64
libselinux-utils-2.9-2.1.el8.x86_64
platform-python-3.6.8-15.1.el8.x86_64
centos-gpg-keys-8.1-1.1911.0.8.el8.noarch
stix-fonts-1.1.0-12.el8.noarch
python3-linux-procfs-0.6-7.el8.noarch
realmd-0.16.3-16.el8.x86_64
iptables-1.8.2-16.el8.x86_64
libsecret-0.18.6-1.el8.x86_64
iwl6000g2b-firmware-18.168.6.1-94.el8.1.noarch
alsa-utils-1.1.9-1.el8.x86_64
clevis-luks-11-2.el8.x86_64
newt-0.52.20-9.el8.x86_64
polkit-pkla-compat-0.1-12.el8.x86_64
thai-scalable-fonts-common-0.6.5-1.el8.noarch
iwl2030-firmware-18.168.6.1-94.el8.1.noarch
python3-cups-1.9.72-21.el8.0.1.x86_64
perl-HTTP-Tiny-0.074-1.el8.noarch
libpmem-1.6-2.el8.x86_64
NetworkManager-1.20.0-3.el8.x86_64
podman-manpages-1.4.2-5.module_el8.1.0+237+63e26edc.noarch
libvirt-libs-4.5.0-35.1.module_el8.1.0+258+1d2a1d58.x86_64
python3-libstoragemgmt-1.8.1-2.el8.noarch
dhcp-client-4.3.6-34.el8.x86_64
PackageKit-glib-1.1.12-3.el8.x86_64
edk2-ovmf-20190308git89910a39dcfd-6.el8.noarch
libvirt-daemon-driver-network-4.5.0-35.1.module_el8.1.0+258+1d2a1d58.x86_64
libpeas-loader-python3-1.22.0-6.el8.x86_64
libatasmart-0.19-14.el8.x86_64
squashfs-tools-4.3-19.el8.x86_64
pulseaudio-libs-glib2-11.1-23.el8.x86_64
pkgconf-m4-1.4.2-1.el8.noarch
mesa-libgbm-19.1.4-3.el8_1.x86_64
python3-pyOpenSSL-18.0.0-1.el8.noarch
nautilus-3.28.1-10.el8.x86_64
vim-minimal-8.0.1763-13.el8.x86_64
libmbim-1.18.2-3.el8.x86_64
glibc-2.28-72.el8.x86_64
webkit2gtk3-plugin-process-gtk2-2.24.4-2.el8_1.x86_64
python3-requests-ftp-0.3.1-11.el8.noarch
rsyslog-8.37.0-13.el8.x86_64
libsolv-0.7.4-3.el8.x86_64
libgcrypt-1.8.3-4.el8.x86_64
libvirt-daemon-driver-storage-gluster-4.5.0-35.1.module_el8.1.0+258+1d2a1d58.x86_64
python3-langtable-0.0.38-5.el8.noarch
libcomps-0.1.11-2.el8.x86_64
libinput-1.13.2-1.el8.x86_64
popt-1.16-14.el8.x86_64
nss-softokn-3.44.0-9.el8_1.x86_64
gnome-video-effects-0.4.3-3.el8.noarch
gnome-shell-3.32.2-9.el8.x86_64
perl-macros-5.26.3-416.el8.x86_64
glib-networking-2.56.1-1.1.el8.x86_64
freetype-2.9.1-4.el8.x86_64
qemu-kvm-block-rbd-2.12.0-88.module_el8.1.0+258+1d2a1d58.1.x86_64
clutter-1.26.2-6.el8.x86_64
lsof-4.91-2.el8.x86_64
perl-constant-1.33-396.el8.noarch
libgusb-0.3.0-1.el8.x86_64
libtdb-1.3.18-2.el8.x86_64
libvirt-daemon-driver-qemu-4.5.0-35.1.module_el8.1.0+258+1d2a1d58.x86_64
gjs-1.56.2-3.el8.x86_64
quota-4.04-10.el8.x86_64
perl-Time-Local-1.280-1.el8.noarch
libX11-xcb-1.6.7-1.el8.x86_64
libgs-9.25-5.el8_1.1.x86_64
gstreamer1-plugins-good-1.14.0-4.el8.x86_64
tpm2-tss-2.0.0-4.el8.x86_64
libxklavier-5.4-11.el8.x86_64
kernel-4.18.0-147.3.1.el8_1.x86_64
gnome-terminal-3.28.2-3.el8.x86_64
gnome-initial-setup-3.28.0-8.el8.x86_64
pigz-2.4-2.el8.x86_64
librbd1-12.2.7-9.el8.x86_64
libbasicobjects-0.1.1-39.el8.x86_64
qemu-guest-agent-2.12.0-88.module_el8.1.0+258+1d2a1d58.1.x86_64
ibus-gtk2-1.5.19-4.el8.x86_64
rsyslog-relp-8.37.0-13.el8.x86_64
checkpolicy-2.9-1.el8.x86_64
selinux-policy-targeted-3.14.3-20.el8.noarch
which-2.21-10.el8.x86_64
ca-certificates-2019.2.32-80.0.el8_1.noarch
evolution-data-server-3.28.5-11.el8.x86_64
gvfs-archive-1.36.2-6.el8.x86_64
libndp-1.7-1.el8.x86_64
libblockdev-swap-2.19-9.el8.x86_64
libXi-1.7.9-7.el8.x86_64
spice-server-0.14.2-1.el8.x86_64
tuned-2.12.0-3.el8.noarch
mallard-rng-1.0.3-1.el8.noarch
gpgme-1.10.0-6.el8.0.1.x86_64
orc-0.4.28-2.el8.x86_64
libreport-gtk-2.9.5-9.el8.x86_64
hyperv-daemons-0-0.27.20180415git.el8.x86_64
libsysfs-2.1.0-24.el8.x86_64
python3-systemd-234-8.el8.x86_64
libacl-2.2.53-1.el8.x86_64
urw-base35-bookman-fonts-20170801-10.el8.noarch
gnome-system-monitor-3.28.2-1.el8.x86_64
gpm-libs-1.20.7-15.el8.x86_64
gtk-update-icon-cache-3.22.30-4.el8.x86_64
file-libs-5.33-8.el8.x86_64
urw-base35-standard-symbols-ps-fonts-20170801-10.el8.noarch
gnome-logs-3.28.5-3.el8.x86_64
libdnet-1.12-26.el8.x86_64
gnome-menus-3.13.3-10.el8.x86_64
libXt-1.1.5-12.el8.x86_64
gvnc-0.9.0-1.el8.x86_64
buildah-1.9.0-5.module_el8.1.0+237+63e26edc.x86_64
libmaxminddb-1.2.0-6.el8.x86_64
libjose-10-2.el8.x86_64
libpcap-1.9.0-3.el8.x86_64
setroubleshoot-plugins-3.3.10-3.el8.noarch
xorg-x11-drv-qxl-0.1.5-9.el8.x86_64
libusal-1.1.11-39.el8.x86_64
device-mapper-multipath-0.8.0-5.el8.x86_64
mpfr-3.1.6-1.el8.x86_64
hplip-libs-3.18.4-9.el8.x86_64
wavpack-5.1.0-9.el8.x86_64
libblockdev-mpath-2.19-9.el8.x86_64
libwebp-1.0.0-1.el8.x86_64
hypervfcopyd-0-0.27.20180415git.el8.x86_64
blktrace-1.2.0-10.el8.x86_64
firewalld-filesystem-0.7.0-5.el8.noarch
libblockdev-nvdimm-2.19-9.el8.x86_64
libXxf86vm-1.1.4-9.el8.x86_64
qpdf-libs-7.1.1-10.el8.x86_64
smartmontools-6.6-3.el8.x86_64
libkcapi-hmaccalc-1.1.1-16_1.el8.x86_64
python3-bind-9.11.4-26.P2.el8.noarch
libcdio-2.0.0-3.el8.x86_64
dleyna-server-0.6.0-2.el8.x86_64
prefixdevname-0.1.0-6.el8.x86_64
cracklib-2.9.6-15.el8.x86_64
volume_key-libs-0.3.11-5.el8.x86_64
libraw1394-2.1.2-5.el8.x86_64
openssh-8.0p1-3.el8.x86_64
iptstate-2.2.6-6.el8.x86_64
openssl-pkcs11-0.4.8-2.el8.x86_64
passwd-0.80-2.el8.x86_64
xorg-x11-server-common-1.20.3-8.el8.x86_64
iprutils-2.4.18.1-1.el8.x86_64
dbus-tools-1.12.8-9.el8.x86_64
xorg-x11-drv-libinput-0.28.0-2.el8.x86_64
nftables-0.9.0-14.el8.x86_64
dnf-plugins-core-4.0.8-3.el8.noarch
google-noto-sans-tai-viet-fonts-20161022-7.el8.noarch
libutempter-1.1.6-14.el8.x86_64
gssproxy-0.8.0-14.el8.x86_64
boost-regex-1.66.0-6.el8.x86_64
libmusicbrainz5-5.1.0-10.el8.x86_64
langpacks-ja-1.0-12.el8.noarch
os-prober-1.74-6.el8.x86_64
libnl3-cli-3.4.0-5.el8.x86_64
fontpackages-filesystem-1.44-22.el8.noarch
xdg-utils-1.1.2-5.el8.noarch
rpm-libs-4.14.2-25.el8.x86_64
libgomp-8.3.1-4.5.el8.x86_64
tzdata-2019c-1.el8.noarch
crypto-policies-20190807-1.git9b1477b.el8.noarch
iso-codes-3.79-2.el8.noarch
gnu-free-fonts-common-20120503-18.el8.noarch
shared-mime-info-1.9-3.el8.x86_64
mozjs60-60.9.0-3.el8.x86_64
bind-license-9.11.4-26.P2.el8.noarch
boost-program-options-1.66.0-6.el8.x86_64
langtable-0.0.38-5.el8.noarch
fontconfig-2.13.1-3.el8.x86_64
webrtc-audio-processing-0.3-8.el8.x86_64
geolite2-city-20180605-1.el8.noarch
platform-python-setuptools-39.2.0-5.el8.noarch
brotli-1.0.6-1.el8.x86_64
emacs-filesystem-26.1-5.el8.noarch
avahi-libs-0.7-19.el8.x86_64
libedit-3.1-23.20170329cvs.el8.x86_64
libgudev-232-4.el8.x86_64
iptables-ebtables-1.8.2-16.el8.x86_64
adobe-mappings-cmap-deprecated-20171205-3.el8.noarch
gsettings-desktop-schemas-3.32.0-3.el8.x86_64
ncurses-6.1-7.20180224.el8.x86_64
dejavu-sans-fonts-2.35-6.el8.noarch
polkit-0.115-9.el8.x86_64
userspace-rcu-0.10.1-2.el8.x86_64
smc-fonts-common-6.1-10.el8.noarch
libnotify-0.7.7-5.el8.x86_64
gutenprint-libs-5.2.14-3.el8.x86_64
tigervnc-license-1.9.0-10.el8.noarch
libldb-1.5.4-2.el8.x86_64
mtdev-1.1.5-12.el8.x86_64
poppler-data-0.4.9-1.el8.noarch
gutenprint-5.2.14-3.el8.x86_64
libwacom-data-0.31-1.el8.noarch
libblockdev-utils-2.19-9.el8.x86_64
lua-socket-3.0-0.17.rc1.el8.x86_64
gnome-user-docs-3.28.2-1.el8.noarch
dbus-glib-0.110-2.el8.x86_64
libiec61883-1.2.0-18.el8.x86_64
anaconda-user-help-8.1.1-1.el8.noarch
centos-logos-80.5-2.el8.x86_64
gdbm-1.18-1.el8.x86_64
publicsuffix-list-dafsa-20180723-1.el8.noarch
ModemManager-glib-1.10.4-1.el8.x86_64
libusbmuxd-1.0.10-9.el8.x86_64
libselinux-2.9-2.1.el8.x86_64
iproute-4.18.0-15.el8.x86_64
attr-2.4.48-3.el8.x86_64
glibc-common-2.28-72.el8.x86_64
cairomm-1.12.0-7.el8.x86_64
libXpm-3.5.12-7.el8.x86_64
zlib-1.2.11-10.el8.x86_64
libevent-2.1.8-5.el8.x86_64
libuuid-2.32.1-17.el8.x86_64
device-mapper-event-libs-1.02.163-5.el8.0.1.x86_64
keyutils-1.5.10-6.el8.x86_64
libcap-2.26-1.el8.x86_64
xmlrpc-c-client-1.51.0-5.el8.x86_64
jasper-libs-2.0.14-4.el8.x86_64
perl-libs-5.26.3-416.el8.x86_64
liboauth-1.0.3-9.el8.x86_64
libidn-1.34-5.el8.x86_64
bzip2-libs-1.0.6-26.el8.x86_64
accountsservice-libs-0.6.50-7.el8.x86_64
perl-Errno-1.28-416.el8.x86_64
libpng-1.6.34-5.el8.x86_64
libappstream-glib-0.7.14-3.el8.x86_64
perl-File-Path-2.15-2.el8.noarch
numactl-libs-2.0.12-7.el8.x86_64
geocode-glib-3.26.0-1.el8.x86_64
perl-threads-2.21-2.el8.x86_64
libtalloc-2.1.16-3.el8.x86_64
python3-decorator-4.2.1-2.el8.noarch
perl-IO-Socket-IP-0.39-5.el8.noarch
nspr-4.21.0-2.el8_0.x86_64
perl-Digest-1.17-395.el8.noarch
libwayland-server-1.15.0-1.el8.x86_64
upower-0.99.7-3.el8.x86_64
perl-Math-BigInt-1.9998.11-7.el8.noarch
lua-libs-5.3.4-11.el8.x86_64
libudisks2-2.8.3-2.el8.x86_64
libss-1.44.6-3.el8.x86_64
pixman-0.36.0-1.el8.x86_64
cyrus-sasl-gssapi-2.1.27-1.el8.x86_64
graphite2-1.3.10-10.el8.x86_64
libseccomp-2.4.1-1.el8.x86_64
poppler-glib-0.66.0-26.el8.x86_64
libxslt-1.1.32-3.el8.x86_64
plymouth-graphics-libs-0.9.3-15.el8.x86_64
vim-common-8.0.1763-13.el8.x86_64
libwayland-cursor-1.15.0-1.el8.x86_64
selinux-policy-3.14.3-20.el8.noarch
dosfstools-4.1-6.el8.x86_64
libdhash-0.5.0-39.el8.x86_64
libblockdev-2.19-9.el8.x86_64
hardlink-1.3-6.el8.x86_64
libXau-1.0.8-13.el8.x86_64
libblockdev-part-2.19-9.el8.x86_64
libnghttp2-1.33.0-1.el8_0.1.x86_64
libXfixes-5.0.3-7.el8.x86_64
pulseaudio-11.1-23.el8.x86_64
pkgconf-pkg-config-1.4.2-1.el8.x86_64
libXrender-0.9.10-7.el8.x86_64
gnupg2-2.2.9-1.el8.x86_64
libsigsegv-2.11-5.el8.x86_64
libogg-1.3.2-10.el8.x86_64
libsss_nss_idmap-2.2.0-19.el8.x86_64
libassuan-2.5.1-3.el8.x86_64
bolt-0.8-2.el8.x86_64
libvarlink-18-3.el8.x86_64
libattr-2.4.48-3.el8.x86_64
python3-ply-3.9-7.el8.noarch
containernetworking-plugins-0.8.1-2.module_el8.1.0+237+63e26edc.x86_64
lz4-libs-1.8.1.2-4.el8.x86_64
gdk-pixbuf2-modules-2.36.12-5.el8.x86_64
jbig2dec-libs-0.14-2.el8.x86_64
perl-parent-0.237-1.el8.noarch
cronie-anacron-1.5.2-4.el8.x86_64
liba52-0.7.4-32.el8.x86_64
libdrm-2.4.98-2.el8.x86_64
at-spi2-atk-2.26.2-1.el8.x86_64
libdv-1.0.0-27.el8.x86_64
libepoxy-1.5.2-1.el8.x86_64
slirp4netns-0.3.0-4.module_el8.1.0+237+63e26edc.x86_64
gavl-1.4.0-12.el8.x86_64
findutils-4.6.0-20.el8.x86_64
bind-libs-lite-9.11.4-26.P2.el8.x86_64
ipcalc-0.2.4-3.el8.x86_64
grub2-common-2.02-78.el8.noarch
rdma-core-22.3-1.el8.x86_64
libmpcdec-1.2.6-20.el8.x86_64
libexif-0.6.21-16.el8.x86_64
libvisual-0.4.0-24.el8.x86_64
libXv-1.0.11-7.el8.x86_64
genisoimage-1.1.11-39.el8.x86_64
protobuf-c-1.3.0-4.el8.x86_64
gdbm-libs-1.18-1.el8.x86_64
sssd-nfs-idmap-2.2.0-19.el8.x86_64
mobile-broadband-provider-info-1.20170310-1.el8.noarch
libdvdread-5.0.3-9.el8.x86_64
kbd-legacy-2.0.4-8.el8.noarch
file-5.33-8.el8.x86_64
ndctl-65-1.el8.x86_64
dhcp-common-4.3.6-34.el8.noarch
libtheora-1.1.1-21.el8.x86_64
rpm-build-libs-4.14.2-25.el8.x86_64
openldap-2.4.46-10.el8.x86_64
libical-3.0.3-3.el8.x86_64
python3-cffi-1.11.5-5.el8.x86_64
libarchive-3.3.2-7.el8.x86_64
bzip2-1.0.6-26.el8.x86_64
ostree-2019.2-1.el8.x86_64
elfutils-default-yama-scope-0.176-5.el8.noarch
libverto-0.3.0-5.el8.x86_64
python3-gpg-1.10.0-6.el8.0.1.x86_64
cracklib-dicts-2.9.6-15.el8.x86_64
libieee1284-0.2.11-28.el8.x86_64
libqmi-utils-1.22.4-4.el8.x86_64
libnsl2-1.2.0-2.20180605git4a062cf.el8.x86_64
adcli-0.8.2-3.el8.x86_64
rpm-4.14.2-25.el8.x86_64
kernel-modules-4.18.0-147.el8.x86_64
libfdisk-2.32.1-17.el8.x86_64
boost-random-1.66.0-6.el8.x86_64
xorg-x11-drv-fbdev-0.5.0-2.el8.x86_64
coreutils-8.30-6.el8.x86_64
libnftnl-1.1.1-4.el8.x86_64
device-mapper-event-1.02.163-5.el8.0.1.x86_64
device-mapper-libs-1.02.163-5.el8.0.1.x86_64
device-mapper-persistent-data-0.8.5-2.el8.x86_64
libverto-libevent-0.3.0-5.el8.x86_64
kmod-25-13.el8.x86_64
xmlsec1-1.2.25-4.el8.x86_64
bluez-obexd-5.50-1.el8.x86_64
man-pages-4.15-6.el8.x86_64
google-noto-sans-cjk-ttc-fonts-20190416-1.el8.noarch
glusterfs-api-6.0-15.el8.x86_64
gnu-free-serif-fonts-20120503-18.el8.noarch
perl-Net-SSLeay-1.88-1.el8.x86_64
libblockdev-dm-2.19-9.el8.x86_64
julietaula-montserrat-fonts-7.200-2.el8.noarch
python3-setools-4.2.2-1.el8.x86_64
lohit-gujarati-fonts-2.92.4-3.el8.noarch
rarian-0.8.1-19.el8.x86_64
runc-1.0.0-60.rc8.module_el8.1.0+237+63e26edc.x86_64
lohit-tamil-fonts-2.91.3-3.el8.noarch
sssd-common-2.2.0-19.el8.x86_64
python3-pydbus-0.6.0-5.el8.noarch
sil-abyssinica-fonts-1.200-13.el8.noarch
sssd-ipa-2.2.0-19.el8.x86_64
chrony-3.5-1.el8.x86_64
gutenprint-doc-5.2.14-3.el8.x86_64
sssd-2.2.0-19.el8.x86_64
python3-bytesize-1.4-1.el8.x86_64
libertas-usb8388-firmware-20190516-94.git711d3297.el8.noarch
fprintd-pam-0.8.1-2.el8.x86_64
python3-brlapi-0.6.7-28.el8.x86_64
iwl6000g2a-firmware-18.168.6.1-94.el8.1.noarch
luksmeta-9-2.el8.x86_64
pcaudiolib-1.1-2.el8.x86_64
iwl4965-firmware-228.61.2.24-94.el8.1.noarch
perl-Pod-Simple-3.35-395.el8.noarch
pulseaudio-utils-11.1-23.el8.x86_64
iwl2000-firmware-18.168.6.1-94.el8.1.noarch
perl-Pod-Perldoc-3.28-396.el8.noarch
iio-sensor-proxy-2.4-3.el8.x86_64
iwl100-firmware-39.31.5.1-94.el8.1.noarch
perl-libnet-3.11-3.el8.noarch
python3-libcomps-0.1.11-2.el8.x86_64
systemd-libs-239-18.el8_1.1.x86_64
dhcp-libs-4.3.6-34.el8.x86_64
qemu-kvm-common-2.12.0-88.module_el8.1.0+258+1d2a1d58.1.x86_64
cockpit-system-196.3-1.el8.noarch
platform-python-coverage-4.5.1-7.el8.x86_64
samba-common-4.10.4-101.el8_1.noarch
xdg-desktop-portal-gtk-1.0.2-1.el8.x86_64
python3-pyatspi-2.26.0-6.el8.noarch
qemu-img-2.12.0-88.module_el8.1.0+258+1d2a1d58.1.x86_64
gvfs-fuse-1.36.2-6.el8.x86_64
libdnf-0.35.1-9.el8_1.x86_64
tracker-2.1.5-1.el8.x86_64
python3-rhnlib-2.8.6-8.module_el8.1.0+211+ad6c0bc7.noarch
kernel-core-4.18.0-147.3.1.el8_1.x86_64
udisks2-iscsi-2.8.3-2.el8.x86_64
kernel-modules-4.18.0-147.3.1.el8_1.x86_64
logrotate-3.14.0-3.el8.x86_64
python3-setuptools-39.2.0-5.el8.noarch
mesa-libEGL-19.1.4-3.el8_1.x86_64
libcanberra-gtk3-0.30-16.el8.x86_64
blivet-data-3.1.0-17.el8.noarch
libvirt-daemon-driver-storage-iscsi-4.5.0-35.1.module_el8.1.0+258+1d2a1d58.x86_64
metacity-3.28.0-1.el8.x86_64
python3-louis-2.6.2-16.el8.noarch
libvirt-daemon-driver-storage-scsi-4.5.0-35.1.module_el8.1.0+258+1d2a1d58.x86_64
color-filesystem-1-20.el8.noarch
python3-pyxdg-0.25-16.el8.noarch
nss-sysinit-3.44.0-9.el8_1.x86_64
gdm-3.28.3-22.el8.x86_64
gd-2.2.5-6.el8.x86_64
qemu-kvm-block-curl-2.12.0-88.module_el8.1.0+258+1d2a1d58.1.x86_64
gnome-shell-extension-desktop-icons-3.32.1-10.el8.noarch
gstreamer1-plugins-base-1.14.0-4.el8.x86_64
qemu-kvm-block-ssh-2.12.0-88.module_el8.1.0+258+1d2a1d58.1.x86_64
gnome-shell-extension-window-list-3.32.1-10.el8.noarch
gtk2-2.24.32-4.el8.x86_64
libvirt-daemon-driver-secret-4.5.0-35.1.module_el8.1.0+258+1d2a1d58.x86_64
anaconda-core-29.19.1.13-1.el8.x86_64
pipewire-0.2.5-1.el8.x86_64
kernel-tools-libs-4.18.0-147.3.1.el8_1.x86_64
initial-setup-gui-0.3.62.1-1.el8.x86_64
libgweather-3.28.2-2.el8.x86_64
mesa-filesystem-19.1.4-3.el8_1.x86_64
libgnomekbd-3.26.0-4.el8.x86_64
ghostscript-9.25-5.el8_1.1.x86_64
spice-glib-0.37-1.el8.x86_64
open-vm-tools-desktop-10.3.10-3.el8_1.1.x86_64
vte291-0.52.2-2.el8.x86_64
webkit2gtk3-2.24.4-2.el8_1.x86_64
chrome-gnome-shell-10.1-6.el8.x86_64
spice-gtk3-0.37-1.el8.x86_64
mutter-3.32.2-11.el8_1.x86_64
gnome-color-manager-3.28.0-1.el8.x86_64
gnome-desktop3-3.32.2-1.el8.x86_64
microcode_ctl-20190618-1.20191115.3.el8_1.x86_64
rsyslog-gssapi-8.37.0-13.el8.x86_64
pinentry-gtk-1.1.0-2.el8.x86_64
python3-requests-2.20.0-2.1.el8_1.noarch
totem-nautilus-3.26.2-1.el8.x86_64
gnome-online-accounts-3.28.0-1.el8.x86_64
bpftool-4.18.0-147.3.1.el8_1.x86_64
gvfs-afp-1.36.2-6.el8.x86_64
glade-libs-3.22.1-1.el8.x86_64
fribidi-1.0.4-7.el8_1.x86_64
gvfs-mtp-1.36.2-6.el8.x86_64
gstreamer1-plugins-ugly-free-1.14.0-2.el8.x86_64
sssd-kcm-2.2.0-19.el8.x86_64
ibus-setup-1.5.19-4.el8.noarch
gnome-remote-desktop-0.1.6-5.el8.x86_64
libwnck3-3.24.1-2.el8.x86_64
paps-0.6.8-41.el8.x86_64
plymouth-plugin-two-step-0.9.3-15.el8.x86_64
gnome-terminal-nautilus-3.28.2-3.el8.x86_64
urw-base35-c059-fonts-20170801-10.el8.noarch
gnome-characters-3.28.2-1.el8.x86_64
urw-base35-nimbus-roman-fonts-20170801-10.el8.noarch
file-roller-3.28.1-2.el8.x86_64
urw-base35-z003-fonts-20170801-10.el8.noarch
vim-enhanced-8.0.1763-13.el8.x86_64
libspectre-0.2.8-5.el8.x86_64
firewalld-0.7.0-5.el8.noarch
gtk-vnc2-0.9.0-1.el8.x86_64
yelp-tools-3.28.0-3.el8.noarch
authselect-libs-1.1-2.el8.x86_64
xorg-x11-drv-nouveau-1.0.15-4.el8.1.x86_64
setroubleshoot-server-3.3.20-2.el8.x86_64
kpatch-0.6.1-5.el8.noarch
sane-backends-libs-1.0.27-19.el8.x86_64
util-linux-user-2.32.1-17.el8.x86_64
mdadm-4.1-9.el8.x86_64
NetworkManager-tui-1.20.0-3.el8.x86_64
wpa_supplicant-2.7-1.el8.x86_64
avahi-0.7-19.el8.x86_64
hypervkvpd-0-0.27.20180415git.el8.x86_64
radvd-2.17-12.el8.x86_64
rng-tools-6.6-2.el8.x86_64
cups-filters-1.20.0-18.el8.x86_64
nautilus-sendto-3.8.6-2.el8.x86_64
fwupd-1.1.4-1.el8.x86_64
ledmon-0.92-7.el8.x86_64
libquvi-0.9.4-12.el8.x86_64
strace-4.24-5.el8.x86_64
bind-export-libs-9.11.4-26.P2.el8.x86_64
sg3_utils-1.44-3.el8.x86_64
openssh-clients-8.0p1-3.el8.x86_64
rsync-3.1.3-6.el8.x86_64
iscsi-initiator-utils-iscsiuio-6.2.0.877-1.gitf71581b.el8.x86_64
time-1.9-3.el8.x86_64
google-noto-sans-mandaic-fonts-20161022-7.el8.noarch
python3-rhn-client-tools-2.8.16-13.module_el8.1.0+211+ad6c0bc7.x86_64
google-noto-sans-tai-tham-fonts-20161022-7.el8.noarch
python3-dnf-plugin-spacewalk-2.8.5-11.module_el8.1.0+211+ad6c0bc7.noarch
dos2unix-7.4.0-3.el8.x86_64
libsrtp-1.5.4-8.el8.x86_64
tree-1.7.0-15.el8.x86_64
nmap-ncat-7.70-5.el8.x86_64
NetworkManager-wwan-1.20.0-3.el8.x86_64
libgcc-8.3.1-4.5.el8.x86_64
unzip-6.0-41.el8.x86_64
util-linux-2.32.1-17.el8.x86_64
xkeyboard-config-2.24-3.el8.noarch
gdisk-1.0.3-6.el8.x86_64
grubby-8.40-37.el8.x86_64
abattis-cantarell-fonts-0.0.25-4.el8.noarch
daxctl-libs-65-1.el8.x86_64
glib2-2.56.4-7.el8.x86_64
cups-filesystem-2.2.6-28.el8.noarch
snappy-1.1.7-5.el8.x86_64
mozilla-filesystem-1.9-18.el8.x86_64
hunspell-en-US-0.20140811.1-12.el8.noarch
atk-2.28.1-1.el8.x86_64
geolite2-country-20180605-1.el8.noarch
libfontenc-1.1.3-8.el8.x86_64
platform-python-pip-9.0.3-15.el8.noarch
python3-pip-wheel-9.0.3-15.el8.noarch
woff2-1.0.2-4.el8.x86_64
json-glib-1.4.4-1.el8.x86_64
centos-repos-8.1-1.1911.0.8.el8.x86_64
libnfnetlink-1.0.1-13.el8.x86_64
libusbx-1.0.22-1.el8.x86_64
basesystem-11-5.el8.noarch
libpath_utils-0.2.1-39.el8.x86_64
gobject-introspection-1.56.1-1.el8.x86_64
liberation-sans-fonts-2.00.3-4.el8.noarch
sg3_utils-libs-1.44-3.el8.x86_64
python3-six-1.11.0-8.el8.noarch
khmeros-fonts-common-5.0-25.el8.noarch
dotconf-1.3-18.el8.x86_64
vim-filesystem-8.0.1763-13.el8.noarch
hyphen-2.8.8-9.el8.x86_64
gvfs-client-1.36.2-6.el8.x86_64
seabios-bin-1.11.1-4.module_el8.1.0+248+298dec18.noarch
sbc-1.3-9.el8.x86_64
python3-libselinux-2.9-2.1.el8.x86_64
man-pages-overrides-8.1.0.0-2.el8.noarch
zip-3.0-23.el8.x86_64
parted-3.2-38.el8.x86_64
hplip-common-3.18.4-9.el8.x86_64
xorg-x11-xauth-1.0.9-12.el8.x86_64
dconf-0.28.0-3.el8.x86_64
appstream-data-8-20190805.el8.noarch
libcdio-paranoia-10.2+0.94+2-3.el8.x86_64
glusterfs-libs-6.0-15.el8.x86_64
quota-nls-4.04-10.el8.noarch
libmpc-1.0.2-9.el8.x86_64
ibus-libs-1.5.19-4.el8.x86_64
pcre2-10.32-1.el8.x86_64
ipset-libs-7.1-1.el8.x86_64
policycoreutils-2.9-3.el8.x86_64
glibc-langpack-ja-2.28-72.el8.x86_64
libXres-1.2.0-4.el8.x86_64
python3-libxml2-2.9.7-5.el8.x86_64
libsepol-2.9-1.el8.x86_64
libxkbcommon-x11-0.8.2-1.el8.x86_64
enchant2-2.2.3-2.el8.x86_64
libgpg-error-1.31-1.el8.x86_64
lua-expat-1.3.0-12.el8.1.x86_64
dbus-x11-1.12.8-9.el8.x86_64
libxml2-2.9.7-5.el8.x86_64
bc-1.07.1-5.el8.x86_64
plymouth-0.9.3-15.el8.x86_64
perl-Exporter-5.72-396.el8.noarch
coreutils-common-8.30-6.el8.x86_64
sqlite-libs-3.26.0-3.el8.x86_64
liblouis-2.6.2-16.el8.x86_64
accountsservice-0.6.50-7.el8.x86_64
libjpeg-turbo-1.5.3-10.el8.x86_64
perl-Socket-2.027-3.el8.x86_64
rest-0.8.1-2.el8.x86_64
expat-2.2.5-3.el8.x86_64
perl-IO-1.38-416.el8.x86_64
geoclue2-libs-2.4.10-1.el8.x86_64
chkconfig-1.11-1.el8.x86_64
perl-threads-shared-1.58-2.el8.x86_64
usbredir-0.8.0-1.el8.x86_64
libICE-1.0.9-15.el8.x86_64
perl-Data-Dumper-2.167-399.el8.x86_64
libwayland-client-1.15.0-1.el8.x86_64
perl-Digest-MD5-2.55-396.el8.x86_64
libimobiledevice-1.2.0-16.el8.x86_64
keyutils-libs-1.5.10-6.el8.x86_64
perl-Pod-Escapes-1.07-395.el8.noarch
libgtop2-2.38.0-3.el8.x86_64
libxkbcommon-0.8.2-1.el8.x86_64
libconfig-1.5-9.el8.x86_64
xorg-x11-xinit-1.3.4-18.el8.x86_64
libicu-60.3-1.el8.x86_64
libvpx-1.7.0-6.el8.x86_64
dleyna-core-0.6.0-2.el8.x86_64
grep-3.1-6.el8.x86_64
less-530-1.el8.x86_64
libreport-plugin-reportuploader-2.9.5-9.el8.x86_64
libref_array-0.1.5-39.el8.x86_64
xdg-user-dirs-0.17-1.el8.x86_64
rpm-plugin-selinux-4.14.2-25.el8.x86_64
jansson-2.11-3.el8.x86_64
efivar-libs-36-1.el8.x86_64
GConf2-3.2.6-22.el8.x86_64
json-c-0.13.1-0.2.el8.x86_64
hdparm-9.54-2.el8.x86_64
libblockdev-loop-2.19-9.el8.x86_64
libXext-1.3.3-9.el8.x86_64
libpipeline-1.5.0-2.el8.x86_64
rtkit-0.11-19.el8.x86_64
libXcomposite-0.4.4-14.el8.x86_64
xorg-x11-font-utils-7.5-40.el8.x86_64
gnupg2-smime-2.2.9-1.el8.x86_64
libXinerama-1.1.4-1.el8.x86_64
gawk-4.2.1-1.el8.x86_64
ostree-libs-2019.2-1.el8.x86_64
libXcursor-1.1.15-3.el8.x86_64
libsss_sudo-2.2.0-19.el8.x86_64
libaio-0.3.112-1.el8.x86_64
lz4-1.8.1.2-4.el8.x86_64
python3-idna-2.5-5.el8.noarch
libmnl-1.0.4-6.el8.x86_64
libgxps-0.3.0-5.el8.x86_64
libidn2-2.2.0-1.el8.x86_64
jbigkit-libs-2.1-14.el8.x86_64
cronie-1.5.2-4.el8.x86_64
libpciaccess-0.14-1.el8.x86_64
libdatrie-0.2.9-7.el8.x86_64
at-spi2-core-2.28.0-1.el8.x86_64
libasyncns-0.8-14.el8.x86_64
libestr-0.1.10-1.el8.x86_64
libvirt-gconfig-2.0.0-1.el8.x86_64
libsemanage-2.9-1.el8.x86_64
libijs-0.35-5.el8.x86_64
net-snmp-libs-5.8-10.el8.x86_64
libplist-2.0.0-10.el8.x86_64
libmcpp-2.7.2-20.el8.x86_64
pciutils-3.5.6-4.el8.x86_64
p11-kit-trust-0.23.14-5.el8_0.x86_64
libmspack-0.7-0.1.alpha.el8.3.x86_64
device-mapper-multipath-libs-0.8.0-5.el8.x86_64
iptables-libs-1.8.2-16.el8.x86_64
mpg123-libs-1.25.10-2.el8.x86_64
bluez-libs-5.50-1.el8.x86_64
criu-3.12-9.el8.x86_64
libnfsidmap-2.3.3-26.el8.x86_64
libXdmcp-1.1.2-11.el8.x86_64
linux-firmware-20190516-94.git711d3297.el8.noarch
libbytesize-1.4-1.el8.x86_64
fuse-common-3.2.1-12.el8.x86_64
libibumad-22.3-1.el8.x86_64
flac-libs-1.3.2-9.el8.x86_64
dbus-common-1.12.8-9.el8.noarch
bind-libs-9.11.4-26.P2.el8.x86_64
xorg-x11-xkb-utils-7.7-27.el8.x86_64
libcurl-7.61.1-11.el8.x86_64
python3-pycparser-2.14-14.el8.noarch
libv4l-1.14.2-3.el8.x86_64
libdb-utils-5.3.28-37.el8.x86_64
cockpit-packagekit-197.3-1.el8.noarch
dmidecode-3.2-3.el8.x86_64
elfutils-libs-0.176-5.el8.x86_64
python3-librepo-1.10.3-3.el8.x86_64
libglvnd-1.0.1-0.9.git5baa1e5.el8.x86_64
procps-ng-3.3.15-1.el8.x86_64
pulseaudio-module-bluetooth-11.1-23.el8.x86_64
libglvnd-egl-1.0.1-0.9.git5baa1e5.el8.x86_64
kpartx-0.8.0-5.el8.x86_64
dleyna-connector-dbus-0.3.0-2.el8.x86_64
libglvnd-glx-1.0.1-0.9.git5baa1e5.el8.x86_64
grub2-tools-minimal-2.02-78.el8.x86_64
usbmuxd-1.1.0-13.el8.x86_64
boost-chrono-1.66.0-6.el8.x86_64
libmount-2.32.1-17.el8.x86_64
poppler-utils-0.66.0-26.el8.x86_64
libpsl-0.20.2-5.el8.x86_64
xorg-x11-server-Xorg-1.20.3-8.el8.x86_64
acl-2.2.53-1.el8.x86_64
libblockdev-lvm-2.19-9.el8.x86_64
startup-notification-0.12-15.el8.x86_64
kmod-libs-25-13.el8.x86_64
python3-unbound-1.7.3-8.el8.x86_64
llvm-libs-8.0.1-1.module_el8.1.0+215+a01033fb.x86_64
cryptsetup-libs-2.2.0-2.el8.x86_64
ModemManager-1.10.4-1.el8.x86_64
thai-scalable-waree-fonts-0.6.5-1.el8.noarch
centos-backgrounds-80.5-2.el8.noarch
google-noto-serif-cjk-ttc-fonts-20190416-1.el8.noarch
libvirt-gobject-2.0.0-1.el8.x86_64
dejavu-sans-mono-fonts-2.35-6.el8.noarch
libblockdev-kbd-2.19-9.el8.x86_64
xmlsec1-openssl-1.2.25-4.el8.x86_64
lohit-assamese-fonts-2.91.5-3.el8.noarch
python3-policycoreutils-2.9-3.el8.noarch
virt-what-1.18-6.el8.x86_64
lohit-gurmukhi-fonts-2.91.2-3.el8.noarch
python3-slip-0.6.4-11.el8.noarch
sssd-client-2.2.0-19.el8.x86_64
lohit-telugu-fonts-2.5.5-3.el8.noarch
libfprint-0.8.2-1.el8.0.1.x86_64
sssd-ad-2.2.0-19.el8.x86_64
sil-nuosu-fonts-2.1.1-14.el8.noarch
python3-configobj-5.0.6-11.el8.noarch
sssd-proxy-2.2.0-19.el8.x86_64
words-3.0-28.el8.noarch
python3-productmd-1.11-3.el8.noarch
authselect-compat-1.1-2.el8.x86_64
iwl7260-firmware-25.30.13.0-94.el8.1.noarch
libao-1.2.0-10.el8.x86_64
libluksmeta-9-2.el8.x86_64
iwl6000-firmware-9.221.4.1-94.el8.1.noarch
espeak-ng-1.49.2-4.el8.x86_64
perl-Encode-2.97-3.el8.x86_64
iwl3945-firmware-15.32.2.9-94.el8.1.noarch
cups-client-2.2.6-28.el8.x86_64
perl-Pod-Usage-1.69-395.el8.noarch
iwl135-firmware-18.168.6.1-94.el8.1.noarch
usb_modeswitch-2.5.2-1.el8.x86_64
perl-IO-Socket-SSL-2.066-3.el8.noarch
NetworkManager-config-server-1.20.0-3.el8.noarch
libstoragemgmt-1.8.1-2.el8.x86_64
e2fsprogs-1.44.6-3.el8.x86_64
systemd-pam-239-18.el8_1.1.x86_64
python3-pwquality-1.4.0-9.el8.x86_64
nss-util-3.44.0-9.el8_1.x86_64
python3-cairo-1.16.3-6.el8.x86_64
xdg-desktop-portal-1.0.3-1.el8.x86_64
samba-client-libs-4.10.4-101.el8_1.x86_64
python3-netifaces-0.10.6-4.el8.x86_64
gvfs-1.36.2-6.el8.x86_64
libvirt-daemon-driver-storage-core-4.5.0-35.1.module_el8.1.0+258+1d2a1d58.x86_64
python3-asn1crypto-0.24.0-3.el8.noarch
tracker-miners-2.1.5-1.el8.x86_64
python3-libdnf-0.35.1-9.el8_1.x86_64
python3-chardet-3.0.4-7.el8.noarch
totem-3.26.2-1.el8.x86_64
gnome-session-3.28.1-7.el8_1.x86_64
python3-kickstart-3.16.7-1.el8.noarch
xorg-x11-drv-wacom-serial-support-0.36.1-5.el8.x86_64
dracut-network-049-27.git20190906.el8_1.1.x86_64
python3-pip-9.0.3-15.el8.noarch
libcanberra-0.30-16.el8.x86_64
mesa-libGL-19.1.4-3.el8_1.x86_64
gom-0.3.3-5.el8.x86_64
gnome-bluetooth-3.28.2-2.el8.x86_64
libvirt-daemon-driver-storage-logical-4.5.0-35.1.module_el8.1.0+258+1d2a1d58.x86_64
python3-ntplib-0.3.3-10.el8.noarch
podman-1.4.2-5.module_el8.1.0+237+63e26edc.x86_64
libvirt-daemon-driver-storage-4.5.0-35.1.module_el8.1.0+258+1d2a1d58.x86_64
python3-speechd-0.8.8-6.el8.x86_64
gnome-control-center-3.28.2-5.el8.x86_64
nss-3.44.0-9.el8_1.x86_64
libXft-2.3.2-10.el8.x86_64
gnome-shell-extension-apps-menu-3.32.1-10.el8.noarch
qemu-kvm-block-gluster-2.12.0-88.module_el8.1.0+258+1d2a1d58.1.x86_64
gcr-3.28.0-1.el8.x86_64
gnome-shell-extension-places-menu-3.32.1-10.el8.noarch
libvirt-daemon-driver-interface-4.5.0-35.1.module_el8.1.0+258+1d2a1d58.x86_64
librsvg2-2.42.7-3.el8.x86_64
anaconda-tui-29.19.1.13-1.el8.x86_64
open-vm-tools-10.3.10-3.el8_1.1.x86_64
clutter-gst3-3.0.26-1.el8.x86_64
subscription-manager-initial-setup-addon-1.25.17-1.el8.x86_64
dnf-data-4.2.7-7.el8_1.noarch
nautilus-extensions-3.28.1-10.el8.x86_64
mesa-dri-drivers-19.1.4-3.el8_1.x86_64
libpeas-gtk-1.22.0-6.el8.x86_64
libvirt-daemon-kvm-4.5.0-35.1.module_el8.1.0+258+1d2a1d58.x86_64
colord-gtk-0.1.26-8.el8.x86_64
firefox-68.4.1-1.el8_1.x86_64
pangomm-2.40.1-5.el8.x86_64
gnome-classic-session-3.32.1-10.el8.noarch
gnome-session-wayland-session-3.28.1-7.el8_1.x86_64
libtimezonemap-0.4.5.1-3.el8.x86_64
cheese-3.28.0-1.el8.x86_64
libsmbclient-4.10.4-101.el8_1.x86_64
rsyslog-gnutls-8.37.0-13.el8.x86_64
sudo-1.8.25p1-8.el8_1.x86_64
usermode-gtk-1.113-1.el8.x86_64
cockpit-196.3-1.el8.x86_64
python3-perf-4.18.0-147.3.1.el8_1.x86_64
libgdata-0.17.9-2.el8.x86_64
gvfs-afc-1.36.2-6.el8.x86_64
binutils-2.30-58.el8.0.1.x86_64
anaconda-widgets-29.19.1.13-1.el8.x86_64
gvfs-gphoto2-1.36.2-6.el8.x86_64
flatpak-libs-1.0.9-1.el8_1.x86_64
gupnp-dlna-0.10.5-9.el8.x86_64
rasdaemon-0.6.1-2.el8.x86_64
sushi-3.28.3-1.el8.x86_64
ibus-1.5.19-4.el8.x86_64
gutenprint-cups-5.2.14-3.el8.x86_64
vino-3.22.0-10.el8.x86_64
plymouth-system-theme-0.9.3-15.el8.x86_64
plymouth-theme-charge-0.9.3-15.el8.x86_64
gnome-font-viewer-3.28.0-1.el8.x86_64
urw-base35-d050000l-fonts-20170801-10.el8.noarch
gnome-calculator-3.28.2-1.el8.x86_64
urw-base35-nimbus-sans-fonts-20170801-10.el8.noarch
baobab-3.28.0-2.el8.x86_64
urw-base35-fonts-20170801-10.el8.noarch
xdg-user-dirs-gtk-0.10-13.el8.x86_64
evince-libs-3.28.4-3.el8.x86_64
alsa-plugins-pulseaudio-1.1.9-1.el8.x86_64
libgsf-1.14.41-5.el8.x86_64
NetworkManager-bluetooth-1.20.0-3.el8.x86_64
cyrus-sasl-2.1.27-1.el8.x86_64
xorg-x11-drv-intel-2.99.917-38.20180618.el8.x86_64
lockdev-1.0.4-0.28.20111007git.el8.x86_64
kernel-4.18.0-147.el8.x86_64
sane-backends-1.0.27-19.el8.x86_64
libblockdev-mdraid-2.19-9.el8.x86_64
NetworkManager-adsl-1.20.0-3.el8.x86_64
NetworkManager-wifi-1.20.0-3.el8.x86_64
usbutils-010-3.el8.x86_64
hypervvssd-0-0.27.20180415git.el8.x86_64
mcelog-162-2.el8.x86_64
librelp-1.2.16-1.el8.x86_64
psacct-6.6.3-4.el8.x86_64
cups-2.2.6-28.el8.x86_64
irqbalance-1.4.0-4.el8.x86_64
libipa_hbac-2.2.0-19.el8.x86_64
totem-pl-parser-3.26.1-2.el8.x86_64
cyrus-sasl-plain-2.1.27-1.el8.x86_64
fipscheck-lib-1.5.0-4.el8.x86_64
xorg-x11-utils-7.5-28.el8.x86_64
gnome-keyring-3.28.2-1.el8.x86_64
nano-2.9.8-1.el8.x86_64
iscsi-initiator-utils-6.2.0.877-1.gitf71581b.el8.x86_64
ed-1.14.2-4.el8.x86_64
python3-libreport-2.9.5-9.el8.x86_64
google-noto-sans-lisu-fonts-20161022-7.el8.noarch
rhn-client-tools-2.8.16-13.module_el8.1.0+211+ad6c0bc7.x86_64
google-noto-sans-tagalog-fonts-20161022-7.el8.noarch
dnf-plugin-spacewalk-2.8.5-11.module_el8.1.0+211+ad6c0bc7.noarch
xorg-x11-xinit-session-1.3.4-18.el8.x86_64
gstreamer1-plugins-bad-free-1.14.0-5.el8.x86_64
symlinks-1.4-19.el8.x86_64
pam-1.3.1-4.el8.x86_64
smc-meera-fonts-6.1-10.el8.noarch
google-noto-fonts-common-20161022-7.el8.noarch
glusterfs-6.0-15.el8.x86_64
perl-Text-ParseWords-3.30-395.el8.noarch
libvirt-glib-2.0.0-1.el8.x86_64
grub2-tools-2.02-78.el8.x86_64
dejavu-serif-fonts-2.35-6.el8.noarch
gnome-control-center-filesystem-3.28.2-5.el8.noarch
libreport-cli-2.9.5-9.el8.x86_64
boost-atomic-1.66.0-6.el8.x86_64
gdk-pixbuf2-2.36.12-5.el8.x86_64
lohit-kannada-fonts-2.5.4-3.el8.noarch
google-noto-cjk-fonts-common-20190416-1.el8.noarch
python3-slip-dbus-0.6.4-11.el8.noarch
libXfont2-2.0.3-2.el8.x86_64
sssd-common-pac-2.2.0-19.el8.x86_64
python3-libs-3.6.8-15.1.el8.x86_64
sil-padauk-fonts-3.003-1.el8.noarch
centos-release-8.1-1.1911.0.8.el8.x86_64
python3-dateutil-2.6.1-6.el8.noarch
libnetfilter_conntrack-1.0.6-5.el8.x86_64
authselect-1.1-2.el8.x86_64
cups-libs-2.2.6-28.el8.x86_64
iwl6050-firmware-41.28.5.1-94.el8.1.noarch
liberation-mono-fonts-2.00.3-4.el8.noarch
libsamplerate-0.1.9-1.el8.x86_64
slang-2.3.2-3.el8.x86_64
perl-Mozilla-CA-20160104-7.el8.noarch
iwl3160-firmware-25.30.13.0-94.el8.1.noarch
vte-profile-0.52.2-2.el8.x86_64
cups-filters-libs-1.20.0-18.el8.x86_64
libevdev-1.5.9-5.el8.x86_64
perl-URI-1.73-3.el8.noarch
libsss_certmap-2.2.0-19.el8.x86_64
gpg-pubkey-8483c65d-5ccc5b19
python3-libstoragemgmt-clibs-1.8.1-2.el8.x86_64
libteam-1.28-4.el8.x86_64
avahi-glib-0.7-19.el8.x86_64
libmodulemd1-1.8.11-4.el8_1.x86_64
centos-indexhtml-8.0-0.el8.noarch
python3-gobject-3.28.3-1.el8.x86_64
libdvdnav-5.0.3-8.el8.x86_64
udisks2-2.8.3-2.el8.x86_64
libpeas-1.22.0-6.el8.x86_64
mesa-libglapi-19.1.4-3.el8_1.x86_64
ncurses-base-6.1-7.20180224.el8.noarch
python3-cryptography-2.3-2.el8.x86_64
ipset-7.1-1.el8.x86_64
grilo-plugins-0.3.8-1.el8.x86_64
libwacom-0.31-1.el8.x86_64
webkit2gtk3-jsc-2.24.4-2.el8_1.x86_64
bash-4.4.19-10.el8.x86_64
python3-requests-file-1.4.3-5.el8.noarch
netcf-libs-0.2.8-12.module_el8.1.0+248+298dec18.x86_64
sound-theme-freedesktop-0.8-9.el8.noarch
xmlrpc-c-1.51.0-5.el8.x86_64
libvirt-daemon-driver-storage-disk-4.5.0-35.1.module_el8.1.0+258+1d2a1d58.x86_64
xz-libs-5.2.4-3.el8.x86_64
python3-hwdata-2.3.6-3.el8.noarch
sqlite-3.26.0-3.el8.x86_64
oci-systemd-hook-0.1.15-2.git2d0b8a3.module_el8.1.0+237+63e26edc.x86_64
atkmm-2.24.2-6.el8.x86_64
nss-softokn-freebl-3.44.0-9.el8_1.x86_64
info-6.5-4.el8.x86_64
frei0r-plugins-1.6.1-6.el8.x86_64
perl-Term-ANSIColor-4.06-396.el8.noarch
gnome-shell-extension-common-3.32.1-10.el8.noarch
libsoup-2.62.3-1.el8.x86_64
qemu-kvm-block-iscsi-2.12.0-88.module_el8.1.0+258+1d2a1d58.1.x86_64
libnl3-3.4.0-5.el8.x86_64
cogl-1.22.2-10.el8.x86_64
perl-PathTools-3.74-1.el8.x86_64
python3-blivet-3.1.0-17.el8.noarch
colord-libs-1.4.2-1.el8.x86_64
systemd-container-239-18.el8_1.1.x86_64
elfutils-libelf-0.176-5.el8.x86_64
libnma-1.8.22-2.el8.x86_64
perl-Storable-3.11-3.el8.x86_64
nfs-utils-2.3.3-26.el8.x86_64
qemu-kvm-2.12.0-88.module_el8.1.0+258+1d2a1d58.1.x86_64
libSM-1.2.3-1.el8.x86_64
nm-connection-editor-1.8.22-2.el8.x86_64
perl-Term-Cap-1.17-395.el8.noarch
hicolor-icon-theme-0.17-2.el8.noarch
kexec-tools-2.0.19-12.el8_1.1.x86_64
libtevent-0.9.39-2.el8.x86_64
gtkmm30-3.22.2-2.el8.x86_64
soundtouch-2.0.0-2.el8.x86_64
cockpit-podman-4-1.module_el8.1.0+237+63e26edc.noarch
libreport-web-2.9.5-9.el8.x86_64
libvirt-daemon-config-network-4.5.0-35.1.module_el8.1.0+258+1d2a1d58.x86_64
libcollection-0.7.0-39.el8.x86_64
c-ares-1.13.0-5.el8.x86_64
xorg-x11-drv-wacom-0.36.1-5.el8.x86_64
harfbuzz-icu-1.7.5-3.el8.x86_64
hwdata-0.314-8.2.el8_1.noarch
augeas-libs-1.12.0-2.el8.x86_64
evolution-data-server-langpacks-3.28.5-11.el8.noarch
jimtcl-0.77-5.el8.x86_64
gvfs-goa-1.36.2-6.el8.x86_64
python3-pyparted-3.11.0-13.el8.x86_64
flatpak-1.0.9-1.el8_1.x86_64
libXdamage-1.1.4-14.el8.x86_64
libdmapsharing-2.9.37-5.el8.x86_64
libquvi-scripts-0.9.20131130-9.el8.noarch
librepo-1.10.3-3.el8.x86_64
libvorbis-1.3.6-2.el8.x86_64
keybinder3-0.3.2-4.el8.x86_64
libstemmer-0-10.585svn.el8.x86_64
libsane-hpaio-3.18.4-9.el8.x86_64
python3-audit-3.0-0.10.20180831git0047a6c.el8.x86_64
sed-4.5-1.el8.x86_64
libbluray-1.0.2-3.el8.x86_64
giflib-5.1.4-3.el8.x86_64
system-config-printer-udev-1.5.11-13.el8.x86_64
crontabs-1.11-16.20150630git.el8.noarch
fuse-libs-2.9.7-12.el8.x86_64
urw-base35-p052-fonts-20170801-10.el8.noarch
libthai-0.1.27-2.el8.x86_64
mousetweaks-3.12.0-11.el8.x86_64
libgexiv2-0.10.8-2.el8.x86_64
xz-5.2.4-3.el8.x86_64
evince-3.28.4-3.el8.x86_64
libiptcdata-1.0.4-21.el8.x86_64
pinfo-0.6.10-18.el8.x86_64
ndctl-libs-65-1.el8.x86_64
libtasn1-4.13-3.el8.x86_64
initscripts-10.00.4-1.el8.x86_64
libnet-1.1.6-15.el8.x86_64
xorg-x11-drv-vmware-13.2.1-8.el8.x86_64
xfsprogs-5.0.0-1.el8.x86_64
adwaita-icon-theme-3.28.0-2.el8.noarch
sane-backends-drivers-scanners-1.0.27-19.el8.x86_64
twolame-libs-0.3.13-11.el8.x86_64
PackageKit-gstreamer-plugin-1.1.12-3.el8.x86_64
openjpeg2-2.3.1-1.el8.x86_64
dnsmasq-2.79-6.el8.x86_64
fuse-2.9.7-12.el8.x86_64
at-3.1.20-11.el8.x86_64
jose-10-2.el8.x86_64
libxkbfile-1.0.9-9.el8.x86_64
libvncserver-0.9.11-9.el8.x86_64
libkcapi-1.1.1-16_1.el8.x86_64
bind-utils-9.11.4-26.P2.el8.x86_64
cpio-2.12-8.el8.x86_64
gupnp-av-0.12.10-6.el8.x86_64
gzip-1.9-9.el8.x86_64
man-db-2.7.6.1-17.el8.x86_64
libblockdev-crypto-2.19-9.el8.x86_64
fipscheck-1.5.0-4.el8.x86_64
device-mapper-1.02.163-5.el8.0.1.x86_64
biosdevname-0.7.3-2.el8.x86_64
usermode-1.113-1.el8.x86_64
lzop-1.03-20.el8.x86_64
rpm-plugin-systemd-inhibit-4.14.2-25.el8.x86_64
dbus-libs-1.12.8-9.el8.x86_64
hostname-3.20-6.el8.x86_64
xorg-x11-drv-vesa-2.4.0-3.el8.x86_64
groff-base-1.22.3-18.el8.x86_64
python3-dnf-plugins-core-4.0.8-3.el8.noarch
dbus-daemon-1.12.8-9.el8.x86_64
pnm2ppa-1.04-40.el8.x86_64
unbound-libs-1.7.3-8.el8.x86_64
lua-5.3.4-11.el8.x86_64
neon-0.30.2-6.el8.x86_64
gnome-getting-started-docs-3.28.2-1.el8.noarch
rpcbind-1.2.5-4.el8.x86_64
diffutils-3.6-5.el8.x86_64
trousers-lib-0.3.14-4.el8.x86_64
dejavu-fonts-common-2.35-6.el8.noarch
gnu-free-sans-fonts-20120503-18.el8.noarch
cups-pk-helper-0.2.6-5.el8.x86_64
sscg-2.3.3-6.el8.x86_64
e2fsprogs-libs-1.44.6-3.el8.x86_64
gnutls-3.6.8-8.el8.x86_64
libreport-filesystem-2.9.5-9.el8.x86_64
lohit-devanagari-fonts-2.95.4-3.el8.noarch
container-selinux-2.107-2.module_el8.1.0+237+63e26edc.noarch
rarian-compat-0.8.1-19.el8.x86_64
taglib-1.11.1-8.el8.x86_64
cairo-1.15.12-3.el8.x86_64
adobe-mappings-cmap-20171205-3.el8.noarch
paratype-pt-sans-fonts-20141121-6.el8.noarch
timedatex-0.5-3.el8.x86_64
sssd-krb5-2.2.0-19.el8.x86_64
libdaemon-0.14-15.el8.x86_64
polkit-libs-0.115-9.el8.x86_64
filesystem-3.8-2.el8.x86_64
mailcap-2.1.48-3.el8.noarch
brltty-5.6-28.el8.x86_64
libyaml-0.1.7-5.el8.x86_64
pulseaudio-libs-11.1-23.el8.x86_64
osinfo-db-20190611-1.el8.noarch
iwl5000-firmware-8.83.5.1_1-94.el8.1.noarch
speech-dispatcher-0.8.8-6.el8.x86_64
perl-Getopt-Long-2.50-4.el8.noarch
libsndfile-1.0.28-8.el8.x86_64
NetworkManager-libnm-1.20.0-3.el8.x86_64
sgabios-bin-0.20170427git-3.module_el8.1.0+248+298dec18.noarch
iwl1000-firmware-39.31.5.1-94.el8.1.noarch
libmtp-1.1.14-3.el8.x86_64
perl-DBI-1.641-3.module_el8.1.0+199+8f0a6bbd.x86_64
libshout-2.2.2-19.el8.x86_64
satyr-0.26-2.el8.x86_64
libX11-common-1.6.7-1.el8.noarch
libvirt-daemon-4.5.0-35.1.module_el8.1.0+258+1d2a1d58.x86_64
python3-schedutils-0.6-6.el8.x86_64
p11-kit-server-0.23.14-5.el8_0.x86_64
libavc1394-0.5.4-7.el8.x86_64
python3-dbus-1.2.4-15.el8.x86_64
adwaita-cursor-theme-3.28.0-2.el8.noarch
samba-common-libs-4.10.4-101.el8_1.x86_64
python3-pycurl-7.43.0.2-3.el8.x86_64
osinfo-db-tools-1.5.0-4.el8.x86_64
grub2-pc-modules-2.02-78.el8.noarch
desktop-file-utils-0.23-8.el8.x86_64
ncurses-libs-6.1-7.20180224.el8.x86_64
dracut-049-27.git20190906.el8_1.1.x86_64
python3-urllib3-1.24.2-2.el8.noarch
udisks2-lvm2-2.8.3-2.el8.x86_64
libdmx-1.1.4-3.el8.x86_64
bluez-5.50-1.el8.x86_64
libstdc++-8.3.1-4.5.el8.x86_64
python3-hawkey-0.35.1-9.el8_1.x86_64
python3-sssdconfig-2.2.0-19.el8.noarch
cheese-libs-3.28.0-1.el8.x86_64
lua-json-1.3.2-9.el8.noarch
plymouth-core-libs-0.9.3-15.el8.x86_64
libxcrypt-4.1.1-4.el8.x86_64
libvirt-daemon-driver-storage-rbd-4.5.0-35.1.module_el8.1.0+258+1d2a1d58.x86_64
python3-pytz-2017.2-9.el8.noarch
colord-1.4.2-1.el8.x86_64
aspell-0.60.6.1-21.el8.x86_64
librados2-12.2.7-9.el8.x86_64
libcap-ng-0.7.9-4.el8.x86_64
qemu-kvm-core-2.12.0-88.module_el8.1.0+258+1d2a1d58.1.x86_64
gtk3-3.22.30-4.el8.x86_64
gnome-shell-extension-horizontal-workspaces-3.32.1-10.el8.noarch
perl-Unicode-Normalize-1.25-396.el8.x86_64
cockpit-bridge-196.3-1.el8.x86_64
readline-7.0-10.el8.x86_64
libvirt-daemon-driver-nwfilter-4.5.0-35.1.module_el8.1.0+258+1d2a1d58.x86_64
pipewire-libs-0.2.5-1.el8.x86_64
anaconda-gui-29.19.1.13-1.el8.x86_64
perl-MIME-Base64-3.15-396.el8.x86_64
kernel-core-4.18.0-147.el8.x86_64
libffi-3.1-21.el8.x86_64
dnf-4.2.7-7.el8_1.noarch
gtksourceview3-3.24.9-1.el8.x86_64
perl-Math-Complex-1.59-416.el8.noarch
lcms2-2.9-2.el8.x86_64
kernel-tools-4.18.0-147.3.1.el8_1.x86_64
system-config-printer-libs-1.5.11-13.el8.noarch
libproxy-0.4.15-5.2.el8.x86_64
gssdp-1.0.2-6.el8.x86_64
libtool-ltdl-2.4.6-25.el8.x86_64
dracut-config-rescue-049-27.git20190906.el8_1.1.x86_64
gnome-themes-standard-3.22.3-4.el8.x86_64
gnome-disk-utility-3.28.3-2.el8.x86_64
redhat-menus-12.0.2-12.el8.noarch
python3-dmidecode-3.12.2-15.el8.x86_64
perl-Scalar-List-Utils-1.49-2.el8.x86_64
setup-2.12.2-2.el8_1.1.noarch
evince-nautilus-3.28.4-3.el8.x86_64
fuse-overlayfs-0.4.1-1.module_el8.1.0+237+63e26edc.x86_64
python3-blockdev-2.19-9.el8.x86_64
libxcb-1.13-5.el8.x86_64
mesa-libxatracker-19.1.4-3.el8_1.x86_64
yelp-3.28.1-3.el8.x86_64
gvfs-smb-1.36.2-6.el8.x86_64
pkgconf-1.4.2-1.el8.x86_64
python3-pyudev-0.21.0-7.el8.noarch
libXrandr-1.5.1-7.el8.x86_64
ibus-gtk3-1.5.19-4.el8.x86_64
openssh-server-8.0p1-3.el8.x86_64
libsss_autofs-2.2.0-19.el8.x86_64
PackageKit-1.1.12-3.el8.x86_64
libsigc++20-2.10.0-5.el8.x86_64
plymouth-plugin-label-0.9.3-15.el8.x86_64
orca-3.28.2-1.el8.noarch
npth-1.5-4.el8.x86_64
python3-syspurpose-1.25.17-1.el8.x86_64
nettle-3.4.1-1.el8.x86_64
urw-base35-nimbus-mono-ps-fonts-20170801-10.el8.noarch
lame-libs-3.100-6.el8.x86_64
iputils-20180629-2.el8.x86_64
vdo-6.2.1.134-11.el8.x86_64
libgdither-0.6-17.el8.x86_64
containers-common-0.1.37-5.module_el8.1.0+237+63e26edc.x86_64
bubblewrap-0.3.0-1.el8.x86_64
audit-3.0-0.10.20180831git0047a6c.el8.x86_64
xorg-x11-drv-ati-19.0.1-1.el8.x86_64
xorg-x11-server-utils-7.7-27.el8.x86_64
libibverbs-22.3-1.el8.x86_64
libxshmfence-1.3-2.el8.x86_64
sane-backends-drivers-cameras-1.0.27-19.el8.x86_64
xfsdump-3.1.8-2.el8.x86_64
pakchois-0.4-17.el8.x86_64
teamd-1.28-4.el8.x86_64
libsmartcols-2.32.1-17.el8.x86_64
alsa-ucm-1.1.9-4.el8.noarch
kbd-misc-2.0.4-8.el8.noarch
libiscsi-1.18.0-8.module_el8.1.0+248+298dec18.x86_64
tar-1.30-4.el8.x86_64
oddjob-mkhomedir-0.34.4-7.el8.x86_64
mlocate-0.26-20.el8.x86_64
libssh-0.9.0-4.el8.x86_64
python3-rpm-4.14.2-25.el8.x86_64
exiv2-0.26-10.el8.x86_64
libgcab1-1.1-1.el8.x86_64
tcpdump-4.9.2-5.el8.x86_64
openssl-1.1.1c-2.el8.x86_64
pciutils-libs-3.5.6-4.el8.x86_64
grub2-tools-extra-2.02-78.el8.x86_64
bash-completion-2.7-5.el8.noarch
libtirpc-1.1.4-4.el8.x86_64
libreport-plugin-rhtsupport-2.9.5-9.el8.x86_64
libglvnd-gles-1.0.1-0.9.git5baa1e5.el8.x86_64
isns-utils-libs-0.99-1.el8.x86_64
libcroco-0.6.12-4.el8.x86_64
kmod-kvdo-6.2.1.138-57.el8.x86_64
boost-thread-1.66.0-6.el8.x86_64
python3-meh-gui-0.47.2-1.el8.noarch
google-noto-sans-meetei-mayek-fonts-20161022-7.el8.noarch
libblkid-2.32.1-17.el8.x86_64
lvm2-libs-2.03.05-5.el8.0.1.x86_64
libXxf86misc-1.0.4-1.el8.x86_64
clevis-11-2.el8.x86_64
lsscsi-0.30-1.el8.x86_64
libpwquality-1.4.0-9.el8.x86_64
itstool-2.0.4-2.el8.noarch
libmetalink-0.1.3-7.el8.x86_64
</pre>
</div>
</details>
{{< /accordion >}}

## 2.dnfコマンド

引き続きrootユーザで作業します。

1.dnfコマンドでhttpdのパッケージを検索してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
# dnf search httpd
  メタデータの期限切れの最終確認: 0:04:45 時間前の 2020年02月02日 23時38分17秒 に実施しました。
  =================================================================== 名前 完全一致: httpd ====================================================================
  httpd.x86_64 : Apache HTTP Server
  ================================================================== 名前 & 概要 一致: httpd ==================================================================
  centos-logos-httpd.noarch : CentOS-related icons and pictures used by httpd
  keycloak-httpd-client-install.noarch : Tools to configure Apache HTTPD as Keycloak client
  python3-keycloak-httpd-client-install.noarch : Tools to configure Apache HTTPD as Keycloak client
  ===================================================================== 名前 一致: httpd ======================================================================
  httpd-devel.x86_64 : Development interfaces for the Apache HTTP server
  httpd-tools.x86_64 : Tools for use with the Apache HTTP Server
  httpd-manual.noarch : Documentation for the Apache HTTP server
  libmicrohttpd.i686 : Lightweight library for embedding a webserver in applications
  libmicrohttpd.x86_64 : Lightweight library for embedding a webserver in applications
  httpd-filesystem.noarch : The basic directory layout for the Apache HTTP server
  ===================================================================== 概要 一致: httpd ======================================================================
  mod_dav_svn.x86_64 : Apache httpd module for Subversion server
  mod_auth_mellon.x86_64 : A SAML 2.0 authentication module for the Apache Httpd Server
</pre>
</div>
</details>
{{< /accordion >}}

2.dnfコマンドでhttpdパッケージの詳細情報を確認してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
# dnf info httpd
  メタデータの期限切れの最終確認: 0:10:37 時間前の 2020年02月02日 23時38分17秒 に実施しました。
  利用可能なパッケージ
  名前         : httpd
  バージョン   : 2.4.37
  リリース     : 16.module_el8.1.0+256+ae790463
  Arch         : x86_64
  サイズ       : 1.7 M
  ソース       : httpd-2.4.37-16.module_el8.1.0+256+ae790463.src.rpm
  リポジトリー : AppStream
  概要         : Apache HTTP Server
  URL          : https://httpd.apache.org/
  ライセンス   : ASL 2.0
  説明         : The Apache HTTP Server is a powerful, efficient, and extensible
               : web server.
</pre>
</div>
</details>
{{< /accordion >}}

3.dnfコマンドでOS内にインストールされているパッケージを確認してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
# dnf list installed
モジュラーの依存に関する問題:

 問題 1: conflicting requests
  - nothing provides module(perl:5.26) needed by module perl-DBD-SQLite:1.58:8010020191114033549:073fa5fe-0.x86_64
 問題 2: conflicting requests
  - nothing provides module(perl:5.26) needed by module perl-DBI:1.641:8010020191113222731:16b3ab4d-0.x86_64
インストール済みパッケージ
GConf2.x86_64                                                             3.2.6-22.el8                                                             @AppStream
ModemManager.x86_64                                                       1.10.4-1.el8                                                             @anaconda
ModemManager-glib.x86_64                                                  1.10.4-1.el8                                                             @anaconda
NetworkManager.x86_64                                                     1:1.20.0-3.el8                                                           @anaconda
NetworkManager-adsl.x86_64                                                1:1.20.0-3.el8                                                           @anaconda
NetworkManager-bluetooth.x86_64                                           1:1.20.0-3.el8                                                           @anaconda
NetworkManager-config-server.noarch                                       1:1.20.0-3.el8                                                           @anaconda
NetworkManager-libnm.x86_64                                               1:1.20.0-3.el8                                                           @anaconda
NetworkManager-team.x86_64                                                1:1.20.0-3.el8                                                           @anaconda
NetworkManager-tui.x86_64                                                 1:1.20.0-3.el8                                                           @anaconda
NetworkManager-wifi.x86_64                                                1:1.20.0-3.el8                                                           @anaconda
NetworkManager-wwan.x86_64                                                1:1.20.0-3.el8                                                           @anaconda
PackageKit.x86_64                                                         1.1.12-3.el8                                                             @AppStream
PackageKit-command-not-found.x86_64                                       1.1.12-3.el8                                                             @AppStream
PackageKit-glib.x86_64                                                    1.1.12-3.el8                                                             @AppStream
PackageKit-gstreamer-plugin.x86_64                                        1.1.12-3.el8                                                             @AppStream
PackageKit-gtk3-module.x86_64                                             1.1.12-3.el8                                                             @AppStream
abattis-cantarell-fonts.noarch                                            0.0.25-4.el8                                                             @AppStream
accountsservice.x86_64                                                    0.6.50-7.el8                                                             @AppStream
accountsservice-libs.x86_64                                               0.6.50-7.el8                                                             @AppStream
acl.x86_64                                                                2.2.53-1.el8                                                             @anaconda
adcli.x86_64                                                              0.8.2-3.el8                                                              @anaconda
adobe-mappings-cmap.noarch                                                20171205-3.el8                                                           @AppStream
adobe-mappings-cmap-deprecated.noarch                                     20171205-3.el8                                                           @AppStream
adobe-mappings-pdf.noarch                                                 20180407-1.el8                                                           @AppStream
adwaita-cursor-theme.noarch                                               3.28.0-2.el8                                                             @AppStream
adwaita-gtk2-theme.x86_64                                                 3.22.3-4.el8                                                             @AppStream
adwaita-icon-theme.noarch                                                 3.28.0-2.el8                                                             @AppStream
alsa-lib.x86_64                                                           1.1.9-4.el8                                                              @AppStream
alsa-plugins-pulseaudio.x86_64                                            1.1.9-1.el8                                                              @AppStream
alsa-ucm.noarch                                                           1.1.9-4.el8                                                              @AppStream
alsa-utils.x86_64                                                         1.1.9-1.el8                                                              @AppStream
anaconda-core.x86_64                                                      29.19.1.13-1.el8                                                         @AppStream
anaconda-gui.x86_64                                                       29.19.1.13-1.el8                                                         @AppStream
anaconda-tui.x86_64                                                       29.19.1.13-1.el8                                                         @AppStream
anaconda-user-help.noarch                                                 1:8.1.1-1.el8                                                            @AppStream
anaconda-widgets.x86_64                                                   29.19.1.13-1.el8                                                         @AppStream
appstream-data.noarch                                                     8-20190805.el8                                                           @AppStream
aspell.x86_64                                                             12:0.60.6.1-21.el8                                                       @AppStream
at.x86_64                                                                 3.1.20-11.el8                                                            @anaconda
at-spi2-atk.x86_64                                                        2.26.2-1.el8                                                             @AppStream
at-spi2-core.x86_64                                                       2.28.0-1.el8                                                             @AppStream
atk.x86_64                                                                2.28.1-1.el8                                                             @AppStream
atkmm.x86_64                                                              2.24.2-6.el8                                                             @AppStream
attr.x86_64                                                               2.4.48-3.el8                                                             @anaconda
audit.x86_64                                                              3.0-0.10.20180831git0047a6c.el8                                          @anaconda
audit-libs.x86_64                                                         3.0-0.10.20180831git0047a6c.el8                                          @anaconda
augeas-libs.x86_64                                                        1.12.0-2.el8                                                             @anaconda
authselect.x86_64                                                         1.1-2.el8                                                                @anaconda
authselect-compat.x86_64                                                  1.1-2.el8                                                                @AppStream
authselect-libs.x86_64                                                    1.1-2.el8                                                                @anaconda
avahi.x86_64                                                              0.7-19.el8                                                               @anaconda
avahi-glib.x86_64                                                         0.7-19.el8                                                               @anaconda
avahi-libs.x86_64                                                         0.7-19.el8                                                               @anaconda
baobab.x86_64                                                             3.28.0-2.el8                                                             @AppStream
basesystem.noarch                                                         11-5.el8                                                                 @anaconda
bash.x86_64                                                               4.4.19-10.el8                                                            @anaconda
bash-completion.noarch                                                    1:2.7-5.el8                                                              @anaconda
bc.x86_64                                                                 1.07.1-5.el8                                                             @anaconda
bind-export-libs.x86_64                                                   32:9.11.4-26.P2.el8                                                      @anaconda
bind-libs.x86_64                                                          32:9.11.4-26.P2.el8                                                      @AppStream
bind-libs-lite.x86_64                                                     32:9.11.4-26.P2.el8                                                      @AppStream
bind-license.noarch                                                       32:9.11.4-26.P2.el8                                                      @AppStream
bind-utils.x86_64                                                         32:9.11.4-26.P2.el8                                                      @AppStream
binutils.x86_64                                                           2.30-58.el8.0.1                                                          @BaseOS
biosdevname.x86_64                                                        0.7.3-2.el8                                                              @anaconda
blivet-data.noarch                                                        1:3.1.0-17.el8                                                           @AppStream
blktrace.x86_64                                                           1.2.0-10.el8                                                             @anaconda
bluez.x86_64                                                              5.50-1.el8                                                               @anaconda
bluez-libs.x86_64                                                         5.50-1.el8                                                               @anaconda
bluez-obexd.x86_64                                                        5.50-1.el8                                                               @anaconda
bolt.x86_64                                                               0.8-2.el8                                                                @anaconda
boost-atomic.x86_64                                                       1.66.0-6.el8                                                             @AppStream
boost-chrono.x86_64                                                       1.66.0-6.el8                                                             @AppStream
boost-date-time.x86_64                                                    1.66.0-6.el8                                                             @AppStream
boost-iostreams.x86_64                                                    1.66.0-6.el8                                                             @AppStream
boost-program-options.x86_64                                              1.66.0-6.el8                                                             @AppStream
boost-random.x86_64                                                       1.66.0-6.el8                                                             @AppStream
boost-regex.x86_64                                                        1.66.0-6.el8                                                             @AppStream
boost-system.x86_64                                                       1.66.0-6.el8                                                             @AppStream
boost-thread.x86_64                                                       1.66.0-6.el8                                                             @AppStream
bpftool.x86_64                                                            4.18.0-147.3.1.el8_1                                                     @BaseOS
brlapi.x86_64                                                             0.6.7-28.el8                                                             @AppStream
brltty.x86_64                                                             5.6-28.el8                                                               @AppStream
brotli.x86_64                                                             1.0.6-1.el8                                                              @anaconda
bubblewrap.x86_64                                                         0.3.0-1.el8                                                              @anaconda
buildah.x86_64                                                            1.9.0-5.module_el8.1.0+237+63e26edc                                      @AppStream
bzip2.x86_64                                                              1.0.6-26.el8                                                             @anaconda
bzip2-libs.x86_64                                                         1.0.6-26.el8                                                             @anaconda
c-ares.x86_64                                                             1.13.0-5.el8                                                             @anaconda
ca-certificates.noarch                                                    2019.2.32-80.0.el8_1                                                     @BaseOS
cairo.x86_64                                                              1.15.12-3.el8                                                            @AppStream
cairo-gobject.x86_64                                                      1.15.12-3.el8                                                            @AppStream
cairomm.x86_64                                                            1.12.0-7.el8                                                             @AppStream
celt051.x86_64                                                            0.5.1.3-15.el8                                                           @AppStream
centos-backgrounds.noarch                                                 80.5-2.el8                                                               @AppStream
centos-gpg-keys.noarch                                                    8.1-1.1911.0.8.el8                                                       @anaconda
centos-indexhtml.noarch                                                   8.0-0.el8                                                                @AppStream
centos-logos.x86_64                                                       80.5-2.el8                                                               @AppStream
centos-release.x86_64                                                     8.1-1.1911.0.8.el8                                                       @anaconda
centos-repos.x86_64                                                       8.1-1.1911.0.8.el8                                                       @anaconda
checkpolicy.x86_64                                                        2.9-1.el8                                                                @anaconda
cheese.x86_64                                                             2:3.28.0-1.el8                                                           @AppStream
cheese-libs.x86_64                                                        2:3.28.0-1.el8                                                           @AppStream
chkconfig.x86_64                                                          1.11-1.el8                                                               @anaconda
chrome-gnome-shell.x86_64                                                 10.1-6.el8                                                               @AppStream
chrony.x86_64                                                             3.5-1.el8                                                                @anaconda
clevis.x86_64                                                             11-2.el8                                                                 @AppStream
clevis-luks.x86_64                                                        11-2.el8                                                                 @AppStream
clutter.x86_64                                                            1.26.2-6.el8                                                             @AppStream
clutter-gst3.x86_64                                                       3.0.26-1.el8                                                             @AppStream
clutter-gtk.x86_64                                                        1.8.4-3.el8                                                              @AppStream
cockpit.x86_64                                                            196.3-1.el8                                                              @anaconda
cockpit-bridge.x86_64                                                     196.3-1.el8                                                              @anaconda
cockpit-packagekit.noarch                                                 197.3-1.el8                                                              @AppStream
cockpit-podman.noarch                                                     4-1.module_el8.1.0+237+63e26edc                                          @AppStream
cockpit-storaged.noarch                                                   197.3-1.el8                                                              @AppStream
cockpit-system.noarch                                                     196.3-1.el8                                                              @anaconda
cockpit-ws.x86_64                                                         196.3-1.el8                                                              @anaconda
cogl.x86_64                                                               1.22.2-10.el8                                                            @AppStream
color-filesystem.noarch                                                   1-20.el8                                                                 @AppStream
colord.x86_64                                                             1.4.2-1.el8                                                              @AppStream
colord-gtk.x86_64                                                         0.1.26-8.el8                                                             @AppStream
colord-libs.x86_64                                                        1.4.2-1.el8                                                              @AppStream
container-selinux.noarch                                                  2:2.107-2.module_el8.1.0+237+63e26edc                                    @AppStream
containernetworking-plugins.x86_64                                        0.8.1-2.module_el8.1.0+237+63e26edc                                      @AppStream
containers-common.x86_64                                                  1:0.1.37-5.module_el8.1.0+237+63e26edc                                   @AppStream
coreutils.x86_64                                                          8.30-6.el8                                                               @anaconda
coreutils-common.x86_64                                                   8.30-6.el8                                                               @anaconda
cpio.x86_64                                                               2.12-8.el8                                                               @anaconda
cracklib.x86_64                                                           2.9.6-15.el8                                                             @anaconda
cracklib-dicts.x86_64                                                     2.9.6-15.el8                                                             @anaconda
criu.x86_64                                                               3.12-9.el8                                                               @AppStream
cronie.x86_64                                                             1.5.2-4.el8                                                              @anaconda
cronie-anacron.x86_64                                                     1.5.2-4.el8                                                              @anaconda
crontabs.noarch                                                           1.11-16.20150630git.el8                                                  @anaconda
crypto-policies.noarch                                                    20190807-1.git9b1477b.el8                                                @anaconda
cryptsetup.x86_64                                                         2.2.0-2.el8                                                              @anaconda
cryptsetup-libs.x86_64                                                    2.2.0-2.el8                                                              @anaconda
cups.x86_64                                                               1:2.2.6-28.el8                                                           @AppStream
cups-client.x86_64                                                        1:2.2.6-28.el8                                                           @AppStream
cups-filesystem.noarch                                                    1:2.2.6-28.el8                                                           @AppStream
cups-filters.x86_64                                                       1.20.0-18.el8                                                            @AppStream
cups-filters-libs.x86_64                                                  1.20.0-18.el8                                                            @AppStream
cups-libs.x86_64                                                          1:2.2.6-28.el8                                                           @anaconda
cups-pk-helper.x86_64                                                     0.2.6-5.el8                                                              @AppStream
curl.x86_64                                                               7.61.1-11.el8                                                            @anaconda
cyrus-sasl.x86_64                                                         2.1.27-1.el8                                                             @anaconda
cyrus-sasl-gssapi.x86_64                                                  2.1.27-1.el8                                                             @anaconda
cyrus-sasl-lib.x86_64                                                     2.1.27-1.el8                                                             @anaconda
cyrus-sasl-plain.x86_64                                                   2.1.27-1.el8                                                             @anaconda
daxctl-libs.x86_64                                                        65-1.el8                                                                 @anaconda
dbus.x86_64                                                               1:1.12.8-9.el8                                                           @anaconda
dbus-common.noarch                                                        1:1.12.8-9.el8                                                           @anaconda
dbus-daemon.x86_64                                                        1:1.12.8-9.el8                                                           @anaconda
dbus-glib.x86_64                                                          0.110-2.el8                                                              @anaconda
dbus-libs.x86_64                                                          1:1.12.8-9.el8                                                           @anaconda
dbus-tools.x86_64                                                         1:1.12.8-9.el8                                                           @anaconda
dbus-x11.x86_64                                                           1:1.12.8-9.el8                                                           @AppStream
dconf.x86_64                                                              0.28.0-3.el8                                                             @AppStream
dejavu-fonts-common.noarch                                                2.35-6.el8                                                               @anaconda
dejavu-sans-fonts.noarch                                                  2.35-6.el8                                                               @anaconda
dejavu-sans-mono-fonts.noarch                                             2.35-6.el8                                                               @anaconda
dejavu-serif-fonts.noarch                                                 2.35-6.el8                                                               @anaconda
desktop-file-utils.x86_64                                                 0.23-8.el8                                                               @AppStream
device-mapper.x86_64                                                      8:1.02.163-5.el8.0.1                                                     @anaconda
device-mapper-event.x86_64                                                8:1.02.163-5.el8.0.1                                                     @anaconda
device-mapper-event-libs.x86_64                                           8:1.02.163-5.el8.0.1                                                     @anaconda
device-mapper-libs.x86_64                                                 8:1.02.163-5.el8.0.1                                                     @anaconda
device-mapper-multipath.x86_64                                            0.8.0-5.el8                                                              @anaconda
device-mapper-multipath-libs.x86_64                                       0.8.0-5.el8                                                              @anaconda
device-mapper-persistent-data.x86_64                                      0.8.5-2.el8                                                              @anaconda
dhcp-client.x86_64                                                        12:4.3.6-34.el8                                                          @anaconda
dhcp-common.noarch                                                        12:4.3.6-34.el8                                                          @anaconda
dhcp-libs.x86_64                                                          12:4.3.6-34.el8                                                          @anaconda
diffutils.x86_64                                                          3.6-5.el8                                                                @anaconda
dleyna-connector-dbus.x86_64                                              0.3.0-2.el8                                                              @AppStream
dleyna-core.x86_64                                                        0.6.0-2.el8                                                              @AppStream
dleyna-server.x86_64                                                      0.6.0-2.el8                                                              @AppStream
dmidecode.x86_64                                                          1:3.2-3.el8                                                              @anaconda
dnf.noarch                                                                4.2.7-7.el8_1                                                            @BaseOS
dnf-data.noarch                                                           4.2.7-7.el8_1                                                            @BaseOS
dnf-plugin-spacewalk.noarch                                               2.8.5-11.module_el8.1.0+211+ad6c0bc7                                     @AppStream
dnf-plugins-core.noarch                                                   4.0.8-3.el8                                                              @anaconda
dnsmasq.x86_64                                                            2.79-6.el8                                                               @AppStream
dos2unix.x86_64                                                           7.4.0-3.el8                                                              @anaconda
dosfstools.x86_64                                                         4.1-6.el8                                                                @anaconda
dotconf.x86_64                                                            1.3-18.el8                                                               @AppStream
dracut.x86_64                                                             049-27.git20190906.el8_1.1                                               @BaseOS
dracut-config-rescue.x86_64                                               049-27.git20190906.el8_1.1                                               @BaseOS
dracut-network.x86_64                                                     049-27.git20190906.el8_1.1                                               @BaseOS
dracut-squash.x86_64                                                      049-27.git20190906.el8_1.1                                               @BaseOS
e2fsprogs.x86_64                                                          1.44.6-3.el8                                                             @anaconda
e2fsprogs-libs.x86_64                                                     1.44.6-3.el8                                                             @anaconda
ed.x86_64                                                                 1.14.2-4.el8                                                             @anaconda
edk2-ovmf.noarch                                                          20190308git89910a39dcfd-6.el8                                            @AppStream
efivar-libs.x86_64                                                        36-1.el8                                                                 @anaconda
elfutils-default-yama-scope.noarch                                        0.176-5.el8                                                              @anaconda
elfutils-libelf.x86_64                                                    0.176-5.el8                                                              @anaconda
elfutils-libs.x86_64                                                      0.176-5.el8                                                              @anaconda
emacs-filesystem.noarch                                                   1:26.1-5.el8                                                             @anaconda
enchant2.x86_64                                                           2.2.3-2.el8                                                              @AppStream
enscript.x86_64                                                           1.6.6-17.el8                                                             @AppStream
eog.x86_64                                                                3.28.4-1.el8                                                             @AppStream
espeak-ng.x86_64                                                          1.49.2-4.el8                                                             @AppStream
ethtool.x86_64                                                            2:5.0-2.el8                                                              @anaconda
evince.x86_64                                                             3.28.4-3.el8                                                             @AppStream
evince-libs.x86_64                                                        3.28.4-3.el8                                                             @AppStream
evince-nautilus.x86_64                                                    3.28.4-3.el8                                                             @AppStream
evolution-data-server.x86_64                                              3.28.5-11.el8                                                            @AppStream
evolution-data-server-langpacks.noarch                                    3.28.5-11.el8                                                            @AppStream
exempi.x86_64                                                             2.4.5-2.el8                                                              @AppStream
exiv2.x86_64                                                              0.26-10.el8                                                              @AppStream
exiv2-libs.x86_64                                                         0.26-10.el8                                                              @AppStream
expat.x86_64                                                              2.2.5-3.el8                                                              @anaconda
file.x86_64                                                               5.33-8.el8                                                               @anaconda
file-libs.x86_64                                                          5.33-8.el8                                                               @anaconda
file-roller.x86_64                                                        3.28.1-2.el8                                                             @AppStream
filesystem.x86_64                                                         3.8-2.el8                                                                @anaconda
findutils.x86_64                                                          1:4.6.0-20.el8                                                           @anaconda
fipscheck.x86_64                                                          1.5.0-4.el8                                                              @anaconda
fipscheck-lib.x86_64                                                      1.5.0-4.el8                                                              @anaconda
firefox.x86_64                                                            68.4.1-1.el8_1                                                           @AppStream
firewalld.noarch                                                          0.7.0-5.el8                                                              @anaconda
firewalld-filesystem.noarch                                               0.7.0-5.el8                                                              @anaconda
flac-libs.x86_64                                                          1.3.2-9.el8                                                              @AppStream
flatpak.x86_64                                                            1.0.9-1.el8_1                                                            @AppStream
flatpak-libs.x86_64                                                       1.0.9-1.el8_1                                                            @AppStream
fontconfig.x86_64                                                         2.13.1-3.el8                                                             @anaconda
fontpackages-filesystem.noarch                                            1.44-22.el8                                                              @anaconda
fprintd.x86_64                                                            0.8.1-2.el8                                                              @AppStream
fprintd-pam.x86_64                                                        0.8.1-2.el8                                                              @AppStream
freetype.x86_64                                                           2.9.1-4.el8                                                              @anaconda
frei0r-plugins.x86_64                                                     1.6.1-6.el8                                                              @AppStream
fribidi.x86_64                                                            1.0.4-7.el8_1                                                            @AppStream
fuse.x86_64                                                               2.9.7-12.el8                                                             @anaconda
fuse-common.x86_64                                                        3.2.1-12.el8                                                             @anaconda
fuse-libs.x86_64                                                          2.9.7-12.el8                                                             @anaconda
fuse-overlayfs.x86_64                                                     0.4.1-1.module_el8.1.0+237+63e26edc                                      @AppStream
fuse3-libs.x86_64                                                         3.2.1-12.el8                                                             @anaconda
fwupd.x86_64                                                              1.1.4-1.el8                                                              @anaconda
gavl.x86_64                                                               1.4.0-12.el8                                                             @AppStream
gawk.x86_64                                                               4.2.1-1.el8                                                              @anaconda
gcr.x86_64                                                                3.28.0-1.el8                                                             @AppStream
gd.x86_64                                                                 2.2.5-6.el8                                                              @AppStream
gdbm.x86_64                                                               1:1.18-1.el8                                                             @anaconda
gdbm-libs.x86_64                                                          1:1.18-1.el8                                                             @anaconda
gdisk.x86_64                                                              1.0.3-6.el8                                                              @anaconda
gdk-pixbuf2.x86_64                                                        2.36.12-5.el8                                                            @anaconda
gdk-pixbuf2-modules.x86_64                                                2.36.12-5.el8                                                            @AppStream
gdm.x86_64                                                                1:3.28.3-22.el8                                                          @AppStream
gedit.x86_64                                                              2:3.28.1-3.el8                                                           @AppStream
genisoimage.x86_64                                                        1.1.11-39.el8                                                            @AppStream
geoclue2.x86_64                                                           2.4.10-1.el8                                                             @AppStream
geoclue2-libs.x86_64                                                      2.4.10-1.el8                                                             @AppStream
geocode-glib.x86_64                                                       3.26.0-1.el8                                                             @AppStream
geolite2-city.noarch                                                      20180605-1.el8                                                           @AppStream
geolite2-country.noarch                                                   20180605-1.el8                                                           @AppStream
gettext.x86_64                                                            0.19.8.1-17.el8                                                          @anaconda
gettext-libs.x86_64                                                       0.19.8.1-17.el8                                                          @anaconda
ghostscript.x86_64                                                        9.25-5.el8_1.1                                                           @AppStream
giflib.x86_64                                                             5.1.4-3.el8                                                              @AppStream
gjs.x86_64                                                                1.56.2-3.el8                                                             @AppStream
glade-libs.x86_64                                                         3.22.1-1.el8                                                             @AppStream
glib-networking.x86_64                                                    2.56.1-1.1.el8                                                           @anaconda
glib2.x86_64                                                              2.56.4-7.el8                                                             @anaconda
glibc.x86_64                                                              2.28-72.el8                                                              @anaconda
glibc-common.x86_64                                                       2.28-72.el8                                                              @anaconda
glibc-langpack-en.x86_64                                                  2.28-72.el8                                                              @anaconda
glibc-langpack-ja.x86_64                                                  2.28-72.el8                                                              @anaconda
glibmm24.x86_64                                                           2.56.0-1.el8                                                             @AppStream
glusterfs.x86_64                                                          6.0-15.el8                                                               @anaconda
glusterfs-api.x86_64                                                      6.0-15.el8                                                               @AppStream
glusterfs-cli.x86_64                                                      6.0-15.el8                                                               @AppStream
glusterfs-client-xlators.x86_64                                           6.0-15.el8                                                               @anaconda
glusterfs-libs.x86_64                                                     6.0-15.el8                                                               @anaconda
glx-utils.x86_64                                                          8.3.0-9.el8                                                              @AppStream
gmp.x86_64                                                                1:6.1.2-10.el8                                                           @anaconda
gnome-autoar.x86_64                                                       0.2.3-1.el8                                                              @AppStream
gnome-bluetooth.x86_64                                                    1:3.28.2-2.el8                                                           @AppStream
gnome-bluetooth-libs.x86_64                                               1:3.28.2-2.el8                                                           @AppStream
gnome-boxes.x86_64                                                        3.28.5-7.el8                                                             @AppStream
gnome-calculator.x86_64                                                   3.28.2-1.el8                                                             @AppStream
gnome-characters.x86_64                                                   3.28.2-1.el8                                                             @AppStream
gnome-classic-session.noarch                                              3.32.1-10.el8                                                            @AppStream
gnome-color-manager.x86_64                                                3.28.0-1.el8                                                             @AppStream
gnome-control-center.x86_64                                               3.28.2-5.el8                                                             @AppStream
gnome-control-center-filesystem.noarch                                    3.28.2-5.el8                                                             @AppStream
gnome-desktop3.x86_64                                                     3.32.2-1.el8                                                             @AppStream
gnome-disk-utility.x86_64                                                 3.28.3-2.el8                                                             @AppStream
gnome-font-viewer.x86_64                                                  3.28.0-1.el8                                                             @AppStream
gnome-getting-started-docs.noarch                                         3.28.2-1.el8                                                             @AppStream
gnome-initial-setup.x86_64                                                3.28.0-8.el8                                                             @AppStream
gnome-keyring.x86_64                                                      3.28.2-1.el8                                                             @AppStream
gnome-keyring-pam.x86_64                                                  3.28.2-1.el8                                                             @AppStream
gnome-logs.x86_64                                                         3.28.5-3.el8                                                             @AppStream
gnome-menus.x86_64                                                        3.13.3-10.el8                                                            @AppStream
gnome-online-accounts.x86_64                                              3.28.0-1.el8                                                             @AppStream
gnome-remote-desktop.x86_64                                               0.1.6-5.el8                                                              @AppStream
gnome-screenshot.x86_64                                                   3.26.0-3.el8                                                             @AppStream
gnome-session.x86_64                                                      3.28.1-7.el8_1                                                           @AppStream
gnome-session-wayland-session.x86_64                                      3.28.1-7.el8_1                                                           @AppStream
gnome-session-xsession.x86_64                                             3.28.1-7.el8_1                                                           @AppStream
gnome-settings-daemon.x86_64                                              3.32.0-4.el8                                                             @AppStream
gnome-shell.x86_64                                                        3.32.2-9.el8                                                             @AppStream
gnome-shell-extension-apps-menu.noarch                                    3.32.1-10.el8                                                            @AppStream
gnome-shell-extension-common.noarch                                       3.32.1-10.el8                                                            @AppStream
gnome-shell-extension-desktop-icons.noarch                                3.32.1-10.el8                                                            @AppStream
gnome-shell-extension-horizontal-workspaces.noarch                        3.32.1-10.el8                                                            @AppStream
gnome-shell-extension-launch-new-instance.noarch                          3.32.1-10.el8                                                            @AppStream
gnome-shell-extension-places-menu.noarch                                  3.32.1-10.el8                                                            @AppStream
gnome-shell-extension-window-list.noarch                                  3.32.1-10.el8                                                            @AppStream
gnome-software.x86_64                                                     3.30.6-2.el8                                                             @AppStream
gnome-system-monitor.x86_64                                               3.28.2-1.el8                                                             @AppStream
gnome-terminal.x86_64                                                     3.28.2-3.el8                                                             @AppStream
gnome-terminal-nautilus.x86_64                                            3.28.2-3.el8                                                             @AppStream
gnome-themes-standard.x86_64                                              3.22.3-4.el8                                                             @AppStream
gnome-user-docs.noarch                                                    3.28.2-1.el8                                                             @AppStream
gnome-video-effects.noarch                                                0.4.3-3.el8                                                              @AppStream
gnu-free-fonts-common.noarch                                              20120503-18.el8                                                          @AppStream
gnu-free-mono-fonts.noarch                                                20120503-18.el8                                                          @AppStream
gnu-free-sans-fonts.noarch                                                20120503-18.el8                                                          @AppStream
gnu-free-serif-fonts.noarch                                               20120503-18.el8                                                          @AppStream
gnupg2.x86_64                                                             2.2.9-1.el8                                                              @anaconda
gnupg2-smime.x86_64                                                       2.2.9-1.el8                                                              @anaconda
gnutls.x86_64                                                             3.6.8-8.el8                                                              @anaconda
gobject-introspection.x86_64                                              1.56.1-1.el8                                                             @anaconda
gom.x86_64                                                                0.3.3-5.el8                                                              @AppStream
google-droid-sans-fonts.noarch                                            20120715-13.el8                                                          @AppStream
google-noto-cjk-fonts-common.noarch                                       20190416-1.el8                                                           @AppStream
google-noto-fonts-common.noarch                                           20161022-7.el8                                                           @AppStream
google-noto-sans-cjk-ttc-fonts.noarch                                     20190416-1.el8                                                           @AppStream
google-noto-sans-lisu-fonts.noarch                                        20161022-7.el8                                                           @AppStream
google-noto-sans-mandaic-fonts.noarch                                     20161022-7.el8                                                           @AppStream
google-noto-sans-meetei-mayek-fonts.noarch                                20161022-7.el8                                                           @AppStream
google-noto-sans-sinhala-fonts.noarch                                     20161022-7.el8                                                           @AppStream
google-noto-sans-tagalog-fonts.noarch                                     20161022-7.el8                                                           @AppStream
google-noto-sans-tai-tham-fonts.noarch                                    20161022-7.el8                                                           @AppStream
google-noto-sans-tai-viet-fonts.noarch                                    20161022-7.el8                                                           @AppStream
google-noto-serif-cjk-ttc-fonts.noarch                                    20190416-1.el8                                                           @AppStream
gpgme.x86_64                                                              1.10.0-6.el8.0.1                                                         @anaconda
gpm-libs.x86_64                                                           1.20.7-15.el8                                                            @AppStream
graphite2.x86_64                                                          1.3.10-10.el8                                                            @AppStream
grep.x86_64                                                               3.1-6.el8                                                                @anaconda
grilo.x86_64                                                              0.3.6-2.el8                                                              @AppStream
grilo-plugins.x86_64                                                      0.3.8-1.el8                                                              @AppStream
groff-base.x86_64                                                         1.22.3-18.el8                                                            @anaconda
grub2-common.noarch                                                       1:2.02-78.el8                                                            @anaconda
grub2-pc.x86_64                                                           1:2.02-78.el8                                                            @anaconda
grub2-pc-modules.noarch                                                   1:2.02-78.el8                                                            @anaconda
grub2-tools.x86_64                                                        1:2.02-78.el8                                                            @anaconda
grub2-tools-extra.x86_64                                                  1:2.02-78.el8                                                            @anaconda
grub2-tools-minimal.x86_64                                                1:2.02-78.el8                                                            @anaconda
grubby.x86_64                                                             8.40-37.el8                                                              @anaconda
gsettings-desktop-schemas.x86_64                                          3.32.0-3.el8                                                             @anaconda
gsm.x86_64                                                                1.0.17-5.el8                                                             @AppStream
gspell.x86_64                                                             1.8.1-1.el8                                                              @AppStream
gssdp.x86_64                                                              1.0.2-6.el8                                                              @AppStream
gssproxy.x86_64                                                           0.8.0-14.el8                                                             @anaconda
gstreamer1.x86_64                                                         1.14.0-3.el8                                                             @AppStream
gstreamer1-plugins-bad-free.x86_64                                        1.14.0-5.el8                                                             @AppStream
gstreamer1-plugins-base.x86_64                                            1.14.0-4.el8                                                             @AppStream
gstreamer1-plugins-good.x86_64                                            1.14.0-4.el8                                                             @AppStream
gstreamer1-plugins-ugly-free.x86_64                                       1.14.0-2.el8                                                             @AppStream
gtk-update-icon-cache.x86_64                                              3.22.30-4.el8                                                            @AppStream
gtk-vnc2.x86_64                                                           0.9.0-1.el8                                                              @AppStream
gtk2.x86_64                                                               2.24.32-4.el8                                                            @AppStream
gtk3.x86_64                                                               3.22.30-4.el8                                                            @AppStream
gtkmm30.x86_64                                                            3.22.2-2.el8                                                             @AppStream
gtksourceview3.x86_64                                                     3.24.9-1.el8                                                             @AppStream
gupnp.x86_64                                                              1.0.3-2.el8                                                              @AppStream
gupnp-av.x86_64                                                           0.12.10-6.el8                                                            @AppStream
gupnp-dlna.x86_64                                                         0.10.5-9.el8                                                             @AppStream
gutenprint.x86_64                                                         5.2.14-3.el8                                                             @AppStream
gutenprint-cups.x86_64                                                    5.2.14-3.el8                                                             @AppStream
gutenprint-doc.x86_64                                                     5.2.14-3.el8                                                             @AppStream
gutenprint-libs.x86_64                                                    5.2.14-3.el8                                                             @AppStream
gvfs.x86_64                                                               1.36.2-6.el8                                                             @AppStream
gvfs-afc.x86_64                                                           1.36.2-6.el8                                                             @AppStream
gvfs-afp.x86_64                                                           1.36.2-6.el8                                                             @AppStream
gvfs-archive.x86_64                                                       1.36.2-6.el8                                                             @AppStream
gvfs-client.x86_64                                                        1.36.2-6.el8                                                             @AppStream
gvfs-fuse.x86_64                                                          1.36.2-6.el8                                                             @AppStream
gvfs-goa.x86_64                                                           1.36.2-6.el8                                                             @AppStream
gvfs-gphoto2.x86_64                                                       1.36.2-6.el8                                                             @AppStream
gvfs-mtp.x86_64                                                           1.36.2-6.el8                                                             @AppStream
gvfs-smb.x86_64                                                           1.36.2-6.el8                                                             @AppStream
gvnc.x86_64                                                               0.9.0-1.el8                                                              @AppStream
gzip.x86_64                                                               1.9-9.el8                                                                @anaconda
hardlink.x86_64                                                           1:1.3-6.el8                                                              @anaconda
harfbuzz.x86_64                                                           1.7.5-3.el8                                                              @AppStream
harfbuzz-icu.x86_64                                                       1.7.5-3.el8                                                              @AppStream
hdparm.x86_64                                                             9.54-2.el8                                                               @anaconda
hicolor-icon-theme.noarch                                                 0.17-2.el8                                                               @AppStream
hostname.x86_64                                                           3.20-6.el8                                                               @anaconda
hplip-common.x86_64                                                       3.18.4-9.el8                                                             @AppStream
hplip-libs.x86_64                                                         3.18.4-9.el8                                                             @AppStream
hunspell.x86_64                                                           1.6.2-1.el8                                                              @AppStream
hunspell-en-US.noarch                                                     0.20140811.1-12.el8                                                      @AppStream
hwdata.noarch                                                             0.314-8.2.el8_1                                                          @BaseOS
hyperv-daemons.x86_64                                                     0-0.27.20180415git.el8                                                   @AppStream
hyperv-daemons-license.noarch                                             0-0.27.20180415git.el8                                                   @AppStream
hypervfcopyd.x86_64                                                       0-0.27.20180415git.el8                                                   @AppStream
hypervkvpd.x86_64                                                         0-0.27.20180415git.el8                                                   @AppStream
hypervvssd.x86_64                                                         0-0.27.20180415git.el8                                                   @AppStream
hyphen.x86_64                                                             2.8.8-9.el8                                                              @AppStream
ibus.x86_64                                                               1.5.19-4.el8                                                             @AppStream
ibus-gtk2.x86_64                                                          1.5.19-4.el8                                                             @AppStream
ibus-gtk3.x86_64                                                          1.5.19-4.el8                                                             @AppStream
ibus-libs.x86_64                                                          1.5.19-4.el8                                                             @AppStream
ibus-setup.noarch                                                         1.5.19-4.el8                                                             @AppStream
iio-sensor-proxy.x86_64                                                   2.4-3.el8                                                                @AppStream
ima-evm-utils.x86_64                                                      1.1-5.el8                                                                @anaconda
info.x86_64                                                               6.5-4.el8                                                                @anaconda
initial-setup.x86_64                                                      0.3.62.1-1.el8                                                           @AppStream
initial-setup-gui.x86_64                                                  0.3.62.1-1.el8                                                           @AppStream
initscripts.x86_64                                                        10.00.4-1.el8                                                            @anaconda
ipcalc.x86_64                                                             0.2.4-3.el8                                                              @anaconda
iproute.x86_64                                                            4.18.0-15.el8                                                            @anaconda
iproute-tc.x86_64                                                         4.18.0-15.el8                                                            @anaconda
iprutils.x86_64                                                           2.4.18.1-1.el8                                                           @anaconda
ipset.x86_64                                                              7.1-1.el8                                                                @anaconda
ipset-libs.x86_64                                                         7.1-1.el8                                                                @anaconda
iptables.x86_64                                                           1.8.2-16.el8                                                             @anaconda
iptables-ebtables.x86_64                                                  1.8.2-16.el8                                                             @anaconda
iptables-libs.x86_64                                                      1.8.2-16.el8                                                             @anaconda
iptstate.x86_64                                                           2.2.6-6.el8                                                              @anaconda
iputils.x86_64                                                            20180629-2.el8                                                           @anaconda
ipxe-roms-qemu.noarch                                                     20181214-3.git133f4c47.el8                                               @AppStream
irqbalance.x86_64                                                         2:1.4.0-4.el8                                                            @anaconda
iscsi-initiator-utils.x86_64                                              6.2.0.877-1.gitf71581b.el8                                               @anaconda
iscsi-initiator-utils-iscsiuio.x86_64                                     6.2.0.877-1.gitf71581b.el8                                               @anaconda
isns-utils-libs.x86_64                                                    0.99-1.el8                                                               @anaconda
iso-codes.noarch                                                          3.79-2.el8                                                               @AppStream
itstool.noarch                                                            2.0.4-2.el8                                                              @AppStream
iwl100-firmware.noarch                                                    39.31.5.1-94.el8.1                                                       @anaconda
iwl1000-firmware.noarch                                                   1:39.31.5.1-94.el8.1                                                     @anaconda
iwl105-firmware.noarch                                                    18.168.6.1-94.el8.1                                                      @anaconda
iwl135-firmware.noarch                                                    18.168.6.1-94.el8.1                                                      @anaconda
iwl2000-firmware.noarch                                                   18.168.6.1-94.el8.1                                                      @anaconda
iwl2030-firmware.noarch                                                   18.168.6.1-94.el8.1                                                      @anaconda
iwl3160-firmware.noarch                                                   1:25.30.13.0-94.el8.1                                                    @anaconda
iwl3945-firmware.noarch                                                   15.32.2.9-94.el8.1                                                       @anaconda
iwl4965-firmware.noarch                                                   228.61.2.24-94.el8.1                                                     @anaconda
iwl5000-firmware.noarch                                                   8.83.5.1_1-94.el8.1                                                      @anaconda
iwl5150-firmware.noarch                                                   8.24.2.2-94.el8.1                                                        @anaconda
iwl6000-firmware.noarch                                                   9.221.4.1-94.el8.1                                                       @anaconda
iwl6000g2a-firmware.noarch                                                18.168.6.1-94.el8.1                                                      @anaconda
iwl6000g2b-firmware.noarch                                                18.168.6.1-94.el8.1                                                      @anaconda
iwl6050-firmware.noarch                                                   41.28.5.1-94.el8.1                                                       @anaconda
iwl7260-firmware.noarch                                                   1:25.30.13.0-94.el8.1                                                    @anaconda
jansson.x86_64                                                            2.11-3.el8                                                               @anaconda
jasper-libs.x86_64                                                        2.0.14-4.el8                                                             @AppStream
jbig2dec-libs.x86_64                                                      0.14-2.el8                                                               @AppStream
jbigkit-libs.x86_64                                                       2.1-14.el8                                                               @AppStream
jimtcl.x86_64                                                             0.77-5.el8                                                               @anaconda
jomolhari-fonts.noarch                                                    0.003-24.el8                                                             @AppStream
jose.x86_64                                                               10-2.el8                                                                 @AppStream
json-c.x86_64                                                             0.13.1-0.2.el8                                                           @anaconda
json-glib.x86_64                                                          1.4.4-1.el8                                                              @anaconda
julietaula-montserrat-fonts.noarch                                        1:7.200-2.el8                                                            @AppStream
kbd.x86_64                                                                2.0.4-8.el8                                                              @anaconda
kbd-legacy.noarch                                                         2.0.4-8.el8                                                              @anaconda
kbd-misc.noarch                                                           2.0.4-8.el8                                                              @anaconda
kernel.x86_64                                                             4.18.0-147.el8                                                           @anaconda
kernel.x86_64                                                             4.18.0-147.3.1.el8_1                                                     @BaseOS
kernel-core.x86_64                                                        4.18.0-147.el8                                                           @anaconda
kernel-core.x86_64                                                        4.18.0-147.3.1.el8_1                                                     @BaseOS
kernel-modules.x86_64                                                     4.18.0-147.el8                                                           @anaconda
kernel-modules.x86_64                                                     4.18.0-147.3.1.el8_1                                                     @BaseOS
kernel-tools.x86_64                                                       4.18.0-147.3.1.el8_1                                                     @BaseOS
kernel-tools-libs.x86_64                                                  4.18.0-147.3.1.el8_1                                                     @BaseOS
kexec-tools.x86_64                                                        2.0.19-12.el8_1.1                                                        @BaseOS
keybinder3.x86_64                                                         0.3.2-4.el8                                                              @AppStream
keyutils.x86_64                                                           1.5.10-6.el8                                                             @anaconda
keyutils-libs.x86_64                                                      1.5.10-6.el8                                                             @anaconda
khmeros-base-fonts.noarch                                                 5.0-25.el8                                                               @AppStream
khmeros-fonts-common.noarch                                               5.0-25.el8                                                               @AppStream
kmod.x86_64                                                               25-13.el8                                                                @anaconda
kmod-kvdo.x86_64                                                          6.2.1.138-57.el8                                                         @anaconda
kmod-libs.x86_64                                                          25-13.el8                                                                @anaconda
kpartx.x86_64                                                             0.8.0-5.el8                                                              @anaconda
kpatch.noarch                                                             0.6.1-5.el8                                                              @anaconda
krb5-libs.x86_64                                                          1.17-9.el8                                                               @anaconda
lame-libs.x86_64                                                          3.100-6.el8                                                              @AppStream
langpacks-ja.noarch                                                       1.0-12.el8                                                               @AppStream
langtable.noarch                                                          0.0.38-5.el8                                                             @AppStream
langtable-data.noarch                                                     0.0.38-5.el8                                                             @AppStream
lcms2.x86_64                                                              2.9-2.el8                                                                @AppStream
ledmon.x86_64                                                             0.92-7.el8                                                               @anaconda
less.x86_64                                                               530-1.el8                                                                @anaconda
libICE.x86_64                                                             1.0.9-15.el8                                                             @AppStream
libSM.x86_64                                                              1.2.3-1.el8                                                              @AppStream
libX11.x86_64                                                             1.6.7-1.el8                                                              @AppStream
libX11-common.noarch                                                      1.6.7-1.el8                                                              @AppStream
libX11-xcb.x86_64                                                         1.6.7-1.el8                                                              @AppStream
libXau.x86_64                                                             1.0.8-13.el8                                                             @AppStream
libXcomposite.x86_64                                                      0.4.4-14.el8                                                             @AppStream
libXcursor.x86_64                                                         1.1.15-3.el8                                                             @AppStream
libXdamage.x86_64                                                         1.1.4-14.el8                                                             @AppStream
libXdmcp.x86_64                                                           1.1.2-11.el8                                                             @AppStream
libXext.x86_64                                                            1.3.3-9.el8                                                              @AppStream
libXfixes.x86_64                                                          5.0.3-7.el8                                                              @AppStream
libXfont2.x86_64                                                          2.0.3-2.el8                                                              @AppStream
libXft.x86_64                                                             2.3.2-10.el8                                                             @AppStream
libXi.x86_64                                                              1.7.9-7.el8                                                              @AppStream
libXinerama.x86_64                                                        1.1.4-1.el8                                                              @AppStream
libXmu.x86_64                                                             1.1.2-12.el8                                                             @AppStream
libXpm.x86_64                                                             3.5.12-7.el8                                                             @AppStream
libXrandr.x86_64                                                          1.5.1-7.el8                                                              @AppStream
libXrender.x86_64                                                         0.9.10-7.el8                                                             @AppStream
libXres.x86_64                                                            1.2.0-4.el8                                                              @AppStream
libXt.x86_64                                                              1.1.5-12.el8                                                             @AppStream
libXtst.x86_64                                                            1.2.3-7.el8                                                              @AppStream
libXv.x86_64                                                              1.0.11-7.el8                                                             @AppStream
libXvMC.x86_64                                                            1.0.10-6.el8                                                             @AppStream
libXxf86dga.x86_64                                                        1.1.4-12.el8                                                             @AppStream
libXxf86misc.x86_64                                                       1.0.4-1.el8                                                              @AppStream
libXxf86vm.x86_64                                                         1.1.4-9.el8                                                              @AppStream
liba52.x86_64                                                             0.7.4-32.el8                                                             @AppStream
libacl.x86_64                                                             2.2.53-1.el8                                                             @anaconda
libaio.x86_64                                                             0.3.112-1.el8                                                            @anaconda
libao.x86_64                                                              1.2.0-10.el8                                                             @AppStream
libappstream-glib.x86_64                                                  0.7.14-3.el8                                                             @anaconda
libarchive.x86_64                                                         3.3.2-7.el8                                                              @anaconda
libassuan.x86_64                                                          2.5.1-3.el8                                                              @anaconda
libasyncns.x86_64                                                         0.8-14.el8                                                               @AppStream
libatasmart.x86_64                                                        0.19-14.el8                                                              @AppStream
libattr.x86_64                                                            2.4.48-3.el8                                                             @anaconda
libavc1394.x86_64                                                         0.5.4-7.el8                                                              @AppStream
libbasicobjects.x86_64                                                    0.1.1-39.el8                                                             @anaconda
libblkid.x86_64                                                           2.32.1-17.el8                                                            @anaconda
libblockdev.x86_64                                                        2.19-9.el8                                                               @AppStream
libblockdev-crypto.x86_64                                                 2.19-9.el8                                                               @AppStream
libblockdev-dm.x86_64                                                     2.19-9.el8                                                               @AppStream
libblockdev-fs.x86_64                                                     2.19-9.el8                                                               @AppStream
libblockdev-kbd.x86_64                                                    2.19-9.el8                                                               @AppStream
libblockdev-loop.x86_64                                                   2.19-9.el8                                                               @AppStream
libblockdev-lvm.x86_64                                                    2.19-9.el8                                                               @AppStream
libblockdev-mdraid.x86_64                                                 2.19-9.el8                                                               @AppStream
libblockdev-mpath.x86_64                                                  2.19-9.el8                                                               @AppStream
libblockdev-nvdimm.x86_64                                                 2.19-9.el8                                                               @AppStream
libblockdev-part.x86_64                                                   2.19-9.el8                                                               @AppStream
libblockdev-swap.x86_64                                                   2.19-9.el8                                                               @AppStream
libblockdev-utils.x86_64                                                  2.19-9.el8                                                               @AppStream
libbluray.x86_64                                                          1.0.2-3.el8                                                              @AppStream
libbytesize.x86_64                                                        1.4-1.el8                                                                @AppStream
libcacard.x86_64                                                          3:2.7.0-2.el8_1                                                          @AppStream
libcanberra.x86_64                                                        0.30-16.el8                                                              @AppStream
libcanberra-gtk3.x86_64                                                   0.30-16.el8                                                              @AppStream
libcap.x86_64                                                             2.26-1.el8                                                               @anaconda
libcap-ng.x86_64                                                          0.7.9-4.el8                                                              @anaconda
libcdio.x86_64                                                            2.0.0-3.el8                                                              @AppStream
libcdio-paranoia.x86_64                                                   10.2+0.94+2-3.el8                                                        @AppStream
libcollection.x86_64                                                      0.7.0-39.el8                                                             @anaconda
libcom_err.x86_64                                                         1.44.6-3.el8                                                             @anaconda
libcomps.x86_64                                                           0.1.11-2.el8                                                             @anaconda
libconfig.x86_64                                                          1.5-9.el8                                                                @anaconda
libcroco.x86_64                                                           0.6.12-4.el8                                                             @anaconda
libcurl.x86_64                                                            7.61.1-11.el8                                                            @anaconda
libdaemon.x86_64                                                          0.14-15.el8                                                              @anaconda
libdatrie.x86_64                                                          0.2.9-7.el8                                                              @AppStream
libdb.x86_64                                                              5.3.28-37.el8                                                            @anaconda
libdb-utils.x86_64                                                        5.3.28-37.el8                                                            @anaconda
libdhash.x86_64                                                           0.5.0-39.el8                                                             @anaconda
libdmapsharing.x86_64                                                     2.9.37-5.el8                                                             @AppStream
libdmx.x86_64                                                             1.1.4-3.el8                                                              @AppStream
libdnet.x86_64                                                            1.12-26.el8                                                              @AppStream
libdnf.x86_64                                                             0.35.1-9.el8_1                                                           @BaseOS
libdrm.x86_64                                                             2.4.98-2.el8                                                             @AppStream
libdv.x86_64                                                              1.0.0-27.el8                                                             @AppStream
libdvdnav.x86_64                                                          5.0.3-8.el8                                                              @AppStream
libdvdread.x86_64                                                         5.0.3-9.el8                                                              @AppStream
libedit.x86_64                                                            3.1-23.20170329cvs.el8                                                   @anaconda
libepoxy.x86_64                                                           1.5.2-1.el8                                                              @AppStream
liberation-fonts-common.noarch                                            1:2.00.3-4.el8                                                           @anaconda
liberation-mono-fonts.noarch                                              1:2.00.3-4.el8                                                           @anaconda
liberation-sans-fonts.noarch                                              1:2.00.3-4.el8                                                           @anaconda
libertas-usb8388-firmware.noarch                                          2:20190516-94.git711d3297.el8                                            @anaconda
libestr.x86_64                                                            0.1.10-1.el8                                                             @AppStream
libevdev.x86_64                                                           1.5.9-5.el8                                                              @AppStream
libevent.x86_64                                                           2.1.8-5.el8                                                              @anaconda
libexif.x86_64                                                            0.6.21-16.el8                                                            @AppStream
libfastjson.x86_64                                                        0.99.8-2.el8                                                             @AppStream
libfdisk.x86_64                                                           2.32.1-17.el8                                                            @anaconda
libffi.x86_64                                                             3.1-21.el8                                                               @anaconda
libfontenc.x86_64                                                         1.1.3-8.el8                                                              @AppStream
libfprint.x86_64                                                          0.8.2-1.el8.0.1                                                          @AppStream
libgcab1.x86_64                                                           1.1-1.el8                                                                @anaconda
libgcc.x86_64                                                             8.3.1-4.5.el8                                                            @anaconda
libgcrypt.x86_64                                                          1.8.3-4.el8                                                              @anaconda
libgdata.x86_64                                                           0.17.9-2.el8                                                             @AppStream
libgdither.x86_64                                                         0.6-17.el8                                                               @AppStream
libgexiv2.x86_64                                                          0.10.8-2.el8                                                             @AppStream
libglvnd.x86_64                                                           1:1.0.1-0.9.git5baa1e5.el8                                               @AppStream
libglvnd-egl.x86_64                                                       1:1.0.1-0.9.git5baa1e5.el8                                               @AppStream
libglvnd-gles.x86_64                                                      1:1.0.1-0.9.git5baa1e5.el8                                               @AppStream
libglvnd-glx.x86_64                                                       1:1.0.1-0.9.git5baa1e5.el8                                               @AppStream
libgnomekbd.x86_64                                                        3.26.0-4.el8                                                             @AppStream
libgomp.x86_64                                                            8.3.1-4.5.el8                                                            @anaconda
libgovirt.x86_64                                                          0.3.4-9.el8                                                              @AppStream
libgpg-error.x86_64                                                       1.31-1.el8                                                               @anaconda
libgphoto2.x86_64                                                         2.5.16-3.el8                                                             @AppStream
libgs.x86_64                                                              9.25-5.el8_1.1                                                           @AppStream
libgsf.x86_64                                                             1.14.41-5.el8                                                            @AppStream
libgtop2.x86_64                                                           2.38.0-3.el8                                                             @AppStream
libgudev.x86_64                                                           232-4.el8                                                                @anaconda
libgusb.x86_64                                                            0.3.0-1.el8                                                              @anaconda
libgweather.x86_64                                                        3.28.2-2.el8                                                             @AppStream
libgxps.x86_64                                                            0.3.0-5.el8                                                              @AppStream
libibumad.x86_64                                                          22.3-1.el8                                                               @anaconda
libibverbs.x86_64                                                         22.3-1.el8                                                               @anaconda
libical.x86_64                                                            3.0.3-3.el8                                                              @anaconda
libicu.x86_64                                                             60.3-1.el8                                                               @anaconda
libidn.x86_64                                                             1.34-5.el8                                                               @AppStream
libidn2.x86_64                                                            2.2.0-1.el8                                                              @anaconda
libiec61883.x86_64                                                        1.2.0-18.el8                                                             @AppStream
libieee1284.x86_64                                                        0.2.11-28.el8                                                            @AppStream
libijs.x86_64                                                             0.35-5.el8                                                               @AppStream
libimobiledevice.x86_64                                                   1.2.0-16.el8                                                             @AppStream
libini_config.x86_64                                                      1.3.1-39.el8                                                             @anaconda
libinput.x86_64                                                           1.13.2-1.el8                                                             @AppStream
libipa_hbac.x86_64                                                        2.2.0-19.el8                                                             @anaconda
libiptcdata.x86_64                                                        1.0.4-21.el8                                                             @AppStream
libiscsi.x86_64                                                           1.18.0-8.module_el8.1.0+248+298dec18                                     @AppStream
libjose.x86_64                                                            10-2.el8                                                                 @AppStream
libjpeg-turbo.x86_64                                                      1.5.3-10.el8                                                             @AppStream
libkcapi.x86_64                                                           1.1.1-16_1.el8                                                           @anaconda
libkcapi-hmaccalc.x86_64                                                  1.1.1-16_1.el8                                                           @anaconda
libksba.x86_64                                                            1.3.5-7.el8                                                              @anaconda
libldb.x86_64                                                             1.5.4-2.el8                                                              @anaconda
liblouis.x86_64                                                           2.6.2-16.el8                                                             @AppStream
libluksmeta.x86_64                                                        9-2.el8                                                                  @AppStream
libmaxminddb.x86_64                                                       1.2.0-6.el8                                                              @AppStream
libmbim.x86_64                                                            1.18.2-3.el8                                                             @anaconda
libmbim-utils.x86_64                                                      1.18.2-3.el8                                                             @anaconda
libmcpp.x86_64                                                            2.7.2-20.el8                                                             @AppStream
libmediaart.x86_64                                                        1.9.4-4.el8                                                              @AppStream
libmetalink.x86_64                                                        0.1.3-7.el8                                                              @anaconda
libmnl.x86_64                                                             1.0.4-6.el8                                                              @anaconda
libmodman.x86_64                                                          2.0.1-17.el8                                                             @anaconda
libmodulemd1.x86_64                                                       1.8.11-4.el8_1                                                           @BaseOS
libmount.x86_64                                                           2.32.1-17.el8                                                            @anaconda
libmpc.x86_64                                                             1.0.2-9.el8                                                              @AppStream
libmpcdec.x86_64                                                          1.2.6-20.el8                                                             @AppStream
libmspack.x86_64                                                          0.7-0.1.alpha.el8.3                                                      @AppStream
libmtp.x86_64                                                             1.1.14-3.el8                                                             @AppStream
libmusicbrainz5.x86_64                                                    5.1.0-10.el8                                                             @AppStream
libndp.x86_64                                                             1.7-1.el8                                                                @anaconda
libnet.x86_64                                                             1.1.6-15.el8                                                             @AppStream
libnetfilter_conntrack.x86_64                                             1.0.6-5.el8                                                              @anaconda
libnfnetlink.x86_64                                                       1.0.1-13.el8                                                             @anaconda
libnfsidmap.x86_64                                                        1:2.3.3-26.el8                                                           @anaconda
libnftnl.x86_64                                                           1.1.1-4.el8                                                              @anaconda
libnghttp2.x86_64                                                         1.33.0-1.el8_0.1                                                         @anaconda
libnl3.x86_64                                                             3.4.0-5.el8                                                              @anaconda
libnl3-cli.x86_64                                                         3.4.0-5.el8                                                              @anaconda
libnma.x86_64                                                             1.8.22-2.el8                                                             @AppStream
libnotify.x86_64                                                          0.7.7-5.el8                                                              @AppStream
libnsl2.x86_64                                                            1.2.0-2.20180605git4a062cf.el8                                           @anaconda
liboauth.x86_64                                                           1.0.3-9.el8                                                              @AppStream
libogg.x86_64                                                             2:1.3.2-10.el8                                                           @AppStream
libosinfo.x86_64                                                          1.5.0-3.el8                                                              @AppStream
libpaper.x86_64                                                           1.1.24-22.el8                                                            @AppStream
libpath_utils.x86_64                                                      0.2.1-39.el8                                                             @anaconda
libpcap.x86_64                                                            14:1.9.0-3.el8                                                           @anaconda
libpciaccess.x86_64                                                       0.14-1.el8                                                               @anaconda
libpeas.x86_64                                                            1.22.0-6.el8                                                             @anaconda
libpeas-gtk.x86_64                                                        1.22.0-6.el8                                                             @AppStream
libpeas-loader-python3.x86_64                                             1.22.0-6.el8                                                             @AppStream
libpipeline.x86_64                                                        1.5.0-2.el8                                                              @anaconda
libpkgconf.x86_64                                                         1.4.2-1.el8                                                              @anaconda
libplist.x86_64                                                           2.0.0-10.el8                                                             @AppStream
libpmem.x86_64                                                            1.6-2.el8                                                                @AppStream
libpng.x86_64                                                             2:1.6.34-5.el8                                                           @anaconda
libproxy.x86_64                                                           0.4.15-5.2.el8                                                           @anaconda
libpsl.x86_64                                                             0.20.2-5.el8                                                             @anaconda
libpwquality.x86_64                                                       1.4.0-9.el8                                                              @anaconda
libqmi.x86_64                                                             1.22.4-4.el8                                                             @anaconda
libqmi-utils.x86_64                                                       1.22.4-4.el8                                                             @anaconda
libquvi.x86_64                                                            0.9.4-12.el8                                                             @AppStream
libquvi-scripts.noarch                                                    0.9.20131130-9.el8                                                       @AppStream
librados2.x86_64                                                          1:12.2.7-9.el8                                                           @AppStream
libraw1394.x86_64                                                         2.1.2-5.el8                                                              @AppStream
librbd1.x86_64                                                            1:12.2.7-9.el8                                                           @AppStream
librdmacm.x86_64                                                          22.3-1.el8                                                               @anaconda
libref_array.x86_64                                                       0.1.5-39.el8                                                             @anaconda
librelp.x86_64                                                            1.2.16-1.el8                                                             @AppStream
librepo.x86_64                                                            1.10.3-3.el8                                                             @anaconda
libreport.x86_64                                                          2.9.5-9.el8                                                              @AppStream
libreport-anaconda.x86_64                                                 2.9.5-9.el8                                                              @AppStream
libreport-cli.x86_64                                                      2.9.5-9.el8                                                              @AppStream
libreport-filesystem.x86_64                                               2.9.5-9.el8                                                              @anaconda
libreport-gtk.x86_64                                                      2.9.5-9.el8                                                              @AppStream
libreport-plugin-reportuploader.x86_64                                    2.9.5-9.el8                                                              @AppStream
libreport-plugin-rhtsupport.x86_64                                        2.9.5-9.el8                                                              @AppStream
libreport-web.x86_64                                                      2.9.5-9.el8                                                              @AppStream
librsvg2.x86_64                                                           2.42.7-3.el8                                                             @AppStream
libsamplerate.x86_64                                                      0.1.9-1.el8                                                              @AppStream
libsane-hpaio.x86_64                                                      3.18.4-9.el8                                                             @AppStream
libseccomp.x86_64                                                         2.4.1-1.el8                                                              @anaconda
libsecret.x86_64                                                          0.18.6-1.el8                                                             @anaconda
libselinux.x86_64                                                         2.9-2.1.el8                                                              @anaconda
libselinux-utils.x86_64                                                   2.9-2.1.el8                                                              @anaconda
libsemanage.x86_64                                                        2.9-1.el8                                                                @anaconda
libsepol.x86_64                                                           2.9-1.el8                                                                @anaconda
libshout.x86_64                                                           2.2.2-19.el8                                                             @AppStream
libsigc++20.x86_64                                                        2.10.0-5.el8                                                             @AppStream
libsigsegv.x86_64                                                         2.11-5.el8                                                               @anaconda
libsmartcols.x86_64                                                       2.32.1-17.el8                                                            @anaconda
libsmbclient.x86_64                                                       4.10.4-101.el8_1                                                         @BaseOS
libsmbios.x86_64                                                          2.4.1-2.el8                                                              @anaconda
libsndfile.x86_64                                                         1.0.28-8.el8                                                             @AppStream
libsolv.x86_64                                                            0.7.4-3.el8                                                              @anaconda
libsoup.x86_64                                                            2.62.3-1.el8                                                             @anaconda
libspectre.x86_64                                                         0.2.8-5.el8                                                              @AppStream
libsrtp.x86_64                                                            1.5.4-8.el8                                                              @AppStream
libss.x86_64                                                              1.44.6-3.el8                                                             @anaconda
libssh.x86_64                                                             0.9.0-4.el8                                                              @anaconda
libssh-config.noarch                                                      0.9.0-4.el8                                                              @anaconda
libsss_autofs.x86_64                                                      2.2.0-19.el8                                                             @anaconda
libsss_certmap.x86_64                                                     2.2.0-19.el8                                                             @anaconda
libsss_idmap.x86_64                                                       2.2.0-19.el8                                                             @anaconda
libsss_nss_idmap.x86_64                                                   2.2.0-19.el8                                                             @anaconda
libsss_sudo.x86_64                                                        2.2.0-19.el8                                                             @anaconda
libstdc++.x86_64                                                          8.3.1-4.5.el8                                                            @anaconda
libstemmer.x86_64                                                         0-10.585svn.el8                                                          @anaconda
libstoragemgmt.x86_64                                                     1.8.1-2.el8                                                              @anaconda
libsysfs.x86_64                                                           2.1.0-24.el8                                                             @anaconda
libtalloc.x86_64                                                          2.1.16-3.el8                                                             @anaconda
libtar.x86_64                                                             1.2.20-15.el8                                                            @AppStream
libtasn1.x86_64                                                           4.13-3.el8                                                               @anaconda
libtdb.x86_64                                                             1.3.18-2.el8                                                             @anaconda
libteam.x86_64                                                            1.28-4.el8                                                               @anaconda
libtevent.x86_64                                                          0.9.39-2.el8                                                             @anaconda
libthai.x86_64                                                            0.1.27-2.el8                                                             @AppStream
libtheora.x86_64                                                          1:1.1.1-21.el8                                                           @AppStream
libtiff.x86_64                                                            4.0.9-15.el8                                                             @AppStream
libtimezonemap.x86_64                                                     0.4.5.1-3.el8                                                            @AppStream
libtirpc.x86_64                                                           1.1.4-4.el8                                                              @anaconda
libtool-ltdl.x86_64                                                       2.4.6-25.el8                                                             @anaconda
libudisks2.x86_64                                                         2.8.3-2.el8                                                              @AppStream
libunistring.x86_64                                                       0.9.9-3.el8                                                              @anaconda
libusal.x86_64                                                            1.1.11-39.el8                                                            @AppStream
libusbmuxd.x86_64                                                         1.0.10-9.el8                                                             @AppStream
libusbx.x86_64                                                            1.0.22-1.el8                                                             @anaconda
libuser.x86_64                                                            0.62-23.el8                                                              @anaconda
libutempter.x86_64                                                        1.1.6-14.el8                                                             @anaconda
libuuid.x86_64                                                            2.32.1-17.el8                                                            @anaconda
libv4l.x86_64                                                             1.14.2-3.el8                                                             @AppStream
libvarlink.x86_64                                                         18-3.el8                                                                 @anaconda
libverto.x86_64                                                           0.3.0-5.el8                                                              @anaconda
libverto-libevent.x86_64                                                  0.3.0-5.el8                                                              @anaconda
libvirt-daemon.x86_64                                                     4.5.0-35.1.module_el8.1.0+258+1d2a1d58                                   @AppStream
libvirt-daemon-config-network.x86_64                                      4.5.0-35.1.module_el8.1.0+258+1d2a1d58                                   @AppStream
libvirt-daemon-driver-interface.x86_64                                    4.5.0-35.1.module_el8.1.0+258+1d2a1d58                                   @AppStream
libvirt-daemon-driver-network.x86_64                                      4.5.0-35.1.module_el8.1.0+258+1d2a1d58                                   @AppStream
libvirt-daemon-driver-nodedev.x86_64                                      4.5.0-35.1.module_el8.1.0+258+1d2a1d58                                   @AppStream
libvirt-daemon-driver-nwfilter.x86_64                                     4.5.0-35.1.module_el8.1.0+258+1d2a1d58                                   @AppStream
libvirt-daemon-driver-qemu.x86_64                                         4.5.0-35.1.module_el8.1.0+258+1d2a1d58                                   @AppStream
libvirt-daemon-driver-secret.x86_64                                       4.5.0-35.1.module_el8.1.0+258+1d2a1d58                                   @AppStream
libvirt-daemon-driver-storage.x86_64                                      4.5.0-35.1.module_el8.1.0+258+1d2a1d58                                   @AppStream
libvirt-daemon-driver-storage-core.x86_64                                 4.5.0-35.1.module_el8.1.0+258+1d2a1d58                                   @AppStream
libvirt-daemon-driver-storage-disk.x86_64                                 4.5.0-35.1.module_el8.1.0+258+1d2a1d58                                   @AppStream
libvirt-daemon-driver-storage-gluster.x86_64                              4.5.0-35.1.module_el8.1.0+258+1d2a1d58                                   @AppStream
libvirt-daemon-driver-storage-iscsi.x86_64                                4.5.0-35.1.module_el8.1.0+258+1d2a1d58                                   @AppStream
libvirt-daemon-driver-storage-logical.x86_64                              4.5.0-35.1.module_el8.1.0+258+1d2a1d58                                   @AppStream
libvirt-daemon-driver-storage-mpath.x86_64                                4.5.0-35.1.module_el8.1.0+258+1d2a1d58                                   @AppStream
libvirt-daemon-driver-storage-rbd.x86_64                                  4.5.0-35.1.module_el8.1.0+258+1d2a1d58                                   @AppStream
libvirt-daemon-driver-storage-scsi.x86_64                                 4.5.0-35.1.module_el8.1.0+258+1d2a1d58                                   @AppStream
libvirt-daemon-kvm.x86_64                                                 4.5.0-35.1.module_el8.1.0+258+1d2a1d58                                   @AppStream
libvirt-gconfig.x86_64                                                    2.0.0-1.el8                                                              @AppStream
libvirt-glib.x86_64                                                       2.0.0-1.el8                                                              @AppStream
libvirt-gobject.x86_64                                                    2.0.0-1.el8                                                              @AppStream
libvirt-libs.x86_64                                                       4.5.0-35.1.module_el8.1.0+258+1d2a1d58                                   @AppStream
libvisual.x86_64                                                          1:0.4.0-24.el8                                                           @AppStream
libvncserver.x86_64                                                       0.9.11-9.el8                                                             @AppStream
libvorbis.x86_64                                                          1:1.3.6-2.el8                                                            @AppStream
libvpx.x86_64                                                             1.7.0-6.el8                                                              @AppStream
libwacom.x86_64                                                           0.31-1.el8                                                               @AppStream
libwacom-data.noarch                                                      0.31-1.el8                                                               @AppStream
libwayland-client.x86_64                                                  1.15.0-1.el8                                                             @AppStream
libwayland-cursor.x86_64                                                  1.15.0-1.el8                                                             @AppStream
libwayland-egl.x86_64                                                     1.15.0-1.el8                                                             @AppStream
libwayland-server.x86_64                                                  1.15.0-1.el8                                                             @AppStream
libwbclient.x86_64                                                        4.10.4-101.el8_1                                                         @BaseOS
libwebp.x86_64                                                            1.0.0-1.el8                                                              @AppStream
libwnck3.x86_64                                                           3.24.1-2.el8                                                             @AppStream
libxcb.x86_64                                                             1.13-5.el8                                                               @AppStream
libxcrypt.x86_64                                                          4.1.1-4.el8                                                              @anaconda
libxkbcommon.x86_64                                                       0.8.2-1.el8                                                              @AppStream
libxkbcommon-x11.x86_64                                                   0.8.2-1.el8                                                              @AppStream
libxkbfile.x86_64                                                         1.0.9-9.el8                                                              @AppStream
libxklavier.x86_64                                                        5.4-11.el8                                                               @AppStream
libxml2.x86_64                                                            2.9.7-5.el8                                                              @anaconda
libxshmfence.x86_64                                                       1.3-2.el8                                                                @AppStream
libxslt.x86_64                                                            1.1.32-3.el8                                                             @anaconda
libyaml.x86_64                                                            0.1.7-5.el8                                                              @anaconda
linux-firmware.noarch                                                     20190516-94.git711d3297.el8                                              @anaconda
llvm-libs.x86_64                                                          8.0.1-1.module_el8.1.0+215+a01033fb                                      @AppStream
lockdev.x86_64                                                            1.0.4-0.28.20111007git.el8                                               @anaconda
logrotate.x86_64                                                          3.14.0-3.el8                                                             @anaconda
lohit-assamese-fonts.noarch                                               2.91.5-3.el8                                                             @AppStream
lohit-bengali-fonts.noarch                                                2.91.5-3.el8                                                             @AppStream
lohit-devanagari-fonts.noarch                                             2.95.4-3.el8                                                             @AppStream
lohit-gujarati-fonts.noarch                                               2.92.4-3.el8                                                             @AppStream
lohit-gurmukhi-fonts.noarch                                               2.91.2-3.el8                                                             @AppStream
lohit-kannada-fonts.noarch                                                2.5.4-3.el8                                                              @AppStream
lohit-odia-fonts.noarch                                                   2.91.2-3.el8                                                             @AppStream
lohit-tamil-fonts.noarch                                                  2.91.3-3.el8                                                             @AppStream
lohit-telugu-fonts.noarch                                                 2.5.5-3.el8                                                              @AppStream
lshw.x86_64                                                               B.02.18-21.el8                                                           @anaconda
lsof.x86_64                                                               4.91-2.el8                                                               @anaconda
lsscsi.x86_64                                                             0.30-1.el8                                                               @anaconda
lua.x86_64                                                                5.3.4-11.el8                                                             @AppStream
lua-expat.x86_64                                                          1.3.0-12.el8.1                                                           @AppStream
lua-json.noarch                                                           1.3.2-9.el8                                                              @AppStream
lua-libs.x86_64                                                           5.3.4-11.el8                                                             @anaconda
lua-lpeg.x86_64                                                           1.0.1-6.el8                                                              @AppStream
lua-socket.x86_64                                                         3.0-0.17.rc1.el8                                                         @AppStream
luksmeta.x86_64                                                           9-2.el8                                                                  @AppStream
lvm2.x86_64                                                               8:2.03.05-5.el8.0.1                                                      @anaconda
lvm2-libs.x86_64                                                          8:2.03.05-5.el8.0.1                                                      @anaconda
lz4.x86_64                                                                1.8.1.2-4.el8                                                            @anaconda
lz4-libs.x86_64                                                           1.8.1.2-4.el8                                                            @anaconda
lzo.x86_64                                                                2.08-14.el8                                                              @anaconda
lzo-minilzo.x86_64                                                        2.08-14.el8                                                              @anaconda
lzop.x86_64                                                               1.03-20.el8                                                              @anaconda
mailcap.noarch                                                            2.1.48-3.el8                                                             @anaconda
mallard-rng.noarch                                                        1.0.3-1.el8                                                              @AppStream
man-db.x86_64                                                             2.7.6.1-17.el8                                                           @anaconda
man-pages.x86_64                                                          4.15-6.el8                                                               @anaconda
man-pages-overrides.noarch                                                8.1.0.0-2.el8                                                            @AppStream
mcelog.x86_64                                                             3:162-2.el8                                                              @anaconda
mcpp.x86_64                                                               2.7.2-20.el8                                                             @AppStream
mdadm.x86_64                                                              4.1-9.el8                                                                @anaconda
mesa-dri-drivers.x86_64                                                   19.1.4-3.el8_1                                                           @AppStream
mesa-filesystem.x86_64                                                    19.1.4-3.el8_1                                                           @AppStream
mesa-libEGL.x86_64                                                        19.1.4-3.el8_1                                                           @AppStream
mesa-libGL.x86_64                                                         19.1.4-3.el8_1                                                           @AppStream
mesa-libgbm.x86_64                                                        19.1.4-3.el8_1                                                           @AppStream
mesa-libglapi.x86_64                                                      19.1.4-3.el8_1                                                           @AppStream
mesa-libxatracker.x86_64                                                  19.1.4-3.el8_1                                                           @AppStream
metacity.x86_64                                                           3.28.0-1.el8                                                             @AppStream
microcode_ctl.x86_64                                                      4:20190618-1.20191115.3.el8_1                                            @BaseOS
mlocate.x86_64                                                            0.26-20.el8                                                              @anaconda
mobile-broadband-provider-info.noarch                                     1.20170310-1.el8                                                         @anaconda
mousetweaks.x86_64                                                        3.12.0-11.el8                                                            @AppStream
mozilla-filesystem.x86_64                                                 1.9-18.el8                                                               @AppStream
mozjs60.x86_64                                                            60.9.0-3.el8                                                             @anaconda
mpfr.x86_64                                                               3.1.6-1.el8                                                              @anaconda
mpg123-libs.x86_64                                                        1.25.10-2.el8                                                            @AppStream
mtdev.x86_64                                                              1.1.5-12.el8                                                             @AppStream
mtools.x86_64                                                             4.0.18-14.el8                                                            @anaconda
mtr.x86_64                                                                2:0.92-3.el8                                                             @anaconda
mutter.x86_64                                                             3.32.2-11.el8_1                                                          @AppStream
nano.x86_64                                                               2.9.8-1.el8                                                              @anaconda
nautilus.x86_64                                                           3.28.1-10.el8                                                            @AppStream
nautilus-extensions.x86_64                                                3.28.1-10.el8                                                            @AppStream
nautilus-sendto.x86_64                                                    1:3.8.6-2.el8                                                            @AppStream
ncompress.x86_64                                                          4.2.4.4-12.el8                                                           @AppStream
ncurses.x86_64                                                            6.1-7.20180224.el8                                                       @anaconda
ncurses-base.noarch                                                       6.1-7.20180224.el8                                                       @anaconda
ncurses-libs.x86_64                                                       6.1-7.20180224.el8                                                       @anaconda
ndctl.x86_64                                                              65-1.el8                                                                 @anaconda
ndctl-libs.x86_64                                                         65-1.el8                                                                 @anaconda
neon.x86_64                                                               0.30.2-6.el8                                                             @AppStream
net-snmp-libs.x86_64                                                      1:5.8-10.el8                                                             @anaconda
net-tools.x86_64                                                          2.0-0.51.20160912git.el8                                                 @anaconda
netcf-libs.x86_64                                                         0.2.8-12.module_el8.1.0+248+298dec18                                     @AppStream
nettle.x86_64                                                             3.4.1-1.el8                                                              @anaconda
newt.x86_64                                                               0.52.20-9.el8                                                            @anaconda
nfs-utils.x86_64                                                          1:2.3.3-26.el8                                                           @anaconda
nftables.x86_64                                                           1:0.9.0-14.el8                                                           @anaconda
nm-connection-editor.x86_64                                               1.8.22-2.el8                                                             @AppStream
nmap-ncat.x86_64                                                          2:7.70-5.el8                                                             @AppStream
npth.x86_64                                                               1.5-4.el8                                                                @anaconda
nspr.x86_64                                                               4.21.0-2.el8_0                                                           @AppStream
nss.x86_64                                                                3.44.0-9.el8_1                                                           @AppStream
nss-softokn.x86_64                                                        3.44.0-9.el8_1                                                           @AppStream
nss-softokn-freebl.x86_64                                                 3.44.0-9.el8_1                                                           @AppStream
nss-sysinit.x86_64                                                        3.44.0-9.el8_1                                                           @AppStream
nss-util.x86_64                                                           3.44.0-9.el8_1                                                           @AppStream
numactl-libs.x86_64                                                       2.0.12-7.el8                                                             @anaconda
numad.x86_64                                                              0.5-26.20150602git.el8                                                   @anaconda
oci-systemd-hook.x86_64                                                   1:0.1.15-2.git2d0b8a3.module_el8.1.0+237+63e26edc                        @AppStream
oddjob.x86_64                                                             0.34.4-7.el8                                                             @AppStream
oddjob-mkhomedir.x86_64                                                   0.34.4-7.el8                                                             @AppStream
open-vm-tools.x86_64                                                      10.3.10-3.el8_1.1                                                        @AppStream
open-vm-tools-desktop.x86_64                                              10.3.10-3.el8_1.1                                                        @AppStream
openjpeg2.x86_64                                                          2.3.1-1.el8                                                              @AppStream
openldap.x86_64                                                           2.4.46-10.el8                                                            @anaconda
openssh.x86_64                                                            8.0p1-3.el8                                                              @anaconda
openssh-clients.x86_64                                                    8.0p1-3.el8                                                              @anaconda
openssh-server.x86_64                                                     8.0p1-3.el8                                                              @anaconda
openssl.x86_64                                                            1:1.1.1c-2.el8                                                           @anaconda
openssl-libs.x86_64                                                       1:1.1.1c-2.el8                                                           @anaconda
openssl-pkcs11.x86_64                                                     0.4.8-2.el8                                                              @anaconda
opus.x86_64                                                               1.3-0.4.beta.el8                                                         @AppStream
orc.x86_64                                                                0.4.28-2.el8                                                             @AppStream
orca.noarch                                                               3.28.2-1.el8                                                             @AppStream
os-prober.x86_64                                                          1.74-6.el8                                                               @anaconda
osinfo-db.noarch                                                          20190611-1.el8                                                           @AppStream
osinfo-db-tools.x86_64                                                    1.5.0-4.el8                                                              @AppStream
ostree.x86_64                                                             2019.2-1.el8                                                             @AppStream
ostree-libs.x86_64                                                        2019.2-1.el8                                                             @AppStream
p11-kit.x86_64                                                            0.23.14-5.el8_0                                                          @anaconda
p11-kit-server.x86_64                                                     0.23.14-5.el8_0                                                          @anaconda
p11-kit-trust.x86_64                                                      0.23.14-5.el8_0                                                          @anaconda
pakchois.x86_64                                                           0.4-17.el8                                                               @AppStream
paktype-naskh-basic-fonts.noarch                                          4.1-9.el8                                                                @AppStream
pam.x86_64                                                                1.3.1-4.el8                                                              @anaconda
pango.x86_64                                                              1.42.4-6.el8                                                             @AppStream
pangomm.x86_64                                                            2.40.1-5.el8                                                             @AppStream
paps.x86_64                                                               0.6.8-41.el8                                                             @AppStream
paps-libs.x86_64                                                          0.6.8-41.el8                                                             @AppStream
paratype-pt-sans-fonts.noarch                                             20141121-6.el8                                                           @AppStream
parted.x86_64                                                             3.2-38.el8                                                               @anaconda
passwd.x86_64                                                             0.80-2.el8                                                               @anaconda
pcaudiolib.x86_64                                                         1.1-2.el8                                                                @AppStream
pciutils.x86_64                                                           3.5.6-4.el8                                                              @anaconda
pciutils-libs.x86_64                                                      3.5.6-4.el8                                                              @anaconda
pcre.x86_64                                                               8.42-4.el8                                                               @anaconda
pcre2.x86_64                                                              10.32-1.el8                                                              @anaconda
perl-Carp.noarch                                                          1.42-396.el8                                                             @anaconda
perl-DBD-SQLite.x86_64                                                    1.58-2.module_el8.1.0+207+bdacd7b7                                       @AppStream
perl-DBI.x86_64                                                           1.641-3.module_el8.1.0+199+8f0a6bbd                                      @AppStream
perl-Data-Dumper.x86_64                                                   2.167-399.el8                                                            @anaconda
perl-Digest.noarch                                                        1.17-395.el8                                                             @AppStream
perl-Digest-MD5.x86_64                                                    2.55-396.el8                                                             @AppStream
perl-Encode.x86_64                                                        4:2.97-3.el8                                                             @anaconda
perl-Errno.x86_64                                                         1.28-416.el8                                                             @anaconda
perl-Exporter.noarch                                                      5.72-396.el8                                                             @anaconda
perl-File-Path.noarch                                                     2.15-2.el8                                                               @anaconda
perl-File-Temp.noarch                                                     0.230.600-1.el8                                                          @anaconda
perl-Getopt-Long.noarch                                                   1:2.50-4.el8                                                             @anaconda
perl-HTTP-Tiny.noarch                                                     0.074-1.el8                                                              @anaconda
perl-IO.x86_64                                                            1.38-416.el8                                                             @anaconda
perl-IO-Socket-IP.noarch                                                  0.39-5.el8                                                               @AppStream
perl-IO-Socket-SSL.noarch                                                 2.066-3.el8                                                              @AppStream
perl-MIME-Base64.x86_64                                                   3.15-396.el8                                                             @anaconda
perl-Math-BigInt.noarch                                                   1:1.9998.11-7.el8                                                        @anaconda
perl-Math-Complex.noarch                                                  1.59-416.el8                                                             @anaconda
perl-Mozilla-CA.noarch                                                    20160104-7.el8                                                           @AppStream
perl-Net-SSLeay.x86_64                                                    1.88-1.el8                                                               @AppStream
perl-PathTools.x86_64                                                     3.74-1.el8                                                               @anaconda
perl-Pod-Escapes.noarch                                                   1:1.07-395.el8                                                           @anaconda
perl-Pod-Perldoc.noarch                                                   3.28-396.el8                                                             @anaconda
perl-Pod-Simple.noarch                                                    1:3.35-395.el8                                                           @anaconda
perl-Pod-Usage.noarch                                                     4:1.69-395.el8                                                           @anaconda
perl-Scalar-List-Utils.x86_64                                             3:1.49-2.el8                                                             @anaconda
perl-Socket.x86_64                                                        4:2.027-3.el8                                                            @anaconda
perl-Storable.x86_64                                                      1:3.11-3.el8                                                             @anaconda
perl-Term-ANSIColor.noarch                                                4.06-396.el8                                                             @anaconda
perl-Term-Cap.noarch                                                      1.17-395.el8                                                             @anaconda
perl-Text-ParseWords.noarch                                               3.30-395.el8                                                             @anaconda
perl-Text-Tabs+Wrap.noarch                                                2013.0523-395.el8                                                        @anaconda
perl-Time-Local.noarch                                                    1:1.280-1.el8                                                            @anaconda
perl-URI.noarch                                                           1.73-3.el8                                                               @AppStream
perl-Unicode-Normalize.x86_64                                             1.25-396.el8                                                             @anaconda
perl-constant.noarch                                                      1.33-396.el8                                                             @anaconda
perl-interpreter.x86_64                                                   4:5.26.3-416.el8                                                         @anaconda
perl-libnet.noarch                                                        3.11-3.el8                                                               @AppStream
perl-libs.x86_64                                                          4:5.26.3-416.el8                                                         @anaconda
perl-macros.x86_64                                                        4:5.26.3-416.el8                                                         @anaconda
perl-parent.noarch                                                        1:0.237-1.el8                                                            @anaconda
perl-podlators.noarch                                                     4.11-1.el8                                                               @anaconda
perl-threads.x86_64                                                       1:2.21-2.el8                                                             @anaconda
perl-threads-shared.x86_64                                                1.58-2.el8                                                               @anaconda
pigz.x86_64                                                               2.4-2.el8                                                                @anaconda
pinentry.x86_64                                                           1.1.0-2.el8                                                              @AppStream
pinentry-gtk.x86_64                                                       1.1.0-2.el8                                                              @AppStream
pinfo.x86_64                                                              0.6.10-18.el8                                                            @AppStream
pipewire.x86_64                                                           0.2.5-1.el8                                                              @AppStream
pipewire-libs.x86_64                                                      0.2.5-1.el8                                                              @AppStream
pixman.x86_64                                                             0.36.0-1.el8                                                             @AppStream
pkgconf.x86_64                                                            1.4.2-1.el8                                                              @anaconda
pkgconf-m4.noarch                                                         1.4.2-1.el8                                                              @anaconda
pkgconf-pkg-config.x86_64                                                 1.4.2-1.el8                                                              @anaconda
platform-python.x86_64                                                    3.6.8-15.1.el8                                                           @anaconda
platform-python-coverage.x86_64                                           4.5.1-7.el8                                                              @AppStream
platform-python-pip.noarch                                                9.0.3-15.el8                                                             @anaconda
platform-python-setuptools.noarch                                         39.2.0-5.el8                                                             @anaconda
plymouth.x86_64                                                           0.9.3-15.el8                                                             @AppStream
plymouth-core-libs.x86_64                                                 0.9.3-15.el8                                                             @AppStream
plymouth-graphics-libs.x86_64                                             0.9.3-15.el8                                                             @AppStream
plymouth-plugin-label.x86_64                                              0.9.3-15.el8                                                             @AppStream
plymouth-plugin-two-step.x86_64                                           0.9.3-15.el8                                                             @AppStream
plymouth-scripts.x86_64                                                   0.9.3-15.el8                                                             @AppStream
plymouth-system-theme.x86_64                                              0.9.3-15.el8                                                             @AppStream
plymouth-theme-charge.x86_64                                              0.9.3-15.el8                                                             @AppStream
pnm2ppa.x86_64                                                            1:1.04-40.el8                                                            @AppStream
podman.x86_64                                                             1.4.2-5.module_el8.1.0+237+63e26edc                                      @AppStream
podman-manpages.noarch                                                    1.4.2-5.module_el8.1.0+237+63e26edc                                      @AppStream
policycoreutils.x86_64                                                    2.9-3.el8                                                                @anaconda
policycoreutils-python-utils.noarch                                       2.9-3.el8                                                                @anaconda
polkit.x86_64                                                             0.115-9.el8                                                              @anaconda
polkit-libs.x86_64                                                        0.115-9.el8                                                              @anaconda
polkit-pkla-compat.x86_64                                                 0.1-12.el8                                                               @anaconda
poppler.x86_64                                                            0.66.0-26.el8                                                            @AppStream
poppler-data.noarch                                                       0.4.9-1.el8                                                              @AppStream
poppler-glib.x86_64                                                       0.66.0-26.el8                                                            @AppStream
poppler-utils.x86_64                                                      0.66.0-26.el8                                                            @AppStream
popt.x86_64                                                               1.16-14.el8                                                              @anaconda
prefixdevname.x86_64                                                      0.1.0-6.el8                                                              @anaconda
procps-ng.x86_64                                                          3.3.15-1.el8                                                             @anaconda
protobuf-c.x86_64                                                         1.3.0-4.el8                                                              @AppStream
psacct.x86_64                                                             6.6.3-4.el8                                                              @anaconda
psmisc.x86_64                                                             23.1-3.el8                                                               @anaconda
publicsuffix-list-dafsa.noarch                                            20180723-1.el8                                                           @anaconda
pulseaudio.x86_64                                                         11.1-23.el8                                                              @AppStream
pulseaudio-libs.x86_64                                                    11.1-23.el8                                                              @AppStream
pulseaudio-libs-glib2.x86_64                                              11.1-23.el8                                                              @AppStream
pulseaudio-module-bluetooth.x86_64                                        11.1-23.el8                                                              @AppStream
pulseaudio-module-x11.x86_64                                              11.1-23.el8                                                              @AppStream
pulseaudio-utils.x86_64                                                   11.1-23.el8                                                              @AppStream
python3-asn1crypto.noarch                                                 0.24.0-3.el8                                                             @anaconda
python3-audit.x86_64                                                      3.0-0.10.20180831git0047a6c.el8                                          @anaconda
python3-bind.noarch                                                       32:9.11.4-26.P2.el8                                                      @AppStream
python3-blivet.noarch                                                     1:3.1.0-17.el8                                                           @AppStream
python3-blockdev.x86_64                                                   2.19-9.el8                                                               @AppStream
python3-brlapi.x86_64                                                     0.6.7-28.el8                                                             @AppStream
python3-bytesize.x86_64                                                   1.4-1.el8                                                                @AppStream
python3-cairo.x86_64                                                      1.16.3-6.el8                                                             @AppStream
python3-cffi.x86_64                                                       1.11.5-5.el8                                                             @anaconda
python3-chardet.noarch                                                    3.0.4-7.el8                                                              @anaconda
python3-configobj.noarch                                                  5.0.6-11.el8                                                             @anaconda
python3-cryptography.x86_64                                               2.3-2.el8                                                                @anaconda
python3-cups.x86_64                                                       1.9.72-21.el8.0.1                                                        @AppStream
python3-dateutil.noarch                                                   1:2.6.1-6.el8                                                            @anaconda
python3-dbus.x86_64                                                       1.2.4-15.el8                                                             @anaconda
python3-decorator.noarch                                                  4.2.1-2.el8                                                              @anaconda
python3-dmidecode.x86_64                                                  3.12.2-15.el8                                                            @anaconda
python3-dnf.noarch                                                        4.2.7-7.el8_1                                                            @BaseOS
python3-dnf-plugin-spacewalk.noarch                                       2.8.5-11.module_el8.1.0+211+ad6c0bc7                                     @AppStream
python3-dnf-plugins-core.noarch                                           4.0.8-3.el8                                                              @anaconda
python3-firewall.noarch                                                   0.7.0-5.el8                                                              @anaconda
python3-gobject.x86_64                                                    3.28.3-1.el8                                                             @AppStream
python3-gobject-base.x86_64                                               3.28.3-1.el8                                                             @anaconda
python3-gpg.x86_64                                                        1.10.0-6.el8.0.1                                                         @anaconda
python3-hawkey.x86_64                                                     0.35.1-9.el8_1                                                           @BaseOS
python3-hwdata.noarch                                                     2.3.6-3.el8                                                              @AppStream
python3-idna.noarch                                                       2.5-5.el8                                                                @anaconda
python3-kickstart.noarch                                                  3.16.7-1.el8                                                             @AppStream
python3-langtable.noarch                                                  0.0.38-5.el8                                                             @AppStream
python3-libcomps.x86_64                                                   0.1.11-2.el8                                                             @anaconda
python3-libdnf.x86_64                                                     0.35.1-9.el8_1                                                           @BaseOS
python3-librepo.x86_64                                                    1.10.3-3.el8                                                             @anaconda
python3-libreport.x86_64                                                  2.9.5-9.el8                                                              @AppStream
python3-libs.x86_64                                                       3.6.8-15.1.el8                                                           @anaconda
python3-libselinux.x86_64                                                 2.9-2.1.el8                                                              @anaconda
python3-libsemanage.x86_64                                                2.9-1.el8                                                                @anaconda
python3-libstoragemgmt.noarch                                             1.8.1-2.el8                                                              @anaconda
python3-libstoragemgmt-clibs.x86_64                                       1.8.1-2.el8                                                              @anaconda
python3-libxml2.x86_64                                                    2.9.7-5.el8                                                              @anaconda
python3-linux-procfs.noarch                                               0.6-7.el8                                                                @anaconda
python3-louis.noarch                                                      2.6.2-16.el8                                                             @AppStream
python3-meh.noarch                                                        0.47.2-1.el8                                                             @AppStream
python3-meh-gui.noarch                                                    0.47.2-1.el8                                                             @AppStream
python3-netifaces.x86_64                                                  0.10.6-4.el8                                                             @AppStream
python3-newt.x86_64                                                       0.52.20-9.el8                                                            @AppStream
python3-ntplib.noarch                                                     0.3.3-10.el8                                                             @AppStream
python3-ordered-set.noarch                                                2.0.2-4.el8                                                              @AppStream
python3-perf.x86_64                                                       4.18.0-147.3.1.el8_1                                                     @BaseOS
python3-pid.noarch                                                        2.1.1-7.el8                                                              @AppStream
python3-pip.noarch                                                        9.0.3-15.el8                                                             @AppStream
python3-pip-wheel.noarch                                                  9.0.3-15.el8                                                             @anaconda
python3-ply.noarch                                                        3.9-7.el8                                                                @anaconda
python3-policycoreutils.noarch                                            2.9-3.el8                                                                @anaconda
python3-productmd.noarch                                                  1.11-3.el8                                                               @AppStream
python3-pwquality.x86_64                                                  1.4.0-9.el8                                                              @anaconda
python3-pyOpenSSL.noarch                                                  18.0.0-1.el8                                                             @AppStream
python3-pyatspi.noarch                                                    2.26.0-6.el8                                                             @AppStream
python3-pycparser.noarch                                                  2.14-14.el8                                                              @anaconda
python3-pycurl.x86_64                                                     7.43.0.2-3.el8                                                           @AppStream
python3-pydbus.noarch                                                     0.6.0-5.el8                                                              @AppStream
python3-pyparted.x86_64                                                   1:3.11.0-13.el8                                                          @AppStream
python3-pysocks.noarch                                                    1.6.8-3.el8                                                              @anaconda
python3-pytz.noarch                                                       2017.2-9.el8                                                             @AppStream
python3-pyudev.noarch                                                     0.21.0-7.el8                                                             @anaconda
python3-pyxdg.noarch                                                      0.25-16.el8                                                              @AppStream
python3-pyyaml.x86_64                                                     3.12-12.el8                                                              @anaconda
python3-requests.noarch                                                   2.20.0-2.1.el8_1                                                         @BaseOS
python3-requests-file.noarch                                              1.4.3-5.el8                                                              @AppStream
python3-requests-ftp.noarch                                               0.3.1-11.el8                                                             @AppStream
python3-rhn-client-tools.x86_64                                           2.8.16-13.module_el8.1.0+211+ad6c0bc7                                    @AppStream
python3-rhnlib.noarch                                                     2.8.6-8.module_el8.1.0+211+ad6c0bc7                                      @AppStream
python3-rpm.x86_64                                                        4.14.2-25.el8                                                            @anaconda
python3-schedutils.x86_64                                                 0.6-6.el8                                                                @anaconda
python3-setools.x86_64                                                    4.2.2-1.el8                                                              @anaconda
python3-setuptools.noarch                                                 39.2.0-5.el8                                                             @anaconda
python3-setuptools-wheel.noarch                                           39.2.0-5.el8                                                             @anaconda
python3-simpleline.noarch                                                 1.1-2.el8                                                                @AppStream
python3-six.noarch                                                        1.11.0-8.el8                                                             @anaconda
python3-slip.noarch                                                       0.6.4-11.el8                                                             @anaconda
python3-slip-dbus.noarch                                                  0.6.4-11.el8                                                             @anaconda
python3-speechd.x86_64                                                    0.8.8-6.el8                                                              @AppStream
python3-sssdconfig.noarch                                                 2.2.0-19.el8                                                             @anaconda
python3-syspurpose.x86_64                                                 1.25.17-1.el8                                                            @anaconda
python3-systemd.x86_64                                                    234-8.el8                                                                @AppStream
python3-unbound.x86_64                                                    1.7.3-8.el8                                                              @AppStream
python3-urllib3.noarch                                                    1.24.2-2.el8                                                             @anaconda
python36.x86_64                                                           3.6.8-2.module_el8.1.0+245+c39af44f                                      @AppStream
qemu-guest-agent.x86_64                                                   15:2.12.0-88.module_el8.1.0+258+1d2a1d58.1                               @AppStream
qemu-img.x86_64                                                           15:2.12.0-88.module_el8.1.0+258+1d2a1d58.1                               @AppStream
qemu-kvm.x86_64                                                           15:2.12.0-88.module_el8.1.0+258+1d2a1d58.1                               @AppStream
qemu-kvm-block-curl.x86_64                                                15:2.12.0-88.module_el8.1.0+258+1d2a1d58.1                               @AppStream
qemu-kvm-block-gluster.x86_64                                             15:2.12.0-88.module_el8.1.0+258+1d2a1d58.1                               @AppStream
qemu-kvm-block-iscsi.x86_64                                               15:2.12.0-88.module_el8.1.0+258+1d2a1d58.1                               @AppStream
qemu-kvm-block-rbd.x86_64                                                 15:2.12.0-88.module_el8.1.0+258+1d2a1d58.1                               @AppStream
qemu-kvm-block-ssh.x86_64                                                 15:2.12.0-88.module_el8.1.0+258+1d2a1d58.1                               @AppStream
qemu-kvm-common.x86_64                                                    15:2.12.0-88.module_el8.1.0+258+1d2a1d58.1                               @AppStream
qemu-kvm-core.x86_64                                                      15:2.12.0-88.module_el8.1.0+258+1d2a1d58.1                               @AppStream
qpdf-libs.x86_64                                                          7.1.1-10.el8                                                             @AppStream
quota.x86_64                                                              1:4.04-10.el8                                                            @anaconda
quota-nls.noarch                                                          1:4.04-10.el8                                                            @anaconda
radvd.x86_64                                                              2.17-12.el8                                                              @AppStream
rarian.x86_64                                                             0.8.1-19.el8                                                             @AppStream
rarian-compat.x86_64                                                      0.8.1-19.el8                                                             @AppStream
rasdaemon.x86_64                                                          0.6.1-2.el8                                                              @anaconda
rdma-core.x86_64                                                          22.3-1.el8                                                               @anaconda
readline.x86_64                                                           7.0-10.el8                                                               @anaconda
realmd.x86_64                                                             0.16.3-16.el8                                                            @anaconda
redhat-menus.noarch                                                       12.0.2-12.el8                                                            @AppStream
rest.x86_64                                                               0.8.1-2.el8                                                              @AppStream
rhn-client-tools.x86_64                                                   2.8.16-13.module_el8.1.0+211+ad6c0bc7                                    @AppStream
rhsm-gtk.x86_64                                                           1.25.17-1.el8                                                            @AppStream
rng-tools.x86_64                                                          6.6-2.el8                                                                @anaconda
rootfiles.noarch                                                          8.1-22.el8                                                               @anaconda
rpcbind.x86_64                                                            1.2.5-4.el8                                                              @anaconda
rpm.x86_64                                                                4.14.2-25.el8                                                            @anaconda
rpm-build-libs.x86_64                                                     4.14.2-25.el8                                                            @anaconda
rpm-libs.x86_64                                                           4.14.2-25.el8                                                            @anaconda
rpm-ostree-libs.x86_64                                                    2019.3-3.el8                                                             @AppStream
rpm-plugin-selinux.x86_64                                                 4.14.2-25.el8                                                            @anaconda
rpm-plugin-systemd-inhibit.x86_64                                         4.14.2-25.el8                                                            @anaconda
rsync.x86_64                                                              3.1.3-6.el8                                                              @anaconda
rsyslog.x86_64                                                            8.37.0-13.el8                                                            @AppStream
rsyslog-gnutls.x86_64                                                     8.37.0-13.el8                                                            @AppStream
rsyslog-gssapi.x86_64                                                     8.37.0-13.el8                                                            @AppStream
rsyslog-relp.x86_64                                                       8.37.0-13.el8                                                            @AppStream
rtkit.x86_64                                                              0.11-19.el8                                                              @AppStream
runc.x86_64                                                               1.0.0-60.rc8.module_el8.1.0+237+63e26edc                                 @AppStream
samba-client-libs.x86_64                                                  4.10.4-101.el8_1                                                         @BaseOS
samba-common.noarch                                                       4.10.4-101.el8_1                                                         @BaseOS
samba-common-libs.x86_64                                                  4.10.4-101.el8_1                                                         @BaseOS
sane-backends.x86_64                                                      1.0.27-19.el8                                                            @AppStream
sane-backends-drivers-cameras.x86_64                                      1.0.27-19.el8                                                            @AppStream
sane-backends-drivers-scanners.x86_64                                     1.0.27-19.el8                                                            @AppStream
sane-backends-libs.x86_64                                                 1.0.27-19.el8                                                            @AppStream
satyr.x86_64                                                              0.26-2.el8                                                               @AppStream
sbc.x86_64                                                                1.3-9.el8                                                                @AppStream
seabios-bin.noarch                                                        1.11.1-4.module_el8.1.0+248+298dec18                                     @AppStream
seavgabios-bin.noarch                                                     1.11.1-4.module_el8.1.0+248+298dec18                                     @AppStream
sed.x86_64                                                                4.5-1.el8                                                                @anaconda
selinux-policy.noarch                                                     3.14.3-20.el8                                                            @anaconda
selinux-policy-targeted.noarch                                            3.14.3-20.el8                                                            @anaconda
setroubleshoot-plugins.noarch                                             3.3.10-3.el8                                                             @AppStream
setroubleshoot-server.x86_64                                              3.3.20-2.el8                                                             @AppStream
setup.noarch                                                              2.12.2-2.el8_1.1                                                         @BaseOS
sg3_utils.x86_64                                                          1.44-3.el8                                                               @anaconda
sg3_utils-libs.x86_64                                                     1.44-3.el8                                                               @anaconda
sgabios-bin.noarch                                                        1:0.20170427git-3.module_el8.1.0+248+298dec18                            @AppStream
shadow-utils.x86_64                                                       2:4.6-8.el8                                                              @anaconda
shared-mime-info.x86_64                                                   1.9-3.el8                                                                @anaconda
sil-abyssinica-fonts.noarch                                               1.200-13.el8                                                             @AppStream
sil-nuosu-fonts.noarch                                                    2.1.1-14.el8                                                             @AppStream
sil-padauk-fonts.noarch                                                   3.003-1.el8                                                              @AppStream
slang.x86_64                                                              2.3.2-3.el8                                                              @anaconda
slirp4netns.x86_64                                                        0.3.0-4.module_el8.1.0+237+63e26edc                                      @AppStream
smartmontools.x86_64                                                      1:6.6-3.el8                                                              @anaconda
smc-fonts-common.noarch                                                   6.1-10.el8                                                               @AppStream
smc-meera-fonts.noarch                                                    6.1-10.el8                                                               @AppStream
snappy.x86_64                                                             1.1.7-5.el8                                                              @anaconda
sos.noarch                                                                3.7-8.el8_1                                                              @BaseOS
sound-theme-freedesktop.noarch                                            0.8-9.el8                                                                @AppStream
soundtouch.x86_64                                                         2.0.0-2.el8                                                              @AppStream
speech-dispatcher.x86_64                                                  0.8.8-6.el8                                                              @AppStream
speech-dispatcher-espeak-ng.x86_64                                        0.8.8-6.el8                                                              @AppStream
speex.x86_64                                                              1.2.0-1.el8                                                              @AppStream
speexdsp.x86_64                                                           1.2-0.13.rc3.el8                                                         @AppStream
spice-glib.x86_64                                                         0.37-1.el8                                                               @AppStream
spice-gtk3.x86_64                                                         0.37-1.el8                                                               @AppStream
spice-server.x86_64                                                       0.14.2-1.el8                                                             @AppStream
spice-vdagent.x86_64                                                      0.19.0-3.el8                                                             @AppStream
sqlite.x86_64                                                             3.26.0-3.el8                                                             @anaconda
sqlite-libs.x86_64                                                        3.26.0-3.el8                                                             @anaconda
squashfs-tools.x86_64                                                     4.3-19.el8                                                               @anaconda
sscg.x86_64                                                               2.3.3-6.el8                                                              @AppStream
sssd.x86_64                                                               2.2.0-19.el8                                                             @anaconda
sssd-ad.x86_64                                                            2.2.0-19.el8                                                             @anaconda
sssd-client.x86_64                                                        2.2.0-19.el8                                                             @anaconda
sssd-common.x86_64                                                        2.2.0-19.el8                                                             @anaconda
sssd-common-pac.x86_64                                                    2.2.0-19.el8                                                             @anaconda
sssd-ipa.x86_64                                                           2.2.0-19.el8                                                             @anaconda
sssd-kcm.x86_64                                                           2.2.0-19.el8                                                             @anaconda
sssd-krb5.x86_64                                                          2.2.0-19.el8                                                             @anaconda
sssd-krb5-common.x86_64                                                   2.2.0-19.el8                                                             @anaconda
sssd-ldap.x86_64                                                          2.2.0-19.el8                                                             @anaconda
sssd-nfs-idmap.x86_64                                                     2.2.0-19.el8                                                             @anaconda
sssd-proxy.x86_64                                                         2.2.0-19.el8                                                             @anaconda
startup-notification.x86_64                                               0.12-15.el8                                                              @AppStream
stix-fonts.noarch                                                         1.1.0-12.el8                                                             @AppStream
strace.x86_64                                                             4.24-5.el8                                                               @anaconda
stress.x86_64                                                             1.0.4-23.el8                                                             @System
subscription-manager-initial-setup-addon.x86_64                           1.25.17-1.el8                                                            @AppStream
sudo.x86_64                                                               1.8.25p1-8.el8_1                                                         @BaseOS
sushi.x86_64                                                              3.28.3-1.el8                                                             @AppStream
switcheroo-control.x86_64                                                 1.1-5.el8                                                                @AppStream
symlinks.x86_64                                                           1.4-19.el8                                                               @anaconda
system-config-printer-libs.noarch                                         1.5.11-13.el8                                                            @AppStream
system-config-printer-udev.x86_64                                         1.5.11-13.el8                                                            @AppStream
systemd.x86_64                                                            239-18.el8_1.1                                                           @BaseOS
systemd-container.x86_64                                                  239-18.el8_1.1                                                           @BaseOS
systemd-libs.x86_64                                                       239-18.el8_1.1                                                           @BaseOS
systemd-pam.x86_64                                                        239-18.el8_1.1                                                           @BaseOS
systemd-udev.x86_64                                                       239-18.el8_1.1                                                           @BaseOS
taglib.x86_64                                                             1.11.1-8.el8                                                             @AppStream
tar.x86_64                                                                2:1.30-4.el8                                                             @anaconda
tcpdump.x86_64                                                            14:4.9.2-5.el8                                                           @AppStream
teamd.x86_64                                                              1.28-4.el8                                                               @anaconda
thai-scalable-fonts-common.noarch                                         0.6.5-1.el8                                                              @AppStream
thai-scalable-waree-fonts.noarch                                          0.6.5-1.el8                                                              @AppStream
tigervnc-license.noarch                                                   1.9.0-10.el8                                                             @AppStream
tigervnc-server-minimal.x86_64                                            1.9.0-10.el8                                                             @AppStream
time.x86_64                                                               1.9-3.el8                                                                @anaconda
timedatex.x86_64                                                          0.5-3.el8                                                                @anaconda
totem.x86_64                                                              1:3.26.2-1.el8                                                           @AppStream
totem-nautilus.x86_64                                                     1:3.26.2-1.el8                                                           @AppStream
totem-pl-parser.x86_64                                                    3.26.1-2.el8                                                             @AppStream
tpm2-tools.x86_64                                                         3.1.4-5.el8                                                              @anaconda
tpm2-tss.x86_64                                                           2.0.0-4.el8                                                              @anaconda
tracker.x86_64                                                            2.1.5-1.el8                                                              @AppStream
tracker-miners.x86_64                                                     2.1.5-1.el8                                                              @AppStream
tree.x86_64                                                               1.7.0-15.el8                                                             @anaconda
trousers.x86_64                                                           0.3.14-4.el8                                                             @anaconda
trousers-lib.x86_64                                                       0.3.14-4.el8                                                             @anaconda
tuned.noarch                                                              2.12.0-3.el8                                                             @anaconda
twolame-libs.x86_64                                                       0.3.13-11.el8                                                            @AppStream
tzdata.noarch                                                             2019c-1.el8                                                              @anaconda
udisks2.x86_64                                                            2.8.3-2.el8                                                              @AppStream
udisks2-iscsi.x86_64                                                      2.8.3-2.el8                                                              @AppStream
udisks2-lvm2.x86_64                                                       2.8.3-2.el8                                                              @AppStream
unbound-libs.x86_64                                                       1.7.3-8.el8                                                              @AppStream
unzip.x86_64                                                              6.0-41.el8                                                               @anaconda
upower.x86_64                                                             0.99.7-3.el8                                                             @AppStream
urw-base35-bookman-fonts.noarch                                           20170801-10.el8                                                          @AppStream
urw-base35-c059-fonts.noarch                                              20170801-10.el8                                                          @AppStream
urw-base35-d050000l-fonts.noarch                                          20170801-10.el8                                                          @AppStream
urw-base35-fonts.noarch                                                   20170801-10.el8                                                          @AppStream
urw-base35-fonts-common.noarch                                            20170801-10.el8                                                          @AppStream
urw-base35-gothic-fonts.noarch                                            20170801-10.el8                                                          @AppStream
urw-base35-nimbus-mono-ps-fonts.noarch                                    20170801-10.el8                                                          @AppStream
urw-base35-nimbus-roman-fonts.noarch                                      20170801-10.el8                                                          @AppStream
urw-base35-nimbus-sans-fonts.noarch                                       20170801-10.el8                                                          @AppStream
urw-base35-p052-fonts.noarch                                              20170801-10.el8                                                          @AppStream
urw-base35-standard-symbols-ps-fonts.noarch                               20170801-10.el8                                                          @AppStream
urw-base35-z003-fonts.noarch                                              20170801-10.el8                                                          @AppStream
usb_modeswitch.x86_64                                                     2.5.2-1.el8                                                              @anaconda
usb_modeswitch-data.noarch                                                20170806-2.el8                                                           @anaconda
usbmuxd.x86_64                                                            1.1.0-13.el8                                                             @AppStream
usbredir.x86_64                                                           0.8.0-1.el8                                                              @AppStream
usbutils.x86_64                                                           010-3.el8                                                                @anaconda
usermode.x86_64                                                           1.113-1.el8                                                              @anaconda
usermode-gtk.x86_64                                                       1.113-1.el8                                                              @AppStream
userspace-rcu.x86_64                                                      0.10.1-2.el8                                                             @anaconda
util-linux.x86_64                                                         2.32.1-17.el8                                                            @anaconda
util-linux-user.x86_64                                                    2.32.1-17.el8                                                            @anaconda
vdo.x86_64                                                                6.2.1.134-11.el8                                                         @anaconda
vim-common.x86_64                                                         2:8.0.1763-13.el8                                                        @AppStream
vim-enhanced.x86_64                                                       2:8.0.1763-13.el8                                                        @AppStream
vim-filesystem.noarch                                                     2:8.0.1763-13.el8                                                        @AppStream
vim-minimal.x86_64                                                        2:8.0.1763-13.el8                                                        @anaconda
vino.x86_64                                                               3.22.0-10.el8                                                            @AppStream
virt-what.x86_64                                                          1.18-6.el8                                                               @anaconda
volume_key-libs.x86_64                                                    0.3.11-5.el8                                                             @AppStream
vte-profile.x86_64                                                        0.52.2-2.el8                                                             @AppStream
vte291.x86_64                                                             0.52.2-2.el8                                                             @AppStream
wavpack.x86_64                                                            5.1.0-9.el8                                                              @AppStream
webkit2gtk3.x86_64                                                        2.24.4-2.el8_1                                                           @AppStream
webkit2gtk3-jsc.x86_64                                                    2.24.4-2.el8_1                                                           @AppStream
webkit2gtk3-plugin-process-gtk2.x86_64                                    2.24.4-2.el8_1                                                           @AppStream
webrtc-audio-processing.x86_64                                            0.3-8.el8                                                                @AppStream
wget.x86_64                                                               1.19.5-8.el8_1.1                                                         @AppStream
which.x86_64                                                              2.21-10.el8                                                              @anaconda
woff2.x86_64                                                              1.0.2-4.el8                                                              @AppStream
words.noarch                                                              3.0-28.el8                                                               @anaconda
wpa_supplicant.x86_64                                                     1:2.7-1.el8                                                              @anaconda
xcb-util.x86_64                                                           0.4.0-10.el8                                                             @AppStream
xdg-desktop-portal.x86_64                                                 1.0.3-1.el8                                                              @AppStream
xdg-desktop-portal-gtk.x86_64                                             1.0.2-1.el8                                                              @AppStream
xdg-user-dirs.x86_64                                                      0.17-1.el8                                                               @AppStream
xdg-user-dirs-gtk.x86_64                                                  0.10-13.el8                                                              @AppStream
xdg-utils.noarch                                                          1.1.2-5.el8                                                              @AppStream
xfsdump.x86_64                                                            3.1.8-2.el8                                                              @anaconda
xfsprogs.x86_64                                                           5.0.0-1.el8                                                              @anaconda
xkeyboard-config.noarch                                                   2.24-3.el8                                                               @AppStream
xml-common.noarch                                                         0.6.3-50.el8                                                             @anaconda
xmlrpc-c.x86_64                                                           1.51.0-5.el8                                                             @anaconda
xmlrpc-c-client.x86_64                                                    1.51.0-5.el8                                                             @anaconda
xmlsec1.x86_64                                                            1.2.25-4.el8                                                             @AppStream
xmlsec1-openssl.x86_64                                                    1.2.25-4.el8                                                             @AppStream
xorg-x11-drv-ati.x86_64                                                   19.0.1-1.el8                                                             @AppStream
xorg-x11-drv-evdev.x86_64                                                 2.10.6-2.el8                                                             @AppStream
xorg-x11-drv-fbdev.x86_64                                                 0.5.0-2.el8                                                              @AppStream
xorg-x11-drv-intel.x86_64                                                 2.99.917-38.20180618.el8                                                 @AppStream
xorg-x11-drv-libinput.x86_64                                              0.28.0-2.el8                                                             @AppStream
xorg-x11-drv-nouveau.x86_64                                               1:1.0.15-4.el8.1                                                         @AppStream
xorg-x11-drv-qxl.x86_64                                                   0.1.5-9.el8                                                              @AppStream
xorg-x11-drv-vesa.x86_64                                                  2.4.0-3.el8                                                              @AppStream
xorg-x11-drv-vmware.x86_64                                                13.2.1-8.el8                                                             @AppStream
xorg-x11-drv-wacom.x86_64                                                 0.36.1-5.el8                                                             @AppStream
xorg-x11-drv-wacom-serial-support.x86_64                                  0.36.1-5.el8                                                             @AppStream
xorg-x11-font-utils.x86_64                                                1:7.5-40.el8                                                             @AppStream
xorg-x11-server-Xorg.x86_64                                               1.20.3-8.el8                                                             @AppStream
xorg-x11-server-Xwayland.x86_64                                           1.20.3-8.el8                                                             @AppStream
xorg-x11-server-common.x86_64                                             1.20.3-8.el8                                                             @AppStream
xorg-x11-server-utils.x86_64                                              7.7-27.el8                                                               @AppStream
xorg-x11-utils.x86_64                                                     7.5-28.el8                                                               @AppStream
xorg-x11-xauth.x86_64                                                     1:1.0.9-12.el8                                                           @AppStream
xorg-x11-xinit.x86_64                                                     1.3.4-18.el8                                                             @AppStream
xorg-x11-xinit-session.x86_64                                             1.3.4-18.el8                                                             @AppStream
xorg-x11-xkb-utils.x86_64                                                 7.7-27.el8                                                               @AppStream
xz.x86_64                                                                 5.2.4-3.el8                                                              @anaconda
xz-libs.x86_64                                                            5.2.4-3.el8                                                              @anaconda
yajl.x86_64                                                               2.1.0-10.el8                                                             @AppStream
yelp.x86_64                                                               2:3.28.1-3.el8                                                           @AppStream
yelp-libs.x86_64                                                          2:3.28.1-3.el8                                                           @AppStream
yelp-tools.noarch                                                         3.28.0-3.el8                                                             @AppStream
yelp-xsl.noarch                                                           3.28.0-2.el8                                                             @AppStream
yum.noarch                                                                4.2.7-7.el8_1                                                            @BaseOS
zenity.x86_64                                                             3.28.1-1.el8                                                             @AppStream
zip.x86_64                                                                3.0-23.el8                                                               @anaconda
zlib.x86_64                                                               1.2.11-10.el8                                                            @anaconda
</pre>
</div>
</details>
{{< /accordion >}}

4.dnfコマンドでアップデートパッケージの一覧を確認してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
# dnf check-update
メタデータの期限切れの最終確認: 0:24:04 時間前の 2020年02月02日 23時38分17秒 に実施しました。
</pre>
</div>
</details>
{{< /accordion >}}