# Strands SDK を使ったツールの作成

このガイドでは、Strands エージェント用のツールを作成するさまざまな方法について説明します。

## ツールの作成方法

### 1. `@tool` デコレータの使用

ツールを作成する最も簡単な方法は、Python 関数で `@tool` デコレータを使用することです。

```python
from strands import tool

@tool
def my_tool(param1: str, param2: int) -> str:
"""
ツールの機能の説明。

引数:
param1: 第 1 パラメータの説明
param2: 第 2 パラメータの説明

戻り値:
戻り値の説明
"""
# ダミー実装
return f"Result: {param1}, {param2}"
```

注: この方法では、ツールの説明とパラメータ検証のための型ヒントとして Python の docstring を使用します。

### 2. TOOL_SPEC ディクショナリの使用

ツール定義をより細かく制御するには、TOOL_SPEC ディクショナリを使用します。

```python
from strands.types.tools import ToolResult, ToolUse
from entering import Any

TOOL_SPEC = {
"name": "my_tool",
"description": "このツールの機能の説明",
"inputSchema": {
"json": {
"type": "object",
"properties": {
"param1": {
"type": "string",
"description": "最初のパラメータの説明"
},
"param2": {
"type": "integer",
"description": "2番目のパラメータの説明",
"default": 2
}
},
"required": ["param1"]
}
}

# 関数名はツール名と一致する必要があります
def my_tool(tool: ToolUse, **kwargs: Any) -> ToolResult:
tool_use_id = tool["toolUseId"]
param1 = tool["input"].get("param1")
param2 = tool["input"].get("param2", 2)

# ツールの実装
result = f"Result: {param1}, {param2}"

return {
"toolUseId": tool_use_id,
"status": "success",
"content": [{"text": result}]
}
```

このアプローチにより、入力スキーマの定義をより細かく制御できます。ここでは、成功状態とエラー状態の明示的な処理を定義できます。

注: これは Amazon Bedrock Converse API 形式に準拠しています。

#### 使用方法

ツールは、関数または別のファイルから次のようにインポートできます。

```python
agent = Agent(tools=[my_tool])
# または
agent = Agent(tools=["./my_tool.py"])
```

### 3. MCP (モデルコンテキストプロトコル) ツールの使用

モデルコンテキストプロトコルを使用して外部ツールを統合することもできます。

```python
from mcp import StdioServerParameters, stdio_client
from strands.tools.mcp import MCPClient

# MCP サーバーに接続します。
mcp_client = MCPClient(
lambda: stdio_client(
StdioServerParameters(
command="uvx", args=["awslabs.aws-documentation-mcp-server@latest"]
)
)
)

# エージェント内のツールを使用する
mcp_client を使用:
tools = mcp_client.list_tools_sync()
agent = Agent(tools=tools)
```

この方法では、MCP を介して外部ツールプロバイダーに接続するため、異なるサーバーのツールを使用できます。 stdio と HTTP の両方のトランスポートをサポートしています。

## ベストプラクティス

1. **ツールの命名**: ツールには、明確で説明的な名前を付けます。
2. **ドキュメント**: ツールの機能とパラメータについて詳細な説明を提供します。
3. **エラー処理**: ツールに適切なエラー処理を組み込みます。
4. **パラメータ検証**: 処理前に入力を検証します。
5. **戻り値**: エージェントが理解しやすい構造化データを返します。

## 例

このディレクトリにあるサンプルノートブックをご覧ください。
- [MCP ツールの使用](01-using-mcp-tools/mcp-agent.ipynb): MCP ツールをエージェントに統合する方法を学びます。
- [カスタムツール](02-custom-tools/custom-tools-with-strands-agents.ipynb): カスタムツールの作成と使用方法を学びます。

詳細については、[Strands ツール] をご覧ください。ドキュメント](https://strandsagents.com/0.1.x/user-guide/concepts/tools/python-tools/)を参照してください。
