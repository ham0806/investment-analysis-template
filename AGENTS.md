# 投資分析テンプレート運用ルール

## 目的

このテンプレートは、Codex が毎回同じ前提で投資分析を進められるようにするための最小構成です。
自動化や特定のデータ取得サービスには寄せず、使うツールと作業先ディレクトリだけを明確にします。

## 基本方針

- すべての説明、回答、作業メモは日本語で行う
- まずは調査と試作を優先し、共通化が必要になったものだけ整理する
- データ取得方法は案件ごとに決める
- 特定の API、ブローカー、SDK を標準前提にしない

## 前提ツール

- `mise`
  - 実行環境や言語バージョンの切り替えに使う
- `marimo`
  - 調査、EDA、仮説検証ノートに使う
- `python`
  - 単発スクリプトや共通処理の実行に使う

## Commands

この repo での検証入口は以下を正とする。

初回のみ:

```powershell
mise trust
mise install
```

構文確認:

```powershell
mise run compile
```

`mise` を使わずに実行する場合:

```powershell
python -m compileall lib scratch notebooks
```

調査開始:

```powershell
marimo edit notebooks/<notebook>.py
```

単発スクリプト実行:

```powershell
python <script>.py
```

## ディレクトリ構成

- `notebooks/`
  - `marimo` で使う調査、EDA、検証ノートを置く
- `lib/`
  - 再利用する共通コードを置く
- `scratch/`
  - Codex が一時的に試すコードや下書きを置く
- `data/raw/`
  - 元データを置く
- `data/processed/`
  - 加工済みデータを置く
- `notes/`
  - 分析メモ、仮説、前提条件、結果サマリを置く

## 作業ルール

- 新しい分析は、まず `notebooks/` か `scratch/` で始める
- `lib/` は共通化が必要になった処理だけを移す
- `data/raw/` のデータは原則そのまま保持し、加工結果は `data/processed/` に出す
- 分析ごとに、前提、対象銘柄、期間、結論を `notes/` に短く残す
- 途中生成物や試作コードをいきなり `lib/` に入れない
- データ取得方法は案件ごとに選び、テンプレート側では決め打ちしない
- 実データ、API キー、認証情報、口座情報、個人情報は Git 管理しない
- 参照した公開情報は URL、取得日、使った理由を `notes/` に残す

## 共通化の目安

- 2回以上使う処理、または別分析でも使う可能性が高い処理だけ `lib/` に移す
- データ読み込み、列検証、指標計算、評価指標は共通化候補とする
- 個別仮説、途中検証、試行錯誤中のコードは `scratch/` か `notebooks/` に置く
- `lib/` に移した処理は、最小限の使用例または呼び出し元を残す

## 推奨する進め方

1. `notes/_template.md` を元に今回の分析テーマと前提を短く書く
2. `notebooks/` で `marimo` ノートを作り、探索や可視化を行う
3. 試作コードは `scratch/` に置いて検証する
4. 再利用価値がある処理だけ `lib/` に移す
5. 最後に `notes/` に結果と次の論点を残す

## 推奨コマンド例

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

## Codex への期待

- まずディレクトリ構成を尊重して作業場所を選ぶ
- 調査段階では `notebooks/` と `scratch/` を優先する
- 共有すべき処理だけ `lib/` に整理する
- 分析結果は必ず `notes/` に残せる形でまとめる
- 変更後は、内容に応じて `Commands` の検証入口を実行し、結果を報告する
