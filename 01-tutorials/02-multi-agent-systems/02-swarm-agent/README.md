# Swarm エージェント

## 概要

Swarm パターンは、複数の AI エージェントが並列処理と共有メモリを通じて複雑なタスクを共同で実行することを可能にします。エージェントは、異なる調整戦略を用いて連携し、創発的な集合知を実現します。

スウォームの例を以下に示します。

![アーキテクチャ](./images/swarm_example.png)

## コーディネーションパターン

- **協調型**: エージェントは互いの洞察に基づいて構築します
- **競争型**: エージェントは独立して独自の解決策を模索します
- **ハイブリッド型**: 両方の戦略を組み合わせたバランスの取れたアプローチ

## 使用方法

```python
from strands import Agent
from strands_tools import swarm

agent = Agent(tools=[swarm])

# 協調型スウォームを作成します
result = agent.tool.swarm(
task="再生可能エネルギー源の環境影響を分析する",
swarm_size=5,
coordination_pattern="collaborative"
)

# 競争型パターンを使用します
result = agent.tool.swarm(
task="新しいスマートフォンのマーケティングキャンペーンコンセプトを生成する",
swarm_size=3,
調整パターン="競合"
)
```

## 主な機能

- **並列処理**: 複数のエージェントが同時に動作します
- **共有メモリ**: エージェント間の知識交換
- **フェーズベースの実行**: ソリューションの段階的な改良
- **エージェントの特化**: 調整パターンに基づいた役割のカスタマイズ

仕組みの詳細については、[こちら](https://strandsagents.com/latest/user-guide/concepts/multi-agent/swarm/#how-the-swarm-tool-works) をご覧ください。

## 使用例

- 複数の視点を必要とする複雑な問題解決
- 創造的なアイデア創出とブレインストーミング
- 包括的な調査と分析
- 複数の基準に基づく意思決定

詳細については、[ドキュメント](https://strandsagents.com/latest/user-guide/concepts/multi-agent/swarm/) をご覧ください。
