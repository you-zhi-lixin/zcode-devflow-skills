---
name: orient
description: 开工定位：读记忆→对照票据与 git 对账→输出 standup 简报（当前阶段/能开工的票/待拍板/建议下一步），并体检记忆小病，病多或疑似孤岛时转介 /memory-audit。
license: MIT
when_to_use: 用户要在既有项目上开工时——新会话续接、隔天再战、换窗口、开场直接派活，或开场问「我们到哪了／接着干」（都先定位再动手）；全新项目和一次性问答不用。
---

# orient（开工定位）

用户要在既有项目上开工——新会话续接、隔天再战、换窗口、开场直接派活。简报第一行向用户复述来意（口语）：「开工前先帮你对了下进度——只看不改；如有小修建议，会先弹窗问你。」

先读 [`../checkpoint/references/memory-discipline.md`](../checkpoint/references/memory-discipline.md)（与本技能同级的 checkpoint 技能目录下；读不到→停下告知用户，尝试从本机其他副本恢复——`~/.agents/skills/` 同套件目录或插件缓存；都没有→告知用户重装本插件，本轮中止）。四层地盘与体检红线以该合同为准。

## 过程

1. **定位记忆**：MEMORY.md 索引通常随会话自动载入（未载入或不确定→先 Read MEMORY.md／`ls` 核对）——索引行仅用于定位：project 型现状条目读全文，其余条目不读全文。
   - **索引空 ≠ 库空**：`ls` 本项目 memory 目录，有 .md 文件而索引无对应行＝索引丢失/损坏→逐文件直读 frontmatter 定位现状条目（口径标「（来自记忆，本轮还没核对）」），转介 /memory-audit 重建索引。
   - memory 根定位不到（子代理场景、或系统提示无 memory 说明时）→ Bash `ls ~/.zcode/cli/memories/projects/` 按**完整工作区名（含哈希段）**匹配；禁止用泛前缀（如 draft），泛前缀会命中其他项目的记忆目录。仍找不到→区分「ls 报错」（记忆根不可达，简报注明）与「ls 为空」（按记忆库为空处理，走第 2、6 步）。
   - **索引行指向的文件不存在（任何类型记忆）＝「索引断链」小病**：该事实按空缺处理，不拿钩子句顶替全文，记入第 7 步清单；先问一句「文件是你本人删的吗」——是→经确认删该索引行了结；否→两条路弹窗：从备份找回文件（优先用户自选备份，次本会话 /handoff 便签所在的 %TEMP% 路径；找回后核对内容与索引口径一致，不一致以文件内容为准并同步索引），或删该索引行。

2. **孤岛扫描（空库也要做；孤岛多产生于搬家/改名/换打开方式）**：
   - 初筛 `grep -il`（只回文件名，不读其他项目记忆内容）；关键词来源：repo 根目录名→票据路径与标题中的专名→AGENTS.md 里的项目名（无 repo 用后两者），排除「中文/记忆/部署」类通用词，**≥2 个不同关键词命中同一目录**才列候选。
   - **先查全局台账 island-checks.md（记忆根下）**：已有结论的目录跳过，不再弹窗。
   - 候选弹窗（多候选可合并一窗）**附命中关键词列表**（词×命中处数，不展示对方内容）；用户确认后才 Read 对方 MEMORY.md 摘要。
   - 确认/排除结论落 island-checks.md（`日期｜目录｜结论`），不落 repo 台账。
   - 目录名不可判读的库（draft-*/纯数字）结论记 island-checks.md「无法排查」态（`日期｜目录｜无法排查（原因）`），不得报「无孤岛」——假阴性会使用户跳过本该做的排查；已记的不再重复弹窗，条件变化（改名/新增可判读线索）后重查。
   **空库先判新旧**：repo 已有记忆套件地图或成套票据，或 git 史 ≥5 笔提交，且 MEMORY.md 与 memory 目录皆空＝疑似 veteran 空库。两种成因库内无法自辨（换机/重装/误删，或 project-init 存量模式铺图未 seed 的首装空库）→先做规定动作：`ls ~/.zcode/cli/memories/projects/` 排查同机旧库（改名/搬家的常见落点）——命中候选→转介 /memory-audit 合并，不走下方路径；未命中→弹窗问「此前在这个项目用过记忆吗」：用过→两条路径（从旧机/备份拷回 memory 目录 `~/.zcode/cli/memories/projects/<项目目录>/memory/`（拷回后先按第 4 步做一次轻体检确认索引↔文件一致，再出简报）；或明示放弃重建——放弃前二次确认，提示回收站/OneDrive 版本历史或可救，并如实告知损失：user/feedback 型记忆 repo 无处可捞，重建只能回收 repo 侧约定）；没用过（首装存量）→走第 6 步口径起步，并说明首条记忆来自首次 /checkpoint；放弃重建→也走第 6 步口径起步。真新项目→走第 6 步。

3. **对账**：将记忆与仓库现状对照——票据状态（含票面 Comments：agent-brief、handoff 便签路径一并取用）、spec/计划文档（含远端 spec 票正文）、`docs/research/` 笔记（存在则读；wayfinder research 落默认分支的产物）、CODING_STANDARDS.md 与交付存档（docs/archive.md 等记忆指针指向物，存在则纳入）、`git log --oneline -15`；repo 有 GLOSSARY.md、docs/adr/、`.out-of-scope/` 存在则一并纳入，GLOSSARY-MAP.md 存在＝multi-context 仓库（各 context 的 GLOSSARY 与 `src/<context>/docs/adr/` 一并纳入）。tracker 文档 PRs-as-request-surface 旗标开启时，ready-for-agent 的外部 PR 一并列入「现在能开工的票」呈现（处置归 /triage）。先识别票种：
   - `.scratch/<目录>/` 内含 `map.md`→按 wayfinder 词表（open/claimed/resolved，无 Status 行＝open，`Type:` 行注明票种——research/prototype/grilling/task 四种，大小写不敏感、值带批注以前缀为准，task 型与决策票同口径收尾；map.md 是整组开关，组内混实现票时向用户报告，收口各归词表：实现票 done、决策/task 票 resolved，不混用；map 本体上游无关闭动作，整组 resolved 即视为地图走完，简报注明即可）。
   - `.scratch/<feature>/spec.md`（to-spec 产物：无验收框，可能带 Status）＝spec 文档：不进「能开工的票」，只作对账源（本地票据模板无 Parent 区，spec 父票判据只适用远端）。
   - 远端票 labels 含 `wayfinder:` 前缀→同按决策票口径（open↔未认领、claimed↔有 assignee、resolved↔closed，`wayfinder:map` 为地图入口）。
   - 其余按 `docs/agents/issue-tracker.md` 词表（本地＝Status 行＋验收勾选；远端＝state＋labels＋assignee）。
   - 该词表读不到、或其中没有终态约定→按本文内嵌最小词表判定，简报注明口径来源：
     - 本地＝Status 行＋验收勾选，终态 done（值以 done 开头即终态，容忍日期批注；wontfix 细则见合同「票据终态约定」）
     - wayfinder 决策/task 票＝resolved（值以 resolved 开头即终态，容忍日期批注）
     - `docs/agents/triage-labels.md` 也读不到→ready-for-agent 按字面匹配；无任何状态词表时，非终态（值不以 done/resolved 开头）且未认领（Status 值不以 claimed 开头）的本地票列为候选
   - 票面与记忆一致、但与 git/工作树矛盾，也算对账发现。

4. **轻体检**：按合同「体检红线」扫行级小病——索引行超 150 字符（按字符数）、断言缺日期锚、description 或索引钩子句与正文脱节（缺正文的关键限定＝脱节；措辞风格差异不算）、索引行残缺到解析不出文件名（格式病：先问该行本意，问不出→转介 /memory-audit 重建索引，见合同「拍板弹窗」节）、**索引↔文件双向核对**（每条索引行验证文件存在；文件无索引行＝孤儿，转介 /memory-audit 补行）。空库报「记忆库不存在」，不报「0 病」。≤3 条→列清单走第 7 步；现状条目超 10KB、混入进度细节/✅、内部矛盾、孤岛待合并、索引条目 ≥30（预警，瘦身是重写级手术非当场小修）→只报告不动手，转介 /memory-audit。转介项与「记忆落后」横幅触发各追加台账一行`病`（`日期｜病｜对象＋一句话`）——升级告警的计数输入；孤岛候选不落本台账（归 island-checks.md）。

5. **输出 standup 简报**（五段标题固定）：
   - **当前阶段**：一两句，带日期锚与证据；来自记忆未经核验的口径标「（来自记忆，本轮还没核对）」
   - **现在能开工的票**：
     - 决策票可开工＝open＋无 blocker＋无人认领；建议下一步给 `/wayfinder`（票号｜标题｜Question 摘要）。
     - 实现票可开工＝以下条件全部满足：
       - 状态 ready-for-agent（按 repo 的 `docs/agents/triage-labels.md` 映射列）＋blocker 闭环
       - 无人认领：本地 Status 值不以 claimed 开头（容忍日期批注）且无 Assignee/Claimed by 字段／远端无 assignee
       - git 无完成迹象：log 无票号的**词边界**匹配、无触及该票涉及路径的提交；**票据文件自身路径豁免**——scaffold commit 含票据不算
       - 验收框未全勾（**全勾＋非终态＝票内漂移**）
       - **非 spec 父票**：无验收框且被其他票以 Parent/sub-issue 引用＝spec 父票→列「待拆票」，建议 /to-tickets
     - 漂移（git 迹象或票内矛盾）不进队列，列入对账发现，经用户拍板后按 tracker 词表补置终态。
     - needs-info／needs-triage／ready-for-human／wontfix 不可开工，另列原因（优先引票面原文）；五档与终态之外的自创状态（如 code-complete、in-observation）同样不进队列、另列并注明词表外。ready-for-human 票有已交付迹象（git/简报证据）→列入对账发现经拍板处置，选项同 checkpoint 收尾（置 done／退回重 triage／搁置）。
     - 实现票每张一行「票号｜标题｜验收要点」。
   - **等你拍板的事**：🟡 记忆挂账（台账`挂账`行逐条重提，已划账的不再提）＋票正文开放问题，重复的合并
   - **建议下一步**：具体到命令——决策票 `/wayfinder`；实现票 `/implement .scratch/<功能>/issues/NN-<slug>.md`（远端票写 `/implement <票号或URL>`）；无票项目给基于挂账或最近 commit 的动作；不确定走哪条→问 ask-matt
   - **记忆健康**：一行（元素多时折 ≤3 行短列表）——轻病 N 条／转介与否／孤岛结论。
     - 现状条目最新日期锚早于最近 5 笔 commit（同日的再比记忆文件更新时间，零变更收口后以台账最新收口行为准；空库不适用）→简报顶部横幅「记忆落后，请跑 /checkpoint」＋可复制命令（台账最新一行若为`病：平台写入异常`→横幅改为「记忆写入通道异常，待恢复后重跑 /checkpoint」，不催写）。
     - 同一病×同一对象连续 ≥2 次未清→升级告警。
     - 距上次清账的收口行满 2-3（票或轮）→建议 /memory-audit。
     - 项目无「记忆套件」地图→提示补跑 /project-init（存量模式）。

6. **全新项目分支**：真新项目（repo 也新）→简报从票据与 git 重建（仍按五段输出，缺来源的段注明），建议收尾 /checkpoint 建库；连票据都没有→建议 /project-init。重建先回收 repo 已沉淀而记忆缺的约定（AGENTS.md 拍板顺序与入口指针、spec 里的拍板）——repo 有的直接引用，征询只留 repo 与记忆都查不到的项。

7. **小修**：修复清单一批弹窗确认（推荐项放第一）→拍板后当场改记忆文件与索引（MEMORY.md 只做单行编辑）；涉及改名的，同批 grep 旧名修复库内指向旧名的 [[双链]]。
   完成＝清单每条要么已执行、要么挂起留账（用户明说，或未获应答按合同「拍板弹窗」节兜底）。

## 边界

只动记忆目录的行级小病，外加台账 `.scratch/memory-health.md` 的追加（无关联 repo 的会话落当前工作目录 `.scratch/`，并在简报注明落点）；孤岛裁决另落记忆根全局台账 island-checks.md。重写级手术与孤岛合并归 /memory-audit；repo 文档与票据治理归 /retro；票状态回写经用户拍板后按 `docs/agents/issue-tracker.md` 词表执行，未经拍板不动票。
