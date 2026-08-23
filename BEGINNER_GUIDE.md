# 编程小白操作手册 / Beginner Operations Manual

## 中文

这份手册给“不会或几乎不会编程”的人用。目标不是让你学会软件工程，而是让你用 `ray-engineering-skill` 管住 AI：你只负责确认目标、卡住范围、批准变更、验收证据；AI 负责走路径、写文档、写代码、跑验证。

### 0. 核心原则

不要让 AI 自由发挥。每个项目都从固定口令开始，每个任务都以证据结束。

> 没有运行命令和结果证据，就不算完成。

### 1. 起步准备

1. 建一个空仓库或空文件夹。
2. 把 `ray-engineering-skill/` 提供给 AI 编程环境。
   - 支持 skills：安装/启用 `ray-engineering-skill`。
   - 不支持 skills：至少先发 `SKILL.md` 和 `MANIFEST.md`，之后按 AI 的路由补发对应 workflow/checklist/template。
3. 发送第一句固定口令：

> 请使用 `ray-engineering-skill`。这是我的新项目。先从 Phase 0 / Phase 1 开始，只问 Critical 问题；在我明确说“requirements gate 通过”之前，不要写实现代码。产物先用最小集：`README.md`、`SPEC.md`、`PROJECT_STATE.md`、`AGENTS.md`。文档用中文写。

### 2. 你只负责 4 个批准点

1. **需求批准**：做什么、不做什么、怎么算完成。
2. **范围批准**：第一刀只做最小可见版本。
3. **架构/重大变更批准**：只有涉及对外接口、数据结构、登录权限、数据库、部署、安全边界时才需要。
4. **发布批准**：检查项全过、证据齐全，才允许说发布。

### 3. 标准流程

#### Step 1：说清最小问题

回答 AI 的关键问题即可：给谁用、解决什么痛、最小可见结果、明确不做什么、硬限制是什么。

AI 产出 `SPEC.md` 后，你只检查三点：目标对不对；非目标有没有卡住范围；验收标准能不能判断成败。

确认后说：

> requirements gate 通过。进入 Phase 3，只选最小 vertical slice；不要做大而全第一版。

#### Step 2：切第一刀

> 请把第一个 vertical slice 写成 `tasks/TASK-001.md`，字段按 `templates/TASK.md`。只做这一刀，别顺手实现后续功能。

要求：一个 TASK 最好 30 分钟到 2 小时能完成；完成时有可见结果；有最少验证方式。

#### Step 3：默认不要重架构

> 除非存在 Material/Critical 风险，否则不要做重型架构设计。若你认为需要架构，请先列出为什么，并等我确认 architecture gate。

如果 AI 要改对外接口、数据结构、登录权限、数据库、部署或安全边界，让它先更新 `SPEC.md` / `ARCHITECTURE.md` / `ADR.md`，你再确认：

> change gate 通过，可以继续。

#### Step 4：先立规矩，再写码

> 请建立最小 `AGENTS.md`：只写这个项目真实需要的运行/测试命令、禁止操作、目录规则。不要写散文。

你重点看：怎么运行、怎么测试、禁止什么、已验证事实是否要求“不要凭印象推翻”。

#### Step 5：任务循环

每个任务都用同一段口令：

> 请只做 `tasks/TASK-001.md`。开始前先读 `AGENTS.md`、`PROJECT_STATE.md`、相关 `SPEC.md`。完成后必须按 `templates/COMPLETION_REPORT.md` 汇报：改了什么、为什么、跑了哪些命令、证据在哪、还有什么不确定。没有证据不要说完成。

你验收时只看四点：验收标准是否逐条对应；命令是否真的跑了；跳过项是否写了 `N/A: 原因`；`PROJECT_STATE.md` 是否更新。

如果 AI 只说“已完成”，回：

> 不接受。没有 verification evidence。请补齐实际运行命令、输出摘要和剩余风险。

#### Step 6：发布前检查

> 请按 `checklists/release.md` 做发布前检查。阻塞项必须过；不适用项写 `N/A: 原因`。通过后更新 `CHANGELOG.md` 和 `PROJECT_STATE.md`。

确认后说：

> release gate 通过。标记当前状态，并给出下一个最高优先级 TASK，但不要开始实现。

### 4. 最小文件集

第一个小项目只需要：

```text
README.md            这是什么、怎么跑
SPEC.md              做什么/不做什么/怎么算成功
PROJECT_STATE.md     当前阶段、下一步、已知问题
AGENTS.md            AI 在本仓库必须遵守的规则
tasks/TASK-001.md    当前这一刀
```

复杂以后再补：`ARCHITECTURE.md`、`ADR.md`、`CHANGELOG.md`。

### 5. 安全红线

出现以下情况，必须停下来单独确认：

- AI 要删除数据、重置环境、force push、改发布配置；
- AI 要新增密钥、Token、账号体系或外部依赖；
- AI 要改 `SPEC.md` 里的目标/非目标/验收标准；
- AI 说“完成”但没有命令、输出、测试或证据位置；
- AI 要跳过 blocking checklist 项，且没有你的明确豁免。

---

## English

This manual is for people with little or no programming experience. The goal is not to teach software engineering. The goal is to let you use `ray-engineering-skill` to control the AI: you confirm the goal, constrain scope, approve material changes, and accept evidence; the AI follows the route, writes the docs, writes the code, and runs verification.

### 0. Core rule

Do not let the AI freestyle. Start every project with the fixed prompt, and end every task with evidence.

> No commands run and no result evidence means not complete.

### 1. Setup

1. Create an empty repository or folder.
2. Provide `ray-engineering-skill/` to the AI coding environment.
   - If skills are supported: install/enable `ray-engineering-skill`.
   - If not: send at least `SKILL.md` and `MANIFEST.md`, then send the routed workflow/checklist/template when asked.
3. Send the fixed first prompt:

> Use `ray-engineering-skill`. This is my new project. Start with Phase 0 / Phase 1 and ask only Critical questions. Do not write implementation code until I explicitly say “requirements gate passed”. Use the minimum artifact set first: `README.md`, `SPEC.md`, `PROJECT_STATE.md`, `AGENTS.md`. Write documents in Chinese.

### 2. You own only 4 approvals

1. **Requirements approval**: what to build, what not to build, and what counts as done.
2. **Scope approval**: the first slice is the smallest visible version.
3. **Architecture/material-change approval**: only when external contracts, data model, auth, database, deployment, or security boundaries are involved.
4. **Release approval**: checks pass and evidence is complete before anyone says “released”.

### 3. Standard flow

#### Step 1: state the smallest real problem

Answer only the critical questions: who uses it, what pain it removes, the smallest visible outcome, explicit non-goals, and hard constraints.

After the AI produces `SPEC.md`, check three things: the goal is right; non-goals constrain scope; acceptance criteria can decide success/failure.

Then say:

> requirements gate passed. Move to Phase 3 and choose only the smallest vertical slice. Do not build a large first version.

#### Step 2: cut the first slice

> Turn the first vertical slice into `tasks/TASK-001.md` using `templates/TASK.md`. Do only this slice; do not implement later features along the way.

Require: one task should finish in about 30 minutes to 2 hours; it has a visible result; it has a minimal verification method.

#### Step 3: no heavy architecture by default

> Unless there is Material/Critical risk, do not do heavy architecture design. If you think architecture is needed, list why first and wait for my architecture gate confirmation.

If the AI wants to change external contracts, data model, auth, database, deployment, or security boundaries, require updates to `SPEC.md` / `ARCHITECTURE.md` / `ADR.md` first, then say:

> change gate passed. Continue.

#### Step 4: rules before code

> Create a minimal `AGENTS.md`: only the run/test commands this project really needs, forbidden operations, and directory rules. Do not write an essay.

Check: how to run, how to test, what is forbidden, and whether verified facts say “do not override from memory”.

#### Step 5: task loop

Use the same prompt for every task:

> Do only `tasks/TASK-001.md`. Before starting, read `AGENTS.md`, `PROJECT_STATE.md`, and the relevant `SPEC.md`. When done, report using `templates/COMPLETION_REPORT.md`: what changed, why, which commands were run, where the evidence is, and what remains uncertain. Do not claim completion without evidence.

When accepting, check only four things: acceptance criteria map one by one; commands actually ran; skipped items say `N/A: <reason>`; `PROJECT_STATE.md` is updated.

If the AI only says “done”, reply:

> Not accepted. No verification evidence. Provide the actual commands, output summary, and remaining risks.

#### Step 6: release check

> Run the release check using `checklists/release.md`. Blocking items must pass; non-applicable items must say `N/A: <reason>`. After passing, update `CHANGELOG.md` and `PROJECT_STATE.md`.

Then say:

> release gate passed. Mark the current state and propose the next highest-priority TASK, but do not start implementing it.

### 4. Minimum file set

The first small project only needs:

```text
README.md            what this is and how to run it
SPEC.md              what / not-what / how success is judged
PROJECT_STATE.md     current phase, next step, known issues
AGENTS.md            rules the AI must follow in this repo
tasks/TASK-001.md    the current slice
```

Add later only when complexity justifies it: `ARCHITECTURE.md`, `ADR.md`, `CHANGELOG.md`.

### 5. Safety red lines

Stop and ask for explicit confirmation when the AI wants to:

- delete data, reset the environment, force push, or change release configuration;
- add secrets, tokens, account systems, or external dependencies;
- change goals/non-goals/acceptance criteria in `SPEC.md`;
- claim completion without commands, output, tests, or evidence location;
- skip a blocking checklist item without your explicit waiver.
