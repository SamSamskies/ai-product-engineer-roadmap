# Roadmap to Becoming an AI Product Engineer

## Philosophy

The goal is **not** to become an ML engineer.

The goal is to become someone who can design, build, ship, and maintain production AI products.

Coming from a 10+ year frontend engineering background, my biggest advantage is already knowing how to build software — and especially how to build **interfaces**. The hardest part of an AI product is usually the UX over nondeterministic output, and that's exactly where my background is an edge. I should focus on learning **AI systems**, **AI workflows**, and **AI product architecture**, while leaning on what I already do well.

Every phase should end with a real project.

---

## Cross-Cutting Threads

These are **not** phases. They are habits I apply to every project from Phase 1 onward. The numbered phases below are where I go deep on each; these threads are how I keep each project honest in the meantime.

- **Evaluation-driven development** — For every project, answer "how do I know this got better?" before shipping a change. Even a handful of hand-written test cases beats vibes. (Formalized in Phase 3.)
- **Observability & cost** — Track tokens, latency, and $ per request. Log prompts and outputs so failures are debuggable.
- **Context engineering** — Everything the model sees is a design decision: system prompt, retrieved context, tool results, memory, and prior turns. Deliberately manage what goes into the window — and what gets summarized, compacted, or dropped. This is the successor framing to prompt engineering. (Deep dive in Phase 7.)
- **Security & guardrails** — Assume untrusted input. Validate model output, scope tool permissions, and watch for prompt injection — especially once tools and agents are involved.
- **Product UX polish** — Streaming, loading/thinking states, and graceful failure are not optional extras; they're the product. (Deep dive in Phase 2.)

---

# Phase 0 — AI-Native Product Development

**Goal:** Become dramatically more productive than a traditional software engineer.

Master:

- [Cursor](https://github.com/SamSamskies/learncursor)
- Claude Code
- Claude Design
- OpenAI Codex / CLI
- [Goose](https://github.com/aaif-goose/goose) — optional; open-source, multi-provider agentic CLI/desktop (also a great agent to study in Phase 7)

These are all **agentic loop** tools. Beyond just using them, pay attention to *how* they run their loops (context, tool calls, verification, when they stop) — it's the best free lesson in loop engineering, which I go deep on in Phase 7.

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

Tools:

- LangSmith
- Langfuse

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

## OpenRouter

Learn:

- Model routing
- Cost optimization
- Provider switching
- Benchmarking models

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
- Nostr MCP Server
- Personal MCP Server

Reference:

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

Topics:

- Tool calling
- Planning
- Memory — short-term (in-context) vs. persistent, cross-session memory; memory tooling like mem0 and Letta/MemGPT. Memory is becoming a first-class product feature, not just an implementation detail.
- Retries
- State
- Structured outputs
- Computer use & browser agents — agents that operate a screen/browser; their own failure modes and guardrail needs
- Agent skills — composable, progressively-disclosed capabilities (the pattern behind Claude Skills) for structuring what an agent knows how to do

## Loop Engineering

The agent *is* the loop. This is the core skill of the phase — the successor to prompt engineering. Learn to design the **observe → act → feedback → repeat** cycle:

- The core loop: gather context, act, observe results, decide next step
- Context management across turns (what to keep, summarize, or compact) — this is where the **context engineering** thread goes deep
- Stop conditions — knowing when the loop is done or stuck
- Error recovery and self-correction within the loop
- Verification steps (letting the agent check its own work)
- Delegation to subagents to keep loops focused
- Multi-agent & agent-to-agent interop (A2A protocol) — connecting agents to each other, ties back to Phase 5's MCP
- Token/latency/cost budgets over long-running loops

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
- Retrieval evaluation (apply the Phase 3 eval skills here)

Note:

With 1M+ token context windows and agentic search, RAG is increasingly *agentic retrieval* — the agent decides what to fetch, when — rather than a fixed embed-and-retrieve pipeline. Learn the fundamentals, but treat retrieval as a tool the agent calls, not always a separate system bolted on the front.

Database:

- PostgreSQL
- pgvector

Reference:

- [Production Agentic RAG course](https://github.com/jamwithai/production-agentic-rag-course) (arXiv Paper Curator) — a hands-on, keyword-search-first build that also doubles as a cross-phase capstone: it reinforces Python/FastAPI (Phase 6), Langfuse monitoring (Phase 3), agentic RAG with LangGraph (Phase 7), and Docker/Redis/SSE (Phase 10). Note: it uses OpenSearch for hybrid search rather than pgvector, so implement the pgvector path separately to hit my stated stack.

Projects:

- Personal knowledge base
- Documentation search
- Semantic search
- PDF assistant

Goal:

Understand why retrieval succeeds or fails.

---

# Phase 9 — Local Models

The most optional phase — valuable for cost and privacy, but not core to shipping on hosted APIs. Don't let it block progress.

Learn:

- Ollama
- Hugging Face
- vLLM

Understand:

- Quantization
- Context windows
- VRAM
- Inference speed

Goal:

Know when local models are the right choice.

---

# Phase 10 — Infrastructure

Learn:

- Docker
- Redis
- Background workers
- Queues
- Streaming
- Server-Sent Events
- WebSockets
- WebRTC & realtime audio transport — the plumbing behind the voice/realtime UX from Phase 2 (low-latency bidirectional streams)

Goal:

Deploy production AI applications.

---

# Phase 11 — AI System Design

Learn to answer questions like:

- Should this be a single call, a workflow, or an agentic loop?
- Should this be an agent?
- Should this use RAG?
- Should I cache?
- Should I summarize?
- Should I fine-tune?
- Should I use multiple models?
- Should I stream responses?

Goal:

Think like an AI architect rather than an API consumer.

---

# Success Milestones

## Level 1

- AI-native developer
- Cursor power user
- Comfortable with OpenAI APIs
- Building AI products with polished, streaming-first UX

## Level 2

- Comfortable across multiple model providers
- Evaluation pipelines as a default habit
- Built and consumed MCP servers
- Shipped multiple AI products

## Level 3

- Comfortable building Python AI services
- Built production RAG systems
- Understand agent architecture

## Level 4

- Built production AI agents with guardrails
- Comfortable deploying AI infrastructure

## Level 5

Operate as an **AI Product Engineer** capable of designing, building, deploying, evaluating, and maintaining production AI applications end-to-end — with the UX quality and reliability that separate real products from demos.

---

# Resources

## My Learning Records

- [learncursor](https://github.com/SamSamskies/learncursor/tree/main/learning-records) — leveling up Cursor skills (Phase 0)
- [learnopenai](https://github.com/SamSamskies/learnopenai/tree/main/learning-records) — working through the OpenAI platform (Phase 1)
- [learn-ai-ux](https://github.com/SamSamskies/learn-ai-ux/tree/main/learning-records) — AI product UX & interaction design (Phase 2)

## Projects

- [habit-tracker](https://github.com/SamSamskies/habit-tracker) — app built while learning Cursor (Phase 0)
- [research-assistant](https://github.com/SamSamskies/learnopenai/tree/main/research-assistant) — Vercel AI SDK + Next.js research assistant; started in Phase 1, continued in Phase 2 for AI UX polish
- [locallab](https://github.com/SamSamskies/locallab) — privacy-first, fully-local blood-work analyzer (local LLM via Ollama)

## Courses & References

- [Production Agentic RAG course](https://github.com/jamwithai/production-agentic-rag-course) — hands-on, keyword-search-first RAG build; cross-phase capstone (Phases 3, 6, 7, 8, 10)
- [Goose](https://github.com/aaif-goose/goose) — production open-source AI agent; codebase to study for loop engineering, MCP, and multi-provider design (Phases 5, 7)
- [Buzz](https://github.com/block/buzz) — optional; Nostr-based human+agent workspace; prior art for the Nostr MCP Server and multi-agent/identity guardrails (Phases 5, 7)
