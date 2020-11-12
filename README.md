# Node.js

![ansible ci](https://github.com/link-u/ansible-roles_node/workflows/ansible%20ci/badge.svg)

## 目次

<!-- TOC depthFrom:2 -->

- [目次](#目次)
- [1. 概要](#1-概要)
- [2. 動作確認バージョン](#2-動作確認バージョン)
- [3. 使い方 (ansible)](#3-使い方-ansible)
    - [3.1. Role variables](#31-role-variables)
    - [3.2. Example Playbook](#32-example-playbook)
- [4. ローカルホスト (つまり自分の PC ) にインストールする方法](#4-ローカルホスト-つまり自分の-pc--にインストールする方法)
    - [4.1. プレイブックの実行例](#41-プレイブックの実行例)
- [5. License](#5-license)

<!-- /TOC -->

## 1. 概要

Node.js と npm のインストールをする ansible role.

本 role では [n](https://github.com/tj/n) という Node.js と npm のバージョンを管理するツールを用いて任意のディレクトリに Node.js と npm をインストールする.

<br>

## 2. 動作確認バージョン

* Ubuntu: 18.04, 20.04
* ansible: 2.8, 2.9

<br>

## 3. 使い方 (ansible)

### 3.1. Role variables

```yaml
## Node.js のバージョンの指定
node_install_version: "stable"
# 設定例
# node_install_version: "14.8.0"
# node_install_version: "14"

## npm のバージョンの指定
node_npm_version: "latest"
# 設定例
# node_npm_version: "6.14.8"
# node_npm_version: "6"

node_prefix: "/usr/local"
```

<br>

### 3.2. Example Playbook

```yaml
- hosts:
    - servers
  become: True
  roles:
    - { role: node, tags: ["node"] }
```

<br>

## 4. ローカルホスト (つまり自分の PC ) にインストールする方法

以下のプレイブックを実行することで, 自分の PC に Node.js をインストールすることができる.

* [playbooks/install_to_localhost.yml](playbooks/install_to_localhost.yml)

ただしユーザ権限で実行できるように, 以下のパッケージのインストールタスクはスキップしている (つまり, `node_skip_pre_install_packages: yes' としている. 

そのため, 予め自分でインストールする必要がある.

```
## Ubuntu
$ sudo apt update && sudo apt -y install build-essential rsync curl git
```

<br>

### 4.1. プレイブックの実行例

```
## 単にプレイブックを実行 (default/main.yml の値を使用)
$ ansible-playbook playbooks/install_to_localhost.yml

## Node.js のバージョンを指定
$ ansible-playbook playbooks/install_to_localhost.yml \
  -e node_install_version="14"

## npm のバージョンを指定
$ ansible-playbook playbooks/install_to_localhost.yml \
  -e node_npm_version="6"

## Node.js と npm のバージョンを指定
$ ansible-playbook playbooks/install_to_localhost.yml \
  -e node_install_version="14" \
  -e node_npm_version="6"
```

<br>

## 5. License
MIT
