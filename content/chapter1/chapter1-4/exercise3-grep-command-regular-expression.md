---
title: "Exercise3 grep command & regular expression"
date: 2017-10-17T15:26:15Z
draft: false
weight: 10
---

## 1.grepコマンドと正規表現を組み合わせて/etc/passwdを確認する

1./etc/passwdファイルの中で、studentという文字列を含む行のみを表示してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ grep student /etc/passwd
student:x:1000:1000:student:/home/student:/bin/bash
</pre>
</div>
</details>
{{< /accordion >}}

2.1で実行したコマンドは、「行内にuserという文字列を含む行」がすべて表示されます。次は、/etc/passwdファイルの中で、行頭がstudentで始まる行のみを表示してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ grep student /etc/passwd
student:x:1000:1000:student:/home/student:/bin/bash
</pre>
</div>
</details>
{{< /accordion >}}

3.2で実行したコマンドは、ユーザ名以外の情報（UIDやGID、ホームディレクトリのパス、デフォルトのシェル）が表示されます。パイプラインを使って、他のコマンドと組み合わせて、ユーザ名とホームディレクトリのみを表示するように変更してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ grep '^student' /etc/passwd | cut -d : -f 1,6
student:/home/student
</pre>
</div>
</details>
{{< /accordion >}}

4.ログインシェルがbashであるユーザを表示してください。行末がbashという観点で考えてみましょう。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ grep -n 'bash$' /etc/passwd
1:root:x:0:0:root:/root:/bin/bash
44:student:x:1000:1000:student:/home/student:/bin/bash
</pre>
</div>
</details>
{{< /accordion >}}

***

## 2.grepコマンドと正規表現を組み合わせてWebサーバのログファイルを確認する

1.サンプル用のログファイルをダウンロードして、解凍します。

```
$ wget https://cyberblack28.github.io/learning/tokyoec/linux/zip/sample_web.zip
--2020-01-28 00:45:48--  https://cyberblack28.github.io/learning/tokyoec/linux/zip/sample_web.zip
cyberblack28.github.io (cyberblack28.github.io) をDNSに問いあわせています... 185.199.110.153, 185.199.108.153, 185.199.109.153, ...
cyberblack28.github.io (cyberblack28.github.io)|185.199.110.153|:443 に接続して います... 接続しました。
HTTP による接続要求を送信しました、応答を待っています... 200 OK
長さ: 425285 (415K) [application/zip]
`sample_web.zip' に保存中
  
sample_web.zip      100%[===================>] 415.32K  --.-KB/s 時間 0.06s
  
2020-01-28 00:45:48 (6.66 MB/s) - `sample_web.zip' へ保存完了 [425285/425285]
```

```
$ unzip sample_web.zip
Archive:  sample_web.zip
  inflating: sample_web.log
```

```
$ ls -l
合計 4712
-rw-rw-r--. 1 student student 4398816  3月 17  2016 sample_web.log
-rw-rw-r--. 1 student student  425285  1月 27 23:42 sample_web.zip
drwxrwxr-x. 2 student student      44  1月 27 23:14 script_dir
drwxr-xr-x. 2 student student       6  1月 21 00:23 ダウンロード
drwxr-xr-x. 2 student student       6  1月 21 00:23 テンプレート
drwxr-xr-x. 2 student student       6  1月 21 00:23 デスクトップ
drwxr-xr-x. 2 student student       6  1月 21 00:23 ドキュメント
drwxr-xr-x. 2 student student       6  1月 21 00:23 ビデオ
drwxr-xr-x. 2 student student       6  1月 21 00:23 音楽
drwxr-xr-x. 2 student student       6  1月 21 00:23 画像
drwxr-xr-x. 2 student student       6  1月 21 00:23 公開
```

2.sample_web.logの行数を確認してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ wc -l sample_web.log
20001 sample_web.log
</pre>
</div>
</details>
{{< /accordion >}}

3.Mac OSユーザのアクセス件数を調べてください。Mac OSという文字列を含む行の行数をカウントします。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ grep -c 'Mac OS' sample_web.log
3092
</pre>
</div>
</details>
{{< /accordion >}}

4.Mac OSユーザで、かつSafariユーザのアクセス件数を調べてください。

Mac OSという文字列を含む行をgrepし、その結果に対してさらにSafariを含む行をgrepし、行数をカウントします。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ grep 'Mac OS' sample_web.log | grep -c Safari
1239
</pre>
</div>
</details>
{{< /accordion >}}

5.2016年3月17日の10時台のアクセスについて、次の質問に解答してください。

- アクセス数を検索してください。
- 10時台の最初にアクセスがあった時間を検索してください。
- 10時台の最後にアクセスがあった時間を検索してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
//a.アクセス数を検索してください。
$ grep '17/Mar/2016:10:' sample_web.log | wc -l
3470
</pre>

<pre>
//b.10時台の最初にアクセスがあった時間を検索してください。
$ grep '17/Mar/2016:10:' sample_web.log | head -n 1
36.33.129.83 - - [17/Mar/2016:10:08:15 +0900] "GET /item/sports/520 HTTP/1.1" 200 77 "http://www.google.com/search?ie=UTF-8&q=google&sclient=psy-ab&q=Sports+Office&oq=Sports+Office&aq=f&aqi=g-vL1&aql=&pbx=1&bav=on.2,or.r_gc.r_pw.r_qf.,cf.osb&biw=4862&bih=63" "Mozilla/5.0 (Windows NT 6.0; rv:10.0.1) Gecko/20100101 Firefox/10.0.1"
</pre>

<pre>
//c.10時台の最後にアクセスがあった時間を検索してください。
$ grep '17/Mar/2016:10:' sample_web.log | tail -n 1
60.33.46.128 - - [17/Mar/2016:10:40:29 +0900] "GET /category/electronics HTTP/1.1" 200 47 "-" "Mozilla/5.0 (compatible; MSIE 9.0; Windows NT 6.1; Trident/5.0)"
</pre>
</div>
</details>
{{< /accordion >}}

6.ログファイル内のアクセスので、Googlebot（ウェブクロール用bot。検索のための情報収集を行っている）以外からのアクセス数を確認してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ grep -v Googlebot sample_web.log | wc -l
18657
</pre>
</div>
</details>
{{< /accordion >}}