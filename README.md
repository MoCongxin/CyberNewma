# 人-Agent 协作开发工作流技能集

> CyberNewma（赛博牛马），一套用于提高 agent 工程能力的技能集。目标是使用廉价模型实现可用度高的工程交付。

一套用于「人 + Agent 协作开发」的流程型技能集。它把开发过程拆成**可判定的域**（需求 → 设计 → 计划 → 实施 → 审核 → 验收），每个域一份 Agent 手册；在此之上有一层**域模型**（跨域裁决条款的唯一权威）和一个**调度者运行时**（主 Agent 如何按缺口派发子代理）。技能条文与具体项目、仓库、技术栈解耦，按域装入子代理使用。

## 它解决什么问题

Agent 协作的失败模式通常不是"模型不够聪明"，而是**判断不可裁决、交付不可复核、过程不可追溯**：

- 需求写成一段散文，谁都能说自己完成了 → 本技能集要求需求落成**可判定的 spec**，不可判定即阻断；
- "我实现完了"当作完成 → 实施域要求 **Claim ≠ Evidence**，交付必须附可独立复核的证据；
- 设计与实现不符时悄悄改设计 → **偏差就地标注**，原方案不删，演化史可还原；
- 层与层之间靠"目测通过"衔接 → 一律换成**硬门控**（命令 + 通过条件 + 不通过则）；
- 临时方案与已知缺口随讨论蒸发 → **债务显式化**，每条带截止与行为验收标准。

## 安装（每台机器一次）

克隆本项目

目录联接：

```powershell
# Windows
cmd /c mklink /J "%USERPROFILE%\.agents\skills" "<克隆路径>\skills"
```

```bash
# Linux / macOS
ln -s <克隆路径>/skills ~/.agents/skills
```

> 若已有 `~/.agents/skills`，请先把想保留的技能目录并入本仓 `skills/`，再建立联接——联接会替换原目录。或者直接将本项目的 skills 复制到 `~/.agents/skills` 目录下。

<!-- SKILL-INDEX:BEGIN -->
## 技能清单（10 项）

见 `skills/workflow-principles/SKILL.md`——总览：技能清单与阅读顺序、七项核心原则、单点真相分工、文档工件生命周期（research→report→spec→arch→plan/task→memory）、新项目引入定制清单。

**按域组织（v2）**：

| 类别 | 技能 |
|---|---|
| 判定依据层 | `domain-model`（跨域裁决唯一权威） |
| 运行时 | `dispatcher-orchestration`（主 Agent 的按域派发手册） |
| 核心域手册（派发给子代理） | `domain-demand` / `domain-design` / `domain-plan` / `domain-implement` / `domain-review` |
| 支撑域 | `research-methodology`（调研，独立/支撑双形态） |
| 沉淀与产出 | `memory-knowledge-system` |
<!-- SKILL-INDEX:END -->

## 怎么用

1. **从 `workflow-principles` 读起**：七项贯穿原则、文档工件生命周期、新项目引入定制清单。
2. **域判定与裁决查 `domain-model`**：这个任务该走哪些域、算不算完成、该谁验收、这个接缝要不要审审多深——跨域裁决条款的唯一权威。
3. **主 Agent 按 `dispatcher-orchestration` 推进**：算性质缺口 → 查审查义务 → 选域 → 按派发契约派发域子代理 → 核对交接 → 循环至缺口为空 → 转验收域闭合。
4. **每个域子代理只装入自己那一份域技能**：域手册条文自足，不需要再读域模型或总览。上下文干净度直接决定判断质量。

配套产物是一条文档流水线：`research → report → spec → arch → plan/task → memory`，各阶段工件有固定的命名、状态机与双向引用规则，见 `workflow-principles` 的「文档工件生命周期」。

## 注意事项

本 skills 可能提高 token 的消耗量。

## 许可

本仓内容以 **MIT** 授权，全文见 `LICENSE`。
