# knowledge/

长期知识库。只放已经过验收、或用户明确要求保留的材料。

当次过程、半成品讲解、未结束的验收不要放这里，放到 `sessions/`。

## 目录

```text
knowledge/
  _index.md              # 主题总表：等级、巩固态、到期
  profile.md             # 当前学习者画像
  profile-history.md     # 画像变化，只在维度真的变了时追加
  <topic-slug>/
    notes.md             # 稳定笔记（templates/note.md）
    cards.md             # 复习卡片（templates/card.md）
    sources.md           # 来源（templates/source.md）
    review.md            # 复习记录（templates/review-log.md）
```

`<topic-slug>` 用小写英文或拼音，短横线连接，例如 `tcp`、`http-caching`。

## 三道门槛

1. **会话通过**：`exam.md` 达到目标等级，无 Core 漏洞。只改主题「等级」，巩固态记为 `fragile`。
2. **主题巩固**：按该主题策略，Core 卡片连续 2 次 `good`/`easy`，且 `interval_days` 达到阈值。
3. **画像升级**：该维度已有 `stable` 主题；维度等级取这些 `stable` 主题当前等级的最小值。新开但尚未巩固的主题不把画像拉下来。已 `stable` 的主题退回 `fragile` 则可能降级。

不要按学习时长或复习次数满 N 次改画像。

## 写入规则

- 新建主题前先看 `_index.md`，避免重复目录。
- 卡片 `due` 一变，必须回写该行的「到期 / 逾期 / 巩固」。进门提醒只读 `_index.md`，不靠翻完全部卡片。
- 笔记写「自己能讲出来的结构」，不要粘贴整章原文。
- 卡片的 `prompt` 是问题；完整讲义不要写进卡片正面。
- 掌握等级来自最近一次 `exam.md`；巩固态来自卡片复习表现。
- 改 `profile.md` 的一句话或维度时，同时追加 `profile-history.md`。
