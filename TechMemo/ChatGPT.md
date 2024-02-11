## ChatGPTのAPIについて

ChatGPTのAPIには2種類ある。

- Completions API
- Chat Completions API

今は基本的にはChat Completions APIが使用されている。

Chat Completions APIは基本的にはステートレス。以前の会話履歴は保持していない。
以前の会話履歴も一緒にリクエストしてやる必要がある。

Chat Completions APIを使うには、OpenAIのライブラリを使用する。

`pip install openai`

## Function calling

Chat Completions APIの新機能。

利用可能な関数をLLMに伝えておいて、LLMに「関数を使いたい」という判断をさせる機能。
LLMが関数を実行する訳ではなく、LLMは「関数を使いたい」という応答を返してくるだけ。

処理の流れは以下の通り。

1. 利用可能な関数の一覧とともに、質問などのテキストを送信する
2. LLMが「関数を使いたい」という応答を返してきたら、Python等のプログラムで該当の関数を実行する
3. その実行結果を含めたリクエストを再度LLMに送ることで、最終的な回答を得る
