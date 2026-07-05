# Introduction to IBM Bob

---

## Overview

**IBM Bob** is an AI-powered coding assistant built specifically for enterprise developers. It works alongside you as an intelligent pair programmer — accessible via a web interface or integrated into your development environment. Unlike simple AI chatbots that only answer questions, Bob is an **Agentic AI** — it can read your code, make edits, run commands, and complete complex tasks autonomously.

---

## What is Bob?

| Aspect | Description |
|--------|-------------|
| **What** | AI-powered coding assistant |
| **Where** | Web interface or integrated development environment |
| **Who** | Built by IBM for enterprise developers |
| **How** | Uses enterprise LLMs + Agentic capabilities |
| **Why** | Accelerate mainframe development & modernization |

---

## Bob at a Glance

```
┌─────────────────────────────────────────────┐
│                   IBM BOB                     │
├─────────────────────────────────────────────┤
│                                              │
│  ┌──────────────┐    ┌───────────────────┐  │
│  │              │    │                   │  │
│  │  Your Code   │◄──►│    IBM Bob        │  │
│  │  (COBOL,JCL) │    │  (AI Assistant)   │  │
│  │              │    │                   │  │
│  └──────────────┘    └───────────────────┘  │
│                              │               │
│                              ▼               │
│                     ┌─────────────────┐      │
│                     │   Enterprise    │      │
│                     │   LLM Models    │      │
│                     └─────────────────┘      │
│                                              │
└─────────────────────────────────────────────┘
```

---

## Key Capabilities

### 1. Understands Mainframe Languages
- **COBOL** — reads, explains, writes, and refactors
- **JCL** — creates, debugs, and optimizes
- **PL/I** — analysis and assistance
- **Assembler** — understanding and documentation
- **DB2 SQL** — query optimization and debugging
- **CICS** — transaction analysis

### 2. Takes Actions (Agentic)
- Reads files from your workspace
- Edits code directly
- Searches across your entire project
- Runs terminal commands
- Creates new files
- Connects to enterprise systems (Jira, GitHub, Confluence, z/OS)
- Accesses mainframe datasets, JCL libraries, and copybooks
- Integrates with enterprise tools via MCP servers

### 3. Plans Complex Tasks
- Breaks down large problems into steps
- Executes each step sequentially
- Verifies its own work
- Reports back when done

### 4. Maintains Context
- Understands your project structure
- Remembers what you discussed earlier
- Knows which files relate to each other

---

## How You Interact with Bob

There are three main ways to interact:

### Chat Interface
```
You: "Explain the PROCESS-PAYMENT paragraph in PAYMNT01.cbl"

Bob: [Reads the file] "This paragraph handles payment processing. 
      It first validates the payment amount against the account balance, 
      then calls the AUTHORIZATION module via CICS LINK..."
```

### Inline Assistance
- Highlight code → Ask Bob to explain, refactor, or fix
- Get suggestions as you type

### Task Delegation
```
You: "Add error handling to all DB2 calls in this program"

Bob: [Plans the task]
     [Finds all DB2 EXEC SQL blocks]
     [Adds SQLCODE checking after each]
     [Adds appropriate error paragraphs]
     [Verifies consistency]
     "Done. I've added error handling to 12 DB2 calls."
```

---

## Getting Started with Bob

1. **Access Bob** — Via web interface or your development environment
2. **Open a project** — Your mainframe source code
3. **Open Bob's chat panel** — Available on the interface sidebar
4. **Start asking** — Type your question or task in natural language

That's it. No special syntax. No commands to memorize. Just talk to Bob like you'd talk to a colleague.

---

## Key Takeaways

| Point | Summary |
|-------|---------|
| **What is Bob** | AI coding assistant for enterprise developers |
| **Built by** | IBM, using various enterprise LLM models |
| **Languages** | COBOL, JCL, PL/I, Assembler, DB2, CICS |
| **Key difference** | Agentic — takes actions, not just answers |
| **Where** | Web interface or development environment |
| **How** | Natural language — just type what you need |

---

*← Previous: How AI is Useful for Mainframe | Next: What is Prompts →*
