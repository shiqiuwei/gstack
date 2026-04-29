# gstack

English | [中文](README.zh-CN.md)

> "我觉得自从去年十二月以来，我基本上没有亲手敲过一行代码——这是一个极大的改变。" — [Andrej Karpathy](https://fortune.com/2026/03/21/andrej-karpathy-openai-cofounder-ai-agents-coding-state-of-psychosis-openclaw/)，No Priors 播客，2026 年 3 月

听到 Karpathy 这番话，我想搞清楚他是怎么做到的。一个人怎么能以一支二十人团队的速度交付产品？Peter Steinberger 凭借 AI 助手几乎独自一人搭建了 [OpenClaw](https://github.com/openclaw/openclaw)——247K GitHub Stars。革命已然到来。单个开发者，配上合适的工具，可以比传统团队跑得更快。

我是 [Garry Tan](https://x.com/garrytan)，[Y Combinator](https://www.ycombinator.com/) 总裁兼 CEO。我和数千家初创公司合作过——Coinbase、Instacart、Rippling——当时他们还只是两个人在车库里打拼。在 YC 之前，我是 Palantir 最早的工程/产品/设计师之一，联合创立了 Posterous（后被 Twitter 收购），并搭建了 Bookface，YC 内部社交网络。

**gstack 是我的答案。** 我做产品已经二十年，而现在我交付的产品比以往任何时候都多。过去 60 天里：3 个生产服务，40+ 个已发布的功能，兼职完成，同时全职运营 YC。从逻辑代码变更来看——而非 AI 会虚增的原始代码行数——我 2026 年的年化效率是 **2013 年的约 810 倍**（每天 11,417 对比 14 逻辑行）。截至 2026 年 4 月 18 日，2026 年迄今产出量已达 **2013 全年的 240 倍**。统计范围覆盖 40 个公开及私有的 `garrytan/*` 仓库（含 Bookface），已排除一个演示仓库。大部分代码由 AI 编写——重要的不是谁敲了键盘，而是交付了什么。

> 批评代码行数指标的人指出 AI 会让原始行数虚增，他们没有错。但他们错在：以通胀校正后的方式衡量，我的生产力并没有下降，而是大幅提升。完整方法论、注意事项及复现脚本请见：**[关于代码行数争议](docs/ON_THE_LOC_CONTROVERSY.md)**。

**2026 年——1,237 次贡献，还在持续增加：**

![GitHub contributions 2026 — 1,237 contributions, massive acceleration in Jan-Mar](docs/images/github-2026.png)

**2013 年——我在 YC 搭建 Bookface 时（772 次贡献）：**

![GitHub contributions 2013 — 772 contributions building Bookface at YC](docs/images/github-2013.png)

同一个人，不同的时代。区别在于工具。

**gstack 就是我的做法。** 它把 Claude Code 变成了一支虚拟工程团队——一位重新审视产品的 CEO、一位锁定架构的工程经理、一位发现 AI 低质代码的设计师、一位找出生产 Bug 的审查者、一位真正打开浏览器的 QA 负责人、一位运行 OWASP + STRIDE 审计的安全官，以及一位负责提交 PR 的发布工程师。二十三个专家角色和八个强力工具，全部是斜杠命令，全部用 Markdown 编写，全部免费，MIT 许可证。

这是我的开源软件工厂。我每天都在用。我把它分享出来，因为这些工具应该向所有人开放。

Fork 它、改进它、让它成为你自己的工具。如果你想喷一个免费开源项目，你当然可以——但我更希望你先试试。

**适用人群：**
- **创始人和 CEO**——尤其是仍然想亲自交付产品的技术型创始人
- **初次使用 Claude Code 的用户**——有了结构化角色，不再面对空白提示词
- **技术负责人和高级工程师**——在每个 PR 上实现严格的审查、QA 和发布自动化

## 快速开始

1. 安装 gstack（30 秒——见下文）
2. 运行 `/office-hours`——描述你正在构建的产品
3. 对任意功能想法运行 `/plan-ceo-review`
4. 对有变更的分支运行 `/review`
5. 对你的预发布 URL 运行 `/qa`
6. 到此为止——你自然会知道这是不是适合你的工具。

## 安装——30 秒

**前置要求：** [Claude Code](https://docs.anthropic.com/en/docs/claude-code)、[Git](https://git-scm.com/)、[Bun](https://bun.sh/) v1.0+、[Node.js](https://nodejs.org/)（仅 Windows）

### 第一步：在你的机器上安装

打开 Claude Code，粘贴以下内容。Claude 会完成剩余工作。

> Install gstack: run **`git clone --single-branch --depth 1 https://github.com/garrytan/gstack.git ~/.claude/skills/gstack && cd ~/.claude/skills/gstack && ./setup`** then add a "gstack" section to CLAUDE.md that says to use the /browse skill from gstack for all web browsing, never use mcp\_\_claude-in-chrome\_\_\* tools, and lists the available skills: /office-hours, /plan-ceo-review, /plan-eng-review, /plan-design-review, /design-consultation, /design-shotgun, /design-html, /review, /ship, /land-and-deploy, /canary, /benchmark, /browse, /connect-chrome, /qa, /qa-only, /design-review, /setup-browser-cookies, /setup-deploy, /setup-gbrain, /retro, /investigate, /document-release, /codex, /cso, /autoplan, /plan-devex-review, /devex-review, /careful, /freeze, /guard, /unfreeze, /gstack-upgrade, /learn. Then ask the user if they also want to add gstack to the current project so teammates get it.

### 第二步：团队模式——共享仓库自动更新（推荐）

在你的仓库内粘贴以下内容。切换到团队模式，初始化仓库让队友自动获取 gstack，并提交变更：

```bash
(cd ~/.claude/skills/gstack && ./setup --team) && ~/.claude/skills/gstack/bin/gstack-team-init required && git add .claude/ CLAUDE.md && git commit -m "require gstack for AI-assisted work"
```

仓库中无需内嵌文件，无版本漂移，无需手动升级。每次 Claude Code 会话启动时自动检查更新（每小时限频一次，网络故障安全，完全静默）。

将 `required` 替换为 `optional`，可改为提示队友而非强制要求。

### OpenClaw

OpenClaw 通过 ACP 生成 Claude Code 会话，因此当 Claude Code 安装了 gstack 后，每个 gstack 技能都可以直接使用。将以下内容粘贴给你的 OpenClaw 代理：

> Install gstack: run `git clone --single-branch --depth 1 https://github.com/garrytan/gstack.git ~/.claude/skills/gstack && cd ~/.claude/skills/gstack && ./setup` to install gstack for Claude Code. Then add a "Coding Tasks" section to AGENTS.md that says: when spawning Claude Code sessions for coding work, tell the session to use gstack skills. Include these examples — security audit: "Load gstack. Run /cso", code review: "Load gstack. Run /review", QA test a URL: "Load gstack. Run /qa https://...", build a feature end-to-end: "Load gstack. Run /autoplan, implement the plan, then run /ship", plan before building: "Load gstack. Run /office-hours then /autoplan. Save the plan, don't implement."

**设置完成后，直接和你的 OpenClaw 代理自然交流：**

| 你说 | 发生什么 |
|------|---------|
| "修复 README 里的错别字" | 简单任务——Claude Code 会话，无需 gstack |
| "对这个仓库做一次安全审计" | 生成 Claude Code 会话，执行 `Run /cso` |
| "帮我做一个通知功能" | 生成 Claude Code 会话，/autoplan → 实现 → /ship |
| "帮我规划 v2 API 重设计" | 生成 Claude Code 会话，/office-hours → /autoplan，保存计划 |

高级调度路由和 gstack-lite/gstack-full 提示模板请见 [docs/OPENCLAW.md](docs/OPENCLAW.md)。

### 原生 OpenClaw 技能（通过 ClawHub）

四个可直接在 OpenClaw 代理中运行的方法论技能，无需 Claude Code 会话。从 ClawHub 安装：

```
clawhub install gstack-openclaw-office-hours gstack-openclaw-ceo-review gstack-openclaw-investigate gstack-openclaw-retro
```

| 技能 | 功能 |
|------|------|
| `gstack-openclaw-office-hours` | 包含 6 个强制性问题的产品质询 |
| `gstack-openclaw-ceo-review` | 包含 4 种范围模式的战略挑战 |
| `gstack-openclaw-investigate` | 根本原因调试方法论 |
| `gstack-openclaw-retro` | 每周工程回顾 |

这些是对话式技能，你的 OpenClaw 代理通过聊天直接运行它们。

### 其他 AI 代理

gstack 支持 10 种 AI 编码代理，不只是 Claude。安装程序自动检测你安装了哪些代理：

```bash
git clone --single-branch --depth 1 https://github.com/garrytan/gstack.git ~/gstack
cd ~/gstack && ./setup
```

或使用 `./setup --host <name>` 指定特定代理：

| 代理 | 参数 | 技能安装位置 |
|------|------|------------|
| OpenAI Codex CLI | `--host codex` | `~/.codex/skills/gstack-*/` |
| OpenCode | `--host opencode` | `~/.config/opencode/skills/gstack-*/` |
| Cursor | `--host cursor` | `~/.cursor/skills/gstack-*/` |
| Factory Droid | `--host factory` | `~/.factory/skills/gstack-*/` |
| Slate | `--host slate` | `~/.slate/skills/gstack-*/` |
| Kiro | `--host kiro` | `~/.kiro/skills/gstack-*/` |
| Hermes | `--host hermes` | `~/.hermes/skills/gstack-*/` |
| GBrain（mod） | `--host gbrain` | `~/.gbrain/skills/gstack-*/` |

**想添加对其他代理的支持？** 请见 [docs/ADDING_A_HOST.md](docs/ADDING_A_HOST.md)。只需一个 TypeScript 配置文件，零代码改动。

## 实战演示

```
你:     我想做一个日历每日简报应用。
你:     /office-hours
Claude: [询问痛点——具体例子，不是假设]

你:     多个 Google 日历，事件信息过时，地点错误。
        准备工作耗时太长，结果也不够好……

Claude: 我要挑战你的框架。你说的是"每日简报应用"。
        但你实际描述的是一个个人 AI 参谋。
        [提炼出 5 项你没意识到自己在描述的能力]
        [质疑 4 个前提——你认同、反对或调整]
        [生成 3 个实现方案及工作量估算]
        建议：明天就交付最小楔形，从真实使用中学习。
        完整愿景是 3 个月的项目——先从真正管用的每日简报开始。
        [撰写设计文档 → 自动输入到下游技能]

你:     /plan-ceo-review
        [读取设计文档，挑战范围，执行 10 节审查]

你:     /plan-eng-review
        [数据流、状态机、错误路径的 ASCII 图]
        [测试矩阵、故障模式、安全顾虑]

你:     批准计划，退出计划模式。
        [写了 11 个文件，共 2,400 行。约 8 分钟。]

你:     /review
        [自动修复] 2 个问题。[待确认] 竞态条件 → 你批准修复。

你:     /qa https://staging.myapp.com
        [打开真实浏览器，点击流程，发现并修复一个 Bug]

你:     /ship
        测试：42 → 51（+9 个新测试）。PR: github.com/you/app/pull/42
```

你说"每日简报应用"，代理说"你在构建一个 AI 参谋"——因为它倾听的是你的痛苦，而不是你的功能需求。八条命令，端到端完成。这不是副驾驶，这是一支团队。

## 冲刺流程

gstack 是一套流程，不是工具集合。技能按照冲刺的顺序运行：

**思考 → 规划 → 构建 → 审查 → 测试 → 交付 → 复盘**

每个技能为下一个提供输入。`/office-hours` 撰写设计文档，`/plan-ceo-review` 读取它。`/plan-eng-review` 撰写测试计划，`/qa` 接手执行。`/review` 发现的 Bug，`/ship` 验证已修复。没有任何环节会被遗漏，因为每一步都了解前一步做了什么。

| 技能 | 你的专家 | 职责 |
|------|---------|------|
| `/office-hours` | **YC 办公时间** | 从这里开始。六个强制性问题，在写代码之前重构你的产品。质疑你的框架，挑战前提，生成实现替代方案。设计文档自动输入到所有下游技能。 |
| `/plan-ceo-review` | **CEO / 创始人** | 重新思考问题。找到需求背后隐藏的 10 星产品。四种模式：扩展、选择性扩展、保持范围、缩减。 |
| `/plan-eng-review` | **工程经理** | 锁定架构、数据流、图表、边界情况和测试。将隐藏假设暴露出来。 |
| `/plan-design-review` | **高级设计师** | 对每个设计维度评 0-10 分，解释 10 分是什么样子，然后编辑计划以达到目标。AI 低质设计检测。交互式——每个设计决策对应一个 AskUserQuestion。 |
| `/plan-devex-review` | **开发者体验负责人** | 交互式 DX 审查：探索开发者画像，对标竞争对手的 TTHW，设计神奇时刻，逐步追踪摩擦点。三种模式：DX 扩展、DX 打磨、DX 分级。20-45 个强制性问题。 |
| `/design-consultation` | **设计伙伴** | 从零开始构建完整设计系统。研究行业现状，提出创意风险，生成真实产品原型。 |
| `/review` | **Staff 工程师** | 找出通过 CI 但会在生产环境崩溃的 Bug。自动修复显而易见的问题。标记完整性缺口。 |
| `/investigate` | **调试专家** | 系统性根本原因调试。铁律：没有调查就没有修复。追踪数据流，测试假设，三次修复失败后停止。 |
| `/design-review` | **会写代码的设计师** | 与 /plan-design-review 相同的审计，然后修复发现的问题。原子提交，修改前后截图对比。 |
| `/devex-review` | **DX 测试员** | 实时开发者体验审计。实际测试你的入门流程：浏览文档，尝试入门流程，计时 TTHW，截图错误。与 `/plan-devex-review` 分数对比——展示计划与现实是否相符的回旋镖。 |
| `/design-shotgun` | **设计探索者** | "给我看看选项。" 生成 4-6 个 AI 原型变体，在浏览器中并排打开对比板，收集你的反馈，然后迭代。品味记忆会随着几轮迭代后开始偏向你真正喜欢的风格。不再需要用文字描述你的愿景然后希望 AI 能理解——你看到选项，挑出好的，视觉迭代。 |
| `/design-html` | **设计工程师** | 将原型转化为真正可用的生产 HTML。使用 Pretext 进行计算文本布局：文本自动换行，高度随内容调整，布局是动态的。30KB 开销，零依赖。检测你的框架（React、Svelte、Vue）并输出正确格式。根据设计类型（落地页、仪表盘、表单、卡片布局）智能路由 API。输出是可以真正交付的，不是演示。 |
| `/qa` | **QA 负责人** | 测试你的应用，发现 Bug，用原子提交修复，再验证。为每个修复自动生成回归测试。 |
| `/qa-only` | **QA 报告员** | 与 /qa 相同的方法论，但只生成报告。纯 Bug 报告，不改代码。 |
| `/pair-agent` | **多代理协调员** | 与任意 AI 代理共享浏览器。一条命令，一次粘贴，即可连接。支持 OpenClaw、Hermes、Codex、Cursor 或任何能 curl 的工具。每个代理有自己的标签页。自动启动有头模式供你观察。自动启动 ngrok 隧道供远程代理使用。作用域 Token、标签页隔离、限速、域名限制和活动归因。 |
| `/cso` | **首席安全官** | OWASP Top 10 + STRIDE 威胁模型。零噪声：17 项误报排除，8/10+ 置信度门槛，独立发现验证。每个发现都包含具体的漏洞利用场景。 |
| `/ship` | **发布工程师** | 同步主干，运行测试，审计覆盖率，推送，开启 PR。如果项目没有测试框架会从零引导搭建。 |
| `/land-and-deploy` | **发布工程师** | 合并 PR，等待 CI 和部署，验证生产健康状态。一条命令，从"已批准"到"生产验证完毕"。 |
| `/canary` | **SRE** | 部署后监控循环。监视控制台错误、性能退化和页面故障。 |
| `/benchmark` | **性能工程师** | 基准页面加载时间、核心 Web 指标和资源大小。每个 PR 的前后对比。 |
| `/document-release` | **技术写作者** | 更新所有项目文档以匹配你刚交付的内容。自动发现过时的 README。 |
| `/retro` | **工程经理** | 团队感知的每周回顾。按人分解，交付连续性，测试健康趋势，成长机会。`/retro global` 跨所有项目和 AI 工具（Claude Code、Codex、Gemini）运行。 |
| `/browse` | **QA 工程师** | 给代理一双眼睛。真实 Chromium 浏览器，真实点击，真实截图。每条命令约 100ms。`/open-gstack-browser` 启动带侧边栏、反爬虫隐身和自动模型路由的 GStack 浏览器。 |
| `/setup-browser-cookies` | **会话管理员** | 从你的真实浏览器（Chrome、Arc、Brave、Edge）导入 Cookie 到无头会话。测试需要认证的页面。 |
| `/autoplan` | **审查流水线** | 一条命令，全面审查的计划。自动运行 CEO → 设计 → 工程审查，并编码决策原则。只将品味决策呈现给你审批。 |
| `/learn` | **记忆** | 管理 gstack 跨会话学到的内容。审查、搜索、精简和导出项目特定的模式、陷阱和偏好。学习内容跨会话积累，使 gstack 在你的代码库上越来越智能。 |

### 应该用哪种审查？

| 构建目标... | 计划阶段（写代码前） | 实时审计（交付后） |
|-------------|---------------------|-------------------|
| **终端用户**（UI、Web 应用、移动端） | `/plan-design-review` | `/design-review` |
| **开发者**（API、CLI、SDK、文档） | `/plan-devex-review` | `/devex-review` |
| **架构**（数据流、性能、测试） | `/plan-eng-review` | `/review` |
| **以上全部** | `/autoplan`（运行 CEO → 设计 → 工程 → DX，自动检测适用项） | — |

### 强力工具

| 技能 | 功能 |
|------|------|
| `/codex` | **第二意见** — 来自 OpenAI Codex CLI 的独立代码审查。三种模式：审查（通过/失败门槛）、对抗性挑战和开放咨询。当 `/review`（Claude）和 `/codex`（OpenAI）都审查了同一分支时，提供跨模型分析。 |
| `/careful` | **安全护栏** — 在执行破坏性命令（rm -rf、DROP TABLE、force-push）前发出警告。说"be careful"即可激活。可覆盖任何警告。 |
| `/freeze` | **编辑锁定** — 将文件编辑限制在一个目录。调试时防止意外更改范围外的代码。 |
| `/guard` | **完全安全** — 一条命令激活 `/careful` + `/freeze`。生产工作的最高安全保障。 |
| `/unfreeze` | **解锁** — 移除 `/freeze` 边界。 |
| `/open-gstack-browser` | **GStack 浏览器** — 启动带侧边栏、反爬虫隐身、自动模型路由（Sonnet 处理操作，Opus 处理分析）、一键 Cookie 导入和 Claude Code 集成的 GStack 浏览器。清理页面，智能截图，编辑 CSS，将信息传回你的终端。 |
| `/setup-deploy` | **部署配置器** — `/land-and-deploy` 的一次性设置。检测你的平台、生产 URL 和部署命令。 |
| `/setup-gbrain` | **GBrain 入门** — 从零到运行 gbrain，不到 5 分钟。PGLite 本地、Supabase 现有 URL，或通过 Management API 自动配置新 Supabase 项目。为 Claude Code + 每仓库信任三元组（读写/只读/拒绝）注册 MCP。[完整指南](USING_GBRAIN_WITH_GSTACK.md)。 |
| `/gstack-upgrade` | **自动升级** — 将 gstack 升级到最新版。检测全局安装与内嵌安装，同步两者，显示变更内容。 |

### 新命令行工具（v0.19）

除斜杠命令技能外，gstack 还提供独立 CLI，用于不适合在会话内运行的工作流：

| 命令 | 功能 |
|------|------|
| `gstack-model-benchmark` | **跨模型基准测试** — 用同一提示词跑 Claude、GPT（通过 Codex CLI）和 Gemini；对比延迟、Token 数量、成本和（可选）LLM 判断质量分数。每个提供商独立检测认证，不可用的提供商自动跳过。以表格、JSON 或 Markdown 输出。`--dry-run` 在不消耗 API 调用的情况下验证参数和认证。 |
| `gstack-taste-update` | **设计品味学习** — 将 `/design-shotgun` 中的批准和拒绝写入持久化的每项目品味档案。每周衰减 5%。反馈到未来的变体生成，使系统学习你真正喜欢什么。 |

### 持续检查点模式（可选，默认本地）

设置 `gstack-config set checkpoint_mode continuous`，技能会在进行中用 `WIP:` 前缀加结构化的 `[gstack-context]` 正文（决策、剩余工作、失败方法）自动提交你的工作。能够在崩溃和上下文切换后继续。`/context-restore` 读取这些提交重建会话状态。`/ship` 在 PR 前过滤并压缩 WIP 提交（保留非 WIP 提交），保持 bisect 的清洁性。推送是可选的（通过 `checkpoint_push=true`）——默认只在本地，不会在每次 WIP 提交时触发 CI。

### 域技能 + 原始 CDP 逃生通道

两个新的浏览器原语可随时间积累强化 gstack 代理：

- **`$B domain-skill save`** — 代理保存每站点笔记（例如，"LinkedIn 的申请按钮在 iframe 里"），下次访问该主机名时自动触发。隔离 → 3 次成功使用后激活 → 通过 `$B domain-skill promote-to-global` 可选地跨项目推广。存储位置与 `/learn` 的每项目学习文件并列。完整参考：**[docs/domain-skills.md](docs/domain-skills.md)**。
- **`$B cdp <Domain.method>`** — 原始 Chrome DevTools 协议逃生通道，用于整理好的命令偶尔遗漏的情况。默认拒绝：方法必须在 `browse/src/cdp-allowlist.ts` 中以一行理由明确添加。双层互斥将浏览器范围的 CDP 调用与每标签页工作串行化。数据导出方法的输出包裹在 UNTRUSTED 信封中。

> 想要无护栏、无白名单、无守护进程的原始 CDP——只是代理到 Chrome 的薄传输层？[browser-use/browser-harness-js](https://github.com/browser-use/browser-harness-js) 是另一种理念（代理编写的辅助程序 vs gstack 的精选命令），如果你不需要 gstack 的安全栈，它是个好选择。两者可以共存：gstack 的 `$B cdp` 和 harness 都可以通过 Playwright 的 `newCDPSession` 附加到同一个 Chrome。

**[每个技能的深度解析，含示例和理念 →](docs/skills.md)**

### Karpathy 的四种故障模式？已全部覆盖。

Andrej Karpathy 的 [AI 编码规则](https://github.com/forrestchang/andrej-karpathy-skills)（17K Stars）精准指出了四种故障模式：错误假设、过度复杂、正交编辑、命令式而非声明式。gstack 的工作流技能全部对此进行了约束。`/office-hours` 在写代码之前就把假设逼出来。困惑协议阻止 Claude 在架构决策上猜测。`/review` 捕捉不必要的复杂性和顺带的改动。`/ship` 将任务转化为可验证的目标，配合测试优先执行。如果你已经在用 Karpathy 风格的 CLAUDE.md 规则，gstack 是让这些规则在整个冲刺中生效的工作流执行层，而不只是单条提示词。

## 并行冲刺

gstack 在单个冲刺中很强大，同时运行十个时更令人着迷。

**设计是核心。** `/design-consultation` 从零构建你的设计系统，研究行业现状，提出创意风险，撰写 `DESIGN.md`。但真正的魔力在于猎枪到 HTML 的流水线。

**`/design-shotgun` 是你探索的方式。** 描述你想要什么，它用 GPT Image 生成 4-6 个 AI 原型变体，然后在浏览器中并排打开对比板。你挑选最喜欢的，留下反馈（"更多空白"、"更粗的标题"、"去掉渐变"），它生成新一轮。重复直到你满意。几轮之后，品味记忆开始偏向你真正喜欢的选项。不再需要用文字描述你的愿景然后希望 AI 能理解——你看到选项，挑出好的，视觉迭代。

**`/design-html` 让它成真。** 拿那个批准的原型（来自 `/design-shotgun`、CEO 计划、设计审查，或者只是一段描述），把它变成生产质量的 HTML/CSS。不是那种在一个视口宽度下看起来不错、在其他地方全坏掉的 AI HTML。这使用 Pretext 进行计算文本布局：文本在调整大小时真正换行，高度随内容调整，布局是动态的。30KB 开销，零依赖。它检测你的框架（React、Svelte、Vue）并输出正确格式。根据设计类型（落地页、仪表盘、表单或卡片布局）智能路由 API。输出是你真正会交付的，不是演示。

**`/qa` 是一个巨大的解锁。** 它让我从 6 个并行工作者增加到 12 个。Claude Code 说 *"我看到问题了"* 然后真正地修复它，生成回归测试，并验证修复——这改变了我的工作方式。代理现在有了眼睛。

**智能审查路由。** 就像一家运营良好的初创公司：CEO 不必看基础设施 Bug 修复，后端变更不需要设计审查。gstack 追踪已运行的审查，判断什么是合适的，然后做正确的事情。审查准备仪表板在你交付前告诉你当前状态。

**测试一切。** `/ship` 如果你的项目没有测试框架，会从零搭建一个。每次 `/ship` 运行都会产生覆盖率审计。每次 `/qa` Bug 修复都会生成回归测试。100% 测试覆盖率是目标——测试让感觉型编程安全而非鲁莽。

**`/document-release` 是你从未有过的工程师。** 它读取项目中的每个文档文件，交叉引用差异，更新所有漂移的内容。README、ARCHITECTURE、CONTRIBUTING、CLAUDE.md、TODOS——全部自动保持最新。现在 `/ship` 会自动调用它——无需额外命令，文档始终保持最新。

**真实浏览器模式。** `/open-gstack-browser` 启动 GStack 浏览器，一个带有反爬虫隐身、自定义品牌和内置侧边栏扩展的 AI 控制 Chromium。Google 和 NYTimes 等网站无需验证码即可工作。菜单栏显示"GStack Browser"而不是"Chrome for Testing"。你的普通 Chrome 保持不变。所有现有浏览命令不变。`$B disconnect` 返回无头模式。浏览器在窗口打开期间保持活动……工作时不会因为空闲超时而被杀死。

**侧边栏代理——你的 AI 浏览器助手。** 在 Chrome 侧边栏中输入自然语言，子 Claude 实例执行它。"导航到设置页面并截图。""用测试数据填写这个表单。""遍历列表中的每一项并提取价格。"侧边栏自动路由到正确的模型：Sonnet 处理快速操作（点击、导航、截图），Opus 处理阅读和分析。每个任务最多 5 分钟。侧边栏代理在隔离会话中运行，不会干扰你的主 Claude Code 窗口。侧边栏底部有一键 Cookie 导入。

**个人自动化。** 侧边栏代理不只用于开发工作流。示例："浏览我孩子的学校家长门户，把所有其他家长的姓名、电话号码和照片添加到我的 Google 联系人。"有两种方式进行身份验证：（1）在有头浏览器中登录一次，你的会话持久保存；或者（2）点击侧边栏底部的"cookies"按钮，从你真实的 Chrome 导入 Cookie。一旦通过身份验证，Claude 就会导航目录，提取数据，并创建联系人。

**提示注入防御。** 恶意网页试图劫持你的侧边栏代理。gstack 内置了分层防御：与浏览器捆绑的 22MB ML 分类器在本地扫描每个页面和工具输出，一个 Claude Haiku 转录检查对完整对话形状进行投票，系统提示词中的随机金丝雀 Token 跨文本、工具参数、URL 和文件写入捕获会话窃取尝试，判定组合器要求两个分类器同意才能阻止（防止对 Stack Overflow 风格指令页面的单模型误报）。侧边栏标题中的盾牌图标显示状态（绿/橙/红）。通过 `GSTACK_SECURITY_ENSEMBLE=deberta` 可选启用 721MB DeBERTa-v3 集成，实现 2/3 同意机制。紧急关闭开关：`GSTACK_SECURITY_OFF=1`。完整技术栈请见 [ARCHITECTURE.md](ARCHITECTURE.md#prompt-injection-defense-sidebar-agent)。

**AI 卡住时的浏览器交接。** 遇到验证码、认证墙或 MFA 提示？`$B handoff` 以完全相同的页面打开一个可见的 Chrome，带有所有 Cookie 和标签页。解决问题，告诉 Claude 你已完成，`$B resume` 从离开的地方继续。代理甚至会在连续三次失败后自动建议这个方案。

**`/pair-agent` 是跨代理协调。** 你在用 Claude Code，同时也在运行 OpenClaw、Hermes 或 Codex。你想让它们都看同一个网站。输入 `/pair-agent`，选择你的代理，一个 GStack 浏览器窗口打开供你观察。技能打印出一块指令，粘贴到另一个代理的聊天中。它用一次性设置密钥换取会话 Token，创建自己的标签页，开始浏览。你看到两个代理在同一个浏览器中工作，各自在自己的标签页里，互不干扰。如果安装了 ngrok，隧道自动启动，另一个代理可以在完全不同的机器上。同机器代理有零摩擦的快捷方式直接写入凭据。这是第一次来自不同供应商的 AI 代理可以通过共享浏览器进行真正安全的协调：作用域 Token、标签页隔离、限速、域名限制和活动归因。

**多 AI 第二意见。** `/codex` 从 OpenAI 的 Codex CLI 获得独立审查——一个完全不同的 AI 查看同一个差异。三种模式：带通过/失败门槛的代码审查、主动尝试破坏你代码的对抗性挑战，以及有会话连续性的开放咨询。当 `/review`（Claude）和 `/codex`（OpenAI）都审查了同一分支时，你会得到一个跨模型分析，显示哪些发现重叠，哪些是每个模型独有的。

**按需安全护栏。** 说"be careful"，`/careful` 会在任何破坏性命令前发出警告——rm -rf、DROP TABLE、force-push、git reset --hard。`/freeze` 在调试时将编辑锁定在一个目录，这样 Claude 就无法意外"修复"不相关的代码。`/guard` 同时激活两者。`/investigate` 自动冻结到正在调试的模块。

**主动技能建议。** gstack 注意到你所处的阶段——头脑风暴、审查、调试、测试——并建议正确的技能。不喜欢？说"stop suggesting"，它会跨会话记住。

## 10-15 个并行冲刺

gstack 在单个冲刺中很强大，同时运行十个时更具变革性。

[Conductor](https://conductor.build) 在并行中运行多个 Claude Code 会话——每个都在自己的隔离工作区中。一个会话对新想法运行 `/office-hours`，另一个对 PR 运行 `/review`，第三个实现功能，第四个对预发布环境运行 `/qa`，另外六个在其他分支上。全部同时进行。我经常运行 10-15 个并行冲刺——这是目前的实际上限。

冲刺结构是让并行工作的原因。没有流程，十个代理就是十个混乱的来源。有了流程——思考、规划、构建、审查、测试、交付——每个代理都清楚地知道该做什么以及何时停止。你像 CEO 管理团队一样管理它们：关注重要的决策，让其余的自行运行。

### 语音输入（AquaVoice、Whisper 等）

gstack 技能有对语音友好的触发短语。自然地说出你想要的——"做一次安全检查"、"测试网站"、"做工程审查"——正确的技能就会激活。你不需要记住斜杠命令名称或缩写词。

## 卸载

### 方式一：运行卸载脚本

如果 gstack 安装在你的机器上：

```bash
~/.claude/skills/gstack/bin/gstack-uninstall
```

这会处理技能、符号链接、全局状态（`~/.gstack/`）、项目本地状态、browse 守护进程和临时文件。使用 `--keep-state` 保留配置和分析数据。使用 `--force` 跳过确认。

### 方式二：手动删除（没有本地仓库）

如果你没有克隆仓库（例如你通过 Claude Code 粘贴安装，之后删除了克隆）：

```bash
# 1. 停止 browse 守护进程
pkill -f "gstack.*browse" 2>/dev/null || true

# 2. 删除指向 gstack/ 的每技能符号链接
find ~/.claude/skills -maxdepth 1 -type l 2>/dev/null | while read -r link; do
  case "$(readlink "$link" 2>/dev/null)" in gstack/*|*/gstack/*) rm -f "$link" ;; esac
done

# 3. 删除 gstack
rm -rf ~/.claude/skills/gstack

# 4. 删除全局状态
rm -rf ~/.gstack

# 5. 删除集成（跳过未安装的）
rm -rf ~/.codex/skills/gstack* 2>/dev/null
rm -rf ~/.factory/skills/gstack* 2>/dev/null
rm -rf ~/.kiro/skills/gstack* 2>/dev/null
rm -rf ~/.openclaw/skills/gstack* 2>/dev/null

# 6. 删除临时文件
rm -f /tmp/gstack-* 2>/dev/null

# 7. 每项目清理（在每个项目根目录运行）
rm -rf .gstack .gstack-worktrees .claude/skills/gstack 2>/dev/null
rm -rf .agents/skills/gstack* .factory/skills/gstack* 2>/dev/null
```

### 清理 CLAUDE.md

卸载脚本不会编辑 CLAUDE.md。在每个添加了 gstack 的项目中，删除 `## gstack` 和 `## Skill routing` 部分。

### Playwright

`~/Library/Caches/ms-playwright/`（macOS）保留原位，因为其他工具可能共享它。如果没有其他工具需要它，可以删除。

---

免费，MIT 许可证，开源。无付费版，无等待名单。

我开源了我构建软件的方式。你可以 Fork 它，让它成为你自己的。

> **我们在招聘。** 想以 AI 编码的速度交付真实产品并帮助强化 gstack？
> 来 YC 工作——[ycombinator.com/software](https://ycombinator.com/software)
> 极具竞争力的薪资和股权。旧金山，Dogpatch 区。

## GBrain——为你的编码代理提供持久知识

[GBrain](https://github.com/garrytan/gbrain) 是 AI 代理的持久知识库——把它想象成代理在会话之间真正保留的记忆。GStack 为你提供从零到"正在运行，代理可以调用它"的一条命令路径。

```bash
/setup-gbrain
```

三种路径，选择一种：

- **Supabase，现有 URL** — 你的云代理已经配置了一个 brain；粘贴 Session Pooler URL，现在这台笔记本使用相同的数据。
- **Supabase，自动配置** — 粘贴 Supabase 个人访问 Token；技能创建一个新项目，轮询至健康状态，获取 pooler URL，并传给 `gbrain init`。全程约 90 秒。
- **PGLite 本地** — 零账户，零网络，约 30 秒。仅在这台 Mac 上的隔离 brain。很适合先试用；之后用 `/setup-gbrain --switch` 迁移到 Supabase。

初始化后，技能提供将 gbrain 注册为 Claude Code 的 MCP 服务器（`claude mcp add gbrain -- gbrain serve`），使 `gbrain search`、`gbrain put_page` 等作为一等类型化工具出现——而非 bash 命令调用。

**每远程信任策略。** 你机器上的每个仓库获得三个层级之一：

- `read-write` — 代理可以搜索 brain 并从该仓库写回新页面
- `read-only` — 代理可以搜索但永远不写（适合多客户顾问：搜索共享 brain，在客户 B 的仓库中不污染客户 A 的工作）
- `deny` — 完全不与 gbrain 交互

技能每个仓库只询问一次。决定在同一远程的所有工作树和分支中持续生效。

**GStack 记忆同步（不同功能，相同的私有仓库基础设施）。** 可选地将你的 gstack 状态（学习内容、CEO 计划、设计文档、回顾、开发者档案）推送到私有 git 仓库，使你的记忆跨机器同步，带有一次性隐私提示（全部白名单/仅工件/关闭）和纵深防御的密钥扫描器，在 AWS 密钥、Token、PEM 块和 JWT 离开你的机器之前拦截它们。

```bash
gstack-brain-init
```

**完整内容——每个场景、每个参数、每个命令行助手、每个故障排除步骤：** [USING_GBRAIN_WITH_GSTACK.md](USING_GBRAIN_WITH_GSTACK.md)

其他参考：[docs/gbrain-sync.md](docs/gbrain-sync.md)（同步专属指南）• [docs/gbrain-sync-errors.md](docs/gbrain-sync-errors.md)（错误索引）

## 文档

| 文档 | 内容 |
|------|------|
| [技能深度解析](docs/skills.md) | 每个技能的理念、示例和工作流（含 Greptile 集成） |
| [构建者信条](ETHOS.md) | 构建者哲学：煮沸湖泊、先搜索再构建、三层知识 |
| [在 GStack 中使用 GBrain](USING_GBRAIN_WITH_GSTACK.md) | `/setup-gbrain` 的每种路径、参数、命令行助手和故障排除步骤 |
| [GBrain 同步](docs/gbrain-sync.md) | 跨机器记忆设置、隐私模式、故障排除 |
| [架构](ARCHITECTURE.md) | 设计决策和系统内部结构 |
| [浏览器参考](BROWSER.md) | `/browse` 的完整命令参考 |
| [贡献指南](CONTRIBUTING.md) | 开发设置、测试、贡献者模式和开发模式 |
| [更新日志](CHANGELOG.md) | 每个版本的新内容 |

## 隐私与遥测

gstack 包含**可选加入**的使用遥测，以帮助改进项目。以下是具体情况：

- **默认关闭。** 除非你明确同意，否则不会向任何地方发送任何内容。
- **首次运行时，** gstack 会询问你是否想分享匿名使用数据。你可以拒绝。
- **发送内容（如果你选择加入）：** 技能名称、持续时间、成功/失败、gstack 版本、操作系统。仅此而已。
- **永远不发送：** 代码、文件路径、仓库名称、分支名称、提示词或任何用户生成的内容。
- **随时更改：** `gstack-config set telemetry off` 立即禁用一切。

数据存储在 [Supabase](https://supabase.com)（开源 Firebase 替代品）中。Schema 在 [`supabase/migrations/`](supabase/migrations/) 中——你可以验证具体收集了什么。仓库中的 Supabase 可发布密钥是公开密钥（类似 Firebase API 密钥）——行级安全策略拒绝所有直接访问。遥测通过经过验证的边缘函数流动，这些函数执行 schema 检查、事件类型白名单和字段长度限制。

**本地分析始终可用。** 运行 `gstack-analytics` 从本地 JSONL 文件查看你的个人使用仪表板——无需远程数据。

## 故障排除

**技能不显示？** `cd ~/.claude/skills/gstack && ./setup`

**`/browse` 失败？** `cd ~/.claude/skills/gstack && bun install && bun run build`

**安装过时？** 运行 `/gstack-upgrade`——或在 `~/.gstack/config.yaml` 中设置 `auto_upgrade: true`

**想要更短的命令？** `cd ~/.claude/skills/gstack && ./setup --no-prefix`——从 `/gstack-qa` 切换为 `/qa`。你的选择会在未来升级时被记住。

**想要命名空间命令？** `cd ~/.claude/skills/gstack && ./setup --prefix`——从 `/qa` 切换为 `/gstack-qa`。如果你同时运行其他技能包，这很有用。

**Codex 说"Skipped loading skill(s) due to invalid SKILL.md"？** 你的 Codex 技能描述已过时。修复：`cd ~/.codex/skills/gstack && git pull && ./setup --host codex`——或对于仓库本地安装：`cd "$(readlink -f .agents/skills/gstack)" && git pull && ./setup --host codex`

**Windows 用户：** gstack 在 Windows 11 上通过 Git Bash 或 WSL 工作。除 Bun 外还需要 Node.js——Bun 在 Windows 上的 Playwright 管道传输存在已知问题（[bun#4253](https://github.com/oven-sh/bun/issues/4253)）。browse 服务器会自动回退到 Node.js。确保 `bun` 和 `node` 都在你的 PATH 中。

**Claude 说看不到技能？** 确保你项目的 `CLAUDE.md` 有 gstack 部分。添加以下内容：

```
## gstack
Use /browse from gstack for all web browsing. Never use mcp__claude-in-chrome__* tools.
Available skills: /office-hours, /plan-ceo-review, /plan-eng-review, /plan-design-review,
/design-consultation, /design-shotgun, /design-html, /review, /ship, /land-and-deploy,
/canary, /benchmark, /browse, /open-gstack-browser, /qa, /qa-only, /design-review,
/setup-browser-cookies, /setup-deploy, /setup-gbrain, /retro, /investigate, /document-release,
/codex, /cso, /autoplan, /pair-agent, /careful, /freeze, /guard, /unfreeze, /gstack-upgrade, /learn.
```

## 许可证

MIT。永远免费。去构建点什么吧。
