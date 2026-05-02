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

## The collection

### Specs for guiding agents inside a project

#### [agents-md](./agents-md) — `AGENTS.md`
- **Repo:** https://github.com/agentsmd/agents.md
- **Maintainer:** the AGENTS.md community (multi-vendor; see https://agents.md)
- **Summary:** A simple, open Markdown format — a "README for agents" — that
  gives coding agents a predictable place for dev environment tips, test
  instructions, and PR rules. Free-form Markdown with conventional headings.

#### [ai-skills](./ai-skills) — Anthropic Agent Skills
- **Repo:** https://github.com/anthropics/skills
- **Maintainer:** Anthropic
- **Summary:** Reference implementation and specification for Agent Skills
  — folders of instructions, scripts, and resources (`SKILL.md` + assets)
  that an agent loads dynamically for specialized tasks. Includes the spec
  (`./spec`), a template (`./template`), and example skills (`./skills`).

#### [open-spec](./open-spec) — OpenSpec
- **Repo:** https://github.com/Fission-AI/OpenSpec
- **Maintainer:** Fission AI
- **Summary:** A spec-driven workflow framework distributed as an npm package
  (`@fission-ai/openspec`). Emphasizes iterative, brownfield-friendly
  specification of changes via slash-commands and an artifact-guided flow.

#### [spec-kit](./spec-kit) — GitHub Spec Kit
- **Repo:** https://github.com/github/spec-kit
- **Maintainer:** GitHub
- **Summary:** An open-source toolkit for *Spec-Driven Development*. Provides
  a `specify` CLI, presets, extensions, and integrations with multiple AI
  coding agents. Captures product scenarios and predictable outcomes as the
  primary artifact, with code generated against them.

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
  index into a context blob.

#### [design-md](./design-md) — `DESIGN.md`
- **Repo:** https://github.com/google-labs-code/design.md
- **Maintainer:** Google Labs
- **Summary:** A format for describing a visual identity to coding agents.
  Combines machine-readable design tokens (YAML front matter) with
  human-readable rationale (Markdown prose) so agents have both the values
  and the *why*.

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
  Mintlify at https://modelcontextprotocol.io.

#### [agent-2-agent](./agent-2-agent) — A2A Protocol
- **Repo:** https://github.com/a2aproject/A2A
- **Maintainer:** A2A Project (Google-initiated; multi-vendor governance)
- **License:** Apache 2.0
- **Summary:** Agent2Agent — an open protocol for inter-agent communication.
  Includes a written specification (`./specification`), ADRs (`./adrs`),
  governance docs, and an SDK published to PyPI as `a2a-sdk`.

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
  server. Written in C#.

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
