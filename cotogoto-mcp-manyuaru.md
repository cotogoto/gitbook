# CotoGoto MCP マニュアル

## 1. CotoGoto MCP サーバー概要

### 1.1 概要

CotoGoto MCP サーバーは、Model Context Protocol（MCP）を利用して CotoGoto および NOBY の機能を AI クライアントから利用できるようにする拡張サーバーです。

MCP に対応したクライアントに設定することで、AI から以下の操作が可能になります。

* CotoGotoとの会話
* 作業開始・完了通知
* 休憩開始・終了通知

---

## 2. ダウンロード

MCP サーバーは以下のページから取得できます。

[https://github.com/cotogoto/cotogoto-mcp-server/releases](https://github.com/cotogoto/cotogoto-mcp-server/releases)

最新の `cotogoto-mcp-server.jar` をダウンロードしてください。

---

## 3. MCP クライアントへの設定

MCP の設定方法は以下の公式ドキュメントを参考にしてください。

[https://code.claude.com/docs/ja/mcp](https://code.claude.com/docs/ja/mcp)

---

## 4. 設定方法

### 4.1 設定例

MCP クライアントの設定ファイルに以下を追加します。

```json
{
  "mcpServers": {
    "cotogoto": {
      "command": "java",
      "args": [
        "-jar",
        "/path/to/cotogoto-mcp-server.jar"
      ],
      "env": {
        "COTOGOTO_API_KEY": "YOUR_API_KEY"
      }
    }
  }
}
```

---

### 4.2 設定項目

#### 4.2.1 COTOGOTO_API_KEY

CotoGoto API を利用するための認証キーです。

---

# 5. MCP ツール仕様

---

## 5.1 利用可能コマンド一覧

| No | Tool名                  | 概要     | パラメータ       | 動作内容                 |
| -- | ---------------------- | ------ | ----------- | -------------------- |
| 1  | cotogoto_conversation  | 会話を実行  | message（必須） | メッセージを API に送信し応答を取得 |
| 2  | cotogoto_work_start    | 作業開始通知 | なし          | 「作業開始」を送信            |
| 3  | cotogoto_work_complete | 作業完了通知 | なし          | 「作業完了」を送信            |
| 4  | cotogoto_break_start   | 休憩開始通知 | なし          | 「休憩開始」を送信            |
| 5  | cotogoto_break_end     | 休憩終了通知 | なし          | 「休憩終了」を送信            |

---

## 5.2 各コマンド詳細

---

### 5.2.1 cotogoto_conversation

#### 概要

CotoGoto または NOBY と会話を行います。
質問、相談、作業サポートなどに使用します。

#### Tool名

```
cotogoto_conversation
```

#### パラメータ

| 項目      | 必須 | 説明   |
| ------- | -- | ---- |
| message | 必須 | 会話内容 |

#### 使用例

```json
{
  "name": "cotogoto_conversation",
  "arguments": {
    "message": "今日の作業内容を整理してください"
  }
}
```

#### 動作

* メッセージを CotoGoto API に送信
* 応答メッセージを返却

---

### 5.2.2 cotogoto_work_start

#### 概要

作業開始を通知します。

#### Tool名

```
cotogoto_work_start
```

#### パラメータ

なし

#### 使用例

```json
{
  "name": "cotogoto_work_start",
  "arguments": {}
}
```

#### 動作

```
作業開始
```

を送信します。

---

### 5.2.3 cotogoto_work_complete

#### 概要

作業完了を通知します。

#### Tool名

```
cotogoto_work_complete
```

#### パラメータ

なし

#### 使用例

```json
{
  "name": "cotogoto_work_complete",
  "arguments": {}
}
```

#### 動作

```
作業完了
```

を送信します。

---

### 5.2.4 cotogoto_break_start

#### 概要

休憩開始を通知します。

#### Tool名

```
cotogoto_break_start
```

#### パラメータ

なし

#### 使用例

```json
{
  "name": "cotogoto_break_start",
  "arguments": {}
}
```

#### 動作

```
休憩開始
```

を送信します。

---

### 5.2.5 cotogoto_break_end

#### 概要

休憩終了を通知します。

#### Tool名

```
cotogoto_break_end
```

#### パラメータ

なし

#### 使用例

```json
{
  "name": "cotogoto_break_end",
  "arguments": {}
}
```

#### 動作

```
休憩終了
```

を送信します。

---

# 6. 応答仕様

すべてのツールは、CotoGoto API から返却されたメッセージを文字列として返します。

---

# 7. エラー仕様

以下の場合、エラーが発生する可能性があります。

1. APIキーが未設定の場合
2. APIから空レスポンスが返却された場合
3. APIレスポンス形式が不正な場合

---

# 8. 利用フロー

```
MCPクライアント
        ↓
ツール呼び出し
        ↓
CotoGoto MCP サーバー
        ↓
CotoGoto API
        ↓
応答返却
```

---

# 9. 想定利用用途

本 MCP サーバーは以下の用途で利用できます。

* AIエージェントによる作業記録
* 作業進捗管理
* 業務サポート会話
* 休憩管理
* 作業ログ生成

---

もしよければ次も対応できます：

* READMEとして公開向けに整形
* 企業内仕様書フォーマット化
* OpenAPI / MCP Tool Schema化
* 利用シーケンス図追加
* 初学者向けチュートリアル追加

どの方向に仕上げますか？
