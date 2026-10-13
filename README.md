# CCMole Skill

English | [简体中文](README.zh-CN.md)

**Switch agents and keep working. Switch tools and bring the configuration you need.**

CCMole is an installable Agent Skill that helps you organize development context, resume work, and reuse selected Rules, Skills, MCP, and non-secret settings across agents. Use it directly in the agent you already work with.

The current release is **0.1.1 preview**. It provides two workflows and client guides for Codex, Claude Code, ZCode, Kimi Code, Grok Build, OpenCode, Qoder, CodeBuddy, and Gemini CLI. Installation instructions have been checked against official documentation; claims about operation in real clients are limited to what has actually been verified.

## Start with a request

```text
Hand off the work in this chat to the next agent. Keep the unresolved issues and next steps.
```

```text
Read this handoff packet, verify the current project, then continue the remaining work.
```

```text
Move this project's Rules, selected Skills, and MCP configuration to another agent. Show me the diff first.
```

For example, hand off work from Kimi Code to ZCode, or move a Grok Build project to OpenCode. Work handoffs use readable packets; configuration transfers begin by checking the format and scope on both sides.

Use `$ccmole` in Codex / ZCode, `/skill:ccmole` in Kimi Code, or `/ccmole` in Claude Code / Grok Build. In OpenCode, ask “Use ccmole to help me hand off my current work.” See the table below for each client's entry point.

## Two workflows

| Workflow | What you get |
|---|---|
| Context handoff | A Markdown packet with goals, decisions, project state, failed attempts, and next steps; supports all available context, a selected scope, or lossy compaction |
| Receive and resume | As part of a handoff, check the project, branch, commit, and uncommitted changes; continue when they match, or report specific differences |
| Configuration reuse | A transfer plan and diff for selected Rules, Skills, MCP, and non-secret settings; after authorization, apply them through supported target mechanisms, verify the result, and retain recovery information |

Configuration transfers check scope, format, relative paths, dependencies, and credential references. Source files are preserved, and existing target content is preserved by default. Unknown versions or unverifiable fields receive a preview only. API keys, login tokens, and native session databases are excluded from the transfer.

## Installation

Download [dusthappy/ccmole](https://github.com/dusthappy/ccmole), then copy the **entire `skills/ccmole` directory** into your host's Skill directory. Keep all supporting files together. The Skill does not require installing CCMole Desktop, Rust, Node.js, a database, or a background service.

```bash
git clone https://github.com/dusthappy/ccmole.git
```

| Client | Current project only | All projects for the current user | Invoke / discover |
|---|---|---|---|
| Codex | `.agents/skills/ccmole/` | `~/.agents/skills/ccmole/` | `$ccmole` |
| Claude Code | `.claude/skills/ccmole/` | `~/.claude/skills/ccmole/` | `/ccmole` |
| ZCode built-in agent | `.zcode/skills/ccmole/` | `~/.zcode/skills/ccmole/` | Settings → Skills → refresh and enable; `$ccmole` |
| Kimi Code CLI / Desktop | `.kimi-code/skills/ccmole/` | `~/.kimi-code/skills/ccmole/`, or `$KIMI_CODE_HOME/skills/ccmole/` | `/skill:ccmole` in a new session |
| Grok Build CLI | `.grok/skills/ccmole/` | `~/.grok/skills/ccmole/` | `/ccmole` |
| OpenCode | `.opencode/skills/ccmole/` | `~/.config/opencode/skills/ccmole/` | Ask to use `ccmole` in natural language |
| Qoder CLI | `.qoder/skills/ccmole/` | `~/.qoder/skills/ccmole/` | `/skills reload`, then `/ccmole` |
| CodeBuddy IDE | `.codebuddy/skills/ccmole/` | Import through Skills in Settings; verify the scope | Confirm it appears in the Skills list, then invoke it in natural language |
| Gemini CLI | `.gemini/skills/ccmole/` | `~/.gemini/skills/ccmole/` | `/skills reload` and `/skills list`, then invoke it in natural language |

These are default paths. Check configuration overrides and the installed version on the target machine. The Kimi paths apply to the current Node.js version of Kimi Code; the older Python CLI requires a separate check. Choose only the clients and scopes you need. Check for an existing directory with the same name, and avoid conflicting copies across shared discovery directories.

Before installing, check whether the target already contains a directory with the same name. When updating, back up local changes, then replace the entire directory so outdated references do not remain. Start a new chat after installation and invoke the Skill. To uninstall, remove only the installed `ccmole` directory; keep your handoff packets and configuration backups separately.

You can also ask your agent to install it:

```text
Install skills/ccmole from the CCMole release package I downloaded into this project's Skill directory.
Check for an existing directory with the same name and preserve my local changes. Tell me how to invoke it afterward.
```

See the [client guide](skills/ccmole/references/clients.md) for official sources, Rules / MCP format differences, and verification limits for each client, checked on 2026-10-13. For other hosts that support the [Agent Skills format](https://agentskills.io/specification), verify their installation locations and tool permissions. Format compatibility does not mean every platform has been tested.

**Identify the specific Grok or Kimi product you use.** Grok Bot private Skills, ordinary Grok chat, and Grok Build CLI do not share one installation method. Kimi Code Web is a browser interface for the local CLI, distinct from ordinary Kimi web chat. IDE integrations and importing the complete resource set into Grok Bot still require verification in the target host. In a chat-only environment, paste a self-contained handoff packet; this does not constitute installation of the full Skill.

## Runtime boundaries

This package contains workflow instructions. Its execution capabilities and permissions come from the host agent. It includes no daemon, network transfer service, or credential store. The host model may still process content you give it.

- Chat-only hosts can organize and receive text context. File verification and configuration changes require host file tools.
- Automatically creating a new chat, sending handoff content, or verifying that the target configuration is active requires supported host tools and user authorization. Manual steps are provided when those tools are unavailable.
- This release does not provide a unified session history index, native session format migration, a desktop interface, automatic background synchronization, a provider proxy, or transaction guarantees across files.
- Writing configuration and confirming that the target agent has loaded it are reported separately.

## Package contents

`skills/ccmole/` is the only directory you need to install. The repository-level documentation and [verification scenarios](verification/scenarios.md) are for users and maintainers.

This package delivers the Skill workflows independently. It does not mean the existing CCMole Desktop V1 has passed acceptance. See the [verification record](verification/results.md) for the current `0.1.1` release and the earlier `0.1.0` release.

This standalone package is available under the [MIT license](LICENSE).

The product design draws inspiration from [yobiru](https://github.com/chekusu/yobiru)'s scenario-based presentation and gradual onboarding. CCMole's workflows and text were written independently; no code or Skill content was copied.
