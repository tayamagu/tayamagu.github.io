---
layout: post
title: Inventoryファイル
date: 2016-08-02
tags: ansible
category: プロビジョニング
---

### Inventoryファイル

***ini形式で実行対象のホスト記述するファイル***

[参照：Inventory — Ansible Documentation](http://docs.ansible.com/ansible/intro_inventory.html)

- 対象ホストの設定
   - コマンド実行時に指定しなかった場合のデフォルトは/usr/local/etc/ansible/(OSXの場合)
   - []で囲むとグループ、それ以外はホストを表す
   - 正規表現やor/not/and指定なども可能
   
   
    mail.example.com

    [webservers]
    foo.example.com
    bar.example.com

    [dbservers]
    one.example.com
    two.example.com
    three.example.com

- ホストの設定
   - target-host: 任意のAnsible上でのターゲット・ホスト名。ansible_hostを指定しない場合、この名前が接続用の実ホスト名となる。
   - ansible_host: 実接続用のホスト名（vagrant ssh-configのホスト名に対応）
   - ansible_port: 接続用ポート番号
   - ansible_user: ログインユーザー名
   - ansible_connection: 接続形式


    [targets]

    localhost              ansible_connection=local
    other1.example.com     ansible_connection=ssh        ansible_user=mpdehaan
    other2.example.com     ansible_connection=ssh        ansible_user=mdehaan
    
> 
[パラメータ詳細は以下を参照  
List of Behavioral Inventory Parameters](http://docs.ansible.com/ansible/intro_inventory.html#list-of-behavioral-inventory-parameters)  

- 備考
  
 ***Note  
Ansible 2.0 has deprecated the “ssh” from ansible_ssh_user, ansible_ssh_host, and ansible_ssh_port to become ansible_user, ansible_host, and ansible_port. If you are using a version of Ansible prior to 2.0, you should continue using the older style variables (ansible_ssh_*). These shorter variables are ignored, without warning, in older versions of Ansible.***

 ***New in version 2.1.  
ansible_shell_executable
This sets the shell the ansible controller will use on the target machine, overrides executable in ansible.cfg which defaults to /bin/sh. You should really only change it if is not possible to use /bin/sh (i.e. /bin/sh is not installed on the target machine or cannot be run from sudo.).***

 [※動的なInventory設定は以下を参照
 DynamicInventory](http://docs.ansible.com/ansible/intro_dynamic_inventory.html)