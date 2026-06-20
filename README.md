# template-invest-insight

投資分析を一定の前提で進めるための、最小構成のテンプレートです。

自動化や特定のデータ取得サービスを前提にせず、作業場所と基本ツールだけを揃えることを目的としています。調査や試作を優先し、再利用価値が確認できた処理だけを共通化する運用を想定しています。

## 目的

- 毎回の分析を同じディレクトリ構成で始められるようにする
- 調査、EDA、試作、メモの置き場を明確にする
- 特定の API やブローカーに依存しない分析テンプレートを維持する

## 前提ツール

- `mise`
  - 実行環境や言語バージョンの切り替えに使います
- `marimo`
  - 調査、EDA、仮説検証ノートに使います
- `python`
  - 単発スクリプトや共通処理の実行に使います

## クイックスタート

環境準備:

```powershell
mise trust
mise install
```

新しい分析メモを作る:

```powershell
Copy-Item notes/_template.md notes/<analysis-name>.md
```

調査ノートを開く:

```powershell
marimo edit notebooks/<notebook>.py
```

構文確認:

```powershell
mise run compile
```

## ディレクトリ構成

```text
.
├─ data/
│  ├─ processed/  加工済みデータ
│  └─ raw/        元データ
├─ lib/           再利用する共通コード
├─ notebooks/     marimo で使う調査・EDA ノート
├─ notes/         分析メモ、前提、結論の記録
└─ scratch/       一時的な試作コードや下書き
```

## 作業ルール

- 新しい分析は、まず `notebooks/` か `scratch/` で始めます
- `lib/` には、共通化が必要になった処理だけを移します
- `data/raw/` のデータは原則そのまま保持します
- 加工結果は `data/processed/` に出力します
- 分析ごとに、前提、対象銘柄、期間、結論を `notes/` に短く残します
- 途中生成物や試作コードを、いきなり `lib/` に入れません
- データ取得方法は案件ごとに選び、テンプレート側では決め打ちしません
- 実データ、API キー、認証情報、口座情報、個人情報は Git 管理しません
- 参照した公開情報は、URL、取得日、使った理由を `notes/` に残します

## データ管理

- 実データは `data/raw/` と `data/processed/` に置きます
- これらのデータファイルは `.gitignore` で Git 管理対象外にしています
- データの列定義、取得元、取得日、対象期間、欠損処理は分析メモに残します
- 詳細は `data/README.md` を参照してください

## メモの型

新しい分析では `notes/_template.md` を元に、以下を最初に記録します。

- テーマ
- 対象銘柄 / ユニバース
- 対象期間
- データソース
- 仮説
- 手法
- 結果
- 判断
- 次の論点

## 推奨フロー

1. `notes/_template.md` を元に、今回の分析テーマと前提を書く
2. `notebooks/` で `marimo` ノートを作り、探索や可視化を進める
3. 試作コードは `scratch/` に置いて検証する
4. 再利用価値がある処理だけ `lib/` に移す
5. 最後に `notes/` に結果と次の論点を残す

## コマンド例

環境準備:

```powershell
mise trust
mise install
```

調査開始:

```powershell
marimo edit notebooks/<notebook>.py
```

単発スクリプト実行:

```powershell
python <script>.py
```

構文確認:

```powershell
mise run compile
```

## 運用メモ

- まずは調査と試作を優先します
- 共通化は必要になってから行います
- 分析結果は `notes/` に残し、後から見返せる状態にします
- `scratch/` の処理が再利用されるようになったら、必要な部分だけ `lib/` に移します
