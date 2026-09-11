# slides_outline.md — 中間発表スライド構成アウトライン

表題：歪み関数重み付き1-Wasserstein距離に基づくquantile fraction学習とCVaR推定誤差の低減
副題：卒業研究 中間発表 ／ 発表者：【氏名】 ／ 所属：【研究室名】 ／ 指導教員：【指導教員名】 ／ 2026年10月2日
発表：本編5分（10枚・各30秒）＋質疑3分（Appendix 7枚）
デザイン：Beamer 16:9・Luebeck／orchid・ゴシック体・block／alertblock／exampleblock

## 本編

| # | 時間 | フレームタイトル | 主要構成ブロック・数式・図 |
|---|------|------------------|----------------------------|
| 1 | 0:00–0:30 | タイトル | titlepage |
| 2 | 0:30–1:00 | 研究背景：期待値最大化の限界と分布型強化学習 | block: $Z^\pi=\sum\gamma^tR_t$, $Q^\pi=\mathbb{E}[Z^\pi]$ ／ alertblock: 稀な極端損失は期待値に埋没 ／ block: 分布ベルマン作用素 $\mathcal{T}^\pi$, 分位点関数 $F^{-1}(\tau)$ の有限原子近似 |
| 3 | 1:00–1:30 | 目標リスク尺度：CVaR | block: $\mathrm{CVaR}_\alpha(Z)=\frac1\alpha\int_0^\alpha F^{-1}(\tau)d\tau=\int_0^1F^{-1}g'\,d\tau$, $g(\tau)=\min(\tau/\alpha,1)$ ／ TikZ: 密度と下側裾 ／ alertblock: 精度は $[0,\alpha]$ 上でのみ決まる |
| 4 | 1:30–2:00 | 既存手法：FQF とその課題 | block: quantile fraction の定義, $W_1$, FQF勾配 $2F^{-1}(\tau_i)-F^{-1}(\hat\tau_i)-F^{-1}(\hat\tau_{i-1})$ ／ 図: fig1_fqf_overview.png ／ alertblock: 下側裾に約 $\alpha N=0.8$ 個 |
| 5 | 2:00–2:30 | 理論的着想：CVaR誤差上界と歪み重み付き目的関数 | exampleblock: 命題 $|\mathrm{CVaR}_\alpha(Z)-\mathrm{CVaR}_\alpha(\hat Z)|\le W_1(g_\#Z,g_\#\hat Z)=L_g$ ／ block: $W_1\to L_g$ 置換 ／ TikZ: 一様 vs 歪み最適配置 |
| 6 | 2:30–3:00 | 提案定理：quantile fraction に関する勾配の閉形式 | exampleblock: $\partial L_g/\partial\tau_i=g'(\tau_i)[2F^{-1}(\tau_i)-F^{-1}(\hat\tau_i)-F^{-1}(\hat\tau_{i-1})]$, $g$-中央値原子 ／ block: 含意（$1/\alpha$ 倍・裾外 0）／ block: アルゴリズム4手順 |
| 7 | 3:00–3:30 | 先行研究との位置づけ | 比較表（IQN／Beyond CVaR／Tail-Safe／FQF／本研究）／ exampleblock: 損失側で配置自体を最適化する新たなアプローチ |
| 8 | 3:30–4:00 | 実験A：1次元最適量子化デモ | 図: fig3_placement.png, fig4_error.png ／ exampleblock: $R=97.9/52.4/39.6$, PASS, 13/15 個が下側裾, 16点 $\approx$ 695点 |
| 9 | 4:00–4:30 | 実験B：RiskyChain-v0 | 図: figB2_estimation_ja.png ／ 表: M-est MAE FQF $7.02\pm0.14$ / 提案B1g $\mathbf{0.96\pm0.51}$ / IQN $\mathbf{0.36\pm0.05}$ / B2p $3.42\pm1.38$, 裾数 $14.06\pm0.11$, 閾値最良 $k^*=0$（1.0000） ／ alertblock: IQN 最良の客観的限定とMC標準誤差の留意点 |
| 10 | 4:30–5:00 | まとめと今後の展望 | exampleblock: 理論・実験A・実験B の達成事項 ／ block: デルタヘッジ環境, 理論の厳密化, 初期化改善 |

## Appendix

| # | フレームタイトル | 内容 |
|---|------------------|------|
| A1 | quantile fraction に関する勾配の導出 | 目的関数の分解, ライプニッツ則, $g$-中央値の一階条件による包絡項消去, 境界項の相殺, 裾外勾配ゼロの注意 |
| A2 | 歪み分布の1次元最適量子化理論 | Graf & Luschgy (2000): 最適原子＝重み付き中央値, 最適区切り＝Voronoi 中点, $e_{N,1}\asymp N^{-1}$ |
| A3 | 実験Aの詳細設定 | D1〜D3 の定義, 数値積分, マルチスタート最適化, N-equivalence, $\alpha N\ge2$ で最小 $R=42.3$, 傾き約 $-1.8$ |
| A4 | 想定質問 Q1〜Q3 | IQN との違い／Beyond CVaR との違い／重み付けの自明性 |
| A5 | 想定質問 Q4〜Q5 | CPU 実験規模／IQN 優位の理由と対策 |
| A6 | 実験B 補足 | M-pol CVaR: IQN $1.01\pm0.01$ ＞ 提案B1g $0.70\pm0.43$ ＞ B1 $-1.15\pm2.38$ ＞ B0 $-10.79\pm0.00$（閾値方策クラス内最良 $k^*=0$: $1.0000$） |
| A7 | 参考文献 | FQF, IQN, Beyond CVaR, Tail-Safe, Graf & Luschgy, Rockafellar & Uryasev |

## 画像ファイル（実在4点のみ）
- fig1_fqf_overview.png（本編4）
- fig3_placement.png（本編8）
- fig4_error.png（本編8）
- fig5_curve.png（本編9）
