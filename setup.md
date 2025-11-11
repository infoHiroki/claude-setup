# Claude Code 基本セットアップ

> このファイルを Claude Code に読ませると、自動的に設定してくれます

## 📝 Claude Code への指示

このファイルを読んだら、私（ユーザー）の設定ファイルを作成してください。

**設定ファイルの場所:**
- Mac/Linux: `~/.claude/settings.json`
- Windows: `%USERPROFILE%\.claude\settings.json`

既に設定ファイルがある場合は、既存の内容を保持したまま追加してください。

---

## ⚙️ 設定する内容

### 1. 基本ルール

**「何かする前に確認してね」というルール:**
```json
"defaultMode": "ask"
```

これで、Claude Code は何かファイルを変更する前に必ず「やっていいですか？」と聞いてくれます。

### 2. できることを許可

Claude Code にいろいろなことをやってもらうため、以下を許可します：

**ファイル操作:**
- ファイルを読む（Read）
- ファイルを書く（Write）
- ファイルを編集する（Edit）
- ファイルを探す（Glob）
- テキストを検索する（Grep）

**よく使うコマンド:**
- Git コマンド（バージョン管理）
- npm コマンド（パッケージ管理）
- Node.js、Python の実行
- ls、cat、cd、mkdir、cp、mv、echo（基本コマンド）

これらを全部許可することで、Claude Code が自由に開発を手伝えるようになります。

### 3. 便利な表示

**Git ブランチを表示:**
今どのブランチで作業しているかが一目で分かるように、画面に表示します。

---

## 🔧 実際の設定（JSON）

以下の内容を設定ファイルに書き込んでください：

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
      "Bash(echo:*)",
      "Bash(rm:*)",
      "Bash(curl:*)",
      "Bash(wget:*)"
    ],
    "deny": [
      "Read(./.git/**)",
      "Write(./.git/**)",
      "Edit(./.git/**)"
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

## ✅ 設定が終わったら

設定が完了したら、私（ユーザー）に以下を伝えてください：

1. 「設定を完了しました！」
2. どのファイルに設定を書き込んだか
3. 何か問題があった場合はその内容

---

## 💡 この設定について

**この設定の特徴:**
- **最小限の制限**: Claude Code を自由に使えます
- **確認は取る**: 何かする前に必ず聞いてくれます
- **`.git`だけ保護**: Git の内部ファイルだけは触らないようにします

**セキュリティが気になる方へ:**
- 機密情報を扱う場合は `setup-secure.md` を使ってください
- `.env` ファイルや秘密の情報を保護する設定が入っています
