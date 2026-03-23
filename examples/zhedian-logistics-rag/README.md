# LogiNexus RAG 订单检索系统

> 📦 基于 RAG 的电商订单自然语言检索系统
>
> **难度**: ⭐⭐⭐ | **学时**: 8 小时 | **核心技能**: RAG、混合检索、元数据过滤

---

## 📋 目录

- [项目概述](#项目概述)
- [快速开始](#快速开始)
- [系统架构](#系统架构)
- [功能说明](#功能说明)
- [代码结构](#代码结构)
- [使用示例](#使用示例)
- [性能优化](#性能优化)
- [扩展方向](#扩展方向)

---

## 项目概述

### 背景

LogiNexus 是一个电商订单管理系统，每天有数万订单需要查询。传统 SQL 查询需要业务人员熟悉数据库结构，效率低下。

### 解决方案

构建 RAG（检索增强生成）系统，让业务人员可以用自然语言查询订单：

- ❌ 传统方式：`SELECT * FROM orders WHERE customer_name='张三' AND status='已发货' AND date >= '2026-03-01'`
- ✅ RAG 方式："张三最近已发货的订单"

### 核心功能

- [x] 自然语言订单查询
- [x] 多条件组合检索
- [x] 查询建议与补全
- [x] 检索结果解释
- [x] 查询日志与分析

---

## 快速开始

### 前置要求

- Python 3.10+
- Docker & Docker Compose
- OpenAI API Key（或本地 LLM）

### 一键启动

```bash
# 1. 克隆项目
cd examples/log nexus-rag

# 2. 配置环境变量
cp .env.example .env
# 编辑 .env，填入 OPENAI_API_KEY

# 3. 启动服务
docker-compose up -d

# 4. 导入示例数据
python scripts/import_sample_data.py

# 5. 访问 Web 界面
open http://localhost:8501
```

### 测试查询

```bash
# CLI 查询
python scripts/query.py "张三 3 月份的订单"

# 预期输出:
# 找到 3 个订单:
# 1. ORD-2026-0301 - 张三 - ¥1,299 - 已发货
# 2. ORD-2026-0315 - 张三 - ¥5,999 - 配送中
# 3. ORD-2026-0320 - 张三 - ¥899 - 已完成
```

---

## 系统架构

```
┌─────────────────────────────────────────────────────────┐
│                      用户界面                            │
│              (Streamlit Web App)                         │
└─────────────────────────────────────────────────────────┘
                            ↓
┌─────────────────────────────────────────────────────────┐
│                   RAG 服务层                             │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐     │
│  │ 查询理解    │  │ 混合检索    │  │ 答案生成    │     │
│  │ (Query      │  │ (Hybrid     │  │ (LLM        │     │
│  │  Parser)    │  │  Search)    │  │  Generator) │     │
│  └─────────────┘  └─────────────┘  └─────────────┘     │
└─────────────────────────────────────────────────────────┘
              ↓                    ↓
    ┌─────────────────┐  ┌─────────────────┐
    │  向量数据库      │  │  关系数据库      │
    │  (Chroma)       │  │  (PostgreSQL)   │
    │  - 订单嵌入      │  │  - 订单详情      │
    │  - 语义检索      │  │  - 精确查询      │
    └─────────────────┘  └─────────────────┘
```

### 技术栈

| 组件 | 技术选型 | 说明 |
|------|----------|------|
| 向量数据库 | Chroma | 轻量级，开发友好 |
| 关系数据库 | PostgreSQL | 订单数据存储 |
| 嵌入模型 | text-embedding-3-small | OpenAI |
| LLM | gpt-4o | OpenAI |
| Web 框架 | Streamlit | 快速构建界面 |
| 检索策略 | 混合检索 | 密集 + 稀疏 |

---

## 功能说明

### 1. 查询理解

```python
# 自然语言 → 结构化查询
输入："张三 3 月份已发货的订单，金额超过 1000 元"

输出:
{
    "customer": "张三",
    "date_range": {"start": "2026-03-01", "end": "2026-03-31"},
    "status": "已发货",
    "amount_min": 1000
}
```

### 2. 混合检索

```python
# 向量检索（语义相似度）
vector_results = chroma_collection.query(
    query_embeddings=[query_embedding],
    n_results=20
)

# 元数据过滤（精确条件）
filtered_results = [
    r for r in vector_results
    if matches_filters(r, filters)
]

# 重排序（提高精度）
reranked_results = reranker.rank(
    query=query,
    documents=filtered_results
)
```

### 3. 答案生成

```python
# 构建 prompt
prompt = f"""
基于以下订单信息回答问题：

{context_orders}

问题：{user_query}

要求:
1. 只基于提供的订单信息回答
2. 列出相关订单的关键信息
3. 如果没有相关订单，明确说明
"""

# 生成答案
response = llm.generate(prompt)
```

---

## 代码结构

```
log nexus-rag/
├── README.md                 # 本文件
├── docker-compose.yml        # Docker 配置
├── requirements.txt          # Python 依赖
├── .env.example              # 环境变量模板
│
├── src/
│   ├── __init__.py
│   ├── config.py             # 配置管理
│   ├── query_parser.py       # 查询解析
│   ├── retriever.py          # 检索引擎
│   ├── generator.py          # 答案生成
│   └── rag_service.py        # RAG 服务主类
│
├── data/
│   ├── sample_orders.csv     # 示例订单数据
│   └── import_script.py      # 数据导入脚本
│
├── scripts/
│   ├── import_sample_data.py # 导入示例数据
│   ├── query.py              # CLI 查询工具
│   └── evaluate.py           # 评估脚本
│
├── tests/
│   ├── test_query_parser.py
│   ├── test_retriever.py
│   └── test_rag_service.py
│
└── app/
    ├── main.py               # Streamlit 应用
    └── components/           # UI 组件
```

---

## 使用示例

### Web 界面查询

启动服务后访问 http://localhost:8501:

1. 在搜索框输入自然语言查询
2. 查看检索结果和答案
3. 点击订单查看详情
4. 导出查询结果

### CLI 查询

```bash
# 简单查询
python scripts/query.py "张三的订单"

# 复杂查询
python scripts/query.py "3 月份北京地区金额超过 5000 元的订单"

# 带导出
python scripts/query.py "已发货的订单" --output results.csv
```

### Python API

```python
from src.rag_service import RAGService

# 初始化服务
rag = RAGService(
    chroma_path="./chroma_db",
    db_url="postgresql://user:pass@localhost/orders"
)

# 查询
result = rag.query("张三最近的订单")

print(f"找到 {len(result.orders)} 个订单")
print(f"答案：{result.answer}")
print(f"来源：{result.sources}")
```

---

## 性能优化

### 检索优化

```python
# 1. 缓存热门查询
@cache(ttl=3600)
def search(query: str):
    return retriever.search(query)

# 2. 批处理嵌入生成
embeddings = embedder.encode_batch(documents, batch_size=32)

# 3. 索引优化
collection.create_index(
    field_name="embedding",
    index_type="HNSW",
    params={"M": 16, "efConstruction": 200}
)
```

### 查询优化

```python
# 1. 查询重写
query = rewrite_query(user_query)
# "最近的大额订单" → "2026 年 3 月金额>5000 的订单"

# 2. 查询扩展
queries = expand_query(user_query)
# "iPhone 订单" → ["iPhone", "苹果手机", "Apple 手机"]

# 3. 结果融合
results = fuse_results(
    vector_results,
    keyword_results,
    method="reciprocal_rank"
)
```

### 性能指标

| 指标 | 目标值 | 当前值 |
|------|--------|--------|
| P50 延迟 | <500ms | 320ms |
| P95 延迟 | <1s | 780ms |
| 检索准确率 | >85% | 88% |
| 查询成功率 | >95% | 97% |

---

## 扩展方向

### 功能扩展

- [ ] 多租户支持（不同公司数据隔离）
- [ ] 权限控制（不同角色看到不同数据）
- [ ] 查询历史与收藏
- [ ] 自动报告生成
- [ ] 异常订单预警

### 技术扩展

- [ ] 切换到 Milvus（生产级向量数据库）
- [ ] 添加多模态检索（订单图片）
- [ ] 实时数据同步
- [ ] 分布式部署
- [ ] 查询分析与优化建议

### 业务扩展

- [ ] 客户画像分析
- [ ] 销售趋势预测
- [ ] 库存智能推荐
- [ ] 供应链优化

---

## 评估方法

### 准备测试集

```json
[
    {
        "query": "张三 3 月份的订单",
        "expected_orders": ["ORD-001", "ORD-002", "ORD-003"],
        "expected_answer_keywords": ["张三", "3 月", "3 个订单"]
    },
    {
        "query": "金额超过 5000 元的已发货订单",
        "expected_orders": ["ORD-005", "ORD-008"],
        "expected_answer_keywords": ["5000", "已发货", "2 个订单"]
    }
]
```

### 运行评估

```bash
python scripts/evaluate.py --test-set test_questions.json

# 输出:
# 检索准确率：88.5%
# 答案相关性：92.3%
# 整体得分：90.4/100
```

---

## 故障排查

### 常见问题

**Q: 检索结果不相关**

```bash
# 检查嵌入质量
python scripts/debug_embedding.py "测试查询"

# 调整检索参数
# 在 config.py 中修改:
RETRIEVAL_TOP_K = 10  # 增加返回数量
SCORE_THRESHOLD = 0.6  # 降低阈值
```

**Q: 查询响应慢**

```bash
# 查看慢查询日志
docker-compose logs retriever | grep "slow"

# 优化建议:
# 1. 启用查询缓存
# 2. 减少 TOP_K
# 3. 检查数据库索引
```

**Q: 内存占用高**

```bash
# 监控内存使用
docker stats

# 优化建议:
# 1. 减少 Chroma 缓存大小
# 2. 分批处理大数据
# 3. 定期清理无用数据
```

---

## 参考资源

- [RAG 指南](../../docs/rag-guide.md)
- [技能包文档](../../skills/rag-builder/SKILL.md)
- [Chroma 文档](https://docs.trychroma.com)
- [Streamlit 文档](https://docs.streamlit.io)

---

## 许可证

MIT License - 详见 [../../LICENSE](../../LICENSE)

---

*最后更新：2026-03-23*
