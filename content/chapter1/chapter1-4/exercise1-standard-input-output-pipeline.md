---
title: "Exercise1 Standard input/output & Pipeline"
date: 2017-10-17T15:26:15Z
draft: false
weight: 10
---

## 1.標準入力、標準出力、標準エラー出力の確認

### 1.カレントディレクトリをホームディレクトリに変更してください。

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

### 2.catコマンドとリダイレクト機能を使って、cloud.txtというファイルをホームディレクトリに作成してください。

ファイルの内容は次の3行です。作成後、catコマンドで確認してください。
aws
gcp
azure

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ cat > cloud.txt
aws //[enterキー]
gcp //[enterキー]
azure //[enterキー]
//[Ctrl]+[D]終了
</pre>

<pre>
$ cat cloud.txt
aws
gcp
azure
</pre>
</div>
</details>
{{< /accordion >}}

### 3.catコマンドとリダイレクト機能を使って、2.で作成したcloud.txtの4行目以降に、次の3行を追記してください。また、catコマンドで追記できたことを確認してください。

oracle cloud
IBM cloud
digital ocean

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ cat >> cloud.txt
oracle cloud //[enterキー]
IBM cloud //[enterキー]
digital ocean //[enterキー]
//[Ctrl]+[D]終了
</pre>

<pre>
$ cat cloud.txt
aws
gcp
azure
oracle cloud
IBM cloud
digital ocean
</pre>
</div>
</details>
{{< /accordion >}}

### 4.cloud.txtの内容を画面表示してください。このとき、cloudベンダーの名称がアルファベットの順と逆順に並べ替えられた状態で表示してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ cat cloud.txt | sort
IBM cloud
aws
azure
digital ocean
gcp
oracle cloud
</pre>

<pre>
$ cat cloud.txt | sort -r
oracle cloud
gcp
digital ocean
azure
aws
IBM cloud
</pre>
</div>
</details>
{{< /accordion >}}

### 5.findコマンドを使って、/etc から拡張子が.txtのファイルを検索してください。パーミッションがないため、「許可がありません」と表示されるファイルがあります。なので、リダイレクト機能を利用して、エラー内容が表示されないようにしてみましょう。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ find /etc -name '*.txt'
/etc/pki/nssdb/pkcs11.txt
find: ‘/etc/pki/rsyslog’: 許可がありません
find: ‘/etc/grub.d’: 許可がありません
find: ‘/etc/lvm/archive’: 許可がありません
find: ‘/etc/lvm/backup’: 許可がありません
find: ‘/etc/lvm/cache’: 許可がありません
find: ‘/etc/dhcp’: 許可がありません
find: ‘/etc/nftables’: 許可がありません
find: ‘/etc/cups/ssl’: 許可がありません
find: ‘/etc/sssd’: 許可がありません
find: ‘/etc/polkit-1/rules.d’: 許可がありません
find: ‘/etc/polkit-1/localauthority’: 許可がありません
/etc/brltty/Input/ba/all.txt
/etc/brltty/Input/bd/all.txt
/etc/brltty/Input/bl/18.txt
/etc/brltty/Input/bl/40_m20_m40.txt
/etc/brltty/Input/ec/all.txt
/etc/brltty/Input/ec/spanish.txt
/etc/brltty/Input/eu/all.txt
/etc/brltty/Input/lb/all.txt
/etc/brltty/Input/lt/all.txt
/etc/brltty/Input/mb/all.txt
/etc/brltty/Input/mn/all.txt
/etc/brltty/Input/tn/all.txt
/etc/brltty/Input/tt/all.txt
/etc/brltty/Input/vd/all.txt
/etc/brltty/Input/vr/all.txt
/etc/brltty/Input/vs/all.txt
/etc/brltty/Input/xw/all.txt
find: ‘/etc/audit’: 許可がありません
find: ‘/etc/libvirt’: 許可がありません
find: ‘/etc/firewalld’: 許可がありません
find: ‘/etc/sudoers.d’: 許可がありません
</pre>

<pre>
$ find /etc -name '*.txt' 2>/dev/null
/etc/pki/nssdb/pkcs11.txt
/etc/brltty/Input/ba/all.txt
/etc/brltty/Input/bd/all.txt
/etc/brltty/Input/bl/18.txt
/etc/brltty/Input/bl/40_m20_m40.txt
/etc/brltty/Input/ec/all.txt
/etc/brltty/Input/ec/spanish.txt
/etc/brltty/Input/eu/all.txt
/etc/brltty/Input/lb/all.txt
/etc/brltty/Input/lt/all.txt
/etc/brltty/Input/mb/all.txt
/etc/brltty/Input/mn/all.txt
/etc/brltty/Input/tn/all.txt
/etc/brltty/Input/tt/all.txt
/etc/brltty/Input/vd/all.txt
/etc/brltty/Input/vr/all.txt
/etc/brltty/Input/vs/all.txt
/etc/brltty/Input/xw/all.txt
</pre>
</div>
</details>
{{< /accordion >}}

### 6.5の検索結果をエラー出力も含めて、画面とfind_results.txtという名前のテキストファイルに出力してください。catコマンドでfind_results.txtを確認してみましょう。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ find /etc -name '*.txt' 2>&1 | tee find_results.txt
/etc/pki/nssdb/pkcs11.txt
find: ‘/etc/pki/rsyslog’: 許可がありません
find: ‘/etc/grub.d’: 許可がありません
find: ‘/etc/lvm/archive’: 許可がありません
find: ‘/etc/lvm/backup’: 許可がありません
find: ‘/etc/lvm/cache’: 許可がありません
find: ‘/etc/dhcp’: 許可がありません
find: ‘/etc/nftables’: 許可がありません
find: ‘/etc/cups/ssl’: 許可がありません
find: ‘/etc/sssd’: 許可がありません
find: ‘/etc/polkit-1/rules.d’: 許可がありません
find: ‘/etc/polkit-1/localauthority’: 許可がありません
/etc/brltty/Input/ba/all.txt
/etc/brltty/Input/bd/all.txt
/etc/brltty/Input/bl/18.txt
/etc/brltty/Input/bl/40_m20_m40.txt
/etc/brltty/Input/ec/all.txt
/etc/brltty/Input/ec/spanish.txt
/etc/brltty/Input/eu/all.txt
/etc/brltty/Input/lb/all.txt
/etc/brltty/Input/lt/all.txt
/etc/brltty/Input/mb/all.txt
/etc/brltty/Input/mn/all.txt
/etc/brltty/Input/tn/all.txt
/etc/brltty/Input/tt/all.txt
/etc/brltty/Input/vd/all.txt
/etc/brltty/Input/vr/all.txt
/etc/brltty/Input/vs/all.txt
/etc/brltty/Input/xw/all.txt
find: ‘/etc/audit’: 許可がありません
find: ‘/etc/libvirt’: 許可がありません
find: ‘/etc/firewalld’: 許可がありません
find: ‘/etc/sudoers.d’: 許可がありません
</pre>

<pre>
$ cat find_results.txt
/etc/pki/nssdb/pkcs11.txt
find: ‘/etc/pki/rsyslog’: 許可がありません
find: ‘/etc/grub.d’: 許可がありません
find: ‘/etc/lvm/archive’: 許可がありません
find: ‘/etc/lvm/backup’: 許可がありません
find: ‘/etc/lvm/cache’: 許可がありません
find: ‘/etc/dhcp’: 許可がありません
find: ‘/etc/nftables’: 許可がありません
find: ‘/etc/cups/ssl’: 許可がありません
find: ‘/etc/sssd’: 許可がありません
find: ‘/etc/polkit-1/rules.d’: 許可がありません
find: ‘/etc/polkit-1/localauthority’: 許可がありません
/etc/brltty/Input/ba/all.txt
/etc/brltty/Input/bd/all.txt
/etc/brltty/Input/bl/18.txt
/etc/brltty/Input/bl/40_m20_m40.txt
/etc/brltty/Input/ec/all.txt
/etc/brltty/Input/ec/spanish.txt
/etc/brltty/Input/eu/all.txt
/etc/brltty/Input/lb/all.txt
/etc/brltty/Input/lt/all.txt
/etc/brltty/Input/mb/all.txt
/etc/brltty/Input/mn/all.txt
/etc/brltty/Input/tn/all.txt
/etc/brltty/Input/tt/all.txt
/etc/brltty/Input/vd/all.txt
/etc/brltty/Input/vr/all.txt
/etc/brltty/Input/vs/all.txt
/etc/brltty/Input/xw/all.txt
find: ‘/etc/audit’: 許可がありません
find: ‘/etc/libvirt’: 許可がありません
find: ‘/etc/firewalld’: 許可がありません
find: ‘/etc/sudoers.d’: 許可がありません
</pre>
</div>
</details>
{{< /accordion >}}

***

## 2.主なフィルタコマンドの確認

### 1.カレントディレクトリをホームディレクトリに変更してください。

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

### 2.catコマンドとリダイレクト機能を使って、programming.txtというファイルをホームディレクトリに作成してください。

ファイルの内容は次の8行です。作成後、catコマンドで確認してください。

ruby
ruby
javascript
shellscript
shellscript
shellscript
python
go

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ cat > programming.txt
ruby //[enterキー]
ruby //[enterキー]
javascript //[enterキー]
shellscript //[enterキー]
shellscript //[enterキー]
shellscript //[enterキー]
python //[enterキー]
go //[enterキー]
//[Ctrl]+[D]終了
</pre>

<pre>
$ cat programming.txt
ruby
ruby
javascript
shellscript
shellscript
shellscript
python
go
</pre>
</div>
</details>
{{< /accordion >}}

### 3.programming.txtから重複行を排除し、昇順（アルファベット順）に並び替えて表示してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ uniq programming.txt | sort
go
javascript
python
ruby
shellscript
</pre>
</div>
</details>
{{< /accordion >}}

### 4.programming.txtから重複行を排除し、逆順（アルファベット順）に並び替えて、上位2行を表示してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ uniq programming.txt | sort -r | head -n 2
shellscript
ruby
</pre>
</div>
</details>
{{< /accordion >}}

### 5.programming.txtから重複行を排除し、逆順に並び替えて、画面表示と同時にファイルtee.txtに保存してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ uniq programming.txt | sort -r | tee tee.txt
shellscript
ruby
python
javascript
go
</pre>

<pre>
$ cat tee.txt
shellscript
ruby
python
javascript
go
</pre>
</div>
</details>
{{< /accordion >}}

