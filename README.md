# ZCode DevFlow Skills

一套衔接 [Matt Pocock 技能集](https://github.com/mattpocock/skills)（grilling → to-spec → to-tickets → implement）与 ZCode 平台记忆系统的开发流程技能。四个技能对应四个不同节奏，覆盖项目全生命周期，彼此零重叠。

> 设计依据：对 Jesse Vincent、Anthropic 官方、github/spec-kit、BMAD-METHOD、Cline Memory Bank、Ralph loop、Manus、AI Hero 等业界实践的三路调研，并经三路独立子代理评审修复（fresh eyes 评审法）。

## 四个技能

| 技能 | 节奏 | 职能 | 触发 |
|---|---|---|---|
| [`project-init`](project-init/SKILL.md) | 每项目一次 | 接通 Matt setup 的 tracker 地基 ＋ 铺 AGENTS.md 记忆套件地图 ＋ seed 首条项目记忆 ＋ 交代日常节奏 | 手动 `/project-init` |
| [`orient`](orient/SKILL.md) | 每会话开始 | 开工定位：读记忆 → 对照票据/git 对账 → standup 简报（当前阶段/frontier/待拍板/建议下一步）→ 轻体检 ＋ 孤岛扫描 | 自动触发，也可手动 `/orient` |
| [`checkpoint`](checkpoint/SKILL.md) | 每票收口/会话收尾 | 收口沉淀：两问测试过滤 → 查重与现状条目整文件重写 → 落盘 → 报变更清单 | 手动 `/checkpoint` |
| [`memory-audit`](memory-audit/SKILL.md) | 每 2-3 大批次 | 记忆深度对账：全库断言级核验（过时/矛盾/越界/形态），治理 ＋ 孤岛合并，处置全过拍板 | 手动 `/memory-audit` |

共享纪律合同 [`checkpoint/references/memory-discipline.md`](checkpoint/references/memory-discipline.md) 是四个技能共用的单一真相源：四层地盘、两问测试、写入四问、重写律、索引律、体检红线。

## 完整流程

```
新项目 → /project-init（引导 setup-matt-pocock-skills + 铺地图 + seed 记忆）
   ↓
grill-with-docs →（research / prototype 旁路）→ to-spec → to-tickets
   ↓
┌─ 执行循环（一票一窗口）────────────────────┐
│ orient 自动弹简报 → /implement <票>          │
│ → /checkpoint → /clear → 下一张票           │
└─────────────────────────────────────────────┘
   ↓
/pr → /retro →（每 2-3 大批次）/memory-audit
```

## 核心设计决策

- **两问测试**（进平台记忆的准入闸，源自 AI Hero）：*下个月还为真吗？agent 能从仓库自行推出来吗？* 两问都过才写——进度细节、commit 号、测试数一律留 repo。
- **重写律**（治记忆膨胀与矛盾的根因）：project 型现状条目**整文件重写**，不做增量补丁；✅ 完结条目压成「结论＋红线＋指针」，交付流水账进 repo 存档。
- **四层地盘**：repo＝主状态 ／ handoff＝运输中的会话状态（落地即弃）／ 平台记忆＝两问测试通过的持久事实 ／ 会话上下文＝即弃。
- **孤岛防御**：平台按工作区路径哈希分桶记忆，换目录＝新空库。orient 每次开工扫同前缀旧库（空库也扫），memory-audit 负责合并。
- **防并发互踩**：落盘前重读，MEMORY.md 只做单行编辑。
- **纪律全域化**：AGENTS.md 记忆套件地图写明「一切记忆写入（含平时主动写入）过两问测试＋写入四问」，用每会话载入的文件约束平台常驻写入行为。

## 安装（ZCode）

```bash
# 把四个技能目录复制到 ZCode 技能目录
cp -r project-init orient checkpoint memory-audit ~/.zcode/skills/
```

**前置**：建议先装 Matt Pocock 技能集（`npx skills add mattpocock/skills`）并跑一次 `/setup-matt-pocock-skills`——本套件与其协作但可独立运行（无 tracker 配置时票走 `.scratch/` 本地文件）。

## 平台适配说明

- 本套件为 **ZCode** 编写（记忆目录 `~/.zcode/cli/memories/projects/<工作区哈希>/memory/`、MEMORY.md 每会话自动载入）。
- 技能正文为中文，术语与 Matt 技能集对齐（frontier / ticket / handoff / retro 等）。
- Windows 环境下用 Read 读候选记忆文件时，注意把 POSIX 路径展开为绝对路径（合同内已提示）。

## License

MIT
