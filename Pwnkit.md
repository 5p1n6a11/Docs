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

1. Ubuntu 18.04.3をインストール
2. インストール時にソフトウェアのアップデートは行わない

## 攻撃手順

* GitHubからCVE-2021-4034のPoCコード[^berdav/CVE-2021-4034]をダウンロード
* ダウンロードしたソースコードをコンパイル

```shell
$ make
```

* シェルからPoCのコードを実行

```shell
$ ./cve-2021-4034
```

* `id`コマンドによりルート権限を取得できていることを確認

```shell
# id
```

[^berdav/CVE-2021-4034]: https://github.com/berdav/CVE-2021-4034

## 攻撃手法

## 攻撃の観測

## 影響範囲

## 対策

## References
