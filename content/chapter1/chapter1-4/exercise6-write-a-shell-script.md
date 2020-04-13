---
title: "Exercise6 Write a Shell Script"
date: 2017-10-17T15:26:15Z
draft: false
weight: 10
---

## 1.シェル変数の演習

1.カレントディレクトリをホームディレクトリに変更してください。これまでの演習で使用したsample_web.logがあることを確認してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ cd
$ pwd
/home/student
$ ls
sample_web.log  ダウンロード  デスクトップ  ビデオ  画像
sample_web.zip  テンプレート  ドキュメント  音楽    公開
</pre>
</div>
</details>
{{< /accordion >}}

2.training06_1.shというファイル名でシェルスクリプトファイルを作成し、iPadまたはiPhoneを使ってアクセスしてきたユーザ数（iPadまたはiPhoneという文字列を含む行の行数）が次のメッセージとともに表示されるようにしてください。〇〇には件数が入ります。

{{< accordion >}}
<strong>＜表示結果＞</strong><br>
<strong>iPadからのアクセス数は○○件です。※スクリプトが正しければ、○○には592と表示</strong><br>
<strong>iPhoneからのアクセス数は○○件です。※スクリプトが正しければ、○○には647と表示</strong>
{{< /accordion >}}

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ vim training06_1.sh

----------------以下を右クリックコピーしてTeraTerm上でペースト----------------------
#!/bin/bash

iPad=$(grep iPad ~/sample_web.log | wc -l)
iPhone=$(grep iPhone ~/sample_web.log | wc -l)

echo iPadからのアクセス数は $iPad件です。
echo iPhoneからのアクセス数は $iPhone件です。
----------------[Esc + :wq]で保存終了---------------------------------------------
</pre>

<pre>
$ chmod +x training06_1.sh
$ bash training06_1.sh
iPadからのアクセス数は 592件です。
iPhoneからのアクセス数は 647件です。
</pre>
</div>
</details>
{{< /accordion >}}

***

## 2.位置パラメータの演習

1.カレントディレクトリをホームディレクトリに変更してください。これまでの演習で使用したsample_web.logがあることを確認してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ cd
$ pwd
/home/student
$ ls
sample_web.log  training06_1.sh  テンプレート  ドキュメント  音楽  公開
sample_web.zip  ダウンロード     デスクトップ  ビデオ        画像
</pre>
</div>
</details>
{{< /accordion >}}

2.training06_1.shをtraining06_2.shとしてコピーしてください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ cp -p training06_1.sh training06_2.sh
$ ls
sample_web.log  training06_1.sh  ダウンロード  デスクトップ  ビデオ  画像
sample_web.zip  training06_2.sh  テンプレート  ドキュメント  音楽    公開
</pre>
</div>
</details>
{{< /accordion >}}

3.training06_1.shの2箇所を位置パラメータ$1に変更して、「bash training06_2.sh ~/sample_web.log」を実行して、training06_1.shと同じ結果になることを確認してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ vim training06_2.sh

----------------以下を右クリックコピーしてTeraTerm上でペースト----------------------
#!/bin/bash
  
iPad=$(grep iPad $1 | wc -l)
iPhone=$(grep iPhone $1 | wc -l)
  
echo iPadからのアクセス数は $iPad件です。
echo iPhoneからのアクセス数は $iPhone件です。
----------------[Esc + :wq]で保存終了---------------------------------------------
</pre>

<pre>
$ bash training06_2.sh ~/sample_web.log
iPadからのアクセス数は 592件です。
iPhoneからのアクセス数は 647件です。
</pre>
</div>
</details>
{{< /accordion >}}

***

## 3.if文の演習

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

2.training06_3.shという名前のシェルスクリプトファイルを作成し、本日が2020年1月27日なら、2020-01-27.txtのように、年-月-日.txtのファイルを作成、すでに同じ名前のファイルが存在する場合はファイルは作成せずに、かわりに「ファイルは既に存在します。」というメッセージを表示させるスクリプトを作成してください。1回目はファイルの作成、2回目はメッセージ表示となるので、スクリプトを2回実行しましょう。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ vim training06_3.sh

----------------以下を右クリックコピーしてTeraTerm上でペースト----------------------
#!/bin/bash

today=$(date '+%Y-%m-%d')

if [ -e $today.txt ] ; then
  echo "ファイルは既に存在します。"
else
  touch ~/$today.txt
fi
----------------[Esc + :wq]で保存終了---------------------------------------------
</pre>

<pre>
$ chmod +x training06_3.sh
$ bash training06_3.sh
$ ls -l
合計 4724
-rw-rw-r--. 1 student student       0  1月 27 21:44 2020-01-27.txt
-rw-rw-r--. 1 student student 4398816  3月 17  2016 sample_web.log
-rw-rw-r--. 1 student student  425285  1月 27 02:05 sample_web.zip
-rw-rw-r--. 1 student student     212  1月 27 21:35 training06_1.sh
-rw-rw-r--. 1 student student     184  1月 27 21:35 training06_2.sh
-rwxrwxr-x. 1 student student     146  1月 27 21:44 training06_3.sh
drwxr-xr-x. 2 student student       6  1月 21 00:23 ダウンロード
drwxr-xr-x. 2 student student       6  1月 21 00:23 テンプレート
drwxr-xr-x. 2 student student       6  1月 21 00:23 デスクトップ
drwxr-xr-x. 2 student student       6  1月 21 00:23 ドキュメント
drwxr-xr-x. 2 student student       6  1月 21 00:23 ビデオ
drwxr-xr-x. 2 student student       6  1月 21 00:23 音楽
drwxr-xr-x. 2 student student       6  1月 21 00:23 画像
drwxr-xr-x. 2 student student       6  1月 21 00:23 公開
</pre>

<pre>
$ bash training06_3.sh
ファイルは既に存在します。
</pre>
</div>
</details>
{{< /accordion >}}

***

## 4.for文の演習

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

2.training06_4.shという名前のシェルスクリプトファイルを作成し、前回の日付ファイルの名前に-1から-5の連番を付与し、5個のファイルが作成されるスクリプトを作成しましょう。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ vim training06_4.sh

----------------以下を右クリックコピーしてTeraTerm上でペースト----------------------
#!/bin/bash

today=$(date '+%Y-%m-%d')

for i in $(seq 1 5)
  do
    touch $today-$i.txt
  done
----------------[Esc + :wq]で保存終了---------------------------------------------
</pre>

<pre>
$ chmod +x training06_4.sh
$ bash training06_4.sh
$ ls -l
合計 4728
-rw-rw-r--. 1 student student       0  1月 27 21:59 2020-01-27-1.txt
-rw-rw-r--. 1 student student       0  1月 27 21:59 2020-01-27-2.txt
-rw-rw-r--. 1 student student       0  1月 27 21:59 2020-01-27-3.txt
-rw-rw-r--. 1 student student       0  1月 27 21:59 2020-01-27-4.txt
-rw-rw-r--. 1 student student       0  1月 27 21:59 2020-01-27-5.txt
-rw-rw-r--. 1 student student       0  1月 27 21:44 2020-01-27.txt
-rw-rw-r--. 1 student student 4398816  3月 17  2016 sample_web.log
-rw-rw-r--. 1 student student  425285  1月 27 02:05 sample_web.zip
-rw-rw-r--. 1 student student     212  1月 27 21:35 training06_1.sh
-rw-rw-r--. 1 student student     184  1月 27 21:35 training06_2.sh
-rwxrwxr-x. 1 student student     146  1月 27 21:44 training06_3.sh
-rwxrwxr-x. 1 student student      96  1月 27 21:59 training06_4.sh
drwxr-xr-x. 2 student student       6  1月 21 00:23 ダウンロード
drwxr-xr-x. 2 student student       6  1月 21 00:23 テンプレート
drwxr-xr-x. 2 student student       6  1月 21 00:23 デスクトップ
drwxr-xr-x. 2 student student       6  1月 21 00:23 ドキュメント
drwxr-xr-x. 2 student student       6  1月 21 00:23 ビデオ
drwxr-xr-x. 2 student student       6  1月 21 00:23 音楽
drwxr-xr-x. 2 student student       6  1月 21 00:23 画像
drwxr-xr-x. 2 student student       6  1月 21 00:23 公開
</pre>
</div>
</details>
{{< /accordion >}}

***

## 5.while文の演習

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

2.training06_5.shという名前のシェルスクリプトファイルを作成し、file1.txt、file2.txt・・・file10.txtのように、fileの後ろに1から10の連番を付けて10個のファイルが作成できるスクリプトを作成及び実行してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ vim training06_5.sh

----------------以下を右クリックコピーしてTeraTerm上でペースト----------------------
#!/bin/bash

i=1

while [ $i -le 10 ]
  do
    touch file$i.txt
    i=$((i+1))
  done
----------------[Esc + :wq]で保存終了---------------------------------------------
</pre>

<pre>
$ chmod +x training06_5.sh
$ bash training06_5.sh
$ ls -l
合計 4732
-rw-rw-r--. 1 student student       0  1月 27 21:59 2020-01-27-1.txt
-rw-rw-r--. 1 student student       0  1月 27 21:59 2020-01-27-2.txt
-rw-rw-r--. 1 student student       0  1月 27 21:59 2020-01-27-3.txt
-rw-rw-r--. 1 student student       0  1月 27 21:59 2020-01-27-4.txt
-rw-rw-r--. 1 student student       0  1月 27 21:59 2020-01-27-5.txt
-rw-rw-r--. 1 student student       0  1月 27 21:44 2020-01-27.txt
-rw-rw-r--. 1 student student       0  1月 27 22:07 file1.txt
-rw-rw-r--. 1 student student       0  1月 27 22:07 file10.txt
-rw-rw-r--. 1 student student       0  1月 27 22:07 file2.txt
-rw-rw-r--. 1 student student       0  1月 27 22:07 file3.txt
-rw-rw-r--. 1 student student       0  1月 27 22:07 file4.txt
-rw-rw-r--. 1 student student       0  1月 27 22:07 file5.txt
-rw-rw-r--. 1 student student       0  1月 27 22:07 file6.txt
-rw-rw-r--. 1 student student       0  1月 27 22:07 file7.txt
-rw-rw-r--. 1 student student       0  1月 27 22:07 file8.txt
-rw-rw-r--. 1 student student       0  1月 27 22:07 file9.txt
-rw-rw-r--. 1 student student 4398816  3月 17  2016 sample_web.log
-rw-rw-r--. 1 student student  425285  1月 27 02:05 sample_web.zip
-rw-rw-r--. 1 student student     212  1月 27 21:35 training06_1.sh
-rw-rw-r--. 1 student student     184  1月 27 21:35 training06_2.sh
-rwxrwxr-x. 1 student student     146  1月 27 21:44 training06_3.sh
-rwxrwxr-x. 1 student student      96  1月 27 21:59 training06_4.sh
-rwxrwxr-x. 1 student student      86  1月 27 22:06 training06_5.sh
drwxr-xr-x. 2 student student       6  1月 21 00:23 ダウンロード
drwxr-xr-x. 2 student student       6  1月 21 00:23 テンプレート
drwxr-xr-x. 2 student student       6  1月 21 00:23 デスクトップ
drwxr-xr-x. 2 student student       6  1月 21 00:23 ドキュメント
drwxr-xr-x. 2 student student       6  1月 21 00:23 ビデオ
drwxr-xr-x. 2 student student       6  1月 21 00:23 音楽
drwxr-xr-x. 2 student student       6  1月 21 00:23 画像
drwxr-xr-x. 2 student student       6  1月 21 00:23 公開
</pre>
</div>
</details>
{{< /accordion >}}

***

## 6.while文の演習

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

2.training06_6.shという名前のシェルスクリプトファイルを作成し、位置パラメータを利用して、引数が01の場合はGoogle、02の場合はMicrosoft、03の場合はAmazon、それ以外はNo matchと表示されるスクリプトをcase文を用いて作成してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ vim training06_6.sh

----------------以下を右クリックコピーしてTeraTerm上でペースト----------------------
#!/bin/bash

case $1 in
  01)
    echo "Google";;
  02)
    echo "Microsoft";;
  03)
    echo "Amazon";;
  *)
    echo "No match";;
esac
----------------[Esc + :wq]で保存終了---------------------------------------------
</pre>

<pre>
$ chmod +x training06_6.sh
$ bash training06_6.sh 01
Google
$ bash training06_6.sh 02
Microsoft
$ bash training06_6.sh 03
Amazon
$ bash training06_6.sh 04
No match
</pre>
</div>
</details>
{{< /accordion >}}

***

## 7.シェル関数の演習

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

2.training06_7.shという名前のシェルスクリプトファイルを作成し、todayというシェル関数を作成して、日付とカレンダーが表示されるスクリプトを作成してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ vim training06_7.sh

----------------以下を右クリックコピーしてTeraTerm上でペースト----------------------
#!/bin/bash

function today(){
  date
  cal
}
  
today
----------------[Esc + :wq]で保存終了---------------------------------------------
</pre>

<pre>
$ chmod +x training06_7.sh
$ bash training06_7.sh
2020年  1月 27日 月曜日 22:22:28 EST
      1月 2020
日 月 火 水 木 金 土
          1  2  3  4
 5  6  7  8  9 10 11
12 13 14 15 16 17 18
19 20 21 22 23 24 25
26 27 28 29 30 31
</pre>
</div>
</details>
{{< /accordion >}}

***

## 8.シェルスクリプトでfizzbuzz（応用演習）

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

2.100までを基準に、3で割り切れる場合はfizzと表示、5で割り切れる場合はbuzzと表示、両方割り切れる場合はfizzbuzzと表示されるシェルスクリプトファイルを作成してください。ファイル名はfizzbuzz.shとします。for文とif文を利用してみましょう。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ vim fizzbuzz.sh

----------------以下を右クリックコピーしてTeraTerm上でペースト----------------------
#!/bin/bash
  
for ((i=1;i<=100; i++))
do
  if (($i % 15 == 0)); then
    echo fizzbuzz
  elif (($i % 3 == 0)); then
    echo fizz
  elif (($i % 5 == 0)); then
    echo buzz
  else
    echo $i
  fi
done
----------------[Esc + :wq]で保存終了---------------------------------------------
</pre>

<pre>
$ chmod +x fizzbuzz.sh
$ bash fizzbuzz.sh
1
2
fizz
4
buzz
fizz
7
8
fizz
buzz
11
fizz
13
14
fizzbuzz
16
17
fizz
19
buzz
fizz
22
23
fizz
buzz
26
fizz
28
29
fizzbuzz
31
32
fizz
34
buzz
fizz
37
38
fizz
buzz
41
fizz
43
44
fizzbuzz
46
47
fizz
49
buzz
fizz
52
53
fizz
buzz
56
fizz
58
59
fizzbuzz
61
62
fizz
64
buzz
fizz
67
68
fizz
buzz
71
fizz
73
74
fizzbuzz
76
77
fizz
79
buzz
fizz
82
83
fizz
buzz
86
fizz
88
89
fizzbuzz
91
92
fizz
94
buzz
fizz
97
98
fizz
buzz
</pre>
</div>
</details>
{{< /accordion >}}