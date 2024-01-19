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