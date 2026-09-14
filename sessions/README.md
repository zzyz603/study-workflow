
# sessions/

一次学习会话一个目录，记录当次目标和验收，不代替 `knowledge/`。

## 命名

```text
sessions/<YYYY-MM-DD>-<topic-slug>/
  plan.md         # 必有，来自 templates/plan.md
  exam.md         # 验收结束后有
  questions.md    # 可选，出题 skill 生成
  notes.md        # 可选，当次草稿
```

同一主题同一天只开一个目录。跨天续学可以新建目录，并在 `plan.md` 里写清「续：上次路径」。

## 生命周期

1. 开始主题 → 创建目录并写 `plan.md`
2. 用户自学 → 需要时追加当次草稿
3. 验收结束 → 写 `exam.md`
4. 达标或用户要求沉淀 → 把稳定内容拷入 `knowledge/<topic>/`
5. 未达标 → 目录保留，下次补学仍读这份 `plan.md` 和 `exam.md`

开始任何学习前，Agent 应先读 `knowledge/_index.md` 做到期提醒。提醒本身不在 `sessions/` 里新建目录。
