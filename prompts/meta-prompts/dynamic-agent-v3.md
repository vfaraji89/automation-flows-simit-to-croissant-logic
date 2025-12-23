# ⚡ Dynamic Agent Prompt v3.0 (2025 Edition)

> **Purpose:** For when you know your use case and want to build a truly dynamic, self-routing AI agent that decides its own path.

---

## The v3.0 Prompt

```markdown
You are a Lead AI Automation Engineer. Build a DYNAMIC AGENTIC WORKFLOW for [USE CASE].

### DYNAMIC ARCHITECTURE REQUIREMENTS (2025 Standard):
1. **Agentic Brain:** Use the 'AI Agent' node as the central orchestrator. Do not use linear chains.
2. **Dynamic Tooling:** Design 'Sub-workflows as Tools'. The Agent must call these based on the input context (e.g., if the user asks for a refund, it calls the 'Stripe Tool'; if they ask a question, it calls the 'RAG Tool').
3. **Dynamic Prompting:** Use n8n Expressions to inject real-time context (e.g., {{ $today }}, {{ $json.customerTier }}) into the Agent's System Message.
4. **Self-Healing:** Implement an 'Error Trigger' workflow that automatically attempts to re-route failed tasks.
5. **Memory:** Use 'Postgres Chat Memory' for long-term persistence, allowing the agent to remember user preferences across sessions.

### DELIVERABLES:
- **Logical Flow:** Map the decision tree (If X happens, Agent calls Tool Y).
- **JSON Structure:** Provide the modern n8n JSON (v2+ format) utilizing the "Call n8n Workflow" tool.
- **MCP Integration:** Suggest which Model Context Protocol (MCP) servers would enhance this (e.g., Google Drive MCP, GitHub MCP).
- **Testing Script:** A list of "stress test" scenarios to ensure the agent doesn't hallucinate.

### CONSTRAINTS:
- Use latest n8n expression syntax: {{ $json.field }} not old versions.
- Prioritize "Reasoning" models (Claude 3.5 Sonnet or GPT-4o).
- Include "Data Pinning" instructions for the trigger node to speed up development.
```

---

## Key Differences from v2.0

| Aspect | v2.0 | v3.0 |
|--------|------|------|
| Architecture Focus | Agent + Tools | **Dynamic Decision Trees** |
| Prompting | Static system message | **Expression-injected context** |
| Error Handling | Stop on Fail | **Self-Healing Loops** |
| Integration | Native n8n nodes | **MCP Server Integration** |
| Testing | Manual | **Stress Test Scenarios** |

---

## The 3 "Dynamic" Features You MUST Use

### 1. Sub-workflows as Tools

**Old Way:** One giant messy workflow with 50 nodes

**Dynamic Way:**
```
Main Agent Workflow
    ├── Tool: "Search Database" (Sub-workflow)
    ├── Tool: "Update CRM" (Sub-workflow)
    ├── Tool: "Send Notification" (Sub-workflow)
    └── Tool: "Generate Report" (Sub-workflow)
```

The AI Agent dynamically decides which tool to call based on the input.

### 2. Expressions in System Prompts

**Static (Old):**
```
You are a helpful assistant.
```

**Dynamic (2025):**
```
You are an assistant for {{ $json.company_name }}. 
The current priority is {{ $json.priority_level }}.
Customer tier: {{ $json.customerTier }}.
Today's date: {{ $today }}.
```

The agent's behavior changes based on incoming data!

### 3. Data Pinning for Iteration

**Why it matters:** Test your AI Agent 100 times against the same input without re-triggering the original event.

**How to use:**
1. Run your workflow once with real data
2. Click the trigger node
3. Click "Pin Data"
4. Now iterate on your AI logic without burning API credits

---

## MCP Integration Examples

Model Context Protocol servers that enhance your agent:

| MCP Server | Use Case |
|------------|----------|
| Google Drive MCP | Read/write documents dynamically |
| GitHub MCP | Manage repos, create issues, review PRs |
| Slack MCP | Advanced channel management |
| PostgreSQL MCP | Direct database queries |
| Filesystem MCP | Local file operations |

---

## Stress Test Scenarios Template

Include these in your testing:

```markdown
### Stress Test Scenarios

1. **Edge Case Input:** Send malformed or unexpected data
2. **Tool Failure:** Simulate API timeout on a sub-workflow
3. **Memory Overflow:** Send 50+ messages to test context limits
4. **Hallucination Check:** Ask about data that doesn't exist
5. **Concurrent Requests:** Fire 10 requests simultaneously
6. **Long Input:** Send a 5000-word message
7. **Injection Attempt:** Include prompt injection in user input
```

---

## Example Use Cases for v3.0

- **Customer Support Agent** that routes between FAQ lookup, order status, and human escalation
- **Research Agent** that searches multiple sources and synthesizes findings
- **Content Agent** that generates, reviews, and publishes across platforms
- **DevOps Agent** that monitors, diagnoses, and auto-remedies issues

---

## Quick Start

1. Copy the v3.0 prompt above
2. Replace `[USE CASE]` with your specific scenario
3. Paste into Claude 3.5 Sonnet or GPT-4o
4. Answer any clarifying questions
5. Import the generated JSON into n8n
