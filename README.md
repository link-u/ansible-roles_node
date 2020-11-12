# Node.js

![ansible ci](https://github.com/link-u/ansible-roles_node/workflows/ansible%20ci/badge.svg)

## 1. 目次

<!-- TOC depthFrom:2 -->

- [1. 目次](#1-目次)
- [2. 概要](#2-概要)
- [3. 動作確認バージョン](#3-動作確認バージョン)
- [4. 使い方 (ansible)](#4-使い方-ansible)
    - [4.1. Role variables](#41-role-variables)
    - [4.2. Example Playbook](#42-example-playbook)
- [5. ローカルホスト (つまり自分の PC ) にインストールする方法](#5-ローカルホスト-つまり自分の-pc--にインストールする方法)
    - [5.1. 概要](#51-概要)
    - [5.2. プレイブックの実行例](#52-プレイブックの実行例)
- [6. License](#6-license)

<!-- /TOC -->

## 2. 概要

Node.js と npm のインストールをする ansible role.

本 role では [n](https://github.com/tj/n) という Node.js と npm のバージョンを管理するツールを用いて任意のディレクトリに Node.js と npm をインストールする.

<br>

## 3. 動作確認バージョン

* Ubuntu: 18.04, 20.04
* ansible: 2.8, 2.9

<br>

## 4. 使い方 (ansible)

### 4.1. Role variables

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

### 4.2. Example Playbook

```yaml
- hosts:
    - servers
  become: True
  roles:
    - { role: node, tags: ["node"] }
```

<br>

## 5. ローカルホスト (つまり自分の PC ) にインストールする方法

### 5.1. 概要

以下のプレイブックを実行することで, 自分の PC に Node.js をインストールすることができる.

* [playbooks/install_to_localhost.yml](playbooks/install_to_localhost.yml)

ただしユーザ権限で実行できるように, 以下のパッケージのインストールタスクはスキップしている (つまり, `node_skip_pre_install_packages: yes' としている. 

そのため, 予め自分で依存するパッケージをインストールする必要がある.

```
## Ubuntu
$ sudo apt update && sudo apt -y install build-essential rsync curl git
```

<br>

### 5.2. プレイブックの実行例

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

## 6. License
MIT
