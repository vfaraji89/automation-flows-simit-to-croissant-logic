# 🚀 N8N AI Empire Prompt Bank

> **Version:** 3.0 (2025 Edition)  
> **Last Updated:** December 23, 2025

A comprehensive collection of AI prompts for building n8n agentic workflows, organized by complexity and use case.

---

## 📁 Prompt Bank Structure

```
prompts/
├── README.md                          # This file
├── master-prompt.md                   # Original v2.0 master prompt
├── meta-prompts/
│   ├── dynamic-builder.md             # Interview-style prompt generator
│   └── dynamic-agent-v3.md            # v3.0 Dynamic Agent (2025)
├── tiers/
│   ├── 01-basic-linear-task-master.md      # Simple automations
│   ├── 02-intermediate-multi-tool.md       # Multi-tool orchestration
│   └── 03-advanced-autonomous-empire.md    # Production-grade agents
└── reference/
    └── 2025-n8n-features.md           # Key features & best practices
```

---

## 🎯 Quick Selection Guide

| Complexity | Prompt | Best For | Time to Build |
|------------|--------|----------|---------------|
| 🟢 Basic | Linear Task Master | Email categorization, notifications | 30 min |
| 🟡 Intermediate | Multi-Tool Orchestrator | Customer support, CRM updates | 2-4 hours |
| 🔴 Advanced | Autonomous Agent Empire | RAG systems, research agents | 1-2 days |
| 🔵 Meta | Dynamic Builder | When you don't know where to start | Varies |

---

## 🔥 2025 n8n Key Updates

These prompts are optimized for the latest n8n features:

| Feature | Old Way | 2025 Way |
|---------|---------|----------|
| AI Processing | Basic LLM Chain | **AI Agent Node** (Reasoning/Tool-use) |
| Workflow Structure | 50 nodes on one canvas | **Sub-workflows as Tools** |
| Memory | None or simple | **Postgres/Redis Long-term Memory** |
| Variables | Old expression syntax | **{{ $json.field }}** v2 syntax |
| Testing | Manual API calls | **Data Pinning** |
| Integration | Custom HTTP requests | **MCP (Model Context Protocol)** |

---

## 🛠️ How to Use

### Step 1: Choose Your Tier
- **New to n8n?** → Start with `01-basic-linear-task-master.md`
- **Building integrations?** → Use `02-intermediate-multi-tool.md`
- **Production system?** → Go for `03-advanced-autonomous-empire.md`
- **Not sure?** → Use `meta-prompts/dynamic-builder.md`

### Step 2: Copy & Customize
1. Open the relevant prompt file
2. Copy the prompt template
3. Fill in the `[PLACEHOLDERS]` with your specifics
4. Paste into Claude 3.5 Sonnet or GPT-4o

### Step 3: Import to n8n
1. Copy the JSON output from the AI
2. Open your n8n canvas
3. Press `Cmd+V` (Mac) or `Ctrl+V` (Windows)
4. Connect your credentials

---

## 📊 Prompt Comparison Matrix

| Feature | Basic | Intermediate | Advanced |
|---------|-------|--------------|----------|
| AI Agent Node | ✅ | ✅ | ✅ |
| Sub-workflow Tools | ❌ | ✅ (2-3) | ✅ (5+) |
| Memory | ❌ | Buffer Window | Postgres |
| Error Handling | Basic IF | Tool retry | Self-healing |
| RAG/Vector Store | ❌ | Optional | ✅ |
| Human-in-the-Loop | ❌ | Optional | ✅ |
| MCP Integration | ❌ | ❌ | ✅ |

---

## 🔗 Related Resources

- [n8n Documentation](https://docs.n8n.io)
- [n8n AI Agent Guide](https://docs.n8n.io/integrations/builtin/cluster-nodes/root-nodes/n8n-nodes-langchain.agent/)
- [Model Context Protocol](https://modelcontextprotocol.io)

---

## 📝 Version History

| Version | Date | Changes |
|---------|------|---------|
| 3.0 | 2025-12-23 | Added tiered prompts, meta-prompts, MCP support |
| 2.0 | 2025-12-23 | Updated for 2025 n8n AI Agent architecture |
| 1.0 | 2025-12-23 | Initial master prompt |
