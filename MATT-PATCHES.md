# Matt 技能本地补丁清单（v6.5，2026-11-05；#16-17 追加 2026-11-06）

本套件与 Matt Pocock 技能集配合使用。以下补丁打在本机 Matt 技能文件上（~/.zcode/skills/ 下的符号链接 → ~/.agents/skills/），**上游 `npx skills add mattpocock/skills` 更新时会冲掉**——更新后按本清单逐条重打。表中「文件」列路径均相对 `~/.agents/skills/`；issue-tracker-*.md 位于 setup-matt-pocock-skills/ 目录内。每条补丁均出自三方咬合评审（全生命周期/初始化矩阵/产物归属），且经用户拍板授权。

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
