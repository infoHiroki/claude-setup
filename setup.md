# Claude Code セットアップ指示書

このファイルの内容を読んで、あなた（Claude Code）自身の設定ファイルを作成・更新してください。

## 指示

以下の設定を `~/.claude/settings.json`（Windows の場合は `%USERPROFILE%\.claude\settings.json`）に適用してください。既存の設定がある場合は、安全にマージしてください。

## 設定内容

### 1. セキュリティ設定（必須）

機密情報を含むファイルへのアクセスを防止し、危険なコマンドの実行を禁止します。

**禁止するファイルアクセス:**
- `.env` および `.env.*` ファイル（環境変数）
- `secrets/**` ディレクトリ配下のすべてのファイル
- `config/credentials.json` などの認証情報ファイル

**禁止するコマンド:**
- `rm -rf` （再帰的なファイル削除）
- `rm:*` （すべての rm コマンド）

### 2. 基本的な許可設定

開発作業に必要な基本的なツールとコマンドを許可します。

**許可するツール:**
- `Read(*)` - すべてのファイルの読み取り（denyで制限されたものを除く）
- `Write(*)` - ファイルの書き込み
- `Edit(*)` - ファイルの編集
- `Glob(*)` - ファイル検索
- `Grep(*)` - テキスト検索

**許可する Bash コマンド:**
- `git:*` - Git コマンド全般
- `npm:*` - npm コマンド全般
- `node:*` - Node.js の実行
- `python:*` および `python3:*` - Python の実行
- `ls:*` - ファイル一覧表示
- `cat:*` - ファイル内容表示
- `cd:*` - ディレクトリ移動
- `mkdir:*` - ディレクトリ作成
- `cp:*` - ファイルコピー
- `mv:*` - ファイル移動
- `echo:*` - テキスト出力

### 3. 便利な機能

開発体験を向上させる便利な機能を設定します。

**Status Line:**
現在の Git ブランチ名をステータスラインに表示します。

```json
"statusLine": {
  "type": "command",
  "command": "git branch --show-current 2>/dev/null || echo 'no git'",
  "padding": 1
}
```

## 設定例（JSON形式）

上記の内容を以下のような JSON 形式で設定してください：

```json
{
  "permissions": {
    "allow": [
      "Read(*)",
      "Write(*)",
      "Edit(*)",
      "Glob(*)",
      "Grep(*)",
      "Bash(git:*)",
      "Bash(npm:*)",
      "Bash(node:*)",
      "Bash(python:*)",
      "Bash(python3:*)",
      "Bash(ls:*)",
      "Bash(cat:*)",
      "Bash(cd:*)",
      "Bash(mkdir:*)",
      "Bash(cp:*)",
      "Bash(mv:*)",
      "Bash(echo:*)"
    ],
    "deny": [
      "Read(./.env)",
      "Read(./.env.*)",
      "Write(./.env)",
      "Write(./.env.*)",
      "Read(./secrets/**)",
      "Write(./secrets/**)",
      "Read(./config/credentials.json)",
      "Write(./config/credentials.json)",
      "Bash(rm -rf:*)",
      "Bash(rm:*)"
    ],
    "defaultMode": "ask"
  },
  "statusLine": {
    "type": "command",
    "command": "git branch --show-current 2>/dev/null || echo 'no git'",
    "padding": 1
  }
}
```

## 設定後の確認

設定が完了したら、以下を確認してください：

1. `~/.claude/settings.json` ファイルが作成されていること
2. JSON 形式が正しいこと（構文エラーがないこと）
3. 既存の設定がある場合、それらが保持されていること

設定完了後、「設定を完了しました」とユーザーに報告してください。
