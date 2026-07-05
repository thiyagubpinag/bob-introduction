# What is Context

---

## Overview

**Context** is the information that Bob can "see" and consider when responding to you. It's one of the most important concepts to understand because it directly affects the quality of Bob's answers. The more relevant context Bob has, the better and more accurate its responses will be.

---

## What is Context?

**Simple Definition:** Context is everything Bob knows about your current conversation, your code, and your project at any given moment.

```
┌──────────────────────────────────────────────────────┐
│              WHAT BOB CAN "SEE"                       │
├──────────────────────────────────────────────────────┤
│                                                      │
│  ┌─────────────────────────────────────────────┐     │
│  │ CONTEXT WINDOW                              │     │
│  │                                             │     │
│  │  • System instructions (who Bob is)         │     │
│  │  • Your conversation history                │     │
│  │  • Files Bob has read                       │     │
│  │  • Code you've highlighted                  │     │
│  │  • Tool results (search, file contents)     │     │
│  │  • Project structure                        │     │
│  │                                             │     │
│  └─────────────────────────────────────────────┘     │
│                                                      │
│  ┌─────────────────────────────────────────────┐     │
│  │ OUTSIDE CONTEXT (Bob cannot see)            │     │
│  │                                             │     │
│  │  • Files not yet opened                     │     │
│  │  • Previous conversations (closed)          │     │
│  │  • Your thoughts (until you type them)      │     │
│  │  • External systems (unless connected)      │     │
│  │                                             │     │
│  └─────────────────────────────────────────────┘     │
│                                                      │
└──────────────────────────────────────────────────────┘
```

---

## The Context Window

The **Context Window** is the total amount of text the AI can hold in its "memory" at once.

**Mainframe Analogy:** The context window is like **WORKING-STORAGE SECTION** — it has a fixed size. Everything Bob considers must fit within this space. If you exceed it, older information gets pushed out.

| Concept | Mainframe Equivalent |
|---------|---------------------|
| Context Window | WORKING-STORAGE (fixed size) |
| Filling context | MOVE data into fields |
| Context overflow | WORKING-STORAGE full — old data overwritten |
| Reading a file | Like a READ statement — brings data into memory |

---

## Types of Context in Bob

### 1. Conversation Context

Everything you and Bob have discussed in the current session:

```
YOU: "What does CALC-INTEREST do?"
BOB: "It calculates daily interest..."

YOU: "Now make it handle leap years"
BOB: [Still remembers the previous question was about CALC-INTEREST]
     "I'll modify CALC-INTEREST to account for 366 days in leap years..."
```

**Key Point:** Bob remembers earlier messages — you don't need to repeat yourself.

---

### 2. File Context

When Bob reads a file, that code becomes part of the context:

```
YOU: "Read PAYMNT01.cbl and explain it"
BOB: [Reads the file → file contents now in context]
     "This program handles payment processing..."

YOU: "Now find the bug"
BOB: [Can reference the file it already read]
     "On line 247, the COMPUTE statement..."
```

---

### 3. Project Context

Bob can see your project structure:

```
Bob knows:
├── src/
│   ├── COBOL/
│   │   ├── PAYMNT01.cbl
│   │   ├── CUSTMR02.cbl
│   │   └── BATCH03.cbl
│   ├── COPYBOOK/
│   │   ├── CUSTREC.cpy
│   │   └── PAYREC.cpy
│   └── JCL/
│       ├── DAILY.jcl
│       └── MONTHLY.jcl
```

---

### 4. Environment Context

Bob automatically knows:
- Your operating system
- Your IDE settings
- Active file you're viewing
- Git status (what's changed)

---

## Why Context Matters

### Example: Without Enough Context

```
YOU: "Fix the bug"

BOB: "I need more information. Which file? What kind of bug? 
      What's the expected vs actual behavior?"
```

### Example: With Good Context

```
YOU: "In PAYMNT01.cbl, the CALC-TAX paragraph is giving S0C7 
      when CUSTOMER-TYPE is 'E' for exempt customers. Fix it."

BOB: [Reads the file, finds the paragraph, sees the issue]
     "The problem is on line 312 — when CUSTOMER-TYPE is 'E', 
      TAX-RATE is SPACES (not numeric), but you're using it 
      in a COMPUTE. I'll add a check..."
```

**More context = better answers.**

---

## How Bob Gathers Context

Bob uses **tools** to gather context automatically:

| Tool | What it Does | Context Added |
|------|-------------|---------------|
| `read_file` | Reads a file's contents | Full file text |
| `grep` | Searches for patterns in code | Matching lines + files |
| `glob` | Finds files by name pattern | File paths |
| `list_files` | Shows directory structure | Project layout |
| `GetSymbolsOverview` | Lists functions/paragraphs | Code structure |
| `FindSymbol` | Finds specific code elements | Symbol definitions |
| `execute_command` | Runs terminal commands | Command output |

**You don't need to manually do this** — Bob decides which tools to use based on your prompt.

---

## Context Window Limits

The context window is large but not infinite:

```
┌─────────────────────────────────────────────────┐
│          CONTEXT WINDOW CAPACITY                 │
├─────────────────────────────────────────────────┤
│                                                  │
│  ████████████████████████░░░░░░░░░░ [60% used]  │
│                                                  │
│  Used by:                                        │
│  ██ System instructions (5%)                     │
│  ████ Conversation history (15%)                 │
│  ████████████ Files read (40%)                   │
│  ░░░░░░░░░░ Available space (40%)               │
│                                                  │
└─────────────────────────────────────────────────┘
```

### What happens when context gets full?

- Older parts of the conversation may be summarized (compacted)
- Bob focuses on the most recent and relevant information
- Very long files may be read in sections rather than all at once

---

## Best Practices for Context

### ✅ DO:

| Practice | Why |
|----------|-----|
| **Mention specific files** | Bob reads exactly what's needed |
| **Give relevant background** | "This is a batch program that runs nightly" |
| **Reference line numbers** | Pinpoints exactly where to look |
| **Keep related work in one conversation** | Maintains accumulated context |
| **Tell Bob about constraints** | "This must work with DB2 v12" |

### ❌ DON'T:

| Avoid | Why |
|-------|-----|
| Assuming Bob knows everything | It only knows what's in context |
| Asking about a file Bob hasn't read | Tell it which file to look at |
| Starting new conversations for related tasks | Loses prior context |
| Pasting enormous files manually | Let Bob use tools to read them |

---

## How Context Makes Bob Smart

```
┌─────────────────────────────────────────────────┐
│  Without Context:                                │
│  "What's wrong?" → "I don't have enough info"   │
│                                                  │
│  With Context:                                   │
│  "In BATCH03.cbl line 450, the SORT is failing   │
│   with SORT-RETURN code 16 when processing the   │
│   monthly customer file (CUST.MONTHLY.FILE)"     │
│  → Bob reads the file, checks the SORT step,     │
│    identifies the DCB mismatch, and fixes it.    │
└─────────────────────────────────────────────────┘
```

---

## Key Takeaways

| Concept | Summary |
|---------|---------|
| **Context** | All information Bob can see right now |
| **Context Window** | Fixed-size memory (like WORKING-STORAGE) |
| **Types** | Conversation, File, Project, Environment |
| **More context = better** | Specific prompts give better results |
| **Tools** | Bob uses tools to gather context automatically |
| **Limits** | Window is large but not infinite — older info may be summarized |
| **Best practice** | Be specific, reference files, keep related work together |

---

*← Previous: What is Prompts | Next: What is Modes →*
