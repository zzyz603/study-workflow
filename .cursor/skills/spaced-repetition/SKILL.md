---
name: spaced-repetition
description: 根据 knowledge/_index.md 做间隔复习：抽出到期主题与卡片、口头提问、按表现更新间隔和巩固态，必要时重算画像。在用户说复习、间隔复习、刷卡片、今天复习什么，或进门检查选择先复习时使用。
---

# Spaced Repetition

复习已有知识，不开新课。先读 `knowledge/_index.md`，只打开到期或逾期主题的 `cards.md`。

## 卡片位置

```text
knowledge/<topic>/cards.md
knowledge/<topic>/review.md
```

新卡片用 `templates/card.md` 追加到 `cards.md`。复习结果追加到 `review.md`（见 `templates/review-log.md`）。

## 步骤

1. 从 `_index.md` 选出「到期 ≤ 今天」或「逾期 > 0」的主题。没有则如实说，不要硬考。
2. 一次复习 5–12 张，优先 Core、低等级、已逾期。
3. 先问 `prompt`，等用户答。不要先揭示 `expected_points`。
4. 对照 `expected_points` 判结果：`again` / `hard` / `good` / `easy`。
5. 更新卡片：

| 结果 | `consecutive_success` | 下次间隔 |
| --- | --- | --- |
| again | 置 0 | 1 天；主题巩固态降为 `fragile` |
| hard | 置 0 | 约 2 倍当前间隔，至少 2 天；巩固态为 `fragile` |
| good | +1 | 约 2.5 倍，至少 4 天 |
| easy | +1 | 约 3.5 倍，至少 7 天 |

新卡：`again` → 1 天；`good` → 4 天。

6. 重算该主题巩固态（只看 `tags` 含 `core` 的卡片；没有 Core 卡则暂留 `fragile`）：

| 巩固态 | 条件 |
| --- | --- |
| `none` | 尚无合格验收 |
| `fragile` | 已验收，但尚无 Core 卡，或任一张 Core 卡 `last_result` 为 `again`/`hard` |
| `stable` | 每张 Core 卡 `consecutive_success ≥ 2`，且 `interval_days` ≥ 阈值（`fast`=7，`strict`=21） |
| `holding` | 已验收且不满足 `fragile`/`stable` |

7. 回写 `_index.md` 的巩固、到期（Core+非 Core 里最早 `due`）、逾期张数。追加 `review.md`。
8. 按 `AGENTS.md` 的画像规则重算。只有维度等级、来源或一句话变了，才改 `profile.md` 并追加 `profile-history.md`。

## 规则

- 卡片 `prompt` 是问题，不是讲义。
- `expected_points` 是要点清单，不是可抄的完整范文。
- 用户答不上来时，按 Teacher 补最小缺口，然后把该卡间隔重置为 1 天。
- 不要把复习会话写成新的 `sessions/` 主题课；除非用户明确要把某张卡升级成新主题。
- 不要因为「又复习了一次」就升级画像。
