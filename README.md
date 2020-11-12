# Node.js

Nodeのインストールを行う。

## 概要

Node.js と npm のインストールする ansible role.

本 role では [n](https://github.com/tj/n) という Node.js と npm のバージョンを管理するツールを用いて任意のディレクトリに Node.js と npm をインストールする.

## 動作確認バージョン

comming soon...

## 使い方 (ansible)

### Role variables

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


### Example Playbook

```yaml
- hosts:
    - servers
  become: True
  roles:
    - { role: node, tags: ["node"] }
```

## License
MIT
