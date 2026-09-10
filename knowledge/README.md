# knowledge/

长期知识库。只放已经过验收、或用户明确要求保留的材料。

当次过程、半成品讲解、未结束的验收不要放这里，放到 `sessions/`。

## 目录

```text
knowledge/
  _index.md              # 主题总表与掌握等级
  <topic-slug>/
    notes.md             # 稳定笔记（templates/note.md）
    cards.md             # 复习卡片（templates/card.md）
    sources.md           # 来源（templates/source.md）
    review.md            # 复习记录（templates/review-log.md）
```

`<topic-slug>` 用小写英文或拼音，短横线连接，例如 `tcp`、`http-caching`。

## 写入规则

- 新建主题前先看 `_index.md`，避免重复目录。
- 笔记写「自己能讲出来的结构」，不要粘贴整章原文。
- 卡片的 `prompt` 是问题；完整讲义不要写进卡片正面。
- 掌握等级与 `sessions/` 里最近一次 `exam.md` 对齐，不要按阅读量改等级。
