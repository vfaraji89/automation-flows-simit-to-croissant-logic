# 🟢 Tier 1: Linear Task Master (Basic)

> **Complexity:** Beginner  
> **Build Time:** ~30 minutes  
> **Best For:** Simple, one-way automations

---

## Overview

The Linear Task Master is for straightforward automations where data flows in one direction without complex decision-making.

### Perfect Use Cases
- ✅ Email categorization and tagging
- ✅ Lead scoring from form submissions
- ✅ Notification drafting and sending
- ✅ Data summarization
- ✅ Simple content transformation

### Not Suitable For
- ❌ Multi-step decision trees
- ❌ Workflows requiring tool selection
- ❌ Long-running conversations with memory
- ❌ Complex error recovery

---

## The Prompt

```markdown
Act as an n8n Workflow Expert. Build a basic AI-powered automation for: [USE CASE].

### WORKFLOW STRUCTURE:
1. **Trigger:** [e.g., New Email in Gmail / New Row in Google Sheets]
2. **AI Processor:** Use the 'AI Agent' node with a simple "System Message" to process the input.
3. **Action:** [e.g., Send Slack Message / Update CRM]

### TECHNICAL REQUIREMENTS:
- Use the basic AI Agent node (No complex tools needed).
- Provide a clean System Prompt for the AI to transform [Input Data] into [Desired Format].
- Include a simple 'IF' node to check if the AI output meets specific criteria.

### DELIVERABLES:
- Step-by-step node configuration instructions.
- The exact System Prompt to use inside the Agent node.
- A checklist for connecting the API credentials.

Start by asking what the specific input and output should be.
```

---

## Architecture Diagram

```
┌─────────────┐    ┌─────────────┐    ┌─────────────┐    ┌─────────────┐
│   Trigger   │───▶│  AI Agent   │───▶│  IF Node    │───▶│   Action    │
│  (Webhook,  │    │  (Process)  │    │  (Validate) │    │  (Output)   │
│   Gmail)    │    │             │    │             │    │             │
└─────────────┘    └─────────────┘    └─────────────┘    └─────────────┘
```

---

## Placeholder Reference

| Placeholder | Description | Examples |
|-------------|-------------|----------|
| `[USE CASE]` | What you're automating | "Categorize support emails" |
| `[Trigger]` | What starts the workflow | "New Email in Gmail", "Webhook" |
| `[Input Data]` | What the AI receives | "Email body", "Form response" |
| `[Desired Format]` | What the AI outputs | "JSON with category and priority" |
| `[Action]` | What happens at the end | "Send Slack message", "Update sheet" |

---

## Example: Email Categorizer

### Filled-In Prompt

```markdown
Act as an n8n Workflow Expert. Build a basic AI-powered automation for: Categorizing incoming support emails into 'Billing', 'Technical', 'Sales', or 'Other'.

### WORKFLOW STRUCTURE:
1. **Trigger:** New Email in Gmail with label "Support"
2. **AI Processor:** Use the 'AI Agent' node with a simple "System Message" to process the input.
3. **Action:** Add a label to the email based on category and send summary to Slack.

### TECHNICAL REQUIREMENTS:
- Use the basic AI Agent node (No complex tools needed).
- Provide a clean System Prompt for the AI to transform the email body into a JSON with 'category' and 'confidence' fields.
- Include a simple 'IF' node to check if confidence is above 0.8.

### DELIVERABLES:
- Step-by-step node configuration instructions.
- The exact System Prompt to use inside the Agent node.
- A checklist for connecting the API credentials.

Start by asking what the specific input and output should be.
```

---

## Sample System Prompt (for AI Agent Node)

```markdown
You are an email classification assistant. Analyze the email content and categorize it.

## Your Task:
1. Read the email carefully
2. Determine the primary category
3. Assign a confidence score

## Categories:
- **Billing**: Payment issues, invoices, refunds, subscription changes
- **Technical**: Bugs, errors, how-to questions, feature requests
- **Sales**: Pricing inquiries, demos, enterprise plans
- **Other**: Everything else

## Output Format (JSON only):
{
  "category": "Billing|Technical|Sales|Other",
  "confidence": 0.0-1.0,
  "reasoning": "Brief explanation"
}

Do not include any text outside the JSON object.
```

---

## Node Configuration Checklist

### 1. Trigger Node (Gmail)
- [ ] Connect Gmail credentials
- [ ] Set label filter (if applicable)
- [ ] Enable polling or use webhook
- [ ] Test with a sample email

### 2. AI Agent Node
- [ ] Select model (Claude 3.5 Sonnet / GPT-4o-mini)
- [ ] Paste System Prompt
- [ ] Set temperature to 0.3 (more consistent)
- [ ] No tools needed for basic tier

### 3. IF Node
- [ ] Condition: `{{ $json.confidence }}` > 0.8
- [ ] True path: Continue to action
- [ ] False path: Send to manual review

### 4. Action Node (Slack)
- [ ] Connect Slack credentials
- [ ] Select channel
- [ ] Format message with AI output

---

## Common Issues & Fixes

| Issue | Cause | Fix |
|-------|-------|-----|
| AI returns text instead of JSON | Weak system prompt | Add "Output JSON only, no other text" |
| Trigger not firing | Polling interval too long | Reduce to 1 minute or use webhook |
| IF node fails | Expression syntax | Use `{{ $json.fieldName }}` format |
| Slow response | Large model | Switch to GPT-4o-mini for speed |

---

## Ready to Level Up?

When you need:
- Multiple tools for the AI to choose from
- Memory across conversations
- More complex routing logic

→ Move to **Tier 2: Multi-Tool Orchestrator**
