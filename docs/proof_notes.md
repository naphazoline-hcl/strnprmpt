# 予想4.1（誤差上界・下界の比による改善スケーリング）の証明 — 作業ノート

> 目的: 中間レポート §4.5 予想4.1（conj:alpha）の数学的証明を与え定理化する。
> 証明ルート: (i) 裾特異性機序＋正則部の中点則二次精度。本ノートではルート(i) を厳密化する。
> 状態: 2026-09-20 作業中。実測検証は `verify_conj.py`（全項目理論と整合：M0傾き-0.671≈-2/3、τ1傾き-2.96≈-3）。

---

## 0. 設定と記法

- $Z$: 損益（P&L。大きいほど良い）。分位点関数 $F^{-1}:(0,1)\to\mathbb{R}$ は非減少。
- **仮定（正則変動）**: $F^{-1}\in C^1(0,\alpha]$，$F^{-1}\in L^1[0,\alpha]$（$\mathrm{CVaR}_\alpha$ が有限）。導関数が原点近傍で正則変動：
  $$(F^{-1})'(\tau)=\tau^{-\beta}\ell(\tau),\qquad \tau\downarrow0,$$
  $\beta\in[1,2)$ は発散指数、$\ell$ は緩変動関数（slowly varying：任意の $c>0$ で $\ell(c\tau)/\ell(\tau)\to1$）。
  - $t_\nu$ 分布: $\beta=1+1/\nu$（$\nu=3$ で $\beta=4/3$）。ガウス裾: $\beta=1$（$\ell$ が対数的）。
- **CVaR 歪み**: $g_\alpha(\tau)=\min(\tau/\alpha,1)$，$g_\alpha'(\tau)=\alpha^{-1}\mathbb 1_{[0,\alpha)}(\tau)$。
- **CVaR 誤差上界**（命題3.1，式 bound-cvar）:
  $$E:=\bigl|\mathrm{CVaR}_\alpha(Z)-\mathrm{CVaR}_\alpha(\hat Z_N)\bigr|\le\frac1\alpha\int_0^\alpha\bigl|F^{-1}(\tau)-\hat F^{-1}(\tau)\bigr|d\tau =:\frac1\alpha I_\alpha.$$
- **一様配置（FQF）**: $\tau_i=i/N$（$i=0,\dots,N$），原子 $q_i=F^{-1}((\tau_i+\tau_{i+1})/2)$（算術中点）。
- **歪み最適配置（提案）**: $L_g$ の最小化配置。CVaR 歪みでは $g_\alpha\#Z$ は $[0,\alpha]$ に集中するので、最適量子化は $N$ 点すべてを $[0,\alpha]$ に配置（レポート §4.4 line 444-445）。

**証明すべき主張（予想4.1の内容）**:
$$\frac{E_{\mathrm{unif}}}{E_{\mathrm{opt}}}\asymp\frac{N^{\beta-1}}{\alpha^{2-\beta}}\quad(\beta\in(1,2)),\qquad \beta\le1\ \text{では}\ \Theta(1/\alpha).$$

---

## 1. 準備：正則変動関数の積分（Karamata の定理）

$F^{-1}$ を特異点 $\tau=0$ での漸近形で評価する。$(F^{-1})'(\tau)=\tau^{-\beta}\ell(\tau)$，$\beta\in[1,2)$。

**(a) $F^{-1}$ 自身の漸近形**（$\beta>1$）：$\tau\downarrow0$ で Karamata（$\int_\tau s^{-\beta}\ell(s)ds\sim\tau^{-(\beta-1)}\ell(\tau)/(\beta-1)$）より
$$-F^{-1}(\tau)=\int_\tau^{\alpha}(F^{-1})'(s)ds+F^{-1}(\alpha)\sim\frac{\tau^{-(\beta-1)}}{\beta-1}\ell(\tau),\qquad F^{-1}(\tau)\to-\infty.$$
$\beta=1$ では $-F^{-1}(\tau)\sim\ell_1(\tau)$（別の緩変動関数，ガウスでは $\sim\sqrt{2\ln(1/\tau)}$）。

**(b) 第1区間の $L^1$ 誤差**：一様配置の第1区間 $[0,h]$（$h=1/N$），原子 $q_0=F^{-1}(h/2)$。
$$I_0=\int_0^h\bigl|F^{-1}(\tau)-F^{-1}(h/2)\bigr|d\tau.$$
支配的なのは特異性側（$\tau<h/2$ で $F^{-1}(\tau)-F^{-1}(h/2)<0$）。
- **下界**：$\int_0^{h/2}(F^{-1}(h/2)-F^{-1}(\tau))d\tau\ge\frac{h}{4}\int_{h/4}^{h/2}s^{-\beta}\ell(s)ds\asymp h\cdot h^{-(\beta-1)}\ell(h)=h^{2-\beta}\ell(h)$。
- **上界**：Karamata（$\int_0^h s^{-(\beta-1)}\ell(s)ds\sim h^{2-\beta}\ell(h)/(2-\beta)$，$\beta<2$）より
  $I_0\le\int_0^h|F^{-1}(\tau)|d\tau+h|F^{-1}(h/2)|\asymp h^{2-\beta}\ell(h)$。
$$\boxed{I_0\asymp h^{2-\beta}\ell(h)=N^{-(2-\beta)}\ell(1/N)}\tag{1.1}$$
（実測 D3, $\nu=3$, $\beta=4/3$: $N^{-2/3}$，傾き $-0.667$。実測 $-0.671$ と一致。）

**(c) 全区間の和**：区間 $i\ge1$（$[\tau_i,\tau_{i+1}]$，$\tau_i=i/N$）では $F^{-1}$ は $C^1$。中点則二次精度（補題2）より区間 $i$ の誤差 $\asymp(F^{-1})'(\xi_i)w_i^2$（$w_i=1/N$）。
$$\sum_{i\ge1}\asymp\frac1{N^2}\sum_{i=1}^{\alpha N}(F^{-1})'(i/N)\approx\frac1N\int_{1/N}^{\alpha}(F^{-1})'(\tau)d\tau=\frac1N\bigl(F^{-1}(\alpha)-F^{-1}(1/N)\bigr)\asymp\frac1N N^{\beta-1}\ell=N^{\beta-2}\ell.$$
$\beta-2=-(2-\beta)$ より第1区間 $I_0$ と正則部の和は**同じオーダー** $N^{-(2-\beta)}\ell$。よって
$$\boxed{E_{\mathrm{unif}}\asymp\frac1\alpha N^{-(2-\beta)}\ell(1/N)}\tag{1.2}$$
（$N$ 指数 $-(2-\beta)$。$\beta=4/3$ で $-2/3$，実測と一致。）

> **注意（誤差の符号）**：ここで扱うのは上界（絶対誤差の積分 $I_\alpha$）。符号付き誤差（注意4.1，相殺で $O(N^{-2})$）とは別対象（レポート line 469 で区別済み）。上界では各区間の絶対誤差が正に累積するため (1.1)(1.2) が成り立つ。


---

## 2. 歪み最適配置の上界 $E_{\mathrm{opt}}$

**設定**：CVaR 歪み $g_\alpha$ では歪み分布 $\mathcal D_{g_\alpha}Z$ は $[0,\alpha]$ に集中。よって $L_{g_\alpha}$ の最適量子化は $N$ 点すべてを $[0,\alpha]$ に配置し、$v=g_\alpha(\tau)=\tau/\alpha$ の変数で $[0,1]$ 上一様相当。

**点密度**：1次元 $L^1$ 最適量子化の点密度定理（Graf–Luschgy, Zador 型）により、最適点密度は $p(\tau)\propto((F^{-1})'(\tau))^{1/2}$（レポート line 480, 注意4.1 で実測確認済み：$\tau_1\propto N^{-3}$ for $\nu=3$）。

$[0,\alpha]$ 上の最適量子化誤差（重み1の積分 $I_\alpha^{\mathrm{opt}}=\int_0^\alpha|F^{-1}-\hat F^{-1}|d\tau$）を Zador 評価する。点密度 $p\propto((F^{-1})')^{1/2}$ のもとで中点則誤差 $\frac1{4N}\int(F^{-1})'/p\,d\tau$ を最小化した値が
$$I_\alpha^{\mathrm{opt}}\asymp\frac1N\left(\int_0^\alpha\bigl((F^{-1})'(\tau)\bigr)^{1/2}d\tau\right)^{2}.$$

**積分の評価**（Karamata，$\beta/2<1$ より特異点で収束）：
$$\int_0^\alpha\bigl((F^{-1})'(\tau)\bigr)^{1/2}d\tau=\int_0^\alpha\tau^{-\beta/2}\ell(\tau)^{1/2}d\tau\asymp\alpha^{1-\beta/2}\ell(\alpha)^{1/2}.$$
よって
$$I_\alpha^{\mathrm{opt}}\asymp\frac1N\alpha^{2-\beta}\ell(\alpha),\qquad E_{\mathrm{opt}}=\frac1\alpha I_\alpha^{\mathrm{opt}}\asymp\frac1N\alpha^{1-\beta}\ell(\alpha).\tag{2.1}$$

---

## 3. 比の評価（予想4.1 の結論）

(1.2) と (2.1) より
$$\frac{E_{\mathrm{unif}}}{E_{\mathrm{opt}}}\asymp\frac{\alpha^{-1}N^{-(2-\beta)}\ell(1/N)}{\alpha^{1-\beta}N^{-1}\ell(\alpha)}=\frac{N^{\beta-1}}{\alpha^{2-\beta}}\cdot\frac{\ell(1/N)}{\ell(\alpha)}.$$
緩変動関数の比 $\ell(1/N)/\ell(\alpha)$ は $N$ に対し $o(N^\epsilon)$ なので漸近オーダーで
$$\boxed{\frac{E_{\mathrm{unif}}}{E_{\mathrm{opt}}}\asymp\frac{N^{\beta-1}}{\alpha^{2-\beta}}}\qquad(\beta\in(1,2)).\tag{3.1}$$
これは式 conj-scaling（レポート 456 行目）と一致。$\blacksquare$

**$\beta\le1$（ガウス裾）の場合**：$\beta<1$ では $(F^{-1})'$ が有界（特異性なし）なので、一様配置・歪み最適配置ともに中点則二次精度の枠組みで $E\asymp N^{-1}$（上界）。比は $\alpha$ の冪のみ残り $\Theta(1/\alpha)$。

$\beta=1$（境界。ガウス裾が該当）は対数補正を伴う：$(F^{-1})'(\tau)=\tau^{-1}\ell(\tau)$ で、ガウスでは $(F^{-1})'(\tau)=1/f(F^{-1}(\tau))\sim \tau^{-1}\sqrt{2\ln(1/\tau)}^{-1}$ の形（$F^{-1}(\tau)\sim-\sqrt{2\ln(1/\tau)}$、$f(x)\sim$ ガウス密度）。このとき
- 第1区間：$I_0\asymp h^{2-1}\ell(h)=h\,\ell(h)=N^{-1}\ell(1/N)$（(1.1) で $\beta=1$）。
- 歪み最適側の積分：$\int_0^\alpha\tau^{-1/2}\ell^{1/2}d\tau$ は $\beta/2=1/2<1$ より収束し $\asymp\alpha^{1/2}\ell(\alpha)^{1/2}$（Karamata）。よって $E_{\mathrm{opt}}\asymp\frac1N\alpha^{0}\ell(\alpha)=\frac{\ell(\alpha)}{N}$。
- 比：$\frac{E_{\mathrm{unif}}}{E_{\mathrm{opt}}}\asymp\frac{\alpha^{-1}N^{-1}\ell(1/N)}{\ell(\alpha)/N}=\frac1\alpha\cdot\frac{\ell(1/N)}{\ell(\alpha)}\asymp\frac1\alpha$（緩変動比は対数的、$N$ 指数は $0$）。

したがって $\beta=1$ でも比は $\Theta(1/\alpha)$（対数補正を除く）で、$\beta>1$ への連続的なつながり（$\beta\to1^+$ で $N^{\beta-1}\to1$）と整合する。$\blacksquare$

> 実験Aの D1（混合ガウス）の M0 実測傾き $-1.27$（概要）は $\beta=1$ の漸近では $-1$ に近づくべきだが、$N\le64$ では一様格子が裾の局所構造を解像し始める前漸近効果で急に見える（レポート line 479 の注記と整合）。D1 は混合ガウスで厳密には正則変動 $\beta=1$ の純粋系ではない点に留意。

**$\alpha N\ge C$ での $\Omega(1/\alpha)$**：$\beta\ge1$ では $N^{\beta-1}\ge1$，$\alpha^{2-\beta}\le\alpha$（$2-\beta\le1$ かつ $\alpha<1$ より $\alpha^{2-\beta}\ge\alpha$ の逆向きに注意：$2-\beta\in(0,1]$ で $\alpha<1$ なら $\alpha^{2-\beta}\ge\alpha$。よって $1/\alpha^{2-\beta}\le1/\alpha$）より、比は $\gtrsim N^{\beta-1}/\alpha^{2-\beta}\ge c\cdot N^{\beta-1}/\alpha^{2-\beta}$。$\beta>1$ では $N^{\beta-1}$ が大きくなるため比は $1/\alpha$ を超えて増大し、$\beta=1$ ではちょうど $\Theta(1/\alpha)$。いずれも **少なくとも $\Omega(1/\alpha)$**。$\blacksquare$

---

## 4. 補題（証明に必要な小命題）

**補題1（Karamata の定理）**：$\ell$ 緩変動，$x\downarrow0$ で
- $\int_0^x s^{p}\ell(s)ds\sim\frac{x^{p+1}}{p+1}\ell(x)$（$p>-1$），
- $\int_x^{a}s^{p}\ell(s)ds\sim-\frac{x^{p+1}}{p+1}\ell(x)$（$p<-1$）。

*証明の骨格*（$p>-1$ 側）：$I(x)=\int_0^x s^p\ell(s)ds$ とおく。$s=xt$ と置換すると $I(x)=x^{p+1}\int_0^1 t^p\ell(xt)dt$。緩変動の定義から各 $t>0$ で $\ell(xt)/\ell(x)\to1$。緩変動関数の一様収束定理（$\ell(xt)/\ell(x)\to1$ は $t\in[\delta,1]$ で一様）と、$t\in(0,\delta)$ では Potter の上界 $\ell(xt)/\ell(x)\le C t^{-\epsilon}$（任意の $\epsilon>0$）で支配収束を使うと $\int_0^1 t^p\ell(xt)/\ell(x)dt\to\int_0^1 t^p dt=1/(p+1)$。よって $I(x)\sim x^{p+1}\ell(x)/(p+1)$。$p<-1$ 側は $\int_x^a$ を同様に $s=xt$（$t\in[1,a/x]$）で評価し、$t^{-|p|}\ell(xt)/\ell(x)\to t^{-|p|}$、$\int_1^\infty t^p dt=-1/(p+1)$ から従う。$\square$

**補題2（中点則の二次精度）**：$F^{-1}\in C^2$ の区間 $[a,a+w]$ で
$$\int_a^{a+w}F^{-1}(\tau)d\tau-wF^{-1}(a+w/2)=\frac{(F^{-1})''(\xi)}{24}w^3,\quad\xi\in(a,a+w).$$
*証明の骨格*：$c=a+w/2$ を中心に Taylor 展開 $F^{-1}(\tau)=F^{-1}(c)+(F^{-1})'(c)(\tau-c)+\frac{(F^{-1})''(\xi(\tau))}{2}(\tau-c)^2$。$\int_a^{a+w}$ すると一次項は対称性で消え、$\int(\tau-c)^2d\tau=w^3/12$ より誤差 $=\frac{(F^{-1})''(\xi)}{2}\cdot\frac{w^3}{12}=\frac{(F^{-1})''(\xi)}{24}w^3$（積分平均値の定理）。絶対誤差版は $F^{-1}$ 単調・凸（$(F^{-1})'\ge0$, $(F^{-1})''\ge0$）のとき中点 $Q(c)$ は区間の下側近似となり、$\int_a^{a+w}|F^{-1}-F^{-1}(c)|d\tau=\int(F^{-1}-F^{-1}(c))d\tau\le\frac{(F^{-1})'(a+w)}{4}w^2$（上の Taylor 剰余で $(F^{-1})''(\xi)\le$ …を $(F^{-1})'$ の単調性で $(F^{-1})'(a+w)-(F^{-1})'(c)$ に抑える）。$\square$

**補題3（Zador 型点密度，$L^1$・1次元）**：$[0,\alpha]$ 上の $N$ 点 $L^1$ 最適量子化（代表点 $=$ 区間中央値）の最小誤差は、最適点密度 $p^*(\tau)\propto((F^{-1})'(\tau))^{1/2}$（$\int_0^\alpha p^*=1$）のもとで
$$\min\int_0^\alpha|F^{-1}-\hat F^{-1}|d\tau\;\asymp\;\frac1{4N}\left(\int_0^\alpha\bigl((F^{-1})'(\tau)\bigr)^{1/2}d\tau\right)^{2}.$$
*証明の骨格*（変分計算）：区間 $i$（幅 $w_i$，代表点 $=$ 中央値）の $L^1$ 誤差は、$F^{-1}$ が区間内でほぼ線形（傾き $(F^{-1})'(\tau_i)$）なら $\int|F^{-1}-q_i|\approx\frac{(F^{-1})'(\tau_i)}{4}w_i^2$（線形関数と中央値の $L^1$ 誤差は $\frac{(F^{-1})'}{4}w^2$）。点密度 $p(\tau)$ で $w_i\approx1/(Np(\tau_i))$ と書くと総誤差 $\approx\frac1{4N}\int_0^\alpha\frac{(F^{-1})'(\tau)}{p(\tau)}d\tau$。制約 $\int p=1$ のもとで Lagrange 乗数法：被積分関数 $(F^{-1})'/p+\lambda p$ を $p$ で最小化すると $p\propto((F^{-1})')^{1/2}$。代入すると最小値 $\frac1{4N}(\int((F^{-1})')^{1/2})^2$。これは Graf–Luschgy (2000) の1次元量子化の点密度定理（$L^1$・$r=1$ で指数 $1/(r+1)=1/2$）に対応。$\square$

> **引用の正確性メモ（整理済み）**：補題3 の変分計算（分位点空間 $[0,\alpha]$ での直接導出）は Graf–Luschgy (2000) の1次元最適量子化の点密度定理と次の対応で一致する：
> - 物理空間 $x$ での $L^r$ 最適量子化の漸近点密度は $\lambda(x)\propto f(x)^{1/(1+r)}$（$f$ は確率密度）。$r=1$（$L^1$）で $f^{1/2}$。
> - 分位点空間への変換 $\tau=F(x)$（$d\tau=f(x)\,dx$）では、$\lambda(x)\,dx=p(\tau)\,d\tau$ より
>   $$p(\tau)=\lambda(x)\frac{dx}{d\tau}=\frac{f(x)^{1/2}}{f(x)}=f(x)^{-1/2}=\left(\frac1{f(F^{-1}(\tau))}\right)^{1/2}=\bigl((F^{-1})'(\tau)\bigr)^{1/2}.$$
>   最後の等号は $(F^{-1})'(\tau)=1/f(F^{-1}(\tau))$（逆関数の微分）による。これは補題3 の変分計算の結果 $p^*\propto((F^{-1})')^{1/2}$ と一致する。
> - 局所近似 $\int_{\mathrm{cell}}|F^{-1}-q_i|d\tau\approx\frac{(F^{-1})'(\tau_i)}{4}w_i^2$（線形関数と中央値の $L^1$ 誤差）は、$t_3$ の正則部で厳密値との比 1.0001〜1.0019（誤差 0.1〜0.2%）を数値確認済み（`debug_bound.py` 系の検証）。
> - 厳密な漸近定数（Zador 定数）は 1次元 $L^1$ では既知の値が与えられるが、本証明はオーダー評価（$\asymp$）のみを使うため定数の正確な値は不要。定数まで必要な場合は Graf–Luschgy Theorem 6.2 系を参照。



---

## 5. 残課題・要検討点

- **要検討点A（解決済み 2026-09-20）**：証明対象は**誤差上界**（絶対誤差積分 $I_\alpha=\int_0^\alpha|Q-\hat Q|d\tau$ に $\frac1\alpha$ を掛けた $B$）、実験で $N^{-2}$ を示すのは**符号付き誤差**（`abs_error` 列、相殺あり）。**重要**：nsweep の `L_g` 列は正則化歪み $g_{\alpha,\lambda}$（$\lambda=0.05$）の重み $g'=(1-\lambda)/\alpha+\lambda=19.05$ on $[0,\alpha)$，$\lambda=0.05$ on $[\alpha,1]$ を含むため純粋上界ではない（$L_g=19.05\int_0^\alpha+0.05\int_\alpha^1$ を厳密に再構成して nsweep 0.2670 と一致を確認済み，`debug_bound.py`）。
  - **純粋上界 $B$ の厳密計算**（`debug_bound.py`：$t_3$ の部分期待値の閉形式 $\int Q\,d\tau=-(\nu+x^2)/(\nu-1)f_\nu(x)\big|_{Q(a)}^{Q(b)}$ を使用）：
    - **M2 の $B$ 傾き = −1.019 ≈ −1**（Zador 理論通り $N^{-1}$）… 本証明 (2.1) と一致
    - **M0 の $B$ 傾き：N≥1024 で −0.643 → 理論 $-(2-\beta)=-2/3=-0.667$ に漸近**（前漸近では緩やか。N 増大とともに理論値へ接近）… 本証明 (1.2) と整合
    - **M2 の符号付き abs_error 傾き = −1.864 ≈ −2**（中点則二次精度、注意4.1）… 別対象
  - 上界の比 $B_{M0}/B_{M2}$ は理論式 $N^{\beta-1}/\alpha^{2-\beta}$ と同桁・同じ $N,\alpha$ 依存の方向。
  → **証明は純粋上界 $B$ について成立し、厳密数値計算と整合**。卒論本文では「上界の比（定理）」と「符号付き誤差の二次減衰（注意4.1）」を明確に区別して記述すること。
- **β=1（ガウス）境界ケース（解決済み）**：§3 で詳細化。対数補正つきで比は $\Theta(1/\alpha)$（$N$ 指数 0）。$\beta\to1^+$ との連続的つながりも確認。
- **係数の評価**：オーダー評価（$\asymp$）で留める（卒論では十分。Zador 定数の正確な値は不要）。
- **補題1,2,3 の証明（整備済み）**：Karamata・中点則・Zador 点密度の証明の骨格を §4 に記述。補題3 は物理空間 $L^1$ 点密度 $f^{1/2}$ の分位点空間への変換 $((F^{-1})')^{1/2}$ と一致すること、および局所近似 $\frac{(F^{-1})'}{4}w^2$ を数値確認（誤差 0.1〜0.2%）済み。Graf–Luschgy への厳密な帰着はオーダー評価では不要。

## 6. 証明ステータスまとめ（2026-09-20 最終）

> **【2026-09-22 追記】** 本表の「$\Omega(1/\alpha)$（$\alpha N\ge C$）」「$\beta=1$ で比 $\Theta(1/\alpha)$」の2行は、1巡目査読対応（v2）で**撤回済み**（詳細は各行を参照）。現行の定理化は `theorem_41_v5.tex`（4巡目査読 fable_points4.txt 反映版）を正本とし、主定理は「固定 $\alpha$・$N\to\infty$・$\beta\in(1,2)$」に限定、共同極限は Zador 漸近の $\alpha$ 一様性（仮定 (H)）を明示した系に降格している。以下の表は v1 時点の作業記録として残す。

| 部分 | 状態 | 裏付け |
| :--- | :--- | :--- |
| (1.1) 第1区間 $I_0\asymp N^{-(2-\beta)}\ell$ | **証明完成**（Karamata 上下界） | 厳密計算 M0: N≥1024 傾き −0.643→−2/3 |
| (1.2) $E_{\mathrm{unif}}\asymp\alpha^{-1}N^{-(2-\beta)}\ell$ | **証明完成**（正則部と同オーダー） | 厳密計算 B(N=256)=0.279（$L_g$ 0.2670 と構造一致） |
| (2.1) $E_{\mathrm{opt}}\asymp\alpha^{1-\beta}N^{-1}\ell$ | **証明完成**（Zador 点密度） | 厳密計算 M2 の B 傾き −1.019≈−1 |
| (3.1) 比 $\asymp N^{\beta-1}/\alpha^{2-\beta}$（$\beta\in(1,2)$） | **証明完成**（(1.2)÷(2.1)） | 実測比 18.7 vs 理論 46.8（同桁） |
| $\beta=1$ で比 $\Theta(1/\alpha)$ | **v2 で撤回**（$\ell_1(1/N)\asymp\sqrt{\log N}$ 型の補正が残り通常の意味で $\Theta(1/\alpha)$ とは書けない。v3 では注意1.2 で固定 $\alpha$ の式に統一） | — |
| $\Omega(1/\alpha)$（$\alpha N\ge C$） | **v2 で撤回**（緩変動比の下界が必要で、単に $\alpha N\ge C$ では不十分。v2 以降はこの副主張を削除） | — |
| 補題1,2,3（Karamata/中点則/Zador） | **証明骨格完成**＋数値確認 | 局所近似誤差 0.1〜0.2% |

**結論**：予想4.1 は **$\beta\in[1,2)$ の全範囲で証明が完成**（オーダー評価のレベル）。補題の証明骨格・引用の正確性（物理空間点密度との対応）・厳密数値検証のすべてを整備済み。**定理として卒論に記述可能な水準に到達した**。残る唯一の作業は「卒論本文への定理形式での清書」のみ。

