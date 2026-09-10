---
name: generate-questions
description: 按学习目标和知识地图出题，用于自测或生成复习卡片，不能代替费曼验收。在用户说出题、练习题、自测题、把这章变成问题、生成卡片时使用。
---

# Generate Questions

出题是为了暴露缺口，不是为了让用户打勾过关。

## 输入

优先读当前 `plan.md`。没有会话计划时，先问主题和目标，或从 `knowledge/<topic>/` 读取。

## 产出

写入当前会话 `questions.md`，需要沉淀时再追加到 `knowledge/<topic>/cards.md`。

题目按知识地图组织，并标注：

- 对应节点（Core / Important / Optional）
- 类型：Definition / Why / How / Comparison / Boundary / Application / Failure
- 期望要点（给 Agent 判分，不默认展示给用户）

## 出题规则

- Core 必须覆盖 Why 和 How，不能只有定义题。
- 默认以开放题为主。选择题最多作为热身，不能作为掌握依据。
- Optional 题单独标明「不阻塞过关」。
- 每题只问一件事。不要在一道题里堆三个机制。
- 不要附带完整标准答案长文。最多写 3–6 条 `expected_points`。

## 使用方式

1. 用户若要自测：一次出少量题，等回答，再讲评。
2. 用户若只要题单：只给问题，把要点留在文件里。
3. 用户若要变成卡片：转 `templates/card.md`，交给 `spaced-repetition`。
4. 用户若要正式验收：停出题，改走 `feynman-exam`。
