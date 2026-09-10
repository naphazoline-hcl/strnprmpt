# README — 中間発表スライド（Beamer 16:9, Luebeck / orchid）

## 構成ファイル
- **slides_concise.tex**: 本番投影用スライド本体（**正式採用版**。文章を削り図・式・表中心に再構成）
- **slides_concise.pdf**: 本番投影用 PDF（17ページ、overfull 0、コンパイル確認済み）
- **slides.tex**: 完全版スライド本体（説明文を残した参照・予備版。9/10 確定の旧正式版）
- **slides.pdf**: 完全版 PDF（17ページ、overfull 0）
- **slides_outline.md**: 構成アウトライン（各スライドの時間配分・主要ブロック・図。完全版ベース）
- **slides_script.md**: 発表原稿（本編5分: 各スライド130〜150字＋ト書き＋質疑応答3分: 想定質問Q1〜Q5スクリプト完備）
- **slides_qa.md**: 質疑応答シート（想定質問Q1〜Q5＋予備Q6〜Q10・バックアップスライド対応表つき）
- **README.md**: 本ファイル

## 参照画像（同階層または ./figures/ に配置）
- `fig1_fqf_overview.png`: FQFアーキテクチャ概要図（S5予稿と同一）
- `fig3_placement.png`: 実験A quantile fraction配置図（中間レポート/_figgen/outA/ 拡大フォント版）
- `fig4_error.png`: 実験A CVaR推定誤差比較図（中間レポート/_figgen/outA/ 拡大フォント版）
- `fig5_curve.png`: 実験B RiskyChain-v0 学習曲線図（中間レポート/_figgen/outB/ 拡大フォント版）

## ビルド方法
### 推奨（LuaLaTeX + luatexja）
```bash
lualatex slides.tex
lualatex slides.tex
```

### 代替（upLaTeX / pLaTeX + dvipdfmx）
```bash
uplatex slides.tex
dvipdfmx slides.dvi
```
※ プリアンブルにて `\ifdefined\directlua` による自動分岐が設定されており、LuaLaTeX と upLaTeX/pLaTeX の両方でそのままコンパイル可能です。

## 正式採用版: slides_concise（2026-09-11 確定）
- **slides_concise.tex / slides_concise.pdf** を本番投影用の正式版として採用。slides.tex / slides.pdf（完全版）は参照・予備として残置。
- slides.tex（完全版）から口頭説明で足りる文章を削り、図・式・表＋キーメッセージのみに再構成した版（17ページ構成は同一）。
  - 本番投影用は本編10枚の文章を削減した版で、口頭内容は **slides_script.md をそのまま使用**（フレーム番号＝scriptの§番号で1対1対応。texの各フレーム冒頭に `% 口頭: slides_script.md §n` のコメントあり）。
- 質疑応答は **slides_qa.md**（想定質問Q1〜Q5＋予備Q6〜Q10）を使用し、Appendix A4・A5 を画面に表示する。
- Appendix 7枚（A1〜A7）は質疑応答・参照用として完全版と同一のまま維持。
- ビルド方法は完全版と同じ（`lualatex slides_concise.tex` を2回実行）。コンパイル確認済み（17ページ・エラー0・Overfull 0）。
- 図4枚（fig1/fig3/fig4/fig5）は完全版と共用のため、配置・削除の管理は同階層で統一すること。
  - 参照用レンダリング: `_pages/concise_p01.png` 〜 `concise_p17.png`。

