# Matt 咬合规则

本插件永远与 Matt Pocock 技能集（本机 `~/.agents/skills/`，`~/.zcode/skills/` 为其符号链接）搭配使用。凡评审、修订、新增涉及四个技能与 Matt 技能的接壤面，按此四条铁律执行。

## 1. 先读透，再断言

动文本前先读 Matt 侧现行文件（`setup-matt-pocock-skills` 及其 issue-tracker-*.md／triage-labels.md／domain.md，`implement`／`to-spec`／`to-tickets`／`handoff`／`retro`／`wayfinder`／`triage`／`ask-matt`），以实际文件为准——上游更新会变，不凭记忆或转述下结论；拿不准「有没有定义」就派只读子代理逐条核实，实测校准。

（先例：done／resolved 词表核查——证实 resolved 有定义于 local 模板 §Wayfinding、实现票终态在上游完全空白、日期批注会让字面判定误报。）

## 2. 双向咬合检查

- **Matt 产出 → 我们消费**：`docs/agents/*.md`、`.scratch/` 票据与 map.md、`docs/research/`、GLOSSARY／ADR（含 multi-context 布局）、handoff 便签——每个工件我们的技能要能认、能收、能对账。
- **我们产出 → Matt 地盘**：凡在 repo 层立下的约定（如终态词表 `done`），必须经用户拍板登记进 `docs/agents/issue-tracker.md` 等 Matt 文档，不私设无出处的词表。

## 3. 补丁层核对

`MATT-PATCHES.md` 是咬合修正的落点（上游更新即冲掉）——动咬合面前先核对补丁在位（grep 抽查，防"台账记了没打"）；新发现的咬合缺口优先写成补丁单条目（含「治什么」列），而非改 Matt 文件本体不留单。

## 4. 副本联动

终态词表等约定以纪律合同（`skills/checkpoint/references/memory-discipline.md`）为单一真相源，README／orient／checkpoint／AGENTS.md 里的复述副本须同步改——改一处漏三处是已犯过的错。
