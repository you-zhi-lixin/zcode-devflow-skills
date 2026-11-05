---
name: project-init
description: 项目一次性初始化：新项目铺全套地基（tracker 地基＋AGENTS.md 协作地图＋首条项目记忆＋交代节奏），存量项目只补地图。
license: MIT
when_to_use: 仅当用户明确输入 /project-init 或要求「初始化项目」时运行——未经用户开口不得自行调用。
disable-model-invocation: true
---

# project-init（项目地基）

两套体系的地基一次铺好：Matt 工程技能（grilling→to-spec→to-tickets→implement）要 tracker 配置；记忆套件（orient/checkpoint/memory-audit）要 AGENTS.md 地图与首条记忆。

先读 [`../checkpoint/references/memory-discipline.md`](../checkpoint/references/memory-discipline.md)（读不到→停下告知用户，可从套件 git 副本恢复）——seed 记忆要过两问测试与写入四问。

## 过程

1. **前置检查**（只读）：新项目还是存量——repo 已有可观代码/票据/git 史但 AGENTS.md/CLAUDE.md 无「记忆套件」子块＝存量；git 仓库有无；`docs/agents/issue-tracker.md` 有无（Matt setup 产出物）；AGENTS.md/CLAUDE.md 有无；记忆库空否。
   tracker 缺失→告知用户先跑 /setup-matt-pocock-skills（手动技能，无法代调），**完成后重新输入 /project-init 继续**（重跑安全，已铺部分自动跳过）；用户不跑则说明后果——工程技能会阻塞要求配置，记忆套件照常可用（票走 `.scratch/` 或无票）。tracker＝记任务清单的地方。
   存量项目→走第 2、4 步（只铺地图＋交代节奏，跳过 tracker 分岔与 seed）。

2. **铺 AGENTS.md 协作地图**：CLAUDE.md 已存在则用它，否则 AGENTS.md，两者都无→弹窗二选一（推荐 **AGENTS.md**，多家 AI 工具通用；CLAUDE.md 是 Claude Code 专用），并附一句大白话：这是写给 AI 助手看的项目说明书，每次开工自动读。
   `## Agent skills` 块不存在则自建，块内追加「记忆套件」子块（已存在则原位更新；周边内容零覆盖）。没跑过 Matt setup→先建议跑 setup 再回来执行本步（第 1 步已明确拒绝的不再问）；此后重跑过 setup→复查子块仍在，被挤掉就补回。

   ```markdown
   ### 记忆套件

   - 一切记忆写入（含平时主动写入）过两问测试＋写入四问
   - 改现状条目＝整文件重写，不做增量补丁；断言带绝对日期
   - 索引（MEMORY.md）只做单行编辑
   - 续接既有项目的会话（含开场直接派活）先 orient 定位，再动手
   - 开工定位 orient（自动触发）；每票收口 /checkpoint（手动，顺手勾验收框＋置终态）；每收口满 2-3 行（票或轮）/memory-audit（手动）
   - 细节见 checkpoint 技能的 references/memory-discipline.md

   （本块为记忆套件流程约定：环境回顾／no-op 清理勿删。）
   ```

   另加两行（有才写，不虚构）：**拍板顺序**（业务规则以需求真相文件为准，视觉/执行值以设计规范为准，互斥以最新拍板为准）；**入口指针**（需求真相文件、设计规范目录路径）。可推断类信息（架构、目录布局、语言惯例）一律不写。地图 ≤10 行。

3. **seed 首条项目记忆**（存量默认跳过；已有项目身份类记忆→跳过）：问两三个具体问题——给谁用、拍板规矩从哪来、硬约束；答不上不编造，留空或标「假设：」。过两问测试写 1 条 project 型记忆；repo 已记录的只留指针。无可写→跳过并说明。同步 MEMORY.md 索引（单行追加，≤150 字符）。

4. **交代节奏**：向用户复述日常循环——开工 orient 自动弹简报；每票收口喊 /checkpoint（顺手把票收尾）；每收口满 2-3 行（票或轮）跑 /memory-audit；迷路问 ask-matt。
