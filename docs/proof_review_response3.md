# 定理4.1 3巡目査読（fable）への対応表 — theorem_41_v4.tex

> 対象査読: `fable_points3.md`（総合判定: **定理として成立（軽微な修正 1 件を要する）**）
> 改訂の軸: `fable_未コンパイル_v4.tex`（fable が査読に基づき作成した v4 草稿）。これを内容検証のうえ最小修正し `theorem_41_v4.tex` とした。
> 対応後のファイル: `theorem_41_v4.tex`（8ページ、Error 0・Overfull 0・未定義参照 0、platex+dvipdfmx、fitz 機械検証 PASS）
> 番号対応の注意: v4 では注意環境の実番号が 注意1.1（仮定の射程）・注意1.2（仮定 (H) の弱形・新設）・注意1.3（β=1）・注意1.4（証明の対象と実験の対応）・注意3.1（$\asymp$ から $\sim$ への強化・新設）であり、査読文書中の「注意1.2（β=1）」「注意1.4（新設）」という呼称とはずれがある（査読が v3 の番号で記述しているため）。以下は v4 の実番号で記す。

## 査読 §4「最終的な修正提案」への対応

| 優先 | 査読の修正提案 | v4 での対応 | 状態 |
| :--- | :--- | :--- | :--- |
| **必須** | 定義1.1 に「$\Finv$ は点 $\alpha$ で連続」を追加（部分区間の原子 $\Finv((M+\frac12)h)$ が $\alpha$ を超え得るため。$F$ が $\Finv(\alpha)$ の右近傍で狭義増加なら十分） | 定義1.1 に「$\Finv$ は点 $\alpha$ で（$(0,1)$ 上の関数として）連続とする」を追加し、十分条件（$F$ が $\Finv(\alpha)$ の右近傍で狭義増加）と使用箇所（補題3.1）を併記 | ✅ |
| **必須** | 補題3.1 部分区間: 原子が $\alpha$ を超える場合を含む評価 $\le h(\Finv(\alpha+\frac h2)-\Finv(\alpha-h))=o(h)$。一様評価では $\alpha+h\le\alpha_0$ を条件に $h^2(\Finv)'(\alpha/2)$ | 部分区間の項を新設し、(i) 固定 $\alpha$ では連続性から寄与 $\le h(\Finv(\alpha+\frac h2)-\Finv(\alpha-h))=o(h)=o(h^{2-\beta}\ell(h))$、(ii) 一様評価では $\alpha+h\le\alpha_0$ より $[Mh,Mh+h]\subset(0,\alpha_0]$ で平均値の定理により $\le h^2(\Finv)'(\alpha/2)$、の2系統で処理。$\alpha=0.05,N=27$ の反例的数値も明示 | ✅ |
| 推奨 | 補題3.1 一様評価の簡素化: 条件を「$h\le h_0$、$2h\le\alpha$、$\alpha+h\le\alpha_0$」に（下界は第1区間のみから）。下界和の $\int_{2h}^{(M+1)h}$ を $\int_{2h}^\alpha$ に。上界の $\Finv(\alpha_0)^+$ 吸収を明示 | 式\eqref{eq:unif-uniform} の条件を3条件に簡素化。下界和は $j=M$ で $h\varphi(Mh)\ge(\alpha-Mh)\varphi(Mh)\ge\int_{Mh}^\alpha\varphi$ として $\frac h4\int_{2h}^\alpha\varphi$ に修正（定義域外の積分記号を解消）。上界では $\Finv(\alpha)\le\Finv(\alpha_0)$ より $\frac h4\Finv(\alpha_0)^+=O(h)$ が $\alpha$ に依らず吸収されることを明示。旧条件 $\lvert\Finv(\alpha)\rvert\le\frac12\lvert\Finv(2h)\rvert$ は「正則部も同オーダーであることの十分条件」として証明中に補足 | ✅ |
| 推奨 | 注意1.1(iii): 定義1.1 の $\alpha$ 単調性（$\alpha_0$ で成立 ⇒ $\alpha\le\alpha_0$ で成立）を明記し、系1.1 の仮定を「$\alpha_0$ で成立」に | 注意1.1(iii) を追加（非増加性・$L^1$・$C^1$ は部分区間に遺伝、$(\Finv)'(\alpha)\ge(\Finv)'(\alpha_0)>0$）。系1.1 の仮定は「定義1.1 の仮定がある $\alpha_0\in(0,1)$ に対し $\beta\in(1,2)$ で成り立ち」と書換え。あわせて注意1.1(iv)（$\Finv\in L^1$ は式(2)と $\beta<2$ から従う冗長性の注記）も追加 | ✅ |
| 推奨 | 系1.1 証明の簡素化（Potter による条件充足の議論は補足に） | 証明を「$N\alpha_N\to\infty$ より $2h\le\alpha_N$、$\alpha_N\downarrow0$ より $\alpha_N+h\le\alpha_0$、注意1.1(iii) により定義1.1 が $\alpha_N$ で成立 → 一様評価\eqref{eq:unif-uniform} を適用」に書換え。旧条件の Potter 議論は「ここでは不要」と明記した補足に降格 | ✅ |
| 推奨 | 注意（β=1）: 第1区間が $h\ell(h)$、$\ell_1$ は正則部から生じる機序を明記 | 注意1.3 に「$\beta=1$ では第1区間は $\int_0^{h/2}s(\Finv)'(s)ds=\int_0^{h/2}\ell(s)ds\sim\frac h2\ell(h)$（Fubini＋Karamata $p=0$）より $I_0\asymp h\ell(h)=o(h\ell_1(h))$ にとどまり、主要項 $\asymp h\ell_1(h)$ は正則部の Darboux 型評価から生じる」ことを明示し、「$\beta>1$ では誤差が特異点に集中、$\beta=1$ では対数的に蓄積」の定性的対比を一文で明記 | ✅ |
| 推奨 | 補題3.2: 割当区間の端点は測度零、構成分布の分位点関数が a.e. 一致、$N'\le N$ | 達成証明を「最適コードブック $Q^\ast=\{q_1<\dots<q_{N'}\}$（$N'\le N$）、Voronoi 中点による最近傍の単調性、各添字の逆像は（端点を除いて）区間、端点の帰属は Lebesgue 測度零の差、構成分布の分位点関数は $(0,\alpha)$ 上ほとんどいたるところ $\Fhinv=q_{i(\tau)}$」に精密化 | ✅ |
| 推奨 | 補題3.3(i): 値域 $(\Finv(0+),\Finv(\alpha)]$、Galois 性の明示 | (i) の証明で値域を $(x_0,\Finv(\alpha)]$（$x_0:=\Finv(0+)$、$\beta>1$ または $\beta=1$ で $\ell_1\to\infty$ のとき $x_0=-\infty$）とし、一般化逆の性質 $\Finv(\tau)\le x\iff\tau\le F(x)$ を明示 | ✅ |
| 推奨 | 補題2.2・2.3: 漸近代入の正当化一文、「部分積分」→ Fubini | 補題2.2 に「$\int_\tau^\alpha=\int_\tau^{s_0}+\int_{s_0}^\alpha$ と分けて第2項は有限定数、$\varepsilon$ 任意より発散項の漸近比較が正当化される」の趣旨を追加。補題2.3 の証明は「積分順序を交換（Fubini）」に修正 | ✅ |
| 任意 | 注意3.1（新設）: $\asymp$ を $\sim$（明示定数 $K_\beta$）へ強化する方針の概略 | 注意3.1 を新設。$\tau=hu$ のスケールで $\Iunif\sim K_\beta h^{2-\beta}\ell(h)$（$K_\beta=\frac1{\beta-1}\sum_{i\ge0}\int_i^{i+1}\lvert u^{-(\beta-1)}-(i+\frac12)^{-(\beta-1)}\rvert du<\infty$）が期待され、定理1.1 が $\Eunif/\Eopt\sim K_\beta C(\alpha)N^{\beta-1}\ell(1/N)$ と明示定数付きで述べられること、詳細は今後の課題であることを記述 | ✅（概略のみ） |
| 任意 | 注意（新設）: (H) の弱形 (H′) の位置づけ | 注意1.2 を新設。系1.1 の結論は $\asymp$ なので実際に必要なのは (H′)（$\alpha$ 一様な両側 $\asymp$: $0<c_\ast\le 4N\eN(X_\alpha)/(\int f_\alpha^{1/2})^2\le C_\ast<\infty$）であること、$\tau$ 空間の明示的配置（各区間で $\int\sqrt{(\Finv)'}$ が等しい区切り）＋補題2.3 型下界＋Cauchy–Schwarz＋Potter で証明可能と期待されること、証明は今後の課題であることを記述 | ✅（概略のみ） |

## v4 作成時に追加で対応した点（fable 草稿 `fable_未コンパイル_v4.tex` の検証で発見）

| 問題 | 対応 | 状態 |
| :--- | :--- | :--- |
| 補題3.1 証明の下界連鎖で「$\sum e_i\;=\;\frac h4\sum h\varphi(jh)$」となっていた（両側評価 $\frac{h^2}4\varphi(\tau_{i+1})\le e_i$ からは $\ge$ が正しい。v3 では $\ge$ だったものが草稿で誤って $=$ に） | $=$ を $\ge$ に修正してからコンパイル | ✅ |
| ヘッダコメントの査読参照が「3巡目査読の指摘に対応」とファイル名なし | `fable_points3.md §4` への参照に修正 | ✅ |

## 検算による確認（v4 の新規・変更箇所をローカルで再検証）

- **定義1.1 の連続性と部分区間の評価**: $\tau\in[Mh,\alpha]\subset[\alpha-h,\alpha]$、原子 $q=\Finv(Mh+\frac h2)\le\Finv(\alpha+\frac h2)$ より $\lvert\Finv(\tau)-q\rvert\le\Finv(\alpha+\frac h2)-\Finv(\alpha-h)$。点 $\alpha$ での（両側）連続性から $o(1)$、寄与は $\le h\cdot o(1)=o(h)$。$\beta>1$ で $h^{2-\beta}\ell(h)/h=h^{1-\beta}\ell(h)\to\infty$ より $o(h)=o(h^{2-\beta}\ell(h))$。整合。一様評価側は $\alpha+h\le\alpha_0$ で $[Mh,Mh+h]\subset(0,\alpha_0]$、$Mh\ge\alpha-h\ge\alpha/2$（$2h\le\alpha$）より $\varphi(Mh)\le\varphi(\alpha/2)$。整合。
- **下界和の修正**: $j=2,\dots,M-1$ で $h\varphi(jh)\ge\int_{jh}^{(j+1)h}\varphi$、$j=M$ で $h\varphi(Mh)\ge(\alpha-Mh)\varphi(Mh)\ge\int_{Mh}^\alpha\varphi$（$\varphi$ 非増加、$\alpha-Mh<h$）。合計して $\sum_{j=2}^M h\varphi(jh)\ge\int_{2h}^\alpha\varphi$。すべての積分区間が $(0,\alpha]$ に収まり、査読 3-1(b) の指摘どおり。
- **注意1.3（β=1）の機序**: $\int_0^{h/2}(\Finv(h/2)-\Finv(\tau))d\tau=\int_0^{h/2}s(\Finv)'(s)ds$（Fubini）は恒等式として正しく、$\beta=1$ で $(\Finv)'(s)\sim s^{-1}\ell(s)$ より $\int_0^{h/2}\ell(s)ds\sim\frac h2\ell(h)$（Karamata $p=0$）。正則部 $\frac h4(\Finv(\alpha)-\Finv(2h))\sim\frac h4\ell_1(h)$ が主要項で $h\ell(h)=o(h\ell_1(h))$（$\ell_1/\ell\to\infty$、BGT Prop. 1.5.9a）。整合。
- **注意3.1 の $K_\beta$**: スケール $\tau=hu$ で $\Finv(hu)/(h^{1-\beta}\ell(h))\to-\frac{u^{-(\beta-1)}}{\beta-1}$（補題2.2）、原子は $-\frac{(i+1/2)^{-(\beta-1)}}{\beta-1}$ に対応。$i$ 番目の区間の寄与は $\lvert u^{-(\beta-1)}-(i+\frac12)^{-(\beta-1)}\rvert$ の振動分で $O(i^{-\beta})$、$\beta>1$ で総和可能。概略として整合（厳密化は今後の課題と明記済み）。
- **注意1.2 の (H′)**: 系1.1 の証明で歪み最適側に (H) の代わりに (H′) を使うと $\Eopt\asymp\frac1{\alpha_N N}(\int_0^{\alpha_N}\sqrt{(\Finv)'})^2\asymp\frac{\alpha_N^{1-\beta}\ell(\alpha_N)}N$ となり、比の $\asymp$ 評価（式(6)）はそのまま従う。「(H′) で十分」の主張は正しい。
- **例1.2（厳密冪裾）**: $\eN(aX)=a\eN(X)$、$\int f_{aX}^{1/2}=a^{1/2}\int f_X^{1/2}$ より比 $4N\eN(X_\alpha)/(\int f_\alpha^{1/2})^2$ は $\alpha$ 非依存。(H) は $X_1'$ 単独の Zador 漸近に帰着。整合（査読 §3-5 も「正しい」）。

## 機械検証の結果（2026-09-22）

- `platex theorem_41_v4.tex` ×2 + `dvipdfmx theorem_41_v4.dvi`: **Error 0、Overfull 0、Underfull 0、Warning 0、未定義参照 0（終了コードすべて 0。ログ: `theorem_41_v4.log`／バックアップ `theorem_41_v4_platex.log`）**
- fitz による PDF 検証（8ページ）: `??` 0件。環境番号 定義1.1／定理1.1／命題1.1／系1.1／注意1.1〜1.4／例1.1,1.2／補題2.1〜2.4／補題3.1〜3.4／注意3.1 をすべて確認。出現順序「命題1.1 → 系1.1 → §2 見出し」で構造を確認。仮定 (H)・(H′)・$K_\beta$・点 $\alpha$ での連続性の記述が PDF 上に存在することを確認。

## 残る論点（卒論での注意）

- **査読の総合判定は「定理として成立」**。3-1(a) の一行修正（定義1.1 への連続性追加）は v4 で反映済みであり、定理1.1・命題1.1・補題群は卒論に「定理」として掲載可能な水準に到達した（査読 §5 の結論）。
- **今後の課題（v4 で明記済み）**: ①一般の緩変動 $\ell$ に対する仮定 (H)／(H′) の証明（注意1.2、例1.2 は厳密冪裾のみ）、②$\asymp$ の $\sim$ 強化（明示定数 $K_\beta$、注意3.1。時間があれば $K_{4/3}$ の数値検証まで進めると貢献が一段上がるとの査読助言）、③符号付き CVaR 誤差の二次精度（実験の $N^{-1.86}$）の理論化。
- Graf–Luschgy Theorem 6.2 の正確な仮定・定数は原書（LNM 1730）で最終確認すること（1・2巡目からの継続事項。査読 §2-8 で $Q_1([0,1])=1/4$、$\lVert f\rVert_{1/2}=(\int f^{1/2})^2$ の整合は確認済み）。
- 定理はあくまで**上界汎関数の配置間比較**であり、実 CVaR 誤差の改善を直接示すものではない点、および実験の M2（正則化 $\lambda=0.05$）と定理の対象（$\lambda=0$）の差は注意1.4 で明記済み。
