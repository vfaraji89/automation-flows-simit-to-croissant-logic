# 🟡 Tier 2: Multi-Tool Orchestrator (Intermediate)

> **Complexity:** Intermediate  
> **Build Time:** 2-4 hours  
> **Best For:** Workflows that need to "decide" what to do

---

## Overview

The Multi-Tool Orchestrator is for automations where the AI Agent needs to choose between different actions based on context. This is where n8n's Sub-workflow as Tool architecture shines.

### Perfect Use Cases
- ✅ Customer support with order lookup + FAQ responses
- ✅ Sales assistant that checks CRM + sends personalized emails
- ✅ Data enrichment from multiple sources
- ✅ Smart routing between departments
- ✅ Multi-step research and synthesis

### Not Suitable For
- ❌ Simple one-way data transformation (use Tier 1)
- ❌ Production systems needing 99.9% uptime (use Tier 3)
- ❌ Complex RAG with vector databases (use Tier 3)

---

## The Prompt

```markdown
Act as a Senior n8n Solutions Architect. Design a dynamic AI Agent workflow for: [USE CASE].

### CORE ARCHITECTURE:
- **Central Brain:** Use the 'AI Agent' node (Reasoning Engine).
- **Tools:** The Agent must have access to 2-3 'Sub-workflow Tools' (e.g., 'Tool A' for Database lookups, 'Tool B' for writing to a CRM).
- **Memory:** Implement 'Window Buffer Memory' so the agent remembers the last 5 interactions.

### DYNAMIC LOGIC:
- Explain how the Agent should choose between the available tools.
- Provide the configuration for the 'Call n8n Workflow' tool nodes.
- Include data transformation logic using n8n expressions {{ $json.field }} to pass data between the agent and tools.

### DELIVERABLES:
- Architecture diagram description.
- Detailed "Tool Descriptions" (The instructions the Agent uses to know when to call a sub-workflow).
- JSON structure for the main workflow and the tool sub-workflows.
- Debugging guide for "Tool Call" failures.

Start by asking me which 3 external apps/APIs I need to integrate.
```

---

## Architecture Diagram

```
                              ┌─────────────────────┐
                              │    Sub-workflow:    │
                         ┌───▶│   Database Lookup   │
                         │    └─────────────────────┘
                         │
┌──────────┐    ┌────────┴────────┐    ┌─────────────────────┐
│ Trigger  │───▶│    AI Agent     │───▶│   Sub-workflow:     │
│          │    │  (Orchestrator) │    │   CRM Update        │
└──────────┘    └────────┬────────┘    └─────────────────────┘
                         │
                         │    ┌─────────────────────┐
                         └───▶│   Sub-workflow:     │
                              │   Send Notification │
                              └─────────────────────┘
                                        │
                                        ▼
                              ┌─────────────────────┐
                              │   Window Buffer     │
                              │      Memory         │
                              └─────────────────────┘
```

---

## Placeholder Reference

| Placeholder | Description | Examples |
|-------------|-------------|----------|
| `[USE CASE]` | Main automation goal | "Customer support agent with order lookup" |
| `[Tool A]` | First sub-workflow | "Shopify Order Lookup" |
| `[Tool B]` | Second sub-workflow | "Zendesk Ticket Creation" |
| `[Tool C]` | Third sub-workflow | "Slack Escalation" |

---

## Example: Customer Support Agent

### Filled-In Prompt

```markdown
Act as a Senior n8n Solutions Architect. Design a dynamic AI Agent workflow for: Customer support that answers questions, looks up orders in Shopify, and escalates complex issues to humans.

### CORE ARCHITECTURE:
- **Central Brain:** Use the 'AI Agent' node (Reasoning Engine).
- **Tools:** The Agent must have access to 3 'Sub-workflow Tools':
  - 'Shopify Lookup' for order status
  - 'FAQ Search' for common questions
  - 'Escalate to Human' for complex issues
- **Memory:** Implement 'Window Buffer Memory' so the agent remembers the last 5 interactions.

### DYNAMIC LOGIC:
- Explain how the Agent should choose between the available tools.
- Provide the configuration for the 'Call n8n Workflow' tool nodes.
- Include data transformation logic using n8n expressions {{ $json.field }} to pass data between the agent and tools.

### DELIVERABLES:
- Architecture diagram description.
- Detailed "Tool Descriptions" (The instructions the Agent uses to know when to call a sub-workflow).
- JSON structure for the main workflow and the tool sub-workflows.
- Debugging guide for "Tool Call" failures.

Start by asking me which 3 external apps/APIs I need to integrate.
```

---

## Tool Description Templates

The AI Agent uses these descriptions to decide WHEN to call each tool:

### Database Lookup Tool
```markdown
**Tool Name:** lookup_order

**Description:** Use this tool when the user asks about an order, shipment, delivery status, or tracking. Requires an order ID or email address.

**Input Schema:**
{
  "order_id": "string (optional)",
  "email": "string (optional)"
}

**When to Use:**
- User mentions "order", "shipment", "tracking", "delivery"
- User provides an order number (format: #12345)
- User asks "where is my order"
```

### CRM Update Tool
```markdown
**Tool Name:** update_customer

**Description:** Use this tool to update customer information in the CRM after resolving their issue. Always call this after a successful resolution.

**Input Schema:**
{
  "customer_email": "string",
  "resolution_summary": "string",
  "satisfaction_score": "number (1-5)"
}

**When to Use:**
- After successfully answering a question
- After resolving a complaint
- When customer confirms issue is resolved
```

### Escalation Tool
```markdown
**Tool Name:** escalate_to_human

**Description:** Use this tool when you cannot resolve the issue, the customer is frustrated, or the request requires human judgment (refunds over $100, account changes).

**Input Schema:**
{
  "reason": "string",
  "priority": "low|medium|high|urgent",
  "conversation_summary": "string"
}

**When to Use:**
- Customer expresses frustration (uses caps, exclamation marks)
- Issue requires policy exception
- You don't have enough information after 2 clarifying questions
- Customer explicitly asks for a human
```

---

## Memory Configuration

### Window Buffer Memory Settings

```javascript
// Recommended settings for Tier 2
{
  "memoryType": "bufferWindowMemory",
  "windowSize": 5,  // Remember last 5 exchanges
  "returnMessages": true,
  "inputKey": "input",
  "outputKey": "output"
}
```

### When to Use What Memory

| Memory Type | Use Case | Persistence |
|-------------|----------|-------------|
| Buffer Window | Short conversations (support chat) | Session only |
| Buffer | Full conversation history | Session only |
| Postgres | Need to remember across days/weeks | Permanent |

---

## Node Configuration Checklist

### 1. Main Workflow: AI Agent Node
- [ ] Select model (Claude 3.5 Sonnet recommended)
- [ ] Temperature: 0.3-0.5 (balanced reasoning)
- [ ] Add System Prompt with role and constraints
- [ ] Connect Window Buffer Memory
- [ ] Add all tool nodes

### 2. Sub-workflow: Database Lookup
- [ ] Trigger: "Execute Workflow" (not Webhook)
- [ ] Input: Parse `{{ $json.order_id }}` and `{{ $json.email }}`
- [ ] Connect to Shopify/Database
- [ ] Return structured JSON response
- [ ] Add error handling for "not found"

### 3. Sub-workflow: CRM Update
- [ ] Trigger: "Execute Workflow"
- [ ] Input: Customer data from main workflow
- [ ] Connect to CRM (HubSpot, Salesforce, etc.)
- [ ] Return confirmation
- [ ] Log update for audit

### 4. Sub-workflow: Escalation
- [ ] Trigger: "Execute Workflow"
- [ ] Create ticket in helpdesk
- [ ] Send Slack notification to team
- [ ] Return ticket ID to agent

### 5. Call n8n Workflow Tool Nodes
- [ ] One for each sub-workflow
- [ ] Set correct workflow ID
- [ ] Write clear tool descriptions
- [ ] Define input schema

---

## Expression Examples

### Passing Data to Tools
```javascript
// In the tool call
{{ $json.customer_email }}
{{ $json.order_id }}
```

### Formatting Tool Response for Agent
```javascript
// In sub-workflow output
{
  "status": "found",
  "order": {
    "id": "{{ $json.order.id }}",
    "status": "{{ $json.order.fulfillment_status }}",
    "tracking": "{{ $json.order.tracking_number }}"
  }
}
```

### Conditional Logic
```javascript
// In IF node
{{ $json.priority === "urgent" }}
{{ $json.attempts > 2 }}
```

---

## Debugging Guide

### Common Tool Call Failures

| Error | Cause | Solution |
|-------|-------|----------|
| "Tool not found" | Workflow ID mismatch | Verify sub-workflow IDs |
| "Invalid input" | Schema mismatch | Check input JSON structure |
| "Timeout" | Sub-workflow too slow | Add timeout handling, optimize queries |
| "Agent loops" | Poor tool descriptions | Make descriptions more specific |
| "Wrong tool called" | Ambiguous descriptions | Add "When NOT to use" examples |

### Debug Mode Checklist
1. [ ] Pin data on trigger node
2. [ ] Enable "Always Output Data" on all nodes
3. [ ] Check execution log for tool calls
4. [ ] Verify sub-workflow inputs match expected schema
5. [ ] Test each sub-workflow independently first

---

## Ready to Level Up?

When you need:
- Vector database for RAG
- Self-healing error recovery
- Long-term persistent memory
- Human-in-the-loop approvals
- Production-grade reliability

→ Move to **Tier 3: Autonomous Agent Empire**
