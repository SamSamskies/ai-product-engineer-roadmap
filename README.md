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
- **Security & guardrails** — Assume untrusted input. Validate model output, scope tool permissions, and watch for prompt injection — especially once tools and agents are involved.
- **Product UX polish** — Streaming, loading/thinking states, and graceful failure are not optional extras; they're the product. (Deep dive in Phase 2.)

---

# Phase 0 — AI-Native Product Development

**Goal:** Become dramatically more productive than a traditional software engineer.

Master:

- Cursor
- Claude Code
- Claude Design
- OpenAI Codex / CLI

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
- Research assistant
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

Projects:

- A polished streaming chat interface
- A human-in-the-loop tool-approval flow
- Retrofit better UX onto an earlier Phase 1 project

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

Projects:

- GitHub MCP Server
- PostgreSQL MCP Server
- Nostr MCP Server
- Personal MCP Server

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
- Memory
- Retries
- Loops
- State
- Structured outputs

## Security & Guardrails

Once agents can call tools and act autonomously, safety stops being optional:

- Prompt injection and untrusted content
- Output validation before acting
- Tool permission scoping and least privilege
- Human-in-the-loop for destructive actions
- PII and secrets handling

Framework:

- LangGraph

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

Database:

- PostgreSQL
- pgvector

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

Goal:

Deploy production AI applications.

---

# Phase 11 — AI System Design

Learn to answer questions like:

- Should this be an agent?
- Should this be a workflow?
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
