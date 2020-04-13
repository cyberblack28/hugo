---
title: "Exercise5 Creation and automatic execution of Shell Script"
date: 2017-10-17T15:26:15Z
draft: false
weight: 10
---

## 1.シェルスクリプトの作成と自動実行

1.カレントディレクトリをホームディレクトリに変更してください。

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

2.ホームディレクトリにscript_dirというディレクトリを作成し、test.txtというファイル名で空のファイルを作成してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ mkdir script_dir
$ cd script_dir
$ touch test.txt
$ ls -l
合計 0
-rw-rw-r--. 1 student student 0  1月 27 23:08 test.txt
</pre>
</div>
</details>
{{< /accordion >}}

3.script_dir内に以下の内容でshellscript.shというスクリプトファイルを作成してください。

実行できるようにshellscript.shに実行権限を付与してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ vim shellscript.sh

----------------以下を右クリックコピーしてTeraTerm上でペースト----------------------
#!/bin/bash

touch ~/script_dir/test.txt
----------------[Esc + :wq]で保存終了---------------------------------------------
</pre>

<pre>
$ chmod +x shellscript.sh
$ ls -l
合計 4
-rwxrwxr-x. 1 student student 41  1月 27 23:14 shellscript.sh
-rw-rw-r--. 1 student student  0  1月 27 23:08 test.txt
</pre>
</div>
</details>
{{< /accordion >}}

4.lsコマンドでtest.txtの作成時間を確認し、現在のLinux時刻よりも過去1分以上過去であることを確認してください。

確認後、shellscript.shを実行してください。

実行後、再度lsコマンドでtest.txtの時刻が、スクリプトを実行した時間になっていることを確認してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ ls -l
合計 4
-rwxrwxr-x. 1 student student 41  1月 27 23:14 shellscript.sh
-rw-rw-r--. 1 student student  0  1月 27 23:08 test.txt
</pre>

<pre>
$ ./shellscript.sh
$ ls -l
-rwxrwxr-x. 1 student student 41  1月 27 23:14 shellscript.sh
-rw-rw-r--. 1 student student  0  1月 27 23:22 test.txt
</pre>
</div>
</details>
{{< /accordion >}}

5.次に、crondを利用して、1分おきに自動実行されるように構成してください。

「systemctl status crond」を実行してActive:active(running)と表示されていることを確認します。

crontabコマンドで、cronの設定ファイルを編集して、1分おきに自動実行される設定をしてください。

設定後2分程待ちましょう。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ systemctl status crond
● crond.service - Command Scheduler
   Loaded: loaded (/usr/lib/systemd/system/crond.service; enabled; vendor preset: enabled)
   Active: active (running) since Mon 2020-01-27 20:28:06 EST; 2h 57min ago
 Main PID: 1109 (crond)
    Tasks: 1 (limit: 23983)
   Memory: 2.1M
   CGroup: /system.slice/crond.service
           mq1109 /usr/sbin/crond -n

 1月 27 21:50:01 localhost.localdomain anacron[2717]: Job `cron.daily' started
 1月 27 21:50:01 localhost.localdomain run-parts[3212]: (/etc/cron.daily) finished logrotate
 1月 27 21:50:01 localhost.localdomain anacron[2717]: Job `cron.daily' terminated
 1月 27 22:01:01 localhost.localdomain CROND[3316]: (root) CMD (run-parts /etc/cron.hourly)
 1月 27 22:10:01 localhost.localdomain anacron[2717]: Job `cron.weekly' started
 1月 27 22:10:01 localhost.localdomain anacron[2717]: Job `cron.weekly' terminated
 1月 27 22:30:01 localhost.localdomain anacron[2717]: Job `cron.monthly' started
 1月 27 22:30:01 localhost.localdomain anacron[2717]: Job `cron.monthly' terminated
 1月 27 22:30:01 localhost.localdomain anacron[2717]: Normal exit (3 jobs run)
 1月 27 23:01:54 localhost.localdomain CROND[3797]: (root) CMD (run-parts /etc/cron.hourly)
</pre>

<pre>
$ crontab -e

----------------以下を右クリックコピーしてTeraTerm上でペースト----------------------
*/1 * * * * ~/script_dir/shellscript.sh
----------------[Esc + :wq]で保存終了---------------------------------------------
</pre>
</div>
</details>
{{< /accordion >}}

6.自動実行が正しく行われているかは、lsコマンドでtest.txtのタイムスタンプの確認とrootユーザに変更して、「/var/log/cron」ファイルをcatコマンドでパイプを利用して、末尾10行を表示して確認してみましょう。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ ls -l
合計 4
-rwxrwxr-x. 1 student student 41  1月 27 23:14 shellscript.sh
-rw-rw-r--. 1 student student  0  1月 27 23:31 test.txt
</pre>

<pre>
$ su -
パスワード:tokyoec
</pre>

<pre>
# cat /var/log/cron | tail -n 10
an 27 22:30:01 localhost anacron[2717]: Normal exit (3 jobs run)
Jan 27 23:01:54 localhost CROND[3797]: (root) CMD (run-parts /etc/cron.hourly)
Jan 27 23:01:54 localhost run-parts[3797]: (/etc/cron.hourly) starting 0anacron
Jan 27 23:01:54 localhost run-parts[3797]: (/etc/cron.hourly) finished 0anacron
Jan 27 23:26:58 localhost crontab[4051]: (student) BEGIN EDIT (student)
Jan 27 23:29:39 localhost crontab[4051]: (student) REPLACE (student)
Jan 27 23:29:39 localhost crontab[4051]: (student) END EDIT (student)
Jan 27 23:30:01 localhost CROND[4082]: (student) CMD (~/script_dir/shellscript.sh)
Jan 27 23:31:01 localhost CROND[4104]: (student) CMD (~/script_dir/shellscript.sh)
Jan 27 23:32:01 localhost CROND[4128]: (student) CMD (~/script_dir/shellscript.sh)
# exit
ログアウト
$
</pre>
</div>
</details>
{{< /accordion >}}

7.確認完了後、crontabで設定を削除しておきましょう。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ crontab -e

----------------以下の設定を削除---------------------------------------------------
*/1 * * * * ~/script_dir/shellscript.sh　← ddで削除してください
----------------[Esc + :wq]で保存終了---------------------------------------------
</pre>
</div>
</details>
{{< /accordion >}}