# CVE-2021-4034(Pwnkit)の検証

## 概要

## 検証環境の構築

### 検証環境

| 構成要素 | 種類とバージョン |
|-|-|
| 脆弱性のあるソフトウェア | Polkit pkexec version 0.105 （パッチ未適用） |
| OS | Ubuntu 18.04.3 LTS (Linux 5.0.0-23-generic) |
| Compiler | gcc 7.5.0 |

### 環境構築

* Ubuntu 18.04.3をインストール
  * インストール時にソフトウェアのアップデートは行わない

## 攻撃手順

### 攻撃コードのダウンロード

* GitHubからCVE-2021-4034のPoCコード[^berdav/CVE-2021-4034]をダウンロード

### 攻撃コードの用意

* ダウンロードしたソースコードをコンパイル
  * 実行ファイル
  * ライブラリ
* 併せて必要な設定ファイルを作成
  * gconv-modules

```shell
$ make
```

### 攻撃コード実行

* シェルからPoCのコードを実行

```shell
$ ./cve-2021-4034
```

### ルート権限奪取

* `id`コマンドによりルート権限を取得できていることを確認

```shell
# id
```

[^berdav/CVE-2021-4034]: https://github.com/berdav/CVE-2021-4034

## 攻撃手法

## 攻撃の観測

## 影響範囲

## 対策

### 緩和策

#### SUIDビットの無効化

```shell
$ sudo chmod 0755 /usr/bin/pkexec
```

## References
