# fasttext memo

facebookが作ったfasttextを動かした時のmemo

**fasttextとは？**

subwordを考慮したword2vecの強化版的なもの．
主にベクトル表現の構築・分類・推薦ができる．

    Faster, better text classification!

らしい．

## 学習の流れ（単語の分散表現の獲得）

wikipedia dataで動かす場合．．．

1. wikipediaデータを [WikiExtractor][wiki-ext]を用いてとってくる．
2. 取ったデータを一つのファイルにまとめる．
3. 日本語データであれば分かち書きする（mecab等の形態素解析器の利用）

```
    mecab -b 81920 input.txt -O wakati -o output.txt
```

4. データをfasttextに入れて学習



<br>

## 文書分類（文書のポジネガ判定）

事前に文書にラベルをつける必要がある．
具体的には，以下のようにラベルを付ける．

```
    __label1__, 食べる 時 に 手 が 汚れる
    __label2__, 近く に レストラン や コンビニ が たくさん あり 便利 です 。
```
（感情分析ニ値分類のケース）

作成したテキストデータを学習する．
[fastText python interface][fasttextpython] を使って学習する．
（fastTextの実行ファイルでも学習可能であるが，学習モデルをpythonでimportした時に
[謎のメモリエラー][error]が起こるので，モデルをpythonで使用する場合は学習もpython越しに行った方がいい）
学習スクリプトは[これ][twitterforpython]．


<br>

## 参考

[fastTextJapaneseTutorial][tutorial]


[wiki-ext]: https://github.com/attardi/wikiextractor "wiki-ext"
[tutorial]: https://github.com/icoxfog417/fastTextJapaneseTutorial "tutorial"
[fasttextpython]: https://github.com/salestock/fastText.py "fasttext"
[twitterforpython]: https://github.com/KChikai/TwitterforPython "twitterforpython"
[error]: https://github.com/salestock/fastText.py/issues/125 "error"
