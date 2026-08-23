# project-engineering Skill 修改意见

- 评审日期：2026-08-23
- 评审对象：本仓库全部内容（`SKILL.md`、`MANIFEST.md`、`workflows/` 7 个、`checklists/` 5 个、`templates/` 7 个）
- 参照项目：[Lethefield](https://github.com/rayyen0902/Lethefield)（一套同理念体系在真实复杂项目上的落地实例）

## 总体评价

这套 skill 的方法论本身是扎实的：阶段划分完整、信源优先级明确、审批门禁和变更分级务实，反模式清单精准命中了 AI 代理的常见失效模式（编造需求、静默扩scope、无证据宣称完成）。与 Lethefield 对照后可以确认：两者是同一哲学的"通用抽象"与"具体实例"，方向没有偏差。

问题集中在**工程化程度**：文件之间断链、内容重复、约束停留在"人工承诺"层、若干高频场景缺少机制。以下问题按主题分组，每条给出问题、证据、影响和建议改法，末尾附优先级排序。

---

## A 组：结构性问题（骨架层面，最优先）

### A1. SKILL.md 与其余 19 个文件完全断链

- **问题**：SKILL.md 通篇没有引用 `workflows/`、`checklists/`、`templates/` 中的任何一个文件（已用 grep 验证，零匹配）。唯一的间接提示是 `MANIFEST.md` 里一句笼统的说明。
- **影响**：一个加载了本 skill 的 agent 并不知道这些文件的存在，更不知道什么时机读哪个。workflows、checklists、templates 三层的投入实际上不会被消费，skill 退化成只有 SKILL.md 单文件生效。
- **改法**：SKILL.md 每个 Phase 小节末尾加一行路由，指明三样东西——执行细则（workflow）、验收标准（checklist）、产物骨架（template）。示例：

  > ### Phase 2 — Requirements
  > …（现有内容）…
  > 执行细则见 `workflows/requirements.md`；通过标准见 `checklists/requirements.md`；产物使用 `templates/SPEC.md`。

  同时把 `MANIFEST.md` 扩成真正的文件地图：每个文件一行"何时用它"。

### A2. SKILL.md 与 workflows/ 内容重复，存在双真源

- **问题**：SKILL.md 的 Phase 2 列了 9 项需求要素，`workflows/requirements.md` 又把同样的内容列成 11 步；Phase 8 与 `workflows/implementation.md`、Phase 9 与 `workflows/testing.md` 同样大面积重叠。
- **影响**：两份内容独立的"真源"必然随时间漂移，而 SKILL.md 自己的信源规则没有覆盖"skill 内部文件冲突"这种情形。
- **改法**：明确分层并单向引用——SKILL.md 只保留原则、门禁、路由（做什么、为什么、去哪看），流程步骤的唯一真源放在 workflows/。这也符合 skill 的渐进披露惯例：SKILL.md 保持精简，细节文件按需加载，节省 agent 上下文。

### A3. 模板太薄，且有缺项

- **问题**：`templates/SPEC.md`、`templates/ARCHITECTURE.md`、`templates/PROJECT_STATE.md` 基本是 `TODO` 占位串，没有传递"写好是什么样"。另外 Phase 7 明确定义了任务五要素（objective / scope / dependencies / acceptance criteria / verification method），模板集中却没有对应的 `templates/TASK.md`。
- **影响**：模板的价值在于降低"写出来但不合格"的概率。纯 TODO 占位起不到这个作用；任务模板缺失则让每个项目自行发明任务格式。
- **改法**：给每个模板的关键小节加 1–2 句写法提示和约束（例如 SPEC 的"非目标"节给一句示例、PROJECT_STATE 标注"全文不超过一屏，历史归 git"）。补齐 `templates/TASK.md`，字段与 Phase 7 五要素一一对应。

## B 组：机制性缺口（有原则、无机制）

### B1. 门禁和约束停留在"人工承诺"层，未要求可执行化

- **问题**：checklists 全部是人工核对的 checkbox；SKILL.md 要求"完成需要证据"，但没有说约束应优先落成自动化检查。
- **对照**：Lethefield 把六条多租户红线写成 AST 静态扫描脚本接进 CI，README 明示"有自动化检查，不是人工承诺"。人工 checklist 是兜底，不是常态。
- **改法**：在 SKILL.md 的 Verify/Review 阶段和 checklists 头部加入原则：**凡可静态或自动检查的约束，必须落成脚本进 CI；人工核对只用于无法自动化的判断**。checklist 条目可标注 `(automatable)` 提示。

### B2. 反模式提了"别把旧文档当现状"，但没给防漂移机制

- **问题**：SKILL.md 只告诫"不要把旧文档当现行文档而不检查"，但没有任何让 agent 能检查的手段。
- **改法**：建立轻量约定：每份受控文档（SPEC、架构、ADR、PROJECT_STATE）头部带 `Status` 与 `Last verified` 日期；每次通过门禁评审时顺带刷新日期。模板中固化该头部。agent 读到长期未刷新的文档时应主动警觉并核实。

### B3. 缺少"中途接手项目"的入口流程

- **问题**：Bootstrap 一节只覆盖空仓库/文档差的仓库。但最高频场景是"加入一个按本体系正常运转的项目"——先读什么、如何从 PROJECT_STATE 判定当前阶段、如何发现文档间冲突，都没有流程。
- **改法**：新增一节"Joining an ongoing project"（或并入 Bootstrap）：固定顺序读 AGENTS.md → PROJECT_STATE.md → SPEC/架构/ADR → 任务；核对各文档 `Last verified`；输出一段话的"当前阶段判定 + 发现的不一致"给用户确认后再动手。

### B4. "material risk" 没有判据

- **问题**："不得静默跳过会带来 material risk 的阶段"——但 material 无定义，agent 无法自判。
- **改法**：直接复用文末已有的变更分级：跳过某阶段若影响 Material/Critical 级事项（API 契约、schema、服务边界、安全边界、重大依赖），即构成 material risk。一句话把两个孤立章节接上。

### B5. Checklist 无阻塞级区分与豁免惯例

- **问题**：所有 checkbox 等权；不适用的条目没有处理惯例。
- **影响**：评审清单的经典失效模式——空洞打勾、跳过不适用项不留痕迹，清单流于形式。
- **改法**：两条小规则写进每个 checklist 头部：① 阻塞项用 **(blocking)** 标注，其余为建议项；② 不适用的条目必须写 `N/A + 原因`，不允许跳过。

### B6. AGENTS.md 模板缺少"已验证事实/踩坑记录"功能

- **问题**：SKILL.md 要求 AGENTS.md "聚焦操作规则，别写成项目散文"，方向对，但漏了一类高价值内容：实测环境事实与踩坑记录。
- **对照**：Lethefield 的 AGENTS.md 大半篇幅是"已验证的环境事实（勿凭印象推翻）"——依赖库的序列化陷阱、内存不足的表现形式、历史 keyspace 累积拖垮测试等。这针对的是 AI 代理特有的失效模式：每个新会话凭训练印象重新"发现"已解决的问题。
- **改法**：在 SKILL.md Phase 6 和 `templates/AGENTS.md` 中增加一节"已验证事实 / Verified facts"：规则是只收录实测验证过、且与直觉或通用经验相悖的结论，每条注明来源（实测/演练记录）；明确指示 agent 不得凭印象推翻。同时保持 SKILL.md 现有的"不写散文"约束，防止该节膨胀。

### B7. 自主性边界缺少快速判据

- **问题**：变更分级（Trivial/Normal/Material/Critical）定义良好，但四级分类需要逐条比对，不适合 agent 在会话中快速自判"这件事我能不能自主做"。
- **对照**：Lethefield 用一句口诀收敛："改错了要不要动文档？要动文档的升级，只动代码的自主"——即设计未覆盖的分支升级确认，纯工程项自主。
- **改法**：在变更分级一节补一条快速判据作为入口（判据命中的直接自主，拿不准的再走四级分类），与 B4 的 material 定义互相引用。

### B8. 决策留痕未上升为基础设施要求

- **问题**：SKILL.md 要求"记录重要决策"（ADR），但记录动作依赖执行者自觉。
- **对照**：Lethefield 的运维操作全部强制参数绑定 + 自动写决策留痕库，留痕库不可达则拒绝执行（fail-closed）——记录决策是系统行为，不是流程要求。
- **改法**：这条不必照抄（多数项目没有留痕库），但可以在 SKILL.md 中加一个原则：**危险/运维类操作的工具设计应让留痕成为执行路径的强制环节**（例如脚本先写记录再执行，失败即中止），而不是事后补录。

## C 组：小问题（顺手改）

### C1. 阶段模型没有显式回路

13 个阶段写得像单行道，实际项目必然回退（实现中发现需求漏洞 → 回 Phase 2）。加一句：阶段可回退，回退时在 PROJECT_STATE 中更新阶段并记录触发原因。

### C2. 完成契约没有配套模板

SKILL.md 末尾的完成契约（六条报告项）很好，但没有模板化。可在 `templates/` 加一个简短的完成报告模板，或在 Phase 12 / maintenance workflow 里内联引用，保证各项目报告格式一致。

### C3. 仓库自身缺元信息

作为分发的 skill，目前无 LICENSE、无版本号、无使用示例（一个最小样例项目长什么样）。建议补 LICENSE 和 CHANGELOG（自家模板现成的）；示例可以等 1.0 再补。

---

## 优先级与实施顺序建议

| 优先级 | 条目 | 理由 |
|---|---|---|
| P0 | A1 断链、A2 去重、B5 checklist 规则 | 低风险高收益，纯文档编辑，立即提升 skill 实际可用性 |
| P1 | B4 material 判据、B7 自主性判据、C1 阶段回路 | 各一两句话，消除现有章节的歧义 |
| P1 | B6 AGENTS.md 已验证事实、B1 约束可执行化 | 从 Lethefield 验证过的经验，需要改写 Phase 6/9/10 表述 |
| P2 | A3 模板加厚 + TASK.md、B2 文档保鲜机制、B3 中途接手流程 | 新增内容较多，建议逐条确认后实施 |
| P2 | B8 留痕基础设施、C2 完成契约模板、C3 元信息 | 有价值但不阻塞使用 |

A 组解决"skill 能不能被正确消费"，B 组解决"原则能不能落地为行为"，C 组是润色。建议按 P0 → P1 → P2 分三轮提交，每轮可独立评审。
