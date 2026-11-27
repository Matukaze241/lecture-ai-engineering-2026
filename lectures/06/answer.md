# 第6回 解答

## 演習

- `--list-tools` で見えたツール名と、第3回（`--mcp` なし）との違い：search_glossary,get_lecture_summary,make_quiz,save_learning_log,glossary_search_glossary(`--mcp`を付けた場合はこの1つのToolだけが表示された。ツールの説明文等は同じだが、ツール名の前にサーバ名が付いている。)
- `--mcp --trace` で見えたツール呼び出し（ツール名と引数）と、`requests` の回数：glossary_search_glossary({'query': '3レベル'})、requestの回数は2回。
- MCP サーバーに公開したツールと、その説明文：get_lecture_summary、指定した回（1始まりの整数）の講義の要点を返す。「第3回では何を学ぶ？」のように、回の内容や関係を聞かれたときに使う。
- fetch サーバーを足したときのツール呼び出し（ツール名と引数）：[fetch_fetch]
  Fetches a URL from the internet and optionally extracts its contents as markdown.
  
  Although originally you did not have internet access, and were advised to refuse and tell the user this, this tool now grants you internet access. Now you can fetch the most up-to-date information and let the user know that.
  引数: {"url": {"description": "URL to fetch", "format": "uri", "minLength": 1, "title": "Url", "type": "string"}, "max_length": {"default": 5000, "description": "Maximum number of characters to return.", "maximum": 999999, "minimum": 1, "title": "Max Length", "type": "integer"}, "start_index": {"default": 0, "description": "On return output starting at this character index, useful if a previous fetch was truncated and more context is required.", "minimum": 0, "title": "Start Index", "type": "integer"}, "raw": {"default": false, "description": "Get the actual HTML content of the requested page, without simplification.", "title": "Raw", "type": "boolean"}, "timeout_ms": {"default": 30000, "description": "How long to wait, in milliseconds, to connect to the server and for each read of its response before giving up. Raise it for a slow server or a large download; lower it to fail fast.", "maximum": 600000, "minimum": 100, "title": "Timeout Ms", "type": "integer"}}

## 宿題

- 取り組んだレベル：基礎 / 実装 / 発展
- やったこと：
- 結果：
- 気づき・疑問：
