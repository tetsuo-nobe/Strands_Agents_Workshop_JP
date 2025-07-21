# Strands SDK を使い始める

このフォルダには、Strands Agents のさまざまな機能を使い始めるための Jupyter Notebook の例が含まれています。

## 基礎
| 例 | 説明 | 紹介する機能 |
|--------|--------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------|
| F1 | [最初の Strands Agent の作成](01-fundamentals/01-first-agent) | エージェントの初期化、デフォルトツールの使用、カスタムツールの作成 |
| F2 | [モデルプロバイダー - OpenAI](01-fundamentals/02-model-providers/02-openai-model) | GPT 4.0 をモデルとしてエージェントを作成 |
| F2 | [モデルプロバイダー - Ollama](01-fundamentals/02-model-providers/01-ollama-model) | Ollama モデルを使用してエージェントを作成 |
| F3 | [AWS サービスとの接続](01-fundamentals/03-connecting-with-aws-services) | Amazon Bedrock ナレッジベースおよび Amazon DynamoDB への接続 |
| F4 | [ツール - MCP ツールの使用](01-fundamentals/04-tools/01-using-mcp-tools) | エージェントへの MCP ツール呼び出しの統合 |
| F4 | [ツール - カスタムツール](01-fundamentals/04-tools/02-custom-tools) | エージェントでのカスタムツールの作成と使用 |
| F5 | [エージェントからのレスポンスのストリーミング](01-fundamentals/05-streaming-agent-response) | 非同期イテレータまたはコールバック (ストリームハンドラー) を使用してエージェントのレスポンスをストリーミング |
| F6 | [Bedrock Guardrail の統合](01-fundamentals/06-guardrail-integration) | Amazon Bedrock Guardrail をエージェントに統合する |
| F7 | [エージェントへのメモリの追加](01-fundamentals/07-memory-persistent-agents) | メモリと Web 検索ツールを使用したパーソナルアシスタント |
| F8 | [可観測性と評価](01-fundamentals/08-observability-and-evaluation) | エージェントへの可観測性と評価の追加 |

## マルチエージェントシステム
| 例 | 説明 | 紹介されている機能 |
|---------|------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------|
| M1 | [エージェントをツールとして使用](02-multi-agent-systems/01-agent-as-tool) | エージェントをツールとして使用したマルチエージェントコラボレーションの例を作成する |
| M2 | [Swarm エージェントの作成](02-multi-agent-systems/02-swarm-agent) |連携して動作する複数の AI エージェントで構成されるマルチエージェントシステムを作成します |
| M3 | [グラフエージェントの作成](02-multi-agent-systems/03-graph-agent) | 定義された通信パターンを持つ、特殊な AI エージェントの構造化ネットワークを作成します |

## デプロイメント
| 例 | 説明 | 紹介する機能 |
|---------|------------------------------------------------------------------|------------------------------------------------------------------------------------------------|
| D1 | [AWS Lambda デプロイメント](03-deployment/01-lambda-deployment) | AWS Lambda 関数へのエージェントのデプロイ |
| D2 | [AWS Fargate デプロイメント](03-deployment/02-fargate-deployment) | AWS Fargate へのエージェントのデプロイ |