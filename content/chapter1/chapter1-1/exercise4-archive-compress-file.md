---
title: "Exercise4 Archive & Compress file"
date: 2017-10-17T15:26:15Z
draft: false
weight: 10
---

## 1.tarコマンド演習

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

2.「tar_training」ディレクトリを作成してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ mkdir tar_training
$ ls
tar_training  テンプレート  ドキュメント  音楽  公開
ダウンロード  デスクトップ  ビデオ        画像
</pre>
</div>
</details>
{{< /accordion >}}

3.touchコマンドを利用して「tar_training」ディレクトリの中にfile01.txt,file02.txt,file03.txt,file04.txt,file05.txt」ファイルを作成します。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ touch tar_training/{file01.txt,file02.txt,file03.txt,file04.txt,file05.txt}
$ ls tar_training
file01.txt  file02.txt  file03.txt  file04.txt  file05.txt
</pre>

<pre>
$ touch tar_training/file01.txt tar_training/file02.txt tar_training/file03.txt tar_training/file04.txt tar_training/file05.txt
$ ls tar_training
file01.txt  file02.txt  file03.txt  file04.txt  file05.txt
</pre>
</div>
</details>
{{< /accordion >}}

4.tarコマンドを利用して、「tar_training」ディレクトリをアーカイブと同時に圧縮して、「tar_training.tar.gz」ファイルができたことを確認します。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ tar czf tar_training.tar.gz tar_training
$ ls
tar_training         ダウンロード  デスクトップ  ビデオ  画像
tar_training.tar.gz  テンプレート  ドキュメント  音楽    公開
</pre>
</div>
</details>
{{< /accordion >}}

5.「tar_training」ディレクトリを削除し、削除できたことを確認してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ rm -r tar_training
$ ls
tar_training.tar.gz  テンプレート  ドキュメント  音楽  公開
ダウンロード         デスクトップ  ビデオ        画像
</pre>
</div>
</details>
{{< /accordion >}}

6.「tar_training.tar.gz」ファイルを展開して、展開できたことを確認してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ tar xzf tar_training.tar.gz
$ ls
tar_training         ダウンロード  デスクトップ  ビデオ  画像
tar_training.tar.gz  テンプレート  ドキュメント  音楽    公開
</pre>
</div>
</details>
{{< /accordion >}}

7.「tar_training.tar.gz」ファイル、「tar_training」ディレクトリ、「training」ディレクトリを削除して、削除できたことを確認してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ rm -r tar_training.tar.gz tar_training
$ ls
ダウンロード  デスクトップ  ビデオ  画像
テンプレート  ドキュメント  音楽    公開
</pre>
</div>
</details>
{{< /accordion >}}

***

## 2.zipコマンド演習

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

2.「zip_training」ディレクトリを作成してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ mkdir zip_training
$ ls
zip_training  テンプレート  ドキュメント  音楽  公開
ダウンロード  デスクトップ  ビデオ        画像
</pre>
</div>
</details>
{{< /accordion >}}

3.touchコマンドを利用して「zip_training」ディレクトリの中にfile01.txt,file02.txt,file03.txt,file04.txt,file05.txt」ファイルを作成します。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ touch zip_training/file01.txt zip_training/file02.txt zip_training/file03.txt zip_training/file04.txt zip_training/file05.txt
$ ls zip_training
file01.txt  file02.txt  file03.txt  file04.txt  file05.txt
</pre>

<pre>
$ touch zip_training/{file01.txt,file02.txt,file03.txt,file04.txt,file05.txt}
$ ls zip_training
file01.txt  file02.txt  file03.txt  file04.txt  file05.txt
</pre>
</div>
</details>
{{< /accordion >}}

4.zipコマンドを利用して、「zip_training」ディレクトリを圧縮して、「zip_training.zip」ファイルができたことを確認します。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ zip -r zip_training.zip zip_training
zip -r zip_training.zip zip_training
adding: zip_training/ (stored 0%)
adding: zip_training/file01.txt (stored 0%)
adding: zip_training/file02.txt (stored 0%)
adding: zip_training/file03.txt (stored 0%)
adding: zip_training/file04.txt (stored 0%)
adding: zip_training/file05.txt (stored 0%)
$ ls
zip_training      ダウンロード  デスクトップ  ビデオ  画像
zip_training.zip  テンプレート  ドキュメント  音楽    公開
</pre>
</div>
</details>
{{< /accordion >}}

5.「zip_training」ディレクトリを削除し、削除できたことを確認してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ rm -r zip_training
$ ls
zip_training.zip  テンプレート  ドキュメント  音楽  公開
ダウンロード      デスクトップ  ビデオ        画像
</pre>
</div>
</details>
{{< /accordion >}}

6.「zip_training.zip」ファイルを展開して、展開できたことを確認してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ unzip zip_training.zip
  Archive:  zip_training.zip
  creating: zip_training/
extracting: zip_training/file01.txt
extracting: zip_training/file02.txt
extracting: zip_training/file03.txt
extracting: zip_training/file04.txt
extracting: zip_training/file05.txt
$ ls
zip_training      ダウンロード  デスクトップ  ビデオ  画像
zip_training.zip  テンプレート  ドキュメント  音楽    公開
</pre>
</div>
</details>
{{< /accordion >}}

7.「zip_training」ディレクトリをパスワード付けて圧縮してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ zip -er zip_training.zip zip_training
Enter password:linux
Verify password:linux
updating: zip_training/ (stored 0%)
updating: zip_training/file01.txt (stored 0%)
updating: zip_training/file02.txt (stored 0%)
updating: zip_training/file03.txt (stored 0%)
updating: zip_training/file04.txt (stored 0%)
updating: zip_training/file05.txt (stored 0%)
$ ls
zip_training      ダウンロード  デスクトップ  ビデオ  画像
zip_training.zip  テンプレート  ドキュメント  音楽    公開
</pre>
</div>
</details>
{{< /accordion >}}

8.パスワードの付いた「zip_training.zip」ファイルを設定したパスワードで解凍してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ unzip zip_training.zip
Archive:  zip_training.zip
[zip_training.zip] zip_training/file01.txt password:
replace zip_training/file01.txt? [y]es, [n]o, [A]ll, [N]one, [r]ename: A //Aと入力
  extracting: zip_training/file01.txt
  extracting: zip_training/file02.txt
  extracting: zip_training/file03.txt
  extracting: zip_training/file04.txt
  extracting: zip_training/file05.txt
$ ls
zip_training      ダウンロード  デスクトップ  ビデオ  画像
zip_training.zip  テンプレート  ドキュメント  音楽    公開
</pre>
</div>
</details>
{{< /accordion >}}

9.「zip_training」ディレクトリ、「zip_training.zip」ファイルを削除してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ rm -r zip_training zip_training.zip
$ ls
ダウンロード  デスクトップ  ビデオ  画像
テンプレート  ドキュメント  音楽    公開
</pre>
</div>
</details>
{{< /accordion >}}