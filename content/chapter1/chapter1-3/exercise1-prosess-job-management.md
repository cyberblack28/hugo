---
title: "Exercise1 Prosess & Job Management"
date: 2017-10-17T15:26:15Z
draft: false
weight: 10
---

## 1.stressコマンドを用いたジョブの操作

stressコマンドを利用して、フォアグラウンドとバックグラウンドのジョブの切替を確認します。

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

2.stressのRPMパッケージをインストールします。

※ダウンロード:https://www.cyberblack.net/practice/linux/zip/stress-1.0.4-23.el8.x86_64.rpm

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
# wget https://www.cyberblack.net/practice/linux/zip/stress-1.0.4-23.el8.x86_64.rpm
--2020-02-02 20:23:05--  https://www.cyberblack.net/practice/linux/zip/stress-1.0.4-23.el8.x86_64.rpm
www.cyberblack.net (www.cyberblack.net) をDNSに問いあわせています... 185.199.108.153, 185.199.109.153, 185.199.110.153, ...
www.cyberblack.net (www.cyberblack.net)|185.199.108.153|:443 に接続して います... 接続しました。
HTTP による接続要求を送信しました、応答を待っています... 200 OK
長さ: 39652 (39K) [application/x-redhat-package-manager]
`stress-1.0.4-23.el8.x86_64.rpm' に保存中
  
stress-1.0.4-23.el8 100%[===================>]  38.72K  77.5KB/s 時間 0.5s
  
2020-02-02 20:23:06 (77.5 KB/s) - `stress-1.0.4-23.el8.x86_64.rpm' へ保存完了 [39652/39652]
# rpm -Uvh stress-1.0.4-23.el8.x86_64.rpm
警告: stress-1.0.4-23.el8.x86_64.rpm: ヘッダー V4 RSA/SHA256 Signature、鍵 ID e755cc63: NOKEY
Verifying...                          ##############################[100%]
準備しています...              ##############################[100%]
更新中 / インストール中...
   1:stress-1.0.4-23.el8              ##############################[100%]
# rpm -qa | grep stress
stress-1.0.4-23.el8.x86_64
</pre>
</div>
</details>
{{< /accordion >}}

3.4つのstressのプロセスを動かして、仮想マシンにで負荷をかけます。以下のstressコマンドを実行します。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
# stress --cpu 3
stress: info: [30808] dispatching hogs: 3 cpu, 0 io, 0 vm, 0 hdd
</pre>
</div>
</details>
{{< /accordion >}}

4.3.で実行したstressコマンドが、フォアグラウンドジョブとして実行されているため、端末ウインドウではほかのコマンドが入力できません。キー入力を行えるようにするため、バックグラウンドジョブに変更してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
# stress --cpu 3
stress: info: [30808] dispatching hogs: 3 cpu, 0 io, 0 vm, 0 hdd
<font color="Red">//[Ctrl]+[z]キーを入力</font>
^Z
[1]+  停止                  stress --cpu 3
</pre>

<pre>
# jobs
# bg %1
[1]+ stress --cpu 3 &
</pre>
</div>
</details>
{{< /accordion >}}

5.バックグラウンドジョブになっていること確認してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
# jobs
[1]+  実行中               stress --cpu 3 &
</pre>
</div>
</details>
{{< /accordion >}}

6.stressコマンドを終了させます。一度、フォアグラウンドジョブに戻した後、[Ctrl] + [c]で終了させて下さい。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
# fg %1
<font color="Red">//[Ctrl]+[c]を入力</font>
stress --cpu 3
^C
#
</pre>
</div>
</details>
{{< /accordion >}}

7.stressコマンドが終了したことを確認してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
# jobs <font color="Red">//何も表示されなければ正常に終了しています。</font>
</pre>
</div>
</details>
{{< /accordion >}}

***

## 2.ジョブとプロセスの確認

stressコマンドを使って、ジョブとプロセスの違い、psコマンドやkillコマンドについて確認します。

1.バックグラウンドジョブとして、「stress --cpu 3」コマンドを実行し、確認してください。

※プロンプトが戻らない場合は、[Enter]キー何度か押してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
# stress --cpu 3 &
[1] 31056
# stress: info: [31056] dispatching hogs: 3 cpu, 0 io, 0 vm, 0 hdd
<font color="Red">//[Enter]キーを押してプロンプトをfgにします。</font>
#
</pre>

<pre>
# jobs
[1]+  実行中               stress --cpu 3 &
</pre>
</div>
</details>
{{< /accordion >}}

2.stress --cpu 3は、ジョブとしては1つです。psコマンドで、プロセス単位でみたときのstress --cpu 3を確認します。

オプション無しで、psコマンドを実行し、stressのプロセス数を確認してみましょう。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
# ps
  PID TTY          TIME CMD
 2424 pts/0    00:00:00 su
 2430 pts/0    00:00:00 bash
31056 pts/0    00:00:00 stress
31057 pts/0    00:02:17 stress
31058 pts/0    00:02:17 stress
31059 pts/0    00:02:17 stress
31119 pts/0    00:00:00 ps

<font color="Red">//psコマンドを実行すると、右端にstressと表示されている行が4行表示されるはずです。これは、stressのプロセスとしては4つ動作していることを表しています。
「stress --cpu 3」は、stressのプロセスを3つ起動するコマンドですが、プロセスが1つ多くあります。内訳は、親プロセス1 + 子プロセス3になります。</font>
</pre>
</div>
</details>
{{< /accordion >}}

3.pstreeコマンドにpオプションを付けて、ツリー構造でstressプロセスの親子関係を確認してみましょう。「pstree -p | grep stress」

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
# pstree -p | grep stress
  |                                                                           `-stress(31395)-+-stress(31396)
  |                                                                                           |-stress(31397)
  |                                                                                           `-stress(31398)
</pre>
</div>
</details>
{{< /accordion >}}

4.killコマンドを使って、すべてのstressのプロセスを強制終了してください。

pstreeコマンドで確認した結果の内、31395が親プロセスそれ以外が子プロセス（31396,31397,31398）になります。まず、3個の子プロセスの内どれか1個を強制終了してください。

※プロセスIDは固定ではないので本内容とは異なる場合があります。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
# kill 31397
stress: FAIL: [31395] (415) <-- worker 31397 got signal 15
stress: WARN: [31395] (417) now reaping child worker processes
stress: FAIL: [31395] (451) failed run completed in 429s
<font color="Red">//[Enter]キーを入力</font>
[1]+  終了 1                stress --cpu 3

<font color="Red">//子プロセスを強制終了させることによる忠告が出て、親プロセスと他の子プロセスと共に終了となります。</font>
</pre>

<pre>
# ps
PID TTY          TIME CMD
2424 pts/0    00:00:00 su
2430 pts/0    00:00:00 bash
31459 pts/0    00:00:00 ps
</pre>
</div>
</details>
{{< /accordion >}}

5.もう一度、「stress --cpu 3 &」を実行、「pstree -p | grep stress」で親プロセスIDを確認して、今度は親プロセスから強制終了してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
# stress --cpu 3 &
[1] 31546
# stress: info: [31546] dispatching hogs: 3 cpu, 0 io, 0 vm, 0 hdd
<font color="Red">//[Enter]キーを入力</font>
</pre>

<pre>
# pstree -p | grep stress
|                                                                           `-stress(31546)-+-stress(31547)
|                                                                                           |-stress(31548)
|                                                                                           `-stress(31549)
# kill 31546
# ps
  PID TTY          TIME CMD
 2424 pts/0    00:00:00 su
 2430 pts/0    00:00:00 bash
31547 pts/0    00:01:17 stress
31548 pts/0    00:01:17 stress
31549 pts/0    00:01:17 stress
31579 pts/0    00:00:00 ps

<font color="Red">//親プロセスを強制終了すると、子プロセスも含めて強制終了されません。子プロセスは親プロセスがなくなると、子プロセス自体が単体のプロセスに変わります。以前はこういう仕組みがなく、子プロセスがゾンビプロセスとして残ってしまうことがありました。</font>
</pre>

<pre>
<font color="Red">//全プロセスを終了する場合は、各プロセスIDでkillコマンドを実行します。</font>
# kill 31547 31548 31549
# pstree -p | grep stress
# ps
PID TTY          TIME CMD
2424 pts/0    00:00:00 su
2430 pts/0    00:00:00 bash
31617 pts/0    00:00:00 ps
</pre>
</div>
</details>
{{< /accordion >}}

