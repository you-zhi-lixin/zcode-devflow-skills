# Matt 技能收编出处与改动清单（v7.0，2026-11-11）

本插件自 v7.0 起，将 Matt Pocock 技能集的子集**收编进仓库**（`skills/` 下 20 个目录随插件分发），不再要求用户本机安装 `~/.agents/skills/`。收编意味着：**上游更新不再自动到达**，同步上游改为手动可选动作（见文末）；下列改动直接落在收编件上，不存在「补丁被上游更新冲掉」的问题。

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

## 收编范围（20）

**硬依赖闭合 17**（收编件运行时以 Skill tool 互相调用，缺一即断链）：
ask-matt、implement、to-spec、to-tickets、handoff、retro、wayfinder、triage、setup-matt-pocock-skills、tdd、code-review、writing-for-agents、grilling、domain-modeling、research、prototype、codebase-design

**咬合可选 3**：
grill-with-docs（ask-matt 主流程第一入口）、implement-spec（改动 #14 覆盖）、improve-codebase-architecture（用户手动触发；其依赖 grilling/domain-modeling/codebase-design 均在闭合内）

**未收编 7**：grill-me、diagnosing-bugs、pr、wizard、wait-what、teach、to-questionnaire——经引用追踪核实：仅被 ask-matt 路由提及，无任何运行时调用者；且其中 pr／wizard／diagnosing-bugs 为 model-invoked（收编后会自动介入用户项目，如自动接管 PR 正文风格），超出本插件咬合面。ask-matt 路由表中对应条目已剪（#19-#23）。

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

### v7.0 收编新增改动（#19-#25）

| # | 文件 | 改动 | 为什么 |
|---|---|---|---|
| 19 | ask-matt/SKILL.md | 主流程步骤 1 括注改为「stateless no-repo 变体 /grill-me 未随本插件收编」 | grill-me 未收编，路由提及成死链 |
| 20 | ask-matt/SKILL.md | On-ramps「Something's broken」条目去掉 /diagnosing-bugs 指向，改为「直接排查，修完跑 /retro；缺好接缝找 /improve-codebase-architecture」 | diagnosing-bugs 未收编；保留条目尾部仍有效的指向 |
| 21 | ask-matt/SKILL.md | 删主流程步骤 3 的 /pr 整段 | pr 未收编（model-invoked，收编即自动接管用户 PR 风格） |
| 22 | ask-matt/SKILL.md | Standalone 删 /grill-me、/to-questionnaire、/wizard、/wait-what、/teach 五条目 | 未收编 |
| 23 | ask-matt/SKILL.md | grilling 条目「`/grill-me` and `/grill-with-docs` are the two named ways in」改「`/grill-with-docs` is the named way in」 | 同 #19 |
| 24 | commands/（新增 12 个薄壳） | ask-matt、grill-with-docs、triage、improve-codebase-architecture、setup-matt-pocock-skills、to-spec、to-tickets、implement、implement-spec、wayfinder、retro、handoff——用户触发型收编技能的 /命令入口；中文 description 为本插件自撰，正文挂载上游技能 | 收编技能需用户可触发的命令入口；model-invoked 收编件不出命令（自动可达） |
| 25 | 收编件 frontmatter | 保留上游原样（name/description/disable-model-invocation），不补 license/when_to_use | 收编保真优先；AGENTS.md 的 frontmatter 约定只约束自撰技能 |

## 上游同步（手动，可选）

上游出了好修复想跟：到 https://github.com/mattpocock/skills 对比对应文件与收编件，手工搬差异；搬完对照本清单过一遍 #19-#23 剪枝区是否仍成立。**不同步完全不影响运行。切勿再跑 `npx skills add mattpocock/skills`**——它会把本机旧副本装回来，遮蔽插件版（与「手动 cp 遮蔽插件版」同一道理）。

## 老用户迁移（装过 Matt 技能集的机器）

装 v7.0 插件后，删除本机 `~/.agents/skills/`（及 `~/.zcode/skills/` 符号链接内）**恰好这 20 个已收编目录**：ask-matt、implement、to-spec、to-tickets、handoff、retro、wayfinder、triage、setup-matt-pocock-skills、tdd、code-review、writing-for-agents、grilling、domain-modeling、research、prototype、codebase-design、grill-with-docs、implement-spec、improve-codebase-architecture。**未收编的 7 个（grill-me、diagnosing-bugs、pr、wizard、wait-what、teach、to-questionnaire）保留在本地**，继续可用；其余无关目录（oil-ui、钉钉系等）不动。删 20 留 7 的道理：已收编的留在本地会遮蔽插件版（改插件不生效）；未收编的本地留着正好补位。
