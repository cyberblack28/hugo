---
title: "10.HTML & CSS"
date: 2017-10-17T15:26:15Z
draft: false
weight: 20
---

## 1.自己紹介ページの作成

自己紹介ページを作成してみましょう。

1.模範解答

```HTML
<!DOCTYPE html>
<html lang="ja">
    <head>
        <meta charset="UTF-8">
        <title>自己紹介</title>
        <link rel="stylesheet" type="text/css" href="css/beginner.css">
    </head>
        
    <body>
        <h1>自己紹介</h1>
        <ol>
            <li>名前：〇〇〇〇</li>
            <li>生年月日： 〇年〇月〇日</li>
            <li>趣味：ライブ・フェス参加及び鑑賞、夜景撮影(<a href="https://www.flickr.com/photos/cyberblack/" target="_blank">https://www.flickr.com/photos/cyberblack/</a>)</li>
            <li>好きなアーティスト：
                <ul>
                    <li>氷室京介</li>
                    <li>布袋寅泰</li>
                    <li>小室哲哉</li>
                    <li>坂本龍一</li>
                    <li>中田ヤスタカ</li>
                    <li>ヒイズミ・マサユ機</li>
                </ul>
                    好きなバンド：
                <ul>
                    <li>BOOWY</li>
                    <li>TM NETWORK</li>
                    <li>YMO</li>
                    <li>Perfume</li>
                    <li>サカナクション</li>
                    <li>マキシマムザホルモン</li>
                    <li>Man With A Mission</li>
                    <li>H ZETTRIO</li>
                    <li>MUSE</li>
                    <li>Radiohead</li>
                    <li>NIRVANA</li>
                </ul>
            </li>
            <li>好きな画像：<br><img src="images/pag.jpg" alt="パグ犬" width="100" height="100" /></li>
            <li>好きなページ：<a href="https://www.nttdocomo.co.jp/special_contents/future_experiment/" target="_blank">FUTURE-EXPERIMENT VOL.01 docomo×Perfume 距離をなくせ。</a></li>
            <li>所有資格：<br>
                <table class="profiletable">
                    <tr>
                        <th>資格ベンダー</th>
                        <th>資格名</th>
                    </tr>
                    <tr>
                        <td>CNCF</td>
                        <td>Certified Kubernetes Administrator（CKA）<br>Certified Kubernetes Application Developer（CKAD）</td>
                    </tr>
                    <tr>
                        <td>Mirantis</td>
                        <td>KCM100</td>
                    </tr>
                    <tr>
                            <td>Red Hat</td>
                            <td>RHCSA(Red Hat Certified System Administrator)</td>
                    </tr>
                    <tr>
                            <td>LPI-Japan</td>
                            <td>LPIC Level3 300 304</td>
                    </tr>
                </table>
            </li>
        </ol>
    </body>
</html>
```

***

## 2.自己紹介ページにCSSを適用

条件としては、文字は左寄せ、リストタグの4辺内側に10pxの幅とします。

1.模範解答

```CSS
body {
    background: #f2f2f2;
}

div {
    background: #ffffff;
    width: 400px;
    padding: 20px;
    text-align: left;
    border: 1px solid #cccccc;
    margin: 30px auto;
}

li {
    padding: 10px;
}

.profiletable th,td {
    border: solid 1px #000000;
  }
```