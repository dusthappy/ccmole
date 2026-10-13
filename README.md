# CCMole Skills

English | [简体中文](README.zh-CN.md)

**Switch agents and keep working. Switch tools and bring the configuration you need.**

CCMole provides four independently installable Agent Skills for carrying development context and selected configuration between agents. Use them in the clients you already work with. Install one for a specific task, or all four for the complete workflow.

The current release is **0.2.0 preview**. It provides four Skills and client guides for Codex, Claude Code, ZCode, Kimi Code, Grok Build, OpenCode, Qoder, CodeBuddy, and Gemini CLI. Installation instructions have been checked against official documentation; claims about operation in real clients are limited to what has actually been verified.

## Start with a request

```text
Hand off the work in this chat to the next agent. Keep the unresolved issues and next steps.
```

```text
This conversation is getting long. Prepare a concise continuation brief, preserving failed tests and missing context.
```

```text
Read this handoff packet, verify the current project, then continue the remaining work.
```

```text
Move this project's Rules, selected Skills, and MCP configuration to another agent. Show me the diff first.
```

For example, hand off work from Kimi Code to ZCode, or move a Grok Build project to OpenCode. Work handoffs use readable packets; configuration transfers begin by checking the format and scope on both sides.

Invoke the chosen Skill by its full name. For example, use `$ccmole-session-handoff` in Codex / ZCode, `/skill:ccmole-session-handoff` in Kimi Code, or `/ccmole-session-handoff` in Claude Code / Grok Build. In OpenCode, ask “Use ccmole-session-handoff to prepare a handoff.” Substitute the other Skill names for different tasks.

## Choose a Skill

| Skill | When to use it | What you get |
|---|---|---|
| [ccmole-session-handoff](skills/ccmole-session-handoff/SKILL.md) | Move work to another agent or chat | A portable packet, full available / selected / compact scope, and supported delivery when authorized |
| [ccmole-context-compact](skills/ccmole-context-compact/SKILL.md) | Shorten a long conversation for later continuation | A lossy but traceable brief preserving corrections, failures, missing context and next steps |
| [ccmole-project-resume](skills/ccmole-project-resume/SKILL.md) | Receive a handoff or continue on another device | Check project and code state, then continue if requested and ready; a check-only request ends with the result |
| [ccmole-config-reuse](skills/ccmole-config-reuse/SKILL.md) | Reuse selected Rules, Skills, MCP or non-secret settings | A plan and diff, followed by authorized application with backups, drift checks and verification |

Each directory includes its own instructions, relevant resources and license. None requires another CCMole Skill. Handoff includes compaction when needed; standalone compaction does not send a packet, create a chat or begin development.

Configuration transfers check scope, format, relative paths, dependencies, and credential references. Source files are preserved, and existing target content is preserved by default. Unknown versions or unverifiable fields receive a preview only. API keys, login tokens, and native session databases are excluded from the transfer.

## Installation

Download [dusthappy/ccmole](https://github.com/dusthappy/ccmole), then choose one or more of the four directories under `skills/`. Copy each **entire Skill directory** into the host's Skill directory, preserving its name and supporting files. Copy all four to install the complete set. The Skills add no CCMole Desktop, Rust, Node.js, database or background-service requirement.

```bash
git clone https://github.com/dusthappy/ccmole.git
```

The table lists destination **parent directories**. Append the chosen Skill's full name, such as `.agents/skills/ccmole-session-handoff/`. Replace `<skill-name>` in commands with that name. Do not nest the whole repository inside a Skill directory.

| Client | Project Skill parent | User Skill parent | Invoke / discover |
|---|---|---|---|
| Codex | `.agents/skills/` | `~/.agents/skills/` | `$<skill-name>` |
| Claude Code | `.claude/skills/` | `~/.claude/skills/` | `/<skill-name>` |
| ZCode built-in agent | `.zcode/skills/` | `~/.zcode/skills/` | Settings → Skills → refresh and enable; `$<skill-name>` |
| Kimi Code CLI / Desktop | `.kimi-code/skills/` | `~/.kimi-code/skills/`, or `$KIMI_CODE_HOME/skills/` | `/skill:<skill-name>` in a new session |
| Grok Build CLI | `.grok/skills/` | `~/.grok/skills/` | `/<skill-name>` |
| OpenCode | `.opencode/skills/` | `~/.config/opencode/skills/` | Ask to use `<skill-name>` in natural language |
| Qoder CLI | `.qoder/skills/` | `~/.qoder/skills/` | `/skills reload`, then `/<skill-name>` |
| CodeBuddy IDE | `.codebuddy/skills/` | Import through Skills in Settings; verify the scope | Confirm it appears in the Skills list, then invoke it in natural language |
| Gemini CLI | `.gemini/skills/` | `~/.gemini/skills/` | `/skills reload` and `/skills list`, then invoke it in natural language |

These are default paths. Check configuration overrides and the installed version on the target machine. The Kimi paths apply to the current Node.js version of Kimi Code; the older Python CLI requires a separate check. Choose only the clients and scopes you need. Check for an existing directory with the same name, and avoid conflicting copies across shared discovery directories.

Before installing, check whether the target already contains a directory with the same name. When updating, back up local changes, then replace the entire directory so outdated references do not remain. Start a new chat after installation and invoke the Skill. To uninstall, remove only the selected installed Skill directories; keep your handoff packets and configuration backups separately.

You can also ask your agent to install it:

```text
Install ccmole-session-handoff and ccmole-project-resume from the CCMole package I downloaded into this project's Skill directory.
Check existing directories, preserve my local changes, and tell me how to invoke each Skill.
```

Each Skill contains its own client guide. See the [handoff guide](skills/ccmole-session-handoff/references/clients.md) for delivery routes or the [configuration client guide](skills/ccmole-config-reuse/references/clients.md) for official sources, Rules / MCP format differences, and verification limits for each client, checked on 2026-10-13. For other hosts that support the [Agent Skills format](https://agentskills.io/specification), verify their installation locations and tool permissions. Format compatibility does not mean every platform has been tested.

**Identify the specific Grok or Kimi product you use.** Grok Bot private Skills, ordinary Grok chat, and Grok Build CLI do not share one installation method. Kimi Code Web is a browser interface for the local CLI, distinct from ordinary Kimi web chat. IDE integrations and importing the complete resource set into Grok Bot still require verification in the target host. In a chat-only environment, paste a self-contained handoff packet; this does not constitute installation of the full Skill.

## Upgrade from 0.1.x

The former `skills/ccmole/` package has been replaced by the four Skills above. Choose the ones you need, preserve local modifications, install them and verify discovery. The old `$ccmole` / `/ccmole` invocation is not an alias for the new Skills.

If the old `ccmole` is still installed, back it up outside the host's Skill discovery directories, then disable or remove it once the replacements are verified. No update script deletes it automatically. Check for collisions with existing Skills bearing any new package's name. Keep generated handoff packets and configuration backups; they are independent of the installed instructions.

## Runtime boundaries

This package contains workflow instructions. Its execution capabilities and permissions come from the host agent. It includes no daemon, network transfer service, or credential store. The host model may still process content you give it.

- Chat-only hosts can organize and receive text context. File verification and configuration changes require host file tools.
- Automatically creating a new chat, sending handoff content, or verifying that the target configuration is active requires supported host tools and user authorization. Manual steps are provided when those tools are unavailable.
- This release does not provide a unified session history index, native session format migration, a desktop interface, automatic background synchronization, a provider proxy, or transaction guarantees across files.
- Writing configuration and confirming that the target agent has loaded it are reported separately.

## Package contents

The four directories under `skills/` are independently installable; references and templates are supporting files, not additional Skills. The repository-level documentation and [verification scenarios](verification/scenarios.md) are for users and maintainers.

This package delivers the Skill workflows independently. It does not mean the existing CCMole Desktop V1 has passed acceptance. See the [verification record](verification/results.md) for `0.2.0` and the earlier `0.1.x` releases.

This collection is available under the [MIT license](LICENSE). Each installable directory includes its own copy.

The product design draws inspiration from [yobiru](https://github.com/chekusu/yobiru)'s scenario-based presentation and gradual onboarding. CCMole's workflows and text were written independently; no code or Skill content was copied.
