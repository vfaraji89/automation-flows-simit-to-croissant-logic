# 🥯 n8n Automation Use Cases

> **The Simit-to-Croissant Framework** — A philosophy for building AI automation with n8n

[![n8n](https://img.shields.io/badge/n8n-Automation-orange?style=flat-square&logo=n8n)](https://n8n.io)
[![AI Powered](https://img.shields.io/badge/AI-Powered-blue?style=flat-square&logo=openai)](https://openai.com)
[![License](https://img.shields.io/badge/License-MIT-green?style=flat-square)](LICENSE)

---

## 🎯 What is This?

A comprehensive collection of **prompts**, **templates**, and **documentation** for building AI-powered automation workflows with n8n. This repository follows the **Simit-to-Croissant** philosophy:

| Phase | Analogy | Focus |
|-------|---------|-------|
| 🥯 **Simit** | Simple, local, satisfying | Start with immediate needs |
| 🥐 **Croissant** | Layered, refined, sophisticated | Scale with security |

---

## 📁 Repository Structure

```
n8n-automation-usecase/
├── 📖 README.md                          # You are here
├── 📂 docs/
│   └── simit-to-croissant-deck.md        # Framework presentation with diagrams
└── 📂 prompts/
    ├── README.md                          # Prompt bank navigation
    ├── master-prompt.md                   # Original v2.0 master prompt
    ├── 📂 meta-prompts/
    │   ├── dynamic-builder.md             # Interview-style prompt generator
    │   └── dynamic-agent-v3.md            # v3.0 Dynamic Agent (2025)
    ├── 📂 tiers/
    │   ├── 01-basic-linear-task-master.md      # 🟢 Simple automations
    │   ├── 02-intermediate-multi-tool.md       # 🟡 Multi-tool orchestration
    │   └── 03-advanced-autonomous-empire.md    # 🔴 Production-grade agents
    └── 📂 reference/
        └── 2025-n8n-features.md           # Key features & best practices
```

---

## 🚀 Quick Start

### 1. Choose Your Tier

| Complexity | Prompt | Best For | Build Time |
|------------|--------|----------|------------|
| 🟢 Basic | [Linear Task Master](prompts/tiers/01-basic-linear-task-master.md) | Email categorization, notifications | 30 min |
| 🟡 Intermediate | [Multi-Tool Orchestrator](prompts/tiers/02-intermediate-multi-tool.md) | Customer support, CRM updates | 2-4 hours |
| 🔴 Advanced | [Autonomous Agent Empire](prompts/tiers/03-advanced-autonomous-empire.md) | RAG systems, research agents | 1-2 days |
| 🔵 Meta | [Dynamic Builder](prompts/meta-prompts/dynamic-builder.md) | When you don't know where to start | Varies |

### 2. Copy the Prompt

Navigate to the appropriate tier file and copy the prompt template.

### 3. Customize

Fill in the `[PLACEHOLDERS]` with your specific use case details.

### 4. Generate with AI

Paste into **Claude 3.5 Sonnet** or **GPT-4o** and follow the interactive process.

### 5. Import to n8n

Copy the generated JSON workflow and paste it into your n8n canvas (`Cmd+V` / `Ctrl+V`).

---

## 📚 Documentation

### The Simit-to-Croissant Framework

Read the full philosophy and see visual diagrams:

👉 [**Simit-to-Croissant Deck**](docs/simit-to-croissant-deck.md)

**Key Concepts:**
- 🥯 Start simple, solve immediate pain points
- 🔄 Iterate continuously, automation is not "set and forget"
- 🔐 Harden for enterprise with security-first approach
- 🥐 Scale to sophisticated multi-agent systems

---

## 🛠️ 2025 n8n Features

This repository is optimized for the latest n8n capabilities:

| Feature | Description |
|---------|-------------|
| **AI Agent Node** | Central reasoning engine replacing linear chains |
| **Sub-workflows as Tools** | Modular architecture for clean canvas |
| **Expression Syntax v2** | `{{ $json.field }}` format |
| **Data Pinning** | Test without burning API credits |
| **Postgres Memory** | Long-term conversation persistence |
| **MCP Integration** | Model Context Protocol servers |

See the full reference: [2025 n8n Features](prompts/reference/2025-n8n-features.md)

---

## 💡 Use Cases

### SEO & Marketing
- Automated keyword detection
- AI article writing pipelines
- Competitor tracking systems

### Video Production
- Script generation with AI
- Leonardo AI + ElevenLabs integration
- "Faceless" content automation

### Customer Support
- Sentiment analysis agents
- Auto-resolve vs. human escalation
- Multi-channel support bots

---

## 🔐 Security Best Practices

Following n8n 2.0 hardening principles:

- ✅ Isolated task runners for code execution
- ✅ Role-Based Access Control (RBAC)
- ✅ Self-hosting recommendations (VPS/Docker)
- ✅ Encrypted credentials management
- ✅ Audit logging

---

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 🙏 Acknowledgments

- [n8n.io](https://n8n.io) — The workflow automation platform
- [Anthropic Claude](https://anthropic.com) — AI assistance
- [OpenAI](https://openai.com) — AI models and embeddings

---

## 📬 Contact

**Vahid Faraji**

- GitHub: [@vfaraji89](https://github.com/vfaraji89)

---

<p align="center">
  <i>"The best automation is the one that solves a real problem today, while being architected for the challenges of tomorrow."</i>
  <br><br>
  <b>— The Simit-to-Croissant Philosophy</b>
</p>
