### 作業映像の特徴抽出器を用いた作業分節法
<div style="text-align: right;">
更新日: 2025/06/01
</div>

---

### 【論文情報】
##### 作業映像の特徴抽出器を用いた作業分節法
 **Author:** 神谷 聡, 藤田 渉, 八田 俊之, 渡邉 信太郎, 近藤 空哉, 齋藤 一誠, 長野 匡隼, 中村 友昭
 三菱電機株式会社　先端技術総合研究所
 電気通信大学

###### URL: [https:pub.confit.atlas.jp/ja/event/ssii2025/presentation/IS1-21](https://pub.confit.atlas.jp/ja/event/ssii2025/presentation/IS1-21)
 **Keywords:**  egocentric video, third-person video, action segmentation, feature extraction, video transformer, GP-HSMM, unsupervised learning

 Published as a conference paper at the 31st Image Sensing Symposium (第31回画像センシングシンポジウム), 
 paper ID: IS1-21.



<div style="text-align: center; margin-top: 10px; margin-bottom: 20px;">
  <a style="background-color:rgb(99, 107, 101); color: white; padding: 10px 20px; text-decoration: none; border-radius: 5px; font-weight: bold;">
    GitHubリポジトリはありません
  </a>
</div>

---

## 論文の要約
### ✅ 要約（Summary）
本研究は，製造現場などで撮影された作業映像を対象に，人の動きと周囲の物体との関係を考慮した作業分節法を提案する．従来手法は骨格情報に依存し，視点が固定された三人称映像にしか対応できず，一人称視点映像や物体の違いを反映した分節が困難だった．

提案手法では，VideoMAEなどの動画処理モデルを用いて映像から時系列特徴を抽出し，それを主成分分析で圧縮した後，**GP-HSMM（ガウス過程×隠れセミマルコフモデル）** により作業をクラス分類・分節化する．

実験では，三人称・一人称両方の模擬作業映像を用いて検証を行い，VideoMAEを用いた提案手法が最も高精度に分節できることを示した．特に，一人称視点においても視点移動に強く，作業分析に有用な特徴を抽出できる点が確認された．

### 🔍 目的と課題
製造現場では，作業のムダを省き品質や生産性を向上させるため，作業映像を用いた改善活動が行われている．しかし，映像を人が目視で分析するのは時間と手間が大きく，自動化が求められている．
従来は **「骨格検知」** による分析が多かったが，これは視点が固定されていることが前提であり，一人称視点（egocentric）映像には非対応．また，周囲の物体との関係（HOI）を考慮できず，動作の区別が困難だった．

### ✍ 先行研究
#### 骨格情報×GP-HSMM（教師なし）：
人の動きをGaussian Process-HSMMで分節．
- 課題：骨格だけでは物体の違いが認識できず，同じ動きでも作業が区別できない．
- 視点固定が前提
→ 一人称視点には不向き．

#### 動画処理モデルの進化：
 **TimeSformer:** 時空間を同時に処理
 → 高計算コスト．
 **ViViT:** 空間と時間を分離して計算し，効率向上．
 **VideoMAE:** Masked AutoEncoderで空間＋時系列の特徴を高精度に学習．
 **X-CLIP:** 動画と言語の関係性学習
 → 一般物体の認識に強い．

### 🧪 提案手法
#### 手法名：作業映像の特徴抽出器を用いた分節法

#### 理論
1. 動画処理モデル（例：VideoMAE）を用いて特徴抽出
2. 複数のフレームから時系列付きの特徴ベクトルを抽出
3. 主成分分析（PCA）で次元を圧縮
4. **GP-HSMM**による分節化
5. ガウス過程で動作の傾向を捉え，HSMMで持続時間や遷移をモデル化
6. 映像を作業クラスに分類

#### 特徴

- 人物の動きだけでなく物体との関係も反映した特徴を抽出
- 一人称視点にも対応可能で，視点変動に頑健

### 💻 実験内容
#### 対象映像: 
- 三人称視点（工場部品の組立）3本：作業クラス7
- 一人称視点（文具を使った作業）4本：作業クラス10

#### 使用モデル: 
- TimeSformer，ViViT，VideoMAE，X-CLIP

#### 評価指標:
Adjusted Rand Index (ARI)

#### パラメータ: 
- 特徴次元：6次元にPCAで圧縮
- 特徴抽出は$t$フレーム単位


### 📈 実験結果（主な貢献）
#### 結果（ARIスコア）：
|モデル名|三人称視点|一人称視点|
|---|---|---|
|TimeSformer|0.590|0.482|
|VideoMAE|0.642|0.598|
|ViViT|0.225|0.127|
|X-CLIP|0.157|0.442|

#### 考察：

- VideoMAEが最高精度．再構成タスクにより，動作の変化に強い特徴を抽出できる．
- 一人称視点でも腕や物体に着目しており，視点の変化に頑健．
- X-CLIPは一般物体（紙・ペンなど）への理解は強いが，工場部品のような専門的物体には弱い傾向．

### 🧩 結論
提案手法は，映像から抽出した特徴を用い，**GP-HSMM**で作業を分節することにより，一人称視点・物体との関係性を含めた作業分析を実現した．
実験により、**VideoMAE**が最も優れた精度を示し，変化に富んだ視点にも対応可能であることが確認された．

---

## 論文の功績
- 一人称視点を含む作業映像の自動分節化を実現

- 動画処理モデルにより人物＋物体の関係性も考慮

- VideoMAEの有効性を定量・定性的に検証

- GP-HSMMとの組合せで教師なし学習でも高精度に分節可能

## 現状の課題・問題点
#### 現状の課題
- 工場以外の環境での検証が未実施

- リアルタイム処理には未対応

- GP-HSMMは高次元特徴の扱いが苦手 
→ PCAに依存

#### 今後のアプローチ
- 実環境映像や多様な現場データでの汎用性評価

- Transformerによる時系列分節をEnd-to-Endで学習するモデルの導入

- 高速処理向けに軽量モデルと特徴量選択の最適化を併用