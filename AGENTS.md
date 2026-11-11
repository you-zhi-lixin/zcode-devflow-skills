# AGENTS.md — zcode-devflow-skills

ZCode 插件（devflow-market）：Matt Pocock 技能管线（grilling → to-spec → to-tickets → implement）的**记忆与对账层**，v7.0 起管线本体 20 技能已收编进本仓库（出处见 `docs/matt-vendored.md`）。纯内容仓库——没有构建／测试／lint 工具链，git 是唯一工具，改动即生效。

## 目录地图

| 路径 | 是什么 |
|---|---|
| `skills/{orient,checkpoint,memory-audit,project-init}/SKILL.md` | 四个自撰技能，正文全部简体中文 |
| `skills/`（其余 27 目录） | v7.0 收编的 Matt 技能全套（清单与全部改动：`docs/matt-vendored.md`），保留英文原文与上游 frontmatter |
| `skills/checkpoint/references/memory-discipline.md` | **单一真相源**：共享纪律合同（两问测试／写入四问／重写律／四层地盘／票据终态与票种口径／体检红线／记忆健康台账／拍板弹窗兜底） |
| `skills/*/references/*.md` | 技能附属分支细则（如 `orient/references/empty-library.md`）——随所属技能一起改，不跨技能引用 |
| `docs/matt-interlock.md` | Matt 咬合规则全文（AGENTS.md 正文只留指针）——动技能文本前必读 |
| `commands/*.md` | 20 条薄壳 /命令（自撰 4：orient、checkpoint、memory-audit、project-init；收编 16：ask-matt、grill-with-docs、triage、improve-codebase-architecture、setup-matt-pocock-skills、to-spec、to-tickets、implement、implement-spec、wayfinder、retro、handoff、grill-me、wait-what、teach、to-questionnaire）：frontmatter（description／argument-hint／skills）＋一行挂载技能＋`$ARGUMENTS`；model-invoked 收编技能不出命令（自动可达：diagnosing-bugs、pr、wizard） |
| `.zcode-plugin/plugin.json`、`marketplace.json` | 插件与市场清单；**版本号两处必须同步改** |
| `.scratch/memory-health.md` | 记忆健康台账：只追加、不改历史行（一行一事：`日期｜类型｜内容`） |
| `docs/matt-vendored.md` | 收编出处与改动清单：上游出处、MIT 许可证全文、收编范围（27 全收含决策轨迹）、烤入补丁 #1-18 与收编改动 #19-21、上游同步与老用户迁移 |

## 硬边界与编辑规则

- **纪律合同是唯一真相源**：两问测试、写入四问、重写律只写在 `memory-discipline.md`，SKILL.md 不重复；其余三个技能经相对路径 `../checkpoint/references/memory-discipline.md` 引用——移动／改名 `skills/checkpoint/` 须同步这三处引用。
- 技能内的相对路径引用以**技能文件所在目录**为基准展开，勿按项目 cwd 解析（commands 薄壳挂载不改变该基准）。
- **新增技能** = `skills/<name>/SKILL.md`（frontmatter：name／description／license／when_to_use）＋ `commands/<name>.md` 薄壳。除 `orient`（唯一自动触发的自撰技能）外，一律 `disable-model-invocation: true`，仅用户明示调用。**收编件例外**：frontmatter 与文本保上游原样，偏离须登记 `docs/matt-vendored.md`（咬合规则第 3 条）。
- **argument-hint 只在 `commands/*.md` 生效**，写在 SKILL.md 里是死键（checkpoint 踩过，见 git 历史）。
- 提交信息用中文 conventional 风格（`feat:`/`fix:`/`polish:`），需用户裁决的改动注明「用户拍板」。

## 平台约束（ZCode + Windows）

- 本套件按 ZCode 编写：记忆落点 `~/.zcode/cli/memories/projects/<项目文件夹>/memory/`，MEMORY.md 是唯一常驻上下文的记忆层；任何记忆写入过两问测试（下月还为真？repo 能自行推出？）——细则见纪律合同。
- Windows 下技能文中的 POSIX 路径（`~/.zcode/...`）用 Read 前先展开为绝对路径。
- 插件安装与手动 `cp` 到 `~/.zcode/skills` **不可并用**：本地副本会永久遮蔽插件版（README「第一次用」有说明）。
- `project-init` 给目标项目铺的协作地图固定落 `AGENTS.md`（ZCode 从 cwd 向上搜到项目根载入；CLAUDE.md 仅作迁移源出现）。

## Matt 咬合规则（动技能文本前必读）

Matt 技能集全部 27 技能已收编进本仓库（v7.0，用户拍板全收）。凡评审、修订、新增涉及自撰技能与收编技能的接壤面，**先读 [docs/matt-interlock.md](docs/matt-interlock.md)**——五条铁律：先读透再断言／双向咬合检查／出处单核对／副本联动／收编边界纪律（全收知情后果、本机旧副本勿复活）。

## 动敏感区前先读

- 动记忆纪律／写入规则 → `skills/checkpoint/references/memory-discipline.md`
- 动安装流程／版本／设计决策 → `README.md`（「第一次用」「核心设计决策」两节）
