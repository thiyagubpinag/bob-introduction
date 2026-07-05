# Generative AI vs Agentic AI

---

## Overview

There are two major categories of modern AI that you need to understand. **Generative AI** creates content when you ask it to. **Agentic AI** goes further — it can plan, decide, and take actions autonomously. Bob is an **Agentic AI** — and this distinction matters for how it helps you.

---

## What is Generative AI?

**Generative AI** = AI that **generates** (creates) new content based on your input.

### How it works:
```
You ask a question → AI generates an answer → You read it → Done.
```

### Examples:
| You Input | AI Generates |
|-----------|-------------|
| "Explain this COBOL code" | A text explanation |
| "Write a JCL for a sort" | A JCL script |
| "Summarize this documentation" | A shorter summary |

### Characteristics:
- **One-shot:** You ask, it answers, conversation over
- **Passive:** It only responds when you prompt it
- **No actions:** It generates text but doesn't DO anything
- **Stateless:** Each request is independent

**Mainframe Analogy:** Gen AI is like a **SORT utility** — you give it input, it produces output, and it's done. It doesn't decide what to sort next or fix errors in the input.

---

## What is Agentic AI?

**Agentic AI** = AI that can **plan**, **decide**, **use tools**, and **take actions** to accomplish goals.

### How it works:
```
You give a goal → AI plans steps → AI uses tools → AI verifies results → AI continues until done.
```

### Examples:
| You Say | AI Does |
|---------|---------|
| "Fix the bug in this program" | Reads code → Identifies bug → Edits file → Tests fix → Confirms |
| "Add error handling to this module" | Analyzes code → Plans changes → Modifies multiple files → Validates |
| "Explain and document this copybook" | Reads file → Understands structure → Writes documentation → Saves it |

### Characteristics:
- **Multi-step:** Plans and executes multiple actions
- **Active:** Takes initiative, makes decisions
- **Tool-using:** Can read files, edit code, run commands
- **Stateful:** Remembers context throughout the task
- **Self-correcting:** Can check its own work and fix mistakes

**Mainframe Analogy:** Agentic AI is like a **skilled developer** — you give them a task, and they:
1. Read the relevant programs
2. Understand the logic
3. Make the changes
4. Test their work
5. Come back with the result

---

## Side-by-Side Comparison

| Aspect | Generative AI | Agentic AI (Bob) |
|--------|--------------|------------------|
| **Interaction** | Question → Answer | Goal → Plan → Execute → Verify |
| **Steps** | Single step | Multiple steps |
| **Tools** | None — only generates text | Uses tools (file editor, terminal, search) |
| **Initiative** | Waits for you | Takes next steps autonomously |
| **Error Handling** | You fix errors | Self-corrects and retries |
| **Output** | Text/content only | Actual changes to your codebase |
| **Memory** | Forgets between messages | Maintains context throughout task |
| **Analogy** | Reference manual | Junior developer on your team |

---

## Why Agentic AI Matters for Mainframe Developers

### Scenario: You need to add a new field to a COBOL copybook

**With Generative AI:**
1. You ask: "How do I add a field to a copybook?"
2. AI gives you instructions
3. You manually edit the copybook
4. You manually find all programs that use it
5. You manually update each program
6. You manually test

**With Agentic AI (Bob):**
1. You say: "Add CUSTOMER-EMAIL to the CUSTOMER-RECORD copybook and update all programs that use it"
2. Bob reads the copybook
3. Bob finds all programs referencing it
4. Bob edits the copybook
5. Bob updates each affected program
6. Bob verifies the changes are consistent

**You went from 6 manual steps to 1 instruction.**

---

## The Agent Loop

Bob operates in what's called an **Agent Loop**:

```
┌─────────────────────────────────────────────┐
│              THE AGENT LOOP                  │
├─────────────────────────────────────────────┤
│                                              │
│   ┌──────────┐                              │
│   │  THINK   │ ← Analyze the situation      │
│   └────┬─────┘                              │
│        ↓                                    │
│   ┌──────────┐                              │
│   │   PLAN   │ ← Decide what to do next     │
│   └────┬─────┘                              │
│        ↓                                    │
│   ┌──────────┐                              │
│   │   ACT    │ ← Use a tool (read/edit/run) │
│   └────┬─────┘                              │
│        ↓                                    │
│   ┌──────────┐                              │
│   │ OBSERVE  │ ← Check the result           │
│   └────┬─────┘                              │
│        ↓                                    │
│   [Goal complete?]                          │
│     No → Loop back to THINK                 │
│     Yes → Return final result               │
│                                              │
└─────────────────────────────────────────────┘
```

**Mainframe Analogy:** The Agent Loop is like a **PERFORM UNTIL** loop in COBOL:
```cobol
PERFORM UNTIL TASK-COMPLETE
    PERFORM THINK-STEP
    PERFORM PLAN-STEP
    PERFORM ACT-STEP
    PERFORM OBSERVE-STEP
END-PERFORM
```

---

## Where is Bob on This Spectrum?

Bob is a **fully Agentic AI**:

- ✅ Plans multi-step solutions
- ✅ Uses tools (file reader, editor, terminal, search)
- ✅ Maintains context across the entire conversation
- ✅ Self-corrects when something goes wrong
- ✅ Can work across multiple files simultaneously
- ✅ Understands mainframe languages (COBOL, JCL, PL/I)

---

## Key Takeaways

| Point | Summary |
|-------|---------|
| **Gen AI** | Creates content (text, code) — passive, one-shot |
| **Agentic AI** | Plans, decides, acts, verifies — active, multi-step |
| **Bob** | Agentic AI — acts like a skilled team member |
| **Key difference** | Gen AI gives answers; Agentic AI solves problems |
| **For mainframe** | Agentic AI can handle complex multi-file tasks autonomously |

---

*← Previous: What is LLM | Next: How AI is Useful for Mainframe →*
