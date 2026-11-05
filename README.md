# ZCode DevFlow Skills

一套衔接 [Matt Pocock 技能集](https://github.com/mattpocock/skills)（grilling → to-spec → to-tickets → implement）与 ZCode 平台记忆系统的开发流程技能。四个技能对应四个不同节奏，覆盖项目全生命周期，彼此零重叠。

## 第一次用（5 分钟上手）

1. 装 Node.js（去 nodejs.org 下载安装包一路下一步；装过就跳过）
2. 终端敲 `npx skills add mattpocock/skills`，装 Matt 技能集，并跑一次 `/setup-matt-pocock-skills` 配置 tracker（本套件可独立运行：没配 tracker 时票走 `.scratch/` 本地文件）
3. 安装本套件（二选一，**不可并用**——`~/.zcode/skills` 本地副本会永久遮蔽插件版，装了插件后请删除本地副本）：
   - **插件方式（推荐）**：ZCode → 设置 → 插件管理 → 发现页 → **＋添加插件市场** → 填本仓库（GitHub `you-zhi-lixin/zcode-devflow-skills` 或本地文件夹）→ 安装「ZCode DevFlow Skills」。四个技能与三条 /命令（`/project-init`、`/checkpoint`、`/memory-audit`）随插件一起装好。
   - **手动方式**：终端（Windows 用 Git Bash）进入本套件文件夹，敲：

     ```bash
     cp -r skills/project-init skills/orient skills/checkpoint skills/memory-audit ~/.zcode/skills/
     mkdir -p ~/.zcode/commands && cp commands/*.md ~/.zcode/commands/
     ```

4. 打开你的项目，输入 `/project-init`（输入 / 开头的命令就是在指挥 AI 干活）——它会带你铺好地基、告诉你以后每天怎么用。已有项目也可以跑：它会识别存量项目，只补 AI 协作地图，不动你的代码。

## 你会看到什么

- 开工时 AI 自动发一份**进度简报**（只看不改）
- 收口时（喊 `/checkpoint`）AI 给一张「这次记了什么」的清单
- 体检时（`/memory-audit`）AI 弹选择题请你拍板——**体检处置全部先问你**；收口写入有把握的直接落盘、写完报清单

## 四个技能

| 技能 | 节奏 | 职能 | 触发 |
|---|---|---|---|
| [`project-init`](skills/project-init/SKILL.md) | 每项目一次 | 接通 Matt setup 的 tracker 地基 ＋ 铺 AGENTS.md 记忆套件地图 ＋ seed 首条项目记忆 ＋ 交代日常节奏（存量项目＝只补地图） | 手动 `/project-init` |
| [`orient`](skills/orient/SKILL.md) | 每会话开始 | 开工定位：读记忆 → 对照票据/git 对账 → 简报（当前阶段/能开工的票/待拍板/建议下一步）→ 轻体检 ＋ 孤岛扫描 | 自动触发，也可手动 `/orient` |
| [`checkpoint`](skills/checkpoint/SKILL.md) | 每票收口/会话收尾 | 收口沉淀：两问测试过滤 → 查重与现状条目整文件重写 → 顺手把票收尾（勾验收框＋置终态）→ 落盘 → 报变更清单 | 手动 `/checkpoint` |
| [`memory-audit`](skills/memory-audit/SKILL.md) | 每收口 2-3 张票 | 记忆深度对账：全库逐句核验（过时/矛盾/越界/形态/断链），治理 ＋ 孤岛合并 ＋ 重建索引，处置全过拍板 | 手动 `/memory-audit` |

共享纪律合同 [`skills/checkpoint/references/memory-discipline.md`](skills/checkpoint/references/memory-discipline.md) 是四个技能共用的单一真相源：四层地盘、两问测试、写入四问、重写律、索引律、体检红线、记忆健康台账。

## 完整流程

```
新项目 → /project-init（引导 setup-matt-pocock-skills + 铺地图 + seed 记忆）
   ↓
grill-with-docs →（research / prototype 旁路）→ to-spec → to-tickets
   ↓
┌─ 执行循环（一票一窗口）──────────────────────┐
│ orient 自动弹简报 → /implement <票>            │
│ → /checkpoint（票收尾+沉淀）→ /clear → 下一张票 │
└───────────────────────────────────────────────┘
   ↓
/pr → /retro →（每收口 2-3 张票）/memory-audit
```

## 术语速查

| 术语 | 大白话 |
|---|---|
| 票（ticket） | 一张任务卡：做什么＋怎样算做完 |
| tracker | 记任务清单的地方 |
| frontier | 现在能开工的票 |
| 孤岛 | 同一项目在旧文件夹留下的另一套记忆 |
| 收口 | 一段活干完后的收尾：票写完结＋记忆存档 |
| 挂账 | 还没了结、等你拍板的事 |
| 对账 | 把两边记录（记忆 vs 票据/git）核对一遍 |
| done / resolved | 票的完结状态（实现票 done／决策票 resolved） |
| /handoff | 交接便签：把本次会话状态打包带走 |
| /retro | 复盘 |
| spec | 需求说明书 |

## 核心设计决策

- **两问测试**（进平台记忆的准入闸，源自 AI Hero）：*下个月还为真吗？agent 能从仓库自行推出来吗？* 两问都过才写——进度细节、commit 号、测试数一律留 repo。
- **重写律**（治记忆膨胀与矛盾的根因）：project 型现状条目**整文件重写**，不做增量补丁；✅ 完结条目压成「结论＋红线＋指针」，交付流水账进 repo 交付存档。
- **四层地盘**：repo＝主状态 ／ handoff＝运输中的会话状态（落地即弃）／ 平台记忆＝两问测试通过的持久事实 ／ 会话上下文＝即弃。
- **票收口闭环**：checkpoint 收口时顺手把票收尾（勾验收框＋置终态），漂移不再每票必现；本地实现票终态约定 `Status: done`，wayfinder 决策票走 `resolved`，远端按 tracker 文档关闭。
- **记忆健康台账**（`.scratch/memory-health.md`）：预警器有计数器——同一病连续报 2 次自动升级，收口满 2-3 票提醒体检，孤岛排查结论落账避免重复弹窗。
- **记忆容量闸**：MEMORY.md 是唯一常驻上下文的记忆层——索引条目 ≥30 触发瘦身预警（删除／合并／搬存档，处置过拍板），不让上下文税无限增长。
- **孤岛防御**：记忆按项目文件夹分开存放，换文件夹＝新空库。orient 每次开工扫旧库（空库也扫，初筛只回文件名不读内容），memory-audit 负责合并（合并前复述两库代表记忆供指认＋本库留溯源行，误合并可回滚）。
- **防并发互踩**：落盘前重读＋写后回读，MEMORY.md 只做单行编辑（唯一例外＝audit 的重建索引，过拍板）。
- **纪律全域化**：AGENTS.md 记忆套件地图写明「一切记忆写入（含平时主动写入）过两问测试＋写入四问」＋重写律短规，用每会话载入的文件约束平台常驻写入行为。

> 设计依据：对 Jesse Vincent、Anthropic 官方、github/spec-kit、BMAD-METHOD、Cline Memory Bank、Ralph loop、Manus、AI Hero 等业界实践的三路调研，并经多轮独立子代理评审修复（fresh eyes 评审法）。

## 平台适配说明

- 本套件为 **ZCode** 编写（记忆目录 `~/.zcode/cli/memories/projects/<项目文件夹>/memory/`、MEMORY.md 每会话自动载入）。
- 技能正文为中文，术语与 Matt 技能集对齐（frontier / ticket / handoff / retro 等）。
- Windows 环境下用 Read 读候选记忆文件时，注意把 POSIX 路径展开为绝对路径（合同内已提示；给 AI 看的技术提醒，你不用管）。

## License

MIT
