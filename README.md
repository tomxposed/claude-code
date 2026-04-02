# Claude Code Best V3 (CCB)

An unofficial project that decompiles/reverse-engineers the source code of the official [Claude Code](https://docs.anthropic.com/en/docs/claude-code) CLI tool by "Prisoner A" (Anthropic). The goal is to reproduce most of the functionalities and engineering capabilities of Claude Code (if you must ask, it's because the "Lafayette" has already paid). Although it's hard not to laugh, it's called CCB (Cai Cai Bei)...

[Documentation is here, PR contributions are welcome](https://ccb.agent-aura.top/)

Sponsor Placeholder

- [x] v1 will complete the basic run and pass basic type checking;
- [x] V2 will completely implement engineering supporting facilities;
  - [ ] Biome formatting might not be implemented first to avoid code conflicts
  - [x] Build pipeline completed, artifacts can run on both Node and Bun
- [x] V3 will write extensive documentation and improve the documentation site
- [ ] V4 will complete a large number of test files to improve stability
- [ ] V5 massive refactoring of the "shit mountain" code, comprehensive modular sub-packaging
  - [ ] V5 will be a brand new branch, the main branch will be archived as a historical version then

> I don't know how long this project will exist, Star + Fork + git clone + .zip package is the most robust way; frankly speaking, it's a flag-bearing project to see how far it can go
>
> This project updates very fast, there is Opus continuously optimizing in the background, new changes happen almost every few hours;
>
> Claude API cost has burned over $1000, out of money, switching to GLM to continue playing;

Survival records:

1. 48 hours after open source: exceeded 7k Stars; tests have achieved some success;
2. 24 hours after open source: exceeded 6k Stars, thanks everyone for the support. Completed the docs site build, reached v3 version, will start test cases maintenance, PRs will be accepted after completion; It seems Anthropic doesn't want to deal with us;
3. 15 hours after open source: completed Node support for build artifacts, it is in its ultimate form now; stars are almost at 3k; waiting for Anthropic's email
4. 12 hours after open source: April Fools' Day, stars broke 1k, and Anthropic didn't send an email to take down this project

## Quick Start

### Prerequisites

You MUST use the latest version of bun, otherwise there will be a bunch of weird BUGs!!! bun upgrade!!!

- [Bun](https://bun.sh/) >= 1.3.11
- Standard ways to configure CC, major providers have their own configuration methods

### Install

```bash
bun install
```

### Run

```bash
# Development mode, seeing version 888 means it's correct
bun run dev

# Build
bun run build
```

Build uses code splitting multi-file bundling (`build.ts`), artifacts output to the `dist/` directory (entry `dist/cli.js` + about 450 chunk files).

The built version can be started with both bun and node, you can publish to a private registry and start directly.

If you encounter bugs, please submit an issue directly, we will prioritize resolving them.

## Related Documentation and Websites

<https://deepwiki.com/claude-code-best/claude-code>

## Star History

<a href="https://www.star-history.com/?repos=claude-code-best%2Fclaude-code&type=date&legend=top-left">
 <picture>
   <source media="(prefers-color-scheme: dark)" srcset="https://api.star-history.com/image?repos=claude-code-best/claude-code&type=date&theme=dark&legend=top-left" />
   <source media="(prefers-color-scheme: light)" srcset="https://api.star-history.com/image?repos=claude-code-best/claude-code&type=date&legend=top-left" />
   <img alt="Star History Chart" src="https://api.star-history.com/image?repos=claude-code-best/claude-code&type=date&legend=top-left" />
 </picture>
</a>

## Feature List

> ✅ = Implemented  ⚠️ = Partially implemented / Conditionally enabled  ❌ = stub / Removed / Feature flag disabled

### Core System

| Feature | Status | Description |
|------|------|------|
| REPL Interactive Interface (Ink terminal rendering) | ✅ | Main screen 5000+ lines, complete interaction |
| API Communication — Anthropic Direct | ✅ | Supports API Key + OAuth |
| API Communication — AWS Bedrock | ✅ | Supports credential refresh, Bearer Token |
| API Communication — Google Vertex | ✅ | Supports GCP credential refresh |
| API Communication — Azure Foundry | ✅ | Supports API Key + Azure AD |
| Streaming dialogue and tool call loop (`query.ts`) | ✅ | 1700+ lines, includes auto compaction, token tracking |
| Session Engine (`QueryEngine.ts`) | ✅ | 1300+ lines, manages dialogue state and attribution |
| Context Building (git status / CLAUDE.md / memory) | ✅ | completely implemented in `context.ts` |
| Permission System (plan/auto/manual modes) | ✅ | 6300+ lines, includes YOLO classifier, path validation, rule matching |
| Hook System (pre/post tool use) | ✅ | Supports settings.json configuration |
| Session Resume (`/resume`) | ✅ | Independent ResumeConversation screen |
| Doctor Diagnostics (`/doctor`) | ✅ | Version, API, Plugin, Sandbox checks |
| Auto Compaction | ✅ | auto-compact / micro-compact / API compact |

### Tools — Always Available

| Tool | Status | Description |
|------|------|------|
| BashTool | ✅ | Shell execution, sandbox, permission checks |
| FileReadTool | ✅ | File / PDF / Image / Notebook reading |
| FileEditTool | ✅ | String-replacement editing + diff tracking |
| FileWriteTool | ✅ | File creation / overwrite + diff generation |
| NotebookEditTool | ✅ | Jupyter Notebook cell editing |
| AgentTool | ✅ | Sub-agent derivation (fork / async / background / remote) |
| WebFetchTool | ✅ | URL fetching → Markdown → AI summary |
| WebSearchTool | ✅ | Web search + domain filtering |
| AskUserQuestionTool | ✅ | Multi-question interactive prompt + preview |
| SendMessageTool | ✅ | Message sending (peers / teammates / mailbox) |
| SkillTool | ✅ | Slash commands / Skill invocation |
| EnterPlanModeTool | ✅ | Enter plan mode |
| ExitPlanModeTool (V2) | ✅ | Exit plan mode |
| TodoWriteTool | ✅ | Todo list v1 |
| BriefTool | ✅ | Brief message + attachment sending |
| TaskOutputTool | ✅ | Background task output reading |
| TaskStopTool | ✅ | Background task stopping |
| ListMcpResourcesTool | ⚠️ | MCP resources list (filtered by specialTools, added under specific conditions) |
| ReadMcpResourceTool | ⚠️ | MCP resource read (same as above) |
| SyntheticOutputTool | ⚠️ | Only created in non-interactive sessions (SDK/pipe mode) |
| CronCreateTool | ✅ | Scheduled task creation (AGENT_TRIGGERS gate removed) |
| CronDeleteTool | ✅ | Scheduled task deletion |
| CronListTool | ✅ | Scheduled task list |
| EnterWorktreeTool | ✅ | Enter Git Worktree (`isWorktreeModeEnabled()` currently hardcoded to true) |
| ExitWorktreeTool | ✅ | Exit Git Worktree |

### Tools — Conditionally Enabled

| Tool | Status | Enable Condition |
|------|------|----------|
| GlobTool | ✅ | Enabled when bfs/ugrep is not embedded (default enabled) |
| GrepTool | ✅ | Same as above |
| TaskCreateTool | ⚠️ | When `isTodoV2Enabled()` is true |
| TaskGetTool | ⚠️ | Same as above |
| TaskUpdateTool | ⚠️ | Same as above |
| TaskListTool | ⚠️ | Same as above |
| TeamCreateTool | ⚠️ | `isAgentSwarmsEnabled()` |
| TeamDeleteTool | ⚠️ | Same as above |
| ToolSearchTool | ⚠️ | `isToolSearchEnabledOptimistic()` |
| PowerShellTool | ⚠️ | Windows platform detection |
| LSPTool | ⚠️ | `ENABLE_LSP_TOOL` environment variable |
| ConfigTool | ❌ | `USER_TYPE === 'ant'` (always false) |

### Tools — Feature Flag Disabled (All Unavailable)

| Tool | Feature Flag |
|------|-------------|
| SleepTool | `PROACTIVE` / `KAIROS` |
| RemoteTriggerTool | `AGENT_TRIGGERS_REMOTE` |
| MonitorTool | `MONITOR_TOOL` |
| SendUserFileTool | `KAIROS` |
| OverflowTestTool | `OVERFLOW_TEST_TOOL` |
| TerminalCaptureTool | `TERMINAL_PANEL` |
| WebBrowserTool | `WEB_BROWSER_TOOL` |
| SnipTool | `HISTORY_SNIP` |
| WorkflowTool | `WORKFLOW_SCRIPTS` |
| PushNotificationTool | `KAIROS` / `KAIROS_PUSH_NOTIFICATION` |
| SubscribePRTool | `KAIROS_GITHUB_WEBHOOKS` |
| ListPeersTool | `UDS_INBOX` |
| CtxInspectTool | `CONTEXT_COLLAPSE` |

### Tools — Stub / Unavailable

| Tool | Description |
|------|------|
| TungstenTool | ANT-ONLY stub |
| REPLTool | ANT-ONLY, `isEnabled: () => false` |
| SuggestBackgroundPRTool | ANT-ONLY, `isEnabled: () => false` |
| VerifyPlanExecutionTool | Requires `CLAUDE_CODE_VERIFY_PLAN=true` environment variable, and is a stub |
| ReviewArtifactTool | stub, not registered in tools.ts |
| DiscoverSkillsTool | stub, not registered in tools.ts |

### Slash Commands — Available

| Command | Status | Description |
|------|------|------|
| `/add-dir` | ✅ | Add directory |
| `/advisor` | ✅ | Advisor configuration |
| `/agents` | ✅ | Agent list/management |
| `/branch` | ✅ | Branch management |
| `/btw` | ✅ | Quick notes |
| `/chrome` | ✅ | Chrome integration |
| `/clear` | ✅ | Clear screen |
| `/color` | ✅ | Agent color |
| `/compact` | ✅ | Compact conversation |
| `/config` (`/settings`) | ✅ | Configuration management |
| `/context` | ✅ | Context information |
| `/copy` | ✅ | Copy last message |
| `/cost` | ✅ | Session cost |
| `/desktop` | ✅ | Claude Desktop integration |
| `/diff` | ✅ | Show diff |
| `/doctor` | ✅ | Health check |
| `/effort` | ✅ | Set effort level |
| `/exit` | ✅ | Exit |
| `/export` | ✅ | Export conversation |
| `/extra-usage` | ✅ | Extra usage information |
| `/fast` | ✅ | Toggle fast mode |
| `/feedback` | ✅ | Feedback |
| `/loop` | ✅ | Scheduled loop execution (bundled skill, can be disabled via `CLAUDE_CODE_DISABLE_CRON`) |
| `/heapdump` | ✅ | Heap dump (debugging) |
| `/help` | ✅ | Help |
| `/hooks` | ✅ | Hook management |
| `/ide` | ✅ | IDE connection |
| `/init` | ✅ | Initialize project |
| `/install-github-app` | ✅ | Install GitHub App |
| `/install-slack-app` | ✅ | Install Slack App |
| `/keybindings` | ✅ | Keybindings management |
| `/login` / `/logout` | ✅ | Login / Logout |
| `/mcp` | ✅ | MCP service management |
| `/memory` | ✅ | Memory / CLAUDE.md management |
| `/mobile` | ✅ | Mobile QR code |
| `/model` | ✅ | Model selection |
| `/output-style` | ✅ | Output style |
| `/passes` | ✅ | Referral passes |
| `/permissions` | ✅ | Permissions management |
| `/plan` | ✅ | Plan mode |
| `/plugin` | ✅ | Plugin management |
| `/pr-comments` | ✅ | PR comments |
| `/privacy-settings` | ✅ | Privacy settings |
| `/rate-limit-options` | ✅ | Rate limit options |
| `/release-notes` | ✅ | Release notes |
| `/reload-plugins` | ✅ | Reload plugins |
| `/remote-env` | ✅ | Remote environment configuration |
| `/rename` | ✅ | Rename session |
| `/resume` | ✅ | Resume session |
| `/review` | ✅ | Code review (local) |
| `/ultrareview` | ✅ | Cloud review |
| `/rewind` | ✅ | Rewind conversation |
| `/sandbox-toggle` | ✅ | Toggle sandbox |
| `/security-review` | ✅ | Security review |
| `/session` | ✅ | Session info |
| `/skills` | ✅ | Skill management |
| `/stats` | ✅ | Session stats |
| `/status` | ✅ | Status info |
| `/statusline` | ✅ | Status line UI |
| `/stickers` | ✅ | Stickers |
| `/tasks` | ✅ | Task management |
| `/theme` | ✅ | Terminal theme |
| `/think-back` | ✅ | Year-in-review / Think back |
| `/upgrade` | ✅ | Upgrade CLI |
| `/usage` | ✅ | Usage info |
| `/insights` | ✅ | Usage insights |
| `/vim` | ✅ | Vim mode |

### Slash Commands — Feature Flag Disabled

| Command | Feature Flag |
|------|-------------|
| `/voice` | `VOICE_MODE` |
| `/proactive` | `PROACTIVE` / `KAIROS` |
| `/brief` | `KAIROS` / `KAIROS_BRIEF` |
| `/assistant` | `KAIROS` |
| `/remote-control` (alias `rc`) | `BRIDGE_MODE` |
| `/remote-control-server` | `DAEMON` + `BRIDGE_MODE` |
| `/force-snip` | `HISTORY_SNIP` |
| `/workflows` | `WORKFLOW_SCRIPTS` |
| `/web-setup` | `CCR_REMOTE_SETUP` |
| `/subscribe-pr` | `KAIROS_GITHUB_WEBHOOKS` |
| `/ultraplan` | `ULTRAPLAN` |
| `/torch` | `TORCH` |
| `/peers` | `UDS_INBOX` |
| `/fork` | `FORK_SUBAGENT` |
| `/buddy` | `BUDDY` |

### Slash Commands — ANT-ONLY (Unavailable)

`/files` `/tag` `/backfill-sessions` `/break-cache` `/bughunter` `/commit` `/commit-push-pr` `/ctx_viz` `/good-claude` `/issue` `/init-verifiers` `/mock-limits` `/bridge-kick` `/version` `/reset-limits` `/onboarding` `/share` `/summary` `/teleport` `/ant-trace` `/perf-issue` `/env` `/oauth-refresh` `/debug-tool-call` `/agents-platform` `/autofix-pr`

### CLI Subcommands

| Subcommand | Status | Description |
|--------|------|------|
| `claude` (default) | ✅ | Main REPL / Interactive / print mode |
| `claude mcp serve/add/remove/list/get/...` | ✅ | MCP service management (7 subcommands) |
| `claude auth login/status/logout` | ✅ | Auth management |
| `claude plugin validate/list/install/...` | ✅ | Plugin management (7 subcommands) |
| `claude setup-token` | ✅ | Long-lived Token setup |
| `claude agents` | ✅ | Agents list |
| `claude doctor` | ✅ | Health check |
| `claude update` / `upgrade` | ✅ | Auto update |
| `claude install [target]` | ✅ | Native installation |
| `claude server` | ❌ | `DIRECT_CONNECT` flag |
| `claude ssh <host>` | ❌ | `SSH_REMOTE` flag |
| `claude open <cc-url>` | ❌ | `DIRECT_CONNECT` flag |
| `claude auto-mode` | ❌ | `TRANSCRIPT_CLASSIFIER` flag |
| `claude remote-control` | ❌ | `BRIDGE_MODE` + `DAEMON` flag |
| `claude assistant` | ❌ | `KAIROS` flag |
| `claude up/rollback/log/error/export/task/completion` | ❌ | ANT-ONLY |

### Service Layer

| Service | Status | Description |
|------|------|------|
| API Client (`services/api/`) | ✅ | 3400+ lines, 4 providers |
| MCP (`services/mcp/`) | ✅ | 34 files, 12000+ lines |
| OAuth (`services/oauth/`) | ✅ | Full OAuth flow |
| Plugins (`services/plugins/`) | ✅ | Complete infrastructure, no built-in plugins |
| LSP (`services/lsp/`) | ⚠️ | Implementation exists, disabled by default |
| Compaction (`services/compact/`) | ✅ | auto / micro / API compaction |
| Hook System (`services/tools/toolHooks.ts`) | ✅ | pre/post tool use hooks |
| Session Memory (`services/SessionMemory/`) | ✅ | Session memory management |
| Memory Extraction (`services/extractMemories/`) | ✅ | Automatic memory extraction |
| Skill Search (`services/skillSearch/`) | ✅ | Local/remote skill search |
| Policy Limits (`services/policyLimits/`) | ✅ | Policy limit enforcement |
| Analytics / GrowthBook / Sentry | ⚠️ | Framework exists, actual sink is empty |
| Voice (`services/voice.ts`) | ❌ | `VOICE_MODE` flag disabled |

### Internal Packages (`packages/`)

| Package | Status | Description |
|------|------|------|
| `color-diff-napi` | ✅ | 1006 lines full TypeScript implementation (syntax highlighted diff) |
| `audio-capture-napi` | ✅ | 151 lines full implementation (cross-platform audio recording, uses SoX/arecord) |
| `image-processor-napi` | ✅ | 125 lines full implementation (macOS clipboard image reading, uses osascript + sharp) |
| `modifiers-napi` | ✅ | 67 lines full implementation (macOS modifier key detection, bun:ffi + CoreGraphics) |
| `url-handler-napi` | ❌ | stub, `waitForUrlEvent()` returns null |
| `@ant/claude-for-chrome-mcp` | ❌ | stub, `createServer()` returns null |
| `@ant/computer-use-mcp` | ⚠️ | Type-safe stub (265 lines, complete type definitions but functions return empty values) |
| `@ant/computer-use-input` | ✅ | 183 lines full implementation (macOS keyboard/mouse simulation, AppleScript/JXA/CGEvent) |
| `@ant/computer-use-swift` | ✅ | 388 lines full implementation (macOS display/app management/screenshots, JXA/screencapture) |

### Feature Flags (31, all return `false`)

`ABLATION_BASELINE` `AGENT_MEMORY_SNAPSHOT` `BG_SESSIONS` `BRIDGE_MODE` `BUDDY` `CCR_MIRROR` `CCR_REMOTE_SETUP` `CHICAGO_MCP` `COORDINATOR_MODE` `DAEMON` `DIRECT_CONNECT` `EXPERIMENTAL_SKILL_SEARCH` `FORK_SUBAGENT` `HARD_FAIL` `HISTORY_SNIP` `KAIROS` `KAIROS_BRIEF` `KAIROS_CHANNELS` `KAIROS_GITHUB_WEBHOOKS` `LODESTONE` `MCP_SKILLS` `PROACTIVE` `SSH_REMOTE` `TORCH` `TRANSCRIPT_CLASSIFIER` `UDS_INBOX` `ULTRAPLAN` `UPLOAD_USER_SETTINGS` `VOICE_MODE` `WEB_BROWSER_TOOL` `WORKFLOW_SCRIPTS`

## Project Structure

```
claude-code/
├── src/
│   ├── entrypoints/
│   │   ├── cli.tsx          # Entry file (includes MACRO/feature polyfill)
│   │   └── sdk/             # SDK submodule stub
│   ├── main.tsx             # Main CLI logic (Commander definition)
│   └── types/
│       ├── global.d.ts      # Global variable/macro declarations
│       └── internal-modules.d.ts  # Internal npm package type declarations
├── packages/                # Monorepo workspace packages
│   ├── color-diff-napi/     # Full implementation (terminal color diff)
│   ├── modifiers-napi/      # stub (macOS modifier key detection)
│   ├── audio-capture-napi/  # stub
│   ├── image-processor-napi/# stub
│   ├── url-handler-napi/    # stub
│   └── @ant/               # Anthropic internal packages stub
│       ├── claude-for-chrome-mcp/
│       ├── computer-use-mcp/
│       ├── computer-use-input/
│       └── computer-use-swift/
├── scripts/                 # Automated stub generation scripts
├── build.ts                 # Build script (Bun.build + code splitting + Node.js compatibility post-processing)
├── dist/                    # Build output (entry cli.js + ~450 chunk files)
└── package.json             # Bun workspaces monorepo configuration
```

## Technical Notes

### Runtime Polyfill

Necessary polyfills are injected at the top of the entry file `src/entrypoints/cli.tsx`:

- `feature()` — All feature flags return `false`, skipping unimplemented branches
- `globalThis.MACRO` — Simulates build-time macro injection (VERSION, etc.)

### Monorepo

The project uses Bun workspaces to manage internal packages. Stubs that were previously manually placed under `node_modules/` have been unified and moved into `packages/`, resolved via `workspace:*`.

## Feature Flags Detailed Explanation

The original Claude Code injects feature flags at build time via `bun:bundle`'s `feature()`, and grayscale releases are controlled by A/B experiment platforms like GrowthBook. In this project, `feature()` is polyfilled to always return `false`, therefore all 30 of the following flags are disabled.

### Autonomous Agent

| Flag | Purpose |
|------|------|
| `KAIROS` | Assistant mode — long-running autonomous Agent (includes brief, push notifications, file sending) |
| `KAIROS_BRIEF` | Kairos Brief — send brief summaries to users |
| `KAIROS_CHANNELS` | Kairos Channels — multi-channel communication |
| `KAIROS_GITHUB_WEBHOOKS` | GitHub Webhook Subscription — PR events pushed to Agent in real-time |
| `PROACTIVE` | Proactive mode — Agent proactively executes tasks, includes SleepTool scheduled wakeups |
| `COORDINATOR_MODE` | Coordinator mode — Multi-Agent orchestration and scheduling |
| `BUDDY` | Buddy pair programming feature |
| `FORK_SUBAGENT` | Fork Sub-agent — Fork an independent sub-agent from the current session |

### Remote / Distributed

| Flag | Purpose |
|------|------|
| `BRIDGE_MODE` | Remote control bridging — allows external clients to interact with Claude Code remotely |
| `DAEMON` | Daemon — background resident service, supports worker and supervisor |
| `BG_SESSIONS` | Background sessions — background process management like `ps`/`logs`/`attach`/`kill`/`--bg` |
| `SSH_REMOTE` | SSH remote — `claude ssh <host>` connects to a remote host |
| `DIRECT_CONNECT` | Direct connect mode — `cc://` URL protocol, server command, `open` command |
| `CCR_REMOTE_SETUP` | Web remote setup — configure Claude Code via browser |
| `CCR_MIRROR` | Claude Code Runtime mirror — session state synchronization/replication |

### Communication

| Flag | Purpose |
|------|------|
| `UDS_INBOX` | Unix Domain Socket inbox — local communication between Agents (`/peers`) |

### Enhanced Tools

| Flag | Purpose |
|------|------|
| `CHICAGO_MCP` | Computer Use MCP — computer operations (screenshots, mouse and keyboard control) |
| `WEB_BROWSER_TOOL` | Web browser tool — embedded browser interaction in terminal |
| `VOICE_MODE` | Voice mode — voice input and output, microphone push-to-talk |
| `WORKFLOW_SCRIPTS` | Workflow scripts — user-defined automated workflows |
| `MCP_SKILLS` | Skill loading mechanism based on MCP |

### Dialogue Management

| Flag | Purpose |
|------|------|
| `HISTORY_SNIP` | History snip — manually crop fragments in dialogue history (`/force-snip`) |
| `ULTRAPLAN` | Ultraplan — large-scale planning feature for remote Agent collaboration |
| `AGENT_MEMORY_SNAPSHOT` | Agent runtime memory snapshot feature |

### Infrastructure / Experiments

| Flag | Purpose |
|------|------|
| `ABLATION_BASELINE` | Scientific experiments — baseline ablation testing, used for A/B experiment control groups |
| `HARD_FAIL` | Hard fail mode — aborts directly on error instead of degrading |
| `TRANSCRIPT_CLASSIFIER` | Transcript classifier — `auto-mode` command, automatically analyze and classify dialogue records |
| `UPLOAD_USER_SETTINGS` | Settings sync upload — synchronize local configuration to the cloud |
| `LODESTONE` | Deep link protocol handler — jump from external application to designated location in Claude Code |
| `EXPERIMENTAL_SKILL_SEARCH` | Experimental Skill search index |
| `TORCH` | Torch feature (specific purpose unknown, might be some highlighting/tracking mechanism) |

## License

This project is for learning and research purposes only. All rights to Claude Code belong to [Anthropic](https://www.anthropic.com/).
