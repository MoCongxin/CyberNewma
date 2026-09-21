<!-- 辅助参考文件（渐进式披露）：本文件是 domain-model/SKILL.md（治理规则总表） 的查表/模板内容搬运。**权威归属该 SKILL.md 对应节（对外回指键），条文实体在本文件——修改先改本文件，并保持 SKILL.md 指针与"何时读"描述同步**；不得两处各自演化。 -->

# 治理规则总表（G1–G25）

> **何时读**：需要查某条 G 规则的完整条文/形式化/操作化位置，或按编号引用前确认语义时读

## 治理规则总表（G1–G25）

跨技能引用一律用编号；每条的操作化位置承载具体条文，本文不重复。

| 编号 | 规则 | 形式化 | 操作化位置 |
|---|---|---|---|
| G1 | 未形成可判定需求，不得进入需要其规格的后续工作 | `¬WellDefined(R) ⇒ Block` | domain-demand·公理 4 / domain-design·接单前置 |
| G2 | 设计必须精化规格 | `D ⊨ R` | domain-design·公理 2 |
| G3 | 分解后必须保持整体契约 | `C₁∧…∧Cₙ ⇒ R` | domain-design·公理 4 |
| G4 | 计划不能偷偷改变设计 | `Plan ≢ Redesign` | domain-plan·接单前置 / dispatcher·调度循环 |
| G5 | 依赖必须可满足且无环 | `Qᵢ ⇒ Pⱼ`，DAG | domain-plan·公理 3 |
| G6 | 无证据不得声明已实现 | 无 Evidence 的 Claim 不成立 | domain-implement·验证门控与公理 3 |
| G7 | Auditor 不得直接继承 Executor 的结论 | `ProducerClaim ⇏ Verdict` | domain-review·公理 1 |
| G8 | Unknown 不得默认为 Pass | `Unknown ≠ Pass` | domain-review·公理 2 |
| G9 | Publisher 不承担技术复证 | `Accept ≠ ReVerification` | dispatcher-orchestration·验收域 |
| G10 | Publisher 可依赖 Verdict，但不得跳过完成契约 | `Accept ⇐ Verdict ∧ Contract`（⇐ 读作"以…为输入前提"，非实质蕴含） | dispatcher-orchestration·集成归档 |
| G11 | 委派执行权不转移 Publisher | `Delegate ⇒ Publisher 不变` | dispatcher-orchestration·角色模型与治理纪律 |
| G12 | 子任务 Done 不自动推出父任务 Done | `Done(child) ⇏ Done(parent)` | dispatcher-orchestration·任务树语义（任意深度通用） |
| G13 | 非 Publisher 不得关闭任务 | `Close(T) ⇒ Actor = Publisher(T)` | dispatcher-orchestration·归档等人类确认 |
| G14 | Done 必须满足关闭谓词 | `Done(T) ⇒ ClosurePredicate(T)` | domain-plan·Acceptance Criteria |
| G15 | 只有信息不足或权限不足才能上冒 | `Escalate ⟺ InfoInsufficient ∨ AuthorityInsufficient` | dispatcher-orchestration·上冒链 |
| G16 | 域选择由性质缺口决定，而非任务类别决定 | `Domain = f(Required, Established, ConversationIntent, Obligations)`（缺口为核心项） | 本技能·域的本体 / dispatcher·调度循环 |
| G17 | 支撑任务可独立存在，也可被其他任务调用 | `Primary(S) ∨ Supports(S, T)`；登记四项 | 本技能·支撑域 / research-methodology |
| G18 | 支撑任务完成不等于主任务完成 | `Done(S) ⇏ Done(T)`；完成=`Useful(S,T)` | 本技能·支撑域 / dispatcher·支撑任务派发 |
| G19 | 验收可依赖审核结果，但不得绕过完成契约 | `Accept ⇐ Verdict ∧ Contract`（⇐ 读法同 G10） | 同 G10（通用任务语境的重申） |
| G20 | 会话域判定（本技能集未内化） | `Session ⇒ ConversationIntent` | 仅见设计文档 §15（未内化） |
| G21 | 复杂度不决定域路径 | `Domain ⊥ Complexity` | 本技能·域的本体（含微任务判据）/ dispatcher·微任务亲做条款 |
| G22 | 任务路径取满足必要性质的最小充分域集合 | `D* = argmin{\|D\| : Properties(D) ⊇ Required(T)}` | 本技能·域的本体 / dispatcher·调度循环 |
| G23 | 每个核心接缝的审查决定必须显式声明，不得静默省略；免审必须显式且留痕 | `∀ 接缝 s: Tier(s) ∈ {免审,轻审,标准审,重审} ∧ 已声明(s)` | 本技能·审查义务与审核强度 / dispatcher·派发契约模板（审核强度节） |
| G24 | 审核强度只能上调，不能下调 | `Tier_final(s) ≥ Tier_initial(s)`（档位全序），上调留痕 | 本技能·审查义务与审核强度 / dispatcher·派发契约模板（审核强度节） |
| G25 | 向人类请求裁决必须自包含 | 提出方只读该条消息即可裁决（决策项 + 背景 + 已确立/已排除 + 选项 + 默认） | 本技能·上冒 / dispatcher·需求访谈与上冒链 |

**编号引用规则（避免重复引用歧义）**：**G19 是 G10 在通用任务语境下的重申，二者形式化相同——引用一律用 G10，G19 不单独引用**（编号保留是为了不改动既有对外引用）。遇到"验收是否能绕过完成契约"的疑问，只查 G10。

规则分组索引（每组管哪段）：G16/G22 → 路由（走哪些域）；G1–G5 → 域内工作合法性（需求/设计/计划）；G6–G8 → 声明与验证的关系（实施/审核）；G9–G14 → 闭合与责任（验收/治理）；G15/G25 → 无法继续时的出口与向上请求裁决的呈现；G17/G18 → 支撑域挂接；G19/G20 → 跨域重申与意图判定；G21 → 路由不得以复杂度为输入；G23/G24 → 审查决定显式化与审核强度。
