# Client installation and routing

Official documentation checked on **2026-10-13**. These are documented routes,
not claims of live installation or activation tests. Verify the installed
surface/version before applying configuration; a product family or model name
alone is insufficient. Supporting a desktop host does not require CCMole Desktop.

## Select a route

Identify the source and destination product, surface (CLI, built-in agent,
editor integration, local web UI, or hosted chat), version, machine and scope.
Use already available context; ask only for a distinction that changes the next
action. For an ambiguous “Grok” or “Kimi” request, prepare a target-neutral
handoff immediately, but resolve the surface before installation or writes.

Copy the **whole `ccmole` directory**, including its references and assets, to
one selected destination. Paths below are defaults; respect documented home or
configuration overrides on the target machine. A project path is relative to
that client's project/workspace root. `~` denotes the target user's home.
Do not install into every listed client, overwrite an existing installation,
or enable shared-directory discovery as an implied prerequisite.

## Documented native Skill routes

| Surface | Project directory | User directory | Invocation / discovery |
|---|---|---|---|
| [Codex](https://learn.chatgpt.com/docs/build-skills) | `.agents/skills/ccmole/` | `~/.agents/skills/ccmole/` | `$ccmole`; start a new conversation after installation |
| [Claude Code](https://code.claude.com/docs/en/skills) | `.claude/skills/ccmole/` | `~/.claude/skills/ccmole/` | `/ccmole` |
| [ZCode built-in Agent](https://zcode.z.ai/en/docs/skill) | `.zcode/skills/ccmole/` | `~/.zcode/skills/ccmole/` | Settings → Skills → Refresh and enable; `$ccmole` or the Skills group in `/` |
| [Kimi Code CLI](https://www.kimi.com/code/docs/en/kimi-code-cli/customization/skills.html) | `.kimi-code/skills/ccmole/` | `$KIMI_CODE_HOME/skills/ccmole/`, default `~/.kimi-code/skills/ccmole/` | New session, then `/skill:ccmole` followed by the request |
| [Kimi Code Desktop](https://www.kimi.com/code/docs/en/kimi-code-desktop/settings-and-extensions.html) | Same as Kimi Code CLI | Same as Kimi Code CLI | Same Skill discovery; `/` menu or `/skill:ccmole` |
| [Grok Build CLI](https://github.com/xai-org/grok-build/blob/main/crates/codegen/xai-grok-pager/docs/user-guide/08-skills.md) | `.grok/skills/ccmole/` | `~/.grok/skills/ccmole/` | `/ccmole`; documented inspection: `grok inspect --json` |
| [OpenCode](https://opencode.ai/docs/skills/) | `.opencode/skills/ccmole/` | `~/.config/opencode/skills/ccmole/` | Ask the agent to use `ccmole`; it loads it through the native `skill` tool |
| [Qoder CLI](https://docs.qoder.com/cli/Skills) | `.qoder/skills/ccmole/` | `~/.qoder/skills/ccmole/` | `/skills reload`, inspect `/skills`, then `/ccmole` |
| [CodeBuddy IDE](https://www.codebuddy.ai/docs/ide/Features/Skills) | `.codebuddy/skills/ccmole/` | Use the documented Settings → Skills import UI; verify its chosen scope | Inspect the Skills list, then ask the agent to use `ccmole` |
| [Gemini CLI](https://geminicli.com/docs/cli/using-agent-skills/) | `.gemini/skills/ccmole/` | `~/.gemini/skills/ccmole/` | `/skills reload`, `/skills list`, then ask to use `ccmole` |

ZCode's project location is also documented in its [FAQ](https://zcode.z.ai/en/docs/qa).
The Kimi paths above apply to the current Node.js CLI documented by Kimi;
legacy Python CLI installations need their own version-matched documentation,
not a blind move from `~/.kimi/`. See the [Kimi migration overview](https://www.kimi.com/code/docs/en/).

Some clients also discover `.agents/skills` or `.claude/skills`. Prefer the
selected client's native route when isolation matters, and inspect existing
same-name definitions before adding a copy. In Qoder CLI a user definition can
override the project definition. In OpenCode a disabled `skill` tool or Skill
permission can prevent loading; this package does not enable its optional slash
metadata, so do not promise `/ccmole` there. Discovery is not proof that the
workflow has run successfully.

## Surfaces that need an additional check

| Surface | Supported next step and limit |
|---|---|
| [Kimi Code IDE / ACP](https://www.kimi.com/code/docs/en/kimi-code-cli/guides/ides.html) | Identify the CLI executable and version used by the IDE. Verify its Skill discovery and command forwarding; do not assume all IDE menus match the CLI. |
| [Kimi Code for VSCode](https://www.kimi.com/code/docs/en/kimi-code-for-vscode/configuration.html) | Check the bundled or overridden CLI and extension version. Its separate configuration is not evidence that every CLI Skill route is exposed. Verify discovery in that host before claiming installation. |
| [Kimi Code Web](https://www.kimi.com/code/docs/en/kimi-code-cli/guides/web.html) | This is the local UI started by `kimi web`, sharing CLI state. Verify Skill access in its supported command subset. It is distinct from ordinary Kimi web chat. |
| [Grok Bot](https://cursor.com/docs/grok-bot/work) | Official docs describe saving a workflow as a private skill and selecting it with `/`. Verify the host can import or retain this package's supporting resources before claiming CCMole is installed. No local `.grok/skills` route is established for this surface. |
| Ordinary Kimi / Grok web or mobile chat, or an unknown client | Provide a self-contained Markdown handoff and receiving prompt for paste/upload. Do not claim standard Skill installation, local file access, configuration application or native chat creation without evidence. |

If the host cannot retain referenced files, handing it only `SKILL.md` breaks
this package. Instead provide the completed, self-contained handoff or a
self-contained excerpt for the requested workflow, and label it manual use.
Do not call that a verified package installation. Remote/cloud execution does
not imply access to the user's local checkout; transfer only selected,
authorized artifacts through supported tools.

## Rules and MCP mapping anchors

These anchors identify what to inspect. They are **not ready-made conversion
templates**. Follow [config-reuse.md](config-reuse.md) for version evidence,
scope, exact diff, authorization, backups, drift checks and verification.
Never copy a source MCP object wholesale just because both clients accept JSON.

| Target | Rules anchors | MCP anchors and migration implications |
|---|---|---|
| ZCode Agent | Workspace `AGENTS.md`; user `~/.zcode/AGENTS.md`. Do not assume recursive nested-rule merging. | User `~/.zcode/cli/config.json`, project `.zcode/config.json`, under `mcp.servers`. Its compatibility `.agents/mcp.json` uses a different `mcpServers` layout; select one actual route. |
| Kimi Code CLI | Project `.kimi-code/AGENTS.md` or `AGENTS.md`; user `$KIMI_CODE_HOME/AGENTS.md`. Check precedence. | Project `.kimi-code/mcp.json`, user `$KIMI_CODE_HOME/mcp.json`, with `mcpServers`. Resolve the home override and current version. Desktop shares the documented MCP locations. |
| Grok Build CLI | Project `AGENTS.md` and `.grok/rules/*.md`; user `$GROK_HOME/rules/`. Project trust affects loading. | User `~/.grok/config.toml`, project `.grok/config.toml`, `[mcp_servers.<name>]`. Same-name project entries replace the user entry, not individual fields. A scope change can discard inherited settings. |
| OpenCode | Project `AGENTS.md`, user `~/.config/opencode/AGENTS.md`; additional files may be listed in `instructions`. | Project `opencode.json` / JSONC, user `~/.config/opencode/opencode.json`; `mcp.<name>`. Local entries use `type: "local"` and a command array; remote entries use `type: "remote"`. Do not retain another host's `mcpServers` wrapper. |

Sources: ZCode [Rules](https://zcode.z.ai/en/docs/agents) and [MCP](https://zcode.z.ai/en/docs/mcp-services);
Kimi [Rules](https://www.kimi.com/code/docs/en/kimi-code-cli/customization/agents.html) and [MCP](https://www.kimi.com/code/docs/en/kimi-code-cli/customization/mcp.html);
Grok Build [Rules](https://github.com/xai-org/grok-build/blob/main/crates/codegen/xai-grok-pager/docs/user-guide/12-project-rules.md) and [MCP](https://github.com/xai-org/grok-build/blob/main/crates/codegen/xai-grok-pager/docs/user-guide/07-mcp-servers.md);
OpenCode [Rules](https://opencode.ai/docs/rules/), [configuration](https://opencode.ai/docs/config/) and [MCP](https://opencode.ai/docs/mcp-servers/).

Verify transports, environment-reference syntax, working directories, trust and
activation separately. For other clients or provider settings, consult current
official version-matched documentation before proposing field mappings.
Supporting a client's Skill format does not prove its Rules, MCP, provider
settings or native sessions are interchangeable with another client's.

## Report the observed level

Distinguish documentation checked, files installed, Skill discovered, workflow
exercised and configuration activated. Name the exact client/surface/version
and remaining limitations. Read-only discovery should be scoped and its output
redacted; an inspection command is not permission to start servers or disclose
all configuration. Apply no configuration or runtime change during routing.
