# CVE-2021-4034(Pwnkit)の検証

## 目次

* [はじめに](#はじめに)
* [検証環境の構築](#検証環境の構築)
* [攻撃手順](#攻撃手順)
* [攻撃手法](#攻撃手法)
* [攻撃の観測](#攻撃の観測)
* [影響範囲](#影響範囲)
* [対策](#対策)
* [おわりに](#おわりに)

## はじめに

<!--
Introduction
-->

### CVE-2021-4034(Pwnkit)の概要

* Polkitの脆弱性
* 脆弱性の悪用により、任意の非特権ユーザがroot権限に権限昇格可能
* 脆弱性のあるホスト上で実行
  * ローカルエクスプロイト
* Linuxに12年前から存在する脆弱性

### Polkit pkexec[^Polkit-ArchWiki]

* Polkit(旧名PolicyKit)は、UNIXライクなオペレーティングシステムでシステム全体の権限を制御するためのコンポーネント
* 非特権プロセスが特権プロセスと通信できるようにするポリシを定義および操作するためのアプリケーションレベルのツールキット
* 特権操作へのアクセス許可を非特権アプリケーションに与えるかの判断を集中的に行うフレームワーク
* sudo などのシステムと対照的に、Polkit は全てのプロセスに root 権限を与えるようなことはせず、より細かいレベルで中心システムのポリシーを制御可能
* Polkitの`pkexec`コマンドを利用して、任意のコマンドを昇格された権限で実行可能

[^Polkit-ArchWiki]: https://wiki.archlinux.jp/index.php/Polkit

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

* GitHubからCVE-2021-4034のエクスプロイトコード[^berdav/CVE-2021-4034]をダウンロード

### 攻撃コードの用意

* ダウンロードしたソースコードをコンパイル
  * 実行ファイル
  * 共有ライブラリ
    * root権限でシェルを実行
* 併せて必要な設定ファイルを作成
  * `gconv-modules`
    * 偽のgconvモジュール
    * 上記の共有ライブラリをロード

<!--
GCONV_PATH=という名前のディレクトリを作成します。
その中にpwnkitという名前の実行ファイルを作成します。
pwnkitというディレクトリを作成します。
その中に偽のgconvモジュールを作成します。このモジュールは、シェルをロードする悪意ある共有ライブラリ（pwnkit.so）を指しています。
-->

### 攻撃コード実行

* シェルからエクスプロイトを実行

```shell
$ ./cve-2021-4034
```

### ルート権限奪取

* ルート権限でシェルが実行
* `id`コマンドによりルート権限を取得できていることを確認

```shell
# id
```

[^berdav/CVE-2021-4034]: https://github.com/berdav/CVE-2021-4034

## 攻撃手法

## 攻撃の観測

## 影響範囲

* 主要なLinuxディストリビューションのほとんど

## 対策

### SUIDビットの無効化

* 緩和策
* `chmod`コマンドを使用

```shell
$ sudo chmod 0755 /usr/bin/pkexec
```

### パッチ適用

* Polkitの更新

## おわりに

<!--
Discussion
Related works
Future works
Conclusion
-->

## References

* https://www.cybereason.co.jp/blog/threat-analysis-report/8529/
* https://gigazine.net/news/20220127-linux-polkit-bug-gives-attackers-root/
