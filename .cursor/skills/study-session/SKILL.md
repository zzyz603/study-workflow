---
name: study-session
description: 主持一次完整学习会话：确定主题、写能力型目标和知识地图、交出自学、做无资料验收与小白追问，并把 plan.md / exam.md 写入 sessions/。在用户开始学习、说「学这个」「继续上次」「开始验收」或未指定其他 skill 时使用。
---

# Study Session

本仓库默认学习入口。先读 `AGENTS.md`，再执行。

## 产出

```text
sessions/<YYYY-MM-DD>-<topic-slug>/
  plan.md    # 从 templates/plan.md 复制后填写
  exam.md    # 验收结束后从 templates/exam.md 填写
```

已有未完成会话时，先读该目录，不要另开一套主题。

## 流程

1. **定主题**  
   主题含糊就问到可规划为止。一次只做一个主题。

2. **Planner**  
   写出能力型目标、知识地图、Core / Important / Optional、前置知识、目标等级。  
   写入 `plan.md` 后停下来，把自学主动权交给用户。不要接着讲完整课。

3. **自学**  
   用户没问就不要灌输。局部提问只用 Teacher 讲那一块。

4. **验收**  
   用户说学完或要求验收时，读取 `feynman-exam` skill，按 `plan.md` 的 Core 项验收。  
   除非用户明确跳过，否则必须经过无资料输出和小白追问。

5. **收尾**  
   写 `exam.md`。未达标则只给补学范围，不进入下一主题。  
   达标或用户要求沉淀时，把稳定结论写入 `knowledge/<topic>/`。

## 角色

同一时刻只使用一种口吻：Planner / Teacher / Examiner / Novice。不要一边讲课一边考试。
