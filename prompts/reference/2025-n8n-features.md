# 📚 2025 n8n Features Reference

> A quick reference guide for the latest n8n features used in these prompts

---

## Key 2025 Updates Summary

| Feature | Description | Why It Matters |
|---------|-------------|----------------|
| AI Agent Node | Central reasoning engine for agentic workflows | Replaces linear chains with dynamic tool selection |
| Sub-workflows as Tools | Modular architecture pattern | Keeps main canvas clean, enables reuse |
| Expression Syntax v2 | `{{ $json.field }}` format | More reliable, cleaner code |
| Data Pinning | Freeze input data for testing | Test AI logic without burning API credits |
| Postgres Memory | Long-term conversation persistence | Remember users across sessions |
| Window Buffer Memory | Short-term context management | Maintain conversation flow |
| MCP Integration | Model Context Protocol servers | Direct integration with external services |
| Error Trigger Workflows | Global error handling | Self-healing and alerting |

---

## AI Agent Node vs LLM Chain

### ❌ Old Way: Basic LLM Chain
```
Trigger → LLM Chain → Action
```
- Linear execution
- No tool selection
- Limited flexibility

### ✅ 2025 Way: AI Agent Node
```
Trigger → AI Agent → [Dynamic Tool Selection] → Action
```
- Reasoning capability
- Multiple tools available
- Agent decides what to call

---

## Expression Syntax v2

### Old Syntax (Avoid)
```javascript
// Don't use these
{{$node["Node Name"].json["field"]}}
{{$item(0).$node["Node Name"].json["field"]}}
```

### New Syntax (Use This)
```javascript
// Modern n8n expressions
{{ $json.field }}
{{ $json.nested.field }}
{{ $json.array[0].field }}
{{ $('Node Name').item.json.field }}

// Built-in variables
{{ $today }}                    // Current date
{{ $now }}                      // Current timestamp
{{ $env.VARIABLE_NAME }}        // Environment variable
{{ $execution.id }}             // Current execution ID
{{ $workflow.id }}              // Workflow ID
{{ $workflow.name }}            // Workflow name
```

### Common Expression Patterns
```javascript
// Conditional
{{ $json.status === 'active' ? 'Yes' : 'No' }}

// String manipulation
{{ $json.name.toLowerCase() }}
{{ $json.email.split('@')[0] }}

// Array operations
{{ $json.items.length }}
{{ $json.items.map(i => i.name).join(', ') }}

// Default values
{{ $json.optional ?? 'default' }}

// JSON stringify for nested data
{{ JSON.stringify($json.complex_object) }}
```

---

## Data Pinning

### What It Is
Freeze real data from a workflow execution to use repeatedly during development.

### How to Use
1. Run your workflow with real data
2. Click on the trigger node
3. Click the 📌 **Pin** icon
4. The data is now frozen
5. Subsequent executions use pinned data

### Benefits
- Test AI logic without re-triggering events
- Save API credits during development
- Consistent test data
- Faster iteration cycles

### Best Practices
```markdown
✅ Pin realistic production-like data
✅ Pin edge cases for testing
✅ Unpin before going to production
❌ Don't pin sensitive data in shared workflows
❌ Don't forget to unpin when testing is complete
```

---

## Memory Types

### Buffer Window Memory
```javascript
{
  "type": "bufferWindowMemory",
  "k": 5  // Keep last 5 messages
}
```
**Use for:** Short conversations, support chats

### Buffer Memory
```javascript
{
  "type": "bufferMemory"
  // Keeps entire conversation
}
```
**Use for:** Single-session deep conversations

### Postgres Memory
```javascript
{
  "type": "postgresMemory",
  "sessionId": "{{ $json.user_id }}",
  "tableName": "chat_memory"
}
```
**Use for:** Long-term persistence, multi-day conversations

### Redis Memory
```javascript
{
  "type": "redisMemory",
  "sessionId": "{{ $json.session_id }}",
  "ttl": 86400  // 24 hours
}
```
**Use for:** High-performance, auto-expiring sessions

---

## Sub-workflow as Tool Pattern

### Main Workflow Structure
```
┌────────────────────────────────────────┐
│           Main Workflow                 │
│                                         │
│  Trigger → AI Agent → Response         │
│               │                         │
│               ├── Tool: Search         │
│               ├── Tool: Update         │
│               └── Tool: Notify         │
└────────────────────────────────────────┘
```

### Sub-workflow Structure
```
┌────────────────────────────────────────┐
│        Sub-workflow: Search             │
│                                         │
│  Execute Workflow Trigger               │
│            │                            │
│            ▼                            │
│     Parse Input Parameters              │
│            │                            │
│            ▼                            │
│       Do The Work                       │
│            │                            │
│            ▼                            │
│     Format Output JSON                  │
└────────────────────────────────────────┘
```

### Tool Configuration in AI Agent
```javascript
{
  "tools": [
    {
      "type": "workflow",
      "workflowId": "abc123",
      "name": "search_database",
      "description": "Search the customer database by email or order ID",
      "parameters": {
        "type": "object",
        "properties": {
          "email": { "type": "string" },
          "order_id": { "type": "string" }
        }
      }
    }
  ]
}
```

---

## Error Handling Patterns

### Stop on Fail
```javascript
// Node settings
{
  "continueOnFail": false,
  "onError": "stopWorkflow"
}
```

### Continue on Fail
```javascript
{
  "continueOnFail": true,
  "onError": "continueRegularOutput"
}
```

### Error Trigger Workflow
```javascript
// Separate workflow that catches all errors
{
  "trigger": "errorTrigger",
  "actions": [
    "logToDatabase",
    "sendSlackAlert",
    "attemptRetry"
  ]
}
```

### Retry Pattern
```javascript
{
  "retry": {
    "enabled": true,
    "maxTries": 3,
    "waitBetweenTries": 2000  // ms
  }
}
```

---

## MCP (Model Context Protocol)

### What It Is
A standardized way for AI models to interact with external tools and data sources.

### Available MCP Servers
```markdown
- Filesystem: Read/write local files
- PostgreSQL: Direct database queries
- GitHub: Repository management
- Google Drive: Document access
- Slack: Team communication
- Browserbase: Web browsing
```

### Using MCP in n8n
```javascript
// MCP Tool configuration
{
  "type": "mcp",
  "server": "postgresql",
  "config": {
    "connectionString": "{{ $env.DATABASE_URL }}"
  }
}
```

---

## Model Recommendations

### For Different Use Cases

| Use Case | Model | Temperature |
|----------|-------|-------------|
| Classification | GPT-4o-mini | 0.0-0.2 |
| Customer Support | Claude 3.5 Sonnet | 0.3-0.5 |
| Content Generation | GPT-4o | 0.7-0.9 |
| Code Generation | Claude 3.5 Sonnet | 0.2-0.4 |
| Research/Analysis | GPT-4o | 0.3-0.5 |
| Creative Writing | Claude 3.5 Sonnet | 0.8-1.0 |

### Cost Optimization
```markdown
1. Use GPT-4o-mini for simple tasks (10x cheaper)
2. Cache frequent queries
3. Limit context window size
4. Use streaming for long responses
5. Batch similar requests when possible
```

---

## Production Best Practices

### Security
```markdown
✅ Use environment variables for all secrets
✅ Sanitize all user inputs
✅ Validate JSON schemas
✅ Implement rate limiting
✅ Log all agent actions for audit
❌ Never hardcode API keys
❌ Never log sensitive data
```

### Performance
```markdown
✅ Use connection pooling for databases
✅ Implement caching for RAG results
✅ Use async patterns for long operations
✅ Monitor response times
✅ Set appropriate timeouts
```

### Reliability
```markdown
✅ Implement retry logic with exponential backoff
✅ Use circuit breakers for external APIs
✅ Set up health checks
✅ Create runbooks for common failures
✅ Test with chaos engineering
```

---

## Quick Reference: Node Settings

### AI Agent Node
```javascript
{
  "agent": "conversationalAgent",
  "model": "claude-3-5-sonnet",
  "systemMessage": "...",
  "temperature": 0.3,
  "maxTokens": 4000,
  "tools": [...],
  "memory": {...}
}
```

### Webhook Node
```javascript
{
  "httpMethod": "POST",
  "path": "my-webhook",
  "responseMode": "lastNode",
  "authentication": "headerAuth"
}
```

### IF Node
```javascript
{
  "conditions": {
    "boolean": [
      {
        "value1": "={{ $json.status }}",
        "operation": "equals",
        "value2": "approved"
      }
    ]
  }
}
```
