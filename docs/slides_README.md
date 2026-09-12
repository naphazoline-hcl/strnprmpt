# README — 中間発表スライド（Beamer 16:9, Luebeck / orchid）

## 構成ファイル
- **slides_main.tex**: 本番投影用スライド本体（**正式採用版**。本編10枚＋参考文献1枚＝計11枚・QA/Appendixなし）
- **slides_main.pdf**: 本番投影用 PDF（11ページ、overfull 0、コンパイル確認済み）
- **slides_concise.tex**: 簡潔版スライド本体（本編10枚＋参考文献1枚＋Appendix A1〜A7＝計18枚。質疑バックアップ用の**予備版**）
- **slides_concise.pdf**: 簡潔版 PDF（18ページ、overfull 0）
- **slides.tex**: 完全版スライド本体（説明文を残した参照・予備版。9/10 確定の旧正式版）
- **slides.pdf**: 完全版 PDF（17ページ、overfull 0）
- **slides_outline.md**: 構成アウトライン（各スライドの時間配分・主要ブロック・図。完全版ベース）
- **slides_script.md**: 発表原稿（本編5分: 各スライド130〜150字＋ト書き＋質疑応答3分: 想定質問Q1〜Q5スクリプト完備、参考文献スライド送り指示入り）
- **slides_qa.md**: 質疑応答シート（想定質問Q1〜Q5＋予備Q6〜Q14・バックアップスライド対応表つき）
- **README.md**: 本ファイル

## 参照画像（同階層または ./figures/ に配置）
- `fig1_fqf_overview.png`: FQFアーキテクチャ概要図（S5予稿と同一）
- `fig3_placement.png`: 実験A quantile fraction配置図（中間レポート/_figgen/outA/ 拡大フォント版）
- `fig4_error.png`: 実験A CVaR推定誤差比較図（中間レポート/_figgen/outA/ 拡大フォント版）
- `figB2_estimation_ja.png`: 実験B RiskyChain-v0 CVaR推定誤差比較図（中間レポート/_figgen/outB/ 拡大フォント版）

## ビルド方法
### 推奨（LuaLaTeX + luatexja）
```bash
lualatex slides_main.tex
lualatex slides_main.tex
```

### 代替（upLaTeX / pLaTeX + dvipdfmx）
```bash
uplatex slides_main.tex
dvipdfmx slides_main.dvi
```
※ プリアンブルにて `\ifdefined\directlua` による自動分岐が設定されており、LuaLaTeX と upLaTeX/pLaTeX の両方でそのままコンパイル可能です。

## 本番投影版: slides_main（2026-09-12 v4 確定）
- **slides_main.tex / slides_main.pdf**（本編10枚＋主要7文献の参考文献1枚＝計11枚・QA/Appendixなし）を本番投影用の正式版として採用。slides_concise.tex/pdf（Appendix つき簡潔版、計18枚）は質疑バックアップ用の予備版、slides.tex/pdf は完全版として残置。
- 口頭内容は **slides_script.md** をそのまま使用（フレーム番号＝scriptの§番号で1対1対応。texの各フレーム冒頭に `% 口頭: slides_script.md §n` のコメントあり）。末尾で参考文献スライドを表示したまま質疑応答へ移行する。
- 質疑応答は **slides_qa.md**（Q1〜Q14）を使用。深掘り時は予備版 slides_concise.pdf の該当 Appendix（A1〜A7）を別デバイス等で表示する。
- ビルド方法は `lualatex slides_main.tex` を2回実行。コンパイル確認済み（11ページ・エラー0・Overfull 0）。
- 図4枚（fig1/fig3/fig4/figB2）は全バージョンで共用のため、配置・削除の管理は同階層で統一すること。


