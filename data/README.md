# データ管理ルール

このディレクトリには、分析で使う元データと加工済みデータを置きます。実データは原則として Git 管理しません。

## ディレクトリ

- `raw/`
  - 取得元から得た元データをそのまま置く
  - 手作業で修正した場合は、修正内容を `notes/` に記録する
- `processed/`
  - 加工済みデータ、スコア、バックテスト結果、集計結果を置く
  - 再生成できるものを優先し、生成条件を `notes/` に残す

## データソース記録

分析ごとに、少なくとも以下を `notes/` に残します。

- データ名
- 取得元 URL または取得方法
- 取得日
- 対象期間
- 対象ユニバース
- 主な列定義
- 欠損、調整後価格、上場廃止銘柄、銘柄コード変更の扱い
- 利用制約、ライセンス、再配布可否

## 推奨する価格データ列

最低限:

```text
date,code,close,volume
```

推奨:

```text
date,code,adjusted_close,close,volume,turnover,market,sector,market_cap,is_common_stock,is_reit,is_etf,is_special_attention,is_delisting
```

## 注意

- `data/raw/` は元データの保管場所であり、加工済みファイルで上書きしない
- `data/processed/` のファイルは、再生成手順が分かる状態にする
- API キー、認証 Cookie、個人情報、口座情報は保存しない
