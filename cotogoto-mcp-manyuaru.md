# CotoGoto MCP マニュアル

## CotoGoto MCP サーバー

### ■ 概要

CotoGoto MCP サーバーは、Model Context Protocol（MCP）を利用して CotoGoto および NOBY の機能を AI クライアントから利用できるようにする拡張サーバーです。

MCP に対応したクライアントに設定することで、AI から以下の操作が可能になります。

* CotoGotoとの会話
* 作業開始・完了通知
* 休憩開始・終了通知

***

### ■ ダウンロード

MCP サーバーは以下のページから取得できます。

👉 [https://github.com/cotogoto/cotogoto-mcp-server/releases](https://github.com/cotogoto/cotogoto-mcp-server/releases)

最新の `cotogoto-mcp-server.jar` をダウンロードしてください。

***

### ■ MCP クライアントへの設定

MCP の設定方法は以下の公式ドキュメントを参考にしてください。

👉 [https://code.claude.com/docs/ja/mcp](https://code.claude.com/docs/ja/mcp)

***

### ■ 設定例

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

***

### ■ 設定項目

#### COTOGOTO\_API\_KEY

CotoGoto API を利用するための認証キーです。

***

### ■ 利用可能コマンド（MCP Tools）

本 MCP サーバーでは、以下のツールを利用できます。

***

#### cotogoto\_conversation

#### ■ 概要

CotoGoto または NOBY と会話を行います。

質問、相談、作業サポートなどを行う際に使用します。

***

#### ■ Tool 名

```
cotogoto_conversation
```

***

#### ■ パラメータ

| 項目      | 必須 | 説明   |
| ------- | -- | ---- |
| message | 必須 | 会話内容 |

***

#### ■ 使用例

```json
{
  "name": "cotogoto_conversation",
  "arguments": {
    "message": "今日の作業内容を整理してください"
  }
}
```

***

#### ■ 動作

* メッセージを CotoGoto API に送信
* 応答メッセージを返却

***

## cotogoto\_work\_start

#### ■ 概要

作業開始を CotoGoto または NOBY に通知します。

***

#### ■ Tool 名

```
cotogoto_work_start
```

***

#### ■ パラメータ

なし

***

#### ■ 使用例

```json
{
  "name": "cotogoto_work_start",
  "arguments": {}
}
```

***

#### ■ 動作

以下のメッセージを送信します。

```
作業開始
```

***

## cotogoto\_work\_complete

#### ■ 概要

作業完了を CotoGoto または NOBY に通知します。

***

#### ■ Tool 名

```
cotogoto_work_complete
```

***

#### ■ パラメータ

なし

***

#### ■ 使用例

```json
{
  "name": "cotogoto_work_complete",
  "arguments": {}
}
```

***

#### ■ 動作

以下のメッセージを送信します。

```
作業完了
```

***

## cotogoto\_break\_start

#### ■ 概要

休憩開始を通知します。

***

#### ■ Tool 名

```
cotogoto_break_start
```

***

#### ■ パラメータ

なし

***

### ■ 使用例

```json
{
  "name": "cotogoto_break_start",
  "arguments": {}
}
```

***

### ■ 動作

以下のメッセージを送信します。

```
休憩開始
```

***

## cotogoto\_break\_end

### ■ 概要

休憩終了を通知します。

***

### ■ Tool 名

```
cotogoto_break_end
```

***

### ■ パラメータ

なし

***

### ■ 使用例

```json
{
  "name": "cotogoto_break_end",
  "arguments": {}
}
```

***

### ■ 動作

以下のメッセージを送信します。

```
休憩終了
```

***

## ■ 応答内容

すべてのツールは、CotoGoto API から返却されたメッセージを文字列として返します。

***

## ■ エラーについて

以下の場合、エラーが発生する可能性があります。

* APIキーが未設定
* APIから空のレスポンスが返却された場合
* APIレスポンス形式が不正な場合

***

## ■ 利用フロー

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

***

## ■ 想定利用用途

本 MCP サーバーは以下の用途で利用できます。

* AIエージェントによる作業記録
* 作業進捗管理
* 業務サポート会話
* 休憩管理
* 作業ログ生成
