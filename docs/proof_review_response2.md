# 定理4.1 2巡目査読（fable）への対応表 — theorem_41_v3.tex

> 対象査読: `fable_points2.md`（総合判定: 条件付きで成立 — §4 の 1〜4 を反映すれば「定理として成立」）
> 改訂の軸: `fable_未コンパイル.tex`（fable が査読に基づき作成した v3 草稿）。これを内容検証のうえ最小修正し `theorem_41_v3.tex` とした。
> 対応後のファイル: `theorem_41_v3.tex`（7ページ、Error 0・Overfull 0・未定義参照 0、platex+dvipdfmx、fitz 機械検証 PASS）

## 査読 §4「最終的な修正提案」への対応（優先度順 1〜9）

| # | 査読の修正提案 | v3 での対応 | 状態 |
| :--- | :--- | :--- | :--- |
| 1 | **[必須] tex 構造の修復**: 命題環境が §2 全体を包含していた破損を直し、命題本文を §1 内で閉じる。導入文を §1 末尾へ。編集履歴コメント削除 | 命題1.1（`prop:alpha`）は §1 内で `\begin`〜`\end` が完結し、仮定 (H)・系1.1（`cor:joint`）・例1.2（`ex:powertail`）・注意1.2（β=1）・注意1.3（`rem:scope`）・証明構成の導入文がすべて §1 内に配置。§2（補助補題）はその後に開始。補題2.2 の「査読指摘により符号を修正」等の編集履歴は削除済み（fitz で出現順序を機械確認: 命題1.1 → 系1.1 → §2 見出し） | ✅ |
| 2 | **[必須] $C(\alpha)$ の修正**: $C(\alpha)=4/(\int_0^\alpha\sqrt{(\Finv)'})^2$。命題1.3(i) を $C(\alpha)\sim4(1-\beta/2)^2\alpha^{-(2-\beta)}\ell(\alpha)^{-1}$ に | 定理1.1（式(4)）で $C(\alpha):=4/(\int_0^\alpha\sqrt{(\Finv)'(\tau)}d\tau)^2$ に修正（分子の余分な $\alpha$ を除去）。命題1.1（式(5)）で $(\int_0^\alpha\sqrt{(\Finv)'})^2\sim\alpha^{2-\beta}\ell(\alpha)/(1-\beta/2)^2$ と $C(\alpha)\sim4(1-\beta/2)^2\alpha^{-(2-\beta)}\ell(\alpha)^{-1}$ を**定数付き**で併記（fitz で式(4)(5) の内容を確認済み） | ✅ |
| 3 | **[必須] 命題1.3(ii) の再定式化**: 仮定 (H)（Zador 漸近の $\alpha$ 一様性）を明示した「系」に降格し、厳密冪裾で (H) が等式で成り立つことを例示。$N^{o(1)}$ 表記を $\asymp N^{\beta-1}\ell(1/N)\alpha^{-(2-\beta)}\ell(\alpha)^{-1}$ に | §1 に**仮定 (H)**（$\sup_{\alpha\in(0,\alpha_0]}\lvert 4N\,e_{N,1}(X_\alpha)/(\int f_\alpha^{1/2})^2-1\rvert\to0$）を明示し、共同極限を**系1.1**（`cor:joint`）として独立させた。式(6) は $\asymp N^{\beta-1}\ell(1/N)\alpha_N^{-(2-\beta)}\ell(\alpha_N)^{-1}$（$N^{o(1)}$ 表記を廃止）。例1.2 で厳密冪裾 $\Finv(\tau)=-c\tau^{-(\beta-1)}$ のスケール不変性（$X_\alpha\overset{d}{=}\alpha^{-(\beta-1)}X_1'$）から (H) が $X_1'$ 単独の Zador 漸近に帰着することを例示し、一般の $\ell$ に対する (H) は今後の課題と明記 | ✅ |
| 4 | **[必須] 注意1.4 の regime 統一**: 固定 $\alpha$ では $E_{\mathrm{opt}}\sim\frac1{4\alpha N}(\int_0^\alpha\sqrt{(\Finv)'})^2$、比 $\asymp\ell_1(1/N)/(\int_0^\alpha\sqrt{(\Finv)'})^2$。「$\ell(\alpha)/N$」は $\alpha\downarrow0$ の付記に | 注意1.2（β=1 の扱い）を固定 $\alpha$ の式 $E_{\mathrm{unif}}\asymp\frac1\alpha\frac{\ell_1(1/N)}{N}$、$E_{\mathrm{opt}}\sim\frac1{4\alpha N}(\int_0^\alpha\sqrt{(\Finv)'})^2$、比 $\asymp4\ell_1(1/N)/(\int_0^\alpha\sqrt{(\Finv)'})^2$ で統一。$\alpha\downarrow0$ の評価（$(\int_0^\alpha\sqrt{(\Finv)'})^2\sim4\alpha\ell(\alpha)$、$C(\alpha)\sim1/(\alpha\ell(\alpha))$）は末尾の付記に分離 | ✅ |
| 5 | **[強く推奨] 同一視の補題を追加**: $I^{\mathrm{opt}}_\alpha=\alpha\,e_{N,1}(X)$ の証明。Zador 条件を定義1.1 から導出し定理の仮定から外す。Graf–Luschgy Theorem 6.2 明記 | **補題3.2（`lem:identify`）新設**: (a) 任意の $N$ 原子分布で $I_\alpha\ge\int_0^\alpha\min_q\lvert\Finv-q\rvert d\tau=\alpha\,\E\min_q\lvert X_\alpha-q\rvert\ge\alpha\,e_{N,1}(X_\alpha)$、(b) 最適コードブックの最近傍割当が $\tau$ 空間の区間になることを利用し達成例を構成、の2段で等式を証明。**補題3.3（`lem:zador-cond`）新設**: (i) 絶対連続性、(ii) $\E\lvert X_\alpha\rvert^{1+\delta}<\infty$（$0<\delta<(2-\beta)/(\beta-1)$）、(iii) $\int f_\alpha^{1/2}=\alpha^{-1/2}\int_0^\alpha\sqrt{(\Finv)'}<\infty$ を定義1.1 から導出。定理1.1 の仮定から外部 Zador 条件を削除し、未定義記号 $\mathcal{D}_g$ も廃止。補題2.4 の証明で Graf–Luschgy (2000, LNM 1730) **Theorem 6.2**（$d=1,r=1$、$Q_1([0,1])=1/4$）を明記 | ✅ |

| 6 | **[推奨] 補題3.1 の細部**: 正則セルの添字を $i=1,\dots,\lfloor\alpha N\rfloor-1$ に、部分セルを $h^2(\Finv)'(\tau_i)=O_\alpha(h^2)$ に、下界の $(1-\varepsilon)$ を明示、$\asymp$ 定数の $\alpha$ 非依存性を明記 | 補題3.1（`lem:unif`）で $M=\lfloor\alpha N\rfloor$、正則区間は $i=1,\dots,M-1$、部分区間 $[Mh,\alpha]$ の寄与は $\le h^2(\Finv)'(\alpha/2)=O_\alpha(h^2)$（原子が部分区間外に出得る点も処理）。第1区間下界は $(1-\varepsilon)$ 因子を明示した二段評価に書換。さらに「$\asymp$ の定数は $\alpha$ に依存しない」ことを条件 $\lvert\Finv(\alpha)\rvert\le\frac12\lvert\Finv(2h)\rvert$ 付きの一様評価 $c_1h^{2-\beta}\ell(h)\le I^{\mathrm{unif}}_\alpha\le c_2h^{2-\beta}\ell(h)+h^2(\Finv)'(\alpha/2)$ として明記（系1.1 の証明で使用） | ✅ |
| 7 | **[推奨] 仮定の整備**: 補題2.3 に $C^1$、定義1.1 に $(\Finv)'(\alpha)>0$、非増加性が実質 $\alpha\le1/2$ を課すことの注記 | 定義1.1 に「$(\Finv)'$ は $(0,\alpha]$ で非増加かつ $(\Finv)'(\alpha)>0$」を追加（非増加性と合わせて $(\Finv)'>0$ が $(0,\alpha]$ 全体に成立）。注意1.1(i) で対称単峰分布では実質 $\alpha\le1/2$ を要求することを注記。補題2.3（中点則）の仮定を「$\Finv\in C^1[a,a+w]$ が非減少」と明記 | ✅ |
| 8 | **[推奨] 文献**: Karamata は BGT Prop. 1.5.8/1.5.10、Potter は BGT Thm 1.5.6、$\beta=1$ の $\ell_1/\ell\to\infty$ は BGT Prop. 1.5.9a | §2 冒頭で Bingham–Goldie–Teugels (1987) を BGT として導入し、補題2.1 に Prop. 1.5.8/1.5.10、証明内の一様収束定理に Thm 1.2.1、Potter の上界に Thm 1.5.6、補題2.2 の $\beta=1$ 系に Prop. 1.5.9a をそれぞれ明記。補題2.1 (1.2) 側の証明は Potter が有効な原点近傍と $[x_0,a]$ 上の $O(1)$ 項に分離する形に修正 | ✅ |
| 9 | **[整合] `proof_notes.md` の更新**: §6 表の「$\Omega(1/\alpha)$ 証明完成」「$\beta=1$ で $\Theta(1/\alpha)$」を撤回済みと明記 | `proof_notes.md` §6 の冒頭に 2026-09-22 追記（v2 で撤回済み・現行の正本は v3）を挿入し、該当2行を「v2 で撤回」と理由付きで更新。表は v1 時点の作業記録として残す旨を明記 | ✅ |

## v3 作成時に追加で対応した点（fable 草稿 `fable_未コンパイル.tex` の検証で発見）

| 問題 | 対応 | 状態 |
| :--- | :--- | :--- |
| プリアンブルで `\newcommand{\Finv}` が `Command \Finv already defined` エラー（v2 にあった `\expandafter\let\csname Finv\endcsname\undefined` の欠落） | 当該行を復活させ再コンパイル。Error 0 を確認 | ✅ |
| ヘッダコメントの参照ファイル名誤り（`review/P9v2_理論証明再査読_結果.md`） | `fable_points2.md §4` への参照に修正 | ✅ |
| 仮定 (H) の導入文が文末コロン「：」 | 用語集ルール（コロン文中文末排除）に従い「．」に修正 | ✅ |

## 検算による確認（v3 の数式をローカルで再検証）

- **定理1.1 の証明**: 補題3.1（$E_{\mathrm{unif}}\asymp\frac1\alpha N^{-(2-\beta)}\ell(1/N)$）と補題3.4（$E_{\mathrm{opt}}\sim\frac1{4\alpha N}(\int_0^\alpha\sqrt{(\Finv)'})^2$）の比は $\frac{4N^{\beta-1}\ell(1/N)}{(\int_0^\alpha\sqrt{(\Finv)'})^2}=C(\alpha)N^{\beta-1}\ell(1/N)$ となり、修正後の $C(\alpha)$ と厳密に一致。
- **命題1.1**: Karamata（$p=-\beta/2>-1$）で $\int_0^\alpha\tau^{-\beta/2}\ell^{1/2}d\tau\sim\frac{\alpha^{1-\beta/2}}{1-\beta/2}\ell(\alpha)^{1/2}$、2乗して式(5) 第1式、$C(\alpha)$ に代入して第2式。整合。
- **系1.1**: 歪み最適側は (H)＋補題3.3(iii)＋命題1.1 より $E_{\mathrm{opt}}=(1+o(1))\frac{\alpha_N^{1-\beta}\ell(\alpha_N)}{4(1-\beta/2)^2N}$。一様側は $N\alpha_N\to\infty$ と Potter から条件 $\lvert\Finv(\alpha_N)\rvert\le\frac12\lvert\Finv(2/N)\rvert$ が満たされ、補題3.1 の一様評価が適用できる。付加項 $h^2(\Finv)'(\alpha_N/2)=o(h^{2-\beta}\ell(h))$（Potter）も確認。比は式(6) と一致。
- **補題3.2**: 下界は $\Fhinv(\tau)\in Q$ から逐点評価で自明。達成は最近傍写像の単調性（$\Finv$ 非減少）から $\tau$ 空間の割当が区間 $[\tau_{i-1},\tau_i)$ となり、質量 $\tau_i-\tau_{i-1}$（最後は $1-\tau_{N-1}$）を持つ $\hat Z_N^*$ で下界を達成。等式として正しい。
- **補題3.1**: 第1区間の下界 $[0,h/4]$ 上の逐点評価→固定比区間での一様収束定理、上界 Karamata、正則部の Darboux 上下（下端は $\frac h4(\Finv(\alpha)-\Finv(2h))$、条件付きで $\frac h8\lvert\Finv(2h)\rvert$ 以上）、端点項 $h^2(\Finv)'(h)\asymp h^{2-\beta}\ell(h)$ は主項と同オーダー。すべて整合。

## 機械検証の結果（2026-09-22）

- `platex theorem_41_v3.tex` ×2 + `dvipdfmx theorem_41_v3.dvi`: **Error 0、Overfull 0、Underfull 0、Warning 0、未定義参照 0（ログ: `theorem_41_v3.log`／バックアップ `theorem_41_v3_platex.log`）**
- fitz による PDF 検証（7ページ）: `??` 0件。環境番号 定義1.1／定理1.1／命題1.1／系1.1／注意1.1〜1.3／例1.1,1.2／補題2.1〜2.4／補題3.1〜3.4 をすべて確認。出現順序「命題1.1 → 系1.1 → §2 見出し」で構造破損（査読 §3-2）の解消を確認。式(4)=定理1.1（修正後の $C(\alpha)$）、式(5)=$C(\alpha)$ の $\alpha\downarrow0$ 漸近（査読の式 (1.5) 相当）、式(6)=共同極限（査読の式 (1.6) 相当）を本文抽出で突合済み。

## 残る論点（卒論での注意）

- **仮定 (H) の成否**（一般の緩変動 $\ell$ に対する Zador 漸近の $\alpha$ 一様性）は未証明であり、系1.1 は (H) を仮定した条件付き結果。厳密冪裾では成立（例1.2）。卒論では「今後の課題」と明記する方針（査読 §5 の助言どおり）。
- Graf–Luschgy Theorem 6.2 の正確な仮定・定数は原書（LNM 1730）で最終確認すること（査読 §2-② の助言。$Q_1([0,1])=1/4$、$\lVert f\rVert_{1/2}=(\int f^{1/2})^2$ は査読でも検算済み）。
- 定理はあくまで**上界汎関数の配置間比較**であり、実 CVaR 誤差の改善を直接示すものではない（注意1.3 で明記済み）。実験の M2 は正則化歪み $g_{\alpha,\lambda}$（$\lambda=0.05$）の実装で、定理の対象は $\lambda=0$ の理想配置である点も注意1.3 で明記済み。
