# 第6回 解答

## 演習

- `--list-tools` で見えたツール名と、第3回（`--mcp` なし）との違い：search_glossary,get_lecture_summary,make_quiz,save_learning_log,glossary_search_glossary(`--mcp`を付けた場合はこの1つのToolだけが表示された。ツールの説明文等は同じだが、ツール名の前にサーバ名が付いている。)
- `--mcp --trace` で見えたツール呼び出し（ツール名と引数）と、`requests` の回数：glossary_search_glossary({'query': '3レベル'})、requestの回数は2回。
- MCP サーバーに公開したツールと、その説明文：get_lecture_summary、指定した回（1始まりの整数）の講義の要点を返す。「第3回では何を学ぶ？」のように、回の内容や関係を聞かれたときに使う。
- fetch サーバーを足したときのツール呼び出し（ツール名と引数）：[fetch_fetch]
  Fetches a URL from the internet and optionally extracts its contents as markdown.
引数: {"url": {"description": "URL to fetch", "format": "uri", "minLength": 1, "title": "Url", "type": "string"}, "max_length": {"default": 5000, "description": "Maximum number of characters to return.", "maximum": 999999, "minimum": 1, "title": "Max Length", "type": "integer"}, "start_index": {"default": 0, "description": "On return output starting at this character index, useful if a previous fetch was truncated and more context is required.", "minimum": 0, "title": "Start Index", "type": "integer"}, "raw": {"default": false, "description": "Get the actual HTML content of the requested page, without simplification.", "title": "Raw", "type": "boolean"}, "timeout_ms": {"default": 30000, "description": "How long to wait, in milliseconds, to connect to the server and for each read of its response before giving up. Raise it for a slow server or a large download; lower it to fail fast.", "maximum": 600000, "minimum": 100, "title": "Timeout Ms", "type": "integer"}}

## 宿題

- 取り組んだレベル：発展
- やったこと：同じ用語集サーバーを **Copilot Chat**（VS Code の MCP クライアント）から使う。このため、新規にjsonファイル（.mcp.json)をリポジトリ直下に作成した（そのため、共有範囲はプロジェクト（workspace)単位となる）。VSCの公式ドキュメント（https://code.visualstudio.com/docs/agents/reference/mcp-configuration#_configure-mcp-for-copilot）によると、MCPの構成の注意書きとして、.vscode/mcp.jsonは使えないとの注意書きがあったためファイル名は上記の形式にした。）
jsonファイル記載の内容は次のとおり。
{
  "mcpServers": {
    "aie-glossary": {
      "type": "stdio",
      "command": "uv",
      "args": ["run", "python", "-m", "app.mcp_server"]
    }
  }
}
これまで使用していたmcp_servers.jsonと比較して、typeの指定が必要となるが、今回はstdioとしており、httpとはしていない。mcp_severs.jsonでawsで接続する場合と異なり、外部サーバーを使わないため、URLの指定もない。また、ほかに、command,args,envの指定が考えられるが、今回は、APIを使う必要がなかったため、envは指定していない。commandの書き方は、mcp_servers,jsonと同じくuvとしており、pythonを活用して実行環境を整えることとしている。

copilotを通じてaie-glossary MCPサーバー（ローカルサーバー）に接続し、利用可能なツールを確認するように依頼したところ、aie-glossary-search_glossaryとaie-glossary-get_lecture_summaryの２件を取得できた。そののち実際にエージェントがToolを使用するか確認するため「AIE2026 の宿題の 3 レベルとは？」と質問し、ツール（search_glossary)が使用されたことを確認した。

- 結果：エージェントに「AIE2026 の宿題の 3 レベルとは？」と質問した結果は以下のとおり。
search_glossary
Completed with input: {
  "query": "宿題 3 レベル"
}

AIE2026 の宿題は、次の3段階です。

- **基礎**：講義内容の確認
- **実装**：自分でコードを書く
- **発展**：調査や試行を行う

どれか1つに取り組めば完了で、原則として採点はしません。（第1回で扱われる用語です）

他方で、`uv run python -m app.agent --mcp --trace` のコマンドを使い、Pydantic AIエージェントに聞いた場合には、  glossary_search_glossary({'query': '3レベル'})を用いて次の回答をした。
[model] gemini-3.5-flash-lite
[tools] MCP サーバー（app/mcp_servers.json）
AIE2026における「宿題の3レベル」とは、各回の宿題として用意されている以下の3段階の構成のことです。

1. **基礎**：講義内容の確認
2. **実装**：自分でコードを書く
3. **発展**：調査や試行

これら3つのレベルの中から**どれか1つ**に取り組めば、その回の宿題は完了となります。なお、原則として宿題の採点は行われません。

第1回

- 気づき・疑問：今回の発展では無料版のco-pilotエージェントを使ってローカルツールを使用できるようにし、問題なく使用ができていた。これを応用すれば、エージェントを使った自社内の独自開発のツールの使用ができる点で便利だとは思うが、元々のエージェントが優秀な場合に、ローカル環境で作成したツールを使わせる必要があるのかが疑問に思えた。他方で、一つのツールを複数のエージェント間で共有して使えるように設定することで、一定のメリットが見込まれる場合もあり得るのかと考えた。
