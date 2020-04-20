---
title: "3.Ansible Environment Construction - Playbook & WordPress"
date: 2017-10-17T15:26:15Z
draft: false
weight: 10
---

## Playbookの作成・WordPress環境構築手順

ansible-server作業

1.wordpress.ymlの作成

※「hosts: ansible-hostのグローバルIP」箇所の書換を忘れないようにしましょう。

```
# vim wordpress.yml
```

```YAML
---
 - name: wordpress環境構築
   hosts: ansible-hostのグローバルIP
   remote_user: root
   become: yes
   vars:
     wordpress_url: https://ja.wordpress.org/latest-ja.tar.gz
     mysql_user: wordpress
     mysql_password: wppass
     mysql_database: wordpress
     mysql_root_password: mariadb123
            
   tasks:
   - name: Apache（httpd）のインストール
     yum: name=httpd state=latest
            
   - name: サービスの起動
     service: name=httpd state=started enabled=yes

   - name: リポジトリ追加
     yum: name=epel-release state=latest

   - name: rpm配置
     get_url:
       url=http://rpms.famillecollet.com/enterprise/remi-release-7.rpm
       dest=/tmp/remi-release-7.rpm

   - name: rpmのインストール
     yum:
       name: /tmp/remi-release-7.rpm
       state: present

   - name: PHPのインストール
     yum: name="{{item}}" enablerepo=epel,remi-php72 state=latest
     with_items:
      - php-mysql
      - php
      - php-devel
      - php-mbstring
      - php-pdo
      - php-gd
      - php-mcrypt
      - libmcrypt

   - name: タイムゾーンの設定
     ini_file: >
      dest=/etc/php.ini
      section=Date
      option=date.timezone
      value='"Asia/Tokyo"'

   - name: httpサービスの再起動
     service: name=httpd state=restarted enabled=yes

   - name: MariaDBインストール
     yum: name="{{item}}" state=latest
     with_items:
      - mariadb
      - mariadb-server
      - MySQL-python

   - name: サービスの起動
     service: name=mariadb state=started enabled=yes

   - name: WordPress用データベースの作成
     mysql_db: name={{ mysql_database }} state=present

   - name: WordPress用データベースユーザの作成
     mysql_user: name={{ mysql_user }} host={{ item }} password={{ mysql_password }} priv={{ mysql_database }}.*:ALL,GRANT state=present
     with_items:
       - localhost

   - name: MariaDB rootパスワード設定
     mysql_user: name=root
                 host=localhost
                 password="{{ mysql_root_password }}"
                 check_implicit_admin=yes
                 login_user="{{ mysql_user }}"
                 login_password="{{ mysql_root_password }}"
                 state=present

   - name: wordpressのダウンロード
     get_url:
       url="{{ wordpress_url }}"
       dest=/tmp/wordpress.tar.gz
            
   - name: wordpressの展開
     unarchive: src=/tmp/wordpress.tar.gz dest=/var/www/html/ copy=no
            
   - name: wordpressの所有権をapacheに変更
     file: path=/var/www/html/wordpress/ owner=apache group=apache recurse=yes
            
   - name: httpサービスの起動
     service: name=httpd state=restarted
```

2.ansibleの実行

```
# ansible-playbook wordpress.yml

PLAY [wordpress環境構築] ***********************************************************

TASK [Gathering Facts] *********************************************************
ok: [133.186.208.195]
  
TASK [Apache（httpd）のインストール] ****************************************************
  
changed: [133.186.208.195]
  
TASK [サービスの起動] *****************************************************************
changed: [133.186.208.195]
  
TASK [リポジトリ追加] *****************************************************************
changed: [133.186.208.195]
  
TASK [rpm配置] *******************************************************************
changed: [133.186.208.195]
  
TASK [rpmのインストール] **************************************************************
changed: [133.186.208.195]
  
TASK [PHPのインストール] **************************************************************
[DEPRECATION WARNING]: Invoking "yum" only once while using a loop via
squash_actions is deprecated. Instead of using a loop to supply multiple items
and specifying `name: "{{item}}"`, please use `name: ['php-mysql', 'php', 'php-
devel', 'php-mbstring', 'php-pdo', 'php-gd', 'php-mcrypt', 'libmcrypt']` and
remove the loop. This feature will be removed in version 2.11. Deprecation
warnings can be disabled by setting deprecation_warnings=False in ansible.cfg.
changed: [133.186.208.195] => (item=[u'php-mysql', u'php', u'php-devel', u'php-mbstring', u'php-pdo', u'php-gd', u'php-mcrypt', u'libmcrypt'])
  
TASK [タイムゾーンの設定] ***************************************************************
changed: [133.186.208.195]
  
TASK [httpサービスの再起動] ************************************************************
changed: [133.186.208.195]
  
TASK [MariaDBインストール] ***********************************************************
[DEPRECATION WARNING]: Invoking "yum" only once while using a loop via
squash_actions is deprecated. Instead of using a loop to supply multiple items
and specifying `name: "{{item}}"`, please use `name: ['mariadb', 'mariadb-
server', 'MySQL-python']` and remove the loop. This feature will be removed in
version 2.11. Deprecation warnings can be disabled by setting
deprecation_warnings=False in ansible.cfg.
changed: [133.186.208.195] => (item=[u'mariadb', u'mariadb-server', u'MySQL-python'])
  
TASK [サービスの起動] *****************************************************************
changed: [133.186.208.195]
  
TASK [WordPress用データベースの作成] *****************************************************
changed: [133.186.208.195]
  
TASK [WordPress用データベースユーザの作成] **************************************************
changed: [133.186.208.195] => (item=localhost)
  
TASK [MariaDB rootパスワード設定] **************************************************
changed: [133.186.208.195]
  
TASK [wordpressのダウンロード] ********************************************************
changed: [133.186.208.195]
  
TASK [wordpressの展開] ************************************************************
changed: [133.186.208.195]
  
TASK [wordpressの所有権をapacheに変更] *************************************************
changed: [133.186.208.195]
  
TASK [httpサービスの起動] *************************************************************
changed: [133.186.208.195]
  
PLAY RECAP *********************************************************************
133.186.208.195            : ok=18   changed=17   unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

3.ブラウザを起動して「http://ansible-hostのグローバルIP/wordpress/」にアクセス