---
title: "11.Javascript"
date: 2017-10-17T15:26:15Z
draft: false
weight: 20
---

## 1.都道府県のドロップボックス作成

for文と配列を組み合わせて右のような都道府県ドロップボックスを作成してみましょう。

1.模範解答

```HTML
<!DOCTYPE html>
<html lang="ja">

    <head>
        <meta charset="UTF-8">
        <title>初めてのJavaScript</title>
    </head>

    <body>

        <p>都道府県</p>

        <select name="pref">
            <script>
                var prefs = new Array('北海道', '青森県', '岩手県', '宮城県', '秋田県', '山形県', '福島県', '茨城県', '栃木県', '群馬県', '埼玉県', '千葉県', '東京都', '神奈川県', '新潟県', '富山県', '石川県', '福井県', '山梨県', '長野県', '岐阜県', '静岡県', '愛知県', '三重県', '滋賀県', '京都府', '大阪府', '兵庫県', '奈良県', '和歌山県', '鳥取県', '島根県', '岡山県', '広島県', '山口県', '徳島県', '香川県', '愛媛県', '高知県', '福岡県', '佐賀県', '長崎県', '熊本県', '大分県', '宮崎県', '鹿児島県', '沖縄県');

                for (var i=0; i<prefs.length; i++) {
                    document.write('<option value="' + prefs[i] + '">' + prefs[i] + '</option>');
                }
            </script>

        </select>

    </body>

</html>
```

***

## 2.おみくじプログラムの作成

Mathオブジェクト、alertメソッド、switch文を使ってプログラミングしてみよう。
大吉、中吉、末吉、小吉、大凶でそれぞれメッセージも入れましょう。

1.模範解答

```HTML
<!DOCTYPE html>
<html lang="ja">

    <head>
        <meta charset="UTF-8">
        <title>初めてのJavaScript</title>
    </head>

    <body>
 
            <script>
                    var a = Math.random() * 5;
                    a = Math.floor(a);
    
                    switch (a) {
                        case 0:
                            alert('大吉　成功あるのみ');
                            break;
                        case 1:
                            alert('中吉　幸せはすぐそこ');
                            break;
                        case 3:
                            alert('小吉　ささやかな喜びに感謝');
                            break;
                        case 4:
                            alert('末吉　明日頑張ろう');
                            break;
                        case 5:
                            alert('凶　今はじっと我慢');
                            break;
                    }
            </script>

    </body>

</html>
```

***

## 3.カウントアッププログラムの作成

カウントアップというボタンをクリックすると数値が上がっていくアプリを作ってみよう。リセットボタンを押すと0に戻るようにしてみよう。

1.模範解答

```HTML
<!DOCTYPE html>
<html lang="ja">

    <head>
        <meta charset="UTF-8">
        <title>初めてのJavaScript</title>
    </head>

    <body>
        
            <script>
            var count = 0;
            function countup() {
                document.getElementById( "output" ).innerHTML = ++count;
            }

            function reset() {
                location.reload()
            }
            </script>
            
            <p><button onclick="countup();">カウントアップ</button> <button onclick="reset();">リセット</button><br><span id="output">0</span></p>

    </body>
```

***

## 4.サンプルプログラム

1.アラートボックス表示

```HTML
<!DOCTYPE html>
<html lang="ja">

	<head>
		<meta charset="UTF-8">
		<title>初めてのJavaScript</title>
	</head>

	<body>

		<script>
			window.alert('初めてのJavaScript');
		</script>

	</body>

</html>
```

2.if分

```HTML
<!DOCTYPE html>
<html lang="ja">

	<head>
		<meta charset="UTF-8">
		<title>初めてのJavaScript</title>
	</head>

	<body>

		<script>
			if ( confirm ('保存しますか？') ) {
				alert ('保存しました。');
			} else {
				alert ('キャンセルしました。');
			}
		</script>

	</body>

</html>
```

3.変数

```HTML
<!DOCTYPE html>
<html lang="ja">

	<head>
		<meta charset="UTF-8">
		<title>初めてのJavaScript</title>
	</head>

	<body>

		<script>
			var answer = confirm ('保存しますか？');

			if (answer) {
				alert ('保存しました。');
			} else {
				alert ('キャンセルしました。');
			}
		</script>

	</body>

</html>
```

4.四則演算

```HTML
<!DOCTYPE html>
<html lang="ja">

	<head>
		<meta charset="UTF-8">
		<title>初めてのJavaScript</title>
	</head>

	<body>

		<script>
			document.write('<p>1年を365日とした場合</p>');
			document.write('<p>1年は' + (365*24) + '時間です。</p>');
			document.write('<p>1年は' + (365*24*60) + '分です。</p>');
			document.write('<p>1年は' + (365*24*60*60) + '秒です。</p>');
		</script>

	</body>

</html>
```

5.比較演算子

```HTML
<!DOCTYPE html>
<html lang="ja">

	<head>
		<meta charset="UTF-8">
		<title>初めてのJavaScript</title>
	</head>

	<body>

		<script>
			var now = new Date();
			var hour = now.getHours();

			if (hour < 12) {
				window.alert ('今は午前' + hour + '時です');
			} else {
				window.alert ('今は午後' + hour + '時です');
			}
		</script>

	</body>

</html>
```

6.論理演算子

```HTML
<!DOCTYPE html>
<html lang="ja">

	<head>
		<meta charset="UTF-8">
		<title>初めてのJavaScript</title>
	</head>

	<body>

		<script>
			var now = new Date();
			var hour = now.getHours();

			if (hour >= 14 && hour < 16) {
				window.alert('タイムセール中です。');
			}
		</script>

	</body>

</html>
```

7.while文

```HTML
<!DOCTYPE html>
<html lang="ja">

	<head>
		<meta charset="UTF-8">
		<title>初めてのJavaScript</title>
	</head>

	<body>

	<select>

 	<script>
 		var i = 10;

                while (i<=80){
			document.write('<option value="' + i + '">' + i + '歳</option>');
			i++;
		}
	</script>

	</select>

	</body>

</html>
```

8.for文

```HTML
<!DOCTYPE html>
<html lang="ja">

	<head>
		<meta charset="UTF-8">
		<title>初めてのJavaScript</title>
	</head>

	<body>

	<select>

 	<script>

		for (var i=10; i<=80; i++){
			document.write('<option value="' + i + '">' + i + '歳</option>');
                	}

	</script>

	</select>

	</body>

</html>
```

9.配列

```HTML
<!DOCTYPE html>
<html lang="ja">

	<head>
		<meta charset="UTF-8">
		<title>初めてのJavaScript</title>
	</head>

	<body>

	<ul>

 	<script>
		var menus = new Array('AWS','GCP','Azure','IBM cloud');

		for (var i=0; i<menus.length; i++){
			document.write('<li>' + menus[i] + '</li>');
		}
	</script>

	</ul>

	</body>

</html>
```

10.連想配列

```HTML
<!DOCTYPE html>
<html lang="ja">

	<head>
		<meta charset="UTF-8">
		<title>初めてのJavaScript</title>
	</head>

	<body>

	<ul>

 	<script>
 		var menus = {
                        		'https://aws.amazon.com/jp/':'AWS',
                        		'https://cloud.google.com/?hl=ja':'GCP',
                        		'https://azure.microsoft.com/ja-jp/':'Azure',
                        		'https://www.ibm.com/cloud-computing/':'IBM Cloud'
		}

		for (var m in menus) {
			document.write('<li><a href="' + m + '" title="' + m + 'に移動します" target="_blank">' + menus[m] + '</a></li>');
		}
	</script>

	</ul>

	</body>

</html>
```

11.イベント

open.html

```HTML
<!DOCTYPE html>
<html lang="ja">

	<head>
		<meta charset="UTF-8">
		<title>初めてのJavaScript</title>
	</head>

	<body>

	<script>
		window.open('index.html');
	</script>

	</body>

</html>
```

index.html

```HTML
<!DOCTYPE html>
<html lang="ja">

	<head>
		<meta charset="UTF-8">
		<title>初めてのJavaScript</title>
		<script src="js/onclick.js"></script>
	</head>

	<body>
		<p><input type="button" value="とじる" onclick="closebt();"></p>
	</body>

</html>
```

onclick.js

```Javascript
function closebt() {
	if(confirm('閉じてよろしいですか？')){
		window.close();
	}
}
```

12.switchとif else

```HTML
<!DOCTYPE html>
<html lang="ja">

	<head>
		<meta charset="UTF-8">
		<title>初めてのJavaScript</title>
	</head>

	<body>

 		<p>年齢</p>

        	<select id="age" name="age">
            		<option value="">お選びください</option>
            		<option value="10">10歳以下</option>
            		<option value="30">11-30歳</option>
            		<option value="50">31-50歳</option>
            		<option value="51">51歳以上</option>
        	</select>

        	<script>
            		document.getElementById('age').onchange = function() { var age = document.getElementById('age').value;
        
            		switch (age) {
            			case '10':
                			alert('10歳以下の方は、半額です');
                			break;
           			case '30':
                			alert('11-30歳以下の方は割引はありません');
                			break;
            			case '50':
                			alert('31-50歳の方は10%の割引です');
                			break;
            			case '51':
                			alert('51歳の方は30%の割引です');
                			break;
            			}
        		}
        	</script>

	</body>

</html>
```