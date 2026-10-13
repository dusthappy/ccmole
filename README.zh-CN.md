# CCMole Skills

[English](README.md) | 简体中文

**换一个 Agent，接着做；换一套工具，带上需要的配置。**

CCMole 提供 4 个可独立安装的 Agent Skill，帮助你在不同 Agent 之间接续开发上下文、复用选定配置。直接在现有客户端使用；可以按需安装一个，也可以安装整套工作流。

当前为 **0.2.0 预览版**：提供 4 个 Skill，以及 Codex、Claude Code、ZCode、Kimi Code、Grok Build、OpenCode、Qoder、CodeBuddy、Gemini CLI 的客户端指南。安装入口已核对官方文档，真实客户端运行情况按实际证据报告。

## 从一句话开始

```text
把这个聊天的工作交给下一个 Agent，保留还没解决的问题和下一步。
```

```text
这个对话太长了，生成一份简洁的续行简报，保留失败测试和缺失上下文。
```

```text
读取这个交接包，先核对当前工程，再接着完成剩余工作。
```

```text
把这个项目的 Rules、指定的 Skill 和 MCP 配置迁到另一 Agent，先给我看差异。
```

例如，把 Kimi Code 中的工作交给 ZCode，或把 Grok Build 的项目交给 OpenCode。接力使用可读的交接包，配置迁移则先核对两端格式和作用域。

显式调用时使用所选 Skill 的完整名称。例如 Codex / ZCode 使用 `$ccmole-session-handoff`，Kimi Code 使用 `/skill:ccmole-session-handoff`，Claude Code / Grok Build 使用 `/ccmole-session-handoff`。OpenCode 可直接说「使用 ccmole-session-handoff 准备交接」。其他任务替换为对应 Skill 名称。

## 选择 Skill

| Skill | 何时使用 | 你得到什么 |
|---|---|---|
| [ccmole-session-handoff](skills/ccmole-session-handoff/SKILL.md) | 把工作交给另一 Agent 或聊天 | 可移植交接包，支持完整可用范围、选定范围或压缩；授权后通过受支持入口投递 |
| [ccmole-context-compact](skills/ccmole-context-compact/SKILL.md) | 将长对话压缩以便后续继续 | 有损但可追溯的简报，保留最新更正、失败、缺失上下文和下一步 |
| [ccmole-project-resume](skills/ccmole-project-resume/SKILL.md) | 接收交接包或换设备继续 | 核对项目与代码状态，就绪后按要求续行；仅要求检查时只报告结果 |
| [ccmole-config-reuse](skills/ccmole-config-reuse/SKILL.md) | 复用选定的 Rules、Skills、MCP 或非敏感设置 | 具体计划与 Diff；授权应用时保留备份、检查漂移并验证结果 |

每个目录都自带指令、所需资源和许可证，不依赖其他 CCMole Skill。交接流程本身支持按需压缩；单独的压缩 Skill 不发送交接包、不新建聊天，也不开始开发。

配置迁移会检查作用域、格式、相对路径、依赖和凭证引用。源文件保留，目标已有内容默认保留。未知版本或无法验证的字段只输出预览；API Key、登录令牌和原生会话数据库不随包迁移。

## 安装

下载 [dusthappy/ccmole](https://github.com/dusthappy/ccmole) 后，从 `skills/` 下的 4 个目录中选择所需项，将每个 **完整的 Skill 目录**复制到宿主的 Skill 目录，保留名称和全部支持文件。整套安装时复制全部 4 个目录。Skills 不引入 CCMole Desktop、Rust、Node.js、数据库或后台服务依赖。

```bash
git clone https://github.com/dusthappy/ccmole.git
```

下表列出安装目标的**父目录**。在其后加上所选 Skill 的完整名称，例如 `.agents/skills/ccmole-session-handoff/`。调用示例中的 `<skill-name>` 也要替换为完整名称。不要把整个仓库嵌套为一个 Skill 目录。

| 客户端 | 项目 Skill 父目录 | 用户 Skill 父目录 | 调用 / 发现 |
|---|---|---|---|
| Codex | `.agents/skills/` | `~/.agents/skills/` | `$<skill-name>` |
| Claude Code | `.claude/skills/` | `~/.claude/skills/` | `/<skill-name>` |
| ZCode 内置 Agent | `.zcode/skills/` | `~/.zcode/skills/` | 设置 → Skills → 刷新并启用；`$<skill-name>` |
| Kimi Code CLI / Desktop | `.kimi-code/skills/` | `~/.kimi-code/skills/`，或 `$KIMI_CODE_HOME/skills/` | 新会话中 `/skill:<skill-name>` |
| Grok Build CLI | `.grok/skills/` | `~/.grok/skills/` | `/<skill-name>` |
| OpenCode | `.opencode/skills/` | `~/.config/opencode/skills/` | 自然语言要求使用 `<skill-name>` |
| Qoder CLI | `.qoder/skills/` | `~/.qoder/skills/` | `/skills reload` 后 `/<skill-name>` |
| CodeBuddy IDE | `.codebuddy/skills/` | 设置中的 Skills 导入入口，核对作用域 | Skills 列表确认后，自然语言调用 |
| Gemini CLI | `.gemini/skills/` | `~/.gemini/skills/` | `/skills reload`、`/skills list` 后自然语言调用 |

表中是默认路径，请以目标机器的配置覆盖和已安装版本为准。Kimi 路径对应当前 Node.js 版 Kimi Code；旧 Python CLI 需另行核对。只选择需要的客户端和作用域，同名目录先检查，避免装到多个共享发现目录后互相覆盖。

安装前检查目标是否已有同名目录；更新时先备份本地修改，再替换完整目录，避免残留旧引用。安装后开启新聊天并调用 Skill。卸载时只移除选定的 Skill 安装目录，用户生成的交接包和配置备份独立保留。

也可以让 Agent 帮你安装：

```text
请把我下载的 CCMole 包中的 ccmole-session-handoff 和 ccmole-project-resume 安装到当前项目的 Skill 目录。
检查已有目录，保留我的本地修改，并告诉我各自如何调用。
```

每个 Skill 自带客户端指南。[交接指南](skills/ccmole-session-handoff/references/clients.md) 说明投递入口；逐客户端官方来源、规则/MCP 格式差异和验证边界见 [配置客户端指南](skills/ccmole-config-reuse/references/clients.md)，核对日期 2026-10-13。其他支持 [Agent Skills 格式](https://agentskills.io/specification) 的宿主需确认其安装位置和工具权限；不据此宣称全部平台已实测。

**Grok 与 Kimi 需要区分具体产品入口。** Grok Bot 的私有 Skill、普通 Grok 聊天、Grok Build CLI 不共用一套安装方式；Kimi Code Web 是本地 CLI 的网页界面，也不同于普通 Kimi 网页聊天。IDE 集成、Grok Bot 的完整资源导入仍需在目标宿主验证。仅有聊天能力时可粘贴自包含交接包，不宣称已安装完整 Skill。

## 从 0.1.x 升级

原来的 `skills/ccmole/` 已拆为上面的 4 个 Skill。选择所需项、保留本地修改，安装后确认发现结果。旧的 `$ccmole` / `/ccmole` 调用不是新 Skill 的别名。

如果旧 `ccmole` 仍在安装目录中，先备份到宿主 Skill 发现目录之外，确认替代项可发现后再停用或移除旧安装。更新不会通过脚本自动删除它。已存在与新包同名的 Skill 时也先核对冲突。用户生成的交接包和配置备份独立保留，不随安装目录移除。

## 实际运行边界

这是工作流指令包，执行能力和权限来自宿主 Agent。它本身不包含守护进程、网络传输服务或凭证存储。宿主模型仍可能处理交给它的内容。

- 仅有聊天能力时，可以整理和接收文本上下文；文件核验和配置应用需要宿主文件工具。
- 自动新建聊天、发送交接内容或验证目标配置实际生效，需要宿主提供相应受支持工具和用户授权；工具不可用时提供手动步骤。
- 当前版本不提供统一历史会话索引、原生会话格式迁移、桌面界面、后台自动同步、Provider 代理或跨文件事务保证。
- 配置已写入与目标 Agent 已加载配置分别报告，不把两者混为成功。

## 发布内容

`skills/` 下的 4 个目录可分别独立安装；参考资料和模板属于支持文件，不是额外的 Skill。仓库根的说明和 [验证场景](verification/scenarios.md) 供使用者与维护者查看。

本包独立交付 Skill 工作流，不代表既有 CCMole Desktop V1 已完成验收。当前版本 `0.2.0` 与此前 `0.1.x` 的验证记录见 [验证记录](verification/results.md)。

本独立合集采用 [MIT 许可证](LICENSE)，每个可安装目录均附带一份。

产品设计参考了 [yobiru](https://github.com/chekusu/yobiru) 的场景表达与渐进上手思路；CCMole 的流程与文本独立编写，未复制其代码或 Skill 内容。
