---
title: Vibe coding setup / AI编程配置
date: 2026-04-29
category: [Technology, environment]
toc_number: false
---

这篇主要记录一下我现在理解的 AI coding / vibe coding 环境配置。很多平台名字、价格和策略都会变，所以这里更想讲清楚“有哪些层”和“怎么把它们连起来”。

# What is CLI?

CLI = Command Line Interface，中文一般叫命令行界面。

和 GUI 最大的区别是，CLI 不是点按钮，而是通过文本命令和系统交互。现在很多 AI 编程工具都会优先提供 CLI 版本，因为它更容易：

- 读取整个 repo
- 搜索多个文件
- 运行 `git status`、test、lint、build
- 批量修改代码
- 在 SSH / 远程机器 / tmux 环境里稳定工作

如果以前主要在 IDE 里开发，可以先把 CLI 理解成“一个更可组合的工作台”。常见的基础命令有：

```bash
pwd
ls
git status
```

如果安装了 terminal agent（例如 Claude Code 一类的工具），通常也是在项目根目录下直接启动：

```bash
claude
```

对 AI coding 来说，CLI 通常负责“搜索、改代码、跑命令”，IDE 负责“看 diff、跳转定义、手动微调”。两者配合会比只用其中一个舒服很多。

# How to subscribe/get tokens?

这里的“token”经常会被混着说，最好先分清楚它到底指什么：

- **Subscription / 订阅**：给产品付月费，比如某个 IDE 的 AI 套餐
- **API Key**：给 CLI、插件或脚本调用模型时使用的密钥
- **LLM tokens**：模型计费单位，输入和输出文本都会折算成 token

## 1. 最省事：直接买产品订阅

适合刚开始体验的人。优点是开箱即用、配置少；缺点是灵活性一般，模型、上下文长度和调用方式通常都由平台决定。

常见场景：

- IDE 自带 AI 能力
- 聊天产品内置 code agent
- 一体化的 AI coding IDE

如果你的目标只是“先开始写起来”，订阅通常是最简单的方案。

## 2. 更灵活：自己申请 API Key

如果你想把同一个模型接到不同工具里，比如 terminal agent、编辑器插件、脚本或者自己的小工具，那通常需要自己申请 API Key。

一般流程：

1. 在模型提供商后台开通 billing / credits
2. 创建 API Key
3. 把 key 放到环境变量里，而不是写死在代码中
4. 让 CLI 或 IDE 插件从环境变量读取

例如在 `zsh` / `bash` 中：

```bash
export ANTHROPIC_API_KEY="your_key_here"
export OPENAI_API_KEY="your_key_here"
export GOOGLE_API_KEY="your_key_here"
```

如果希望每次打开终端都生效，可以写进 `~/.zshrc` 或 `~/.bashrc`，然后重新加载配置。

如果是 Windows PowerShell，写法会不一样，但思路完全一样：不要把 key 硬编码到项目里。

## 3. 关于安全

API Key 本质上就是权限凭证，所以最好养成几个习惯：

- 不要把 API Key 直接提交到 git 仓库
- 不要发到公开 issue、聊天记录或截图里
- 如果项目用 `.env`，记得加入 `.gitignore`
- 如果怀疑泄露，第一时间 revoke / rotate key

# How to use in IDEs?

我现在更推荐把 AI 编程工具分成三层来理解，而不是只盯着某一个具体产品。

## 1. IDE 内补全（tab completion）

这是最轻量的用法，适合：

- 补几行样板代码
- 根据注释生成函数
- 做单文件内的小修改

优点是响应快、打断少；缺点是它更像“高级自动补全”，不太擅长理解整个仓库。

## 2. IDE 内聊天 / agent

适合：

- 解释报错
- 生成某个文件的初稿
- 做中小规模重构
- 在编辑器里直接 review diff

这种方式通常最适合日常开发，因为上下文离代码最近，切换成本也最低。

## 3. Terminal agent + IDE

这是我觉得最适合真实项目的一种组合：

- 在 **terminal** 里让 agent 搜索仓库、改多个文件、跑测试
- 在 **IDE** 里看 diff、跳定义、做最后的人工确认

这个组合的好处是：

- terminal 更适合执行命令和自动化
- IDE 更适合阅读、比较和局部精修
- 对远程开发机、SSH、tmux 更友好

所以如果后面真的要进入“vibe coding”状态，我会更推荐把 terminal 和 IDE 配合起来，而不是只依赖一个聊天窗口。

## VS Code / Cursor / JetBrains 的共通检查项

不管你用哪个 IDE，先确保下面几件事是通的：

1. 能正常打开项目根目录
2. 内置 terminal 能跑 `git status`
3. 项目运行时已经装好（例如 Python / Node.js / Java）
4. lint / test / build 至少能在本地手动跑一次
5. 如果在校园网、公司网或国内网络环境下，代理设置可用

因为 AI 工具本质上是在“已有开发环境”上加速，而不是替你补齐环境本身。

## 一个简单够用的配置思路

如果只是个人学习或 side project，我会建议：

- **编辑器**：VS Code 或 Cursor
- **终端**：iTerm2 / Windows Terminal / 系统终端
- **Shell**：zsh 或 bash
- **版本控制**：git
- **AI 工具**：
  - 一个 IDE 内补全 / 聊天工具
  - 一个 terminal agent
- **可选增强**：SSH、tmux、代理、`ripgrep`

这里最重要的不是“装得多全”，而是这几个组件之间要顺畅：编辑器能看代码，终端能跑命令，git 能看变更，模型能稳定调用。

## 新手工作流建议

如果是刚开始接触 AI coding，我会建议按这个顺序来：

1. 先在 IDE 里用补全和聊天
2. 再学会在 terminal 里看 `git status`、跑测试
3. 最后再上 agent 式工具做多文件修改

这样不容易一开始就“黑箱感太强”，也更容易知道问题到底是出在代码、环境，还是模型本身。

# Popular AI coding tools comparison

下面这个表更偏“怎么选工具”，不是严格的 benchmark。价格和额度变化很快，尤其是 2026 年很多产品都在从固定请求数切到 token / credits / usage-based 计费，所以这里按 **2026-05-06** 看到的公开页面记录一版。

| 产品 | 主要使用方式 | 典型价格 / 计费方式 | 更适合谁 | 备注 |
| --- | --- | --- | --- | --- |
| GitHub Copilot | VS Code / JetBrains / Visual Studio / Xcode / Neovim / GitHub / CLI；补全、chat、agent、code review、cloud agent | Free；Pro $10/月；Pro+ $39/月；Business / Enterprise 另计。GitHub 说明 2026-06-01 起切到 GitHub AI Credits，用量超过 included credits 后继续按 credits 付费 | 已经重度使用 GitHub 和主流 IDE 的开发者 / 团队 | 覆盖面最广，补全体验成熟；Pro / Pro+ 新订阅在 2026-04 后有暂停提示，购买前要看当前账户页面 |
| Cursor | 独立 AI IDE；Tab 补全、chat、agent、rules、MCP、cloud agents | Hobby 免费；Pro $20/月；Pro+ $60/月；Ultra $200/月；Teams $40/user/月 | 想要“IDE 内完成大部分 AI coding”的个人开发者 | 上手快，适合 side project 和真实 repo；如果已经习惯 VS Code，迁移成本低 |
| Windsurf | 独立 AI IDE + Cascade agent；也有插件和后台开发能力 | Free；Pro $20/月；Max $200/月；Teams $40/user/月；Enterprise 定制；超出额度通常按 API price / credits | 喜欢 agent-first IDE、想用 Cascade 做多文件修改的人 | 和 Cursor 定位接近；价格页显示支持主流模型、Fast Context、SWE 模型、Devin Cloud sessions 等能力 |
| Claude Code | Terminal agent，也可通过 Claude 订阅访问；适合读 repo、改多文件、跑测试 | Claude Pro $20/月；Max from $100/月；Team 标准席 $30/月，含 Claude Code 的 Premium seat $150/月；也可走 Anthropic API token 用量 | 喜欢 terminal 工作流、需要强代码理解和多文件修改的人 | 用量差异很大。Anthropic 文档给过企业部署粗略均值：约 $13/active day，约 $150-250/developer/月 |
| OpenAI Codex | Codex CLI / IDE extension / Codex app / cloud task；可本地 pair，也可把任务交给 cloud agent | Codex 包含在 ChatGPT Plus、Pro、Business、Enterprise/Edu 等计划；Plus $20/月，Pro $200/月，Business $30/user/月按月；Codex 用量已按 token/credits 计 | 想把 ChatGPT 账号直接接入 terminal / IDE / cloud agent 的用户 | 适合和 ChatGPT 项目、文档、代码一起用；实际成本取决于模型、上下文和输出量 |
| Gemini Code Assist | VS Code / JetBrains / Android Studio / Cloud Shell / Gemini CLI / GitHub PR review | Individual $0；Standard $19/user/月，或无年度承诺 $22.80/user/月；Enterprise $45/user/月，或无年度承诺 $54/user/月 | 想要免费额度大、Google Cloud / Firebase / Android 生态内开发的人 | 免费个人版公开写明每天 6,000 code-related requests 和 240 chat requests；Gemini CLI / Agent Mode 请求数与 Code Assist 共享 |
| JetBrains AI Assistant / Junie | JetBrains IDE 内 AI Assistant、补全、chat、agent / Junie；也支持本地模型和部分云模型 | AI Free；AI Pro 个人 $10/月、商业 $20/月；AI Ultimate 个人 $30/月、商业 $60/月；Enterprise $60 起或定制 | 已经使用 IntelliJ IDEA / PyCharm / WebStorm / GoLand 等 JetBrains IDE 的人 | IDE 集成深，适合不想换到 Cursor/Windsurf 的 JetBrains 用户；额度用 AI Credits 表示 |
| Devin | 云端 autonomous software engineer；给任务、让它计划、编码、测试、交付；也有 DeepWiki / review / integrations | Free；Pro $20/月；Max $200/月；Teams $80/月；Enterprise 定制；超出 quota 后 pay-as-you-go | 想把明确 ticket / migration / refactor 交给后台 agent 的团队或重度个人用户 | 更像“委派任务”而不是实时 pair programming；适合边界清楚、可测试、可 review 的任务 |
| Replit Agent | 浏览器 IDE + Agent + deploy；从自然语言生成、修改、部署应用 | Starter 免费；Core $25/月或 $20/月年付，含 $25 monthly credits；Pro $100/月或 $95/月年付，含 $100 credits；AI 和云资源消耗 credits | 快速做 web app / demo / MVP，尤其是不想本地配环境的人 | 优点是从编码到部署一体化；缺点是 credits 成本会随任务复杂度浮动 |
| Cline | VS Code extension / CLI；本地 agent，可读写文件、跑命令、接 MCP | 开源版免费；自己付模型 API / inference；Enterprise 定制 | 想 BYOK、控制模型和成本、在 VS Code 里使用 agent 的人 | 平台不锁模型，成本主要来自 OpenAI / Anthropic / Gemini / OpenRouter 等模型调用 |
| Roo Code | VS Code extension + Roo Code Cloud；可 BYOM / BYOK，也可用 Roo Router | VS Code extension 免费 + inference；Cloud Free $0 + credits；Cloud Team $99/月 + credits；Cloud agent $5/hour credits，模型 inference 另计 | 想要开源 VS Code agent，同时可选云端后台任务的人 | 价格更透明，但要自己理解模型 token 和 cloud agent 运行时间 |
| Continue | VS Code / JetBrains extension；自定义 code agents，BYOK / managed credits | Starter $3 / million tokens pay-as-you-go；Team $20/seat/月，含 $10 credits；Company 定制；另有开源 / BYOK 路线 | 想自定义 agent、团队共享 rules / blocks / prompts 的开发者或团队 | 更像可组装的 AI coding layer；适合愿意配置模型、规则和团队治理的人 |
| aider | Terminal pair programmer；直接在 git repo 里指定文件、让模型编辑 | 工具本身开源免费；成本来自你连接的 LLM API 或本地模型 | 喜欢 terminal、想要简单直接 BYOK 的开发者 | 轻量、透明、git 友好；不追求漂亮 UI，适合精确控制上下文和 diff |

简单选型可以这样看：

- **只想最稳妥地开始**：GitHub Copilot / Cursor / Windsurf
- **喜欢 terminal agent**：Claude Code / OpenAI Codex / aider
- **已经在 JetBrains 生态里**：JetBrains AI Assistant / Junie
- **想要免费或低成本试水**：Gemini Code Assist / Cline / Roo Code / Continue / aider
- **想把整块任务交给后台跑**：Devin / Replit Agent / Copilot cloud agent / Codex cloud task
- **在意成本可控**：优先选 BYOK 工具，并给 API key 设置预算上限

几个价格陷阱也要注意：

- “Unlimited” 通常会有 fair use、模型限制或高峰期限制，不等于无限算力。
- Agent 模式比普通 chat 贵很多，因为它会多轮读取文件、生成 diff、跑命令、再修复。
- 大 repo 的上下文、长输出、并行多个 agent session，都会显著增加 token / credits。
- 团队采购时要看 SSO、日志、数据保留、训练策略、代码引用过滤、预算上限，而不只是单人月费。

资料来源：GitHub Copilot [plans](https://github.com/features/copilot/plans) / [usage-based billing](https://docs.github.com/en/copilot/concepts/billing/usage-based-billing-for-individuals)、[Cursor pricing](https://cursor.com/en-US/pricing)、[Windsurf pricing](https://windsurf.com/pricing)、[Claude pricing](https://www.claude.com/pricing) / [Claude Code costs](https://code.claude.com/docs/en/costs)、OpenAI [ChatGPT pricing](https://openai.com/chatgpt/pricing) / [Codex in ChatGPT](https://help.openai.com/en/articles/11369540-codex-in-chatgpt) / [Codex rate card](https://help.openai.com/en/articles/20001106-codex-rate-card)、[Gemini Code Assist](https://codeassist.google/)、[JetBrains AI plans](https://www.jetbrains.com/help/ai-assistant/licensing-and-subscriptions.html)、[Devin pricing](https://devin.ai/pricing)、[Replit pricing](https://replit.com/site/pricing)、[Cline pricing](https://cline.bot/pricing)、[Roo Code pricing](https://roocode.com/pricing)、[Continue pricing](https://www.continue.dev/pricing)、[aider usage](https://aider.chat/docs/usage.html)。


