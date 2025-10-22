<div align="center">

![logo](src/img/logo-min.webp)

# AIClient-2-API 🚀

**複数のクライアント専用大規模言語モデルAPI（Gemini CLI、Qwen Code Plus、Kiro Claude...）を模擬リクエストし、ローカルのOpenAI互換インターフェースに統一的にラッピングする強力なプロキシ。**

</div>

<div align="center">

<a href="https://deepwiki.com/justlovemaki/AIClient-2-API"><img src="https://deepwiki.com/badge.svg" alt="Ask DeepWiki"  style="width: 134px; height: 23px;margin-bottom: 3px;"></a>

[![License: GPL v3](https://img.shields.io/badge/License-GPLv3-blue.svg)](https://www.gnu.org/licenses/gpl-3.0)
[![Node.js](https://img.shields.io/badge/Node.js-≥20.0.0-green.svg)](https://nodejs.org/)
[![Docker](https://img.shields.io/badge/docker-≥20.0.0-blue.svg)](https://aiproxy.justlikemaki.vip/ja/docs/installation/docker-deployment.html)


[**中文**](./README.md) | [**English**](./README-EN.md) | [**日本語**](./README-JA.md) | [**📚 完全ドキュメント**](https://aiproxy.justlikemaki.vip/ja/)

</div>

`AIClient2API` はクライアント制限を突破するAPIプロキシサービスで、元々クライアント内でのみ使用可能な無料大規模モデル（Gemini CLI、Qwen Code Plus、Kiro Claudeなど）を、あらゆるアプリケーションから呼び出せる標準OpenAI互換インターフェースに変換します。Node.jsをベースに構築され、OpenAI、Claude、Geminiの3大プロトコル間のインテリジェント変換をサポートし、Cherry-Studio、NextChat、Clineなどのツールで、Claude Sonnet 4.5、Gemini 2.5 Flash、Qwen3 Coder Plusなどの高度なモデルを大規模に無料で使用できるようにします。プロジェクトはストラテジーパターンとアダプターパターンに基づくモジュラーアーキテクチャを採用し、アカウントプール管理、インテリジェントポーリング、自動フェイルオーバー、ヘルスチェック機構を内蔵し、99.9%のサービス可用性を保証します。

> [!NOTE]
> **🎉 重要なマイルストーン**
>
> - Ruan Yifeng先生による[週刊359号](https://www.ruanyifeng.com/blog/2025/08/weekly-issue-359.html)での推薦に感謝します
>
> **📅 バージョン更新ログ**
>
> - **2025.10.18** - Kiroオープン登録、新規アカウントに500クレジット付与、Claude Sonnet 4.5を完全サポート
> - **2025.09.01** - Qwen Code CLIを統合、`qwen3-coder-plus`モデルサポートを追加
> - **2025.08.29** - アカウントプール管理機能をリリース、マルチアカウントポーリング、インテリジェントフェイルオーバー、自動ダウングレード戦略をサポート
>   - 設定方法：config.jsonに`PROVIDER_POOLS_FILE_PATH`パラメータを追加
>   - 参考設定：[provider_pools.json](./provider_pools.json.example)

---

## 💡 コアアドバンテージ

### 🎯 統一アクセス、ワンストップ管理
*   **マルチモデル統一インターフェース**：標準OpenAI互換プロトコルを通じて、一度の設定でGemini、Claude、GPT、Qwen Code、Kimi K2、GLM-4.6などの主流大規模モデルにアクセス
*   **柔軟な切り替えメカニズム**：起動パラメータ、Pathルーティング、環境変数の3つの方法で動的にモデルを切り替え、異なるシナリオのニーズに対応
*   **ゼロコスト移行**：OpenAI API仕様と完全互換、Cherry-Studio、NextChat、Clineなどのツールを変更なしで使用可能
*   **マルチプロトコルインテリジェント変換**：OpenAI、Claude、Geminiの3大プロトコル間のインテリジェント変換をサポートし、クロスプロトコルモデル呼び出しを実現
    *   OpenAIプロトコルでClaudeモデルを呼び出す：`claude-custom`または`claude-kiro-oauth`プロバイダーを使用
    *   OpenAIプロトコルでGeminiモデルを呼び出す：`gemini-cli-oauth`プロバイダーを使用
    *   ClaudeプロトコルでGeminiモデルを呼び出す：`gemini-cli-oauth`プロバイダーを使用
    *   ClaudeプロトコルでOpenAIモデルを呼び出す：`openai-custom`または`openai-qwen-oauth`プロバイダーを使用

### 🚀 制限を突破、効率を向上
*   **公式制限の回避**：OAuth認証メカニズムを利用して、Geminiなどの無料APIのレート制限と割り当て制限を効果的に突破
*   **無料高度モデル**：Kiro APIモードでClaude Sonnet 4.5を無料使用、Qwen OAuthモードでQwen3 Coder Plusを使用し、使用コストを削減
*   **インテリジェントアカウントプールスケジューリング**：マルチアカウントポーリング、自動フェイルオーバー、設定ダウングレードをサポートし、99.9%のサービス可用性を保証

### 🛡️ 安全で制御可能、データ透明
*   **フルチェーンログ記録**：すべてのリクエストとレスポンスデータをキャプチャし、監査とデバッグをサポート
*   **プライベートデータセット構築**：ログデータに基づいて専用トレーニングデータセットを迅速に構築
*   **システムプロンプト管理**：オーバーライドと追加の2つのモードをサポートし、統一された基本指示と個別拡張の完璧な組み合わせを実現

### 🔧 開発者フレンドリー、拡張が容易
*   **モジュラーアーキテクチャ**：ストラテジーパターンとアダプターパターンに基づき、新しいモデルプロバイダーの追加はわずか3ステップ
*   **完全なテストカバレッジ**：統合テストと単体テストのカバレッジ90%+、コード品質を保証
*   **コンテナ化デプロイ**：Dockerサポートを提供、ワンクリックデプロイ、クロスプラットフォーム実行
*   **MCPプロトコルサポート**：Model Context Protocolと完全互換、機能を簡単に拡張

---

## 📑 クイックナビゲーション

- [🐳 Docker デプロイ](https://aiproxy.justlikemaki.vip/ja/docs/installation/docker-deployment.html)
- [🎨 モデルプロトコルとプロバイダー関係図](#-モデルプロトコルとプロバイダー関係図)
- [🔧 使用方法](#-使用方法)
- [🚀 プロジェクト起動パラメータ](#-プロジェクト起動パラメータ)
- [📄 オープンソースライセンス](#-オープンソースライセンス)
- [🙏 謝辞](#-謝辞)
- [⚠️ 免責事項](#-免責事項)

---

## 🎨 モデルプロトコルとプロバイダー関係図

本プロジェクトは異なるプロトコルを通じて複数のモデルプロバイダーをサポートします。以下はそれらの関係の概要です：

*   **OpenAIプロトコル (P_OPENAI)**：`openai-custom`、`gemini-cli-oauth`、`claude-custom`、`claude-kiro-oauth`、`openai-qwen-oauth`モデルプロバイダーによって実装。
*   **Claudeプロトコル (P_CLAUDE)**：`claude-custom`、`claude-kiro-oauth`、`gemini-cli-oauth`、`openai-custom`、`openai-qwen-oauth`モデルプロバイダーによって実装。
*   **Geminiプロトコル (P_GEMINI)**：`gemini-cli-oauth`モデルプロバイダーによって実装。

詳細な関係図：

  ```mermaid

   graph TD
       subgraph Core_Protocols["コアプロトコル"]
           P_OPENAI[OpenAI Protocol]
           P_GEMINI[Gemini Protocol]
           P_CLAUDE[Claude Protocol]
       end

       subgraph Supported_Model_Providers["サポートモデルプロバイダー"]
           MP_OPENAI[openai-custom]
           MP_GEMINI[gemini-cli-oauth]
           MP_CLAUDE_C[claude-custom]
           MP_CLAUDE_K[claude-kiro-oauth]
           MP_QWEN[openai-qwen-oauth]
       end

       P_OPENAI ---|サポート| MP_OPENAI
       P_OPENAI ---|サポート| MP_QWEN
       P_OPENAI ---|サポート| MP_GEMINI
       P_OPENAI ---|サポート| MP_CLAUDE_C
       P_OPENAI ---|サポート| MP_CLAUDE_K

       P_GEMINI ---|サポート| MP_GEMINI

       P_CLAUDE ---|サポート| MP_CLAUDE_C
       P_CLAUDE ---|サポート| MP_CLAUDE_K
       P_CLAUDE ---|サポート| MP_GEMINI
       P_CLAUDE ---|サポート| MP_OPENAI
       P_CLAUDE ---|サポート| MP_QWEN

       style P_OPENAI fill:#f9f,stroke:#333,stroke-width:2px
       style P_GEMINI fill:#ccf,stroke:#333,stroke-width:2px
       style P_CLAUDE fill:#cfc,stroke:#333,stroke-width:2px

  ```

---

## 🔧 使用方法

### 📋 コア機能

#### MCPプロトコルサポート
本プロジェクトは**Model Context Protocol (MCP)**と完全互換で、MCPをサポートするクライアントとシームレスに統合し、強力な機能拡張を実現します。

#### マルチモーダル入力機能
画像、ドキュメントなど様々なタイプの入力をサポートし、よりリッチなインタラクティブ体験とより強力なアプリケーションシナリオを提供します。

#### 最新モデルサポート
以下の最新大規模モデルをシームレスにサポート、[`config.json`](./config.json)で対応するOpenAIまたはClaude互換インターフェースを設定するだけで使用可能：
*   **Kimi K2** - 月之暗面の最新フラッグシップモデル
*   **GLM-4.5** - 智譜AIの最新バージョン
*   **Qwen Code** - アリババ通義千問のコード専用モデル

---

### 🔐 認証設定ガイド

#### Gemini CLI OAuth設定
1. **OAuth認証情報の取得**：[Google Cloud Console](https://console.cloud.google.com/)にアクセスしてプロジェクトを作成し、Gemini APIを有効化
2. **初回認証**：Geminiサービス使用後、コマンドラインにGoogle認証ページが表示されるので、ページをブラウザにコピーして認証し、コマンドラインに戻る
3. **認証情報の保存**：認証成功後、`oauth_creds.json`ファイルが自動生成され、`~/.gemini`ディレクトリに保存される
4. **プロジェクト設定**：有効なGoogle CloudプロジェクトIDを提供する必要があり、起動パラメータ`--project-id`で指定可能

#### Qwen Code OAuth設定
1. **初回認証**：サービス起動後、システムが自動的にブラウザで認証ページを開く
2. **認証情報の保存**：認証成功後、`oauth_creds.json`ファイルが自動生成され、`~/.qwen`ディレクトリに保存される
3. **推奨パラメータ**：最良の結果を得るために公式デフォルトパラメータを使用
   ```json
   {
     "temperature": 0,
     "top_p": 1
   }
   ```

#### Kiro API設定
1. **環境準備**：[Kiroクライアントをダウンロードしてインストール](https://aibook.ren/archives/kiro-install)
2. **認証完了**：クライアントでアカウントにログインし、`kiro-auth-token.json`認証情報ファイルを生成
3. **ベストプラクティス**：**Claude Code**との併用を推奨、最適な体験を得られる
4. **重要なお知らせ**：Kiroサービス使用ポリシーが更新されました、最新の使用制限と条件については公式ウェブサイトをご確認ください

#### OpenAI Responses API
*   **適用シナリオ**：Codexなど、OpenAI Responses APIを使用した構造化対話が必要なシナリオに適用
*   **設定方法**：
    *   方法1：[`config.json`](./config.json)で`MODEL_PROVIDER`を`openaiResponses-custom`に設定
    *   方法2：起動パラメータ`--model-provider openaiResponses-custom`を使用
    *   方法3：パスルーティング`/openaiResponses-custom`を使用
*   **必須パラメータ**：有効なAPIキーとベースURLを提供

---

### 🔄 モデルプロバイダー切り替え

本プロジェクトは2つの柔軟なモデル切り替え方法を提供し、異なる使用シナリオのニーズに対応します。

#### 方法1：起動パラメータ切り替え

コマンドラインパラメータでデフォルトのモデルプロバイダーを指定：

```bash
# Geminiプロバイダーを使用
node src/api-server.js --model-provider gemini-cli-oauth --project-id your-project-id

# Claude Kiroプロバイダーを使用
node src/api-server.js --model-provider claude-kiro-oauth

# Qwenプロバイダーを使用
node src/api-server.js --model-provider openai-qwen-oauth
```

**利用可能なモデルプロバイダー識別子**：
- `openai-custom` - 標準OpenAI API
- `claude-custom` - 公式Claude API
- `gemini-cli-oauth` - Gemini CLI OAuth
- `claude-kiro-oauth` - Kiro Claude OAuth
- `openai-qwen-oauth` - Qwen Code OAuth
- `openaiResponses-custom` - OpenAI Responses API

#### 方法2：Pathルーティング切り替え（推奨）

APIリクエストパスでプロバイダー識別子を指定して即座に切り替え：

| ルートパス | 説明 | 使用ケース |
|---------|------|---------|
| `/claude-custom` | 設定ファイルのClaude APIを使用 | 公式Claude API呼び出し |
| `/claude-kiro-oauth` | Kiro OAuth経由でClaudeにアクセス | Claude Sonnet 4.5の無料使用 |
| `/openai-custom` | OpenAIプロバイダーでリクエストを処理 | 標準OpenAI API呼び出し |
| `/gemini-cli-oauth` | Gemini CLI OAuth経由でアクセス | Gemini無料制限の突破 |
| `/openai-qwen-oauth` | Qwen OAuth経由でアクセス | Qwen Code Plusの使用 |
| `/openaiResponses-custom` | OpenAI Responses API | 構造化対話シナリオ |

**使用例**：
```bash
# Cline、Kiloなどのプログラミングエージェントで設定
API_ENDPOINT=http://localhost:3000/claude-kiro-oauth

# 直接API呼び出し
curl http://localhost:3000/gemini-cli-oauth/v1/chat/completions \
  -H "Content-Type: application/json" \
  -d '{"model":"gemini-2.0-flash-exp","messages":[...]}'
```

---

### 📁 認証ファイル保存パス

各サービスの認証情報ファイルのデフォルト保存場所：

| サービス | デフォルトパス | 説明 |
|------|---------|------|
| **Gemini** | `~/.gemini/oauth_creds.json` | OAuth認証情報 |
| **Kiro** | `~/.aws/sso/cache/kiro-auth-token.json` | Kiro認証トークン |
| **Qwen** | `~/.qwen/oauth_creds.json` | Qwen OAuth認証情報 |

> **説明**：`~`はユーザーホームディレクトリを表します（Windows: `C:\Users\ユーザー名`、Linux/macOS: `/home/ユーザー名`または`/Users/ユーザー名`）
>
> **カスタムパス**：設定ファイルの関連パラメータまたは環境変数でカスタム保存場所を指定可能

---

## 🚀 プロジェクト起動パラメータ

本プロジェクトは豊富なコマンドラインパラメータ設定をサポートし、必要に応じてサービスの動作を柔軟に調整できます。以下は機能別にグループ化されたすべての起動パラメータの詳細説明です：

### 🔧 サーバー設定パラメータ

| パラメータ | タイプ | デフォルト値 | 説明 |
|------|------|--------|------|
| `--host` | string | localhost | サーバーリッスンアドレス |
| `--port` | number | 3000 | サーバーリッスンポート |
| `--api-key` | string | 123456 | 認証用APIキー |

### 🤖 モデルプロバイダー設定パラメータ

| パラメータ | タイプ | デフォルト値 | 説明 |
|------|------|--------|------|
| `--model-provider` | string | gemini-cli-oauth | AIモデルプロバイダー、選択可能値：openai-custom, claude-custom, gemini-cli-oauth, claude-kiro-oauth, openai-qwen-oauth |

### 🧠 OpenAI互換プロバイダーパラメータ

| パラメータ | タイプ | デフォルト値 | 説明 |
|------|------|--------|------|
| `--openai-api-key` | string | null | OpenAI APIキー（`model-provider`が`openai-custom`の場合必須） |
| `--openai-base-url` | string | null | OpenAI APIベースURL（`model-provider`が`openai-custom`の場合必須） |

### 🖥️ Claude互換プロバイダーパラメータ

| パラメータ | タイプ | デフォルト値 | 説明 |
|------|------|--------|------|
| `--claude-api-key` | string | null | Claude APIキー（`model-provider`が`claude-custom`の場合必須） |
| `--claude-base-url` | string | null | Claude APIベースURL（`model-provider`が`claude-custom`の場合必須） |

### 🔐 Gemini OAuth認証パラメータ

| パラメータ | タイプ | デフォルト値 | 説明 |
|------|------|--------|------|
| `--gemini-oauth-creds-base64` | string | null | Gemini OAuth認証情報のBase64文字列（`model-provider`が`gemini-cli-oauth`の場合オプション、`--gemini-oauth-creds-file`と二者択一） |
| `--gemini-oauth-creds-file` | string | null | Gemini OAuth認証情報JSONファイルパス（`model-provider`が`gemini-cli-oauth`の場合オプション、`--gemini-oauth-creds-base64`と二者択一） |
| `--project-id` | string | null | Google CloudプロジェクトID（`model-provider`が`gemini-cli-oauth`の場合必須） |

### 🎮 Kiro OAuth認証パラメータ

| パラメータ | タイプ | デフォルト値 | 説明 |
|------|------|--------|------|
| `--kiro-oauth-creds-base64` | string | null | Kiro OAuth認証情報のBase64文字列（`model-provider`が`claude-kiro-oauth`の場合オプション、`--kiro-oauth-creds-file`と二者択一） |
| `--kiro-oauth-creds-file` | string | null | Kiro OAuth認証情報JSONファイルパス（`model-provider`が`claude-kiro-oauth`の場合オプション、`--kiro-oauth-creds-base64`と二者択一） |

### 🐼 Qwen OAuth認証パラメータ

| パラメータ | タイプ | デフォルト値 | 説明 |
|------|------|--------|------|
| `--qwen-oauth-creds-file` | string | null | Qwen OAuth認証情報JSONファイルパス（`model-provider`が`openai-qwen-oauth`の場合必須） |

### 🔄 OpenAI Responses APIパラメータ

| パラメータ | タイプ | デフォルト値 | 説明 |
|------|------|--------|------|
| `--model-provider` | string | openaiResponses-custom | モデルプロバイダー、OpenAI Responses API使用時は`openaiResponses-custom`に設定 |
| `--openai-api-key` | string | null | OpenAI APIキー（`model-provider`が`openaiResponses-custom`の場合必須） |
| `--openai-base-url` | string | null | OpenAI APIベースURL（`model-provider`が`openaiResponses-custom`の場合必須） |

### 📝 システムプロンプト設定パラメータ

| パラメータ | タイプ | デフォルト値 | 説明 |
|------|------|--------|------|
| `--system-prompt-file` | string | input_system_prompt.txt | システムプロンプトファイルパス |
| `--system-prompt-mode` | string | overwrite | システムプロンプトモード、選択可能値：overwrite（上書き）、append（追加） |

### 📊 ログ設定パラメータ

| パラメータ | タイプ | デフォルト値 | 説明 |
|------|------|--------|------|
| `--log-prompts` | string | none | プロンプトログモード、選択可能値：console（コンソール）、file（ファイル）、none（なし） |
| `--prompt-log-base-name` | string | prompt_log | プロンプトログファイルベース名 |

### 🔄 リトライ機構パラメータ

| パラメータ | タイプ | デフォルト値 | 説明 |
|------|------|--------|------|
| `--request-max-retries` | number | 3 | APIリクエスト失敗時の自動リトライ最大回数 |
| `--request-base-delay` | number | 1000 | 自動リトライ間の基本遅延時間（ミリ秒）、各リトライ後に遅延が増加 |

### ⏰ 定期タスクパラメータ

| パラメータ | タイプ | デフォルト値 | 説明 |
|------|------|--------|------|
| `--cron-near-minutes` | number | 15 | OAuthトークンリフレッシュタスクの間隔時間（分） |
| `--cron-refresh-token` | boolean | true | OAuthトークン自動リフレッシュタスクを有効にするか |

### 🎯 アカウントプール設定パラメータ

| パラメータ | タイプ | デフォルト値 | 説明 |
|------|------|--------|------|
| `--provider-pools-file` | string | null | プロバイダーアカウントプール設定ファイルパス |

### 使用例

```bash
# 基本的な使用法
node src/api-server.js

# ポートとAPIキーを指定
node src/api-server.js --port 8080 --api-key my-secret-key

# OpenAIプロバイダーを使用
node src/api-server.js --model-provider openai-custom --openai-api-key sk-xxx --openai-base-url https://api.openai.com/v1

# Claudeプロバイダーを使用
node src/api-server.js --model-provider claude-custom --claude-api-key sk-ant-xxx --claude-base-url https://api.anthropic.com

# OpenAI Responses APIプロバイダーを使用
node src/api-server.js --model-provider openaiResponses-custom --openai-api-key sk-xxx --openai-base-url https://api.openai.com/v1

# Geminiプロバイダーを使用（Base64認証情報）
node src/api-server.js --model-provider gemini-cli-oauth --gemini-oauth-creds-base64 eyJ0eXBlIjoi... --project-id your-project-id

# Geminiプロバイダーを使用（認証情報ファイル）
node src/api-server.js --model-provider gemini-cli-oauth --gemini-oauth-creds-file /path/to/credentials.json --project-id your-project-id

# システムプロンプトを設定
node src/api-server.js --system-prompt-file custom-prompt.txt --system-prompt-mode append

# ログを設定
node src/api-server.js --log-prompts console
node src/api-server.js --log-prompts file --prompt-log-base-name my-logs

# 完全な例
node src/api-server.js \
  --host 0.0.0.0 \
  --port 3000 \
  --api-key my-secret-key \
  --model-provider gemini-cli-oauth \
  --project-id my-gcp-project \
  --gemini-oauth-creds-file ./credentials.json \
  --system-prompt-file ./custom-system-prompt.txt \
  --system-prompt-mode overwrite \
  --log-prompts file \
  --prompt-log-base-name api-logs
```
---

## 📄 オープンソースライセンス

本プロジェクトは [**GNU General Public License v3 (GPLv3)**](https://www.gnu.org/licenses/gpl-3.0) オープンソースライセンスに従います。詳細はルートディレクトリの `LICENSE` ファイルをご覧ください。

## 🙏 謝辞

本プロジェクトの開発は公式Google Gemini CLIから大きなインスピレーションを受け、Cline 3.18.0版 `gemini-cli.ts` の一部のコード実装を参考にしました。ここにGoogle公式チームとCline開発チームの優れた仕事に心より感謝申し上げます！

## 🌟 Star History

[![Star History Chart](https://api.star-history.com/svg?repos=justlovemaki/AIClient-2-API&type=Timeline)](https://www.star-history.com/#justlovemaki/AIClient-2-API&Timeline)

---

## ⚠️ 免責事項

### 使用リスクの注意

本プロジェクト（AIClient-2-API）は学習と研究目的のみです。ユーザーは本プロジェクト使用時、すべてのリスクを自己負担する必要があります。作者は本プロジェクトの使用により生じた直接的、間接的、結果的損失について一切の責任を負いません。

### サードパーティサービスの責任説明

本プロジェクトはAPIプロキシツールであり、AIモデルサービスを提供していません。すべてのAIモデルサービスは対応するサードパーティプロバイダー（Google、OpenAI、Anthropicなど）により提供されます。ユーザーが本プロジェクトを通じてこれらのサードパーティサービスにアクセスする際は、各サードパーティサービスの利用規約とポリシーを遵守する必要があります。作者はサードパーティサービスの可用性、品質、セキュリティ、合法性について責任を負いません。

### データプライバシー説明

本プロジェクトはローカルで実行され、ユーザーのデータを収集またはアップロードしません。ただし、ユーザーは本プロジェクト使用時、APIキーやその他の機密情報を保護することに注意する必要があります。定期的にAPIキーを確認・更新し、安全でないネットワーク環境での本プロジェクトの使用を避けることを推奨します。

### 法的コンプライアンスの注意

ユーザーは本プロジェクト使用時、所在国/地域の法律法規を遵守する必要があります。本プロジェクトを違法な目的に使用することは厳禁です。ユーザーが法律法規に違反したことによるいかなる結果も、ユーザー自身がすべての責任を負うものとします。
