# VALL-E-X導入 (2024/06/28)

## 概要

|ライセンス|GitHubリポジトリ (OSS)|論文 (Microsoft)|
|:-:|:-:|:-:|
|MIT (商用利用可能)|[https://github.com/Plachtaa/VALL-E-X](https://github.com/Plachtaa/VALL-E-X)|[https://arxiv.org/abs/2303.03926](https://arxiv.org/abs/2303.03926)|

* 社内研修動画などのナレーションに利用することを目的として、音声合成モデル「VALL-E-X」を導入を検討する。
    * はじめにPythonが動作する環境にCUIの生成AI環境を導入し、次にWebUIを使用したGUIツールを導入する。
    * 「VALL-E-X」自体の概要説明は下記参照。

~~~
VALL-E-XはMicrosoftが開発した音声合成モデルのOSS実装です。
Microsoftのものは論文は公開されていますが、ソースコードと学習済みモデルはMicrosoftから公開されていないため、非公式の実装となっています。
単一言語の音声合成モデルのVALL-Eを、多言語対応した音声合成モデルがVALL-E-Xとなります。
~~~

---

## Python動作環境導入

|OS|MEMORY|CPU|GPU|STRAGE|
|:-:|:-:|:-:|:-:|:-:|
|Windows11 Pro|DDR3 16GB|i7 4770|GeForce RTX2060 6GB|Intel SSD128GB + SSD256GB|

* このドキュメントの内容は、上記ハードウェア構成のパソコンで動作確認しています。
    * 生成AIで必須のPyTorchモジュールを動作させる構成としては、ギリギリアウトな感じです。<br>
        * 「GeForce RTX 3060 8GB」以上のGPU推奨。
        * 「Intel第8世代Core」以降のCPU推奨。 (上記CPUはWindows11非サポート)
* Python動作環境導入の詳細は「Python仮想環境導入.pdf」をご参照ください。

---

## CUIの生成AI環境導入

### ① 管理者権限でコマンドプロンプトを開き、下記のコマンドを実行する。

~~~powershell
cd ~/
rmdir /s /q VALL-E-X
git clone --recursive https://github.com/Plachtaa/VALL-E-X
cd VALL-E-X
python -m pip install -r requirements.txt
mkdir checkpoints
~~~

* Gitクライアントはあらかじめインストールしておいてください。

### ② 音声合成用の機械学習データをダウンロードして配置する。

1. [https://drive.google.com/uc?id=10gdQWvP-K_e1undkvv0p2b7SU6I4Egy](https://drive.google.com/uc?id=10gdQWvP-K_e1undkvv0p2b7SU6I4Egy)
2. 上記URLにアクセスして「vallex-checkpoint.pt」をダウンロードする。
3. ダウンロードしたファイルを「checkpoints」フォルダ直下に配置する。

### ③ テストコードを実行して動作確認する。

1. 「VALL-E-X」フォルダ直下に「tts.py」を作成し、下記のコードを記述する。

~~~python
from utils.generation import SAMPLE_RATE, generate_audio, preload_models
from scipy.io.wavfile import write as write_wav
preload_models()
text_prompt = """
最先端技術とデジタル人材で、お客様に感動を与えられるサービスを生み出すと同時に、
社会との信頼を大事にするという意志が込めて、名付けました。
毎日「すごい」で満たせる感動を、お客様と一緒に進めて参ります。
"""
audio_array = generate_audio(text_prompt)
write_wav("chapter1-1.wav", SAMPLE_RATE, audio_array)
~~~

2. 下記のコマンドを実行する。

~~~python
py tts.py
~~~

* テストコードの実行に成功すると、「VALL-E-X」フォルダ直下に「chapter1-1.wav」が出力されます。
* 「VALL-E-Xを自動でインストール＆実行してくれるスクリプト」もあるようですが未確認です。
    * [https://note.com/0me84/n/nb32b81d195ff](https://note.com/0me84/n/nb32b81d195ff)

---

## WebUIを使用したGUIツール導入

* 準備中・・・

---

## 参考サイト

* [https://www.kkaneko.jp/ai/win/vall_e_x.html](https://www.kkaneko.jp/ai/win/vall_e_x.html)
* [https://github.com/kuwacom/VALL-E-X-JP](https://github.com/kuwacom/VALL-E-X-JP)
* [https://torish.hatenablog.com/entry/2023/09/02/142004](https://torish.hatenablog.com/entry/2023/09/02/142004)
* [https://note.com/0me84/n/nb32b81d195ff](https://note.com/0me84/n/nb32b81d195ff)
* [https://medium.com/axinc/vall-e-x-977efc19ac84](https://medium.com/axinc/vall-e-x-977efc19ac84)
* [https://qiita.com/fuyu_quant/items/0bf07e43e03c2251a53f](https://qiita.com/fuyu_quant/items/0bf07e43e03c2251a53f)

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