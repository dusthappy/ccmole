# CCMole Skill

**换一个 Agent，接着做；换一套工具，带上需要的配置。**

CCMole 是一个可安装的 Agent Skill，帮助你整理开发上下文、接续工作，并在不同 Agent 之间复用选定的 Rules、Skills、MCP 和非敏感配置。直接在你原本使用的 Agent 中操作。

当前为 **0.1.1 预览版**：提供两条工作流，以及 Codex、Claude Code、ZCode、Kimi Code、Grok Build、OpenCode、Qoder、CodeBuddy、Gemini CLI 的客户端指南。安装入口已核对官方文档，真实客户端运行情况按实际证据报告。

## 从一句话开始

```text
把这个聊天的工作交给下一个 Agent，保留还没解决的问题和下一步。
```

```text
读取这个交接包，先核对当前工程，再接着完成剩余工作。
```

```text
把这个项目的 Rules、指定的 Skill 和 MCP 配置迁到另一 Agent，先给我看差异。
```

例如，把 Kimi Code 中的工作交给 ZCode，或把 Grok Build 的项目交给 OpenCode。接力使用可读的交接包，配置迁移则先核对两端格式和作用域。

Codex / ZCode 使用 `$ccmole`，Kimi Code 使用 `/skill:ccmole`，Claude Code / Grok Build 使用 `/ccmole`。OpenCode 可直接说「使用 ccmole 帮我交接当前工作」。具体入口见下表。

## 两条工作流

| 工作流 | 你得到什么 |
|---|---|
| 上下文接力 | 包含目标、决定、工程状态、失败记录和下一步的 Markdown 交接包；支持完整可用范围、选定范围和有损压缩 |
| 接收并续行 | 核对项目、分支、提交和未提交修改；匹配后继续，不匹配时给出具体差异 |
| 配置复用 | 选定 Rules、Skills、MCP、非敏感设置的迁移计划与 Diff；授权后按目标实际支持的方式应用、验证并保留恢复信息 |

配置迁移会检查作用域、格式、相对路径、依赖和凭证引用。源文件保留，目标已有内容默认保留。未知版本或无法验证的字段只输出预览；API Key、登录令牌和原生会话数据库不随包迁移。

## 安装

下载 [dusthappy/ccmole](https://github.com/dusthappy/ccmole) 后，将 `skills/ccmole` **整个目录**复制到宿主的 Skill 目录。支持文件必须一起保留；无需安装 CCMole Desktop、Rust、Node.js、数据库或后台服务。

```bash
git clone https://github.com/dusthappy/ccmole.git
```

| 客户端 | 仅当前项目 | 当前用户所有项目 | 调用 / 发现 |
|---|---|---|---|
| Codex | `.agents/skills/ccmole/` | `~/.agents/skills/ccmole/` | `$ccmole` |
| Claude Code | `.claude/skills/ccmole/` | `~/.claude/skills/ccmole/` | `/ccmole` |
| ZCode 内置 Agent | `.zcode/skills/ccmole/` | `~/.zcode/skills/ccmole/` | 设置 → Skills → 刷新并启用；`$ccmole` |
| Kimi Code CLI / Desktop | `.kimi-code/skills/ccmole/` | `~/.kimi-code/skills/ccmole/`，或 `$KIMI_CODE_HOME/skills/ccmole/` | 新会话中 `/skill:ccmole` |
| Grok Build CLI | `.grok/skills/ccmole/` | `~/.grok/skills/ccmole/` | `/ccmole` |
| OpenCode | `.opencode/skills/ccmole/` | `~/.config/opencode/skills/ccmole/` | 自然语言要求使用 `ccmole` |
| Qoder CLI | `.qoder/skills/ccmole/` | `~/.qoder/skills/ccmole/` | `/skills reload` 后 `/ccmole` |
| CodeBuddy IDE | `.codebuddy/skills/ccmole/` | 设置中的 Skills 导入入口，核对作用域 | Skills 列表确认后，自然语言调用 |
| Gemini CLI | `.gemini/skills/ccmole/` | `~/.gemini/skills/ccmole/` | `/skills reload`、`/skills list` 后自然语言调用 |

表中是默认路径，请以目标机器的配置覆盖和已安装版本为准。Kimi 路径对应当前 Node.js 版 Kimi Code；旧 Python CLI 需另行核对。只选择需要的客户端和作用域，同名目录先检查，避免装到多个共享发现目录后互相覆盖。

安装前检查目标是否已有同名目录；更新时先备份本地修改，再替换完整目录，避免残留旧引用。安装后开启新聊天并调用 Skill。卸载时只移除安装的 `ccmole` 目录，用户生成的交接包和配置备份独立保留。

也可以让 Agent 帮你安装：

```text
请把我下载的 CCMole 发布包中的 skills/ccmole 安装到当前项目的 Skill 目录。
先检查同名目录，保留我的本地修改。安装后告诉我如何调用。
```

逐客户端官方来源、规则/MCP 格式差异和验证边界见 [客户端指南](skills/ccmole/references/clients.md)，核对日期 2026-10-13。其他支持 [Agent Skills 格式](https://agentskills.io/specification) 的宿主需确认其安装位置和工具权限；不据此宣称全部平台已实测。

**Grok 与 Kimi 需要区分具体产品入口。** Grok Bot 的私有 Skill、普通 Grok 聊天、Grok Build CLI 不共用一套安装方式；Kimi Code Web 是本地 CLI 的网页界面，也不同于普通 Kimi 网页聊天。IDE 集成、Grok Bot 的完整资源导入仍需在目标宿主验证。仅有聊天能力时可粘贴自包含交接包，不宣称已安装完整 Skill。

## 实际运行边界

这是工作流指令包，执行能力和权限来自宿主 Agent。它本身不包含守护进程、网络传输服务或凭证存储。宿主模型仍可能处理交给它的内容。

- 仅有聊天能力时，可以整理和接收文本上下文；文件核验和配置应用需要宿主文件工具。
- 自动新建聊天、发送交接内容或验证目标配置实际生效，需要宿主提供相应受支持工具和用户授权；工具不可用时提供手动步骤。
- 当前版本不提供统一历史会话索引、原生会话格式迁移、桌面界面、后台自动同步、Provider 代理或跨文件事务保证。
- 配置已写入与目标 Agent 已加载配置分别报告，不把两者混为成功。

## 发布内容

`skills/ccmole/` 是唯一需要安装的目录。仓库根的说明和 [验证场景](verification/scenarios.md) 供使用者与维护者查看。

本包独立交付 Skill 工作流，不代表既有 CCMole Desktop V1 已完成验收。当前版本 `0.1.1` 与此前 `0.1.0` 的验证记录见 [验证记录](verification/results.md)。

本独立发布包采用 [MIT 许可证](LICENSE)。

产品设计参考了 [yobiru](https://github.com/chekusu/yobiru) 的场景表达与渐进上手思路；CCMole 的流程与文本独立编写，未复制其代码或 Skill 内容。
