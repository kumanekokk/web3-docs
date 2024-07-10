# Python仮想環境導入 (2024/06/26)

## 概要

* venv (ブイエンブ)を利用して、プロジェクト毎に必要なPythonモジュールをインストールした仮想環境を導入する。
    * 生成AIの普及によりPythonを利用するケースが増えてきたため、その場合の注意点もあわせて記載する。

---

## 利用するPythonバージョン

* 仮想環境内でPythonのバージョン切替はできないため、はじめに使用するPythonのバージョンを選定する。
    * 新規プロジェクト、またはPythonのバージョン指定がないアプリケーションの場合、ひとまず最新版のPythonで仮想環境を利用してみる。
        * Pythonが原因と思われるエラーが発生した場合、3.10系のバージョンで仮想環境を利用してみる。<br>
        (特にGPUを利用した生成AIのPyTorch系モジュールでエラーが発生する場合、このバージョンで仮想環境の利用を検討する。)
    * Pythonのバージョン指定があるアプリケーションの場合、基本的には指定されたバージョンで仮想環境を利用する。<br>
    (最新版のPythonを利用することによるメリットが大きい場合、正常に動作しない可能性をじゅうぶんに考慮した上で、最新版のPythonで仮想環境の導入を検討する。)

---

## WindowsのPython仮想環境導入

### ① Pythonをインストールする。 (以下は3.10系を想定)

* [https://www.python.org/downloads](https://www.python.org/downloads)
    * インストールするPythonのバージョンについては、前項「venvを利用するPythonのバージョン」を参照。
    * 「Python Launcher」が有効な状態でインストールする。<br>(Pythonのバージョン3.3以降はデフォルトで有効。)
    * 複数プロジェクト間でPythonモジュールが競合しない場合など、開発端末のシステム構成によっては仮想環境の導入が必須ではないため、手順②以降は仮想環境が必要な場合のみ実施する。

### ② プロジェクトを新規作成する。

~~~powershell
$ mkdir ~/[プロジェクト名]
$ cd ~/[プロジェクト名]
$ py -3.10 -m venv [仮想環境名]
~~~

### ③ 仮想環境を起動する。

~~~powershell
$\[仮想環境名]\Scripts\activate
~~~

### ④ 仮想環境でPythonを実行する。

~~~powershell
([仮想環境名])$ py -V 
Python 3.10.11
~~~

### ⑤ 仮想環境を終了する。

~~~powershell
([仮想環境名])$ deactivate
~~~

---

## 参考サイト

* [https://qiita.com/fiftystorm36/items/b2fd47cf32c7694adc2e](https://qiita.com/fiftystorm36/items/b2fd47cf32c7694adc2e)
* [https://gammasoft.jp/blog/find-out-python-launcher](https://gammasoft.jp/blog/find-out-python-launcher)

<br>

<style>
font-family: 'Note Sans JP','Hiragino Kaku Gothic Pro', 'ヒラギノ角ゴ Pro W3, Meiryo', メイリオ, Arial, sans-serif;
table {border-left:1px solid #333;}
th {background:#eee;color:#000 !important;border-top:1px solid #333;}
td {background:#fff;color:#333;border-bottom:1px solid #333;}
th,td {border-left:dotted 1px #333;}
th:first-of-type {border-left:1px solid #333;}
td:first-of-type {border-left:1px solid #333;}
th:last-of-type {border-right:1px solid #333;}
td:last-of-type {border-right:1px solid #333;}
hr {border-bottom:1px dashed #999;}
</style>
