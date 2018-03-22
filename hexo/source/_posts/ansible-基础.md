---
layout: maintetechnology
title: ansible 基础
date: 2018-03-21 21:58:55
tags:
categories: mainteTechnology
---

## 一、简要
1. 基本概念

Ansible是一个部署一群远程主机的工具;Ansible通过SSH协议实现远程节点和管理节点之间的通信。理论上说，只要管理员通过ssh登录到一台远程主机上能做的操作，Ansible都可以做到。Ansible是python开发的,故依赖一些python库和组件,如:paramiko，PyYaml和jinja三个关键组件

2. 测试环境
ansible: CentOS7.4_x64 172.16.3.167 epel yum安装ansible
node1: 172.16.3.152 CenOS7.2_x64
node2: 172.16.3.216 CentOS7.2_x64
从ansible上生成ssh私钥同步到两台node主机上,实现无密钥登录管理(推荐)
```
[root@ansible ~]# ssh-keygen -t rsa
```
直接回车生成私钥;
同步到到两台node上
```
[root@ansible ~]# ssh-copy-id -i ~/.ssh/id_rsa  172.16.3.216
[root@ansible ~]# ssh-copy-id -i ~/.ssh/id_rsa  172.16.3.152
```
注意同步过程需要输入yes和各自的root密码即可;此进可直接ssh root@172.16.3.152 就无密码登录上去啦!
配置ansible的主机清单,即把node1与node2主机添加到管理清单中
```
[root@ansible ~]# egrep -v '(^$|^#)' /etc/ansible/hosts
[websrvs]
172.16.3.152
172.16.3.216
```