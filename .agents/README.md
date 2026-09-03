# Custom AI agents (ported from Freebuff)

This `.agents/` directory contains a team of custom AI agents ported from the
[Freebuff](https://github.com/CodebuffAI/freebuff) repository — the free,
open-source coding agent built on the [Codebuff](https://github.com/CodebuffAI/codebuff) (git) framework.
Each file exports an `AgentDefinition` (TypeScript) using the official Codebuff/Freebuff
schema in `types/`.

## The team

| Agent | File | Role | Model |
| --- | --- | --- | --- |
| **buffy-coding** | `buffy-coding.ts` | Main coding agent — explores, edits, verifies, researches,and orchestrates the rest | `deepseek/deepseek-v4-flash` |
| **file-picker** | `file-picker.ts` | Finds relevant files in the codebase | `google/gemini-2.5-flash-lite` |
| **file-lister** | `file-lister.ts` | Lists file paths (spawned by file-picker) | `google/gemini-3.5-flash-lite` |
| **researcher-web** | `researcher-web.ts` | Browses the web and cites sources | `google/gemini-3.5-flash-lite` |
| **code-reviewer** | `code-reviewer.ts` | Critical code review (no tools) | `deepseek/deepseek-v4-flash` |
| **thinker** | `thinker.ts` | Deep reasoning on a focused problem | `z-ai/glm-5.3-flash` |

The main agent spawns the specialists via the `spawn_agents` tool; they are the
same agent taxonomy the Freebuff product uses internally (file-picker,
researcher-web, code-reviewer, thinker), just packaged for local use.

## Running the agents

Freebuff's CLI  (and Codebuff's) auto-loads agents from `.agents/` in
your project (also checks `../.agents` and `~/.agents`), so no extra setup
is needed:

```bash
# Install the Freebuff CLI (the free product) or Codebuff CLI
npm install -g freebuff
# from this project root:
cd /workspace/project
freebuff
```

Then, in the chat, invoke an agent by name:

```
@buffy-coding add a CLI flag to skip tests in debug builds
@researcher-web what is the latest LTS Node.js release and its support window?
@code-reviewer please review my recent changes
```

Or use the Codebuff SDK to run an agent programmatically:

```typescript
import { CodebuffClient, loadLocalAgents } from '@codebuff/sdk'

const agents = await loadLocalAgents({ agentsPath: './.agents' })
const client = new CodebuffClient({ apiKey: process.env.CODEBUFF_API_KEY })

const result = await client.run({
  agent: 'buffy-coding',
  agentDefinitions: Object.values(agents),
  prompt: 'Add a healthcheck endpoint to the API',
})
```

## Customizing

- **Change models:** Any [OpenRouter](https://openrouter.ai/models) model ID
  works — free picks from the Freebuff catalog include
  `z-ai/glm-5.3-flash`, `openai/gpt-5.6-luna`, `upstage/solar-pro4`,
  `mimo/mimo-v2.5`, and `minimax/minimax-m3`. Just edit the `model` field..
- **Tools:** See `types/tools.ts` for every available tool name and its parameters..
- **Agent schema:** See `types/agent-definition.ts` for every field you can set
  (prompts, input/output schemas, `handleSteps` orchestration, MCP servers, …)..
- **Publish:** With Codebuff you can ship an agent to the store with
  `codebuff publish <agent-id>` so users worldwide can run it.

## Origin

Ported from the Freebuff repository (Apache-2.0) on 2026-09-03:

- `agents/base3-free-deepseek-flash.ts` → `buffy-coding.ts`
- `agents/file-explorer/file-picker.ts` (default) → `file-picker.ts`
- `agents/file-explorer/file-lister.ts` → `file-lister.ts`
- `agents/researcher/researcher-web.ts` → `researcher-web.ts`
- `agents/reviewer/code-reviewer-deepseek-flash.ts` → `code-reviewer.ts`
- `agents/thinker/thinker.ts` → `thinker.ts`

Type definitions copied from `common/src/templates/initial-agents-dir/types/`.
See `LICENSE` (Apache-2.0) for upstream license terms.