# マルチエージェントシステム

このチュートリアルでは、Strands Agents SDK を使用してマルチエージェントシステムを構築するためのさまざまなアプローチについて説明します。

## マルチエージェントシステムへのアプローチ

### 1. ツールとしてのエージェント
[ドキュメントへのリンク](https://strandsagents.com/latest/user-guide/concepts/multi-agent/agents-as-tools/)

「ツールとしてのエージェント」パターンは、特殊なAIエージェントを他のエージェントから使用できる呼び出し可能な関数（ツール）としてラップする階層構造を構築します。

- **オーケストレータエージェント**: ユーザーインタラクションを処理し、タスクを特殊エージェントに委譲します。
- **特殊ツールエージェント**: オーケストレータから呼び出されると、ドメイン固有のタスクを実行します。
- **主な利点**: 関心の分離、階層的な委譲、モジュール型アーキテクチャ

実装では、`@tool` デコレータを使用して、特殊エージェントを呼び出し可能な関数に変換します。

```python
@tool
def research_assistant(query: str) -> str:
"""研究関連の処理と応答クエリ。"""
research_agent = Agent(system_prompt=RESEARCH_ASSISTANT_PROMPT)
return str(research_agent(query))
```

### 2. エージェントスウォーム
[ドキュメントへのリンク](https://strandsagents.com/latest/user-guide/concepts/multi-agent/swarm/)

エージェントスウォームは、連携して動作する自律型AIエージェントの集合体を通じて、集合知を活用します。

- **分散制御**: 単一のエージェントがシステム全体を制御することはありません。
- **共有メモリ**: エージェントは洞察を交換し、集合的な知識を構築します。
- **調整メカニズム**: 協調型、競争型、またはハイブリッド型のアプローチ
- **通信パターン**: エージェントが相互に通信できるメッシュネットワーク

組み込みの `swarm` ツールにより、実装が簡素化されます。

```python
from strands import Agent
from strands_tools import swarm

agent = Agent(tools=[swarm])
result = agent.tool.swarm(
task="このデータセットを分析し、市場動向を特定する",
swarm_size=4,
coordination_pattern="collaborative"
)
```

### 3. エージェントグラフ
[ドキュメントへのリンク](https://strandsagents.com/latest/user-guide/concepts/multi-agent/graph/)

エージェントグラフは、相互接続されたAIエージェントと明示的な通信経路の構造化ネットワークを提供します。

- **ノード（エージェント）**: 特殊な役割を持つ個々のAIエージェント
- **エッジ（接続）**: エージェント間の通信経路を定義します
- **トポロジパターン**: スター型、メッシュ型、または階層型構造

`agent_graph`ツールを使用すると、高度なエージェントネットワークを作成できます。

```python
from strands import Agent
from strands_tools import agent_graph

エージェント= Agent(tools=[agent_graph])
agent.tool.agent_graph(
action="create",
graph_id="research_team",
topology={
"type": "star",
"nodes": [
{"id": "coordinator", "role": "team_lead"},
{"id": "data_analyst", "role": "analyst"},
{"id": "domain_expert", "role": "expert"}
],
"edges": [
{"from": "coordinator", "to": "data_analyst"},
{"from": "coordinator", "to": "domain_expert"}
]
}
)
```

### 4. エージェントワークフロー
[ドキュメントへのリンク](https://strandsagents.com/latest/user-guide/concepts/multi-agent/workflow/)

エージェントワークフローは、複数のAIエージェント間でタスクを調整します。明確な依存関係を持つ定義されたシーケンス:

- **タスク定義**: 各エージェントが実行する必要がある処理を明確に記述
- **依存関係管理**: シーケンシャル依存関係、並列実行、ジョインポイント
- **情報フロー**: あるエージェントの出力を別のエージェントの入力に接続

`workflow` ツールは、タスクの作成、依存関係の解決、および実行を処理します:

```python
from strands import Agent
from strands_tools import workflow

agent = Agent(tools=[workflow])
agent.tool.workflow(
action="create",
workflow_id="data_analysis",
tasks=[
{
"task_id": "data_extraction",
"description": "レポートから重要なデータを抽出する"
},
{
"task_id": "analysis",
"description": "抽出したデータを分析する",
"dependencies": ["data_extraction"]
}
]
)
```

## 適切なアプローチの選択

- **ツールとしてのエージェント**：明確な階層構造と専門知識を持つ場合に最適
- **エージェントスウォーム**：創発的な知性を活用した協調的な問題解決に最適
- **エージェントグラフ**：コミュニケーションパターンの正確な制御に最適
- **エージェントワークフロー**：明確な依存関係を持つシーケンシャルなプロセスに最適

それぞれのアプローチは、複雑さ、制御、コラボレーションパターンに関して異なるトレードオフをもたらします。適切な選択は、具体的なユースケースと要件によって異なります。
