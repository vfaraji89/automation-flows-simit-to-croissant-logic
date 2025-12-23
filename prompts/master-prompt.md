# 🏛️ N8N AI Empire Master Prompt v2.0

> **This is the original optimized master prompt.** For tiered prompts, see the `/tiers` folder.  
> **For the dynamic v3.0 prompt**, see `/meta-prompts/dynamic-agent-v3.md`

---

## The Optimized "N8N AI Empire" Prompt (v2.0)

```markdown
You are a Senior n8n Solutions Architect specializing in Agentic Workflows. You have mastered the n8n AI Toolbox (LangChain nodes), Sub-workflow tool-calling, and production-grade error handling. 

Your goal is to design a robust, scalable AI Agent workflow for: [DESCRIBE YOUR USE CASE].

### 1. CONTEXT ABOUT THE BUILD:
- **Core Objective:** [e.g., Automate customer support and update Notion]
- **Inputs/Triggers:** [e.g., Webhook, Typeform, Gmail]
- **Data Sources & Tools:** [e.g., Pinecone for RAG, Google Sheets for pricing, Slack for notifications]
- **Target AI Model:** [e.g., Claude 3.5 Sonnet, GPT-4o]
- **Complexity:** [Beginner/Intermediate/Advanced]

### 2. ARCHITECTURAL REQUIREMENTS:
- **Agent Type:** Use the "AI Agent" node (Reasoning/Tool-use) rather than a simple linear chain.
- **Modularity:** Design for "Sub-workflow as a Tool" architecture to keep the main canvas clean.
- **Memory:** Implement appropriate memory (Buffer Window or Postgres for long-term).
- **Resilience:** Include Error Trigger workflows and "Stop on Fail" logic for API calls.
- **Data Handling:** Use the latest n8n expression syntax (v2) and ensure data is sanitized.

### 3. DELIVERABLES:
#### A. High-Level Blueprint
Describe the logical flow from Trigger → Agent → Tools → Output.

#### B. The "Tooling" Strategy
List specific n8n tools the Agent will have access to (e.g., Custom tool for DB lookup, Calculator, etc.).

#### C. Node-by-Node Configuration
Provide the specific settings for:
1. **Trigger Node** (including specific JSON body examples)
2. **AI Agent Node** (Prompting strategy: System message, Tools assigned)
3. **Model & Memory Nodes** (Recommended temperature and window size)
4. **Tool Nodes** (Sub-workflow configurations)

#### D. The Code / JSON Structure
Provide the JSON structure for the workflow. *Note: Ensure you use the modern n8n format where node connections are clearly defined.*

#### E. Production Checklist
- Environment variables needed (API Keys).
- Data Pinning instructions for testing.
- Rate limiting and retry settings.

### 4. CONSTRAINTS:
- No "Demo" logic; if a database is needed, assume a production connection.
- Prioritize the "AI Agent" node over "Basic LLM Chain" for flexibility.
- Ensure the prompt within the Agent is optimized using Chain-of-Thought instructions.

Start by asking 3-5 clarifying questions to ensure the architecture matches my specific environment. Once I answer, provide the full implementation plan.
```

---

## Quick Reference Variables

| Placeholder | Description | Example Values |
|-------------|-------------|----------------|
| `[DESCRIBE YOUR USE CASE]` | Main automation objective | "AI-powered email classifier and responder" |
| `[Core Objective]` | What the workflow achieves | "Automate customer support and update Notion" |
| `[Inputs/Triggers]` | How the workflow starts | "Webhook, Typeform, Gmail, Slack" |
| `[Data Sources & Tools]` | External systems to connect | "Pinecone, Google Sheets, Airtable, Slack" |
| `[Target AI Model]` | LLM to use | "Claude 3.5 Sonnet, GPT-4o, GPT-4o-mini" |
| `[Complexity]` | Skill level required | "Beginner / Intermediate / Advanced" |

---

## Usage Instructions

1. **Copy the Master Prompt** above
2. **Fill in the placeholders** with your specific use case details
3. **Submit to your AI assistant** (Claude, ChatGPT, etc.)
4. **Answer the clarifying questions** the AI will ask
5. **Receive your full implementation plan** with JSON workflow structure

---

## What Was Improved in v2.0 (2025 n8n Updates)

| Update | Why It Matters |
|--------|----------------|
| **AI Agent Node vs LLM Chain** | The AI Agent node allows dynamic tool selection instead of linear execution |
| **Sub-workflows as Tools** | Modern architecture keeps the main canvas clean and modular |
| **Advanced Memory** | Buffer Window for sessions, Postgres for long-term persistence |
| **Data Pinning** | Debug without burning API credits |
| **Expression Syntax v2** | Uses `{{ $json.field }}` to avoid "Node not found" errors |

---

## How to Import the Generated JSON

1. Copy the JSON output from the AI
2. Open your n8n canvas
3. Press `Cmd+V` (Mac) or `Ctrl+V` (Windows)
4. Nodes will appear automatically
5. Connect your credentials

---

## Related Prompts in This Bank

| Prompt | Location | Best For |
|--------|----------|----------|
| Dynamic Builder | `/meta-prompts/dynamic-builder.md` | When you're not sure what you need |
| Dynamic Agent v3.0 | `/meta-prompts/dynamic-agent-v3.md` | Self-routing agents with MCP |
| Basic Tier | `/tiers/01-basic-linear-task-master.md` | Simple automations |
| Intermediate Tier | `/tiers/02-intermediate-multi-tool.md` | Multi-tool orchestration |
| Advanced Tier | `/tiers/03-advanced-autonomous-empire.md` | Production-grade systems |

---

## Version History

| Version | Date | Changes |
|---------|------|---------|
| 2.0.0 | 2025-12-23 | Updated for 2025 n8n architecture, added improvements section |
| 1.0.0 | 2025-12-23 | Initial master prompt creation |
