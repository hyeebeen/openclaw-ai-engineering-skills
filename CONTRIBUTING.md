# 贡献指南

> 欢迎加入 OpenClaw AI Engineering Skills 社区！
>
> 你的每一份贡献都让这个项目变得更好 🌟

---

## 📋 目录

- [快速开始](#快速开始)
- [贡献方式](#贡献方式)
- [开发环境设置](#开发环境设置)
- [代码规范](#代码规范)
- [提交指南](#提交指南)
- [审查流程](#审查流程)
- [贡献者权益](#贡献者权益)

---

## 快速开始

### 第一次贡献？

1. **Fork 项目** - 点击 GitHub 右上角的 Fork 按钮
2. **克隆仓库** - `git clone https://github.com/YOUR_USERNAME/ai-engineering-skills.git`
3. **创建分支** - `git checkout -b feature/your-feature`
4. **做出修改** - 代码、文档、示例都可以
5. **提交 PR** - 推送到 GitHub 并创建 Pull Request

### 寻找任务

- [Good First Issues](https://github.com/openclaw/ai-engineering-skills/issues?q=is%3Aissue+is%3Aopen+label%3A%22good+first+issue%22) - 适合新手
- [Help Wanted](https://github.com/openclaw/ai-engineering-skills/issues?q=is%3Aissue+is%3Aopen+label%3A%22help+wanted%22) - 需要帮助的任务
- [文档改进](https://github.com/openclaw/ai-engineering-skills/issues?q=is%3Aissue+is%3Aopen+label%3Adocumentation) - 文档相关

---

## 贡献方式

### 📝 文档贡献

**适合人群**: 所有人

**贡献内容**:
- 修正错别字和语法错误
- 改进文档结构和可读性
- 添加缺失的说明
- 翻译文档（多语言支持）

**如何开始**:
```bash
# 找到需要修改的文档
cd docs/

# 修改后提交
git add docs/xxx.md
git commit -m "docs: 改进 RAG 指南的检索策略说明"
```

---

### 💻 代码贡献

**适合人群**: 开发者

**贡献内容**:
- 修复 Bug
- 添加新功能
- 优化性能
- 增加测试覆盖

**如何开始**:
```bash
# 创建功能分支
git checkout -b feat/add-new-skill

# 开发完成后运行测试
pytest tests/

# 确保代码格式正确
ruff check .
ruff format .
```

---

### 🎬 示例项目贡献

**适合人群**: 有项目经验的开发者

**贡献内容**:
- 新的完整示例项目
- 扩展现有示例
- 添加使用场景

**示例项目要求**:
```
examples/your-example/
├── README.md          # 项目说明（必需）
├── requirements.txt   # 依赖列表
├── src/               # 源代码
├── tests/             # 测试（推荐）
└── demo.gif           # 演示动图（推荐）
```

---

### 🐛 Bug 报告

**提交前检查**:
- [ ] 搜索现有 Issues，避免重复
- [ ] 确认是 Bug 而非使用问题
- [ ] 准备复现步骤

**Bug 报告模板**:
```markdown
### 问题描述
简要描述问题

### 复现步骤
1. ...
2. ...
3. ...

### 预期行为
应该发生什么

### 实际行为
实际发生了什么

### 环境信息
- OS: 
- Python: 
- OpenClaw: 
- 相关包版本:

### 日志/截图
```

---

### 💡 功能建议

**提交前思考**:
- 这个功能是否契合项目定位？
- 是否有现有替代方案？
- 实现复杂度如何？

**功能建议模板**:
```markdown
### 功能描述
简要描述建议的功能

### 使用场景
什么情况下需要这个功能

### 实现思路
如何实现（可选）

### 替代方案
考虑过哪些其他方案

### 额外信息
任何补充说明
```

---

## 开发环境设置

### 基础要求

- Python 3.10+
- Git
- 代码编辑器（VS Code 推荐）

### 环境配置

```bash
# 克隆项目
git clone https://github.com/openclaw/ai-engineering-skills.git
cd ai-engineering-skills

# 创建虚拟环境
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate

# 安装开发依赖
pip install -r requirements-dev.txt

# 安装 pre-commit 钩子
pre-commit install
```

### 依赖说明

```yaml
# requirements.txt - 运行时依赖
openclaw>=0.5.0
chromadb>=0.4.0
openai>=1.0.0
tiktoken>=0.5.0

# requirements-dev.txt - 开发依赖
-r requirements.txt
pytest>=7.0.0
ruff>=0.1.0
mypy>=1.0.0
pre-commit>=3.0.0
```

---

## 代码规范

### Python 代码

**格式化工具**: ruff + black

```bash
# 检查代码
ruff check .

# 自动格式化
ruff format .
```

**代码规范**:
```python
# ✅ 推荐
def calculate_similarity(vec1: list[float], vec2: list[float]) -> float:
    """计算两个向量的余弦相似度"""
    dot_product = sum(a * b for a, b in zip(vec1, vec2))
    norm1 = math.sqrt(sum(a * a for a in vec1))
    norm2 = math.sqrt(sum(b * b for b in vec2))
    return dot_product / (norm1 * norm2)

# ❌ 避免
def calc_sim(v1, v2):
    # 缺少类型注解和文档字符串
    ...
```

### 文档规范

**Markdown 格式**:
```markdown
# 一级标题

## 二级标题

### 三级标题

- 列表项 1
- 列表项 2

```python
# 代码块带语言标识
code here
```

**文档结构**:
```markdown
# 标题

> 简短描述（引用格式）

## 概述
背景和目标

## 快速开始
5 分钟上手指南

## 详细说明
完整功能说明

## 示例
代码示例

## 常见问题
FAQ

## 参考
相关链接
```

### 提交信息规范

**格式**: `<type>: <subject>`

**Type 类型**:
- `feat`: 新功能
- `fix`: Bug 修复
- `docs`: 文档更新
- `style`: 代码格式（不影响功能）
- `refactor`: 重构
- `test`: 测试相关
- `chore`: 构建/工具相关

**示例**:
```bash
# ✅ 好的提交信息
feat: 添加 Agent 编排器技能包
fix: 修复 RAG 检索结果排序问题
docs: 更新快速开始指南
refactor: 优化向量数据库接口

# ❌ 避免
更新代码
修 bug
```

---

## 提交指南

### 分支命名

```
feature/add-new-skill      # 新功能
fix/rag-retrieval-bug      # Bug 修复
docs/improve-rag-guide     # 文档改进
refactor/simplify-api      # 重构
```

### 提交前检查清单

- [ ] 代码通过测试 (`pytest`)
- [ ] 代码格式化 (`ruff format`)
- [ ] 代码检查通过 (`ruff check`)
- [ ] 类型检查通过 (`mypy`)
- [ ] 文档更新（如适用）
- [ ] 示例更新（如适用）
- [ ] 提交信息规范

### PR 描述模板

```markdown
## 变更描述
简要说明这个 PR 做了什么

## 相关 Issue
Fixes #123

## 变更类型
- [ ] 新功能
- [ ] Bug 修复
- [ ] 文档更新
- [ ] 性能优化
- [ ] 重构
- [ ] 其他

## 测试
- [ ] 已添加/更新测试
- [ ] 本地测试通过
- [ ] 需要额外测试场景：...

## 截图/演示
（如适用）

## 检查清单
- [ ] 代码符合规范
- [ ] 文档已更新
- [ ] 提交信息规范
```

---

## 审查流程

### PR 审查流程

```
1. 创建 PR
       ↓
2. 自动检查（CI/CD）
   - 代码检查
   - 测试运行
   - 构建验证
       ↓
3. 维护者审查
   - 代码质量
   - 功能正确性
   - 文档完整性
       ↓
4. 反馈与修改
   - 根据审查意见修改
   - 重新提交
       ↓
5. 合并
   - Squash Merge（推荐）
   - 关闭关联 Issue
```

### 审查响应时间

- **工作日**: 24-48 小时内响应
- **周末/节假日**: 可能延迟
- **紧急 Bug**: 标注 `priority: high` 加速处理

### 审查意见处理

**收到审查意见后**:
1. 逐条回复（接受/讨论/解释）
2. 做出相应修改
3. 推送新提交（无需 rebase，保持审查历史）
4. 通知审查者重新查看

---

## 贡献者权益

### 贡献等级

| 等级 | 要求 | 权益 |
|------|------|------|
| 🥉 新手贡献者 | 首次 PR 合并 | Discord 特殊角色 |
| 🥈 活跃贡献者 | 3 次 PR 合并 | GitHub 感谢名单 + 贴纸 |
| 🥇 核心贡献者 | 10 次 PR 合并 | 周边礼包 + 联合署名 |
| 👑 模块维护者 | 负责一个模块 | Co-maintainer 身份 |

### 认可方式

- **README 贡献者名单**: 所有贡献者列入
- **Release Notes**: 每个版本感谢贡献者
- **年度总结**: 年度贡献者表彰
- **社区展示**: 优秀贡献者故事分享

### 成长路径

```
新手贡献者 → 活跃贡献者 → 核心贡献者 → 模块维护者 → 项目维护者
    ↓              ↓              ↓              ↓
  首次 PR       持续贡献       深度参与       负责模块
```

---

## 社区准则

### 行为准则

- **尊重他人**: 包容不同观点和经验水平
- **建设性反馈**: 对事不对人
- **帮助新手**: 耐心回答初学者问题
- **遵守法律**: 不贡献侵权内容

### 沟通渠道

- **GitHub Issues**: Bug 报告和功能建议
- **GitHub Discussions**: 技术讨论和问题求助
- **Discord**: 日常交流和社区活动
- **邮件**: 敏感话题（security@...）

### 冲突解决

1. 直接沟通解决
2. 寻求维护者调解
3. 遵循社区共识

---

## 常见问题

### Q: 我的 PR 多久能被审查？

A: 通常 24-48 小时。如果超过一周未响应，可以 @ 维护者或到 Discord 提醒。

### Q: 我可以贡献什么？

A: 任何你有热情和能力贡献的内容！文档、代码、示例、翻译、设计都可以。

### Q: 我不确定我的贡献是否合适？

A: 先开一个 Discussion 或 Issue 讨论想法，我们会给你反馈。

### Q: 我的 PR 被拒绝了怎么办？

A: 不要灰心！审查意见是为了保证项目质量。根据反馈修改或讨论替代方案。

### Q: 如何成为模块维护者？

A: 持续贡献某个模块，展示专业能力和责任心，联系现有维护者申请。

---

## 资源链接

- [OpenClaw 官方文档](https://openclaw.dev)
- [GitHub 贡献指南](https://docs.github.com/en/get-started/exploring-projects-on-github/contributing-to-a-project)
- [首次贡献指南](https://github.com/firstcontributions/first-contributions)
- [代码审查指南](https://google.github.io/eng-practices/)

---

## 致谢

感谢所有为这个项目做出贡献的开发者！

<a href="https://github.com/openclaw/ai-engineering-skills/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=openclaw/ai-engineering-skills" />
</a>

---

*最后更新：2026-03-23*
