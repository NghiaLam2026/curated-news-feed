# Interests

<!--
How this file works:
- Core interests: written by you. The agent never edits this section.
- Everything below Core is maintained by /learn based on what you Like or mark Not for me.
- Be specific: "MCP server design" steers the research much better than "AI tools".
- The indented notes under each interest set the angle and depth the research should aim for.
-->

## Core interests (written by me, agent never edits)

- New model releases, from any lab in any country
  - covers both open-weight and closed models: frontier labs, US, Chinese, European, and other labs alike
  - what's new: capabilities, benchmarks, context length, pricing, license, availability
  - include notable smaller or specialized models (coding, reasoning, small or on-device), not just flagships
  - prefer official announcements, model cards, and technical reports over hype or leaderboard reposts
  - prioritize significant releases; skip minor fine-tunes and incremental version bumps
- AI engineering concepts and building blocks
  - agent harnesses: how they're structured, the agent loop, tool execution, permissions
  - MCP: spec changes, server design patterns, notable new servers and clients
  - skills and other ways of packaging instructions and context for agents
  - context engineering, tool design, subagents, and how coding agents work internally
  - practical and implementation-focused: how it works and how to build with it
- Agentic design architectures
  - new patterns: orchestrator-worker, planner-executor, multi-agent coordination, long-running agents
  - agent memory and state management
  - human-in-the-loop design, reliability, and failure modes
  - prefer real-world case studies and write-ups with design rationale over purely theoretical takes
- Evaluating and testing LLM apps and agents
  - LLM-as-judge design, and calibrating judges against human labels
  - multi-turn and trajectory evals for agents; golden datasets built from real production traffic
  - eval tooling such as promptfoo and LangSmith, and running evals in CI as a release gate
  - red-teaming and prompt-injection testing
  - deterministic tests for LLM code: fake model gateways, frozen tool fixtures, replaying recorded sessions
- Retrieval and knowledge grounding (RAG)
  - chunking strategies, embedding model choice, hybrid lexical plus vector search, reranking
  - managed vector stores (for example S3 Vectors) and their cost and quality tradeoffs
  - long context versus retrieval: when stuffing everything into context stops working
  - building knowledge bases from web crawls, transcripts, documents and code
- Agent security and guardrails
  - defending against prompt injection from untrusted content (web pages, documents, tool results)
  - guardrails: classifier-based checks and managed options such as Bedrock Guardrails; PII handling
  - human approval gates for agent writes, scoped short-lived credentials, policy wrappers around tools (caps, allowlists)
  - authorization for MCP servers and agents: OAuth 2.1 with PKCE and dynamic client registration, JWTs, SigV4
  - tenant isolation for AI features in multi-tenant products (for example Postgres row-level security)
- Data agents and text-to-SQL
  - semantic layers: describing tables, joins and metrics so agents query correctly
  - safe SQL execution: read-only roles, query parsing and allowlists, row and time limits
  - checking an agent's claims against the real data instead of trusting its output
- LLM application engineering in production
  - structured outputs and schema-first tools (JSON Schema, Pydantic, Zod, forcing a tool call)
  - prompt caching, routing between cheap and strong models, tracking token cost per run
  - streaming agent output to a UI: Server-Sent Events, resumable streams, WebSockets, cancellation
  - observability and tracing for LLM apps (OpenTelemetry GenAI conventions, LangSmith, Logfire)
  - versioning prompts and models alongside evals; coping with model deprecations and API behavior changes
- Agent frameworks and cloud AI platforms
  - Claude Agent SDK (headless use, permissions, turn and budget limits), LangGraph, pydantic-ai
  - Amazon Bedrock: Converse API and tool use, cross-region inference profiles, AgentCore (Gateway, Runtime)
  - prefer engineering write-ups and case studies over release notes and docs
- LLMs inside data pipelines
  - LLM classification and entity resolution, cascading from LLM to rules to fuzzy matching to embeddings
  - validating and measuring LLM output in batch jobs; orchestrating LLM steps (for example with Step Functions)
  - data quality and schema drift as inputs to AI systems; fast local tools such as Polars and DuckDB
- Deploying and operating AI services
  - infrastructure as code for AI workloads (AWS CDK, Terraform), private networking and least-privilege IAM for model access
  - GitOps on Kubernetes (Argo CD, EKS) for internal AI platforms
  - LLMOps tooling such as MLflow and self-hosted eval dashboards; secrets management for AI services

## Learned interests (agent-maintained)

<!--
Format:
- Topic name — strength: emerging | medium | high
  - evidence: YYYY-MM-DD, YYYY-MM-DD
-->

- Open-weight frontier model releases — strength: medium
  - evidence: 2026-10-06
- Sandboxing and credential isolation for cloud coding agents — strength: emerging
  - evidence: 2026-10-06
- Multi-agent versus single-agent trade-offs (decomposition, handoff cost) — strength: emerging
  - evidence: 2026-10-06
- Agent memory design: retrieval versus curated documentation — strength: emerging
  - evidence: 2026-10-06
- Verification harnesses for long-horizon agent output — strength: emerging
  - evidence: 2026-10-06

## Exploring (agent-maintained)

<!--
Format:
- Topic name — adjacent | wildcard
  - because: which of your likes this grew from
  - shown: N, liked: N
-->

- Agent security and real-world failure modes — adjacent
  - because: you follow agent permissions, reliability and failure modes; this is what happens when agents act on outside systems
  - shown: 1, liked: 1
- How developer work changes with agents — wildcard
  - because: you like human-in-the-loop design; this is the human side of the same question
  - shown: 1, liked: 1
- Cost and latency engineering for agents — adjacent
  - because: you like agent harness internals; routing models per task is a harness design decision with direct cost impact
  - shown: 1, liked: 1

## Retired explorations

<!--
Format:
- Topic name — shown N, liked N (retired YYYY-MM-DD)
-->

## Not interested

<!-- You can add entries here by hand. /learn also proposes additions after repeated Not for me ticks. -->

- Funding rounds and business news
- Listicles and "top 10 prompts" style posts

## Changelog

<!-- /learn adds one line per change: - YYYY-MM-DD: what changed (why) -->

- 2026-10-06: added learned interest "Open-weight frontier model releases" at medium (liked "Introducing Mistral Large 4" and "Introducing Beam", 2 likes)
- 2026-10-06: added learned interest "Sandboxing and credential isolation for cloud coding agents" at emerging (liked "Claude Code in the cloud: a field guide to cloud sessions")
- 2026-10-06: added learned interest "Multi-agent versus single-agent trade-offs" at emerging (liked "Attention Tax, Handoff Tax")
- 2026-10-06: added learned interest "Agent memory design: retrieval versus curated documentation" at emerging (liked "Agents Don't Need Memory. They Need Documentation.")
- 2026-10-06: added learned interest "Verification harnesses for long-horizon agent output" at emerging (liked "VeriHarness")
- 2026-10-06: added exploring topic "Agent security and real-world failure modes" (adjacent), shown 1, liked 1 (liked Wikimedia's report on OpenAI agent activity)
- 2026-10-06: added exploring topic "How developer work changes with agents" (wildcard), shown 1, liked 1 (liked "Fragments: October 4")
- 2026-10-06: added exploring topic "Cost and latency engineering for agents" (adjacent), shown 1, liked 1 (liked "How to Build a Model Router in the Harness")
- 2026-10-06: recorded Not for me on "I stopped reviewing my agents' code" (orchestrator-worker, human-in-the-loop); one dislike, no profile change