<!-- 辅助参考文件（渐进式披露）：本文件是 domain-model/SKILL.md（易混词订正） 的查表/模板内容搬运。**权威归属该 SKILL.md 对应节（对外回指键），条文实体在本文件——修改先改本文件，并保持 SKILL.md 指针与"何时读"描述同步**；不得两处各自演化。 -->

# 易混词订正

> **何时读**：裁决时对两个概念（如 Publisher vs Executor、审查义务 vs 性质）拿不准归属或判据时读

## 易混词订正

| 区分 | 判据 |
|---|---|
| ~~Owner~~ → **Publisher** | 已废弃 Owner（易误读为资源拥有者/长期负责人）；谁发布任务，谁保留最终验收权 |
| **Publisher vs Executor** | 决定任务是否最终闭合 vs 实际执行任务；可同一主体，但职责必须可区分 |
| **Verification vs Acceptance** | "它是否满足技术/契约条件？"（Auditor）vs "任务是否满足最终关闭条件？"（Publisher） |
| **Verdict vs Done** | `Verdict = Pass ⇏ Done`——还可能缺必产工件、范围要求、契约条件、PublisherAccept |
| **Claim vs Evidence** | "我认为它完成了" vs "以下事实可让别人验证这个判断" |
| **Evidence vs Verdict** | 原始事实与可复核材料 vs Auditor 依据 Artifact+Evidence+Contract 得出的判断 |
| **Requirement vs Acceptance Criterion** | 要解决什么问题（Specification）vs 在什么条件下认为已解决（Closure Predicate） |
| **Design vs Plan** | 系统应如何构成 vs 已确定的结构按依赖如何执行；Planner 不重新设计 |
| **Domain vs Role** | 解决哪类问题 vs 以什么身份解决 |
| **Domain vs Task Type** | 任务当前需要建立哪种性质 vs 任务"属于哪一类"；进入哪个域由 Gap(T) 决定（G16） |
| **Support Domain vs Action** | 拥有自己契约/工件/证据/完成语义的工作职责 vs 域内具体操作（search/retrieve 是 action，research 不是） |
| **Complexity vs Domain** | 规模属性 vs 性质/职责；`Domain ⊥ Complexity`（G21） |
| **supports vs dependsOn** | 支撑任务为调用者提供成果、不进主路径 vs 前序输出满足后序前置、属主路径因果链；支撑完成只推出 `Useful(S,T)`（G18） |
| **Service vs Support Domain** | 都可被调用；支撑域有自己的契约/工件/证据/完成语义且可独立成任务；服务只提供能力，不产生 Done Claim、不被验收 |
| **Closure Decision vs Acceptance Authority** | 验收域管"任务是否满足关闭条件"（闭合决策）vs 横切治理管"谁有权关闭该任务"（验收权） |
| **Primary vs Support Task** | 独立任务（支撑域作为根任务成立）vs 支撑任务（被主任务调用）；`Relation(T)` 的显式取值，必须登记不得推断（G17） |
| **Done(S) vs Useful(S,T)** | 支撑任务完成 vs 支撑成果满足调用者规定的输入条件；支撑任务以后者为完成判据（G18） |
| **scope vs domain（术语变更）** | arch/spec 的受控词汇字段原名 `domain`，与模型概念"域（Domain）"冲突，**已统一改名为 `scope`**；技能正文中的"域"只指本模型的核心域/支撑域 |
| **审核强度 vs 审核结果** | 强度：契约输入的覆盖面约定（档位/维度子集，审查前由定档人声明） vs 结果：审核域产出的三值 Verdict；Verdict 不合预期 ≠ "强度定错"，可上调后重审（G24） |
| **接缝 vs 阶段** | 接缝：核心域工件产出后的审查决定点（数据驱动、位置由义务成熟涌现） vs 阶段：固定流程位置；审核没有固定阶段位置 |
| **发布者 vs 上游域** | 发布者：契约与责任主体 vs 上游域：任务图中的前序职责域；接缝审查的定档人是**被审任务的 Publisher**，不必然是"上游域"本身——支撑任务被审时 = 主任务 Publisher，独立形态时 = 用户 |
| **审查义务 vs 性质** | 义务：契约声明的"须先独立审查方可采信"的数据 vs 性质：任务状态中的建立/缺失项；义务驱动审核域进入（使能/阻塞），性质缺口驱动其余域；`Verified ∈ Gap` 而无义务 ⇒ 不审查 |
