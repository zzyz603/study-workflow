---
name: spaced-repetition
description: 根据 knowledge/ 中的卡片做间隔复习：抽出到期卡片、口头或简答提问、按表现更新 due 与掌握等级。在用户说复习、间隔复习、刷卡片、今天复习什么时使用。
---

# Spaced Repetition

复习已有知识，不开新课。先读 `knowledge/_index.md` 和各主题 `cards.md`。

## 卡片位置

```text
knowledge/<topic>/cards.md
knowledge/<topic>/review.md
```

新卡片用 `templates/card.md` 追加到 `cards.md`。复习结果追加到 `review.md`（见 `templates/review-log.md`）。

## 步骤

1. 选出 `due` 为空或 `due <= 今天` 的卡片；没有到期卡片就如实说，不要硬考 Core 以外的新内容。
2. 一次复习 5–12 张，优先 Core、低等级、已到期。
3. 先问 `prompt`，等用户答。不要先揭示 `expected_points`。
4. 对照 `expected_points` 判结果：`again` / `hard` / `good` / `easy`。
5. 更新卡片：

| 结果 | 下次间隔 |
| --- | --- |
| again | 1 天，等级可降 |
| hard | 约 2 倍当前间隔，至少 2 天 |
| good | 约 2.5 倍，至少 4 天 |
| easy | 约 3.5 倍，至少 7 天 |

新卡：`again` → 1 天；`good` → 4 天。

6. 把日期、卡片 id、结果写入 `review.md`。必要时回写 `_index.md` 的主题状态。

## 规则

- 卡片 `prompt` 是问题，不是讲义。
- `expected_points` 是要点清单，不是可抄的完整范文。
- 用户答不上来时，按 Teacher 补最小缺口，然后把该卡间隔重置为 1 天。
- 不要把复习会话写成新的 `sessions/` 主题课；除非用户明确要把某张卡升级成新主题。
