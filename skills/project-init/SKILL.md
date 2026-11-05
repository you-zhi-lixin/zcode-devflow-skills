---
name: project-init
description: 项目一次性初始化：新项目铺全套地基（tracker 地基＋AGENTS.md 协作地图＋首条项目记忆＋告知日常节奏），存量项目只补地图。
license: MIT
when_to_use: 仅当用户明确输入 /project-init 或要求「初始化项目」时运行——未经用户明示要求不得自行调用。
disable-model-invocation: true
---

# project-init（项目地基）

两套体系的地基一次铺好：Matt 工程技能（grilling→to-spec→to-tickets→implement）要 tracker 配置；记忆套件（orient/checkpoint/memory-audit）要 AGENTS.md 地图与首条记忆。

先读 [`../checkpoint/references/memory-discipline.md`](../checkpoint/references/memory-discipline.md)（读不到→停下告知用户，尝试从本机其他副本恢复——`~/.agents/skills/` 同套件目录或插件缓存；都没有→告知用户重装本插件，本轮中止）——seed 记忆要过两问测试与写入四问。

## 过程

1. **前置检查**（只读）：新项目还是存量——repo 已有实质代码、票据或 git 史（任一即可）且 AGENTS.md/CLAUDE.md 无「记忆套件」子块＝存量；git 仓库有无；`docs/agents/issue-tracker.md` 有无（Matt setup 产出物）；AGENTS.md/CLAUDE.md 有无；记忆库空否。
   tracker 缺失→告知用户先跑 /setup-matt-pocock-skills（手动技能，本技能不得代为调用），**完成后重新输入 /project-init 继续**（重跑安全，已铺部分自动跳过）；用户不跑→向用户说明后果：工程技能会阻塞要求配置，记忆套件照常可用（票走 `.scratch/` 或无票）。tracker：记录任务清单的载体。
   存量项目→走第 2、4 步（只铺地图＋告知日常节奏，跳过 tracker 分岔与 seed）。

2. **铺 AGENTS.md 协作地图**：固定写 `<repo>/AGENTS.md`——ZCode 官方唯一自动载入的指令文件（CLAUDE.md 专用 Claude Code，ZCode 不保证载入）。项目只有 CLAUDE.md→新建 AGENTS.md，弹窗向用户说明分工：「记忆套件地图住 AGENTS.md，每次开工自动读；CLAUDE.md 留给读它的其他工具，不动。」Matt setup 写进 CLAUDE.md 的子块不被 ZCode 载入，但其技能按路径读 `docs/agents/*.md`，不受影响——只向用户说明，不迁移。「记忆套件」子块只在 CLAUDE.md 里→迁入 AGENTS.md，CLAUDE.md 侧旧块经用户确认后删。
   `## Agent skills` 块不存在则自建，块内追加「记忆套件」子块（已存在则原位更新；周边内容零覆盖）。没跑过 Matt setup→先建议跑 setup 再回来执行本步（第 1 步已明确拒绝的不再问）；此后重跑过 setup→复查子块是否仍在；子块被后续 setup 或内置 /init 覆盖丢失→补回。

   ```markdown
   ### 记忆套件

   - 一切记忆写入（含平时主动写入）过两问测试＋写入四问
   - 改现状条目＝整文件重写，不做增量补丁；断言带绝对日期
   - 索引（MEMORY.md）只做单行编辑
   - 续接既有项目的会话（含开场直接派活）先 orient 定位，再动手
   - 开工定位 orient（自动触发）；每票收口 /checkpoint（手动，并勾验收框＋置终态）；每收口满 2-3 行（票或轮）/memory-audit（手动，到值只是提醒，跑不跑由你决定）
   - 手工改过记忆文件后建议跑 /memory-audit 核一遍（手改当下没有自动检查）
   - 细节见 checkpoint 技能的 references/memory-discipline.md

   （本块为记忆套件流程约定：环境回顾、no-op 清理时勿删本块。）
   ```

   另加两行（存在才写，不虚构）：**拍板顺序**（业务规则以需求真相文件为准，视觉/执行值以设计规范为准，互斥以最新拍板为准）；**入口指针**（需求真相文件、设计规范目录路径）。可推断类信息（架构、目录布局、语言惯例）一律不写。「记忆套件」子块 ≤10 行（按非空行计）。
   **初始化台账**：`.scratch/memory-health.md` 不存在→创建（一行说明＋格式示例，见合同「记忆健康台账」节；只建档不追加行——初始化不是收口，不进体检计数）；已存在则不动。
   **终态词表登记**（repo 有 `docs/agents/issue-tracker.md` 且其 Conventions 无实现票终态、台账无「拒绝登记」病行时）：弹窗建议追加一行「本地实现票收口＝验收全勾＋`Status: done`（可带日期批注）；wayfinder 决策票（含 task 型）＝`Status: resolved`（见其 Wayfinding operations 节）」——经用户拍板后写入；拒绝→台账追加一行`病：用户拒绝终态词表登记（不再主动弹）`，不动 repo 文档，套件按合同「票据终态约定」继续，收口报告注明口径来源；弹窗未获应答→按合同兜底并追加`挂账`行（orient 简报重提）。

3. **seed 首条项目记忆**（存量默认跳过；已有项目身份类记忆→跳过）：向用户问两三个具体问题：产品给谁用、拍板规矩来源、硬约束；用户无法回答→不编造，留空或标「假设：」。过两问测试写 1 条 project 型记忆；repo 已记录的只留指针。无可写→跳过并向用户说明。同步 MEMORY.md 索引（单行追加，≤150 字符）。

4. **告知日常节奏**：向用户复述日常循环——开工 orient 自动弹简报；每票收口运行 /checkpoint（并收尾票据）；每收口满 2-3 行（票或轮）跑 /memory-audit（计数器到值只是提醒，跑不跑由用户决定）；流程不确定时问 ask-matt。
   **存量起步**：未 seed 的存量项目向用户说明「首条记忆由首次 /checkpoint 收口生成（空库新建合法）」，并问一句要不要现在就梳理一条项目现状记忆——要→按第 3 步口径补 seed；不要→止于说明，不代写，台账记一行（重跑不再问）。
   **拒绝记忆**：本技能内任何询问被用户明确拒绝→台账追加一行`病`注明「用户拒绝 X，不再主动询问」，重跑时先查台账跳过该询问；弹窗未获应答→按合同兜底＋`挂账`行（orient 简报重提）。
   完成＝按第 1 步分支该执行的第 2-4 步均已执行，跳过项已向用户说明。
