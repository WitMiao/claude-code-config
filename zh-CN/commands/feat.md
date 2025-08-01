---
description: 新增功能

allowed-tools:
  - Task
  - Bash
  - Glob
  - Grep
  - Read
  - Edit
  - MultiEdit
  - Write
  - WebFetch
  - WebSearch
  - Notebook.*
  - Edit|Write
  - mcp__.*
  - mcp__memory__.*
  - mcp__filesystem__.*
  - mcp__github__.*
---

$ARGUMENTS

## 核心工作流程

### 1. 输入分析与类型判断

每次收到用户输入时，首先进行类型判断并明确告知用户：

**判断标准：**

- **需求规划类型**: 用户提出新功能需求、项目构想或需要制定计划

- **讨论迭代类型**: 用户要求继续讨论、修改或完善已有规划

- **执行实施类型**: 用户确认规划完成，要求开始具体实施工作

### 2. 分类处理机制

#### A. 需求规划处理

**触发条件**: 识别为功能需求输入

**执行动作**:

- 启用 Planner Agent

- 生成详细的 markdown 规划文档

- 将文档存储至 `./.claude/plan` 目录，并以 plan/xxx.md 的格式命名

- 包含：目标定义、功能分解、实施步骤、验收标准

#### B. 讨论迭代处理

**触发条件**: 用户要求继续讨论或修改规划

**执行动作**:

- 检索并分析上次生成的规划文件

- 识别用户反馈和确认内容

- 启用 Planner Agent

- 生成详细的 markdown 规划文档

- 建立一个新的文档，比如上一次是 plan/xxx.md，那么这次就是 plan/xxx-1.md，如果上一次是 plan/xxx-1.md，那么这次就是 plan/xxx-2.md，以此类推

- 重新组织待实施任务优先级

#### C. 执行实施处理

**触发条件**: 用户确认规划完成，要求开始执行

**执行动作**:

- 按规划文档顺序启动任务执行

- 每个子任务开始前进行任务类型识别

- **前端任务特殊处理**:

- 检查是否存在可用 UI 设计

- 如无设计方案，must use UI-UX-Designer Agent

- 完成 UI 设计后再进行开发实施

### 3. 关键执行原则

#### 强制响应要求

- **每次交互必须首先说明**: "我判断此次操作类型为：[具体类型]"

- 类型判断必须准确且明确传达给用户

#### 任务执行规范

- 严格按照文档化规划执行

- 子任务启动前必须明确任务性质和依赖关系

- 前端任务必须确保 UI 设计完整性

#### 状态管理机制

- 维护任务完成状态跟踪

- 及时更新规划文档状态

- 确保用户对进度的可见性

## 质量保证要点

1. **类型判断准确性**: 每次交互开始的类型识别必须准确

2. **文档一致性**: 规划文档与实际执行保持同步

3. **依赖关系管理**: 特别关注前端任务的 UI 设计依赖

4. **用户沟通透明**: 所有判断和动作都要明确告知用户
