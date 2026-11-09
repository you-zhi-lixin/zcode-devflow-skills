# ZCode DevFlow Skills

一套衔接 [Matt Pocock 技能集](https://github.com/mattpocock/skills)（grilling → to-spec → to-tickets → implement）与 ZCode 平台记忆系统的开发流程技能。四个技能对应四个不同节奏，覆盖项目全生命周期，彼此零重叠。

## 第一次用（5 分钟上手）

1. 装 Node.js（去 nodejs.org 下载安装包一路下一步；装过就跳过）
2. 终端敲 `npx skills add mattpocock/skills`，装 Matt 技能集，并跑一次 `/setup-matt-pocock-skills` 配置 tracker（本套件可独立运行：没配 tracker 时票走 `.scratch/` 本地文件）
3. 安装本套件（二选一，**不可并用**——`~/.zcode/skills` 本地副本会永久遮蔽插件版，装了插件后请删除本地副本）：
   - **插件方式（推荐）**：ZCode → 设置 → 插件管理 → 发现页 → **＋添加插件市场** → 填本仓库（GitHub `you-zhi-lixin/zcode-devflow-skills` 或本地文件夹）→ 安装「ZCode DevFlow Skills」。四个技能与四条 /命令（`/project-init`、`/orient`、`/checkpoint`、`/memory-audit`）随插件一起装好。
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
| [`orient`](skills/orient/SKILL.md) | 每会话开始 | 开工定位：读记忆 → 对照票据/git 对账 → 简报（当前阶段/能开工的票/待拍板/建议下一步）→ 轻体检 ＋ 空库时孤岛扫描 | 自动触发，也可手动 `/orient` |
| [`checkpoint`](skills/checkpoint/SKILL.md) | 每票收口/会话收尾 | 收口沉淀：两问测试过滤 → 查重与现状条目整文件重写 → 顺手把票收尾（勾验收框＋置终态）→ 落盘 → 报变更清单 | 手动 `/checkpoint` |
| [`memory-audit`](skills/memory-audit/SKILL.md) | 每收口 2-3 行（票或轮） | 记忆深度对账：全库逐句核验（过时/矛盾/越界/形态/断链），治理 ＋ 孤岛合并（转介/点名）＋ 重建索引，处置全过拍板 | 手动 `/memory-audit` |

共享纪律合同 [`skills/checkpoint/references/memory-discipline.md`](skills/checkpoint/references/memory-discipline.md) 是四个技能共用的单一真相源：四层地盘、两问测试、写入四问、重写律、索引律、体检红线、记忆健康台账。

## 完整流程

```
新项目 → /project-init（引导 setup-matt-pocock-skills + 铺地图 + seed 记忆）
   ↓
grill-with-docs →（research / prototype 旁路）→ to-spec → to-tickets
   ↓
┌─ 执行循环（大任务一票一窗口；小任务可多票/无票一窗口）┐
│ orient 自动弹简报 → /implement <票>            │
│ → /checkpoint（票收尾+沉淀）→ /clear → 下一张票 │
└───────────────────────────────────────────────┘
   ↓
/pr → /retro →（收口行满 2-3）/memory-audit
```

节奏的锚点是「收口」不是「票」：一个窗口跑完多张小票，收口一次记一行即可（有票记票数，无票记轮 N）；大任务习惯一票一窗口只是拆分偏好，不是流程要求。

## 术语速查

| 术语 | 大白话 |
|---|---|
| 票（ticket） | 一张任务卡：做什么＋怎样算做完 |
| tracker | 记任务清单的地方 |
| frontier | 现在能开工的票（Matt 侧叫法） |
| 台账 | 记忆健康台账（.scratch/memory-health.md），预警计数器 |
| 清账 | 挂账/病行办结后补的分界行 |
| 现状条目 | project 型记忆：记录「系统现在长什么样」的主文件 |
| 钩子句 | 索引行里的一句提示语 |
| 孤岛 | 同一项目在旧文件夹留下的另一套记忆 |
| 收口 | 一段活干完后的收尾：票写完结＋记忆存档 |
| 挂账 | 还没了结、等你拍板的事 |
| 对账 | 把两边记录（记忆 vs 票据/git）核对一遍 |
| done / resolved | 票的完结状态（实现票 done，可带日期批注／决策票含 task 型 resolved） |
| /handoff | 交接便签：把本次会话状态打包带走 |
| /retro | 复盘 |
| spec | 需求说明书 |

## 核心设计决策

每条＝决策＋治什么病；机制细则见技能正文与纪律合同，不在此复述。

- **两问测试**（准入闸，源自 AI Hero）：*下个月还为真吗？agent 能从仓库自行推出来吗？*——两问都过才写，防进度流水账毒化记忆。
- **重写律**（治膨胀与矛盾的根因）：project 型现状条目整文件重写，不做增量补丁。
- **四层地盘**：repo／handoff／平台记忆／会话上下文，每样东西只有一个真相源。
- **票收口闭环**（治票漂移）：checkpoint 顺手勾验收框＋置终态；终态词表（实现票 done／决策票 resolved，容忍日期批注）经拍板登记进 repo 的 issue-tracker 文档。
- **记忆健康台账**（预警器）：同一病连续报 2 次告警提级，收口行满 2-3（每轮一行）提醒体检；**计数器只做提醒，到值不代跑、不代执行，一切由用户拍板**。
- **记忆容量闸**（防上下文税）：MEMORY.md 索引 ≥30 触发瘦身预警。
- **孤岛防御**（治换文件夹丢记忆）：orient 仅在本库为空/新建时扫旧库——搬家后第一个会话自动发现并弹窗合并，已建库日常会话不扫不弹窗（2026-11-09 拍板）；audit 带防护合并（复述供指认＋溯源行，误合并可回滚）。
- **防并发互踩**（治多入口写坏）：落盘前重读＋写后回读，MEMORY.md 只做单行编辑（唯一例外＝audit 重建索引，过拍板）。
- **纪律全域化**（防平台写入绕过技能）：AGENTS.md 记忆套件地图约束一切记忆写入（含平台主动写入）。
- **弹窗未应答分级兜底**（防静默处置）：形式性修复照推荐执行并标注，内容性处置一律挂起留账、orient 简报重提；未获应答可同会话补拍一次再兜底；**应答不掌握**（如「不清楚／都是你干的」）同样不算拍板——不代编、不按推荐默认执行，能弱化的呈报弱化方案（＝补拍一次），不能弱化的挂起注明「因用户不掌握」。
- **收料弹窗结构化**（防自由输入空转）：向用户收事实/拍板/修正优先给可点选候选（附来源指针），点选确认或改写，不依赖自由文本——真实环境实测自由输入通道易空转。
- **收口推翻问句**（治「变更只往前写、不往回清」）：checkpoint 收口时从本会话提交增量预生成候选，主动问「本轮推翻了哪些既有描述」——记忆断言走写入四问第 4 问修正/删除，repo 文档只挂账提醒不代写；扫描必做、弹窗按需（无候选不弹）。
- **不做 hook**（既定决策）：hook 全局生效与「手动触发为主」「上下文是有限资源」相悖，`mcpServers`/`userConfig` 同理不引入；触发可靠性靠 when_to_use 措辞与 AGENTS.md 地图。

> 设计依据：对 Jesse Vincent、Anthropic 官方、github/spec-kit、BMAD-METHOD、Cline Memory Bank、Ralph loop、Manus、AI Hero 等业界实践的三路调研，并经多轮独立子代理评审修复（fresh eyes 评审法）。

## 平台适配说明

- 本套件为 **ZCode** 编写（记忆目录 `~/.zcode/cli/memories/projects/<项目文件夹>/memory/`、MEMORY.md 每会话自动载入）。
- 技能正文为中文，术语与 Matt 技能集对齐（frontier / ticket / handoff / retro 等）。
- Windows 环境下用 Read 读候选记忆文件时，注意把 POSIX 路径展开为绝对路径（合同内已提示；给 AI 看的技术提醒，你不用管）。

## License

MIT
