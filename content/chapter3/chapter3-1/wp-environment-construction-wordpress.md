---
title: "4.WordPress Environment Construction - WordPress"
date: 2017-10-17T15:26:15Z
draft: false
weight: 10
---

## 1.WordPressのインストール手順

1.WordPress最新版のダウンロード

```
# cd /usr/share/nginx/html/
```

```
# wget https://ja.wordpress.org/latest-ja.tar.gz
--2020-02-12 15:08:35--  https://ja.wordpress.org/latest-ja.tar.gz
Resolving ja.wordpress.org (ja.wordpress.org)... 198.143.164.252
Connecting to ja.wordpress.org (ja.wordpress.org)|198.143.164.252|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 12479892 (12M) [application/octet-stream]
Saving to: ‘latest-ja.tar.gz’

100%[===================================================================================================================>] 12,479,892  4.18MB/s   in 2.8s

2020-02-12 15:08:38 (4.18 MB/s) - ‘latest-ja.tar.gz’ saved [12479892/12479892]
```

2.tarコマンドで展開

```
# tar xvzf latest-ja.tar.gz
wordpress/
・
・省略
・
wordpress/wp-links-opml.php                              enabled
```

3.wordpressディレクトリの所有者をnginxに変更

```
# chown -R nginx:nginx /usr/share/nginx/html/wordpress/
```

```
# ls -l /usr/share/nginx/html/wordpress/
total 220
-rw-r--r--  1 nginx nginx   420 Dec  1  2017 index.php
-rw-r--r--  1 nginx nginx 19935 Jan  2  2019 license.txt
-rw-r--r--  1 nginx nginx 10180 Jan  2 14:00 readme.html
-rw-r--r--  1 nginx nginx  6939 Sep  3 09:41 wp-activate.php
drwxr-xr-x  9 nginx nginx  4096 Jan  2 14:00 wp-admin
-rw-r--r--  1 nginx nginx   369 Dec  1  2017 wp-blog-header.php
-rw-r--r--  1 nginx nginx  2283 Jan 21  2019 wp-comments-post.php
-rw-rw-rw-  1 nginx nginx  4223 Feb 12 16:15 wp-config.php
-rw-r--r--  1 nginx nginx  3944 Jan  2 14:00 wp-config-sample.php
drwxr-xr-x  7 nginx nginx  4096 Feb 12 16:16 wp-content
-rw-r--r--  1 nginx nginx  3955 Oct 11 07:52 wp-cron.php
drwxr-xr-x 20 nginx nginx 12288 Jan  2 14:00 wp-includes
-rw-r--r--  1 nginx nginx  2504 Sep  3 09:41 wp-links-opml.php
-rw-r--r--  1 nginx nginx  3326 Sep  3 09:41 wp-load.php
-rw-r--r--  1 nginx nginx 47597 Dec  9 22:30 wp-login.php
-rw-r--r--  1 nginx nginx  8483 Sep  3 09:41 wp-mail.php
-rw-r--r--  1 nginx nginx 19120 Oct 16 00:37 wp-settings.php
-rw-r--r--  1 nginx nginx 31112 Sep  3 09:41 wp-signup.php
-rw-r--r--  1 nginx nginx  4764 Dec  1  2017 wp-trackback.php
-rw-r--r--  1 nginx nginx  3150 Jul  1  2019 xmlrpc.php
```

4.「/etc/nginx/conf.d/default.conf」を設定

{{< accordion >}}
<div>
<pre>
# vim /etc/nginx/conf.d/default.conf

---------------------以下赤字の内容に設定変更-------------------------------
server {
    listen       80;
    server_name  localhost;

    #charset koi8-r;
    #access_log  /var/log/nginx/host.access.log  main;

    location / {
        root   /usr/share/nginx/html;
        index  index.html index.htm index.php; <font color="Red">//←「index  index.html index.htm;」変更⇒「index  index.html index.htm index.php;」</font>
        allow all; <font color="Red">//←追記</font>
    }

    #error_page  404              /404.html;

    # redirect server error pages to the static page /50x.html
    #
    error_page   500 502 503 504  /50x.html;
    location = /50x.html {
        root   /usr/share/nginx/html;
    }

    # proxy the PHP scripts to Apache listening on 127.0.0.1:80
    #
    #location ~ \.php$ {
    #    proxy_pass   http://127.0.0.1;
    #}

    # pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
    #
    <font color="Red">//⇓先頭の#を削除//</font>
    location ~ \.php$ {
        root           /usr/share/nginx/html; <font color="Red">//←「html」変更⇒「/usr/share/nginx/html」</font>
        fastcgi_pass   127.0.0.1:9000;
        fastcgi_index  index.php;
        #fastcgi_param  SCRIPT_FILENAME  /scripts$fastcgi_script_name; <font color="Red">//←#を付けてコメントアウト</font>
        fastcgi_param  SCRIPT_FILENAME  $document_root$fastcgi_script_name;　<font color="Red">//←追記</font>
        include        fastcgi_params;
    <font color="Red">//⇑先頭の#を削除//</font>
    }

    # deny access to .htaccess files, if Apache's document root
    # concurs with nginx's one
    #
    #location ~ /\.ht {
    #    deny  all;
    #}
}
---------------------[Esc + :wq]で保存終了します。-------------------------
</pre>
</div>
{{< /accordion >}}

5.Nginxの再起動

```
# systemctl restart nginx
```

```
# systemctl status nginx
● nginx.service - nginx - high performance web server
   Loaded: loaded (/usr/lib/systemd/system/nginx.service; enabled; vendor preset: disabled)
   Active: active (running) since Wed 2020-02-12 16:14:08 KST; 15min ago
     Docs: http://nginx.org/en/docs/
  Process: 11510 ExecStop=/bin/kill -s TERM $MAINPID (code=exited, status=0/SUCCESS)
  Process: 11512 ExecStart=/usr/sbin/nginx -c /etc/nginx/nginx.conf (code=exited, status=0/SUCCESS)
 Main PID: 11513 (nginx)
   CGroup: /system.slice/nginx.service
           tq11513 nginx: master process /usr/sbin/nginx -c /etc/nginx/nginx.conf
           mq11514 nginx: worker process

Feb 12 16:14:08 wordpress.novalocal systemd[1]: Starting nginx - high performance web server...
Feb 12 16:14:08 wordpress.novalocal systemd[1]: Started nginx - high performance web server.
```

6.ブラウザを起動して「http://グローバルIP/wordpress/」にアクセス