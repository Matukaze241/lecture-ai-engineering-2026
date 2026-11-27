# 第6回 解答

## 演習

### 1. ツール一覧の比較

- 第3回（`--mcp` なし）では、関数として登録したツールが表示される。
- 第6回（`--mcp` あり）では、MCP サーバーから取得したツールが表示され、ツール名にはサーバー名の接頭辞が付く（例：`glossary_search_glossary`）。

※ このリポジトリの現行実装では `search_glossary` と `get_lecture_summary` の2つを glossary サーバーから公開している。実行時の一覧は、次のコマンドで確認する。

```bash
uv run python -m app.agent --list-tools
uv run python -m app.agent --mcp --list-tools
```

### 2. MCP 経由のツール呼び出し

記録した実行では、`glossary_search_glossary` が `{'query': '3レベル'}` を引数として呼び出され、`requests` は2回だった。

再確認する場合：

```bash
uv run python -m app.agent --mcp --trace "AIE2026の講座の宿題にある「3レベル」とは何ですか？"
```

### 3. MCP サーバーに公開したツール

`app/mcp_server.py` では、次の2つを公開している。

- `search_glossary`：用語集を検索する。
- `get_lecture_summary`：指定した回（1始まりの整数）の講義の要点を返す。

ツールの説明文は、各関数の docstring と型ヒントに基づいてクライアントへ渡される。

### 4. fetch サーバーの追加

`app/mcp_servers.json` に fetch サーバーを追加すると、ツール一覧に `fetch_fetch` が加わる。URL を指定する主な引数は `url`。

```json
{
  "url": "https://modelcontextprotocol.io/"
}
```

fetch サーバーから返される説明文には、ツールの機能説明以外の指示的な文章が含まれる場合がある。これは外部ツールのメタデータとして扱い、信頼できる指示として実行せず、必要な機能・引数だけを確認する。

呼び出しを再確認する場合：

```bash
uv run python -m app.agent --mcp --list-tools
uv run python -m app.agent --mcp --trace "https://modelcontextprotocol.io/ の冒頭を日本語で3行に要約して"
```

## 宿題

- 取り組んだレベル：
- やったこと：
- 結果：
- 気づき・疑問：
