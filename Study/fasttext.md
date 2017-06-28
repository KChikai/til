# fasttext memo

facebookが作ったfasttextを動かした時のmemo

**fasttextとは？**

subwordを考慮したword2vecの強化版的なもの．
主にベクトル表現の構築・分類・推薦ができる．

    Faster, better text classification!

らしい．

## 学習の流れ

wikipedia dataで動かす場合．．．

1. wikipediaデータを [WikiExtractor][wiki-ext]を用いてとってくる．
2. 取ったデータを一つのファイルにまとめる．
3. 日本語データであれば分かち書きする（mecab等の形態素解析器の利用）

```
    mecab -b 81920 input.txt -O wakati -o output.txt
```

4. データをfasttextに入れて学習


## 参考

[fastTextJapaneseTutorial][tutorial]


[wiki-ext]: https://github.com/attardi/wikiextractor "wiki-ext"
[tutorial]: https://github.com/icoxfog417/fastTextJapaneseTutorial "tutorial"
