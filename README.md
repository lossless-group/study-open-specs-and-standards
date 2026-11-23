# Open Specs & Standards — Study

A reading collection of open specifications, standards, and conventions that
shape how humans and AI agents cooperate through files. Each entry is cloned
as a git submodule under this directory.

## Why this study exists

We are interested in the *file-as-interface* between humans and agents.
Most of the projects below propose, define, or implement a file format,
folder convention, or protocol that lets a person and an agent share
context without ambiguity. We are studying them along two axes:

**1. Project structure & tooling for Human+Agent cooperation**
- How is the spec itself authored, versioned, and published?
- What build tooling, parsers, validators, compressors, or generators are
  used to keep machine-readable and human-readable views in sync?
- What scripts, trees, manifests, or lockfiles support reproducibility?
- How is content organized so both a reader and an agent can navigate it?

**2. Data formats, naming conventions, and standards**
- What primitives (front-matter, JSON Schema, TypeScript types, OpenAPI,
  Markdown sections) are chosen and why?
- What naming conventions emerge (`AGENTS.md`, `SKILL.md`, `llms.txt`,
  `DESIGN.md`)?
- Which of these patterns generalize beyond developer projects to
  non-dev workflows (research, ops, design, content, business)?

The intent is to extract patterns we can apply across our own dev *and*
non-dev workflows — not to adopt any one of them wholesale.

---

## Pins last refreshed 2026-11-23

Every submodule was moved to the latest commit on its upstream default
branch. Dates are commit dates of the old and new pins. Profiles in
`context-v/profiles/` each carry a "Changes since the previous pin" section.

| Repo | Old → new pin | Commits | Latest release at new pin |
|---|---|---:|---|
| 12-factor-agents | 2025-09-21 → 2025-09-21 | 0 | none (untagged) |
| agent-2-agent | 2026-04-23 → 2026-11-18 | 105 | v1.0.1 |
| agents-md | 2026-03-12 → 2026-09-10 | 3 | none (untagged) |
| ai-skills | 2026-04-23 → 2026-11-16 | 33 | none (untagged) |
| design-md | 2026-05-02 → 2026-11-17 | 45 | 0.4.0 tag; package 0.4.1 |
| frictionless-specs | 2026-01-08 → 2026-08-25 | 2 | v2.0 |
| gsd-core (was get-shit-done) | 2026-05-31 → 2026-11-23 | 4414 | v1.23.0 (`@opengsd/gsd-core`) |
| llms-txt | 2026-04-29 → 2026-09-25 | 20 | 0.0.7 (proposal "v2") |
| mcp-api | 2026-02-08 → 2026-02-08 | 0 | v1.0.0 |
| modelcontextprotocol | 2026-04-27 → 2026-11-21 | 1232 | spec `2026-07-28` |
| open-spec | 2026-05-01 → 2026-11-19 | 487 | v2.1.1 |
| openui | 2026-05-06 → 2026-11-21 | 665 | none (per-package; lang-core 1.1.1, spec 1.0) |
| spec-kit | 2026-05-01 → 2026-11-20 | 1579 | v1.4.3 |
| superpowers | 2026-05-04 → 2026-11-03 | 247 | v7.0.2 |
| symphony | 2026-04-27 → 2026-09-15 | 35 | v0.0.3 |

What a reader should know first:

- **MCP `2026-07-28`** is stateless: no `initialize` handshake or sessions,
  a `server/discover` RPC, and Multi Round-Trip Requests in place of
  server-initiated requests. Roots, Sampling, and Logging are deprecated.
- **llms.txt v2** drops the special meaning of `## Optional`, scopes files to
  paths, and adds `rel="alternate"` / `rel="describedby"` discovery.
- **The study now pins gsd-core.** `gsd-build/get-shit-done` was archived,
  so the study follows its successor, `open-gsd/gsd-core` (GSD Core,
  v1.23.0). The two share history until a May 2026 fork; the old
  2026-05-31 pin is not in gsd-core, so its commit count runs from the
  2026-05-04 pin.
- **A2A joined the Agentic AI Foundation**, alongside MCP and AGENTS.md, and
  its TSC grew to nine companies.
- **OpenSpec 2.0** installs skills only; `/opsx:*` became `/openspec-*`.
- **OpenUI** published a written 1.0 specification for OpenUI Lang.
- **ai-skills** moved the docx, pdf, pptx, and xlsx skills from an
  all-rights-reserved license to Apache 2.0.

---

## Candidates
`https://github.com/nmelo/initech`
`https://github.com/obra/superpowers`

## The collection

### Specs for guiding agents inside a project

#### [agents-md](./agents-md) — `AGENTS.md`
- **Repo:** https://github.com/agentsmd/agents.md
- **Maintainer:** the AGENTS.md community (multi-vendor; see https://agents.md)
- **Summary:** A simple, open Markdown format — a "README for agents" — that
  gives coding agents a predictable place for dev environment tips, test
  instructions, and PR rules. Free-form Markdown with conventional headings.
  Stewarded as an LF Projects series under the Agentic AI Foundation; the
  repo now includes its `Technical_Charter.pdf` (MIT code, CC BY 4.0 docs).

#### [ai-skills](./ai-skills) — Anthropic Agent Skills
- **Repo:** https://github.com/anthropics/skills
- **Maintainer:** Anthropic
- **Summary:** Reference implementation and specification for Agent Skills
  — folders of instructions, scripts, and resources (`SKILL.md` + assets)
  that an agent loads dynamically for specialized tasks. Includes the spec
  (`./spec`), a template (`./template`), and example skills (`./skills`).
  The docx, pdf, pptx, and xlsx skills moved to Apache 2.0 in this pin
  range, so the whole repo is now open source; most other changes are
  `claude-api` skill updates.

#### [open-spec](./open-spec) — OpenSpec
- **Repo:** https://github.com/Fission-AI/OpenSpec
- **Maintainer:** Fission AI
- **Summary:** A spec-driven workflow framework distributed as an npm package
  (`@fission-ai/openspec`, v2.x) and a standalone binary. Emphasizes
  iterative, brownfield-friendly specification of changes via delta specs
  and an artifact-guided flow. Since 2.0 it installs agent skills
  (`/openspec-propose`, …) instead of `/opsx:*` slash commands.

#### [spec-kit](./spec-kit) — GitHub Spec Kit
- **Repo:** https://github.com/github/spec-kit
- **Maintainer:** GitHub
- **Summary:** An open-source toolkit for *Spec-Driven Development*, and since
  v1.0 (August 2026) for other agent processes too: bug fixing and idea
  assessment ship as bundled extensions. Provides a `specify` CLI, presets,
  extensions, workflows, bundles, and 43 coding-agent integrations. Captures
  product scenarios and predictable outcomes as the primary artifact, with
  code generated against them.

### Methodology / principles

#### [12-factor-agents](./12-factor-agents)
- **Repo:** https://github.com/humanlayer/12-factor-agents
- **Author / Maintainer:** Dex Horthy and the HumanLayer team
- **License:** Apache 2.0 (code) / CC BY-SA 4.0 (content)
- **Summary:** Twelve principles for building reliable LLM applications,
  in the spirit of the original 12-Factor App. Source content lives as
  Markdown files in `content/factor-XX-*.md`.

### Markdown-as-protocol (file conventions for AI consumption)

#### [llms-txt](./llms-txt) — `/llms.txt`
- **Repo:** https://github.com/AnswerDotAI/llms-txt
- **Author:** Jeremy Howard (Answer.AI)
- **Summary:** A proposal for websites to publish a root `/llms.txt` Markdown
  file plus `.md`-suffixed versions of pages, providing LLM-friendly content
  at inference time. Includes the `llms_txt2ctx` CLI for compressing the
  index into a context blob. The proposal's v2 (August 2026) lets files sit
  at any path, adds link-relation discovery, and removes the CLI and the
  `## Optional` semantic from the proposal itself; the code still ships.

#### [design-md](./design-md) — `DESIGN.md`
- **Repo:** https://github.com/google-labs-code/design.md
- **Maintainer:** Google Labs
- **Summary:** A format for describing a visual identity to coding agents.
  Combines machine-readable design tokens (YAML front matter) with
  human-readable rationale (Markdown prose) so agents have both the values
  and the *why*. Published as `@google/design.md` (0.4.x, Apache 2.0) with a
  linter and exporters (Tailwind, CSS variables, DTCG); the spec gained
  Motion and Voice & Content sections, grouped tokens, and `@`-references.

### Wire protocols & schemas

#### [modelcontextprotocol](./modelcontextprotocol) — MCP
- **Repo:** https://github.com/modelcontextprotocol/modelcontextprotocol
- **Authors:** David Soria Parra ([@dsp](https://github.com/dsp)) and
  Justin Spahr-Summers ([@jspahrsummers](https://github.com/jspahrsummers))
- **Maintainer:** Anthropic and the MCP community
- **License:** MIT
- **Summary:** The Model Context Protocol — a standard for connecting LLM
  applications to context, tools, and prompts. The schema is authored in
  TypeScript and emitted to JSON Schema. Documentation is built with
  Mintlify at https://modelcontextprotocol.io. Latest protocol version is
  `2026-07-28`, which made the protocol stateless. A project of the
  Agentic AI Foundation since December 2025.

#### [agent-2-agent](./agent-2-agent) — A2A Protocol
- **Repo:** https://github.com/a2aproject/A2A
- **Maintainer:** A2A Project (Google-initiated; nine-company TSC; an
  Agentic AI Foundation project since August 2026)
- **License:** Apache 2.0
- **Summary:** Agent2Agent — an open protocol for inter-agent communication.
  Includes a written specification (`./specification`), ADRs (`./adrs`),
  and governance docs. SDKs live in sibling repos (Python `a2a-sdk`, Go,
  JS, Java, .NET, and now Rust), plus an A2A CLI.

### Reference implementations

Production code that implements one of the specs above. Useful for seeing
how a written spec lands as a real codebase — what's idiomatic, what's
left as an exercise, what's needed to bridge existing systems.

#### [mcp-api](./mcp-api) — Dynamic MCP server for REST APIs
- **Repo:** https://github.com/Parslee-ai/mcp-api
- **Maintainer:** Parslee AI (`Parslee-ai` org)
- **Summary:** Generates MCP tools dynamically from existing API
  definitions (OpenAPI, Swagger, Postman Collections, GraphQL). A direct
  counterpart to the MCP spec above — read together to see how the
  protocol's tool/prompt/resource primitives translate into a working
  server. Written in C#. No upstream changes in the 2026-11-23 refresh.

### Data & dataset specifications

#### [frictionless-specs](./frictionless-specs) — Data Package
- **Repo:** https://github.com/frictionlessdata/specs
- **Maintainer:** Frictionless Data community (Open Knowledge Foundation
  lineage); funded in part by NLnet / NGI0 Entrust
- **Summary:** A family of small, composable specs (Data Package, Data
  Resource, Table Schema, Tabular Data Package) for describing datasets and
  tabular data so they are findable, accessible, interoperable, and
  reusable (FAIR). A natural reference point for "what does
  `data.md`/`dataset.json` look like?"

### Also pinned (profiled, not yet grouped above)

- [gsd-core](./gsd-core) — GSD Core (`@opengsd/gsd-core`), a
  context-engineering workflow orchestrator that runs a phase loop through
  fresh-context subagents across 18 AI runtimes. Successor to the archived
  `gsd-build/get-shit-done`.
- [openui](./openui) — Thesys's OpenUI, a generative-UI framework with its
  own language, OpenUI Lang, now specified in a written 1.0 spec (`spec/`).
- [superpowers](./superpowers) — Jesse Vincent's agent-development
  methodology delivered as a multi-harness skill plugin (v7.x).
- [symphony](./symphony) — OpenAI's service specification for a daemon
  that turns an issue tracker into a work queue for coding agents; now
  tracker-generic (Linear, GitHub Issues, Jira, Asana, GitLab).

---

## What we are looking at, repo by repo

A working checklist when reading each project:

- **Spec artifact:** Where does the spec actually live? Single Markdown,
  schema-first (JSON Schema / TypeScript), or distributed across files?
- **Front matter & metadata:** Is YAML/TOML/JSON front matter used? What
  fields are required vs optional?
- **Build pipeline:** Is there a generator that emits multiple
  representations from one source (TS → JSON Schema, MD → site, etc.)?
- **Validation:** Linters, schema validators, CI checks?
- **Compression / context-shaping:** Tools that reduce a large repo or
  documentation set into an LLM-sized context blob (e.g. `llms_txt2ctx`).
- **Parser ergonomics:** Can a non-AI program parse the artifact reliably?
- **Naming conventions:** Filename, location, casing, file extension.
- **Versioning & change management:** SemVer, dated schema directories,
  ADR process, deprecation policy.
- **Discovery:** How does an agent find the file? Root-of-repo, root-of-site,
  manifest entry, or registry?
- **Cross-domain transfer:** Does the convention extend cleanly to
  non-developer artifacts (research notes, operational runbooks, content
  briefs, design systems, datasets)?

## Notes on grouping

The categories above are descriptive, not authoritative — several entries
straddle multiple groups (`ai-skills` is both a spec and a methodology;
MCP is both a wire protocol and a schema discipline). Treat the grouping
as a reading order, not a taxonomy.
