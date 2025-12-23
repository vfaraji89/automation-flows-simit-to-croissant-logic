# 🧠 Dynamic Builder Meta-Prompt

> **Purpose:** When you don't know exactly what you need, use this prompt to have the AI interview you and dynamically generate the perfect custom prompt for your situation.

---

## The Meta-Prompt

```markdown
I want to build a dynamic n8n AI automation. Instead of me giving you a static use case, I want you to act as a Senior n8n Solutions Architect. 

Ask me 5 targeted questions about:
1. The business outcome I want.
2. The specific "bottlenecks" where human decision-making is currently needed.
3. My existing tech stack (APIs, DBs, etc.).
4. The "unpredictable" parts of the data (What changes every time?).
5. My desired level of autonomy (Human-in-the-loop vs. Full Auto).

Once I answer, dynamically generate a custom "Mega Prompt" tailored specifically for my situation that utilizes the 2025 n8n AI Agent node and Sub-workflow Tool architecture.
```

---

## When to Use This

| Scenario | Use Dynamic Builder? |
|----------|---------------------|
| "I know I need AI automation but don't know where to start" | ✅ Yes |
| "I have a vague idea but need help defining scope" | ✅ Yes |
| "I know exactly what I want to build" | ❌ Use tiered prompts instead |
| "I need to explore multiple automation possibilities" | ✅ Yes |

---

## What You'll Get

After answering the 5 questions, the AI will generate:

1. **Custom-tailored prompt** specific to your use case
2. **Recommended architecture tier** (Basic/Intermediate/Advanced)
3. **Suggested tools and integrations** based on your tech stack
4. **Risk assessment** for your desired autonomy level

---

## Example Conversation Flow

**AI Asks:**
> 1. What business outcome do you want?

**You Answer:**
> "I want to automatically respond to customer support emails, look up their order in Shopify, and escalate complex issues to a human."

**AI Asks:**
> 2. Where is human decision-making currently a bottleneck?

**You Answer:**
> "Deciding if an email is a simple FAQ or needs investigation. Also approving refunds over $100."

*...continues through all 5 questions...*

**AI Generates:**
> A fully customized prompt combining elements from the Intermediate and Advanced tiers, with specific Shopify integration, refund approval gates, and FAQ RAG system.

---

## Pro Tips

1. **Be specific with your bottlenecks** - The more detail you give about where humans slow things down, the better the automation design.

2. **List ALL your tools** - Even if you think they're not relevant. The AI might find creative ways to connect them.

3. **Be honest about autonomy** - If you're nervous about full automation, say so. Human-in-the-loop is perfectly valid.

4. **Mention scale** - "10 emails/day" vs "1000 emails/day" requires different architectures.

---

## Related Prompts

- After generating your custom prompt, you may want to reference:
  - `tiers/02-intermediate-multi-tool.md` for tool configuration details
  - `tiers/03-advanced-autonomous-empire.md` for production hardening
  - `reference/2025-n8n-features.md` for implementation specifics
