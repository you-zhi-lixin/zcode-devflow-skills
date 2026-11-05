# AGENTS.md — zcode-devflow-skills

ZCode 插件（devflow-market）：衔接 Matt Pocock 技能管线（grilling → to-spec → to-tickets → implement）的**记忆与对账层**。纯内容仓库——没有构建／测试／lint 工具链，git 是唯一工具，改动即生效。

## 目录地图

| 路径 | 是什么 |
|---|---|
| `skills/{orient,checkpoint,memory-audit,project-init}/SKILL.md` | 四个技能，正文全部简体中文 |
| `skills/checkpoint/references/memory-discipline.md` | **单一真相源**：共享纪律合同（两问测试／写入四问／重写律／四层地盘／体检红线／记忆健康台账／拍板弹窗兜底） |
| `commands/*.md` | 四条薄壳 /命令（orient、checkpoint、memory-audit、project-init）：frontmatter（description／argument-hint／skills）＋一行挂载技能＋`$ARGUMENTS` |
| `.zcode-plugin/plugin.json`、`marketplace.json` | 插件与市场清单；**版本号两处必须同步改** |
| `.scratch/memory-health.md` | 记忆健康台账：只追加、不改历史行（一行一事：`日期｜类型｜内容`） |
| `MATT-PATCHES.md` | 打在本机 Matt 技能（`~/.agents/skills/`）上的补丁台账；上游 `npx skills add mattpocock/skills` 更新会冲掉，按单重打 |

## 硬边界与编辑规则

- **纪律合同是唯一真相源**：两问测试、写入四问、重写律只写在 `memory-discipline.md`，SKILL.md 不重复；其余三个技能经相对路径 `../checkpoint/references/memory-discipline.md` 引用——移动／改名 `skills/checkpoint/` 须同步这三处引用。
- 技能内的相对路径引用以**技能文件所在目录**为基准展开，勿按项目 cwd 解析（commands 薄壳挂载不改变该基准）。
- **新增技能** = `skills/<name>/SKILL.md`（frontmatter：name／description／license／when_to_use）＋ `commands/<name>.md` 薄壳。除 `orient`（唯一自动触发的技能）外，一律 `disable-model-invocation: true`，仅用户明示调用。
- **argument-hint 只在 `commands/*.md` 生效**，写在 SKILL.md 里是死键（checkpoint 踩过，见 git 历史）。
- 提交信息用中文 conventional 风格（`feat:`/`fix:`/`polish:`），需用户裁决的改动注明「用户拍板」。

## 平台约束（ZCode + Windows）

- 本套件按 ZCode 编写：记忆落点 `~/.zcode/cli/memories/projects/<项目文件夹>/memory/`，MEMORY.md 是唯一常驻上下文的记忆层；任何记忆写入过两问测试（下月还为真？repo 能自行推出？）——细则见纪律合同。
- Windows 下技能文中的 POSIX 路径（`~/.zcode/...`）用 Read 前先展开为绝对路径。
- 插件安装与手动 `cp` 到 `~/.zcode/skills` **不可并用**：本地副本会永久遮蔽插件版（README「第一次用」有说明）。
- `project-init` 给目标项目铺的协作地图固定落 `AGENTS.md`（ZCode 从 cwd 向上搜到项目根载入；CLAUDE.md 仅作迁移源出现）。

## Matt 咬合规则（动技能文本前必读）

本插件永远与 Matt Pocock 技能集（本机 `~/.agents/skills/`，`~/.zcode/skills/` 为其符号链接）搭配使用——凡是评审、修订、新增涉及四个技能与 Matt 技能的接壤面，按此流程：

1. **先读透，再断言**：动文本前先读 Matt 侧现行文件（`setup-matt-pocock-skills` 及其 issue-tracker-*.md／triage-labels.md／domain.md，`implement`／`to-spec`／`to-tickets`／`handoff`／`retro`／`wayfinder`／`triage`／`ask-matt`），以实际文件为准——上游更新会变，不凭记忆或转述下结论；拿不准「有没有定义」就派只读子代理逐条核实，实测校准（先例：done／resolved 词表核查，证实 resolved 有定义于 local 模板 §Wayfinding、实现票终态在上游完全空白）。
2. **双向咬合检查**：
   - Matt 产出 → 我们消费：`docs/agents/*.md`、`.scratch/` 票据与 map.md、`docs/research/`、GLOSSARY／ADR（含 multi-context 布局）、handoff 便签——每个工件我们的技能要能认、能收、能对账；
   - 我们产出 → Matt 地盘：凡在 repo 层立下的约定（如终态词表 `done`），必须经用户拍板登记进 `docs/agents/issue-tracker.md` 等Matt 文档，不私设无出处的词表。
3. **补丁层核对**：`MATT-PATCHES.md` 是咬合修正的落点（上游更新即冲掉）——动咬合面前先核对补丁在位（grep 抽查）；新发现的咬合缺口优先写成补丁单条目（含「治什么」列），而非改 Matt 文件本体不留单。
4. **副本联动**：终态词表等约定以纪律合同为单一真相源，README／orient／checkpoint／本文件里的复述副本须同步改——改一处漏三处是已犯过的错。

## 动敏感区前先读

- 动记忆纪律／写入规则 → `skills/checkpoint/references/memory-discipline.md`
- 动安装流程／版本／设计决策 → `README.md`（「第一次用」「核心设计决策」两节）
