## LangChainのユースケース

以下の2パターンで捉える。

- LLMを使ったアプリケーション開発に必要な部品を、抽象化された「モジュール」として提供している
    - アプリの例
        - ChatGPTのように会話できるチャットボット
        - 文章の要約ツール
        - 社内文書やPDFファイルへのQ&Aアプリ
        - AIエージェント
- 特定のユースケースに特化した機能を提供している

## LangChainのモジュールについて

大きく以下の6つに整理できる。

- Model I/O
    - Prompts
        - Prompts templates
        - Example selectors
    - Language models
        - LLMs
        - Chat models
    - Output parsers
- Data connection
    - Document loaders
    - Document transformers
        - Text splitters
        - Post retrieval
    - Text embedding models
    - Vector stores
    - Retrievers
- Chains
- Agents
    - Agent types
    - Tools
    - Toolkits
- Memory
- Callbacks

## Language Models

LangChainでの言語モデルの使用方法を提供するモジュール。
様々な言語モデルを共通のインターフェースで使用することができる。

要は、LLMをLangChain流で使えるようにするラッパー。

LangChainでは、Language modelsを「LLMs」と「Chat models」の大きく２種類に整理している。

### LLMs

LangCainの「LLMs」は、一つのテキストの入力に対して一つのテキストの出力を返す、典型的な大規模言語モデルを扱うモジュール。

### Chat models

OpenAIのChat Completions APIは、単に一つのテキストを入力するのではなく、チャット形式のやり取りを入力して応答を得るようになっている。

OpenAIのChat Completions APIに対応するために作られたLang ChainのモジュールがChat models。

Lang ChainでChat Completions APIを使う際は「ChatOpenAI」クラスを使用する。

### Callbackを使ったストリーミング

LangChainでは、Callback機能を使うことでストリーミング（一括ではなく少しずつ回答を得る）で応答を得ることができる。

## Prompts

LangChainにおけるプロンプトの扱いを抽象化したモジュール。

### PromptTemplate

PromptTemplateを使うとプロンプトをテンプレート化できる。

### ChatPromptTemplate

PromptTemplateをChat Completions APIの形式に対応させたのが、ChatPromptTemplate。

### Example selectors

Few-shotプロンプティングを使うと、LLMから期待する応答を得やすくなる。

Example selectorsは、Few-shotプロンプティングで使う例を選択する機能。

※Few-shotプロンプティング: モデルに例やデモンストレーションを提供し、文脈学習を通して質問や指示と回答のパターンを学習させる手法

## Output parsers

LLMに特定の形式で出力させて、その出力をプログラム的に扱いたい場合がある。

そこで使えるのがOutput Parsers。
LLMの応答をJSONなどの構造化されたデータに変換・解析する。

## Chains

ここから！！

LLMを使ったアプリケーションでは、単に
