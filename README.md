# AI Agent from Freebuff

A team of custom **Freebuff** AI agents (TypeScript), ported from the
[Freebuff open-source repo](https://github.com/CodebuffAI/freebuff) — the free
coding agent built on the Codebuff agent framework.

* **Main agent:** `.agents/buffy-coding.ts` — a single-loop coding agent that
  explores, edits, verifies, researches,and orchestrates specialist subagents
  (file-picker, researcher-web, code-reviewer, thinker).
* **Subagents:** `.agents/file-picker.ts`, `.agents/file-lister.ts`,
  `.agents/researcher-web.ts`, `.agents/code-reviewer.ts`, `.agents/thinker.ts`.
* **Types:** `.agents/types/` — official Codebuff/Freebuff agent type definitions.



## Quick start

```bash
npm install -g freebuff
# from this project root —
freebuff
# then, in the chat:
#   @buffy-coding add unit tests for the CLI parser
```

Freebuff/Codebuff CLI auto-loads everything under `.agents/`. See
`.agents/README.md` for model customization, the SDK usage example, and the
upstream file mapping.