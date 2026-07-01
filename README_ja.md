# 孫栄 個人ウェブサイト

このリポジトリは，愛知県がんセンター 腫瘍制御学分野 リサーチレジデント 孫栄の個人研究者ウェブサイトです．

Hugo により構築された三言語対応サイトであり，論文，研究プロジェクト，研究指導，ニュース，プロフィール情報を `data/` 以下の YAML ファイルで管理します．

## 主な機能

- 英語，日本語，中国語の三言語対応．
- プロフィール，略歴，研究分野，メッセージ，外部リンクを含むホームページ．
- Publications，Projects，Supervision，News，Access，Links のデータ管理．
- 論文情報は `data/publications/` に年度別で保存．
- 研究紹介は `data/research/` に研究方向ごとに保存．
- `scripts/update_citations.py` による Google Scholar 引用数更新．
- GitHub Actions による GitHub Pages 自動デプロイ．

## ローカル確認

```powershell
hugo server -D
```

本番用ビルド：

```powershell
hugo --minify
```

## データ管理

- `data/home/`: プロフィールとホームページ内容．
- `data/access/`: 連絡先・アクセス情報．
- `data/links/`: 外部プロフィールリンク．未設定のリンクは後から追加できます．
- `data/research/`: 研究方向と代表論文．
- `data/publications/`: 年度別論文リスト．
- `data/projects/items.yaml`: 研究プロジェクト．
- `data/supervision/items.yaml`: 研究指導・メンタリング情報．
- `data/news/<year>/`: 年度別ニュースと経歴情報．
- `data/citations/meta.yaml`: 引用統計と最終更新時刻．

三言語データでは，共通項目を可能な限り `en.yaml` に置き，`ja.yaml` と `zh.yaml` には同じ ID に対応する翻訳・上書き情報のみを記述します．

## 引用数更新

手動更新：

```powershell
python scripts/update_citations.py
```

このスクリプトは Google Scholar プロフィールから論文情報を取得し，全ての論文 YAML に引用数を反映します．また `data/citations/meta.yaml` を更新し，新しい論文が検出された場合は対応する年度ファイルへ追加できます．

`.github/workflows/update-citations.yml` は，日本時間の深夜頃と中国時間の正午頃に毎日自動実行されます．

Google Scholar では自動アクセスが一時的に制限される場合があります．その場合は時間を置いて workflow またはローカルスクリプトを再実行してください．

## デプロイ

`.github/workflows/hugo.yml` により GitHub Pages へ自動公開されます．GitHub に push すると，サイトが自動的にビルド・公開されます．
