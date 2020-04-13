---
title: "Exercise4 Advanced Text Processing"
date: 2017-10-17T15:26:15Z
draft: false
weight: 10
---

## 1.sedによる文字列の置き換え

1.vimコマンドで、company.txtという名前で以下の内容が記載されているファイルを作成します。

{{< accordion >}}
Google<br>
Google<br>
Google<br>
Google<br>
Apple<br>
Apple<br>
Microsoft<br>
Microsoft<br>
{{< /accordion >}}

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ vim company.txt

----------------以下を右クリックコピーしてTeraTerm上でペースト----------------------
Google
Google
Google
Google
Apple
Apple
Microsoft
Microsoft
----------------[Esc + :wq]で保存終了---------------------------------------------
</pre>
</div>
</details>
{{< /accordion >}}

2.GoogleをIBMに置換してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ sed 's/Google/IBM/g' company.txt
IBM
IBM
IBM
IBM
Apple
Apple
Microsoft
Microsoft
</pre>
</div>
</details>
{{< /accordion >}}

3.正規表現を利用して、Aで始まりeで終わる文字列をFacebookに置換してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ sed 's/A.*e/Facebook/g' company.txt
Google
Google
Google
Google
Facebook
Facebook
Microsoft
Microsoft
</pre>
</div>
</details>
{{< /accordion >}}

4.2,3は標準出力に結果が表示されるだけなので、元ファイルの内容は変更されません。-iオプションを利用して、ファイルを上書きしてみます。Mで始まりtで終わる文字列をRedHatに置換してください。

{{< accordion >}}
<details style="margin-top: 10px;">
<summary>Answer</summary>
<div>
<pre>
$ sed -i 's/M.*t/RedHat/g' company.txt
$ cat company.txt
Google
Google
Google
Google
Apple
Apple
RedHat
RedHat
</pre>
</div>
</details>
{{< /accordion >}}