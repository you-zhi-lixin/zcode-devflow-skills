# Matt 技能收编出处与改动清单（v7.0，2026-11-11）

本插件自 v7.0 起，将 Matt Pocock 技能集**全部 27 个技能收编进仓库**（`skills/` 下随插件分发），不再要求用户本机安装 `~/.agents/skills/`。收编意味着：**上游更新不再自动到达**，同步上游改为手动可选动作（见文末）；下列改动直接落在收编件上，不存在「补丁被上游更新冲掉」的问题。

## 出处与许可证

- 上游仓库：https://github.com/mattpocock/skills （MIT License）
- 收编基线：2026-11-11 自本机已装副本拷贝（该副本含下表 #1-#18 全部改动），拷贝后逐目录 `diff -r` 核对逐字节一致
- 上游许可证全文（MIT，须随收编件保留）：

```
MIT License

Copyright (c) 2026 Matt Pocock

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

## 收编范围（27，全收集）

**决策轨迹**：2026-11-11 初版方案收 20（17 硬依赖闭合＋3 咬合可选），其余 7 个以「model-invoked 自动介入用户项目超出咬合面」为由不收；**同日用户翻案拍板全收**——插件定位是给用户完整的 Matt 技能集体验，独立使用的工具不必与记忆层咬合，AI 自动用上它们正是提升准确与效率的题中之义。据此 7 个补收，ask-matt 剪枝（初版 #19-#23）全部撤销恢复上游原文。

- **硬依赖闭合 17**（收编件运行时以 Skill tool 互相调用，缺一即断链）：ask-matt、implement、to-spec、to-tickets、handoff、retro、wayfinder、triage、setup-matt-pocock-skills、tdd、code-review、writing-for-agents、grilling、domain-modeling、research、prototype、codebase-design
- **管线咬合可选 3**：grill-with-docs（ask-matt 主流程第一入口）、implement-spec（改动 #14 覆盖）、improve-codebase-architecture（依赖全在闭合内）
- **独立工具 7**（不参与管线咬合，单独使用）：grill-me（无仓库拷问）、diagnosing-bugs（疑难排查，model-invoked）、pr（PR 正文模板，model-invoked）、wizard（人肉步骤向导，model-invoked）、wait-what（没听懂重讲）、teach（跨会话教学）、to-questionnaire（异步问卷）

**model-invoked 说明**（diagnosing-bugs／pr／wizard 三件无 `disable-model-invocation` 键）：AI 在用户项目中匹配到场景会**自动**启用（自动接管 PR 正文风格、自动进排查纪律、自动出人肉步骤向导）。此为全收拍板的知情后果，非缺陷。

## 对上游的改动清单

### 烤入的历史补丁（原 MATT-PATCHES #1-#18，v6.5-v6.8 期间经用户拍板，已直接落在收编件上）

| # | 文件 | 补丁 | 治什么 |
|---|---|---|---|
| 1 | implement/SKILL.md | 开头加「先 claim 票（本地置 claimed／远端 assign 自己）」 | 只查不写 claim→双窗口重复实现同票 |
| 2 | implement/SKILL.md | Commit 句后加「commit message 引票号；经 PR 关票的 tracker 在 PR body 写 Closes #n」 | 跳过 checkpoint 时票零兜底；orient 漂移检查与 code-review spec 轴同时复活 |
| 3 | setup-matt-pocock-skills/SKILL.md | 块更新条款后加「保留不认识的子块（属于其他技能套件）」 | init→setup 顺序下记忆套件子块被静默清除 |
| 4 | setup-matt-pocock-skills/SKILL.md | docs/agents 写入前加「已存在且 tracker 未切换→保留，只补缺失」 | setup 重跑冲掉用户改的 label 映射列 |
| 5 | handoff/SKILL.md | 末尾加「打印绝对路径；有开放票则把路径留票 Comments」 | 便签路径只在创建会话脑中，下个会话找不到 |
| 6 | wayfinder/SKILL.md | research branch push 后加「发现复制一份到默认分支（如 docs/research/）」 | throwaway branch 被 prune→笔记蒸发 |
| 7 | prototype/SKILL.md | 规则 6 加「push 该分支」 | prototype 产物出本机即死 |
| 8 | setup-matt-pocock-skills/issue-tracker-github.md | Conventions 加「Tick acceptance boxes: gh issue edit --body（先取旧 body 只翻勾选）」 | 远端票收尾无勾框命令，退化为只关不勾 |
| 9 | setup-matt-pocock-skills/issue-tracker-gitlab.md | 同上（glab issue update --description） | 同上 |
| 10 | setup-matt-pocock-skills/issue-tracker-local.md | Conventions 加「.scratch/ 纳入版本控制；刻意 ignore 则在此记录备份约定」 | 票+台账随 gitignore/换机丢失 |
| 11 | to-spec/SKILL.md | 开场句后加「无 label 映射（如未装 triage）→按 canonical 字符串」 | 提示重跑 setup 的死循环 |
| 12 | to-tickets/SKILL.md | 同上 | 同上 |
| 13 | retro/SKILL.md | 第 4 步加「用户搁置的候选逐条落票或 repo 笔记文件」 | 复盘候选会话即蒸发 |
| 14 | implement-spec/SKILL.md | 第 7 步加「评审发现先贴 PR/票评论，修复子代理以该评论为 context pointer」 | 发现在对话中，压缩后失真 |
| 15 | code-review/SKILL.md | 聚合后加「问用户是否把发现落 PR/票评论或 docs」 | standalone 评审发现只存在于对话 |
| 16 | ask-matt/SKILL.md | Standalone 节末尾加「记忆套件」条目：/orient 开工定位、/checkpoint 收口沉淀、/memory-audit 记忆体检、/project-init 项目初始化（zcode-devflow-skills 插件；用户问「接下来干嘛/要不要收口/记忆要不要紧」时指向它们） | ask-matt 路由表不含记忆套件，记忆节奏的兜底入口断头 |
| 17 | setup-matt-pocock-skills/issue-tracker-local.md | Conventions 加「本地实现票收口＝验收全勾＋Status: done（可带日期批注，如 done（2026-11-05 收口））；wayfinder 决策票（含 task 型）Status: resolved（见 Wayfinding operations 节）」 | 本地实现票无终态定义（上游 implement 对本地票零收口规定，done 只是项目习惯无出处），新 setup 的仓库天生缺词表 |
| 18 | setup-matt-pocock-skills/SKILL.md | 块保留条款扩为「Preserve any sub-blocks you don't recognize …, as well as any other lines inside the `## Agent skills` block」 | setup 重跑冲掉 project-init 铺的「拍板顺序／入口指针」同级散行→入口指针失效（推翻问句 repo 文档侧断链） |

### v7.0 收编改动

| # | 文件 | 改动 | 为什么 |
|---|---|---|---|
| 19 | ~~ask-matt/SKILL.md 剪枝 5 处~~ | **已撤销**（2026-11-11 用户拍板全收）：ask-matt 恢复上游原文（含 #16），初版 20 收方案中为未收编 7 技能剪的 7 处路由提及全部还原 | 全收后无死链可剪 |
| 20 | commands/（新增 16 个薄壳） | ask-matt、grill-with-docs、triage、improve-codebase-architecture、setup-matt-pocock-skills、to-spec、to-tickets、implement、implement-spec、wayfinder、retro、handoff、grill-me、wait-what、teach、to-questionnaire——用户触发型收编技能的 /命令入口；中文 description 为本插件自撰，正文挂载上游技能 | 收编技能需用户可触发的命令入口；model-invoked 收编件不出命令（自动可达） |
| 21 | 收编件 frontmatter | 保留上游原样（name/description/disable-model-invocation），不补 license/when_to_use | 收编保真优先；AGENTS.md 的 frontmatter 约定只约束自撰技能 |

## 上游同步（手动，可选）

上游出了好修复想跟：到 https://github.com/mattpocock/skills 对比对应文件与收编件，手工搬差异；搬完 grep 抽查本表 #1-#18 是否仍成立。**不同步完全不影响运行。切勿再跑 `npx skills add mattpocock/skills`**——它会把本机旧副本装回来，遮蔽插件版（与「手动 cp 遮蔽插件版」同一道理）。

## 老用户迁移（装过 Matt 技能集的机器）

装 v7.0 插件后，删除本机 `~/.agents/skills/`（及 `~/.zcode/skills/` 符号链接内）**Matt 技能集的全部 27 个目录**（清单即上节「收编范围」）。其余无关目录（oil-ui、钉钉系等）不动。道理：收编件与本地副本逐字节一致，删本地零损失；不删则本地副本永久遮蔽插件版，以后改插件不生效。装完跑一句 `/ask-matt` 冒烟核对即可。
