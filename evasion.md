# Evasion technique

## Malware Evasion Encyclopedia[^Malware_Evasion_Encyclopedia]

[^Malware_Evasion_Encyclopedia]: https://evasions.checkpoint.com/

### 概要

* マルウェアが仮想マシン（Virtual Machine、以降、VM）で実行されているかを検出するために、マルウェアが使用する手法を整理
  * カテゴリごとに情報を分類
* Check Point Researchによって作成
* VirtualBoxおよびVMWareなどの仮想化環境を対象

### VM上での検知および解析回避の目的

* セキュリティリサーチャーによる検出および解析回避のため
* VM上で実行されていることがマルウェアによって検知された場合、マルウェアは実行を終了
  * 場合によっては、解析防止のため、自身を削除

### 回避テクニックのカテゴリ

* 各カテゴリ内には、マルウェアがVM上で実行されているか判断する方法、およびこれらのチェックを無効にするための推奨される対策を示すコードスニペットが提示

<table>
  <tr>
    <td>Filesystem</td>
    <td>Registry</td>
    <td>Generic OS queries</td>
    <td>Global OS objects</td>
  </tr>
  <tr>
    <td>UI artifacts</td>
    <td>OS features</td>
    <td>Processes</td>
    <td>Network</td>
  </tr>
  <tr>
    <td>CPU</td>
    <td>Hardware</td>
    <td>Firmware tables</td>
    <td>Hooks</td>
  </tr>
  <tr>
    <td>Timing</td>
    <td>WMI</td>
    <td>Human-like behavior</td>
    <td>macOS</td>
  </tr>
</table>

### Check Pointの考え

* この情報共有により、マルウェア開発者はいくつかの新しい手法を学ぶことが可能
* だが、セキュリティコミュニティにおける価値は、マルウェア開発者におけるメリットよりもはるかに重要

### References

* https://www.bleepingcomputer.com/news/security/new-evasion-encyclopedia-shows-how-malware-detects-virtual-machines/
