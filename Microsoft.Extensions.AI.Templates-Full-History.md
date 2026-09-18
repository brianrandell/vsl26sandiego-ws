# Microsoft.Extensions.AI.Templates — Full Release History

Source: [dotnet/extensions releases](https://github.com/dotnet/extensions/releases). This repo ships the `aichatweb` (and formerly `mcpserver`) templates alongside the core `Microsoft.Extensions.AI` libraries — one version number covers the whole repo.

---

## Current state (as of Sept 18, 2026)

- **Latest release:** v10.9.0 (Aug 12, 2026). The `Microsoft.Extensions.AI.Templates` package in it is `10.9.0-preview.3.26411.16`.
- **What `dotnet new install Microsoft.Extensions.AI.Templates` gives you:** only `aichatweb` (RAG chat web app).
- **Provider selection is now mandatory.** As of v10.8.4 the GitHub Models provider was removed and `--provider` has no default — you must pass `azureopenai`, `ollama`, or `openai`. (This is the key delta from the 10.7.0 `-h` output, which still listed `githubmodels` as the default.)
- **The MCP server template no longer lives here.** As of v10.9.0 it was removed from dotnet/extensions, migrated to dotnet/aspnetcore, and is now bundled in the .NET 10 and .NET 11 SDKs — so `mcpserver` ships in-box and `Microsoft.McpServer.ProjectTemplates` is discontinued.
- **Agent template:** `aiagent-webapi` continues to ship separately in `Microsoft.Agents.AI.Templates` (aligned to Agent Framework v1.13.0 as of v10.8.x).

---

## 2025 — Origin and early growth

### v9.2.0 — Feb 11, 2025 — 🎉 First public appearance
- **PR [#5837](https://github.com/dotnet/extensions/pull/5837)** — "Initial chat template" by Steve Sanderson. This is the first commit of what became `aichatweb`.
- Follow-up PRs same release: chat template code-review feedback, PDF citation viewer, small fixes.

### v9.3.0 — Mar 11, 2025 — Branded as "Preview 1"
- **PR [#5994](https://github.com/dotnet/extensions/pull/5994)** — "AI Template Preview 1 - ID cleanup & link to survey" — this is the official public preview announcement, matching the [.NET Blog post](https://devblogs.microsoft.com/dotnet/announcing-dotnet-ai-template-preview1/) from ~March 6, 2025.
- GitHub Models support added as a provider option.
- Managed identity support added.
- Overview/README added to the template.
- `Microsoft.Extensions.AI.Templates` third-party notices added.
- Chat template updates following a threat-model security review.
- Vector dimension mismatch fix for Ollama + Azure AI Search.

### v9.4.0 — Apr 8, 2025
- Favicon added to the `AiChatWeb` template.
- Template switched to use just-built packages by default (dev convenience).
- Fixed: template now creates a directory when a project name is specified.
- Framework symbol casing fix so template config options display correctly in VS Code.

### v9.5.0 — May 15, 2025
- Fixed missing reference to `Microsoft.Extensions.AI.OpenAI` in the chat template.
- Chat template dependencies updated; OpenAI/Aspire config fixes; build warnings addressed.
- JS dependency update instructions added to the template README.

### v9.6.0 — Jun 10, 2025
- **Replaced the JSON-file vector store with SQLite** (`Microsoft.Extensions.AI.Templates` — PR #6438) — a meaningful default-storage change for anyone using the local/on-disk vector store option.
- Chat template's `Microsoft.SemanticKernel` dependency bumped to 1.53.0; other external dependencies updated.

*(Releases between v9.6.0 and v10.1.0 — likely including the .NET 10 GA wave — aren't captured in what I pulled; happy to dig further into that gap if useful.)*

---

## Late 2025 — into .NET 10 GA

### v10.1.0 — Dec 10, 2025
- Chat Web template switched to use `Microsoft.Extensions.DataIngestion` for RAG ingestion.
- **New package: `Microsoft.Agents.AI.Templates`** with an `aiagent-webapi` project template — the first Agent Framework project template.
- Agent Framework DevUI added into the `aiagent-webapi` template.
- Chat Web template updated to Aspire 13.0.0.
- Image generation tool support landed in `Microsoft.Extensions.AI`.

---

## 2026 — MCP split and steady iteration

### v10.2.0 — Jan 13, 2026 — 🔑 MCP Server template moved out
- **PR [#7168](https://github.com/dotnet/extensions/pull/7168)** — "Introduce local vs. remote mcpserver template option" — moved `mcpserver` out of `Microsoft.Extensions.AI.Templates` into its own new package, **`Microsoft.McpServer.ProjectTemplates`**, with a local (stdio) vs. remote (HTTP) transport choice.
- From this release on, `dotnet new install Microsoft.Extensions.AI.Templates` only installs `aichatweb`.
- Added support for custom headers in `HostedMcpServerTool`.
- `AmbientMetadata.Build` released to GA.

### v10.3.0 — Feb 11, 2026
- `mcpserver` template (now standalone) updated to ModelContextProtocol `0.7.0-preview.1`.
- `aiagent-webapi` updated to Agent Framework `1.0.0-preview.260127.1`.
- `IChatReducer` interface graduated to stable.
- `MEAI001` experimental diagnostic split into feature-specific IDs (`OPENAI001`, `OPENAI002`, `SCME0001`) — breaking if you suppressed `MEAI001` for OpenAI APIs.

### v10.4.0 — Mar 12, 2026
- MCP Server Tool Content and Function Call Approval APIs graduated to stable.
- `mcpserver` template updated to ModelContextProtocol `1.1.0`.
- New hosted file, web search, and reasoning content types.
- Streaming latency metrics added to OpenTelemetry instrumentation.

### v10.4.1 — Mar 18, 2026
- New experimental APIs: Realtime Client Sessions, Text-to-Speech client.
- ModelContextProtocol libraries bumped in template dependencies.

### v10.5.0 — Apr 15, 2026
- `Microsoft.Extensions.VectorData.Abstractions` moved into this repo from Semantic Kernel.
- **Stateless mode enabled in the remote MCP server template** (MCP-side release v1.2.0, 2026-04-01).
- HTTP Logging Middleware APIs graduated to stable.
- Breaking: `VectorStoreVectorAttribute.Dimensions` renamed to lowercase `dimensions` (source-breaking only).

### v10.5.1 — May 2, 2026
- CodeInterpreter, WebSearch, ImageGeneration tool content types graduated to stable.
- New `HostedToolSearchTool` (deferred tool loading) and `OpenAIRequestPolicies` hook.
- `aiagent-webapi` updated to Agent Framework v1.3.0.
- Breaking (experimental): `WebSearchToolResultContent.Results` renamed to `Outputs`.

### v10.5.2 — May 5, 2026
- Patch: `VectorData.Abstractions` `StorageName` fix. No template changes.

### v10.6.0 — May 12, 2026
- `ResponseContinuationToken` and background-response APIs graduated to stable. Rollup release, no template changes.

### v10.7.0 — Jun 9, 2026
- `Microsoft.Extensions.Diagnostics.ResourceMonitoring.Kubernetes` graduated to stable.
- `Microsoft.Extensions.AI.OpenAI` moved to OpenAI SDK 2.11.0; fixed a `ToolJson.AdditionalProperties` deserialization bug.
- `HostedFileContent.SizeInBytes` / `.CreatedAt` graduated to stable.
- No `aichatweb` or MCP template changes in this release.

### v10.8.0 — Jul 15, 2026
- `Microsoft.Extensions.AI.OpenAI` upgraded to OpenAI SDK 2.12.0.
- New experimental APIs: `AIFunctionNameAttribute` / `AIParameterNameAttribute`, and `ToolApprovalRequestContent.RequiresConfirmation` (`MEAI001`).
- `aiagent-webapi` template updated to Agent Framework v1.13.0.
- Replaced Semantic Kernel connectors with CommunityToolkit (SQLite vector store) to resolve a `SQLitePCLRaw` vulnerability; fixed a transitive MessagePack vulnerability in template AppHost projects.

### v10.8.1 — Jul 21, 2026
- Servicing: fixed tool-call/tool-result ordering when resuming approval-gated functions with service-managed chat history; preserved the OpenAI Responses reasoning item id for stateless (store=false) encrypted reasoning.

### v10.8.2 — Jul 23, 2026
- Servicing: `Microsoft.Extensions.VectorData.ConformanceTests` moved to xUnit 3. (`VectorData.Abstractions` 10.8.2 was published Aug 7, 2026 to fix an accidental omission.)

### v10.8.3 — Jul 27, 2026
- Servicing: fixed `MEAI001` leakage from `ToolApprovalRequestContent.RequiresConfirmation` into consumer source-generated `AIContent` JSON metadata.

### v10.8.4 — Jul 30, 2026 — 🔑 GitHub Models provider removed
- **PR [#7667](https://github.com/dotnet/extensions/pull/7667)** — removed the GitHub Models provider from the AI Chat Web (`aichatweb`) and AI Agent Web API (`aiagent-webapi`) templates, ahead of [GitHub Models being fully retired on July 30, 2026](https://github.blog/changelog/2026-07-01-github-models-is-being-fully-retired-on-july-30-2026/).
- **`--provider` is now required with no default** — must be one of `azureopenai`, `ollama`, or `openai`.
- Bumped `Aspire.Hosting.AppHost` to 13.4.6 and `CommunityToolkit.VectorData.SqliteVec` to 1.0.0-preview.4.

### v10.9.0 — Aug 12, 2026 (latest at time of writing) — 🔑 MCP server template removed from this repo
- **PR [#7680](https://github.com/dotnet/extensions/pull/7680)** — removed the MCP server project template from dotnet/extensions. It was **migrated to the dotnet/aspnetcore repository and is now included in the .NET 10 and .NET 11 SDKs** — so `mcpserver` ships in-box and `Microsoft.McpServer.ProjectTemplates` is discontinued.
- New experimental AI routing/failover clients: abstract `RoutingChatClient` with concrete `SemanticRoutingChatClient`; abstract `FailoverChatClient` with concrete `OrderedFailoverChatClient` (`MEAI001`).
- New experimental HTTP request latency log enrichment (`EXTEXP0013`).
- AI Evaluation report redesign (Overview, Cases, History, Comparison views).
- Note: `Microsoft.Extensions.AI.OpenAI` constrains OpenAI to 2.12.x (a fix was expected in 10.9.1).

---

## The big picture

| Era | What `dotnet new install Microsoft.Extensions.AI.Templates` gave you |
|---|---|
| Feb–Mar 2025 (v9.2–v9.3) | First preview of `aichatweb` (RAG chat) |
| 2025 (v9.4–v9.6) | `aichatweb` matured: SQLite vector store, GitHub Models, managed identity |
| Dec 2025 (v10.1) | `aichatweb` + first-time separate `aiagent-webapi` package; `mcpserver` still bundled |
| Jan 2026 (v10.2) | **Only `aichatweb`** — `mcpserver` split into `Microsoft.McpServer.ProjectTemplates`, agents live in `Microsoft.Agents.AI.Templates` |
| Jul 2026 (v10.8.4) | Same, but GitHub Models provider dropped — `--provider` now required |
| **Aug 2026 (v10.9) onward** | Still only `aichatweb`; `mcpserver` removed entirely and folded into the .NET 10/11 SDKs |

So the single command you ran has quietly narrowed in scope over its lifetime — it started as the only game in town, and is now specifically and only the RAG chat template, with MCP scaffolding now shipping in the SDK itself and Agent scaffolding in its own package.

### The MCP template — three acts
1. **Bundled** in `Microsoft.Extensions.AI.Templates` (through v10.1).
2. **Split out** into its own `Microsoft.McpServer.ProjectTemplates` package with local/remote transport options (v10.2, Jan 2026).
3. **Removed from dotnet/extensions and moved into the .NET SDK** via dotnet/aspnetcore — now in-box in .NET 10 and .NET 11 (v10.9, Aug 2026).

---

## Appendix — Source URLs

### Microsoft Blog Posts
- [.NET AI Template Now Available in Preview](https://devblogs.microsoft.com/dotnet/announcing-dotnet-ai-template-preview1/) — .NET Blog, Mar 2025. Original Preview 1 announcement.
- [Building Your First MCP Server with .NET and Publishing to NuGet](https://devblogs.microsoft.com/dotnet/mcp-server-dotnet-nuget-quickstart/) — .NET Blog, Jul 2025. Original MCP server template walkthrough (predates the package split).
- [GitHub Models is being fully retired on July 30, 2026](https://github.blog/changelog/2026-07-01-github-models-is-being-fully-retired-on-july-30-2026/) — GitHub Changelog. The retirement that drove the provider removal in v10.8.4.

### GitHub Repositories
- [dotnet/extensions](https://github.com/dotnet/extensions) — main repository; source for `Microsoft.Extensions.AI.Templates`, `Microsoft.McpServer.ProjectTemplates`, `Microsoft.Agents.AI.Templates`, and the core AI libraries.
- [dotnet/extensions — Releases](https://github.com/dotnet/extensions/releases) — full version history used to build this document.
- [dotnet/extensions — Discussion #7174](https://github.com/dotnet/extensions/discussions/7174) — "MCP Server .NET docs reference incorrect project template package," where the template package split was flagged and confirmed.
- [dotnet/extensions — Commit b60d3bb (PR #7168)](https://github.com/dotnet/extensions/commit/b60d3bb431fc78a47f69ecc45f9c1e6adc32e933) — the exact commit that moved `mcpserver` into `Microsoft.McpServer.ProjectTemplates`.
- [dotnet/aspire — Issue #10630](https://github.com/dotnet/aspire/issues/10630) — feature request for an MCP-focused Aspire template (context on ecosystem direction, not a shipped change).

### Microsoft Learn Documentation
- [Quickstart: Create a .NET AI app using the AI app template](https://learn.microsoft.com/en-us/dotnet/ai/quickstarts/ai-templates) — current install/usage steps for `aichatweb`.
- [Quickstart: Create a minimal MCP server and publish to NuGet](https://learn.microsoft.com/en-us/dotnet/ai/quickstarts/build-mcp-server) — current install/usage steps for the standalone `Microsoft.McpServer.ProjectTemplates`.
- [Microsoft.Extensions.AI libraries overview](https://learn.microsoft.com/en-us/dotnet/ai/microsoft-extensions-ai) — conceptual overview of the underlying `Microsoft.Extensions.AI` abstractions.

### Package Registry
- [Microsoft.Extensions.AI on NuGet](https://www.nuget.org/packages/Microsoft.Extensions.AI/) — current published package/version listing.
