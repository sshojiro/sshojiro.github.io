---
published: false
title: 研究紹介 - 連続生産へ向けた解析手法の検討
---
## 研究紹介 - 連続生産へ向けた解析手法の検討

以下の論文が昨年採択されて、年明けに公開となりました。

- [ Investigation of Preprocessing and Validation Methodologies for PAT: Case Study of the Granulation and Coating Steps for the Manufacturing of Ethenzamide Tablets.](https://link.springer.com/article/10.1208%2Fs12249-020-01911-w)

### 論文の概要

本論文で検討したのは、
1. NIRを用いた品質管理手法の検討
2. Adversarial Validationを使ったデータのトレーニングデータとテストデータの類似性検証
となります。

1点目については、NIRを入力に、PLSモデルを活用して
モデル構築する検討を行いました。データが少ないときにどのようにモデル検証するか、
前処理のハイパーパラメータをどのように決定するかを試しました。

2点目について、データ解析コンペのKaggle界隈で使用される手法として
adversarial validationというものがあります。トレーニングデータと
テストデータを最もうまく分割する特徴量を順に除外することで
トレーニングデータとテストデータの分布が重なり合うような特徴量のみを利用して
モデルの検証を進めることができます。
PAT利用時のモデル構築にadversarial validationを適用すると、
物理現象のデータは消しようがないので、物理現象として
どの変数の違いがモデル構築時とモデル使用時に異なっていたのか
（=トレーニングデータとテストデータのうちどの変数が最も
異なっていたのか）が明らかになります。

## 今後の展望

研究遂行時の議論の中で、NIRスペクトルのうち、高周波帯域はノイズが乗りやすく
うまく解析ができないという問題点が挙げられました。これは、Fourier Transformを利用している
限界と言えます。インターフェログラムを使った別のスペクトル計算手法を提案すべきと思いました。

### 最後に
もし参考になれば、引用していただけると幸いです。

Shibayama, S., Funatsu, K. Investigation of Preprocessing and Validation Methodologies for PAT: Case Study of the Granulation and Coating Steps for the Manufacturing of Ethenzamide Tablets. AAPS PharmSciTech 22, 41 (2021). https://doi.org/10.1208/s12249-020-01911-w