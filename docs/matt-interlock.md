# Matt 咬合规则（v7.0 收编版）

本插件自 v7.0 起将 Matt Pocock 技能集的 20 技能子集**收编进仓库**（`skills/` 下随插件分发，出处与全部改动见 [docs/matt-vendored.md](matt-vendored.md)），不再依赖用户本机安装 Matt 技能集。凡评审、修订、新增涉及自撰四技能（project-init／orient／checkpoint／memory-audit）与收编技能的接壤面，按此五条铁律执行。

## 1. 先读透，再断言

动收编件文本前先读其现行文件（本仓库 `skills/` 内即真相源，不再有「上游会变」的间接性）；断言「上游是什么样」时以 [docs/matt-vendored.md](matt-vendored.md) 的基线与改动清单为准，不凭记忆。拿不准「有没有定义」就派只读子代理逐条核实。

（先例：done／resolved 词表核查——证实 resolved 有定义于 local 模板 §Wayfinding、实现票终态在上游完全空白、日期批注会让字面判定误报；该缺口已由烤入补丁 #17 治理。）

## 2. 双向咬合检查

- **收编技能产出 → 我们消费**：`docs/agents/*.md`、`.scratch/` 票据与 map.md、`docs/research/`、GLOSSARY／ADR、handoff 便签——每个工件自撰技能要能认、能收、能对账。
- **我们产出 → 收编技能地盘**：凡在 repo 层立下的约定（如终态词表 `done`），必须经用户拍板登记进 `docs/agents/issue-tracker.md` 等收编技能认可的文档，不私设无出处的词表。

## 3. 出处单核对（替代旧「补丁在位核对」）

收编件上的每处偏离上游的改动都必须登记进 [docs/matt-vendored.md](matt-vendored.md)（含「治什么」列）——改动在仓库内，不会被冲掉，但**改收编件不记出处单＝私改**。动接壤面前先核对相关条目在位（grep 抽查）；上游同步（手动，可选）后须复查 #19-#23 剪枝区是否仍成立。

## 4. 副本联动

终态词表等约定以纪律合同（`skills/checkpoint/references/memory-discipline.md`）为单一真相源，README／orient／checkpoint／AGENTS.md 里的复述副本须同步改——改一处漏三处是已犯过的错。

## 5. 收编边界纪律

- **未收编不冒充**：grill-me、diagnosing-bugs、pr、wizard、wait-what、teach、to-questionnaire 七技能未收编（理由见出处单「收编范围」），自撰技能与 ask-matt 剪枝后文本不得向用户推荐它们；用户想收编哪个，走出处单流程（拷目录＋记出处＋重算闭合）。
- **本机旧副本勿复活**：不跑 `npx skills add mattpocock/skills`、不手动 cp 收编件到 `~/.zcode/skills/`——本地副本会遮蔽插件版，改插件不生效（README「第一次用」有说明）。
- **收编件 frontmatter 保真**：保留上游原样（name/description/disable-model-invocation），frontmatter 增补约定只约束自撰技能。
