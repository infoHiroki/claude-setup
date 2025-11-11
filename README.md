# Claude Setup

Claude Code を安全かつ便利に使うための基本設定を、**Claude Code 自身に設定してもらう**ためのリポジトリです。

## 特徴

- **設定ファイルではなく、指示書**: 設定ファイルを配布するのではなく、Claude Code への指示書を提供
- **Claude Code が自分で設定**: 指示書を渡すだけで、Claude Code が自分の設定を作成・更新
- **安全重視**: 機密情報の保護と危険なコマンドの防止を優先
- **シンプル**: 最低限必要な設定のみ、すぐに使い始められる

## 前提条件

このセットアップを始める前に、以下が完了していることを確認してください：

1. **Claude Code がインストール済み**
   - [公式サイト](https://code.claude.com) からインストール

2. **Claude Code の認証が完了済み**
   - `claude` コマンドを実行してログイン済み

3. **Git がインストール済み**（リポジトリをクローンするため）

## 使い方

### ステップ1: リポジトリをクローン

```bash
git clone https://github.com/infoHiroki/claude-setup.git
cd claude-setup
```

### ステップ2: Claude Code に指示書を渡す

Claude Code を起動して、以下のメッセージを送信：

```
setup.md の内容を読んで、指示に従って設定を適用してください
```

### ステップ3: 完了

Claude Code が自動的に設定を適用します。「設定を完了しました」というメッセージが表示されたら完了です。

## 何が設定されるか

このセットアップでは、以下の設定が適用されます：

### 1. セキュリティ設定

**保護される機密ファイル:**
- `.env` ファイル（環境変数）
- `secrets/` ディレクトリ
- `config/credentials.json` などの認証情報

**禁止される危険なコマンド:**
- `rm -rf`（再帰的な削除）
- `rm` コマンド全般

### 2. 基本的な許可

開発に必要な以下のツールとコマンドが許可されます：

- **ファイル操作**: Read, Write, Edit, Glob, Grep
- **Git コマンド**: すべての git コマンド
- **パッケージ管理**: npm コマンド
- **言語**: Node.js, Python
- **基本コマンド**: ls, cat, cd, mkdir, cp, mv, echo

### 3. 便利な機能

- **Status Line**: 現在の Git ブランチ名を表示

## カスタマイズ方法

設定をカスタマイズしたい場合は、以下の方法があります：

### 方法1: Claude Code に直接依頼

最も簡単な方法です。Claude Code に以下のように依頼してください：

```
settings.json に Python の black フォーマッターを自動実行する hook を追加してください
```

Claude Code が適切に設定を追加してくれます。

### 方法2: 設定ファイルを直接編集

`~/.claude/settings.json`（Windows の場合は `%USERPROFILE%\.claude\settings.json`）を直接編集することもできます。

詳しくは [公式ドキュメント](https://code.claude.com/docs) を参照してください。

## プロジェクト用のルール設定

各プロジェクトで独自のルールを設定したい場合は、`templates/CLAUDE.md.example` を参考にしてください。

プロジェクトのルートディレクトリに `CLAUDE.md` ファイルを作成すると、Claude Code が自動的にそのルールを読み込みます。

## トラブルシューティング

### 設定が反映されない

Claude Code を再起動してください：

```bash
# 現在のセッションを終了（Ctrl+C または exit）
# 再度起動
claude
```

### 設定ファイルの場所が分からない

以下のコマンドで確認できます：

**macOS/Linux:**
```bash
cat ~/.claude/settings.json
```

**Windows:**
```powershell
type %USERPROFILE%\.claude\settings.json
```

### 設定をリセットしたい

設定ファイルをバックアップしてから削除し、再度このセットアップを実行してください：

**macOS/Linux:**
```bash
mv ~/.claude/settings.json ~/.claude/settings.json.backup
```

**Windows:**
```powershell
move %USERPROFILE%\.claude\settings.json %USERPROFILE%\.claude\settings.json.backup
```

## 参考リンク

- [Claude Code 公式ドキュメント](https://code.claude.com/docs)
- [Claude Code Hooks ガイド](https://code.claude.com/docs/en/hooks-guide)
- [Claude Code 設定リファレンス](https://code.claude.com/docs/en/settings)

## ライセンス

MIT License

## 作成者

[@infoHiroki](https://github.com/infoHiroki)
