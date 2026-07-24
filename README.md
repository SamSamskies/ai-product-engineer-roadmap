# Roadmap to Becoming an AI Product Engineer

## Philosophy

The goal is **not** to become an ML engineer.

The goal is to become someone who can design, build, ship, and maintain production AI products.

Coming from a 10+ year frontend engineering background, my biggest advantage is already knowing how to build software — and especially how to build **interfaces**. The hardest part of an AI product is usually the UX over nondeterministic output, and that's exactly where my background is an edge. I should focus on learning **AI systems**, **AI workflows**, and **AI product architecture**, while leaning on what I already do well.

Every phase should end with a real project.

**Evidence hierarchy** (use this when deciding what to trust):

production telemetry > controlled evals > staged tests > demos

---

## Cross-Cutting Threads

These are **not** phases. They are habits I apply to every project from Phase 1 onward. The numbered phases below are where I go deep on each; these threads are how I keep each project honest in the meantime.

- **Harness engineering** — The model is not the product; the *harness* around it is. Guides (`AGENTS.md` / `CLAUDE.md` / rules), sensors (tests, linters, evals), tools/MCP, context pipelines, permissions, and observability. When the agent fails, fix the harness — add a rule, sensor, or constraint — not just the one-off output. (Practiced in Phase 0; deep dive in Phase 7.)
- **Evaluation-driven development** — For every project, answer "how do I know this got better?" before shipping a change. Even a handful of hand-written test cases beats vibes. Prefer trajectory-aware checks and repeated trials over single lucky runs. (Formalized in Phase 3.)
- **Observability & cost** — Track tokens, latency, and $ per request — and for agents, **cost/latency per resolved task**. Log prompts and outputs so failures are debuggable. Promote interesting production failures into eval cases. (Deep dive in Phase 10.)
- **Context engineering** — Everything the model sees is a design decision: system prompt, retrieved context, tool results, memory, and prior turns. Deliberately manage what goes into the window — and what gets summarized, compacted, or dropped. This is the successor framing to prompt engineering. (Deep dive in Phase 7.)
- **Security & guardrails** — Assume untrusted input. Validate model output, scope tool permissions, and watch for prompt injection — especially once tools and agents are involved.
- **Privacy & payment models** — Bearer-token auth (Cashu eCash), pay-per-request vs subscriptions, and no-PII access patterns. Log $/request and compare centralized APIs vs decentralized routers vs local inference. (Deep dive in Phase 4.)
- **Product UX polish** — Streaming, loading/thinking states, and graceful failure are not optional extras; they're the product. (Deep dive in Phase 2.)

---

# Phase 0 — AI-Native Product Development

**Goal:** Become dramatically more productive than a traditional software engineer — by engineering the environment agents work in, not just prompting them.

Master:

- [Cursor](https://github.com/SamSamskies/learncursor)
- Claude Code
- Claude Design
- OpenAI Codex / CLI
- [Goose](https://github.com/aaif-goose/goose) — optional; open-source, multi-provider agentic CLI/desktop (also a great agent to study in Phase 7)

These are all **agentic loop** tools. Beyond just using them, pay attention to *how* they run their loops (context, tool calls, verification, when they stop) — it's the best free lesson in loop engineering, which I go deep on in Phase 7.

## Project Harness Files

Practice authoring the environment coding agents run inside — this is how AI-native product work compounds:

- `AGENTS.md` / `CLAUDE.md` / Cursor rules — project conventions, constraints, and quality gates
- Agent skills — composable, progressively-disclosed capabilities the agent can load on demand
- Hooks and verification steps — sensors that catch failures after the agent acts (tests, linters, schema checks)
- Scoped permissions — least privilege for shell, filesystem, and network tools

When something goes wrong, ratchet the harness: update the guide or sensor so that class of failure can't silently recur.

---

# Phase 1 — OpenAI Platform

Become an expert in:

- Responses API
- Streaming
- Structured Outputs
- Tool Calling
- Background Mode
- Prompt Caching
- File Search
- Image Generation
- Conversation State
- MCP Integration

## Reasoning Models

Frontier models increasingly come in fast vs. reasoning variants. Learn when each is the right default:

- When a single strong reasoning call replaces a multi-step agent chain
- Thinking budgets / effort controls and the latency–cost–quality tradeoff
- When to route hard tasks to reasoning models and easy ones to fast models (ties into Phase 4 routing)

Projects:

- AI coding assistant
- [Research assistant](https://github.com/SamSamskies/learnopenai/tree/main/research-assistant)
- Calendar assistant
- GitHub assistant
- Multi-step planner

Goal:

Understand how modern AI applications are actually built.

---

# Phase 2 — AI Product UX & Interaction Design

**Goal:** Turn my frontend background into a differentiator. Learn to build interfaces that make nondeterministic AI feel fast, trustworthy, and usable — the part most backend/ML engineers do poorly.

Learn:

- Streaming UI (token-by-token, progressive rendering)
- Loading, thinking, and partial-result states
- Graceful failure and retry UX
- Human-in-the-loop patterns (approvals, edits, confirmations)
- Generative / dynamic UI
- Chat vs. inline vs. background interaction patterns
- Perceived latency and optimistic updates
- Citing sources and showing model uncertainty

## Voice, Realtime & Multimodal

Text is only one surface. Voice and multimodal are one of the fastest-growing product areas — and the UX of a nondeterministic *voice* agent is exactly the kind of hard interface problem my frontend background is built for.

- Speech-to-speech and realtime interaction
- Interruption / barge-in and turn-taking
- Partial transcripts and live "thinking" cues (audio + visual)
- Multimodal I/O — vision input, image and audio output
- Latency budgets for realtime (where "fast enough" is a hard requirement, not a nicety)

Tools:

- Vercel AI SDK — foundational for streaming and AI UX in React/Next
- OpenAI Realtime API — speech-to-speech and low-latency voice agents
- CopilotKit — in-app copilots, generative UI, and agent↔UI wiring (revisited in Phase 7)

The concepts above matter more than any single library. Treat these as implementations of the patterns, not the point.

Projects:

- [research-assistant](https://github.com/SamSamskies/learnopenai/tree/main/research-assistant) — continue the Phase 1 app; retrofit polished streaming UX, loading/thinking states, graceful failure, and human-in-the-loop patterns

Goal:

Ship AI products that feel great to use, not just demos that work.

---

# Phase 3 — Evaluation

Learn this early. Evals are what let me tell whether a prompt, model, or retrieval change actually helped — the foundation every later phase (Multi-Model, Agents, RAG) builds on. This formalizes the evaluation thread I start practicing in Phase 1.

Learn:

- Golden datasets
- Prompt versioning
- Regression testing
- LLM-as-a-judge
- AI evaluation workflows

## Agentic & Trajectory Evals

Output-only grading is not enough once systems take multiple steps. Level up to:

- **Trajectory / process evals** — grade the steps and tool use, not only the final text (wrong path that lucks into a good answer still fails)
- **Pass@k / Pass^k** — run the same case multiple times; Pass@k measures "ever succeeds," Pass^k measures "consistently succeeds." Lucky once ≠ reliable
- **Online → offline loop** — promote failed production traces into golden cases (wired end-to-end in Phase 10)
- **Outcome metrics for agents** — cost and latency *per resolved task*, not only $/request

The concepts matter more than any SaaS. A thin local harness (golden JSON + scripts/pytest, optionally an Ollama judge) is enough to practice everything above — and it's the right fit when the app itself must stay local (e.g. locallab). Cloud eval platforms (LangSmith, etc.) are optional later for non-local products; don't let them gate this phase.

Projects:

- [locallab](https://github.com/SamSamskies/locallab) — add a local eval suite (golden cases + regression runs against Ollama); keep all data on-machine. Stretch: multi-trial runs (Pass^k) on a few flaky cases.

Goal:

Ship reliable AI systems — and be able to prove they're reliable.

---

# Phase 4 — Multi-Model Development

## Anthropic

Learn:

- Messages API
- Prompting philosophy
- Tool use
- Long context
- Reasoning / extended thinking — when Claude's thinking modes beat a fast Messages call (pairs with Phase 1 reasoning literacy)

## OpenRouter

Learn:

- Model routing
- Cost optimization
- Provider switching
- Benchmarking models
- Reasoning vs fast model routing — route by task hardness, latency budget, and $/resolved-task, not vibes

## Routstr

The decentralized, privacy-first counterpart to OpenRouter — same OpenAI-compatible client, different architecture: Nostr relay discovery, Cashu/Lightning micropayments, no accounts or KYC.

Learn:

- Drop-in provider swap (`base_url` + Cashu bearer token as API key)
- Pay-per-request cost tracking (ties into the observability thread)
- Nostr-based provider discovery
- When permissionless routing beats centralized APIs

Tools:

- [Routstr Chat](https://github.com/Routstr/routstr-chat) — production Next.js chat client; study how it wires streaming UI, wallet flows, and model selection to the Routstr protocol
- [Routstr Platform](https://routstr.com/) — top up, generate API keys, browse models

Projects:

- Swap an earlier app (e.g. research-assistant) to `api.routstr.com/v1` and benchmark latency, cost, and availability vs OpenRouter/OpenAI using Phase 3 evals
- Compare a reasoning model vs a fast model on the same golden set — quality, latency, and $/resolved-task

Stretch goal: contribute to [routstr-chat](https://github.com/Routstr/routstr-chat). The stack (Next.js, React, TypeScript, Tailwind, Zustand, TanStack Query) plays directly to my frontend background — start with UX bugs, streaming polish, or wallet/settings flows rather than the Rust proxy core. Good on-ramps: chat history search, attachment limits, theme/settings fixes, graceful error states (413/payload-too-large already has MSW mocks to build against).

Develop intuition for:

- GPT
- Claude
- Gemini
- DeepSeek
- Mistral
- Qwen
- GLM
- Llama
- MiniMax
- Kimi (Moonshot)
- xAI models

Goal:

Know which model is best for different problems — and use Phase 3 evals to prove it rather than guess.

---

# Phase 5 — Model Context Protocol (MCP)

Learn:

- MCP architecture
- Clients
- Servers
- Authentication
- Tool discovery
- A2A (Agent-to-Agent) protocol — the emerging companion to MCP. MCP connects agents to *tools*; A2A connects agents to *each other*. Revisited for multi-agent work in Phase 7.

Projects:

- GitHub MCP Server
- PostgreSQL MCP Server
- Nostr MCP Server — Routstr uses Nostr relays for provider discovery; building this while using Routstr in Phase 4 ties Nostr + inference + tools together
- Personal MCP Server

Reference:

- [Routstr](https://routstr.com/) — see how Nostr relay discovery routes inference requests in a real protocol (pairs with the Nostr MCP Server project)
- [Buzz](https://github.com/block/buzz) — optional; a Nostr-based workspace where agents are first-class members. Useful prior art for the Nostr MCP Server project — see its `buzz-acp` (ACP ↔ MCP bridge) and `buzz-dev-mcp` (shell/file-edit MCP tools). Earlier-stage and more experimental than Goose, so treat as inspiration.

Goal:

Understand how AI connects to external systems.

---

# Phase 6 — Python

Goal:

Become comfortable building AI services.

Learn:

- Modern Python
- uv
- asyncio
- Type hints
- FastAPI
- Pydantic
- pytest

Projects:

- Rebuild an earlier AI app in Python
- Build AI APIs
- Create backend services

Important:

I do **not** need to become a Python expert.

I need to become fluent enough to comfortably read, write, and debug Python AI applications.

Note:

Later phases (Agents, RAG) lean on Python. If I hit a Python-only tool sooner, pull this phase forward. LangGraph also has a JS/TS version, so early agent work can happen in my native language if needed.

---

# Phase 7 — AI Agents

Learn concepts before frameworks.

## Workflow vs Agent (decide first)

Most product flows should be **deterministic workflows with LLM steps**, not open agentic loops. Reach for an agent only when the path is genuinely unpredictable and tool choice must be dynamic. Ask before building:

- Is the sequence known? → workflow (graph, pipeline, or structured tool calls)
- Must the model choose tools and branch at runtime? → agentic loop
- Would a single reasoning-model call be enough? → prefer that over a multi-step agent (Phase 1)

Topics:

- Tool calling
- Planning
- Memory — short-term (in-context) vs. persistent, cross-session memory; memory tooling like mem0 and Letta/MemGPT. Memory is becoming a first-class product feature, not just an implementation detail.
- Retries
- State
- Structured outputs
- Computer use & browser agents — agents that operate a screen/browser; their own failure modes and guardrail needs
- Agent skills — composable, progressively-disclosed capabilities (the pattern behind Claude Skills) for structuring what an agent knows how to do

## Harness & Loop Engineering

The agent *is* the loop — but the **harness** is everything around it that makes the loop reliable. This is the core skill of the phase — the successor to prompt engineering. Learn to design the **observe → act → feedback → repeat** cycle *and* the guides/sensors/tools that constrain it:

- The core loop: gather context, act, observe results, decide next step
- Context management across turns (what to keep, summarize, or compact) — this is where the **context engineering** thread goes deep
- Guides — system prompts, `AGENTS.md`-style conventions, tool schemas that make wrong actions hard
- Sensors — verification after each step (schema validation, tests, evals); when a failure class appears, ratchet the harness
- Stop conditions — knowing when the loop is done or stuck
- Error recovery and self-correction within the loop
- Verification steps (letting the agent check its own work)
- Delegation to subagents to keep loops focused
- Multi-agent & agent-to-agent interop (A2A protocol) — connecting agents to each other, ties back to Phase 5's MCP
- Token/latency/cost budgets over long-running loops — optimize for $/resolved-task

## Security & Guardrails

Once agents can call tools and act autonomously, safety stops being optional:

- Prompt injection and untrusted content
- Output validation before acting
- Tool permission scoping and least privilege
- Human-in-the-loop for destructive actions
- PII and secrets handling

Frameworks:

- LangGraph — the one to go deep on
- OpenAI Agents SDK — builds directly on my Phase 1 investment
- Pydantic AI — pairs with the Phase 6 Pydantic/FastAPI stack
- Mastra — TS-native; lets me do agent work without leaving my native language

Go deep on LangGraph, but stay literate in the others and know why I'd reach for each. Concepts transfer; frameworks are interchangeable.

Note: provider SDKs are absorbing memory, tools, and basic eval into opinionated defaults. Learn the concepts so I can choose custom harness layers vs provider defaults deliberately — not because a tutorial started with a framework.

## Study a Production Agent

Read the source of a real, mature open-source agent to see the concepts above in practice — not just in tutorials:

- [Goose](https://github.com/aaif-goose/goose) — production open-source agent (CLI/desktop/API). Study how it runs its loop, integrates 70+ tools over MCP (ties back to Phase 5), supports multiple providers, and implements ACP.
- [Buzz](https://github.com/block/buzz) — optional; interesting take on **multi-agent** design and identity-based guardrails (agents are members with their own keypair, channel memberships, and audit trail — scoped by identity, not permission flags).

Stretch goal: land a contribution to Goose. Treat it as aspirational (merges depend on maintainers, not just me) and start small on a surface that plays to my strengths rather than the Rust core:

- The TypeScript/React desktop UI — reinforces Phase 2 (Agent ↔ UI)
- An MCP extension — reinforces Phase 5
- Docs or a good-first-issue to learn the contribution workflow

## Agent ↔ UI

Connect the agent back to the Phase 2 UX work — stream agent state, steps, and tool calls into a real interface:

- CopilotKit + AG-UI protocol (LangGraph → UI)
- Rendering intermediate steps, plans, and human-in-the-loop approvals

Projects:

- Coding agent
- Research agent
- GitHub issue triage
- Email assistant

Goal:

Understand how production agents work — and how they fail.

---

# Phase 8 — Retrieval-Augmented Generation (RAG)

Learn:

- Embeddings
- Chunking
- Hybrid Search
- Re-ranking
- Metadata
- Graph / relational retrieval — when entities and relationships matter more than semantic similarity alone; vector-only RAG is often insufficient for hard knowledge products
- Retrieval evaluation (apply the Phase 3 eval skills here)

Note:

With 1M+ token context windows and agentic search, RAG is increasingly *agentic retrieval* — the agent decides what to fetch, when — rather than a fixed embed-and-retrieve pipeline. Learn the fundamentals, but treat retrieval as a tool the agent calls, not always a separate system bolted on the front.

Also learn **vectorless / reasoning-based retrieval** (e.g. [PageIndex](https://github.com/VectifyAI/PageIndex)): hierarchical tree index + LLM tree search when document structure and true relevance beat embedding similarity — no chunking or vector DB. Stretch for the PDF assistant project when vector RAG fails on long professional docs.

Database:

- PostgreSQL
- pgvector

Reference:

- [Production Agentic RAG course](https://github.com/jamwithai/production-agentic-rag-course) (arXiv Paper Curator) — a hands-on, keyword-search-first build that also doubles as a cross-phase capstone: it reinforces Python/FastAPI (Phase 6), agentic RAG with LangGraph (Phase 7), and Docker/Redis/SSE + Langfuse monitoring (Phase 10). Note: it uses OpenSearch for hybrid search rather than pgvector, so implement the pgvector path separately to hit my stated stack.
- [PageIndex](https://github.com/VectifyAI/PageIndex) — vectorless, reasoning-based RAG; tree index + LLM tree search (no vector DB / chunking). Useful contrast when long professional docs break similarity search.

Projects:

- Personal knowledge base
- Documentation search
- Semantic search
- PDF assistant

Goal:

Understand why retrieval succeeds or fails.

---

# Phase 9 — Local Models

Strategic for cost, privacy, and offline — open/local reasoning models have closed much of the gap with hosted APIs. Still don't let this phase block progress on hosted products; pull it forward when a project actually needs local inference (e.g. locallab).

Learn:

- Ollama
- Hugging Face
- vLLM

Understand:

- Quantization
- Context windows
- VRAM
- Inference speed
- Open reasoning models — when local reasoning is "good enough" vs when hosted frontier still wins (use Phase 3 evals)

Goal:

Know when local models are the right choice — and prove it with evals, not assumptions.

---

# Phase 10 — Infrastructure & Observability

Learn:

- Docker
- Redis
- Background workers
- Queues
- Streaming
- Server-Sent Events
- WebSockets
- WebRTC & realtime audio transport — the plumbing behind the voice/realtime UX from Phase 2 (low-latency bidirectional streams)

## Observability & Cost

Formalizes the observability thread. By now apps have multi-step traces (agents, tools, RAG) worth instrumenting — not just single-call logs from Phase 1–3. Production telemetry sits at the top of the evidence hierarchy.

Learn:

- Tracing and span structure (LLM calls, tool calls, retrieval steps)
- Prompt/output logging for debugging failures
- Token, latency, and $ per request — dashboards and budgets
- Cost and latency **per resolved task** for multi-step agents
- Connecting production traces back to Phase 3 evals (failed traces → golden dataset cases) — the online → offline loop

Tools:

- Langfuse — open-source LLM observability (tracing, cost, prompt management); self-hostable when data must stay local
- LangSmith — optional; fine for cloud-hosted products, not a fit when prompts/outputs can't leave the machine

Projects:

- Instrument an earlier app (e.g. research-assistant or a Phase 7 agent) end-to-end: traces, cost/latency dashboards (including $/resolved-task), and a loop that promotes interesting failures into eval cases. Prefer Langfuse (or a local harness) over LangSmith when the app is privacy-first / local-only.

Goal:

Deploy production AI applications — and see what they're doing once they are live.

---

# Phase 11 — AI System Design

Learn to answer questions like:

- Should this be a single call, a workflow, or an agentic loop?
- Would a reasoning model make a multi-step agent unnecessary?
- Should this be an agent?
- Should this use RAG (vector, hybrid, graph, agentic, or vectorless / reasoning-based retrieval)?
- Should I cache?
- Should I summarize / compact context?
- Should I fine-tune? (Last resort — prefer prompt/context, RAG, routing, and evals first.)
- Should I use multiple models?
- Should I stream responses?
- What does the harness need — guides, sensors, permissions — before this is safe to run unattended?

Goal:

Think like an AI architect rather than an API consumer.

---

# Success Milestones

## Level 1

- AI-native developer who engineers the harness (`AGENTS.md`, skills, verification), not just the prompt
- Cursor power user
- Comfortable with OpenAI APIs, including reasoning vs fast model tradeoffs
- Building AI products with polished, streaming-first UX

## Level 2

- Comfortable across multiple model providers (including decentralized routing via Routstr)
- Evaluation pipelines as a default habit — including multi-trial / Pass^k checks where it matters
- Built and consumed MCP servers
- Shipped multiple AI products

## Level 3

- Comfortable building Python AI services
- Built production RAG systems
- Understand agent architecture — and default to workflows when an open loop isn't needed

## Level 4

- Built production AI agents with guardrails and a deliberate harness
- Comfortable deploying AI infrastructure and observability (including $/resolved-task and online → offline evals)

## Level 5

Operate as an **AI Product Engineer** capable of designing, building, deploying, evaluating, and maintaining production AI applications end-to-end — with the UX quality and reliability that separate real products from demos.

---

# Resources

## My Learning Records

- [learncursor](https://github.com/SamSamskies/learncursor/tree/main/learning-records) — leveling up Cursor skills (Phase 0)
- [learnopenai](https://github.com/SamSamskies/learnopenai/tree/main/learning-records) — working through the OpenAI platform (Phase 1)
- [learn-ai-ux](https://github.com/SamSamskies/learn-ai-ux/tree/main/learning-records) — AI product UX & interaction design (Phase 2)
- [learn-evals](https://github.com/SamSamskies/learn-evals/tree/main/learning-records) — learning evals (Phase 3)

## Projects

- [habit-tracker](https://github.com/SamSamskies/habit-tracker) — app built while learning Cursor (Phase 0)
- [research-assistant](https://github.com/SamSamskies/learnopenai/tree/main/research-assistant) — Vercel AI SDK + Next.js research assistant; started in Phase 1, continued in Phase 2 for AI UX polish
- [locallab](https://github.com/SamSamskies/locallab) — privacy-first, fully-local blood-work analyzer (local LLM via Ollama)

## Courses & References

- [Routstr](https://routstr.com/) — decentralized OpenAI-compatible inference router; Cashu micropayments, Nostr discovery, no accounts (Phase 4)
- [routstr-chat](https://github.com/Routstr/routstr-chat) — Next.js chat client for the Routstr protocol; contribution target and reference implementation for streaming AI UX + wallet flows (Phases 2, 4)
- [Production Agentic RAG course](https://github.com/jamwithai/production-agentic-rag-course) — hands-on, keyword-search-first RAG build; cross-phase capstone (Phases 6, 7, 8, 10)
- [PageIndex](https://github.com/VectifyAI/PageIndex) — vectorless, reasoning-based RAG; tree index + LLM tree search as a contrast to vector RAG (Phase 8)
- [Goose](https://github.com/aaif-goose/goose) — production open-source AI agent; codebase to study for harness/loop engineering, MCP, and multi-provider design (Phases 5, 7)
- [Buzz](https://github.com/block/buzz) — optional; Nostr-based human+agent workspace; prior art for the Nostr MCP Server and multi-agent/identity guardrails (Phases 5, 7)
