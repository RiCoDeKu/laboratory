## EgoNCE++
<div style="text-align: right;">
更新日: 2025/06/01
</div>

---

### 【論文情報】
##### DO EGOCENTRIC VIDEO-LANGUAGE MODELS TRULYUNDERSTAND HAND-OBJECT INTERACTIONS?
 **Author:** Boshen Xu Ziheng Wang Yang Du Zhinan Song Sipeng Zheng Qin Jin Renmin University of China Beijing Academy of Artificial Intelligence
###### URL: [https://openreview.net/forum?id=M8gXSFGkn2](https://openreview.net/forum?id=M8gXSFGkn2)
 **Keywords:**  egocentric, hand-object interaction, video-language model, contrastive learning, multimodal representation learning

 Published as a conference paper at ICLR 2025

<div style="text-align: center; margin-top: 10px; margin-bottom: 20px;">
  <a href="https://github.com/xuboshen/EgoNCEpp" style="background-color:rgb(0, 121, 34); color: white; padding: 10px 20px; text-decoration: none; border-radius: 5px; font-weight: bold;">
    GitHubリポジトリはこちら 💻
  </a>
</div>

---

## 論文の要約
### ✅ 要約（Summary）
本研究は、 **エゴセントリック映像と言語モデル（EgoVLM** が、 **手と物体のインタラクション（HOI）** を本当に理解しているかを検証するものです。著者らは、以下の重要な知見と提案を示しています。

### 🔍 背景と課題
EgoVLMは、VR/ARや身体化エージェントなどの応用が期待される領域で有望であり、Ego4Dなどの大規模データセットによって学習されてきた。

しかし、既存のモデルは **「フライパンを振る」vs「フライパンを掛ける」のような動詞や名詞の微細な違いを正確に区別できない**。

この限界は、動詞の理解が困難であり、また、細粒度の否定的監督（hard negatives）が不足していることに起因すると考えられる。

### 🧪 提案手法：EgoNCE++
新たな非対称型コントラスト学習目的関数 EgoNCE++ を提案。

>映像 → テキスト損失（V2T）

LLMまたは語彙ベースで生成された動詞・名詞の一語違いの否定文を用い、HOI理解を強化。

>テキスト → 映像損失（T2V）

名詞が同一の映像表現をクラスタリングすることで、オブジェクト中心の特徴空間を維持。

### 🧪 EgoHOIBench：新ベンチマーク
EgoVLMのHOI理解を精緻に評価するために、多肢選択形式の新ベンチマーク EgoHOIBench を構築。

動詞・名詞の一語違いに対して正しくキャプションを選べるかをテスト。

SOTAモデル（EgoVLP, EgoVLPv2, LaViLa）もこのベンチマークで苦戦。

### 📈 実験結果（主な貢献）
EgoNCE++によって：

HOI-動詞タスクで最大 +34%の精度向上。

ゼロショットでも、マルチインスタンス検索・アクション認識・時間的理解タスクの性能が一貫して向上。

EgoNCE++は、LaViLaやEgoVLPなど既存のEgoVLMに簡単に適用可能で、追加パラメータも少ない。

### 🧩 結論
EgoVLMは現状、HOIの微細な意味理解に限界がある。

EgoNCE++は、動詞と名詞の違いをより深く理解させるための訓練戦略として効果的であり、EgoHOIタスク全般において性能を強化する有望なアプローチである。

---

## 論文の功績
-  **EgoVLMのHOI理解における限界を指摘:** 
既存の一人称視点ビデオ言語モデル（EgoVLM）が、簡単な単語（動詞や名詞）の置き換えによって容易に誤認識する問題を提起し、HOI（手と物のインタラクション）の真の理解度に対する疑問を投げかけた点。
-  **新しい評価ベンチマーク「EgoHOIBench」の開発:**  
EgoVLMがHOIのバリエーションをどの程度理解しているかを評価するために特化した、新しい多肢選択式のテストベッド **「EgoHOIBench」** を提案・開発した点。このベンチマークは、動詞や名詞の変化に対するモデルの感度を測るように設計されている。
-  **EgoVLMの課題の原因分析:**
EgoVLMがEgoHOIBenchで苦戦する原因として、きめ細かいネガティブサンプルの不足と、モデルが動詞よりも名詞を認識しやすい「オブジェクト中心の特徴空間」を形成する傾向があることを特定した点。
-  **新しい学習目的関数「EgoNCE++」の提案:** 
上記の課題を解決するために、HOIを意識した非対称な対照学習目的関数「EgoNCE++」を提案した点。   
    - ビデオからテキストへの損失 (V2T) では、LLMや語彙ベースでハードネガティブキャプションを生成し、きめ細かいテキスト監視を強化
    - テキストからビデオへの損失 (T2V) では、類似の名詞を持つビデオ表現をクラスタリングすることで、オブジェクト中心の特徴空間を維持・強化
- **EgoNCE++の有効性の実証:**
EgoNCE++が、複数の既存EgoVLM（EgoVLP, EgoVLPv2, LaViLa）のHOI理解を大幅に向上させ、EgoHOIBenchだけでなく、7つの下流タスク（多事例検索、行動認識、時間的理解など）においても汎化性能を改善することを広範な実験で示した点。

## 現状の課題・問題点
- **HOI以外の多様な一人称視点活動への対応:** 
EgoNCE++は手と物のインタラクション (Hand-Object Interacton)に焦点を当てているが、一人称視点の活動は単純な環境観察やVR/AR活動（ダンス、スポーツなど）といったより広範なものを含むため、これらへの対応は今後の課題である。
- **テキスト監視のみによる物体認識能力向上の限界:** 
テキスト監視だけでは、EgoVLMの物体認識能力を向上させるのは難しいと認識している点。実世界の物体カテゴリは行動の種類よりも多様であり、限られたネガティブサンプルで効果的に捉えるのが困難であるため。
- **プライバシーへの懸念:** 
一人称視点ビデオは個人的で機密性の高い情報を含むため、プライバシーの問題があり、慎重な管理が必要である点。
- **危険な活動の誤認識リスク:** 
特にキッチン環境などでは、危険な活動（鋭利な物体を扱うタスクなど）の誤認識が有害な結果につながる可能性がある点。