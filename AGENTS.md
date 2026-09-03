# Freebuff Custom Agents (this project)

Custom Freebuff/Codebuff AI agents ported from https://github.com/CodebuffAI/freebuff (Apache-2.0 license).

## Repository layout

- `.agents/types/` — official Codebuff agent type definitions (`agent-definition.ts`, `tools.ts`, `util-types.ts`); do not edit (upstream copies).
- `.agents/buffy-coding.ts` — main coding agent (ports `agents/base3-free-deepseek-flash.ts`; spawns the specialists below).
- `.agents/file-picker.ts` / `.agents/file-lister.ts` — codebase file finding (ports of `agents/file-explorer/*`).
- `.agents/researcher-web.ts` — web research (port of `agents/researcher/researcher-web.ts`).
- `.agents/code-reviewer.ts` — code review (port of `agents/reviewer/code-reviewer-deepseek-flash.ts`).
- `.agents/thinker.ts` — deep reasoning (port of `agents/thinker/thinker.ts`).
- `.agents/README.md` — usage + origin mapping.

## Conventions

- Agents are free-tier models by default (change `model` in each file to swap).
- All agent files import types via relative `./types/agent-definition` — must stay that
  way for the Freebuff/Codebuff SDK (`loadLocalAgents`) to load them.

## Verification

- Run `freebuff` (or `codebuff`) in this directory — `.agents/` auto-loads.
- To typecheck the agents locally without the harness: `bun x tsc --noEmit` with the
  workspace's tsconfig; agents require Bun 1.3.14+ (see `.bun-version` convention upstream)。