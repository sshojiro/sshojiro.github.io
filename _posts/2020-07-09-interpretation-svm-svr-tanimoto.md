---
published: true
title: タニモトカーネルを使う場合の解釈方法
---
## 本が出ます

近日書籍が販売されます．

<iframe style="width:120px;height:240px;" marginwidth="0" marginheight="0" scrolling="no" frameborder="0" src="https://rcm-fe.amazon-adsystem.com/e/cm?ref=qf_sp_asin_til&t=emyornil-22&m=amazon&o=9&p=8&l=as1&IS1=1&detail=1&asins=4764906155&linkId=9000f3156e2643eea525ec48832f4bd6&bc1=ffffff&lt1=_blank&fc1=333333&lc1=0066c0&bg1=ffffff&f=ifr">
</iframe>

ALT: [実践 マテリアルズインフォマティクス](https://amzn.to/3dSszJL)

この書籍の中で，タニモトカーネルとSVMを使った分析を取り上げました．[Morgan fingerprint](https://pubs.acs.org/doi/10.1021/c160017a018)を折りたたんだものや[ECFP](https://pubs.acs.org/doi/10.1021/ci100050t)がケモインフォマティクスで使われる事が多いです．回帰/分類モデルを作る際にこれと組み合わせるのは，タニモトカーネルとなります．自分では初めて用いて、うまくいかないと思っていたのですがRBFカーネルを使う場合よりも，分類タスクで高い精度を示しました．
カーネル法というとガウス過程か，サポートベクターマシン(SVM)が浮かぶと思います．分子のフィンガープリントを直接入力できる点が非常に魅了的です．一方で，やはりケモインフォマティクスではモデル解釈が必須となります．


## RBFカーネルの場合

例えばRBFカーネルを使うと
[ノートブック](https://nbviewer.jupyter.org/gist/sshojiro/8f6051e6629f709e4aeb247f0b8b5dd4)に書いたように実装できます．
RBFカーネルにて入力が連続変数であるとき，SVMの関数を変数毎に偏微分すれば，入力の出力への寄与を計算することができます．

## タニモトカーネルの場合

Bonn大学のBajorath先生のチームから，以下の3報の論文が出ています．タニモトカーネルのSVMを解釈する原案は1., 2.番目の論文で，3.番目の論文ではSHAP値を使った解釈の様子を詳細に調査しています．端的に言うと，タニモトカーネルの形を注視すれば，サポートベクター毎に分母が定数として定まる線形カーネルのようにかけるので，1サンプルあたりの各bitの目的変数への寄与が定数として計算できるというものでした．実装が公開されているわけではないですが，それぞれの論文でかなり詳細にかつ分かりやすく説明されており，（これが手法研究ですな...）と感じて面白かったのでまとめました．

1. [Visualization and Interpretation of Support Vector Machine Activity Predictions (2015)](https://pubs.acs.org/doi/10.1021/acs.jcim.5b00175)
1. [Support Vector Machine Classification and Regression Prioritize Different Structural Features for Binary Compound Activity and Potency Value Prediction (2017)](https://pubs.acs.org/doi/10.1021/acsomega.7b01079)
1. [Interpretation of Compound Activity Predictions from Complex Machine Learning Models Using Local Approximations and Shapley Values (2019)](https://pubs.acs.org/doi/10.1021/acs.jmedchem.9b01101)

## まとめと感想

タニモトカーネルを線形カーネルと見立てて解釈するというのは見事でした．どう解釈しようかな，fingerprintは整数値を取るからSHAP値を利用しようかなと思ったらSHAPを用いた検証も既に行われていて完敗でした．

一方で，ガウス過程でタニモトカーネルを利用する場合に，カーネル関数の融合をすると，解釈が困難となることが予想されます．線形カーネルとタニモトカーネルとホワイトカーネルの和をカーネル関数とすれば解析的に各bitの寄与を計算できるかもしれません．RBFカーネルなどを挟むと数値微分するわけにもいかないので，[GPR-SA](https://ieeexplore.ieee.org/document/7805174)を利用するわけにもいきません．サンプル数が少ないときの（ベイズ）推定はどうすればよいのでしょうか…ベイズ推定時にわざわざモデル解釈する奴などいないと言われるとそんな気もしますが，問題は残されたままですね…