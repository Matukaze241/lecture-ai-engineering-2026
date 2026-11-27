# 第6回 解答

## 演習

- `--list-tools` で見えたツール名と、第3回（`--mcp` なし）との違い：search_glossary,get_lecture_summary,make_quiz,save_learning_log,glossary_search_glossary(`--mcp`を付けた場合はこの1つのToolだけが表示された。ツールの説明文等は同じだが、ツール名の前にサーバ名が付いている。)
- `--mcp --trace` で見えたツール呼び出し（ツール名と引数）と、`requests` の回数：glossary_search_glossary({'query': '3レベル'})、requestの回数は2回。
- MCP サーバーに公開したツールと、その説明文：get_lecture_summary、指定した回（1始まりの整数）の講義の要点を返す。「第3回では何を学ぶ？」のように、回の内容や関係を聞かれたときに使う。
- fetch サーバーを足したときのツール呼び出し（ツール名と引数）：[fetch_fetch]

## 宿題

- 取り組んだレベル：基礎 / 実装 / 発展
- やったこと：
- 結果：
- 気づき・疑問：
