---
title: "3.Cloud Computing of All Term"
date: 2017-10-17T15:26:15Z
draft: false
weight: 10
description: "calling custom Shortcodes into your content files."
TableOfContents: true
---

## Training Environment & Practice Contents

### a.実践環境について

仮想マシン利用をベースとしてます。下記1~5については、パブリッククラウド等のインスタンス「vCPU1,Mem2GB以上」、3については、2台のインスタンスが必要となります。6のKubernetesについては「vCPU2,Mem4GB以上」2台のインスタンスが最低必要です。
OSは、下記1~5については、CentOS7.5以上を推奨、4、5についてはUbuntu18.04LTS以上でも可能。6については、Ubuntu18.04LTS以上を推奨とします。

### b.実践内容について

以下各ページの内容に従って実行してください。

#### 1.WordPress

* [1.WordPress Environment Construction - Nginx](chapter3-1/wp-environment-construction-nginx)
* [2.WordPress Environment Construction - PHP](chapter3-1/wp-environment-construction-php)
* [3.WordPress Environment Construction - MariaDB](chapter3-1/wp-environment-construction-mariadb)
* [4.WordPress Environment Construction - WordPress](chapter3-1/wp-environment-construction-wordpress)

#### 2.ECCUBE

* [1.ECCUBE Environment Construction - Apache Web Server](chapter3-2/eccube-environment-construction-httpd)
* [2.ECCUBE Environment Construction - PHP](chapter3-2/eccube-environment-construction-php)
* [3.ECCUBE Environment Construction - MariaDB](chapter3-2/eccube-environment-construction-mariadb)
* [4.ECCUBE Environment Construction - ECCUBE](chapter3-2/eccube-environment-construction-eccube)

#### 3.Ansible

2台のインスタンスを用意します。ホスト名はansible-serverとansible-hostとします。（ホスト名は任意名で構いません）

* [1.Ansible Environment Construction - SSH](chapter3-3/ansible-environment-construction-sshd)
* [2.Ansible Environment Construction - Ansible-Server](chapter3-3/ansible-environment-construction-ansible-server)
* [3.Ansible Environment Construction - Playbook & WordPress](chapter3-3/ansible-environment-construction-playbook-wp)

#### 4.Docker

* [1.Docker Environment Construction - Docker](chapter3-4/docker-environment-construction-docker)

#### 5.Docker Compose

* [1.Docker Environment Construction - Docker Compose](chapter3-5/docker-environment-construction-docker-compose)

#### 6.Kubernetes

2台のインスタンスを用意します。ホスト名はrancher-serverとrancher-hostとします。（ホスト名は任意名で構いません）

* [1.Kubernetes Environment Construction - Kubernetes](chapter3-6/kubernetes-environment-construction-kubernetes)
* [2.Kubernetes Environment Construction - kubectl](chapter3-6/kubernetes-environment-construction-kubectl)
* [3.Kubernetes Environment Construction - Kubernetes & WordPress](chapter3-6/kubernetes-environment-construction-kubernetes-wp)