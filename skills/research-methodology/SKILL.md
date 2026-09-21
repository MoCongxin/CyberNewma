---
name: research-methodology
description: 技术调研工作方法论（调研支撑域手册）——5 类研究型态（规范解读/库对比/竞品分析/内部探查/工具生态）× 5 阶段工作流（定界/术语/证据/综合/结论，每阶段含动作·产出·自检点）× 文档模板 × 质量红线 × 双形态（Primary 独立调研/Support 支撑调研，登记四项与 Useful 判据）× 交接清单与 Blocked/SupportRequest 回报格式。当出现"调研 X"、"看看 X 怎么做"、"对比这几个库"、"调查 X 是否可用"、"引入新依赖前评估"时使用。触发词：调研、research、spike、横向对比、选型、技术评估、HVQ、来源证据、双形态。
---

# 调研工作方法论（Research Methodology）

> 你被调度者派发来执行**调研支撑域**的工作。本手册是你的域条文，且**条文自足**——只需本手册即可执行，不需要另外读取 domain-model（调度者层的规则编号只作为引用键出现在回报里）。
>
> 整合 Microsoft Technical Spike（Goal/Method/Evidence/Conclusions/Next Steps）、ElastiFlow 4-phase（HVQ + Success Thresholds）、ATAM-Lite trade-off、Wohlin SLR 的思想。research 是**带结论的可引用知识**——不是踩坑记录（→ memory/feedback），不是设计决策（→ arch）。

## 双形态：独立调研（Primary）与支撑调研（Support）

调研是一等支撑域：`Domain(T) = research` 不变，两形态的差别**只体现在任务图关系** `Relation(T) ∈ {Primary, Support}` 上（互斥但穷尽，必须显式登记、不得靠任务描述或角色推断）。

- **Primary（独立调研——调研本身构成当前任务的主要成果）**：`Result(T) → Goal(T)`。判据是"调研是否构成当前任务的主要成果"，"用户直接提出"只是常见情形不是判定标准。路径由缺口路由决定：目标谓词已给定时走 `需求 → 调研 → 验收`；调研本身也需要被设计/计划/审核时走全链。
- **Support（支撑调研——为父任务提供继续执行所需的信息/证据/决策依据）**：`Result(T_s) ⊨ RequiredInput(T_p)`。可嵌入任何域（设计/实施/审核 → 调研 → 原域）。**复杂度与支撑关系正交**：支撑调研同样可以是使用多个域的复杂任务。

### 支撑形态的登记四项（开工前置，未登记只算域内动作）

| 项 | 内容 |
|---|---|
| ① 登记形态 | Primary 还是 Support（显式取值，不靠推断） |
| ② 登记调用者 | 支撑调研的 Publisher = 调用它的主任务 |
| ③ 登记输入条件 | `Useful` 判据 = 父任务声明的输入义务——开工前必须明确"拿这个调研结果做什么用"，否则完成判据无法判定 |
| ④ 登记出口 | 成果回填到哪个域、以什么形式进入调用者的输入装配 |

### 完成判据

| 形态 | 完成判据 |
|---|---|
| Primary | 自身 Done 公式（目标谓词满足 + 验收闭合） |
| Support | **`Useful(S,T)`**——成果满足调用者规定的输入条件；`Done(调研) ⇏ Done(主任务)` |

### 被派发时的协作方式（子代理是叶子节点）

- 你**不能派发子代理**：需要更大范围的调研拆解时，回报调度者由其决定是否开子任务；
- 你是**被调度者派出**的支撑域子代理时，成果经调度者回填给原域；
- 遇到关键信息不可获得 → 明示 Unknown 并回报（上冒由调度者执行），**不要用推测填满报告**。

## 1. Research 在文档体系中的定位

调研的**工件**是 `docs/research/` 下的调研报告（结论 + 依据 + 不确定性声明）。报告写完后有两个出口：

- **结论被采纳为决策** → 进 **arch 工件**（决策与取舍在 arch 里演化，调研报告只作依据被引用）；
- **经验 / 事实要沉淀复用** → 走 **memory 沉淀体系**，归类判定**以 memory-knowledge-system 的分类判定表（六类）为唯一权威**，本手册不复述。

**research 与 feedback 的分界一句话**：research 答"外部/未知领域是什么样"（横向矩阵 + 来源证据，中长期）；feedback 答"我刚才踩了什么坑"（单点症状 + 根因 + 规避，永久）。分不清时问：**换一个项目这条还有用吗？** 有 → 不是 feedback，按 memory 表归类；没有 → feedback。

**调研型任务自身的域映射**（调研是一等支撑域——独立形态与支撑形态都按域推进）：

| 域 | 在调研任务中的形态 |
|---|---|
| 需求域 | HVQ：问题良定义且可判定（`R(x) ∈ {True, False}`） |
| 设计域 | 调研方案的结构设计：对比框架、维度轴、检索策略的组织（§2 型态选择即小型设计决策） |
| 计划域 | 阶段 0 定界 + timebox + 型态识别 |
| 实施域 | 阶段 2 证据收集（`file:line` / URL = Evidence） |
| 审核域 | §5 证据红线自检（每条事实可追溯、可复核） |
| 验收域 | 阶段 4 HVQ 必答 + 调用者/用户采信（Support 形态下判据为 `Useful(S,T)`） |

## 2. 五种研究型态（开工前先识别属于哪类）

### 2.1 Spec / Standard 解读型

- **对象**：成文规范、国标、RFC、行业白皮书
- **方法**：术语表 → 机制图 → 关键章节行号索引 → 对接本系统的位置
- **输出特征**：原文行号引用是核心（如 `spec/README.adoc:169-178`），方便回查
- **红线**：禁止仅复述规范——必须有"本系统中对应字段/位置"对照

### 2.2 库/框架横向对比型

- **对象**：3-5 个同类候选库，按维度横向比较
- **方法**：维度轴设计 → 多库逐维读源码 → 横向矩阵 → "对我们的启发"
- **输出特征**：每维都给"本项目选择"列；最后必须给"应该/不应该模仿的清单"
- **红线**：禁止"维度无差异"的列——没有差异就删掉该维度

### 2.3 竞品功能分析型（多产品特征矩阵）

- **对象**：同类产品（不是库）的功能集对比
- **方法**：维度表（扩展模型 / 数据来源 / 状态管理 / 序列化 / 隔离机制）→ 每产品一份子文档 → 汇总到主文档的共识 + 差异化
- **输出特征**：每个产品独立成文，主文档只做 cross-cutting
- **红线**：特性枚举不要堆砌——必须分类，且给"我们 MVP 取哪些"建议

### 2.4 内部代码探查型（hook 点 / 现状盘点）

- **对象**：自己仓库的代码现状（缺什么扩展点、已有什么 API）
- **方法**：搜索关键方法 → 列出已有/缺失 → 给推荐注入位置（带 `file:line`）
- **输出特征**：✅ 已存在 / ❌ 缺失 双栏；推荐位置精确到行号
- **红线**：必须声明"代码引用截至 YYYY-MM-DD，重新接入前需验证"——否则引用会过期失效

### 2.5 工具生态全景型

- **对象**：某个领域的可用工具全集（不是单产品分析）
- **方法**：穷举工具 → 维度矩阵（采集指标 / 接入方式 / 导出格式 / 程序化控制 / License）→ 自研 vs 复用决策
- **输出特征**：决策表 + 格式选型 + 落地 phase
- **红线**：禁止罗列不附决策——每个工具必须给"复用 / 复用并改造 / 不用"三选一的理由

## 3. 工作流：5 阶段法（每阶段：动作 → 产出 → 自检点）

### 阶段 0：定界（Timebox + High-Value Questions）

- **动作**：① 识别属于五种型态的哪一种（决定后续模板）；② 列出 3-5 个 **HVQ**——这次研究必须回答的核心问题，**每个必须是可判定谓词**（答案形态 Yes / No / Conditional；"X 好不好用"不可判定，要改写成可判定的）；③ 设定 timebox（默认 1-3 天，超过一个迭代周期就拆分）；④ 设定 **Superior Targets**（理想结论形态）与 **Critical Risk Ceilings**（不可接受的结论）。
- **产出**：型态判定 + HVQ 清单 + timebox + 目标/风险界。
- **自检点**：每个 HVQ 我能不能说出"什么答案算 Yes、什么算 No"？不能 → 它还不是谓词，重写。
- **反例**：跳过 HVQ 直接读源码 → 陷入"什么都知道一点但回答不了 plan"。

### 阶段 1：术语与全景

- **动作**：① 抓术语定义（规范术语 / 库 API 名 / 竞品概念词），消除歧义；② 看官方文档/规范顶部，建立领域地图；③ 列出待比较对象清单（不要漏主流玩家）。
- **产出**：术语表 + 领域地图 + 对象清单。
- **自检点**：两个来源对同一术语的用法一致吗？不一致 → 在报告里显式区分（术语没对齐就开工 → 后期矩阵前后矛盾）。

### 阶段 2：证据收集（Evidence）

| 型态 | 一手证据 | 二手证据 |
|------|---------|---------|
| Spec 解读 | 规范文本 + schema 文件 | 行业解读文章 |
| 库对比 | 源码（本地 clone） + 官方 API 文档 | issue / blog |
| 竞品分析 | 实际跑产品 / 本地 clone 源码 | 产品 docs / community |
| 内部探查 | 仓库搜索 + 带行号阅读 | git blame / 历史计划 |
| 工具生态 | README + 试跑 | 跨项目 issue tracker |

- **动作**：按型态采集一手/二手证据，逐条记录锚点（`file:line` / URL / 命令输出）。
- **产出**：证据清单（每条带锚点）。
- **自检点**：**每条事实都能追溯到 `file:line` 或 URL 吗**？（Claim ≠ Evidence：无来源支撑的判断只是 Claim）无来源的判断写进"启发"段，不混入"事实"段。
- **铁律**：比较实验在受控环境（本地 clone / 容器）进行，避免被版本漂移污染。

### 阶段 3：综合（Comparative Analysis）

- **动作**：① 填横向矩阵（维度 × 对象）；② 标共识（N 方一致）与差异化点（少数方做对了什么）；③ 对每个对象给"复用 / 复用并改造 / 不用"判定，每个候选的 trade-off 显式列出；④ **必须给"对本项目的启发"段**——research 价值的兑现。
- **产出**：横向矩阵 + 共识/差异化 + 决策清单 + 启发段。
- **自检点**：每条启发是"X 库做了 Y"（不合格）还是"本项目模块 M 在 P 阶段可以借鉴 X 的 Y"（合格，具体到模块/阶段且可被 arch/plan 引用为依据）？

### 阶段 4：结论 + 落点（Next Steps）

- **动作**：① 回顾阶段 0 的 HVQ——每个问题给出 Yes / No / Conditional 答案（+ 条件）；② 列"应该做的 / 不应该做的 / 待定的"三栏；③ 列出引用建议（"arch X / plan X 可基于本结论设计 Y"）；④ **声明时效**（"工具版本/字段以 YYYY-MM 调研时为准"）；⑤ 更新 research 索引（一行；载体 = `docs/research/RESEARCH.md` 索引表，首次落盘时随报告一并建立）；⑥ **Support 形态额外输出"满足调用者输入条件"的说明**。
- **产出**：结论段 + 三栏清单 + 引用建议 + 时效声明 + 索引行（+ Support 形态的 Useful 说明）。
- **自检点**：HVQ 全部回答了吗（含"未回答"也要显式写并说明原因）？

## 4. 文档模板

```markdown
---
name: <标题>
description: <一句话，含关键结论 + 引用的 arch/plan 编号 + 时效锚点>
type: reference | research
---

# <标题>

> 出处：<来源任务>。形态：Primary | Support（Support 时写调用者与输入条件 OQ）。
> HVQ：1. <问题1> 2. <问题2> 3. <问题3>

## 一、Scope（对象清单 / 术语表）
## 二、横向矩阵
| 维度 | 对象 A | 对象 B | 本项目选择 |
## 三、关键设计详解（逐对象，含 file:line 引用 + 对本项目的启发）
## 四、共识与差异化
## 五、对本项目的启发汇总（应该做 / 不应该做 / 待定期权）
## 六、Conclusions（逐条回答 HVQ）
## Sources
- [Title](url)
- 本地源码：`/path/to/file:line`
```

不同型态可裁剪：**Spec 解读型**弱化横向矩阵、强化"关键章节行号索引"；**内部探查型**弱化"启发"、强化"✅ 已存在 / ❌ 缺失 + 推荐注入位置（行号）"；**竞品分析型**每竞品独立一篇子文档、主文档只做 cross-cutting。

## 5. 质量红线（写完自检，任一条不达标不允许交接）

### 5.1 内容红线

- [ ] **HVQ 必答**：阶段 0 列的问题，结论段必须明确答复（Yes/No/Conditional + 条件）
- [ ] **每条事实有出处**：要么 `file:line`，要么 URL；模糊判断归入"启发"段
- [ ] **启发具体到模块/阶段**：禁止"可借鉴 X 库的 Y"空话
- [ ] **横向矩阵每列有差异**：无差异的列删掉或合并
- [ ] **决策清单完整**：每个对象都给"复用 / 改造复用 / 不用"判定

### 5.2 时效红线

- [ ] 文档开头注明"以 YYYY-MM 调研时为准"
- [ ] 引用本项目代码：声明"重新接入前需验证"
- [ ] 引用外部库：注明版本号
- [ ] 结论附**不确定性声明**（适用范围 / 有效期 / 未回答的问题）——调研报告必产工件为"结论 + 依据 + 不确定性声明"

### 5.3 结构红线

- [ ] frontmatter `description` 含关键结论（"调查 X，结论是 Y"，不是"调查了 X"）
- [ ] 同类多对象：每个独立成文，主文档只做汇总
- [ ] 末尾必有 `## Sources` 段

### 5.4 双形态红线

- [ ] `Relation(T)` 已显式登记（Primary / Support），未登记只算域内动作
- [ ] Support 形态：登记四项齐全（形态/调用者/输入条件/出口）
- [ ] Support 形态：结论含"满足调用者输入条件"的说明（`Useful(S,T)` 判据）

### 5.5 索引红线

- [ ] 交接后同步更新 research 索引一行

## 6. 反模式（必须避免）

| 反模式 | 症状 | 修正 |
|--------|------|------|
| **复述规范** | 文档只是规范的翻译版 | 加"本系统对应字段"段；删纯复述部分 |
| **无决策罗列** | 矩阵列了 15 个工具但没说复用谁 | 每个工具给"复用/改造/不用"判定 |
| **启发空话** | "可借鉴 X 的设计模式" | 改为"模块 M 的接口 P 阶段引入 X 的 Y 模式" |
| **跨型态混淆** | 把踩坑记录写成 research | 单点踩坑 → memory/feedback；系统性外部调查 → research |
| **过期不声明** | 引用行号但代码已重排 | 加"截至 YYYY-MM-DD"声明 |
| **HVQ 后置** | 写完才发现没回答调用者的问题 | 阶段 0 先列 HVQ，整篇围绕 HVQ 组织 |
| **未更新索引** | 写完文档但不入索引 | 交接动作必含索引一行更新 |
| **降格为 action** | "调研"变成一次搜索调用，失去契约与证据要求 | 调研是一等支撑域；search/retrieve/compare/synthesize 只是域内动作 |
| **支撑调研塞进主路径** | 主任务 DAG 被信息收集步骤污染，掩盖"支撑而非依赖" | 用 supports 关系登记（登记四项见 §双形态），不进 `depends_on` |
| **用独立调研公式判支撑调研** | 把"调研报告写完"当成支撑调研的完成 | 完成判据 = `Useful(S,T)`：调用者输入义务被满足 |
| **靠描述或角色推断关系** | "这是调研任务，所以它是支撑任务"式推断 | `Relation(T)` 是任务图显式取值，必须登记（推断会同时破坏路由与闭合） |

## 7. 交接、回报与失败处理

### 7.1 停止条件 / 交接条件 / 失败处理（本域行；跨域对照表权威见 domain-model）

| 项 | 内容 |
|---|---|
| **停止条件** | 调用者（或需求规格）规定的信息缺口已填满，结论有可复核来源 |
| **交接条件** | 调研工件（结论 + 依据 + 不确定性声明）+ 来源证据；**Support 形态额外输出"满足调用者输入条件"的说明** |
| **失败处理** | 关键信息不可获得 → 明示 Unknown 并回报（上冒由调度者执行）；无权限访问所需来源 → 回报 Blocked 权限不足；需扩大调研范围 → 回报由调度者决定是否开子任务（你**不能派发子代理**） |

### 7.2 交接清单

- [ ] §5 五组红线全部打勾
- [ ] HVQ 逐条有答复
- [ ] `Sources` 段完整
- [ ] frontmatter description 含结论 + 时效锚点
- [ ] 索引已更新
- [ ] （Support）登记四项 + Useful 说明齐全

### 7.3 回报格式（给调度者）

**正常交接**：

```text
【调研域交付】
- 形态：Primary / Support（Support 时：调用者 + 输入条件）
- 工件：<文件路径>（含结论 + 依据 + 不确定性声明）
- HVQ 答复：1. <Q> → Yes/No/Conditional  2. …
- 关键证据锚点：<file:line / URL 若干>
- 未回答/Unknown 项：<列出 + 原因>
- 自检结论：红线 N/N 打勾
```

**Blocked 回报**（信息不可获得 / 权限不足）：

```text
【调研域 Blocked：<信息不可获得 | 权限不足>】
- 挡住的 HVQ：<哪一问无法回答>
- 已尝试的获取路径：<搜过什么、试过什么>
- 需要谁提供什么：<具体到"只要拿到 X 就能回答">
- 其余部分可继续：<哪些 HVQ 已有结论>
```

**SupportRequest 回报**（支撑形态下再往下探一层）：

```text
【调研域 SupportRequest】
- 缺口：<需要什么上游事实/权限>
- 建议输入条件：<什么样的成果就能满足我这一层>
- 阻塞程度：<完全 / 部分>
```

## 8. 外部方法论参考

- [Template: Technical Spike — Microsoft Engineering Playbook](https://microsoft.github.io/code-with-engineering-playbook/design/design-reviews/recipes/templates/template-technical-spike/) — Goal / Method / Evidence / Conclusions / Next Steps 五段模板
- [The Art of the Technical Spike — ElastiFlow](https://www.elastiflow.com/blog/posts/the-art-of-the-technical-spike-how-to-research-what-you-dont-know) — HVQ + Superior Targets / Critical Risk Ceilings
- [ADRs, Trade-offs, and an ATAM-Lite Checklist — Microsoft Azure Architecture](https://techcommunity.microsoft.com/blog/azurearchitectureblog/how-great-engineers-make-architectural-decisions-%E2%80%94-adrs-trade-offs-and-an-atam-l/4463013) — 候选显式列 trade-off
- [Architecture Decision Record — Martin Fowler](https://martinfowler.com/bliki/ArchitectureDecisionRecord.html) — ADR 单决策粒度
- [Engineering Feasibility Spikes — Microsoft Engineering Playbook](https://microsoft.github.io/code-with-engineering-playbook/design/design-reviews/recipes/engineering-feasibility-spikes/) — 风险识别 + 缓解

## 9. 触发时机

- 用户说"调研 X / 看看 X 怎么做 / 调查 X 库"
- 调用者（设计/实施/审核域）发出 SupportRequest，由调度者派发
- 选型阶段：需要在 2 个以上候选方案中决策
- 引入新外部依赖前
- 写完一篇 research 准备交接时（用 §5 红线自检）

## 相关技能

- **dispatcher-orchestration**：调度者运行时；支撑请求闭环（SupportRequest → 派发 → 回填）由它执行。
- **domain-model**：支撑域双形态语义、`Useful(S,T)` 与 supports/dependsOn 区分的判定依据（**本手册已自足，无需读取**）。
- **domain-design / domain-implement / domain-review**：你的常见调用者（它们发 SupportRequest）。
- **memory-knowledge-system**：调研产出的"坑"归 memory/feedback，不混入 research。
