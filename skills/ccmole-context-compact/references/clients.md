# Client installation and routing

Official documentation checked on **2026-10-13**. These are documented routes,
not claims of live installation or activation tests. Verify the installed
surface/version before applying configuration; a product family or model name
alone is insufficient. Supporting a desktop host does not require CCMole Desktop.

## Select a route

Identify the source and destination product, surface (CLI, built-in agent,
editor integration, local web UI, or hosted chat), version, machine and scope.
Use already available context; ask only for a distinction that changes the next
action. For an ambiguous “Grok” or “Kimi” request, resolve the surface before
installation or writes. Continue independent preparation within the requested
workflow while that distinction is unresolved.

Copy the **whole `ccmole-context-compact` directory**, including its references and assets, to
one selected destination. Paths below are defaults; respect documented home or
configuration overrides on the target machine. A project path is relative to
that client's project/workspace root. `~` denotes the target user's home.
Do not install into every listed client, overwrite an existing installation,
or enable shared-directory discovery as an implied prerequisite.

## Documented native Skill routes

| Surface | Project directory | User directory | Invocation / discovery |
|---|---|---|---|
| [Codex](https://learn.chatgpt.com/docs/build-skills) | `.agents/skills/ccmole-context-compact/` | `~/.agents/skills/ccmole-context-compact/` | `$ccmole-context-compact`; start a new conversation after installation |
| [Claude Code](https://code.claude.com/docs/en/skills) | `.claude/skills/ccmole-context-compact/` | `~/.claude/skills/ccmole-context-compact/` | `/ccmole-context-compact` |
| [ZCode built-in Agent](https://zcode.z.ai/en/docs/skill) | `.zcode/skills/ccmole-context-compact/` | `~/.zcode/skills/ccmole-context-compact/` | Settings → Skills → Refresh and enable; `$ccmole-context-compact` or the Skills group in `/` |
| [Kimi Code CLI](https://www.kimi.com/code/docs/en/kimi-code-cli/customization/skills.html) | `.kimi-code/skills/ccmole-context-compact/` | `$KIMI_CODE_HOME/skills/ccmole-context-compact/`, default `~/.kimi-code/skills/ccmole-context-compact/` | New session, then `/skill:ccmole-context-compact` followed by the request |
| [Kimi Code Desktop](https://www.kimi.com/code/docs/en/kimi-code-desktop/settings-and-extensions.html) | Same as Kimi Code CLI | Same as Kimi Code CLI | Same Skill discovery; `/` menu or `/skill:ccmole-context-compact` |
| [Grok Build CLI](https://github.com/xai-org/grok-build/blob/main/crates/codegen/xai-grok-pager/docs/user-guide/08-skills.md) | `.grok/skills/ccmole-context-compact/` | `~/.grok/skills/ccmole-context-compact/` | `/ccmole-context-compact`; documented inspection: `grok inspect --json` |
| [OpenCode](https://opencode.ai/docs/skills/) | `.opencode/skills/ccmole-context-compact/` | `~/.config/opencode/skills/ccmole-context-compact/` | Ask the agent to use `ccmole-context-compact`; it loads it through the native `skill` tool |
| [Qoder CLI](https://docs.qoder.com/cli/Skills) | `.qoder/skills/ccmole-context-compact/` | `~/.qoder/skills/ccmole-context-compact/` | `/skills reload`, inspect `/skills`, then `/ccmole-context-compact` |
| [CodeBuddy IDE](https://www.codebuddy.ai/docs/ide/Features/Skills) | `.codebuddy/skills/ccmole-context-compact/` | Use the documented Settings → Skills import UI; verify its chosen scope | Inspect the Skills list, then ask the agent to use `ccmole-context-compact` |
| [Gemini CLI](https://geminicli.com/docs/cli/using-agent-skills/) | `.gemini/skills/ccmole-context-compact/` | `~/.gemini/skills/ccmole-context-compact/` | `/skills reload`, `/skills list`, then ask to use `ccmole-context-compact` |

ZCode's project location is also documented in its [FAQ](https://zcode.z.ai/en/docs/qa).
The Kimi paths above apply to the current Node.js CLI documented by Kimi;
legacy Python CLI installations need their own version-matched documentation,
not a blind move from `~/.kimi/`. See the [Kimi migration overview](https://www.kimi.com/code/docs/en/).

Some clients also discover `.agents/skills` or `.claude/skills`. Prefer the
selected client's native route when isolation matters, and inspect existing
same-name definitions before adding a copy. In Qoder CLI a user definition can
override the project definition. In OpenCode a disabled `skill` tool or Skill
permission can prevent loading; this package does not enable its optional slash
metadata, so do not promise `/ccmole-context-compact` there. Discovery is not proof that the
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

## Report the observed level

Distinguish documentation checked, files installed, Skill discovered, workflow
exercised and configuration activated. Name the exact client/surface/version
and remaining limitations. Read-only discovery should be scoped and its output
redacted; an inspection command is not permission to start servers or disclose
all configuration. Apply no configuration or runtime change during routing.

Client routing does not broaden this Skill's task. Prepare only the requested
output; installation, delivery, continuation and configuration changes each
remain subject to the workflow and authorization in this package.
