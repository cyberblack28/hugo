---
title: "Exercise2 About Bash"
date: 2017-10-17T15:26:15Z
draft: false
weight: 10
---

## 1.環境変数とシェル変数

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

2.「training/linux」構成でディレクトリを作成してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ mkdir -p training/linux
$ ls training/
linux
</pre>
</div>
</details>
{{< /accordion >}}

3.環境変数trainを作成します。trainの値には、/home/student/training/linuxディレクトリを絶対指定で指定してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ train='/home/student/training/linux/'
$ export train='/home/student/training/linux/'
</pre>
</div>
</details>
{{< /accordion >}}

4.現在のユーザが、各種コマンドで環境変数$trainをディレクトリ名のかわりに指定すると、常に/home/student/training/linuxが指定されたものと同じ動作をします。

たとえば、カレントディレクトリに関係なく、touch $train/sample.txtで、sample.txtという空のファイルが/home/studnet/training/linuxに作成されます。
ls $trainで、/home/student/training/linuxのファイルが表示されます。
実際にこれらのコマンドを実行し、確認してみましょう。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ cd /
$ touch $train/sample.txt
$ ls $train
sample.txt
</pre>
</div>
</details>
{{< /accordion >}}

上記のように、シェル変数や環境変数に、ディレクトリを登録しておくと、長いディレクトリパスを指定しなくても、シェル変数や環境変数を指定すれば、簡単に目的のディレクトリを利用できます。
また、コンピュータによって、ディレクトリパスが異なる場合でも、ディレクトリパスを直接指定せずに、シェル変数や環境変数を指定するようにプログラムやシェルスクリプトを記述することで、汎用性を高めることができます。

5.usetコマンドで環境変数$trainを削除します。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ unset train
</pre>
</div>
</details>
{{< /accordion >}}

6.ホームディレクトリに移動し、applicationという名前のディレクトリを作成してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ cd
$ pwd
/home/student
$ mkdir application
application     sample_web.zip  ダウンロード  デスクトップ  ビデオ  画像
sample_web.log  training        テンプレート  ドキュメント  音楽    公開
</pre>
</div>
</details>
{{< /accordion >}}

7.シェル変数PATHに、applicationディレクトリを追加してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ PATH=$PATH:/home/student/application
</pre>
</div>
</details>
{{< /accordion >}}

8.echoコマンドでPATHにapplicationが追加されていることを確認してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ echo $PATH
/home/student/.local/bin:/home/student/bin:/usr/local/bin:/usr/bin:/usr/local/sbin:/usr/sbin:/home/student/application
</pre>
</div>
</details>
{{< /accordion >}}

9.環境変数trainや、シェル変数PATHとして指定したapplicationの設定は、端末を閉じると消えます。

別の端末を開いても、その端末には設定が引き継がれません。

永続化するためには、.bashrcに追加する必要があります。

実際に.bashrcに設定してみましょう。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ vim ~/.bashrc

----------------[Shift]+[g]で最終行にカーソルを移動して追記------------------------
# .bashrc

# Source global definitions
if [ -f /etc/bashrc ]; then
        . /etc/bashrc
fi

# User specific environment
PATH="$HOME/.local/bin:$HOME/bin:$PATH"
export PATH

# Uncomment the following line if you don't like systemctl's auto-paging feature:
# export SYSTEMD_PAGER=

# User specific aliases and functions
PATH=$PATH:~/application
----------------[Esc + :wq]で保存終了---------------------------------------------
</pre>
</div>
</details>
{{< /accordion >}}

端末を新規に開いて、変数trainやPATHが利用できるようになったことを確認します。単純にprintenvコマンドで確認してみましょう。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ printenv PATH
/home/student/.local/bin:/home/student/bin:/usr/local/bin:/usr/bin:/usr/local/sbin:/usr/sbin:/home/student/application
</pre>
</div>
</details>
{{< /accordion >}}

***

## 2.エイリアスの登録

1.登録済みのエイリアスを一覧表示してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ alias
/home/student/.local/bin:/home/student/bin:/usr/local/bin:/usr/bin:/usr/local/sbin:/usr/sbin:/home/student/application
[student@localhost ~]$ alias
alias egrep='egrep --color=auto'
alias fgrep='fgrep --color=auto'
alias grep='grep --color=auto'
alias l.='ls -d .* --color=auto'
alias ll='ls -l --color=auto'
alias ls='ls --color=auto'
alias vi='vim'
alias which='(alias; declare -f) | /usr/bin/which --tty-only --read-alias --read-functions --show-tilde --show-dot'
alias xzegrep='xzegrep --color=auto'
alias xzfgrep='xzfgrep --color=auto'
alias xzgrep='xzgrep --color=auto'
alias zegrep='zegrep --color=auto'
alias zfgrep='zfgrep --color=auto'
alias zgrep='zgrep --color=auto'
</pre>
</div>
</details>
{{< /accordion >}}

2.1.を確認すると、いままで私たちが実行していたlsコマンドは、ls --color=autoのエイリアスであることが分かります。エイリアスではない本来のlsコマンドを、現在のエイリアスを削除、変更せずに実行してください。カレントディレクトリをホームディレクトリに変更して実行してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ cd
$ pwd
/home/student
$ ls
//TeraTerm上では色がつきます。
application     sample_web.zip  ダウンロード  デスクトップ  ビデオ  画像
sample_web.log  training        テンプレート  ドキュメント  音楽    公開
</pre>

<pre>
$ /bin/ls
//TeraTerm上では色がつきません。
application     sample_web.zip  ダウンロード  デスクトップ  ビデオ  画像
sample_web.log  training        テンプレート  ドキュメント  音楽    公開
</pre>

<pre>
$ command ls
//TeraTerm上では色がつきません。
application     sample_web.zip  ダウンロード  デスクトップ  ビデオ  画像
sample_web.log  training        テンプレート  ドキュメント  音楽    公開
</pre>

<pre>
$ \ls
//TeraTerm上では色がつきません。
application     sample_web.zip  ダウンロード  デスクトップ  ビデオ  画像
sample_web.log  training        テンプレート  ドキュメント  音楽    公開
</pre>
</div>
</details>
{{< /accordion >}}

3.カレントディレクトリをホームディレクトリに変更して、touchコマンドでalias_testというファイルを作成してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ cd
$ pwd
/home/student
$ touch alias_test
$ ls
alias_test      sample_web.zip  テンプレート  ビデオ  公開
application     training        デスクトップ  音楽
sample_web.log  ダウンロード    ドキュメント  画像
</pre>
</div>
</details>
{{< /accordion >}}

4.rmコマンドでalias_testを削除して、何もメッセージが表示されずに削除できることを確認してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ rm alias_test
</pre>
</div>
</details>
{{< /accordion >}}

5.もう一度、alias_testファイルを作成し、rmに-iオプションを付けてalias_testファイルを削除してください。-iは、誤削除を防ぐため確認メッセージに対して y とタイプしないと削除できないようにするオプションです。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ touch alias_test
$ rm -i alias_test
//yと入力
rm: 通常の空ファイル 'alias_test' を削除しますか?
</pre>
</div>
</details>
{{< /accordion >}}

6.rm -iをエイリアス rmとして登録してください。登録後、実際に登録できていることを確認します。alias_testファイルを作成して、rmコマンドでiオプション無しで実行してもメッセージが表示されることを確認してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ alias rm='rm -i'
$ alias
alias egrep='egrep --color=auto'
alias fgrep='fgrep --color=auto'
alias grep='grep --color=auto'
alias l.='ls -d .* --color=auto'
alias ll='ls -l --color=auto'
alias ls='ls --color=auto'
alias rm='rm -i'
alias vi='vim'
alias which='(alias; declare -f) | /usr/bin/which --tty-only --read-alias --read-functions --show-tilde --show-dot'
alias xzegrep='xzegrep --color=auto'
alias xzfgrep='xzfgrep --color=auto'
alias xzgrep='xzgrep --color=auto'
alias zegrep='zegrep --color=auto'
alias zfgrep='zfgrep --color=auto'
alias zgrep='zgrep --color=auto'
$ touch alias_test
$ rm alias_test
//yと入力
rm: 通常の空ファイル 'alias_test' を削除しますか?
</pre>
</div>
</details>
{{< /accordion >}}

7.エイリアスを削除する場合は「unalias エイリアス名」となります。「unalias rm」で元に戻してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ unalias rm
$ alias
alias egrep='egrep --color=auto'
alias fgrep='fgrep --color=auto'
alias grep='grep --color=auto'
alias l.='ls -d .* --color=auto'
alias ll='ls -l --color=auto'
alias ls='ls --color=auto'
alias vi='vim'
alias which='(alias; declare -f) | /usr/bin/which --tty-only --read-alias --read-functions --show-tilde --show-dot'
alias xzegrep='xzegrep --color=auto'
alias xzfgrep='xzfgrep --color=auto'
alias xzgrep='xzgrep --color=auto'
alias zegrep='zegrep --color=auto'
alias zfgrep='zfgrep --color=auto'
alias zgrep='zgrep --color=auto'
$ touch alias_test
$ rm alias_test
</pre>
</div>
</details>
{{< /accordion >}}