# Design

本文件是系统设计准则，不是学习会话手册。

- 怎么学、怎么验收 → `AGENTS.md`
- 程序 / AI / 用户如何分工、什么可以自动化 → 本文件

改脚本、skill、模板、阶段或产物结构时先读这里。普通学习会话不必展开全文。

## 三方协作

工作流不是「全程 prompt」，也不是给其他项目调用的后端编排。它是文件驱动的状态机，三方各管一块：

```text
程序：建目录、拷模板、校验、改阶段、算间隔
  → 把当前节点和文件交给 AI
AI：规划 / 讲解 / 追问 / 评级
  → 只产出结构化结论
程序：写入并检查下一跳是否合法
用户：自学、讲解、回答
```

状态以仓库文件为准，不以对话记忆为准。

## 判断标准

| 类型 | 交给谁 |
| --- | --- |
| 同样输入必须得到同样结果 | 程序 / 脚本 / 模板 |
| 质量取决于用户原话的含义 | AI |
| 知识必须在用户脑子里发生 | 用户；AI 和程序都要停住等 |

## 阶段

```text
idle → planning → learning → examining → remedial → retained
                                   ↘ reviewing（并行：复习卡片，不新开主题课）
```

合法跳转由程序守门。AI 可以建议下一阶段，不能擅自改阶段。

| 从 → 到 | 门禁 |
| --- | --- |
| planning → learning | `plan.md` 有能力目标、Core、目标等级 |
| learning → examining | 用户明确说开始验收（人闸，不自动开考） |
| examining → retained | `exam.md` 总评 ≥ 目标，且无 Core 漏洞 |
| examining → remedial | 有明显漏洞 |
| remedial → examining | 用户再次要求验收 |
| 任意 → reviewing | `knowledge/` 中有到期卡片 |

## 文件分工

每个会话分两层，避免把机器状态埋进散文：

```text
sessions/<YYYY-MM-DD>-<topic-slug>/
  state.json   # 程序所有：stage、target_level、flags
  plan.md      # AI + 用户：目标、地图、说明
  exam.md      # AI：验收结论（按模板）
```

Markdown 给人看，结构化状态给脚本看。Skill 应先跑脚本，再思考；不要靠模型手改目录名或心算间隔。

`state.json` 字段以实际脚本为准，至少包括：

- `topic`
- `stage`
- `target_level`
- `no_notes_output`
- `novice_done`

## 对照表

| 节点 | 用户 | AI | 程序 |
| --- | --- | --- | --- |
| 定主题 | 说出主题 | 判断是否可规划、范围是否过大 | 建会话目录，复制 `templates/plan.md` |
| 目标 / 知识地图 | 确认范围 | 写能力型目标、地图、Core 分级 | 校验必填栏；不通过则不能进入 `learning` |
| 自主学习 | 读书、看文档、写代码 | 只在被问时讲局部 | 阶段停在 `learning`，不自动往下 |
| 无资料输出 / 小白追问 | 连续讲解、回答 | 追问、识别漏洞 | 确认 `plan.md` 存在；记录验收 flags |
| 最终评估 | — | 按当场表现给 L0–L4 | 对照目标等级决定下一跳是否合法 |
| 拆书 / 出题 | 提供资料或要求 | 切 Core、设计问题 | 按模板落盘 |
| 间隔复习 | 回答卡片 | 判 `again/hard/good/easy`，必要时补最小缺口 | 筛到期卡片、算间隔、写 `review.md` |

## Skill 的位置

Skill 不是工作流引擎，是某个 AI 节点的操作手册。

| 层 | 负责 |
| --- | --- |
| `AGENTS.md` + `.cursor/rules/` | 学习原则与硬约束 |
| 本文件 + 脚本 + `state` | 阶段、门禁、落盘、间隔 |
| `.cursor/skills/` | 规划、拆书、追问、判档、出题 |
| `knowledge/` `sessions/` | 学习结果 |

`study-session` 只做调度：读当前阶段 → 调脚本 → 再进入 Planner 或 Examiner。不要在 skill 正文里再实现一套建目录、改模板、心算 SM-2 的逻辑。

## 程序该做的

固定、易算错、算错会坏数据的，做成脚本（计划放 `scripts/`）：

- 新建会话目录并复制模板
- 校验 `plan.md` / `exam.md` / 卡片字段
- 列出到期卡片
- 按档位更新 `due` / `interval_days`
- 合法阶段迁移
- 验收通过后把稳定内容提升到 `knowledge/`

## AI 该做的

- 学习目标是否写成能力
- 知识怎么切、什么算 Core
- 下一问问什么
- 用户这句话是 L1 还是 L3
- 拆书时什么该剪掉
- 最小补学讲哪一块

## 不要做的

- 自动替用户学完
- 定时自动开考
- 用选择题机代替费曼验收
- 把整条学习链做成对外 API / 队列 / 工作流服务
- 把间隔公式放进 prompt 让模型心算
- 把阶段只记在对话里
