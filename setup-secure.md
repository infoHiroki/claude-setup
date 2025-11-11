# Claude Code セキュア設定 🔒

> 機密情報を扱う場合や、セキュリティを重視する方向けの設定です

## 📝 Claude Code への指示

このファイルを読んだら、私（ユーザー）の設定ファイルにセキュリティ強化版の設定を作成してください。

**設定ファイルの場所:**
- Mac/Linux: `~/.claude/settings.json`
- Windows: `%USERPROFILE%\.claude\settings.json`

既に設定ファイルがある場合は、既存の内容を保持したまま追加してください。

---

## 🛡️ この設定について

**こんな人におすすめ:**
- 会社の仕事で Claude Code を使う
- API キーやパスワードを扱うプロジェクトがある
- `.env` ファイルに秘密の情報が入っている
- セキュリティを特に気にする

**基本版との違い:**
- ✅ 機密ファイルを自動的に保護
- ✅ 危険なコマンドをブロック
- ✅ 外部への通信を制限
- ✅ 会話ログの自動削除

---

## ⚙️ 設定する内容

### 1. 機密ファイルの保護 🔐

以下のファイルは絶対に読み書きできないようにします：

**保護するファイル:**
- `.env` ファイル（環境変数、API キーなど）
- `secrets/` フォルダの中身
- `config/credentials.json`（認証情報）

**なぜ？**
- うっかり API キーを見せてしまうのを防ぐ
- 秘密の情報が外部に漏れるのを防ぐ

### 2. 危険なコマンドをブロック ⚠️

以下のコマンドは使えないようにします：

**ブロックするコマンド:**
- `rm` コマンド（ファイル削除）
- `curl` / `wget` / `fetch`（外部からデータを取得）

**なぜ？**
- 間違ってファイルを消してしまうのを防ぐ
- 悪意のあるスクリプトをダウンロードさせないため
- 機密情報を外部に送信させないため

### 3. 会話ログの自動削除 🗑️

**2週間経った会話は自動的に削除:**
```json
"cleanupPeriodDays": 14
```

**なぜ？**
- 古い会話に秘密の情報が残っているかもしれない
- ディスク容量を節約できる
- プライバシーを守れる

### 4. 基本ルール

**「何かする前に確認してね」:**
```json
"defaultMode": "ask"
```

これで、Claude Code は何かする前に必ず確認してくれます。

### 5. 便利な表示 📊

**Git ブランチを表示:**
今どのブランチで作業しているかが一目で分かります。

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
      "Read(./.git/**)",
      "Write(./.git/**)",
      "Edit(./.git/**)",
      "Bash(rm:*)",
      "Bash(rm -rf:*)",
      "Bash(curl:*)",
      "Bash(wget:*)",
      "Bash(fetch:*)"
    ],
    "defaultMode": "ask"
  },
  "cleanupPeriodDays": 14,
  "statusLine": {
    "type": "command",
    "command": "git branch --show-current 2>/dev/null || echo 'no git'",
    "padding": 1
  }
}
```

---

## ✅ 設定が終わったら

設定が完了したら、私（ユーザー）に以下を伝えてください：

1. 「セキュア設定を完了しました！🔒」
2. どのファイルに設定を書き込んだか
3. 何か問題があった場合はその内容

---

## 💡 注意事項

### 制限があることを理解しよう

この設定では以下のことができなくなります：

❌ **curl でAPIを叩く**
- 必要な場合は Claude Code の WebFetch 機能を使ってください
- または、プロジェクトごとに `curl` を許可する設定を追加

❌ **rm コマンドでファイルを削除**
- Git で削除する（`git rm`）か
- 手動でファイルを削除してください

❌ **.env ファイルを読む**
- どうしても必要な場合は、一時的に deny 設定を外す必要があります

### もっと自由に使いたい場合

- 個人開発で機密情報を扱わない場合は `setup.md`（基本版）を使ってください
- 必要に応じて、この設定をカスタマイズできます

### カスタマイズ例

**curl を使いたい場合:**
```json
"allow": [
  "Bash(curl:*)",
  // 他の設定...
]
```

**rm を使いたい場合:**
```json
// deny から "Bash(rm:*)" を削除
```

---

## 🔗 参考情報

- [Claude Code 公式ドキュメント](https://code.claude.com/docs)
- [セキュリティ設定の詳細](https://code.claude.com/docs/en/settings)
