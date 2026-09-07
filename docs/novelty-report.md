# **学位論文の新規性調査報告書：リスク感応型分布型強化学習における歪み重み付き分位点フラクション学習（引用修正版）**

> **本ファイルは引用検証（2026-09-08実施）に基づく修正版である。** 誤帰属・著者名混同の修正、未掲載だった原典の追加、重複引用の統合、非学術的URL（eBay、Scribd、chatpaper、学生レポート等）の学術的ソースへの差し替えを行った。修正内容の詳細は末尾「**8. 引用修正履歴**」および「**9. 追加調査結果**」を参照。全調査文献の一覧は別ファイル「**Risk-Sensitive FQF 調査文献リスト.md**」にまとめてある。本文中の引用番号 [n] は修正版の引用文献リストに対応する。

## **1. 結論**

本研究アイデアの新規性は「高」と判定される。FQF（Fully Parameterized Quantile Function）のフラクション提案ネットワークの目的関数を、一様重み付きWasserstein距離から「歪み重み付きWasserstein距離」へと拡張する着眼点は、理論的かつ実用的に極めて独創的である。IQNにおけるサンプリング分布を尾部に偏らせるヒューリスティックな手法や、静的・動的リスク尺度を扱う研究は多数存在するが、提案手法のように分位点フラクションの適応的学習を「歪み分布の1次元最適量子化（Optimal Quantization）」として理論的に定式化し、フラクション勾配の閉形式を導出して推定誤差の上界改善までを証明した研究は確認されない。数理ファイナンスにおけるリスク管理（デルタヘッジ等）の高度化という応用上の意義も深く、トップジャーナルや難関国際会議において高い学術的価値を有する。

## **2. Q1: 直接的な先行研究の有無（最重要）**

指定された4つの観点（(a) FQFとリスク尺度の結合、(b) ![][image1] サンプリング・サポート点配置のW1最適化、(c) 歪みW1と損失設計、(d) 統計・最適輸送における歪み尺度の最適量子化）について、英語・日本語・中国語の文献を対象に網羅的な文献検索を実施した結果、**本提案と完全に一致する直接的な先行研究は存在しない**ことが確認された。
分布型強化学習（Distributional RL）の分野では、リターン分布の形状を捉えるために分位点関数を学習するアプローチが主流となっている。しかし、その多くはリスク中立的な期待値最大化を前提とした近似誤差（一様重みの1-Wasserstein距離）の最小化に留まっている。リスク感応型RLにおいて歪みリスク尺度を導入する試みは存在するが、それらはいずれも「関数近似のノード（サポート点）をリスク尺度に合わせて適応的に再配置する」という踏み込んだネットワーク設計には至っていない。以下は、各要素において部分的に関連するものの、本提案とは明確な乖離がある先行研究の候補一覧である。

| 観点 | 該当文献の候補 (著者, 年, 掲載先) | 該当箇所の要約 | 本提案との一致度 |
| :---- | :---- | :---- | :---- |
| **(a)** | Wu et al. (2026), *DRL-ORA*, UAI Proceedings [21] | 分布型RLにおいて、認識論的リスクと暗黙の偶然的リスクの不確実性を統合し、オンラインでエピステミック・リスク水準を動的に調整する枠組み（DRL-ORA）を提案した研究 [21]。 | **部分一致**（不確実性とリスクの適応的調整を行うが、FQFのフラクション最適化には無関係） |
| **(a)** | Zhang, Pan, Chen, Courville & Bengio (2024), *Distributional GFlowNets with Quantile Flows*, TMLR [22] | 分位点マッチング（quantile matching）を用いて歪みリスク尺度（CPW・Wang・CVaR）下のポリシーをGenerative Flow Networksで学習する手法。非決定論的環境でのリスク感応型方策を導出 [22]。 | **部分一致**（分位点と歪みリスク尺度の結合だが、フラクション学習の機構は持たない） |
| **(b)** | Zhang, J. (2025), *Tail-Safe Hedging*, arXiv:2510.04555 [23]（※単著・査読なしプレプリント） | 金融制約下のヘッジングにおいて、CVaR推定を安定化させるため「Tail-Coverage Controller」を導入し、温度付きサンプリング（temperature tilting）や尾部ブースティングを用いて ![][image1] のサンプリングを尾部に集中させる手法 [23]。 | **部分一致**（![][image1] の分布を尾部に偏らせるが、Wasserstein距離に基づく最適量子化ではなく発見的制御） |
| **(c)** | 該当なし | \- | **不在** |
| **(d)** | Graf & Luschgy (2000), *Foundations of Quantization for Probability Distributions*, Springer LNM 1730 [27] | 確率分布の最適量子化に関する基礎理論。1次元および多次元確率分布の量子化誤差の漸近的性質（Zador型定理）や、最適量子化器の存在とVoronoi構造について詳述 [27]。 | **部分一致**（分布型RLの動的学習とは独立した、純粋な確率論の文脈での静的な量子化） |
| **(d)** | Bardou, Frikha & Pagès (2016), *CVaR Hedging Using Quantization-Based Stochastic Approximation Algorithm*, Mathematical Finance [26] | 量子化に基づく確率近似アルゴリズムを用いてCVaRの計算とヘッジングを行う数学的研究 [26]。 | **部分一致**（数理ファイナンスにおける静的な確率分布の量子化であり、強化学習アーキテクチャではない） |
| **(d)** | Faugeras & Pagès (2024), *Risk Quantization by Magnitude and Propensity*, Insurance: Mathematics and Economics [43] | リスク変数の「大きさ（magnitude）」と「生起確率（propensity）」への2点分布射影をWasserstein輸送で定義し、制約付き最適量子化問題としても定式化した研究 [43]。 | **部分一致**（リスク尺度×最適量子化×Wassersteinの交差は既存だが、歪み重み付きW1による分位点分数配置の学習は含まない） |

**【不在の証拠と検索の網羅性】** 上記の結論を導出するため、arXiv、OpenReview、NeurIPS/ICML/ICLR proceedings 等の主要な学術データベースに対して、2024年から2026年の最新プレプリントを中心に徹底した検索を行った。検索には "fully parameterized quantile function" risk-sensitive / CVaR / distortion や "fraction proposal network" CVaR OR "risk measure" などの高度に特化したクエリを使用した。結果として、FQF [4] のFraction Proposal Networkの損失関数を、歪み測度空間上のWasserstein距離に置換して学習するアーキテクチャを提案した文献は一つも発見されなかった。この「高度に体系化された不在」は、本研究アイデアが既存のパラダイムにおける盲点を突いた非常に価値の高いものであることを示唆している。

## **3. Q2〜Q4の文献表：近接する先行研究との詳細な比較と差分**

本節では、分布型強化学習、リスク感応型制御、最適輸送理論、および数理ファイナンス（デルタヘッジ等）の各領域における主要な先行研究を網羅し、提案手法との類似点、相違点、および本提案が明確に主張できる学術的差分を精緻に分析する。これらはQ2（近接する先行研究）、Q3（金融応用面の先行研究）、Q4（理論的先行研究）の要求に合致するよう体系化されている。

### **3.1. Q2: 分布型強化学習とリスク感応型制御の先行研究群**

分布型RLの進化は、リターン分布の表現方法の高度化の歴史である。Categorical DQN (C51) が離散的なサポート上の確率を学習したのに対し [1]、QR-DQNは固定された分位点フラクション上の値を学習し [2]、IQNはランダムな分位点フラクション ![][image2] 上での値を学習する暗黙的ネットワークを構築した [3]。FQFはこれらをさらに進め、フラクション自体を状態依存的に学習する [4]。一方で、テールリスクを制御するリスク感応型RLも同時に発展してきたが、これら二つの流れ（フラクションの最適化とリスク尺度の適用）を理論的に統合した研究は存在しなかった。

| 比較対象の研究カテゴリー | 類似点 | 相違点 | 本提案が差分として主張できる点 |
| :---- | :---- | :---- | :---- |
| **Tail-Safe (Zhang, J. 2025) の ![][image1] サンプリング偏重手法** [23] | リスク感応型分布型RL（IQNベース）を用い、CVaR等の左側尾部推定を安定化させるため、![][image1] のサンプリングを尾部に偏らせている点 [23]。 | Tail-SafeはIQNの枠組み内で「Tail-Coverage Controller」というヒューリスティックな温度スケーリング（temperature tilting）と尾部ブースティングを用いてサンプリング確率を操作するに過ぎない [23]。 | 提案手法は、![][image1] の配置を「歪み分布の最適量子化」として理論的に定式化し、勾配ベースで解析的に最適なフラクションを自動学習する点で、発見的なサンプリング操作よりも理論的に強固である。 |
| **EX-DRL (Malekzadeh et al. 2024) 等のパラメトリック補正手法** [24] | 分布の尾部（テールリスク）のモデリング解像度と精度を向上させ、極端なリターンに対するリスク評価を正確に行うことを目的としている点 [24]。 | EX-DRLは損失分布の尾部を一般化パレート分布（GPD）でパラメトリックに補正する（GPDは極値理論EVTの標準的な尾部モデル） [24]。本提案はステップ関数近似のサポート点配置自体を最適化する。 | 尾部に対して追加の分布仮定（パラメトリックな制約）を置くことなく、エンドツーエンドのフラクション学習のみで、ノンパラメトリックに尾部の解像度を動的に向上させることができる。 |
| **Dabney et al. (2018) IQN の risk-sensitive 実験** [3] | 歪み関数（CPWやWang、CVaR）を通じてリスク感応型の方策を学習し、期待値以外の目的関数を最大化するアプローチをとる点 [3]。 | IQNはサンプリングされる ![][image1] を固定の歪み関数で変換して推定を行うが、分位点関数の近似誤差自体を最小化するようなフラクションの適応的な再配置や学習は行わない [3]。 | 有限のパラメータ（限られた ![][image3] 個のフラクション）で近似を行う際、本提案のようにリスク尺度に最適化されたサポート点を明示的に学習する方が、誤差上界を ![][image4] 倍程度改善できるという理論的・実証的優位性がある。 |
| **静的/動的CVaRと時間非整合性を扱う研究 (Lim & Malik 2022 [15], Bäuerle & Ott 2011 [16], Bäuerle & Glauner 2022 [17])** | 分布型RLやMDPを用いてCVaRなどのリスク尺度を最適化する際の方策勾配や状態価値の挙動、特にリスク尺度の静的・動的評価を扱っている点 [15, 16, 17]。 | これらの研究は「マルコフ決定過程（MDP）において、時間非整合性を持つ静的/動的リスク尺度をいかにして整合的に最適化するか（状態拡張など）」という制御理論的性質に焦点を当てている [15, 16]。 | 本提案はMDPの時間整合性の議論ではなく、関数近似（Value Function Approximation）の観点から、任意の特定状態におけるリスク尺度の評価精度を最大化するためのアーキテクチャの改善を提供するものである。 |
| **NC-QR-DQN [5] および NDQFN [6]（分位点交差のバイアスを扱う研究）** | 分位点回帰における交差（Quantile Crossing）による近似誤差やバイアスを解消し、分布の正確な推定を目指している点 [5, 6]。 | これらの手法は非交差ペナルティや単調ネットワークを用いて分位点の逆転を防ぐアーキテクチャの提案であり、リスク尺度に基づく重点的な学習領域の変更を目的としていない。 | 分位点交差の回避は分布型RLの基盤的な改良であるが、本提案は「どの分位点にリソース（フラクション）を割くべきか」という全く異なる次元での関数近似の最適化アプローチである。 |
| **MMDQN [11], SinkhornDRL [12], Cramér距離 [10] 系などの損失関数置換研究** | 分布型RLの目的関数であるWasserstein距離を、Cramér距離 [10]、最大平均自己矛盾（MMD）によるモーメントマッチング（MMDQN） [11]、Sinkhorn divergenceで正則化したWasserstein損失（SinkhornDRL） [12] 等に置き換え・正則化して学習を安定化させている点 [10, 11, 12]。 | これらの研究は真の分布と近似分布の間の「距離測度」そのものを変更し、計算の効率化や不偏推定量の獲得を目指すものであり（SinkhornDRLはWasserstein損失のSinkhorn正則化である点に注意）、歪み分布に基づく重み付けを行っていない（なお損失側の改良としてquantile Huber損失をロバスト化したMalekzadeh et al. [13] もあるが、分位点グリッドは固定のままである）。 | リスク中立的な距離測度の探索に終始する既存研究に対し、本提案は「リスク尺度にとって重要なのは歪み分布のW1距離である」という洞察に基づき、損失関数とリスク評価を理論的に直結させている。 |
| **スペクトルリスク尺度(SRM)を最適化する研究 (Moghimi & Ku 2025 [18, 19], Kim et al. 2024 [20])** | 歪み関数の積分として表現されるスペクトルリスク尺度（SRM）を分布型RLの枠組みで最適化（Actor-Criticや双対最適化）している点 [18, 19, 20]。 | 静的SRMを用いたActor-Critic（オンライン・オフライン双方に適用可能） [19] や、双対変数を用いたリスク制約付きsafe RL（収束保証付き、オンライン設定） [20] の提案であり、関数近似の量子化レベル（フラクション配置）の最適化については議論していない。 | 複雑な形状のSRMを使用する場合、重要となる分布領域は動的に変わる。本提案は、任意の歪み関数 ![][image5] に対して自動的に最適な量子化点を見つけ出す普遍的なメカニズムを提供する。 |
| **FQF の後続研究 (E-FQF [9], NDQFN [6], QEMRL [8] 等)** | Fraction Proposal Network (FPN) の枠組みを継承し、計算効率や安定性、分散の削減などを改善する目的を持つ点 [6, 8, 9]。 | QEMRLはCornish-Fisher展開による分散制御 [8]、E-FQFは計算効率化（知覚不確実性下の自動運転という応用論文内で提案されたFQFの効率化版） [9]、NDQFNは単調性保証 [6] を目的としており、リスク尺度に応じたフラクション再配分は行われていない（なおTQC [7] はQR-DQN系の分位点criticを連続制御用actor-criticへ拡張した手法であり、FPNの継承とは位置づけられない）。 | 既存のFQF改良手法はリスク中立的な期待値の枠組みに留まっていたが、本提案はFQFを「リスク感応型制御のためのアーキテクチャ」へと本質的に拡張する最初のアプローチである。 |
| **DSAC (Ma et al. 2020/2023) — リスク文脈でのFQF利用** [46] | 値分布を分位点分数で近似し、CVaR等のリスク感応型制御に用いる点。FQF型の分数提案ネットワークを「モジュールとして差し替え可能」と明記している点 [46]。 | 分数生成器はQR-DQN（固定）・IQN（一様サンプル）・FQF（学習型）から選択可能とするのみで、学習損失はリスク中立のままであり、歪み重み付きW1への変更は一切ない [46]。 | リスク尺度を読み出し側で適用するだけでは分数配置は最適化されないことを対比として示し、提案手法が初めて「損失側」で歪み重みを扱うことを主張できる。 |
| **Coache & Jaimungal (2024) 等の歪みリスク×分位点表現の理論系** [45] | 歪みリスク尺度の分位点表現を用いて方策勾配を導出し、歪み関数をNNで推定する点 [45]。 | 分位点分数は一様サンプリング U[0,1] であり、分数の配置学習は行わない。ロバスト化もWasserstein球内のモデル最悪化であり、criticの量子化とは別次元である [45]。 | 歪みの分位点表現を「方策勾配」ではなく「分数配置の学習目的（歪み重み付きW1の最小化）」に用いる点が本提案の差分である。 |

### **3.2. Q3: 金融応用面（デルタヘッジ等）の先行研究**

金融市場における自己資本の保護やダウンサイドリスクの管理という観点から、分布型RLの応用は急速に拡大している。特に、Buehlerらによる「Deep Hedging」の登場以降 [25]、デリバティブのヘッジング問題は期待値の最大化から、CVaRなどの凸リスク尺度の最小化へとパラダイムシフトを遂げた [25]。

| 比較対象の研究カテゴリー | 類似点 | 相違点 | 本提案が差分として主張できる点 |
| :---- | :---- | :---- | :---- |
| **Deep Hedging [25] および分布型RLを用いたヘッジング研究 (Tail-Safe [23], EX-DRL [24], Deep Diffusion RL [32]（※査読なし）)** | オプションのデルタヘッジやポートフォリオ最適化において、CVaR等のテールリスク尺度を目的関数（または制約条件）として用いてP\&Lの分布を最適化している点 [23, 24, 25]。 | 大半のDeep Hedging研究は、リスク尺度の評価に経験分布やC51等の固定グリッド、あるいは一様サンプリングのIQNを使用しており、関数近似のノード自体を最適化していない。 | オプションのペイオフは原資産価格に対して非線形（ガンマやベガ等）であり、テールリスクの精密な評価が不可欠である。本提案は、限られたネットワーク容量でもテール部分に自動的に解像度を集中させるため、ヘッジ効率を劇的に向上させ得る。 |
| **フラクション学習・![][image1] サンプリング設計に言及した金融研究 (Tail-Safe, Zhang, J. 2025) [23]** | Tail-Safe Hedging (Zhang, J. 2025) のように、CVaRの推定精度を担保するために、小さい ![][image6] においても実効的なサンプルサイズを確保する工夫をしている点 [23]。 | Tail-Safeは温度付きサンプリング（temperature tilting）という発見的な手法に依存しており、分位点の配置を明示的に「歪みWasserstein距離の最小化」として解析的に解いているわけではない [23]。 | デルタヘッジ等のリスク制約付き最適化において、フラクション自体の勾配を ![][image7] 倍として解析的に導出し、適応的グリッドを用いたヘッジ成績の向上を理論的裏付けとともに実証できる。 |
| **分位点回帰型ヘッジング (Cao, Chen, Hull et al. 2022 [51]; Sharma et al. 2024 [52])** | オプションや構造商品のヘッジに分位点回帰型の分布型criticを用い、VaR/CVaRでヘッジ成績を評価している点 [51, 52]。 | いずれも全文確認の結果、分位点レベルは固定一様グリッドであり、学習されるのは分位点の「値」のみ。リスク尺度は方策・目的関数側で適用される [51, 52]。 | criticのサポート点配置自体をリスク尺度に適応して学習する提案手法との明確な差分となり、金融応用における空白を実証的に示せる。 |

### **3.3. Q4: 理論的先行研究（数理ファイナンスと最適輸送）**

本提案の中核をなす「歪みWasserstein距離」と「最適量子化」の概念は、純粋な数理ファイナンスおよび最適輸送理論（Optimal Transport）の分野で長年研究されてきたテーマである。本研究アイデアの理論的妥当性を裏付ける一方で、査読者からの「既知の数学的帰結に過ぎないのではないか」という批判に対する防衛線を構築する必要がある。

| 比較対象の研究カテゴリー | 類似点 | 相違点 | 本提案が差分として主張できる点 |
| :---- | :---- | :---- | :---- |
| **歪みリスク尺度とWasserstein距離の関係 (Pichler & Xu 2022 [28], Pflug & Pichler 2014 [29], Balbás, Garrido & Mayoral 2009 [30], Rahimian & Mehrotra 2022 [31])** | リスク尺度（歪みリスク尺度等）とWasserstein距離の関係に関する定量的安定性の結果が数学的に確立されている点 [28, 29]。 | Pichler & Xu (2022) [28] は歪みリスクを目的に含むミニマックス分布的ロバスト最適化（DRO）のWasserstein距離に関する定量的安定性を、Pflug & Pichler (2014) [29] は多段階確率最適化の安定性理論を扱っており、Balbás, Garrido & Mayoral (2009) [30] は歪みリスク尺度の公理的性質を純粋な確率変数の汎関数として研究している。いずれも深層学習における関数近似誤差や強化学習アーキテクチャの設計には言及していない。 | 既存の数学的定理（リスク尺度の誤差が歪みW1距離で上から抑えられること）を、初めて深層強化学習の損失関数設計として再解釈し、アルゴリズムの最適化目的として実装した実践的貢献がある。 |
| **1次元分布の最適量子化 (Graf & Luschgy 2000 [27], Bardou, Frikha & Pagès 2016 [26])** | 確率分布を有限個の代表点で近似する「最適量子化（Optimal Quantization）」の理論を用いており、FQFの理論的基盤と同一の数学的構造を持つ点 [27]。 | Graf & Luschgy (2000) [27] は一様測度や特定の連続測度に対する静的な量子化（Voronoi分割など）を扱い、Bardou, Frikha & Pagès (2016) [26] の量子化に基づくCVaRヘッジも事前に構成した静的な量子化グリッドを用いる。いずれも動的に変化する歪み測度下での強化学習最適化ではない。 | リスク中立な一様測度に基づく従来のFQFのProposition 1 [4] を、「歪み測度空間上での最適量子化」へと拡張し、Fraction Proposal Networkの勾配導出という具体的な計算手法を提示した点が新規である。 |
| **歪みリスク尺度の基礎理論 (Yaari 1987 [33], Wang 1996 [34], Kusuoka 2001 [35], Acerbi 2002 [36], Dhaene et al. 2006 [37], Rockafellar & Uryasev 2000/2002 [38, 39])** | 歪み選好の公理論、分位点関数の歪み変換（Wang変換）、法則不変整合的リスク尺度の表現定理、分位点積分表現といった、本提案の数学的前提を構成する既知の理論 [33-39]。 | いずれも静的な確率変数の汎関数としての理論であり、深層学習・強化学習の関数近似やアーキテクチャ設計には言及しない。 | 既知の数学的前提を、分位点分数の学習アルゴリズム（FPNの損失設計と閉形式勾配）として実装した点に本提案の貢献を置く。 |
| **リスク尺度と最適輸送・最適量子化の交差 (Escobar & Pflug 2018 [40], Bernard et al. 2022 [41], Faugeras & Pagès 2024 [43], Bonalli et al. 2025 [44])** | リスク尺度をWasserstein距離や最適輸送と結びつける研究は数理ファイナンス・確率論に既に存在する [40, 41, 43, 44]。 | Escobar & Pflug [40] とBernard et al. [41] はWasserstein曖昧性下の歪みリスク尺度の挙動、Faugeras & Pagès [43] は2点分布への特殊な射影、Bonalli et al. [44] はOTによる表現定理であり、いずれも「歪み重み付きW1の最小化による分位点分数配置の学習」を含まない。 | 「歪み重み付き1-Wasserstein距離」という名前の定義されたオブジェクト、およびそれを最小化する分数配置学習の理論は、検索した限り存在しない（第9節参照）。 |

## **4. 差分の主張として推奨する言い回し (Related Work文案)**

論文の「Related Work」節において、既存の分布型RLや金融工学におけるアプローチと本研究との明確な線引きを行い、理論的かつ実用的な優位性を強調するため、以下の英文案（3〜5文）を使用することを強く推奨する。
> "While risk-sensitive distributional reinforcement learning has extensively leveraged distorted sampling distributions within Implicit Quantile Networks (IQN) (Dabney et al., 2018 [3]) and heuristic tail-coverage regularizers for financial applications (Zhang, 2025 [23]), these methods inherently rely on continuous approximation capacity and do not explicitly optimize the discrete support locations of the quantile representation. On the other hand, the Fully Parameterized Quantile Function (FQF) (Yang et al., 2019 [4]) adaptively learns the quantile fractions via 1D optimal quantization, yet it strictly minimizes the uniform 1-Wasserstein metric. Recent risk-sensitive extensions apply distortion or spectral weights only to the sampled τ or to the quantile values, leaving the quantile fractions uniformly fixed (Moghimi & Ku, 2025 [18]; Coache & Jaimungal, 2024 [45]). This uniform objective inevitably leads to suboptimal sample efficiency and structural bias when evaluating specific tail risks, such as CVaR. Our work bridges this critical gap by extending the foundations of optimal quantization (Graf & Luschgy, 2000 [27]) to distorted probability measures, rederiving the fraction proposal network's objective as the distortion-weighted 1-Wasserstein distance. By doing so, we provide a theoretically grounded framework that automatically concentrates quantile fractions in risk-sensitive regions, yielding a tighter ![][image8] error bound for CVaR estimation and significantly enhancing risk-averse control without increasing the model's parameter footprint."

## **5. リスク指摘：査読者からの予想される反論と防衛戦略**

本論文をNeurIPSやICML、あるいはMathematical Financeなどのトップレベルの国際会議・ジャーナルに投稿する際、数理ファイナンスや分布型RLの専門家である査読者から予想される厳しい批判（Risk Points）と、それに対する論理的な防衛策を以下に列挙する。

> 1. **「理論的結果（誤差の上界等）は、Pichler & Xu 等の既存のWasserstein安定性定理の単なる再述・応用ではないか？」**
   * **想定される批判**: Pichler & Xu (2022) [28]、Pflug & Pichler (2014) [29]、Escobar & Pflug (2018) [40]、Bernard et al. (2022) [41] により、リスク尺度とWasserstein距離の定量的安定性は既に広く研究されている。命題2は自明（Folklore）である。
   * **防衛戦略**: 命題自体が全く新しい数学的発見であると主張するのではなく、「数理ファイナンスにおいて独立して知られていた最適量子化とリスク尺度の連続性の結果を、初めて深層強化学習（FQF）のFraction Proposal Networkのアーキテクチャ設計に直接的に翻訳・実装したこと」を主眼に置く。理論と深層学習アーキテクチャ（勾配計算の閉形式の導出）の架け橋を構築し、強化学習の文脈で実用的なCVaRの誤差改善を証明した実証的価値を強調する。
> 2. **「勾配に ![][image7] を乗じるだけなら、損失関数の重み付けを変えただけであり、機械学習の新規性として効果が限定的（Incremental）ではないか？」**
   * **想定される批判**: FQFの実装において、フラクションの勾配計算時に係数を掛けるだけの変更であれば、アルゴリズム上の新規性は極めて薄い。
   * **防衛戦略**: 勾配が単なるスケール変換になることは、逆に「アルゴリズムのシンプルさと既存フレームワークへの組み込みやすさ（Plug-and-play性）」という強みとしてアピールする。同時に、一見単純なこの重み付けが「歪み分布上での1D最適量子化」という強固な理論的裏付けを持っていることを数学的に証明し、単なるアドホックなヒューリスティックではないことを明確にする。
> 3. **「IQNに適切な歪み（CVaRに合わせた重点サンプリング）を適用するだけで十分であり、FQFをわざわざ拡張するほどの計算コストに見合う効果がないのではないか？」**
   * **想定される批判**: Dabney et al. (2018) [3] のリスク感応型IQNや、Zhang, J. (2025) のTail-Safe [23] のように、![][image1] を単に尾部で多くサンプリングすれば済む話ではないか。ネットワークを一つ追加するFQFは非効率である。
   * **防衛戦略**: ランダムサンプリングに基づくIQNと、決定論的なサポート点を最適化するFQFでは、近似の性質が本質的に異なることを説明する。特に、![][image6] が0.01などの極端なテールリスクを評価する場合、IQNではサンプリング分散が極端に大きくなるが、提案手法（歪みFQF）は限られた ![][image3] 個のフラクションを確定的に最適な位置に配置するため、バイアスと分散の両面で定量的な優位性があることをアブレーション・スタディで証明する。
> 4. **「フラクションが極端に偏ることで、分布全体の形状（特にリスク中立的な期待値の評価）が崩れ、学習が不安定になるのではないか？」**
   * **想定される批判**: CVaRの評価のためにフラクションを下側尾部に集中させると、中央から上側尾部にかけての分布の解像度が極端に低下し、ベルマンバックアップによる価値更新全体が不安定化するリスクがある。
   * **防衛戦略**: 提案手法がTD誤差の学習に与える影響を分離し、「ポリシーの目的関数としてどのリスク尺度を用いるか」と「分布推定のための表現力をどこに割り当てるか」のトレードオフを論じる。必要であれば、完全にCVaRのみに特化するのではなく、一様重みと歪み重みのハイブリッド損失（正則化項の導入）などの工夫を補足的に提示する。

## **6. 推奨する追加ベースライン**

本提案の実験評価において、論文の主張（「フラクションの最適化が単なるサンプリング操作を上回る」こと）を裏付けるために、以下のベースライン手法との厳密な比較を含めることを強く推奨する。

> 1. **Tail-Safe近似 (IQN \+ Temperature-tilted Sampling / Tail-Coverage Controller)** (Zhang, J., arXiv:2510.04555, 2025) [23]（※単著・査読なしプレプリント）: 直近の金融応用（デリバティブヘッジ）に特化した分布型RL手法である。IQNのサンプリングを尾部に偏らせる手法（温度スケーリング等）を模倣したベースラインとの比較が必須である。これにより、「発見的なサンプリング確率の操作」に対する「解析的な最適量子化」の優位性を実証できる。
> 2. **Risk-sensitive IQN** (Dabney et al., 2018) [3]: IQNにおいて、標準的な ![][image2] ではなく、CVaRに合わせた ![][image9] でサンプリングを行う最も標準的な手法。これと比較して、提案手法の「フラクション自体の適応的学習」がいかに近似誤差を減らすかを示す。
> 3. **FQF \+ 損失の重要度重み付け (Heuristic Weighted FQF)** (Yang et al., 2019) [4]:
>    フラクションの学習（Proposal Network）自体は通常の1-Wasserstein距離（一様重み）で行い、Actor（方策更新）側の目的関数の計算時のみCVaRを使用する、従来型のFQFの素朴な流用。提案手法のように「フラクション自体が尾部に自動的に集中すること」による表現力向上の優位性を示すためのアブレーションとして極めて有効である。
> 4. **DRL-ORA** (Wu et al., 2026, UAI) [21]: オンラインで認識論的リスクと暗黙の偶然的リスクを適応的に調整する最新手法 [21]。直接的なアルゴリズムの競合ではないが、近年のリスク適応型分布型RLとして言及し実験に含めることで、査読者に最新の動向を熟知しているという強い印象を与えることができる。

## **7. 使用した検索クエリの一覧（再現性のため）**

検索の網羅性の担保と、本報告書の「不在証明」の証拠として、以下の検索クエリ群を用いて各種データベース（arXiv, OpenReview, NeurIPS/ICML/ICLR proceedings, JMLR, TMLR, SSRN, Google Scholar, Semantic Scholar等）を走査した。

* "fully parameterized quantile function" risk-sensitive / CVaR / distortion
* "fully parameterized quantile function" "risk" OR "CVaR" OR "spectral" OR "distortion"
* "fraction proposal network" CVaR OR "risk measure"
* "fraction proposal network" "risk" OR "CVaR" OR "spectral"
* "quantile fractions" "distributional reinforcement learning" tail OR CVaR OR "risk-sensitive"
* "distorted" OR "distortion" "Wasserstein" "distributional reinforcement learning" quantile
* "spectral risk measure" "distributional reinforcement learning" quantile
* "optimal quantization" "distortion risk measure" OR "spectral risk measure" Pflug OR Pichler OR Pagès
* "weighted Wasserstein" "risk measure" quantile approximation
* IQN tau sampling distribution non-uniform tail CVaR "importance"
* "learned quantile levels" OR "adaptive quantile levels" reinforcement learning risk
* distributional RL "delta hedging" CVaR quantile IQN FQF
* "Tail-Safe" "quantile" OR "distributional" OR "arXiv:2510.04555"
* "DRL-ORA" "distributional" OR "quantile" OR "OpenReview"
* "Spectral-Risk Safe Reinforcement Learning with Convergence Guarantees"

これらの緻密なクエリを通じ、提案手法の「FQFのフラクションネットワークを歪み分布間のWasserstein距離で学習する」というコアアイデアに対する直接の先行研究は存在しないことが確認された。本修正版の作成にあたり2026-09-08に主要引用の実在性・内容の再検証を行ったが、この結論を覆す直接的な先行研究は確認されなかった。本研究は、数学的基盤（数理ファイナンスにおけるWasserstein計量の性質）と応用（分布型RLアーキテクチャおよびヘッジング）を高度に接続するものであり、学術界に多大な貢献をもたらすものと確信する。

## **8. 引用修正履歴（2026-09-08の検証に基づく）**

### **8.1. 誤帰属・著者名の修正（重大）**

* **旧文献25「Pflug & Pichler (2016)」→ 誤り。** 引用先URL（OJMO 10.5802/ojmo.15）の実際の論文は **Rahimian & Mehrotra (2022) "Frameworks and Results in Distributionally Robust Optimization"**（DROのサーベイ）であり、PflugでもPichlerでも著者に含まれない。新文献31として修正。Pflug & Pichlerの実在業績として、書籍 *Multistage Stochastic Optimization*（Springer, 2014）を新文献29として追加。
* **旧文献26「Pichler (2015), Properties of Distortion Risk Measures」→ 誤り。** 同名論文の実際の著者は **Balbás, Garrido & Mayoral**（*Methodology and Computing in Applied Probability*, 2009）であり、「Pichler (2015)」という著者・年の組み合わせの論文は実在未確認。新文献30として修正。
* **「Pan & Jain (2024), Distributional GFlowNets, TMLR」→ 著者名の混同。** *Distributional GFlowNets with Quantile Flows*（TMLR 2024）の著者は **Zhang, Pan, Chen, Courville & Bengio** であり、Jainは含まれない。「Pan & Jain」は別の論文 *Pre-Training and Fine-Tuning Generative Flow Networks*（Pan, Jain, Madan, Bengio, ICLR 2024）の著者で、両者が混同されていた。前者を新文献22として修正し、後者（本件とは無関係）は削除。
* **「Bastani 2025」→ 削除。** 文献16（旧）＝arXiv:2507.03900 の著者は **Moghimi & Ku** であり、「Bastani」という著者は存在しない。「Kim 2024」はNeurIPS 2024のSRM safe RL論文（Kim et al.）として正当なため残した（新文献20）。
* **「MMD-DRL (Feng et al., UAI 2019)」→ 実在未確認のため削除。** 実在する最も近い研究は **Nguyen, Gupta & Venkatesh (2021) "Distributional Reinforcement Learning via Moment Matching"（AAAI 2021, 手法名MMDQN）** であり、こちらを新文献11として採用。
* **旧文献9「Pagès et al. (2016)」→ 著者表記を修正。** 該当論文の著者は **Bardou, Frikha & Pagès**（*Mathematical Finance* 26(1), 2016）であり、Pagèsは第三著者。併せて、表記されていた「CVaR estimation with adaptive quantization」という題名の論文は実在しない（近接業績の題名混同）ため、正式題名に修正（新文献26）。

### **8.2. 会場・題名・内容記述の修正**

* **TQC（旧文献22）**: 会場は **ICML 2020**（PMLR v119）。NeurIPS 2020という記載は誤り。正式題名は "Controlling Overestimation Bias with Truncated Mixture of Continuous Distributional **Quantile Critics**"（旧記載の "...Quantile Regression" は不正確）。またTQCはQR-DQN系criticの連続制御への拡張であり、FQFのFPNを継承しないため「FQF後続研究」行の記述を修正（新文献7）。
* **NDQFN**: **IJCAI 2021**（Zhou, Zhu, Kuang, Zhang）。旧版では「NDQFNは単調性保証」の根拠としてFQFのSemantic Scholarページ（旧文献18）を引用していたが誤引用であり、原典（新文献6）を追加。
* **NC-QR-DQN**: 原典 **Zhou, Wang & Feng, NeurIPS 2020**（新文献5）を追加。旧版では原典が引用リストに存在しなかった。
* **Lim & Malik (2022)**: 正式題名は **"Distributional Reinforcement Learning for Risk-Sensitive **Policies**"**（NeurIPS 2022）。「...Sequential Decision Making」という題名は誤り（新文献15）。
* **Pichler & Xu**: 正式題名は "Quantitative Stability Analysis for Minimax Distributionally Robust **Risk** Optimization"（*Mathematical Programming* 191:47–77、オンライン2018／印刷2022）。旧記載から "risk" が欠落していた（新文献28）。
* **Bäuerle**: 旧版の「Bäuerle & Ottone (2018)」「Bäuerle & Glass (2021)」は確認不能（おそらく **Bäuerle & Ott (2011)** および **Bäuerle & Glauner (2022)** の混同）。実在が確認できた次の2編を採用：Bäuerle & Ott, "Markov Decision Processes with Average-Value-at-Risk Criteria"（MMOR 74, 2011、新文献16）；Bäuerle & Glauner, "Markov Decision Processes with Recursive Risk Measures"（EJOR, 2022、新文献17）。
* **SinkhornDRL**: 実在（Sun et al., NeurIPS 2024）だが、内容は「Wasserstein損失の**Sinkhorn正則化**」であり、「置換」という記述を修正（新文献12）。
* **Cramér距離論文**: Bellemare et al., arXiv:1705.10743（2017）。ICLR 2018に投稿されたが採録記録は確認できず、arXiv版が一次情報（新文献10）。旧版では会場不記載。
* **文献17/20（旧）の「オフライン環境でのSRMの適用」→ 修正。** NeurIPS 2024のSRM safe RL論文（Kim et al.）は**オンライン**のリスク制約RLであり、offlineは扱っていない。「online and offline」を扱うのはMoghimi & Kuの別論文（arXiv:2507.03900）である。両者を分けて記載（新文献19, 20）。
* **E-FQF**: 実在するが、**知覚不確実性下の自動運転という応用論文（Xu et al., 2023）内で定義されたFQFの効率化版**であり、独立のアルゴリズム論文ではない旨を注記（新文献9）。
* **EX-DRL**: 実在確認（Malekzadeh et al., arXiv:2408.12446）。旧版では引用リストに存在しなかったため原典を追加（新文献24）。なお「EVT」という語自体は原典のアブストラクトに現れず、GPDによる尾部モデル化として記述を修正。
* **旧文献13（Grün et al., Invariance to Quantile Selection）**: 実在するが、内容は分位点の「選択」に対する不変性であり、「分位点交差（crossing）」とは別問題のため引用文脈を修正し、本文で未参照のため参考文献として保持（新文献14）。

### **8.3. 追加した原典（旧版で本文から参照されていたが引用リストに存在しなかったもの）**

* C51: Bellemare, Dabney & Munos, ICML 2017（新文献1）
* QR-DQN: Dabney, Rowland, Bellemare & Munos, AAAI 2018（新文献2）
* IQN: Dabney, Ostrovski, Silver & Munos, ICML 2018（新文献3）— リスク感応実験（CPW・Wang・CVaR）の記述は原典で確認済み
* Deep Hedging: Buehler, Gonon, Teichmann & Wood, *Quantitative Finance* 19(8), 2019（新文献25）— 旧版では査読なしプレプリント（旧文献23）のみを「Deep Hedging」の根拠としていた
* MMDQN（AAAI 2021）、SinkhornDRL（NeurIPS 2024）、Cramér（arXiv 2017）: 「損失関数置換」行の根拠として追加（新文献10–12）

### **8.4. 削除・差し替えた出力先URL**

* **削除**: chatpaper.com（旧文献5、Tail-Safeの重複）、Stanford SHTEM学生レポート（旧文献14、査読なしの学生プロジェクト報告。DSAC原典はMa et al. 2020, arXiv:2004.14547）、Pan & Jain "Pre-Training and Fine-Tuning Generative Flow Networks"（旧文献3、本件と無関係）、eBay・Scribd（旧文献7・8、非学術的ソース）
* **差し替え**: Graf & Luschgy (2000) は Springer公式DOI（10.1007/BFb0103945）へ（新文献27）。Tail-SafeはarXiv公式ページへ統合（新文献23）。FQFは4つの重複参照（旧10/12/18/27）を1件に統合（新文献4）。Tail-Safeの3重複（旧4/5/6）とKim et al.の2重複（旧17/20）も統合。
* **注記を追加した文献**: Tail-Safe（単著・査読なしプレプリント）、Deep Diffusion RL for Options Hedging（Preprints.org・査読なし）、Moghimi & Ku arXiv:2507.03900（プレプリント）、Grün et al. arXiv:2212.14262（プレプリント）

### **8.5. 検証で正しいと確認できた主な引用**

FQF（Yang et al., NeurIPS 2019）のProposition 1（1-Wasserstein最小化）とフラクション勾配の閉形式、QEMRLのCornish-Fisher展開、E-FQFの存在、DRL-ORA（UAI 2026）の記述、Tail-Safeの「Tail-Coverage Controller」・temperature tilting・tail boosting・CBF-QP層、IQNのCPW/Wang/CVaR実験、EX-DRLのGPDによる尾部補正、Deep Hedgingの凸リスク尺度最適化、Kim et al.（NeurIPS 2024）の双対変数と収束保証、Graf & Luschgy（LNM 1730）の書誌事実、Bardou, Frikha & Pagès（Mathematical Finance 2016）の内容 — いずれも原典との照合で正しいことを確認した。

## **9. 追加調査結果（2026-09-08 第二次調査）**

第一次修正版の作成後、不在結論の頑健性を試すため、(i) 2025-2026年の最新研究、(ii) 数理的基盤の原典、(iii) 金融応用、(iv) コアアイデア正面からの不在確認、の4角度から追加調査を実施した（候補約40件をabstractまたは全文レベルで検証）。本節の知見は第2・3節の文献表と第4節のRelated Work文案にも反映し、新たな引用文献を33番以降に追加した。全調査文献の一覧は別ファイル「**Risk-Sensitive FQF 調査文献リスト.md**」を参照。

**総括: 「FQFのFPN目的関数を歪み重み付き1-Wasserstein距離へ変更し、分位点分数の配置を学習する」直接の先行研究は引き続き確認されず、不在結論は維持される。** ただし、以下の知見を得た。

### **9.1. 新規性の位置づけに必須の近接文献**

> 1. **IQN (Dabney et al., 2018) [3] が「歪み×分位点」の元祖であることの明示。** τの再エンコード（読み出し時）に歪みを適用する発想はIQNに既に存在する。本提案の貢献は「歪み重み付きW1としての理論的再定式化（等価性の証明と誤差評価）」であり、「歪みの適用」そのものではないことをRelated Workで明記すること。
> 2. **Beyond CVaR (Moghimi & Ku, ICML 2025) [18] との対比が最重要。** 同論文のスペクトル重み μ̃ᵢ = φ(τᵢ₋₁) − φ(τᵢ) は本提案の歪み重みと数学的に同型であるが、全文確認の結果、重みは分位点の「値」に掛かるだけで、分数は一様固定（τᵢ = i/N）、学習損失は標準quantile Huberのままである。差分は「重みを値側ではなく損失側（FPN勾配）へ移すことによる分数配置の非対称化と、それに伴う誤差評価」であり、これを新規性の核として明示すべきである。
> 3. **Faugeras & Pagès (2024) [43]** —「リスク尺度 × 最適量子化 × Wasserstein」の交差が数理ファイナンス側に既に存在する（リスク変数のmagnitude/propensityへの2点分布射影）。ただし歪み重み付きW1によるタウ配置の理論は含まず、related workでの位置づけが必要。
> 4. **Bonalli, Bonnet & Pfeiffer (2025) [44]** — 法則不変な整合的リスク尺度を最適輸送で特徴づける表現定理（Kusuoka型）。時期的・概念的に最も衝突しやすい最新理論であり、精読のうえ、本提案の表現（単一の歪み重み付きW1の最小化）が含まれないことを確認すること。
> 5. **Coache & Jaimungal (2024) [45]** — 歪みリスク尺度の分位点表現から方策勾配を導出するが、τは一様サンプリングで分数学習はなし。歪みの分位点表現を「方策勾配」ではなく「分数配置の学習目的」に用いる点が差分。
> 6. **DSAC (Ma et al.) [46]** — FQF型の分数提案ネットワークを「モジュールとして差し替え可能」と明記した、リスク文脈でFQFを使う建築的先行例。ただし歪み重み付き学習は一切ない。
> 7. **2025-2026年の新潮流**: RQIQN (Zhang et al., 2026) [49]（IQN＋Wasserstein DRO）、Jullien et al. (UAI 2025) [50]（expectileとquantileの同時学習）、DRIQN等が「IQN/FQFの分位点幾何をリスク目的で改造する」方向で活発化している。プレプリントが多く、投稿直前の再検索を推奨。
> 8. **用語衝突**: Iwaki & Osogami (ICONIP 2025) [48] が「quantile distortion」という用語を（オフライン方策評価の悲観化の意味で）既に使用している。本提案での用語選択と引用に注意。
> 9. **動機の第三者的支持**: Prasad (2026) [47] は、固定一様グリッドの分位点criticのテール統計（CVaR等）精度そのものの信頼性を監査しており、「一様配置では尾部精度が不十分」という本提案の動機付けを支持する引用元となる。
> 10. **金融応用の空白の確認**: Cao, Chen, Hull et al. (2022) [51]、Sharma et al. (2024) [52] など分位点回帰型ヘッジング研究を全文確認した結果、分位点レベルはいずれも固定一様グリッドであった。「学習済み分位点配置＋CVaRヘッジング」の組み合わせは2026年9月時点で空白。

### **9.2. 基礎原典の追加（引用文献33-42）**

本提案は「歪みリスク尺度の分位点表現 ρ_φ(X) = ∫₀¹ F⁻¹_X(u) dφ(u)」等を数学的前提としているが、第一次修正版ではその原典を引用していなかった。以下を実在確認のうえ追加した：歪み選好の公理論 Yaari (1987) [33]、Wang変換 Wang (1996) [34]、法則不変整合的リスク尺度の表現定理 Kusuoka (2001) [35]、スペクトルリスク尺度 Acerbi (2002) [36]、分位点積分表現のレビュー Dhaene et al. (2006) [37]、CVaRの分位点表現 Rockafellar & Uryasev (2000, 2002) [38, 39]、リスク汎関数のW1安定性 Escobar & Pflug (2018) [40]、Bernard, Pesenti & Vanduffell (2022) [41]、Prashanth & Bhat (2019) [42]。

### **9.3. 書誌上の注意点**

> 1. **Wang (1996) の書誌**: 通説で引用される題名 "Premium Calculation by Transforming the Rank Size Distribution" は、Crossref・OpenAlex・doi.orgのいずれでも確認できなかった。一次DBで実在を確認できたWang変換の標準出典は **"Premium Calculation by Transforming the Layer Premium Density"（*ASTIN Bulletin* 26(1): 71–92）** であり、こちらを採用した [34]。原本での最終確認を推奨。
> 2. **旧文献26「Pichler (2015)」の混同元の推定**: Pichlerには **"Premiums and Reserves, Adjusted by Distortions"（*Scandinavian Actuarial Journal* 2015(4): 332–351）** という実在論文があり、旧版がこれを同名の別論文（Balbás et al.）のURLと混同した可能性が高い。
> 3. **「DRL-ORA」略称の重複**: UAI 2026のWu et al. [21] のほかに、同名略称を掲題に用いる別論文（Yan et al., arXiv:2310.05179）が存在する。引用時は著者・掲載先を明記すること。
> 4. **確認不能文献**: Kjetil Ståhlum（NTNU修論、歪みリスク×分布型RLと想定される文献）は全主要インデックスで確認不能。ProQuestの博士論文1件（"learned quantile levels"の唯一のヒット）も内容検証不能。関連研究節で「確認できなかった」旨に一行記載するのが安全。

### **9.4. 不在結論の頑健性と盲点**

**傍証**: (a) "distortion-weighted Wasserstein" / "risk-weighted Wasserstein" という語句はarXiv・学術索引に事例ゼロ; (b) "fraction proposal network" を含むarXiv論文はFQF本体のみで、リスク文脈でのFPN改変は0件; (c) FQFの被引用192件の全走査で金融関連は3件のみ（いずれも分数固定）; (d) Tail-Safe Hedgingの被引用は0件; (e) 約40件の候補を全文レベルで検証し、「分数配置の勾配学習」＋「歪み重み付きW1目的」を両立するものは皆無であった。

**盲点（限界として明記すべき）**: Semantic Scholarの被引用全数スイープはレート制限で未完了; 非索引ソース（日本の学内紀要・修士論文、中国語学位論文、CNKI、J-STAGE一部）は未網羅; paywall先（IEEE/World Scientific等）は抄録ベースの確認に留まる; 2026年後半の極近期プレプリントは発見漏れの可能性がある。

#### **引用文献（修正版）**

> 1. Bellemare, M. G., Dabney, W., Munos, R. (2017). "A Distributional Perspective on Reinforcement Learning." ICML 2017, PMLR 70. https://proceedings.mlr.press/v70/bellemare17a.html （C51）
> 2. Dabney, W., Rowland, M., Bellemare, M. G., Munos, R. (2018). "Distributional Reinforcement Learning with Quantile Regression." AAAI 2018. https://arxiv.org/abs/1710.10044 （QR-DQN）
> 3. Dabney, W., Ostrovski, G., Silver, D., Munos, R. (2018). "Implicit Quantile Networks for Distributional Reinforcement Learning." ICML 2018. https://arxiv.org/abs/1806.06923 （IQN）
> 4. Yang, D., Zhao, L., Lin, Z., Qin, T., Bian, J., Liu, T.-Y. (2019). "Fully Parameterized Quantile Function for Distributional Reinforcement Learning." NeurIPS 2019. https://arxiv.org/abs/1911.02140 （FQF）
> 5. Zhou, F., Wang, J., Feng, X. (2020). "Non-Crossing Quantile Regression for Distributional Reinforcement Learning." NeurIPS 2020. https://proceedings.neurips.cc/paper/2020/hash/b6f8dc086b2d60c5856e4ff517060392-Abstract.html （NC-QR-DQN）
> 6. Zhou, F., Zhu, Z., Kuang, Q., Zhang, L. (2021). "Non-decreasing Quantile Function Network with Efficient Exploration for Distributional Reinforcement Learning." IJCAI 2021. https://doi.org/10.24963/ijcai.2021/476 （NDQFN）
> 7. Kuznetsov, A., Shvechikov, P., Grishin, A., Vetrov, D. (2020). "Controlling Overestimation Bias with Truncated Mixture of Continuous Distributional Quantile Critics." ICML 2020, PMLR 119. https://arxiv.org/abs/2005.04269 （TQC）
> 8. Kuang, Q., Zhu, Z., Zhang, L., Zhou, F. (2023). "Variance Control for Distributional Reinforcement Learning." ICML 2023, PMLR v202. https://proceedings.mlr.press/v202/kuang23a.html （QEMRL）
> 9. Xu, S., Liu, Q., Hu, Y., Xu, M., Hao, J. (2023). "Decision-making models on perceptual uncertainty with distributional reinforcement learning." *Green Energy and Intelligent Transportation* 2(2): 100062. https://doi.org/10.1016/j.geits.2022.100062 （E-FQF：本応用論文内で定義されたFQFの効率化版）
> 10. Bellemare, M. G., Danihelka, I., Dabney, W., Mohamed, S., Lakshminarayanan, B., Hoyer, S., Munos, R. (2017). "The Cramér Distance as a Solution to Biased Wasserstein Gradients." arXiv:1705.10743. https://arxiv.org/abs/1705.10743 （ICLR 2018に投稿。採録記録は確認できず、arXiv版が一次情報）
> 11. Nguyen, T. T., Gupta, S., Venkatesh, S. (2021). "Distributional Reinforcement Learning via Moment Matching." AAAI 2021. https://arxiv.org/abs/2007.12354 （MMDQN）
> 12. Sun, K., Zhao, Y., Liu, W., Jiang, B., Kong, L. (2024). "Distributional Reinforcement Learning with Regularized Wasserstein Loss." NeurIPS 2024. https://arxiv.org/abs/2202.00769 （SinkhornDRL）
> 13. Malekzadeh, P., Plataniotis, K. N., Poulos, Z., Wang, Z. (2024). "A Robust Quantile Huber Loss with Interpretable Parameter Adjustment in Distributional Reinforcement Learning." ICASSP 2024. https://arxiv.org/abs/2401.02325 （Wasserstein由来のquantile Huber lossの改善・一般化。「損失置換」研究とは区別して参照のこと）
> 14. Grün, F., Saif-ur-Rehman, M., Glasmachers, T., Iossifidis, I. (2022). "Invariance to Quantile Selection in Distributional Continuous Control." arXiv:2212.14262. https://arxiv.org/abs/2212.14262 （査読なしプレプリント。分位点の「選択」の不変性を扱い、「交差」問題とは別課題）
> 15. Lim, S. H., Malik, I. (2022). "Distributional Reinforcement Learning for Risk-Sensitive Policies." NeurIPS 2022. https://proceedings.neurips.cc/paper_files/paper/2022/hash/c88a2bd0e793550d0e885aa6e31ca277-Abstract-Conference.html
> 16. Bäuerle, N., Ott, J. (2011). "Markov Decision Processes with Average-Value-at-Risk Criteria." *Mathematical Methods of Operations Research* 74(3): 361–379.
> 17. Bäuerle, N., Glauner, A. (2022). "Markov Decision Processes with Recursive Risk Measures." *European Journal of Operational Research*. https://arxiv.org/abs/2010.07220
> 18. Moghimi, M., Ku, H. (2025). "Beyond CVaR: Leveraging Static Spectral Risk Measures for Enhanced Decision-Making in Distributional Reinforcement Learning." ICML 2025, PMLR v267. https://arxiv.org/abs/2501.02087
> 19. Moghimi, M., Ku, H. (2025). "Risk-sensitive Actor-Critic with Static Spectral Risk Measures for Online and Offline Reinforcement Learning." arXiv:2507.03900. https://arxiv.org/abs/2507.03900 （査読なしプレプリント）
> 20. Kim, D., Cho, T., Han, S., Chung, H., Lee, K., Oh, S. (2024). "Spectral-Risk Safe Reinforcement Learning with Convergence Guarantees." NeurIPS 2024. https://arxiv.org/abs/2405.18698
> 21. Wu, Y., Li, W., Huang, W., Ho, C. P. (2026). "DRL-ORA: Distributional Reinforcement Learning with Online Epistemic Risk Adaptation." UAI 2026, PMLR v337. https://proceedings.mlr.press/v337/wu26e.html
> 22. Zhang, D., Pan, L., Chen, R. T. Q., Courville, A., Bengio, Y. (2024). "Distributional GFlowNets with Quantile Flows." TMLR. https://arxiv.org/abs/2302.05793
> 23. Zhang, J. (2025). "Tail-Safe Hedging: Explainable Risk-Sensitive Reinforcement Learning with a White-Box CBF–QP Safety Layer in Arbitrage-Free Markets." arXiv:2510.04555. https://arxiv.org/abs/2510.04555 （単著・査読なしプレプリント）
> 24. Malekzadeh, P., Poulos, Z., Chen, J., Wang, Z., Plataniotis, K. N. (2024). "EX-DRL: Hedging Against Heavy Losses with EXtreme Distributional Reinforcement Learning." arXiv:2408.12446. https://arxiv.org/abs/2408.12446
> 25. Buehler, H., Gonon, L., Teichmann, J., Wood, B. (2019). "Deep Hedging." *Quantitative Finance* 19(8): 1271–1291. https://doi.org/10.1080/14697688.2019.1571683 （プレプリント: arXiv:1802.03042）
> 26. Bardou, O., Frikha, N., Pagès, G. (2016). "CVaR Hedging Using Quantization-Based Stochastic Approximation Algorithm." *Mathematical Finance* 26(1): 184–229. https://doi.org/10.1111/mafi.12049
> 27. Graf, S., Luschgy, H. (2000). *Foundations of Quantization for Probability Distributions*. Lecture Notes in Mathematics 1730. Springer. https://doi.org/10.1007/BFb0103945
> 28. Pichler, A., Xu, H. (2022). "Quantitative Stability Analysis for Minimax Distributionally Robust Risk Optimization." *Mathematical Programming* 191: 47–77（オンライン2018）. https://doi.org/10.1007/s10107-018-1347-4
> 29. Pflug, G. C., Pichler, A. (2014). *Multistage Stochastic Optimization*. Springer Series in Operations Research and Financial Engineering. Springer. https://doi.org/10.1007/978-3-319-08843-3
> 30. Balbás, A., Garrido, J., Mayoral, S. (2009). "Properties of Distortion Risk Measures." *Methodology and Computing in Applied Probability* 11(3): 385–399. https://doi.org/10.1007/s11009-008-9089-z
> 31. Rahimian, H., Mehrotra, S. (2022). "Frameworks and Results in Distributionally Robust Optimization." *Open Journal of Mathematical Optimization* 3: Article 4. https://doi.org/10.5802/ojmo.15
> 32. Liu, Y., Li, J., Chen, Y., Du, L., Xu, J. (2025). "Deep Diffusion Reinforcement Learning for Options Hedging." Preprints.org 202507.0360. https://doi.org/10.20944/preprints202507.0360.v1 （査読なしプレプリント）
> 33. Yaari, M. E. (1987). "The Dual Theory of Choice under Risk." *Econometrica* 55(1): 95–115. https://doi.org/10.2307/1911158 （歪み（双対）選好の公理論）
> 34. Wang, S. S. (1996). "Premium Calculation by Transforming the Layer Premium Density." *ASTIN Bulletin* 26(1): 71–92. （Wang変換の標準出典。※通説の題名 "Premium Calculation by Transforming the Rank Size Distribution" は一次DBで確認できなかったため本題名を採用。原本での最終確認を推奨）
> 35. Kusuoka, S. (2001). "On Law Invariant Coherent Risk Measures." *Advances in Mathematical Economics* 3: 83–95. https://doi.org/10.1007/978-4-431-67891-5_4 （法則不変整合的リスク尺度の表現定理）
> 36. Acerbi, C. (2002). "Spectral Measures of Risk: A Coherent Representation of Subjective Risk Aversion." *Journal of Banking & Finance* 26(7): 1505–1518. https://doi.org/10.1016/S0378-4266(02)00281-9
> 37. Dhaene, J., Vanduffel, S., Goovaerts, M. J., Kaas, R., Tang, Q., Vyncke, D. (2006). "Risk Measures and Comonotonicity: A Review." *Stochastic Models* 22(4): 573–606. https://doi.org/10.1080/15326340600878016 （歪みリスク尺度の分位点積分表現の標準レビュー）
> 38. Rockafellar, R. T., Uryasev, S. (2000). "Optimization of Conditional Value-at-Risk." *The Journal of Risk* 2(3): 21–41. https://doi.org/10.21314/jor.2000.038
> 39. Rockafellar, R. T., Uryasev, S. (2002). "Conditional Value-at-Risk for General Loss Distributions." *Journal of Banking & Finance* 26(7): 1443–1471. https://doi.org/10.1016/S0378-4266(02)00271-6 （CVaRの分位点積分表現）
> 40. Escobar & Pflug (2018). "The Distortion Principle for Insurance Pricing: Properties, Identification and Robustness." *Annals of Operations Research* 292(2): 771–794. https://doi.org/10.1007/s10479-018-3119-1 （曖昧性をWasserstein距離で測定）
> 41. Bernard, C., Pesenti, S. M., Vanduffel, S. (2022). "Robust Distortion Risk Measures." arXiv:2205.08850. https://arxiv.org/abs/2205.08850 （Wasserstein ball内の歪みリスク尺度の鋭い評価）
> 42. Prashanth, L. A., Bhat, S. P. (2019). "A Wasserstein Distance Approach for Concentration of Empirical Risk Estimates." arXiv:1902.10709. https://arxiv.org/abs/1902.10709 （歪みリスク尺度を含む推定誤差のW1集中評価。期刊版はCrossrefで未確認のためarXiv版で引用）
> 43. Faugeras, O. P., Pagès, G. (2024). "Risk Quantization by Magnitude and Propensity." *Insurance: Mathematics and Economics* 116: 134–147. https://doi.org/10.1016/j.insmatheco.2024.02.005 （プレプリント: arXiv:2105.13002。リスク×最適量子化×Wassersteinの既存交差）
> 44. Bonalli, Bonnet & Pfeiffer (2025). "A Characterization of Law-Invariant and Coherent Risk Measures through Optimal Transport." arXiv:2512.19157. https://arxiv.org/abs/2512.19157 （OTによるリスク尺度の表現定理。精読推奨）
> 45. Coache, A., Jaimungal, S. (2024). "Robust Reinforcement Learning with Dynamic Distortion Risk Measures." arXiv:2409.10096. https://arxiv.org/abs/2409.10096 （歪みの分位点表現による方策勾配。τは一様サンプリング）
> 46. Ma, X., Chen, J., Xia, L., Yang, J., Zhao, Q., Zhou, Z. (2020/2023). "DSAC: Distributional Soft Actor-Critic for Risk-Sensitive Reinforcement Learning." arXiv:2004.14547（期刊版はJAIR 2023）. https://arxiv.org/abs/2004.14547 （FQF型分数提案をモジュールとして差し替え可能と明記）
> 47. Prasad, H. (2026). "Auditing the Risk Claims of Distributional Reinforcement Learning." arXiv:2607.11607. https://arxiv.org/abs/2607.11607 （固定一様グリッドのテール統計精度の監査）
> 48. Iwaki, R., Osogami, T. (2025). "Distorted Distributional Policy Evaluation for Offline Reinforcement Learning." ICONIP 2025. arXiv:2601.01917. https://arxiv.org/abs/2601.01917 （「quantile distortion」の用語使用に注意）
> 49. Zhang, Z., Yang, M., Chen, R., Xie, S., Xiong, H. (2026). "Quantile Geometry Regularization for Distributional Reinforcement Learning." arXiv:2605.08182. https://arxiv.org/abs/2605.08182 （RQIQN。査読なしプレプリント）
> 50. Jullien, S., Deffayet, R., Renders, J.-M., Groth, P., de Rijke, M. (2025). "Distributional Reinforcement Learning with Dual Expectile-Quantile Regression." UAI 2025, PMLR v286. https://arxiv.org/abs/2305.16877 （expectileとquantileの同時学習）
> 51. Cao, J., Chen, J., Farghadani, S., Hull, J., Poulos, Z., Wang, Z., Yuan, J. (2022). "Gamma and Vega Hedging Using Deep Distributional Reinforcement Learning." arXiv:2205.05614. https://arxiv.org/abs/2205.05614 （分位点レベル固定一様 — 全文確認済み）
> 52. Sharma, N., Chen, J., Noh, E., Hull, J., et al. (2024). "Hedging Beyond the Mean: A Distributional Reinforcement Learning Perspective for Hedging Portfolios with Structured Products." arXiv:2407.10903. https://arxiv.org/abs/2407.10903 （分位点レベル固定一様 — 全文確認済み）


















