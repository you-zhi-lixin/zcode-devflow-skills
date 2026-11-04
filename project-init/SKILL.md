---
name: project-init
description: 项目一次性初始化（新项目铺全套地基，存量项目只补地图）：接通 Matt 工程技能的地基（tracker 配置），铺记忆套件的地基（AGENTS.md 协作地图、首条项目记忆），并交代日常使用节奏。
disable-model-invocation: true
---

# project-init（项目地基）

两套体系的地基一次铺好：Matt 工程技能（grilling→to-spec→to-tickets→implement）要 tracker 配置；记忆套件（orient/checkpoint/memory-audit）要 AGENTS.md 地图与首条记忆。

先读 [`../checkpoint/references/memory-discipline.md`](../checkpoint/references/memory-discipline.md)（读不到→停下告知用户，可从套件 git 副本恢复）——seed 记忆要过它的两问测试与写入四问。

## 过程

1. **前置检查**（只读）：新项目还是存量项目——repo 已有可观代码/票据/git 史但 AGENTS.md/CLAUDE.md 无「记忆套件」子块＝存量项目；git 仓库有无；`docs/agents/issue-tracker.md` 存在与否（Matt setup 的产出物）；AGENTS.md/CLAUDE.md 存在与否；记忆库（路径见系统提示的 memory 说明）空否。
   tracker 配置缺失→告知用户：先跑 /setup-matt-pocock-skills（手动技能，本技能无法代调），**它完成后重新输入 /project-init 继续**（重跑安全：已铺好的部分自动跳过，不会写重）；用户不跑则说明后果——to-tickets/triage 等工程技能会阻塞并要求配置，记忆套件照常可用（票走 `.scratch/` 或无票）。tracker 就是记任务清单的地方，Matt 那套发任务的工具要用它。
   存量项目→走第 2、4 步（只铺地图＋交代节奏，跳过 tracker 分岔与 seed），除非用户想要工程技能地基。
   完成＝四项现状在手，setup 分岔／存量分支有明确下一步。

2. **铺 AGENTS.md 协作地图**：按 Matt setup 的选文件规则——CLAUDE.md 已存在则用它，否则 AGENTS.md，两者都无→弹窗二选一（推荐项放第一）：**推荐 AGENTS.md**（多家 AI 工具都认这个文件名，通用）；CLAUDE.md 是 Claude Code 专用。弹窗附一句大白话：这个文件是写给 AI 助手看的项目说明书，每次开工 AI 会自动读它，告诉它这个项目的规矩。
   `## Agent skills` 块不存在则自建一个最小块，然后在块内追加「记忆套件」子块（已存在则原位更新；周边用户内容零覆盖）。本仓库还没跑过 Matt setup→先建议跑 setup 再回来执行本步；此后若重跑过 setup，复查本子块仍在（setup 的原位更新可能把它挤掉），丢了就原位补回。

   ```markdown
   ### 记忆套件

   - 一切记忆写入（含平时主动写入）过两问测试＋写入四问
   - 改现状条目＝整文件重写，不做增量补丁；断言带绝对日期
   - 索引（MEMORY.md）只做单行编辑
   - 续接既有项目的会话（含开场直接派活）先 orient 定位，再动手
   - 开工定位 orient（自动触发）；每票收口 /checkpoint（手动，收口时顺手把票的验收勾选与终态补上）；每收口 2-3 张票 /memory-audit（手动）
   - 细节见 checkpoint 技能的 references/memory-discipline.md
   ```

   另加两行（有才写，不虚构）：**拍板顺序**一行（业务规则以需求真相文件为准，视觉/执行值以设计规范为准，互斥以最新拍板为准）；**入口指针**一行（需求真相文件、设计规范目录的路径）。可推断类信息（架构、目录布局、语言惯例）一律不写。
   完成＝地图 ≤10 行，既有内容零覆盖。

3. **seed 首条项目记忆**（存量项目默认跳过）：记忆库已有项目身份类记忆→跳过（重复 init 不重建）。否则先向用户问两三个具体问题——给谁用、拍板规矩从哪来、硬约束（预算/环境/人的依赖）；用户答不上来的项不编造，留空或标注「假设：」。过两问测试后写 1 条 project 型记忆；repo 已记录的（PRD 内容本身）只留指针。确实无可写→跳过并向用户说明。同步更新 MEMORY.md 索引（单行追加，≤150 字符）。
   完成＝记忆文件与索引行已落盘，或明确跳过并说明。

4. **交代节奏**：向用户复述日常循环四句话——开工 orient 自动弹简报（开场直接派活也先 orient）；每票收口喊 /checkpoint（收口时会把票的验收框勾上、状态置终态）；每收口 2-3 张票跑 /memory-audit；迷路问 ask-matt。
   完成＝四句话已向用户复述。
