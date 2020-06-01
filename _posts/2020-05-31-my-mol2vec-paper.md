---
published: true
categories:
  - cheminformatics
title: 研究紹介 - Mol2Vecの大規模データへの適用
---
## 研究紹介 - mol2vec

本日は日本語で研究成果の紹介を書いてみます。

以下の論文を直近で報告しました:

- [Application of the mol2vec Technology to Large‐size Data Visualization and Analysis](https://onlinelibrary.wiley.com/doi/10.1002/minf.201900170)

### 論文の概要

mol2vecという技術を使ってフラグメント記述子（部分構造の出現回数）を取り出し、
機械学習を用いた予測に用いるというものです。
先行研究には以下のものがあります（発表された順）。

1. [Mol2vec: Unsupervised Machine Learning Approach with Chemical Intuition](https://pubs.acs.org/doi/abs/10.1021/acs.jcim.7b00616?src=recsys)
1. [Distributed Representation of Chemical Fragments]( https://doi.org/10.1021/acsomega.7b02045)
1. [Evaluating Polymer Representations via Quantifying Structure–Property Relationships](https://pubs.acs.org/doi/10.1021/acs.jcim.9b00358)

重要なのは、mol2vecでは部分構造の周辺に位置する部分構造を取り出し3層のニューラルネットワークを
構築する点です。隠れ層がmol2vecの計算結果で、入力層と出力層では部分構造に対応するone-hotベクトル
を与えます。既往のmol2vec論文と私のmol2vec論文での違いは以下の点です。

1. Word2vecでなくfastTextというsubwordを理解する方法で学習させた
1. 部分構造取り出しにはMorgan fingerprintだけではなくてISIDA Fragmentorというソフトを使った。ISIDA FragmentorではAtom coloringとfragment shapeを指定できて、pharmacophoreやforce fieldを考慮した部分構造が取り出せます。
1. Morgan fingerprintとISIDA Fragmentorではいずれも部分構造が文字列で取り出され学習されます

予測モデルにはgenerative topographic mappingと呼ばれる確率モデルを利用しています。
医薬品の化合物データChEMBL 23のデータを使い検証しました。ChEMBLでは。分類タスクに対して次元削減したこととなり、mol2vecを用いると予測精度が高くなることを確認しました。

### 長所と短所

mol2vecを使う利点は以下の通りです。

1. mol2vec学習用のデータが多いほど全てのフラグメントを網羅できる
1. ハッシュ化（折りたたみ処理）せずに固定長のベクトルを取り出すことができる
1. 予測モデル構築のデータは必ずしも多くなくて良い

一方で、現在認識している今後の課題としては以下の点が挙げられます。

1. Morgan fingerprintを利用するとき部分構造の正しい並び順を学習していない [github](https://github.com/samoturk/mol2vec)。RDKitというライブラリの部分構造取り出しアルゴリズムに従っている。大規模データによって軽減されているのかもしれないが、基本的には部分構造の並び順を一部無視している。
1. 回帰分析には必ずしも利用できない。分類であれば次元削減で似た分子に似たベクトルを割り当てられるが、回帰分析の場合も同様に扱えるかというと、検証が必要である。

### 最後に

もし参考になれば、引用していただけると幸いです。

> Shojiro Shibayama, Gilles Marcou,  Dragos Horvath,  Igor I. Baskin,  Kimito Funatsu, Alexandre Varnek, Application of the mol2vec Technology to Large‐size Data Visualization and Analysis, Molecular Informatics, 2020, 39, 1900170
