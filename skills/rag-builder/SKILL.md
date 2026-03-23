# RAG Builder Skill

> 🧠 **OpenClaw 技能包：RAG 系统构建器**
>
> 快速构建生产级 RAG（检索增强生成）应用，支持多种向量数据库和嵌入模型

**版本**: v0.1.0  
**作者**: OpenClaw AI Engineering Skills  
**许可证**: MIT

---

## 📋 目录

- [技能描述](#技能描述)
- [快速开始](#快速开始)
- [配置说明](#配置说明)
- [使用示例](#使用示例)
- [API 参考](#api-参考)
- [最佳实践](#最佳实践)
- [故障排查](#故障排查)

---

## 技能描述

### 核心功能

`rag-builder` 是 OpenClaw 的技能包，用于快速构建和部署 RAG（Retrieval-Augmented Generation）系统。它提供：

- 📦 **一键初始化** - 5 分钟搭建 RAG 原型
- 🔌 **多后端支持** - Chroma, Milvus, Pinecone, Weaviate
- 🎯 **智能检索** - 密集检索、稀疏检索、混合检索
- ⚡ **性能优化** - 缓存、批处理、并行查询
- 📊 **评估工具** - 内置检索质量评估

### 适用场景

| 场景 | 描述 | 示例 |
|------|------|------|
| 文档问答 | 基于文档库的智能问答 | 产品手册、内部 Wiki |
| 知识检索 | 企业知识库查询 | 客服知识、技术文档 |
| 订单检索 | 业务数据自然语言查询 | 电商订单、CRM 记录 |
| 代码助手 | 代码库智能检索 | 代码搜索、API 文档 |

### 技术栈

```
┌─────────────────────────────────────────┐
│            RAG Builder 架构              │
├─────────────────────────────────────────┤
│  LLM Layer                               │
│  ├── OpenAI (gpt-4o, gpt-4o-mini)       │
│  ├── Anthropic (claude-3.5-sonnet)      │
│  └── 本地模型 (ollama, vllm)            │
├─────────────────────────────────────────┤
│  Embedding Layer                         │
│  ├── OpenAI (text-embedding-3-small)    │
│  ├── Cohere (embed-multilingual-v3)     │
│  └── 本地模型 (bge-m3, m3e)             │
├─────────────────────────────────────────┤
│  Vector Store Layer                      │
│  ├── Chroma (轻量级，开发首选)           │
│  ├── Milvus (高性能，生产推荐)           │
│  ├── Pinecone (托管服务)                │
│  └── Weaviate (图 + 向量)               │
├─────────────────────────────────────────┤
│  Retrieval Strategies                    │
│  ├── 密集检索 (Dense Retrieval)         │
│  ├── 稀疏检索 (BM25)                    │
│  ├── 混合检索 (Hybrid)                  │
│  └── 多向量检索 (Multi-vector)          │
└─────────────────────────────────────────┘
```

---

## 快速开始

### 前置要求

```bash
# Python 版本
Python 3.10+

# OpenClaw 版本
openclaw >= 0.5.0

# 系统依赖
pip install chromadb openai tiktoken
```

### 5 分钟上手

```python
# 1. 在 OpenClaw 中加载技能
from openclaw.skills import rag_builder

# 2. 初始化 RAG 系统
rag = rag_builder.init(
    name="my-rag-system",
    vector_store="chroma",
    embedding_model="text-embedding-3-small",
    llm_model="gpt-4o"
)

# 3. 添加文档
rag.add_documents([
    "docs/product_manual.pdf",
    "docs/faq.md",
    "docs/api_reference.md"
])

# 4. 开始查询
response = rag.query("如何重置订单状态？")
print(response.answer)
```

### 使用 OpenClaw 命令

```bash
# 创建新的 RAG 项目
openclaw rag create my-project

# 添加文档
openclaw rag add my-project ./docs/

# 查询
openclaw rag query my-project "如何重置订单状态？"

# 评估检索质量
openclaw rag evaluate my-project --test-set test_questions.json
```

---

## 配置说明

### 基础配置

创建 `config.yaml` 配置文件：

```yaml
# RAG Builder 配置文件

# 系统名称
name: my-rag-system

# LLM 配置
llm:
  provider: openai
  model: gpt-4o
  temperature: 0.7
  max_tokens: 2048
  api_key: ${OPENAI_API_KEY}  # 支持环境变量

# 嵌入模型配置
embedding:
  provider: openai
  model: text-embedding-3-small
  dimensions: 1536
  api_key: ${OPENAI_API_KEY}

# 向量数据库配置
vector_store:
  type: chroma  # chroma | milvus | pinecone | weaviate
  persist_directory: ./chroma_db
  collection_name: documents

# 检索配置
retrieval:
  strategy: hybrid  # dense | sparse | hybrid
  top_k: 5
  score_threshold: 0.7
  rerank: true
  rerank_model: bge-reranker-large

# 缓存配置
cache:
  enabled: true
  type: redis  # memory | redis
  ttl: 3600  # 秒

# 日志配置
logging:
  level: INFO
  file: ./logs/rag.log
```

### 环境变量

```bash
# 必需的环境变量
export OPENAI_API_KEY="sk-..."
export CHROMA_DB_PATH="./chroma_db"

# 可选的环境变量
export REDIS_URL="redis://localhost:6379"
export LOG_LEVEL="INFO"
```

### 高级配置

```yaml
# 高级检索配置
advanced_retrieval:
  # 查询扩展
  query_expansion:
    enabled: true
    num_variants: 3
  
  # 上下文压缩
  context_compression:
    enabled: true
    target_length: 1000
  
  # 多跳检索
  multi_hop:
    enabled: false
    max_hops: 2
  
  # 元数据过滤
  metadata_filter:
    enabled: true
    fields:
      - source
      - date
      - category

# 性能优化
performance:
  # 批处理
  batch_size: 32
  # 并行查询
  parallel_queries: 4
  # 结果缓存
  cache_size: 1000
```

---

## 使用示例

### 示例 1: 文档问答系统

```python
from openclaw.skills import rag_builder

# 初始化
rag = rag_builder.init(
    name="doc-qa-system",
    config="config.yaml"
)

# 批量添加文档
documents = [
    {"path": "docs/manual_ch1.pdf", "metadata": {"section": "intro"}},
    {"path": "docs/manual_ch2.pdf", "metadata": {"section": "setup"}},
    {"path": "docs/manual_ch3.pdf", "metadata": {"section": "usage"}},
]
rag.add_documents(documents)

# 多轮对话查询
conversation = []
while True:
    user_query = input("Q: ")
    if user_query.lower() == "quit":
        break
    
    response = rag.query(
        query=user_query,
        conversation_history=conversation,
        include_sources=True
    )
    
    print(f"A: {response.answer}")
    print(f"来源：{response.sources}")
    
    conversation.append({"role": "user", "content": user_query})
    conversation.append({"role": "assistant", "content": response.answer})
```

### 示例 2: 订单检索系统（LogiNexus 案例）

```python
from openclaw.skills import rag_builder

# 初始化订单检索 RAG
order_rag = rag_builder.init(
    name="order-retrieval",
    vector_store="milvus",  # 生产环境推荐 Milvus
    embedding_model="bge-m3",  # 中文优化
    llm_model="gpt-4o"
)

# 导入订单数据（从数据库）
orders = [
    {
        "id": "ORD-2026-001",
        "customer": "张三",
        "products": ["iPhone 15", "AirPods Pro"],
        "status": "已发货",
        "date": "2026-03-20",
        "amount": 9999
    },
    # ... 更多订单
]

# 将订单转换为文档格式
for order in orders:
    doc_text = f"""
    订单号：{order['id']}
    客户：{order['customer']}
    商品：{', '.join(order['products'])}
    状态：{order['status']}
    日期：{order['date']}
    金额：¥{order['amount']}
    """
    order_rag.add_text(
        text=doc_text,
        metadata={"order_id": order["id"], "customer": order["customer"]}
    )

# 自然语言查询
queries = [
    "张三最近的订单是什么？",
    "显示所有已发货的订单",
    "金额超过 5000 的订单有哪些？"
]

for query in queries:
    response = order_rag.query(
        query=query,
        metadata_filter={"customer": "张三"} if "张三" in query else None
    )
    print(f"查询：{query}")
    print(f"结果：{response.answer}\n")
```

### 示例 3: 带评估的 RAG 系统

```python
from openclaw.skills import rag_builder

# 初始化
rag = rag_builder.init(name="evaluated-rag")

# 添加文档
rag.add_documents(["docs/"])

# 准备测试集
test_set = [
    {
        "query": "如何重置密码？",
        "expected_answer": "在设置页面点击忘记密码...",
        "expected_sources": ["docs/account.md"]
    },
    {
        "query": "支持哪些支付方式？",
        "expected_answer": "我们支持支付宝、微信、银联...",
        "expected_sources": ["docs/payment.md"]
    }
]

# 运行评估
evaluation = rag.evaluate(test_set)

# 查看评估结果
print(f"检索准确率：{evaluation.retrieval_precision:.2%}")
print(f"答案相关性：{evaluation.answer_relevance:.2%}")
print(f"整体得分：{evaluation.overall_score:.2f}/100")

# 详细分析
for result in evaluation.detailed_results:
    print(f"\n查询：{result.query}")
    print(f"检索命中：{result.retrieved_docs}")
    print(f"答案质量：{result.answer_score}")
```

### 示例 4: 高级检索策略

```python
from openclaw.skills import rag_builder

rag = rag_builder.init(name="advanced-rag")

# 混合检索（密集 + 稀疏）
response = rag.query(
    query="如何优化数据库查询性能？",
    strategy="hybrid",
    top_k=10,
    rerank=True
)

# 带查询扩展
response = rag.query(
    query="数据库慢查询",
    query_expansion=True,  # 自动生成相关查询变体
    num_expansion_variants=3
)

# 多跳检索（复杂推理）
response = rag.query(
    query="找出所有购买过 iPhone 的客户中，谁的订单金额最高？",
    multi_hop=True,
    max_hops=2
)

# 带元数据过滤
response = rag.query(
    query="最新的订单",
    metadata_filter={
        "date": {"$gte": "2026-03-01"}
    }
)
```

---

## API 参考

### 核心类

#### `RAGBuilder`

主类，用于构建和管理 RAG 系统。

```python
class RAGBuilder:
    def __init__(self, config: dict | str)
    def add_documents(self, paths: list[str | dict]) -> None
    def add_text(self, text: str, metadata: dict = None) -> None
    def query(self, query: str, **kwargs) -> RAGResponse
    def evaluate(self, test_set: list[dict]) -> EvaluationResult
    def clear(self) -> None
    def save(self, path: str) -> None
    def load(self, path: str) -> None
```

#### `RAGResponse`

查询响应对象。

```python
class RAGResponse:
    answer: str                    # 生成的答案
    sources: list[SourceDocument]  # 参考文档
    confidence: float              # 置信度 (0-1)
    latency_ms: int                # 响应时间
    tokens_used: dict              # token 使用统计
```

#### `EvaluationResult`

评估结果对象。

```python
class EvaluationResult:
    retrieval_precision: float     # 检索准确率
    retrieval_recall: float        # 检索召回率
    answer_relevance: float        # 答案相关性
    faithfulness: float            # 忠实度
    overall_score: float           # 整体得分
    detailed_results: list         # 详细结果
```

### 配置参数

| 参数 | 类型 | 默认值 | 描述 |
|------|------|--------|------|
| `name` | str | - | RAG 系统名称 |
| `vector_store` | str | "chroma" | 向量数据库类型 |
| `embedding_model` | str | "text-embedding-3-small" | 嵌入模型 |
| `llm_model` | str | "gpt-4o" | LLM 模型 |
| `top_k` | int | 5 | 返回文档数量 |
| `score_threshold` | float | 0.7 | 相似度阈值 |
| `rerank` | bool | False | 是否重排序 |

---

## 最佳实践

### 1. 文档预处理

```python
# ✅ 推荐：分块策略
rag.add_documents(
    paths=["docs/"],
    chunk_size=500,      # 每块 500 tokens
    chunk_overlap=50,    # 重叠 50 tokens
    separators=["\n\n", "\n", "。", "！", "？"]  # 智能分割
)

# ✅ 推荐：添加丰富元数据
rag.add_text(
    text=document_content,
    metadata={
        "source": "product_manual",
        "chapter": "3",
        "date": "2026-03-20",
        "version": "v2.1"
    }
)
```

### 2. 查询优化

```python
# ✅ 推荐：使用具体查询
# 不好
rag.query("订单")

# 好
rag.query("2026 年 3 月张三的订单状态")

# ✅ 推荐：利用元数据过滤
rag.query(
    query="最新订单",
    metadata_filter={"date": {"$gte": "2026-03-01"}}
)
```

### 3. 性能优化

```python
# ✅ 启用缓存
config = {
    "cache": {
        "enabled": True,
        "type": "redis",
        "ttl": 3600
    }
}

# ✅ 批量处理
documents = load_large_dataset()
rag.add_documents(documents, batch_size=32)

# ✅ 异步查询
responses = await rag.query_batch(queries, parallel=4)
```

### 4. 评估与迭代

```python
# ✅ 定期评估
test_set = load_test_questions()
evaluation = rag.evaluate(test_set)

if evaluation.retrieval_precision < 0.8:
    # 调整检索策略
    rag.update_config({"retrieval": {"top_k": 10}})
    # 重新评估
    evaluation = rag.evaluate(test_set)
```

---

## 故障排查

### 常见问题

#### Q1: 检索结果不相关

**原因**: 嵌入模型不匹配或文档分块不当

**解决方案**:
```python
# 尝试不同的嵌入模型
rag = rag_builder.init(embedding_model="bge-m3")  # 中文优化

# 调整分块大小
rag.add_documents(paths, chunk_size=300, chunk_overlap=30)

# 启用重排序
rag.query(query, rerank=True)
```

#### Q2: 答案包含幻觉

**原因**: 检索文档质量低或 LLM 温度过高

**解决方案**:
```python
# 降低温度
rag = rag_builder.init(llm_config={"temperature": 0.3})

# 提高相似度阈值
rag.query(query, score_threshold=0.8)

# 要求引用来源
rag.query(query, require_sources=True)
```

#### Q3: 响应速度慢

**原因**: 向量数据库未优化或网络延迟

**解决方案**:
```python
# 启用缓存
config = {"cache": {"enabled": True}}

# 使用本地向量数据库
rag = rag_builder.init(vector_store="chroma", persist_directory="./local_db")

# 减少 top_k
rag.query(query, top_k=3)
```

#### Q4: 内存占用过高

**原因**: 文档量过大或嵌入维度过高

**解决方案**:
```python
# 使用量化嵌入
rag = rag_builder.init(embedding_model="bge-m3-quantized")

# 分批次添加文档
for batch in document_batches:
    rag.add_documents(batch)
    rag.save()  # 定期保存

# 使用外部向量数据库
rag = rag_builder.init(vector_store="milvus", connection="localhost:19530")
```

### 调试模式

```python
# 启用详细日志
rag = rag_builder.init(logging_level="DEBUG")

# 查看检索过程
response = rag.query(query, debug=True)
print(response.debug_info)
# 输出：
# - 原始查询
# - 查询扩展（如有）
# - 检索到的文档及分数
# - 重排序结果（如有）
# - 最终 prompt
# - LLM 响应
```

---

## 贡献与反馈

- 🐛 **报告问题**: [GitHub Issues](https://github.com/openclaw/ai-engineering-skills/issues)
- 💡 **功能建议**: [GitHub Discussions](https://github.com/openclaw/ai-engineering-skills/discussions)
- 📖 **文档改进**: 欢迎提交 PR

---

## 许可证

MIT License - 详见 [LICENSE](../../LICENSE)

---

*最后更新：2026-03-23*
