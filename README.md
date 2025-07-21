<div align="center">
<div>
<a href="https://strandsagents.com">
<img src="https://strandsagents.com/latest/assets/logo-auto.svg" alt="Strands Agents" width="55px" height="105px">
</a>
</div>

<h1>
Strands Agents サンプル
</h1>

<h2>
わずか数行のコードでAIエージェントを構築できるモデル駆動型アプローチ
</h2>


<p>
<a href="https://strandsagents.com/">ドキュメント</a>
◆ <a href="https://github.com/strands-agents/samples">サンプル</a>
◆ <a href="https://github.com/strands-agents/sdk-python">Python SDK</a>
◆ <a href="https://github.com/strands-agents/tools">ツール</a>
◆ <a href="https://github.com/strands-agents/agent-builder">エージェントビルダー</a>
◆ <a href="https://github.com/strands-agents/mcp-server">MCP Server</a>
</p>
</div>

Strands Agents サンプルリポジトリへようこそ！

<a href="https://strandsagents.com">Strands Agents</a> を使い始めるための、使いやすいサンプルをご覧ください。

**このリポジトリのサンプルは、[GitHub の Strands Agents の samples リポジトリの 01-tutorials](https://github.com/strands-agents/samples/tree/main/01-tutorials) のノートブックや LLM へのプロンプトなどを日本語化したものです。**

**このリポジトリのサンプルは、Linux のコンピュータまたは Amazon Sage Maker AI JupyterLab 環境で実行することを前提にしています。**
**このリポジトリのサンプルは、AWS リージョン us-west-2 の Amazon Bedrock のいくつかの基盤モデルを使用することを前提にしています。**

このリポジトリのサンプルは、**デモンストレーションおよび教育目的**のみに提供されています。概念や手法を示すものであり、**本番環境での直接使用を意図したものではありません**。本番環境で使用する前に、必ず適切な**セキュリティ**および**テスト**手順を適用してください。

## 📚 目次

- [📚 目次](#-table-of-contents)
- [🏁 はじめに](#-getting-started)
- [ステップ 1: 必要なパッケージのインストール](#step-1-install-required-packages)
- [ステップ 2: モデルプロバイダーのセットアップ](#step-2-setup-model-provider)
- [ステップ 3: 最初の Strands エージェントの構築](#step-3-build-your-first-strands-agent)
- [ステップ 4: SDK の使用開始](#step-4-getting-started-with-the-sdk)
- [ステップ 5: その他のサンプルの探索](#step-5-explore-more-samples)

## 🏁 はじめに

### ステップ 1: 必要なパッケージのインストール

```bash
pip install strands-agents
pip install strands-agents-tools
```

### ステップ 2: モデルプロバイダーの設定

[こちら](https://strandsagents.com/latest/user-guide/quickstart/#model-providers) の手順に従って、モデルプロバイダーとモデルアクセスを構成します。

### ステップ 3: 最初の Strands エージェントを作成する

```python
from strands import Agent, tool
from strands_tools import calculator, current_time, python_repl

@tool
def letter_counter(word: str, letter: str) -> int:
"""
単語内の特定の文字の出現回数をカウントします。
"""
if not isinstance(word, str) or not isinstance(letter, str):
return 0
if len(letter) != 1:
raise ValueError("'letter' パラメータは1文字である必要があります")
return word.lower().count(letter.lower())

agent = Agent(tools=[calculator, current_time, python_repl, letter_counter])

message = """
4つのリクエストがあります:

1. 正しい時刻はいつですか？今？
2. 3111696 / 74088 を計算してください。
3. 「strawberry」という単語には R がいくつ含まれているか教えてください 🍓
4. 今説明した内容を実行するスクリプトを出力してください！
出力する前に、Python ツールを使用してスクリプトが動作することを確認してください。
"""

agent(message)
```

### ステップ 4: SDK の使用開始

[01-tutorials](./01-tutorials/) ディレクトリから開始します。
[最初のエージェント](./01-tutorials/01-fundamentals/01-first-agent/) を作成し、コア機能を網羅したノートブックベースのサンプルを調べてください。




