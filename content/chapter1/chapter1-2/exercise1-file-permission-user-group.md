---
title: "Exercise1 File,Permission,User,Group"
date: 2017-10-17T15:26:15Z
draft: false
weight: 10
---

## 1.suコマンドとパーミッションの変更

1.studentとしてログインしている状態で、端末を開きます。idコマンドを実行し、現在のユーザを確認してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ id
uid=1000(student) gid=1000(student) groups=1000(student),10(wheel) context=unconfined_u:unconfined_r:unconfined_t:s0-s0:c0.c1023
</pre>
</div>
</details>
{{< /accordion >}}

2.suコマンドを使って、rootユーザに切り替えてください。

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

3.idコマンドを実行し、現在のユーザを確認してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
# id
uid=0(root) gid=0(root) groups=0(root) context=unconfined_u:unconfined_r:unconfined_t:s0-s0:c0.c1023
</pre>
</div>
</details>
{{< /accordion >}}

4.rootユーザのまま、カレントディレクトリを/usr/tmp/に変更します。

以降の操作は、指示が無い限りはrootユーザで行ってください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
# cd /usr/tmp
</pre>
</div>
</details>
{{< /accordion >}}

5.touchコマンドで、test1.txtおよびtest2.txtという空のファイルを、カレントディレクトリに作成してください。その後、lsコマンドでtest1.txtとtest2.txtのパーミッションを確認してください。

rootにはrw（読み取りと書き込み）、その他のユーザにはr（読み取りのみ）が割り当てられています。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
# touch test{1..2}.txt
# ls -l test*
-rw-r--r--. 1 root root 0  1月 30 03:41 test1.txt
-rw-r--r--. 1 root root 0  1月 30 03:41 test2.txt
</pre>
</div>
</details>
{{< /accordion >}}

6.現在の端末ウインドウはそのまま閉じずに、新たにもう一つ端末ウインドウを開いてください。

新たに開いた端末ウインドウは、studentのまま（rootには切り替えない）にします。

新しく開いたsutdentの端末で、/usr/tmp/test1.txtをvimコマンドで開いてみましょう。

すると、上書き保存ができない状態で、ファイルが開きます。文字を入力して保存できないことを確認してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ vim /usr/tmp/test1.txt

----------------［i］か［a］で入力モードに切り替えます。何か文字を入力して、[Esc]キー[:wq]----------------------
testtest
----------------[Esc + :wq]で保存終了すると、以下のエラーが出ます。-------------------------------------------
E45: 'readonly' オプションが設定されています (! を追加で上書き)
続けるにはENTERを押すかコマンドを入力してください
----------------ENTERを押して、[:q!]で保存せずにvimを終了しましょう。-----------------------------------------
</pre>
</div>
</details>
{{< /accordion >}}

7.test1.txtとtest2.txtのパーミッションを、以下の要件に従い変更します。※開いたrootの端末ウインドウで実行してください。

a. test1.txtおよびtest2.txtに、studentが文字を追加し、上書き保存できるようにしてください

b. オーナー（所有者）であるroot関連のパーミッションは変更しないでください

c. test1.txtのパーミッションはシンボルモードで変更してください

d. test2.txtのパーミッションは数値モードで変更してください

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
# chmod o+w test1.txt
# chmod 646 test2.txt
# ls -l test*
-rw-r--rw-. 1 root root 0  1月 30 03:41 test1.txt
-rw-r--rw-. 1 root root 0  1月 30 03:41 test2.txt
</pre>
</div>
</details>
{{< /accordion >}}

8.新たに開いたstudentの端末ウインドウで、/usr/tmp/test1.txtをテキストエディタで開きます。

今度は、ファイルを上書き保存できるはずです。適当な文字を入力後、上書き保存動作を行い、確認してください。同様に、test2.txtも確認してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ vim /usr/tmp/test1.txt

----------------［i］か［a］で入力モードに切り替えます。何か文字を入力して、[Esc]キー[:wq]---------
testtest
----------------[Esc + :wq]で保存終了します。--------------------------------------------------

$ cat /usr/tmp/test1.txt
testtest
</pre>

<pre>
$ vim /usr/tmp/test2.txt

----------------［i］か［a］で入力モードに切り替えます。何か文字を入力して、[Esc]キー[:wq]---------
test2test2
----------------[Esc + :wq]で保存終了します。--------------------------------------------------
  
$ cat /usr/tmp/test2.txt
test2test2
</pre>
</div>
</details>
{{< /accordion >}}

***

## 2.ユーザの作成とUID、所属グループの確認

1.rootユーザの状態で、次の作業を行ってください。

a. student02というユーザを作成してください。

b. student02にpasswordというパスワードを設定てください。

c. idコマンドを使ってstudent02が存在していることを確認してください。

d. 上記の管理作業が完了したら、rootからstudnetに戻してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
//a.student02というユーザを作成してください。
# useradd student02
</pre>

<pre>
//b.student02にpasswordというパスワードを設定てください。
# passwd student02
ユーザー student02 のパスワードを変更。
新しいパスワード:tokyoec2020
新しいパスワードを再入力してください:tokyoec2020
passwd: すべての認証トークンが正しく更新できました。
</pre>

<pre>
//c.idコマンドを使ってstudent02が存在していることを確認してください。
# id student02
uid=1001(student02) gid=1001(student02) groups=1001(student02)
</pre>

<pre>
//d.上記の管理作業が完了したら、rootからstudnetに戻してください。
# exit
ログアウト
$
</pre>
</div>
</details>
{{< /accordion >}}

2.端末上でsuコマンドを使ってstudent02に切り替えてください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ su student02
パスワード:tokyoec2020
$
</pre>
</div>
</details>
{{< /accordion >}}

3.student02として任意のパスワードに変更してください。

※一般ユーザは、rootとは異なり、自分のパスワードしか変更できません。パスワードの変更時には、現在使用中のパスワードの入力が必要です。新しいパスワードは、セキュリティレベルの低いパスワードは受け付けてもらえません。なお、パスワードの変更を中断する場合は、［Ctrl］+［C］キーを押します。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ passwd
ユーザー student02 のパスワードを変更。
Current password:tokyoec2020
新しいパスワード:gakusei@@@
新しいパスワードを再入力してください:
passwd: すべての認証トークンが正しく更新できました。
</pre>
</div>
</details>
{{< /accordion >}}

4.student02としての作業が完了したため、studentに戻ります。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ exit
$
</pre>
</div>
</details>
{{< /accordion >}}

***

## 3.グループ作成とsudoコマンド

user01、user02をメンバーとするグループgrp01を新規に作成し、このグループのメンバーであればsudoコマンドを使って、管理が行えるようにします。

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

2.user01、user02を作成してください。パスワード「gakusei@@@」としてください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
# useradd user01
# useradd user02
</pre>

<pre>
# passwd user01
ユーザー user01 のパスワードを変更。
新しいパスワード:gakusei@@@
新しいパスワードを再入力してください:gakusei@@@
passwd: すべての認証トークンが正しく更新できました。
# passwd user02
ユーザー user02 のパスワードを変更。
新しいパスワード:gakusei@@@
新しいパスワードを再入力してください:gakusei@@@
passwd: すべての認証トークンが正しく更新できました。
</pre>
</div>
</details>
{{< /accordion >}}

3.idコマンドでuser01とuser02ができていることを確認します。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
# id user01
uid=1002(user01) gid=1002(user01) groups=1002(user01)
# id user02
uid=1003(user02) gid=1003(user02) groups=1003(user02)
</pre>
</div>
</details>
{{< /accordion >}}

4.grp01グループを作成してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
# groupadd grp01
# getent group | grep grp01
grp01:x:1004:
</pre>
</div>
</details>
{{< /accordion >}}

5.user01とuser02をgrp01グループに所属させてください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
# gpasswd -M user01,user02 grp01
# getent group | grep grp01
grp01:x:1004:
# id user01
uid=1002(user01) gid=1002(user01) groups=1002(user01),1004(grp01)
# id user02
uid=1003(user02) gid=1003(user02) groups=1003(user02),1004(grp01)
</pre>
</div>
</details>
{{< /accordion >}}

6.visudoコマンドを使用して、最終行に「%grp01 ALL=(ALL) ALL」と入力します。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
# visudo

----------------[shift]+[g]キーで最終行まで移動、［i］か［a］で入力モードに切り替えます。何か文字を入力して、[Esc]キー[:wq]---------
・
・
・
・
・
%grp01 ALL=(ALL) ALL
----------------[Esc + :wq]で保存終了します。---------------------------------------------------------------------------------
</pre>
</div>
</details>
{{< /accordion >}}

7.root,studentからログアウトしてください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
# exit
ログアウト
$ exit
</pre>
</div>
</details>
{{< /accordion >}}

8.TeraTermを起動して、user01でログインしてください。※パスワードは「gakusei@@@」です。

9.「sudo useradd user03」を実行してください。

※パスワードの入力を求められるので、user01のパスワード「gakusei@@@」を入力してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
# sudo useradd user03

あなたはシステム管理者から通常の講習を受けたはずです。
これは通常、以下の3点に要約されます:
  
    #1) 他人のプライバシーを尊重すること。
    #2) タイプする前に考えること。
    #3) 大いなる力には大いなる責任が伴うこと。
  
[sudo] user01 のパスワード:gakusei@@@
</pre>
</div>
</details>
{{< /accordion >}}

10.同じやり方でuser03にパスワードを設定してみましょう。パスワードは「gakusei@@@」とします。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
# sudo passwd user03
ユーザー user03 のパスワードを変更。
新しいパスワード:gakusei@@@
新しいパスワードを再入力してください:gakusei@@@
passwd: すべての認証トークンが正しく更新できました。
</pre>
</div>
</details>
{{< /accordion >}}

11.idコマンドでuser03を確認してください。

※user03の情報が表示されれば、useraddコマンドがsudoで実行できたと見なします。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
# id user03
uid=1004(user03) gid=1005(user03) groups=1005(user03)
</pre>
</div>
</details>
{{< /accordion >}}

12.user01からログアウトしてください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ exit
ログアウト
</pre>
</div>
</details>
{{< /accordion >}}

13.TeraTermを起動して、user03でログインしてください。※パスワードは「gakusei@@@」です。

14.「sudo useradd user04」を実行してください。

※パスワードの入力を求められるので、user03のパスワード「gakusei@@@」を入力してください。
「user03は、sudoersファイル内にありません。この事象は記録・報告されます。」というメッセージが表示されます。
user03にはsudoコマンドでuseraddコマンドを実行できないことを確認しましょう。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ sudo useradd user04

あなたはシステム管理者から通常の講習を受けたはずです。
これは通常、以下の3点に要約されます:
  
    #1) 他人のプライバシーを尊重すること。
    #2) タイプする前に考えること。
    #3) 大いなる力には大いなる責任が伴うこと。
  
[sudo] user03 のパスワード:gakusei@@@
user03 は sudoers ファイル内にありません。この事象は記録・報告されます。
</pre>
</div>
</details>
{{< /accordion >}}