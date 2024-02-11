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

LLMを使ったアプリケーションでは、単にLLMに入力して出力を得て終わりではなく、処理を連鎖的に繋ぎたいことが多い。

- PromptTemplateのテンプレートを穴埋めして、その結果をLanguage modelsに与え、その結果をPythonのオブジェクトとして得たい
- LLMの出力結果をもとに、SQLを実行して、データ分析させてみたい

Chainsを使うことで、様々な処理を連鎖させることができる。

LangChainには様々なChainがあるが、とりあえず押さえたいのはLLMChain。
LLMChainは、PromptTemplateとLanguage model、OutputParserをつなぐ。

また、ChainとChainを接続するChainも存在する。SimpleSequentialChainを使うと、ChainとChainを直列に連結できる。

### Chainの内部の動きを確認する

```py
import langchain

langchain.verbose = True # フォーマットされたプロンプトなどが表示される
langchain.debug = True # LangChainの挙動が最も詳細に出力される
```

## Memory

会話履歴の保存などに関する便利な機能を提供するのがLangChainのMemory。

### Memoryの保存先について

デフォルトだとメモリ上に保存される。
-> プロセスが停止した場合は会話履歴は保持されない

いくつかの保存先をサポートしている。
-> SQLite、Redisなど

## Data connection（P98）

LLMと外部のデータを接続するための機能。

Data connectionを使うことで、たとえば社内文書に対してQ&Aが可能なチャットボットを実装することができる。

### RAG（Retrieval Augmented Generation）について

GPT-3.5やGPT-4は、本稿執筆時点では2021年9月までの公開されている情報しか知らない。
しかし、もっと新しい情報やプライベートな情報を使わせたいことは多い。

そこで、プロンプトに文脈（context）を入れる方法が考えられる。

質問に関する文書の内容をcontextに含めることで、LLMが本来知らないことを回答してもらうことができる（ただし、LLMにはトークン数の最大値の制限があるため、あらゆるデータをcontextに入れることはできない）

そこで、入力に関係しそうな文書を検索してcontextに含める手法がある。

文書をOPenAIのEmbedding APIなどでベクトル化しておいて、入力にベクトルが近い文書を検索して、contextに含める手法はRA（Retrieval Augmented Generation）と呼ばれる。

文書はあらかじめ用意したデータベースから検索することもあれば、Googleなどの検索エンジンでWeb上から検索することも考えられる。

LangChainのData connectionでは、特にVector storeを使い、文書をベクトル化して保存しておいて、入力のテキストとベクトルの近い文書を検索してcontextに含めて使う方法が提供される。

RAGワークフロー
-> RAGワークフローは、モデルを使って情報を検索（retrieval）する工程と、モデルを使って回答を生成（generation）する工程を組み合わせて利用することで、知識に対する回答を、文章スタイルなどを指定して生成する方法

※テキストのベクトル化: テキストを数値の配列に変換する

### Data connectionの概要

RAGに使えるLangChainのモジュールが「Data connection」。

Data connectionには次の5種類の機能がある。

- Document loaders
    - データソースからドキュメントを読み込む
    - LangChainは多くのDocumentLoaderを提供している
        - GitLoader
            - GitHubリポジトリからファイルを読み込む
            - TODO: 自分の技術メモでRAGを作る場合に使えそう
- Document transformers
    - ドキュメントに何かしらの変換をかける
- Text embedding models
    - ドキュメントをベクトル化する
- Vector stores
    - ベクトル化したドキュメントの保存先
- Retrievers
    - 入力したテキストと関連するドキュメントを検索する

### RetrievalQAとは？

LangChainに実装されているRetrievalQAは、大量の（ベクトル化された）テキストデータの中からユーザーの質問に合致する情報を迅速に検索し、LLMを使用してその情報を基に回答を生成するためのツール。

特定の知識ベースやドキュメントセット（VectorStore）をベースにして回答をしたい場合に有効。

参考: https://qiita.com/mashmoeiar11/items/214984400e3452615ea5

## Agents

Chainsは、固定的な処理の流れを実現するもの。
一方で、どんな処理を行うべき（どのツールを使うべき）か、LLMに選択して動いて欲しい場合がある。

そのような動作を実現できるのがLangChainのAgents。

## 参考資料

- [LangChainのエコシステムをまとめたGitHubリポジトリ](https://github.com/kyrolabs/awesome-langchain)
