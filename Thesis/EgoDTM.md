## EgoDTM
<div style="text-align: right;">
更新日: 2025/06/01
</div>

---

### 【論文情報】
##### EgoDTM: Towards 3D-Aware Egocentric Video-Language Pretraining
 **Author:** Boshen Xu Ziheng Wang Yang Du Zhinan Song Sipeng Zheng Qin Jin Renmin University of China Beijing Academy of Artificial Intelligence
###### URL: [https://arxiv.org/abs/2503.15470](https://arxiv.org/abs/2503.15470)
 **Keywords:**  egocentric, hand-object interaction, 3D-awareness, video-language model, contrastive learning, multimodal representation learning

 Published as a conference paper at CVPR 2025

<div style="text-align: center; margin-top: 10px; margin-bottom: 20px;">
  <a href="https://github.com/xuboshen/EgoDTM" style="background-color:rgb(0, 121, 34); color: white; padding: 10px 20px; text-decoration: none; border-radius: 5px; font-weight: bold;">
    GitHubリポジトリはこちら 💻
  </a>
</div>

---

## 論文の要約
### ✅ 要約（Summary）
本論文は、**一人称視点（egocentric）** の動画に対して、**深度情報（3D-awareness）を取り入れた動画と言語の事前学習モデル「EgoDTM** を提案する．従来の手法ではテキストや2D画像に依存しており、手と物体の相互作用（HOI）や空間理解が不十分だった．

EgoDTMは、事前学習の段階で、既存のDepth Estimationモデルを活用して疑似Depth Mapを生成し、Transformerベースの軽量な3D-awareデコーダを通して深度を学習する．さらに、手と物体の位置関係を考慮した空間的に拡張されたキャプションをLLMで生成し、テキスト監督にも空間情報を加える．

実験では、EgoDTMが複数のベンチマークにおいて、動画検索・アクション認識・深度推定・ロボット操作・自然言語による動画検索などでSOTA性能を達成．Depthの導入により、特に3D空間理解とHOI推論の性能が顕著に向上することを示した．

### 🔍 目的と課題
- 目的: 人間のように3D空間を理解できる、一人称視点の動画と言語の学習モデルを構築。

- 課題：

  - 既存のモデル（例：EgoVLP, LaViLa）は2D画像やテキストから学習するが、3D的な空間理解が不十分。
  - HOI理解において「深さ（Depth）」や「手の位置関係」といった空間情報の欠如が精度を制限していると推測。

- 本研究の差異：テキストや2Dバウンディングボックスだけでなく、 **疑似Depth Map** を使い、3D空間を明示的に学習。

### ✍ 先行研究
#### テキストベース学習：
EgoVLP、LaViLaなどが代表。大規模な動画・テキスト対を使用しコントラスト学習を実施。
  - 課題：物体位置の精密な理解や3D構造把握が困難。

#### 領域（Region）ベース学習：
HelpingHands、HENASYなどは手や物体の領域情報を利用。
  - 課題：2Dベースのため、奥行きや空間的な関係把握が不十分。

##### 本研究はこれらの限界を超えて、Depth情報とテキストの融合による3D-aware学習を目指す。

### 🧪 提案手法：EgoDTM（Egocentric Depth- and Text-aware Model）
#### 簡単な説明：
「Depth Map」で奥行きを、「LLMによる拡張テキスト」で空間情報を学び、動画の理解精度を向上。

#### 技術要点：
1. Depth Map生成：DepthAnythingなどのモデルから動画にDepthを付加。
2. 軽量Depthデコーダ：TransformerベースでDepthを推定。高解像度不要でメモリ効率◎。
3. テキスト強化：HOI検出 → 追跡 → LLM生成で、テキストに「手の動き」「位置関係」を自動注入。

<img src="https://github.com/xuboshen/EgoDTM/blob/main/assets/paper/method.png?raw=true" alt="Structure Image of EgoDTM">

#### 学習方法：
Depth予測損失（Ldepth）＋ テキスト一致損失（Laugvtc）による同時学習。

### 💻 実験内容
#### ベンチマーク：
Ego4D、Epic-Kitchens-100、EGTEA、H2O、Franka Kitchenなど計7つ。

#### 学習データ：
- 4M動画×テキストペア
- そのうちHOIありの200万件にDepthと拡張テキストを付加

#### 評価指標：
- 動画検索：mAP, nDCG
- アクション認識：Top-1/mean accuracy
- Depth推定：δ1, RMSEなど
- ロボット操作：成功率（%）


### 📈 実験結果（主な貢献）
#### 動画理解（ZS-Video Retrieval）：
EgoVLP/LaViLaなど従来手法より **1〜3%改善**
（例：EK-100-MIRにてmAP +0.9%）

#### Depth推定：
RMSEで9.8%改善、CLIP等に比べてDepth予測が大幅に向上。

#### ロボット操作：
LaViLaより6.6%改善、CLIPより20%以上の成功率改善
→ **3D理解の高さが影響。**

#### 長時間動画理解（NLQ）：
EgoMCQにて精度向上（1〜2%） 
→ **奥行き情報** により空間理解が進んだ結果。

### 🧩 結論
EgoDTMは、「Depth＋空間テキスト」から3D空間を意識した学習を行う手法であり、HOIの精度向上にも貢献。

特に、Depthを導入したことで動画内の物体位置・相互関係の理解が向上し、多様な下流タスクに対して汎用的な性能向上が確認された。

---

## 論文の功績
- 3D-AwareなEgocentricモデルを初めて実現

- Depthデータと空間テキストの融合を大規模に達成

- 多くの下流タスク（動画検索・ロボ操作など）でSOTAを更新

- 汎用的な3D理解が可能なビジュアル基盤モデルの一歩となる

## 現状の課題・問題点
#### 残る課題：
- 深度推定は擬似（pseudo）Depthに依存 
→ 絶対的な精度保証がない

- HOI検出に __SAM2__ を使うが、手の細かい動きに弱く、過学習気味

- 利用分野が **Egocentric（主観視点）** に限定 
→ 一般動画への汎化力に課題

#### 解決に向けたアプローチ：
- HOI検出をファインチューニング済みTransformerで高精度化

- 第三者視点データとの併用で一般動画シナリオにも汎化