# **調査文献リスト：リスク感応型分布型強化学習における歪み重み付き分位点フラクション学習**

> **本ファイルは、新規性調査報告書（引用修正版）の作成・検証過程（2026-09-08実施の第一次・第二次調査）で確認した全文献を体系的にまとめたものである。** 抜き番号はない。基礎的グループ（G1-G4）の番号は報告書修正版の引用文献番号 [n] と一致する。各グループの見出しの「〔必要性〕」は、本提案の関連研究・理論構成における扱いの目安である。
>
> 判定記号： ✅＝実在・内容確認済み ／ ⚠️＝実在するが注意点あり（注記参照） ／ ❌＝実在未確認・誤帰属

---

## **G1. 分布型強化学習の基盤的手法（分位点・損失設計）** 〔必要性：本文の対比の基軸。必須〕

| 番号 | 文献 | 判定・備考 |
| :--- | :--- | :--- |
| [1] | Bellemare, M. G., Dabney, W., Munos, R. (2017). "A Distributional Perspective on Reinforcement Learning." ICML 2017, PMLR 70. https://proceedings.mlr.press/v70/bellemare17a.html | ✅ C51。固定離散サポート上の確率を学習 |
| [2] | Dabney, W., Rowland, M., Bellemare, M. G., Munos, R. (2018). "Distributional Reinforcement Learning with Quantile Regression." AAAI 2018. https://arxiv.org/abs/1710.10044 | ✅ QR-DQN。固定一様分位点フラクション＋quantile Huber損失 |
| [3] | Dabney, W., Ostrovski, G., Silver, D., Munos, R. (2018). "Implicit Quantile Networks for Distributional Reinforcement Learning." ICML 2018. https://arxiv.org/abs/1806.06923 | ✅ IQN。**「歪み×分位点」の元祖**（τの再エンコードでCPW・Wang・CVaRを実装）。リスク感応実験の記述は原典確認済み |
| [4] | Yang, D., Zhao, L., Lin, Z., Qin, T., Bian, J., Liu, T.-Y. (2019). "Fully Parameterized Quantile Function for Distributional Reinforcement Learning." NeurIPS 2019. https://arxiv.org/abs/1911.02140 | ✅ **FQF（本提案のベース）**。Proposition 1（一様重みW1の最小化）と分数勾配の閉形式を原典確認済み |
| [10] | Bellemare, M. G., Danihelka, I., Dabney, W., Mohamed, S., Lakshminarayanan, B., Hoyer, S., Munos, R. (2017). "The Cramér Distance as a Solution to Biased Wasserstein Gradients." arXiv:1705.10743. https://arxiv.org/abs/1705.10743 | ⚠️ ICLR 2018に投稿されたが採録記録は確認できず、arXiv版が一次情報 |
| [11] | Nguyen, T. T., Gupta, S., Venkatesh, S. (2021). "Distributional Reinforcement Learning via Moment Matching." AAAI 2021. https://arxiv.org/abs/2007.12354 | ✅ MMDQN。※旧報告書の「MMD-DRL (Feng et al., UAI 2019)」は実在未確認のため本文献に置換 |
| [12] | Sun, K., Zhao, Y., Liu, W., Jiang, B., Kong, L. (2024). "Distributional Reinforcement Learning with Regularized Wasserstein Loss." NeurIPS 2024. https://arxiv.org/abs/2202.00769 | ✅ SinkhornDRL。内容は「Wasserstein損失のSinkhorn正則化」であり「置換」ではない |
| [13] | Malekzadeh, P., Plataniotis, K. N., Poulos, Z., Wang, Z. (2024). "A Robust Quantile Huber Loss with Interpretable Parameter Adjustment in Distributional Reinforcement Learning." ICASSP 2024. https://arxiv.org/abs/2401.02325 | ✅ Wasserstein由来のquantile Huber損失のロバスト化。分位点グリッドは固定 |
| [14] | Grün, F., Saif-ur-Rehman, M., Glasmachers, T., Iossifidis, I. (2022). "Invariance to Quantile Selection in Distributional Continuous Control." arXiv:2212.14262. https://arxiv.org/abs/2212.14262 | ⚠️ 査読なしプレプリント。分位点の「選択」の不変性であり「交差」とは別課題 |

## **G2. 分位点交差・単調性・分散制御（FQF系の改良）** 〔必要性：FQF後続研究としての差別化。必須〕

| 番号 | 文献 | 判定・備考 |
| :--- | :--- | :--- |
| [5] | Zhou, F., Wang, J., Feng, X. (2020). "Non-Crossing Quantile Regression for Distributional Reinforcement Learning." NeurIPS 2020. https://proceedings.neurips.cc/paper/2020/hash/b6f8dc086b2d60c5856e4ff517060392-Abstract.html | ✅ NC-QR-DQN |
| [6] | Zhou, F., Zhu, Z., Kuang, Q., Zhang, L. (2021). "Non-decreasing Quantile Function Network with Efficient Exploration for Distributional Reinforcement Learning." IJCAI 2021. https://doi.org/10.24963/ijcai.2021/476 | ✅ NDQFN。※旧報告書がFQFのS2ページで代用していた誤引用を修正 |
| [7] | Kuznetsov, A., Shvechikov, P., Grishin, A., Vetrov, D. (2020). "Controlling Overestimation Bias with Truncated Mixture of Continuous Distributional Quantile Critics." ICML 2020, PMLR 119. https://arxiv.org/abs/2005.04269 | ⚠️ TQC。会場は**ICML 2020**（NeurIPSではない）。QR-DQN系の拡張でありFPN継承ではない |
| [8] | Kuang, Q., Zhu, Z., Zhang, L., Zhou, F. (2023). "Variance Control for Distributional Reinforcement Learning." ICML 2023, PMLR v202. https://proceedings.mlr.press/v202/kuang23a.html | ✅ QEMRL。Cornish-Fisher展開の使用を原典確認済み |
| [9] | Xu, S., Liu, Q., Hu, Y., Xu, M., Hao, J. (2023). "Decision-making models on perceptual uncertainty with distributional reinforcement learning." *Green Energy and Intelligent Transportation* 2(2): 100062. https://doi.org/10.1016/j.geits.2022.100062 | ⚠️ E-FQF。知覚不確実性下の自動運転という**応用論文内で定義されたFQFの効率化版**。独立のアルゴリズム論文ではない |

## **G3. リスク感応型分布型RL・スペクトルリスク尺度** 〔必要性：最重要の近接研究群。必須〕

| 番号 | 文献 | 判定・備考 |
| :--- | :--- | :--- |
| [15] | Lim, S. H., Malik, I. (2022). "Distributional Reinforcement Learning for Risk-Sensitive Policies." NeurIPS 2022. https://proceedings.neurips.cc/paper_files/paper/2022/hash/c88a2bd0e793550d0e885aa6e31ca277-Abstract-Conference.html | ✅ 静的/動的CVaRの区別と分布Bellman演算子の修正。※題名は「…Risk-Sensitive **Policies**」が正 |
| [16] | Bäuerle, N., Ott, J. (2011). "Markov Decision Processes with Average-Value-at-Risk Criteria." *Mathematical Methods of Operations Research* 74(3): 361–379. | ✅ ※旧報告書の「Bäuerle & Ottone (2018)」は確認不能のため本文献に置換 |
| [17] | Bäuerle, N., Glauner, A. (2022). "Markov Decision Processes with Recursive Risk Measures." *European Journal of Operational Research*. https://arxiv.org/abs/2010.07220 | ✅ ※旧報告書の「Bäuerle & Glass (2021)」は確認不能のため本文献に置換 |
| [18] | Moghimi, M., Ku, H. (2025). "Beyond CVaR: Leveraging Static Spectral Risk Measures for Enhanced Decision-Making in Distributional Reinforcement Learning." ICML 2025, PMLR v267. https://arxiv.org/abs/2501.02087 | ✅ **最重要の近接研究**。スペクトル重み μ̃ᵢ = φ(τᵢ₋₁) − φ(τᵢ) は本提案の歪み重みと数学的に同型。ただし重みは分位点の「値」に掛かるだけで、分数は一様固定・損失は標準quantile Huber（全文確認済み） |
| [19] | Moghimi, M., Ku, H. (2025). "Risk-sensitive Actor-Critic with Static Spectral Risk Measures for Online and Offline Reinforcement Learning." arXiv:2507.03900. https://arxiv.org/abs/2507.03900 | ⚠️ 査読なしプレプリント。[18]の拡張。※「Bastani 2025」という著者は存在しない（旧報告書の誤り） |
| [20] | Kim, D., Cho, T., Han, S., Chung, H., Lee, K., Oh, S. (2024). "Spectral-Risk Safe Reinforcement Learning with Convergence Guarantees." NeurIPS 2024. https://arxiv.org/abs/2405.18698 | ✅ SRCPO。双対変数と収束保証を原典確認済み。**オンライン**のリスク制約RL（旧報告書の「オフライン適用」記述は誤り） |
| [21] | Wu, Y., Li, W., Huang, W., Ho, C. P. (2026). "DRL-ORA: Distributional Reinforcement Learning with Online Epistemic Risk Adaptation." UAI 2026, PMLR v337. https://proceedings.mlr.press/v337/wu26e.html | ✅ エピステミック＋暗黙的偶然的不確実性の統合、オンライン調整。※同名略称の別論文（Yan et al., arXiv:2310.05179）に注意 |
| [22] | Zhang, D., Pan, L., Chen, R. T. Q., Courville, A., Bengio, Y. (2024). "Distributional GFlowNets with Quantile Flows." TMLR. https://arxiv.org/abs/2302.05793 | ✅ 歪みリスク尺度（CPW・Wang・CVaR）＋quantile matching＋GFlowNets。※著者はZhang & Pan等であり「Pan & Jain」は誤り（Pan & Jainは別の無関係論文の著者） |
| [45] | Coache, A., Jaimungal, S. (2024). "Robust Reinforcement Learning with Dynamic Distortion Risk Measures." arXiv:2409.10096. https://arxiv.org/abs/2409.10096 | ✅ 歪みリスク尺度の分位点表現から方策勾配を導出。**τは一様サンプリングで分数学習なし**。Wasserstein球内のロバスト化 |
| [46] | Ma, X., Chen, J., Xia, L., Yang, J., Zhao, Q., Zhou, Z. (2020/2023). "DSAC: Distributional Soft Actor-Critic for Risk-Sensitive Reinforcement Learning." arXiv:2004.14547（期刊版はJAIR 2023）. https://arxiv.org/abs/2004.14547 | ✅ FQF型分数提案を「モジュールとして差し替え可能」と明記した、リスク文脈でFQFを使う建築的先行例。歪み重み付き学習なし |

### G3-補. リスク感応型分布型RL（周辺・文脈参照）

| 文献 | 判定・備考 |
| :--- | :--- |
| Coache, A., Jaimungal, S., Cartea, Á. (2022). "Conditionally Elicitable Dynamic Risk Measures for Deep Reinforcement Learning." arXiv:2206.14666. https://arxiv.org/abs/2206.14666 | ✅ 動的スペクトル・リスク尺度のスコアリング関数ベース最適化 |
| Coache, A., Jaimungal, S. (2023). "Reinforcement Learning with Dynamic Convex Risk Measures." *Mathematical Finance*. https://doi.org/10.1111/mafi.12388 | ✅ 時間整合的な動的凸リスク尺度 |
| Cho, T., Han, S., Lee, H., Lee, K., Lee, J. (2023). "Pitfall of Optimism: Distributional Reinforcement Learning by Randomizing Risk Criterion." NeurIPS 2023. arXiv:2310.16546. https://arxiv.org/abs/2310.16546 | ✅ リスク基準のランダム化による探索改善 |
| Schubert, F., Eimer, T., Rosenhahn, B., Lindauer, M. (2021). "Automatic Risk Adaptation in Distributional Reinforcement Learning." ICML 2021 Workshop. arXiv:2106.06317. https://arxiv.org/abs/2106.06317 | ✅ 歪み測度のリスク水準の状態依存適応（分数適応ではない） |
| Yan, Z. et al. (2023). "DRL-ORA: Distributional RL with Online Risk Adaption." arXiv:2310.05179. https://arxiv.org/abs/2310.05179 | ⚠️ 文献[21]（UAI 2026）とは**著者が異なる同名略称の別論文**。引用時は要注意 |
| Rowland, M., Dadashi, R., Kumar, S., Munos, R., Bellemare, M. G., Dabney, W. (2019). "Statistics and Samples in Distributional Reinforcement Learning." ICML 2019. arXiv:1902.08102. https://arxiv.org/abs/1902.08102 | ✅ expectile版DRL（EDRL/ER-DQN）を含む統一理論。expectileは非対称重み付けとして歪み重みと概念的に隣接 |
| Jullien, S., Deffayet, R., Renders, J.-M., Groth, P., de Rijke, M. (2025). "Distributional Reinforcement Learning with Dual Expectile-Quantile Regression." UAI 2025, PMLR v286. arXiv:2305.16877. https://arxiv.org/abs/2305.16877 | ✅ **expectileとquantileを同時に学習**し分布Bellman演算子へ収束を証明。「分数を学習する」系の先行例。目的は非対称L2で歪み測度の最適量化ではない |
| Iwaki, R., Osogami, T. (2025). "Distorted Distributional Policy Evaluation for Offline Reinforcement Learning." ICONIP 2025. arXiv:2601.01917. https://arxiv.org/abs/2601.01917 | ⚠️ **「quantile distortion」という用語を別の意味（オフラインOPEの悲観化）で既に使用**。用語衝突に注意 |
| Prasad, H. (2026). "Auditing the Risk Claims of Distributional Reinforcement Learning." arXiv:2607.11607. https://arxiv.org/abs/2607.11607 | ✅ 固定一様グリッドの分位点criticのテール統計精度を監査。**本提案の動機を第三者的に支持する引用元** |
| Zhang, Z., Yang, M., Chen, R., Xie, S., Xiong, H. (2026). "Quantile Geometry Regularization for Distributional Reinforcement Learning." arXiv:2605.08182. https://arxiv.org/abs/2605.08182 | ⚠️ RQIQN。IQNベース＋Wasserstein DROの補正。FPN不使用・歪み重みなし。査読なしプレプリント |
| Shen, S. et al. (2023). "RiskQ: Risk-sensitive Multi-Agent Reinforcement Learning Value Factorization." NeurIPS 2023. arXiv:2311.01753. https://arxiv.org/abs/2311.01753 | ✅ MARLの価値分解。分数固定 |

## **G4. FQF・IQN系のリスク適用（モジュール利用・拡張候補）** 〔必要性：分類の整理に必要〕

| 文献 | 判定・備考 |
| :--- | :--- |
| Duan, J., Wang, W., Xiao, L., Gao, J., Li, S. E., et al. (2023/2025). "Distributional Soft Actor-Critic with Three Refinements" (DSAC-T). IEEE TPAMI. arXiv:2310.05858. https://arxiv.org/abs/2310.05858 | ✅ 値分布は**対角ガウスのパラメトリックモデル**で分位点表現を持たない（「リスク下での分数学習」の着想は現れない） |
| State-Fraction Coupled Quantile Network-Based DRL (2026). *Unmanned Systems*. https://doi.org/10.1142/s2301385028500495 | ⚠️ 状態とfractionの入力段結合。CVaR/歪みの記載なし（Crossref抄録確認） |
| Grün, F. et al. (2022)「Invariance to Quantile Selection」はG1の[14]に同じ | — |

## **G5. Tail-Safe・テールリスク重点化（τサンプリング設計）** 〔必要性：ベースライン対比の中核。必須〕

| 番号 | 文献 | 判定・備考 |
| :--- | :--- | :--- |
| [23] | Zhang, J. (2025). "Tail-Safe Hedging: Explainable Risk-Sensitive Reinforcement Learning with a White-Box CBF–QP Safety Layer in Arbitrage-Free Markets." arXiv:2510.04555. https://arxiv.org/abs/2510.04555 | ✅ IQNベース。「Tail-Coverage Controller」・temperature tilting・tail boosting・CBF-QP層を原典確認済み。**単著・査読なしプレプリント**。被引用0件（2026-09時点） |
| [24] | Malekzadeh, P., Poulos, Z., Chen, J., Wang, Z., Plataniotis, K. N. (2024). "EX-DRL: Hedging Against Heavy Losses with EXtreme Distributional Reinforcement Learning." arXiv:2408.12446. https://arxiv.org/abs/2408.12446 | ✅ GPDによる尾部補正を原典確認済み。分位点レベルは固定一様（τ_n = n/N） |
| Gao, S. et al. (2025). "Extreme Value Policy Optimization for Safe Reinforcement Learning" (EVO). ICML 2025. arXiv:2601.12008. https://arxiv.org/abs/2601.12008 | ✅ 極値理論によるextreme quantile最適化目的（安全RL）。分布RLの分数学習ではない |

## **G6. 金融応用：ヘッジング・ポートフォリオ（分位点型critic）** 〔必要性：応用面の先行研究と空白の実証。必須〕

| 番号 | 文献 | 判定・備考 |
| :--- | :--- | :--- |
| [25] | Buehler, H., Gonon, L., Teichmann, J., Wood, B. (2019). "Deep Hedging." *Quantitative Finance* 19(8): 1271–1291. https://doi.org/10.1080/14697688.2019.1571683 | ✅ 凸リスク尺度（CVaR等）下のヘッジ最適化。arXiv:1802.03042 |
| [26] | Bardou, O., Frikha, N., Pagès, G. (2016). "CVaR Hedging Using Quantization-Based Stochastic Approximation Algorithm." *Mathematical Finance* 26(1): 184–229. https://doi.org/10.1111/mafi.12049 | ✅ 量子化＋確率近似によるCVaRヘッジ。※旧報告書の「Pagès et al.」は第三著者のみの表記、「CVaR estimation with adaptive quantization」は題名混同のため修正 |
| [32] | Liu, Y., Li, J., Chen, Y., Du, L., Xu, J. (2025). "Deep Diffusion Reinforcement Learning for Options Hedging." Preprints.org 202507.0360. https://doi.org/10.20944/preprints202507.0360.v1 | ⚠️ 査読なしプレプリント。CVaR等のリスク尺度を目的関数に使う記述は確認されず |
| [51] | Cao, J., Chen, J., Farghadani, S., Hull, J., Poulos, Z., Wang, Z., Yuan, J. (2022). "Gamma and Vega Hedging Using Deep Distributional Reinforcement Learning." arXiv:2205.05614. https://arxiv.org/abs/2205.05614 | ✅ QR-D4PG。**全文確認で分位点レベルは固定一様グリッド**（学習されるのは値のみ） |
| [52] | Sharma, N., Chen, J., Noh, E., Hull, J., et al. (2024). "Hedging Beyond the Mean: A Distributional Reinforcement Learning Perspective for Hedging Portfolios with Structured Products." arXiv:2407.10903. https://arxiv.org/abs/2407.10903 | ✅ オートコーラブル・ノートのヘッジ。**分位点レベル固定一様**（全文確認済み） |
| Sharma, N., Chen, J., Noh, E., et al. (2024). "Hedging and Pricing Structured Products Featuring Multiple Underlying Assets." ACM ICAIF 2024. arXiv:2411.01121. https://arxiv.org/abs/2411.01121 | ✅ 3資産オートコーラブルのプライシング＋分布型RLヘッジ。95%/99% VaR・CVaRで左テール改善 |
| Ma, Y. (2025). "Deep Hedging to Manage Tail Risk." arXiv:2506.22611. https://arxiv.org/abs/2506.22611 | ✅ CVaR/ESの凸リスク最小化をNNでパラメータ化。分布型critic・分位点学習なし（ポリシー層でCVaR） |
| Zhang, S., Godin, F. (2026). "Insights on Time-consistent Deep Hedging under Elicitable Dynamic Risk Measures." arXiv:2609.02014. https://arxiv.org/abs/2609.02014 | ✅ スペクトルリスク尺度（CVaR含む）の条件付きelicitabilityで時間整合ヘッジング。critic配置学習なし |
| Wu, D., Jaimungal, S. (2023). "Robust Risk-Aware Option Hedging." *Quantitative Finance*. arXiv:2303.15216. https://arxiv.org/abs/2303.15216 | ✅ RDEU（歪み＋効用）を目的とするロバストpolicy gradient RLでバリアオプションをヘッジ。critic配置学習なし |
| Peng, X., Zhou, X., Xiao, B., Wu, Y. (2024). "A Risk Sensitive Contract-unified Reinforcement Learning Approach for Option Hedging." arXiv:2411.09659. https://arxiv.org/abs/2411.09659 | ✅ オプション売りのテールリスク最小化（契約統合RL）。分数学習なし |
| Hêche, F., Nigro, B., Barakat, O., Robert-Nicoud, S. (2025). "Risk-averse policies for natural gas futures trading using distributional reinforcement learning." arXiv:2501.04421. https://arxiv.org/abs/2501.04421 | ✅ C51/QR-DQN/IQNをCVaR目的で比較。**いずれも固定一様グリッド／一様サンプリング** |
| Özsoy, A. U. (2025). "Distributional Reinforcement Learning on Path-dependent Options." arXiv:2507.12657. https://arxiv.org/abs/2507.12657 | ✅ 経路依存オプションのリスクアウェア評価。分数学習なし |
| Zhao, L., Cai, L., Lu, W.-S. (2025). "Adaptive Nesterov Accelerated Distributional Deep Hedging for Efficient Volatility Risk Management." arXiv:2502.17777. https://arxiv.org/abs/2502.17777 | ✅ IQN型critic（τはサンプリング）＋Nesterov加速。配置学習なし |
| Oya, K. (2024). "Deep Hedging Bermudan Swaptions." arXiv:2411.10079. https://arxiv.org/abs/2411.10079 | ✅ 柔軟な凸リスク尺度で残余P&Lのダウンサイド制御 |
| Jin, B. (2022). "An intelligent algorithmic trading based on a risk-return reinforcement learning algorithm." arXiv:2208.10707. https://arxiv.org/abs/2208.10707 | ✅ 分位点回帰criticで累積収益分布を学習し、期待値＋VaRを最大化。固定グリッド |
| Noguer i Alonso, M. (2026). "Distributional Portfolio Optimization (DPO): A Unified Framework for Distributions over Weights, Returns, and Parameters." arXiv:2605.30464. https://arxiv.org/abs/2605.30464 | ✅ サーベイ/統合枠組み。ポジショニング節の参考 |
| Lucius, T., Koch, C., Starling, J., Zhu, J. (2025). "Deep Hedging with Reinforcement Learning: A Practical Framework for Option Risk Management." arXiv:2512.12420. https://arxiv.org/abs/2512.12420 | ✅ SPX/SPY実データでのSAC型エージェント。分布型criticなし |

### G6-補. Deep Hedging関連（無関係と判断した群・文脈確認用）

| 文献 | 判定・備考 |
| :--- | :--- |
| Buehler, H., Murray, P., Pakkanen, M. S., Wood, B. (2021). "Deep Hedging: Learning to Remove the Drift under Trading Frictions with Minimal Equivalent Near-Martingale Measures." arXiv:2111.07844. https://arxiv.org/abs/2111.07844 | ✅ ドリフト除去。テールリスク・分位点とは無関与。※Cao/Chen/Hullの実論文は arXiv:2103.16409（平均±標準偏差目的、無関係） |
| Horvath, B., Teichmann, J., Zuric, Z. (2021). "Deep Hedging under Rough Volatility." arXiv:2102.01962 | ✅ 無関係（ロバスト化は分位点配置に触れない） |
| He, X., Sutter, M., Gonon, L. (2025). "Distributional Adversarial Attacks and Training in Deep Hedging." NeurIPS 2025. arXiv:2508.14757 | ✅ Wasserstein ballによる敵対的ロバスト化。無関係 |
| Carbonneau, A., Godin, F. (2021). "Deep Equal Risk Pricing of Financial Derivatives..." arXiv:2102.12694 / "…Non-Translation Invariant Risk Measures" arXiv:2107.11340 | ✅ ERPの残余リスクに凸リスク尺度＋深層RL。周辺 |
| Cherrat, E. A., Raj, S., Kerenidis, I. et al. (2023). "Quantum Deep Hedging." *Quantum* 7: 1191. arXiv:2303.16585 | ✅ 量子RL。固定グリッドの分布型critic。周辺 |
| Poddar, M. (2026). "Uncertainty-Aware Deep Hedging." arXiv:2603.10137 | ✅ 深層アンサンブル＋CVaRブレンディング。分布型criticなし。周辺 |
| Queeney, J., Benosman, M. (2023). "Risk-Averse Model Uncertainty for Distributionally Robust Safe Reinforcement Learning." arXiv:2301.12593 | ✅ 歪みリスク尺度によるモデル不確実性扱い（safe RL・制御ドメイン）。周辺 |
| Théate, T., Ernst, D. (2022). "Risk-Sensitive Policy with Distributional Reinforcement Learning." arXiv:2212.14743 | ✅ 期待値＋テール関数へのQ関数置換。周辺 |
| Benavides, M. A. C. (2023). "Quantile Formulation Risk-Aware Reinforcement Learning for Goal-Based Portfolio Optimisation." University of Toronto MSc thesis. https://utoronto.scholaris.ca/handle/1807/130073 | ⚠️ 修論。RDEU下のゴール・ベース・ポートフォリオ。分数学習は示されず |

## **G7. 歪みリスク尺度・スペクトルリスク尺度の基礎理論** 〔必要性：数学的前提の原典。必須〕

| 番号 | 文献 | 判定・備考 |
| :--- | :--- | :--- |
| [33] | Yaari, M. E. (1987). "The Dual Theory of Choice under Risk." *Econometrica* 55(1): 95–115. https://doi.org/10.2307/1911158 | ✅ 歪み（双対）選好の公理論 |
| [34] | Wang, S. S. (1996). "Premium Calculation by Transforming the Layer Premium Density." *ASTIN Bulletin* 26(1): 71–92. | ⚠️ **Wang変換の標準出典として一次DBで確認できた版**。※通説の題名 "Premium Calculation by Transforming the Rank Size Distribution"（IME 19巻と流布）はCrossref・OpenAlex・doi.orgで確認不能 — 原本での最終確認を推奨 |
| [35] | Kusuoka, S. (2001). "On Law Invariant Coherent Risk Measures." *Advances in Mathematical Economics* 3: 83–95. https://doi.org/10.1007/978-4-431-67891-5_4 | ✅ 法則不変整合的リスク尺度の表現定理 |
| [36] | Acerbi, C. (2002). "Spectral Measures of Risk: A Coherent Representation of Subjective Risk Aversion." *Journal of Banking & Finance* 26(7): 1505–1518. https://doi.org/10.1016/S0378-4266(02)00281-9 | ✅ スペクトルリスク尺度（歪みの密度版） |
| [37] | Dhaene, J., Vanduffel, S., Goovaerts, M. J., Kaas, R., Tang, Q., Vyncke, D. (2006). "Risk Measures and Comonotonicity: A Review." *Stochastic Models* 22(4): 573–606. https://doi.org/10.1080/15326340600878016 | ✅ 歪みリスク尺度の分位点積分表現の標準レビュー |
| [30] | Balbás, A., Garrido, J., Mayoral, S. (2009). "Properties of Distortion Risk Measures." *Methodology and Computing in Applied Probability* 11(3): 385–399. https://doi.org/10.1007/s11009-008-9089-z | ✅ 歪みリスク尺度の公理的性質。※旧報告書の「Pichler (2015)」という帰属は誤り |
| [38] | Rockafellar, R. T., Uryasev, S. (2000). "Optimization of Conditional Value-at-Risk." *The Journal of Risk* 2(3): 21–41. https://doi.org/10.21314/jor.2000.038 | ✅ CVaR最適化の事実上の標準 |
| [39] | Rockafellar, R. T., Uryasev, S. (2002). "Conditional Value-at-Risk for General Loss Distributions." *Journal of Banking & Finance* 26(7): 1443–1471. https://doi.org/10.1016/S0378-4266(02)00271-6 | ✅ CVaRの分位点積分表現（一般分布版） |
| Pichler, A. (2015). "Premiums and Reserves, Adjusted by Distortions." *Scandinavian Actuarial Journal* 2015(4): 332–351. https://doi.org/10.1080/03461238.2013.830228 | ✅ 歪みプレミアム原理の双対表現。※旧報告書の「Pichler (2015)」の混同元と推定される実在論文 |

## **G8. 最適量子化・最適輸送とリスク尺度の交差** 〔必要性：理論的防衛線。必須〕

| 番号 | 文献 | 判定・備考 |
| :--- | :--- | :--- |
| [27] | Graf, S., Luschgy, H. (2000). *Foundations of Quantization for Probability Distributions*. Lecture Notes in Mathematics 1730. Springer. https://doi.org/10.1007/BFb0103945 | ✅ 1D最適量子化の基礎。※旧報告書のeBay・ScribdリンクをSpringer公式DOIに差し替え済み |
| [28] | Pichler, A., Xu, H. (2022). "Quantitative Stability Analysis for Minimax Distributionally Robust Risk Optimization." *Mathematical Programming* 191: 47–77（オンライン2018）. https://doi.org/10.1007/s10107-018-1347-4 | ✅ 歪みリスクを目的に含むDROのW1安定性。※旧記載題名から "risk" が欠落していたため修正 |
| [29] | Pflug, G. C., Pichler, A. (2014). *Multistage Stochastic Optimization*. Springer. https://doi.org/10.1007/978-3-319-08843-3 | ✅ 多段階確率最適化の安定性理論。※旧報告書の「Pflug & Pichler (2016)」はOJMO論文の誤帰属のため、実在業績として本書を追加 |
| [40] | Escobar & Pflug (2018). "The Distortion Principle for Insurance Pricing: Properties, Identification and Robustness." *Annals of Operations Research* 292(2): 771–794. https://doi.org/10.1007/s10479-018-3119-1 | ✅ 抄録に「曖昧性はWasserstein距離で測定」と明記。歪み汎関数のW1感度 |
| [41] | Bernard, C., Pesenti, S. M., Vanduffell, S. (2022). "Robust Distortion Risk Measures." arXiv:2205.08850. https://arxiv.org/abs/2205.08850 | ✅ Wasserstein ball内の歪みリスク尺度の鋭い評価 |
| [42] | Prashanth, L. A., Bhat, S. P. (2019). "A Wasserstein Distance Approach for Concentration of Empirical Risk Estimates." arXiv:1902.10709. https://arxiv.org/abs/1902.10709 | ⚠️ 歪みリスク尺度を含む推定誤差のW1集中評価。期刊版をCrossrefで確認できずarXiv版で引用 |
| [43] | Faugeras, O. P., Pagès, G. (2024). "Risk Quantization by Magnitude and Propensity." *Insurance: Mathematics and Economics* 116: 134–147. https://doi.org/10.1016/j.insmatheco.2024.02.005 | ✅ **リスク×最適量子化×Wassersteinの既存交差**（2点分布射影）。arXiv:2105.13002 |
| [44] | Bonalli, Bonnet & Pfeiffer (2025). "A Characterization of Law-Invariant and Coherent Risk Measures through Optimal Transport." arXiv:2512.19157. https://arxiv.org/abs/2512.19157 | ✅ OTによるリスク尺度の表現定理。**時期的・概念的に最も衝突しやすい最新理論 — 精読推奨** |
| [31] | Rahimian, H., Mehrotra, S. (2022). "Frameworks and Results in Distributionally Robust Optimization." *Open Journal of Mathematical Optimization* 3: Article 4. https://doi.org/10.5802/ojmo.15 | ✅ DROサーベイ。※旧報告書が「Pflug & Pichler (2016)」と誤帰属した論文の実際の著者 |
| Pesenti, S. M., Vanduffell, S. (2023). "Optimal Transport Divergences induced by Scoring Functions." arXiv:2311.12183. https://arxiv.org/abs/2311.12183 | ✅ スコア関数をOTのコストにしたダイバージェンス族。別系統の「リスク×OT」 |
| Pagès, G., Wilbertz, B. (2012). "Intrinsic Stationarity for Vector Quantization: Foundation of Dual Quantization." *SIAM J. Numer. Anal.* 50(2): 747–780. / "Optimal Delaunay and Voronoi Quantization Schemes for Pricing American Style Options." Springer Proc. Math. | ✅ dual quantization・American option量子化。※「distortion」は量子化誤差の意味でありリスク測度ではない。リスク加重によるタウ配置の先行例はこの流れに存在せず |
| Delattre, S., Graf, S., Luschgy, H., Pagès, G. (2004). "Quantization of probability distributions under norm-based distortion measures." *Statistics & Decisions* 22(4). | ✅ 「distortion measure」はノルム基盤の量子化誤差。リスク測度ではない |
| Bardou, O., Frikha, N., Pagès, G. (2009). "Computing VaR and CVaR using stochastic approximation and adaptive unconstrained importance sampling." *Monte Carlo Methods and Applications* 15(3). https://doi.org/10.1515/mcma.2009.011 | ✅ 「adaptive」はサンプリング側の適応化。※旧報告書の「CVaR estimation with adaptive quantization」という題名の論文は実在しない（本論文との混同） |
| Nakano, T. (2015). "Quasi-Monte Carlo methods for Choquet integrals." *J. Comput. Appl. Math.* 287: 63–66. | ✅ Choquet（歪み）積分の数値法。周辺 |
| Bonalli et al. 以外の関連： Egan, R. (2025). "Fixed-Length Lossy Compression with Distortion Risk Measure Constraints" / "Goal-Oriented 1-bit Quantization with Uncertain Distortion Measures." *IEEE Communications Letters*. | ✅ 情報理論での「量子化＋歪みリスク制約」。金融の分位点配置とは目的が異なるが言及可能 |

## **G9. 2025-2026年の新潮流（投稿直前に再検索すべき群）** 〔必要性：動向監視。プレプリント多数〕

| 文献 | 判定・備考 |
| :--- | :--- |
| Zhang et al. (2026). "Quantile Geometry Regularization for DRL" (RQIQN). arXiv:2605.08182 | ⚠️ G3-補に同じ（2026年最接近のRL側研究） |
| Zhang et al. (2025). "Distributionally Robust IQN (DRIQN)" (USV航行の摂動緩和). arXiv:2512.00030. https://arxiv.org/abs/2512.00030 | ✅ DRO＋IQN。部分関連 |
| "A Noise-Robust Elicit-to-Optimize Framework for Distortion Riskmetrics via Inverse RL." arXiv:2607.14373. https://arxiv.org/abs/2607.14373 | ✅ **最重要近接（全文検証済み）**。学習されるのは歪み関数自体（ベイズIRL）で、分位点レベルは固定・損失は標準ピンボール。歪み重みは読み出し時のみ |
| Prasad, H. (2026). "Auditing the Risk Claims of DRL." arXiv:2607.11607 | ✅ G3-補に同じ |
| Wang, K., Deng, Y., Lyu, Y., Redmond, S., Li, S. E. (2026). "A Spectral Revisit of the Distributional Bellman Operator under the Cramér Metric." arXiv:2603.12576. https://arxiv.org/abs/2603.12576 | ✅ 「spectral」はヒルベルト空間のスペクトルでリスク尺度ではない。無関係 |
| Shen, G. et al. (2025). "Deep Distributional Learning with Non-crossing Quantile Network." arXiv:2504.08215. https://arxiv.org/abs/2504.08215 | ✅ 分位点交差の回避が主題。リスク要素なし。無関係 |
| "Risk-Sensitive DRL for Robust Stratospheric Balloon Station-Keeping." ICIC 2026 | ✅ IQN上の指数スペクトル・リスク重み。「underlying learning objective を変更しない」と明記 |
| "Quantile-Coupled Flow Matching for DRL" (arXiv:2605.08515) / "Online Inference for Quantile TD" (arXiv:2608.12973) / "Occupancy-based Quantile Risk Control" (arXiv:2609.03104) / "Policy gradient for risk-sensitive DRL" (arXiv:2405.14749) / "Safe RLHF... Spectral Risk Control" (arXiv:2603.10938) / "Risk-Sensitive RL with Smoothed Quantile Objectives" (arXiv:2608.22227) / "Robust distortion risk measures with linear penalty" (arXiv:2503.15824) / "A Distribution Optimization Framework for Confidence Bounds of Risk Measures" (ICML 2023, arXiv:2306.07059) | ✅ いずれも全文/抄録検証の結果、歪み重み付きW1による分数配置学習を含まないため無関係と判断 |

## **G10. その他（確認不能・検証限界の記録）** 〔必要性：不在証明の限界明記用〕

| 文献・事項 | 状況 |
| :--- | :--- |
| Ståhlum, K.（NTNU修論、〜2021と想定。「歪みリスク×分布型RL」の適用研究） | ❌ Google Scholar・OpenAlex・一般検索の全てで確認不能。存在断定は不可。関連研究節に「確認できなかった」旨を一行記載推奨 |
| ProQuest博士論文（Xie 2026, "Data-Driven Decision Analytics..."） | ❌ "learned quantile levels" の唯一のヒット。内容検証不能 |
| 中国語文献（CNKI等「分布强化学习 风险 分位数」系） | ❌ 検索環境の制約（ボットブロック）で学術的該当は確認できず。存在保証なし |
| Feng et al. (2019, UAI) "Distributional RL via Maximum Mean Discrepancy"（旧報告書の「MMD-DRL」） | ❌ arXiv・S2・OpenAlexのいずれでも実在未確認 → [11] MMDQNに置換 |
| Wang, S. S. (1996) "Premium Calculation by Transforming the Rank Size Distribution"（通説の書誌） | ❌ 一次DBで確認不能（G7の[34]参照） |
| Frontiers in Artificial Intelligence (2026)「Portfolio management based on value distribution reinforcement learning algorithm」 | ⚠️ FQF被引用リストで発見。レート制限で詳細未確認（要確認） |
| Semantic Scholar上のFQF被引用の全数スイープ | ⚠️ APIレート制限（429）で未完了。キーワード検索で部分的に補完済み |

---

## **補遺：主要な「不在」検証結果の要約**

1. **"distortion-weighted Wasserstein" / "risk-weighted Wasserstein"** — arXiv・学術索引に事例ゼロ。
2. **"fraction proposal network" × CVaR/distortion/risk** — FQF本体以外に該当論文ゼロ（OpenReview全文検索含む）。
3. **"learnable/learned/adaptive quantile levels"** — 学習文脈での該当ゼロ（統計・計算グリッドのみ）。
4. **FQFの被引用192件の全走査** — 金融関連3件（いずれも分数固定）。FPN目的関数をリスク文脈で改変した研究ゼロ。
5. **Tail-Safe Hedging (arXiv:2510.04555) の被引用** — 0件（2026-09-08時点）。
6. **分位点レベル配置の最適化に応じたCVaR/テール近似誤差の理論** — 統計学・数理金融で先行を発見できず（本提案の理論的貢献として主張可能）。
7. **「歪み重み付き1-Wasserstein距離」という名前の定義されたオブジェクト** — OT・数理金融文献に存在せず（定式化自体が本提案の理論的貢献）。

## **補遺2：投稿直前の再検索推奨事項**

1. arXiv 2601-2612帯（2026年新着）およびOpenReview ICLR/NeurIPS 2026 の「risk-aware distributional RL quantile」「distortion RL quantile」系。
2. arXiv:2512.19157（Bonalli et al.）の精読 — 本提案の表現が含まれないことの最終確認。
3. Tail-Safe Hedging (arXiv:2510.04555) の被引用状況 — 今後引用が増える可能性が高い。
4. CNKI等の中国語学位論文およびProQuest博士論文（内容検証不能のまま残存）。
