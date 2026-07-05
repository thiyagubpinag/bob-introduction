# What is Modes

---

## Overview

**Modes** in Bob define *how* Bob operates and what tools it has access to. Think of modes as different "operational configurations" — just like how a mainframe can run in different modes (batch, online, test), Bob can switch between modes depending on what you need.

---

## What Are Modes?

Bob has **three built-in modes**, each optimized for a different type of work:

```
┌─────────────────────────────────────────────────────────┐
│                    BOB'S MODES                           │
├─────────────────────────────────────────────────────────┤
│                                                         │
│  ┌─────────┐    ┌─────────┐    ┌─────────┐            │
│  │  PLAN   │    │  AGENT  │    │   ASK   │            │
│  │  Mode   │    │  Mode   │    │  Mode   │            │
│  ├─────────┤    ├─────────┤    ├─────────┤            │
│  │ Think & │    │ Execute │    │ Explain │            │
│  │ Design  │    │ & Build │    │ & Learn │            │
│  └─────────┘    └─────────┘    └─────────┘            │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

**Mainframe Analogy:** Modes are like different **job classes** on a mainframe:
- **CLASS A** = High-priority, full access (Agent Mode)
- **CLASS B** = Planning and design work (Plan Mode)
- **CLASS T** = Test/inquiry only, read-only (Ask Mode)

---

## Mode 1: Agent Mode (The Builder)

**Purpose:** Execute tasks, write code, make changes, run commands.

**When to use:** When you want Bob to **DO** something — write code, fix bugs, create files, refactor programs.

### Capabilities:
| Can Do | Example |
|--------|---------|
| ✅ Read files | Open and analyze COBOL programs |
| ✅ Edit files | Fix bugs, add code, refactor |
| ✅ Create files | Generate new programs, JCL, copybooks |
| ✅ Run commands | Execute builds, tests, searches |
| ✅ Search code | Find patterns across your project |
| ✅ Use all tools | Full access to MCP tools, skills, workflows |

### Example Interaction:
```
YOU: "Add error handling to all EXEC SQL blocks in PAYMNT01.cbl"

BOB (Agent Mode):
[Reads PAYMNT01.cbl]
[Finds 8 EXEC SQL blocks]
[Adds SQLCODE checking after each one]
[Adds error-handling paragraph]
[Verifies all changes are consistent]
"Done. I've added error handling to all 8 DB2 calls. Each now 
checks SQLCODE and calls ERROR-HANDLER if not zero."
```

**Mainframe Analogy:** Agent Mode is like running a job that **reads AND writes** — it has full DISP=(OLD,KEEP) access to your datasets. It can modify them.

---

## Mode 2: Plan Mode (The Architect)

**Purpose:** Think through problems, design solutions, create plans before implementation.

**When to use:** When you have a complex task and want Bob to **PLAN** the approach before making any changes.

### Capabilities:
| Can Do | Cannot Do |
|--------|-----------|
| ✅ Read files | ❌ Run arbitrary commands |
| ✅ Analyze code | |
| ✅ Create plan documents | |
| ✅ Design architecture | |
| ✅ Break down complex problems | |
| ✅ Write plans to files | |

### Example Interaction:
```
YOU: "I need to modernize the account closure process. 
      Plan the approach."

BOB (Plan Mode):
"Here's my plan for modernizing the account closure process:

Phase 1: Analysis
- Identify all 12 programs in the closure flow
- Map data dependencies between them
- Document current business rules

Phase 2: Design  
- Design new modular structure
- Define API interfaces
- Plan database changes

Phase 3: Implementation (to be done in Agent Mode)
- Refactor program by program
- Add API wrapper layer
- Update JCL procedures"
```

**Mainframe Analogy:** Plan Mode is like the **design phase** of a project — you're creating the specifications and architecture before any coding begins. Like writing a program spec document before opening the editor.

---

## Mode 3: Ask Mode (The Teacher)

**Purpose:** Answer questions, explain concepts, provide information — without making any changes.

**When to use:** When you want to **LEARN** or **UNDERSTAND** something without Bob modifying anything.

### Capabilities:
| Can Do | Cannot Do |
|--------|-----------|
| ✅ Read files | ❌ Edit files |
| ✅ Explain code | ❌ Create files |
| ✅ Answer questions | ❌ Run commands |
| ✅ Analyze patterns | ❌ Make any changes |
| ✅ Search codebase | ❌ Use editing tools |

### Example Interaction:
```
YOU: "Explain how the SORT works in BATCH03.cbl"

BOB (Ask Mode):
"The SORT in BATCH03.cbl (line 234-278) works as follows:

1. INPUT PROCEDURE (SORT-INPUT, lines 240-255):
   - Reads from CUSTOMER-FILE
   - Filters only active customers (STATUS = 'A')
   - RELEASEs matching records to sort

2. SORT KEY:
   - Ascending on ACCOUNT-NUMBER
   - Descending on TRANSACTION-DATE

3. OUTPUT PROCEDURE (SORT-OUTPUT, lines 260-278):
   - RETURNs sorted records
   - Writes to SORTED-CUSTOMER-FILE
   - Counts total records processed"
```

**Mainframe Analogy:** Ask Mode is like running a **read-only inquiry** — DISP=SHR only. You can look at the data but can't change anything.

---

## Mode Comparison Table

| Feature | Plan Mode | Agent Mode | Ask Mode |
|---------|-----------|------------|----------|
| **Purpose** | Design & strategize | Build & execute | Learn & understand |
| **Reads files** | ✅ | ✅ | ✅ |
| **Edits files** | ✅ (plans only) | ✅ | ❌ |
| **Creates files** | ✅ (plans only) | ✅ | ❌ |
| **Runs commands** | ❌ | ✅ | ❌ |
| **Uses tools** | Limited | Full access | Read-only |
| **Best for** | Complex planning | Implementation | Questions |
| **Analogy** | Project design | Coding & testing | Training |

---

## How to Switch Modes

You can ask Bob to switch modes, or Bob may switch automatically:

```
YOU: "Switch to Plan mode — I need to design the new batch process"
BOB: [Switches to Plan Mode]

YOU: "OK, the plan looks good. Switch to Agent mode and implement step 1"
BOB: [Switches to Agent Mode, starts implementing]

YOU: "Wait — explain what COMP-3 means before we continue"
BOB: [Switches to Ask Mode to explain]
```

---

## Typical Workflow Using Modes

```
┌─────────────────────────────────────────────────┐
│          TYPICAL DEVELOPMENT WORKFLOW            │
├─────────────────────────────────────────────────┤
│                                                  │
│  Step 1: ASK MODE                               │
│  "Explain the current account closure process"   │
│  → Bob explains the existing system              │
│                                                  │
│  Step 2: PLAN MODE                              │
│  "Plan how to add email notifications"           │
│  → Bob creates a detailed implementation plan    │
│                                                  │
│  Step 3: AGENT MODE                             │
│  "Implement the plan"                           │
│  → Bob writes code, edits files, tests          │
│                                                  │
│  Step 4: ASK MODE                               │
│  "Explain what was changed and why"              │
│  → Bob provides a summary for documentation     │
│                                                  │
└─────────────────────────────────────────────────┘
```

---

## Custom Modes

Beyond the three built-in modes, Bob supports **custom modes** — specialized configurations for specific tasks:

- **Code Review Mode** — focuses on finding issues and suggesting improvements
- **Documentation Mode** — optimized for generating documentation
- **Migration Mode** — specialized for code conversion tasks

Custom modes can be created by your team to match your specific workflow needs.

---

## Mainframe-Specific Modes: Z Architect & Z Code

For mainframe developers, Bob ships with two dedicated modes purpose-built for z/OS work. These are the modes you will use most often.

```
┌─────────────────────────────────────────────────────────┐
│            MAINFRAME-SPECIFIC MODES                      │
├─────────────────────────────────────────────────────────┤
│                                                         │
│  ┌──────────────────┐     ┌──────────────────┐         │
│  │   Z ARCHITECT    │     │     Z CODE       │         │
│  │      Mode        │     │      Mode        │         │
│  ├──────────────────┤     ├──────────────────┤         │
│  │ Read, Analyse,   │     │ Write, Fix,      │         │
│  │ Understand       │     │ Improve, Build   │         │
│  └──────────────────┘     └──────────────────┘         │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

### Z Architect Mode — The Application Analyst

**Purpose:** Understand and analyse entire mainframe applications — across hundreds of programs — and deliver architecture-level insights.

**When to use:** When you need to *understand* the system before touching it.

| Can Do | Example |
|--------|---------|
| ✅ Read entire applications | Scan 450 COBOL programs at once |
| ✅ Build dependency maps | Which programs call CARDVAL? |
| ✅ Generate architecture diagrams | Current vs proposed flow |
| ✅ Produce business-aware documentation | Using your data dictionary for context |
| ✅ Perform impact analysis | What breaks if I change copybook CARDDATA? |

```
YOU:  "Give me a complete overview of the payment system"

BOB:  [Scans all programs, copybooks, DB2 tables, JCL]

      "The payment system has 3 main subsystems:
       1. PAYMENT INTAKE  — 12 programs, entry via PAYMNT01
       2. PAYMENT PROCESSING — 28 programs, core: PAYPRC01
       3. SETTLEMENT — 15 programs, nightly batch: SETLBCH1

       Key dependency: COPYBOOK CARDDATA used by 87 programs."

Time: 3 minutes  (vs 6 months learning it manually)
```

**Mainframe Analogy:** Z Architect Mode is like a **cross-reference listing + XREF report** — but for your entire application, not just one program.

---

### Z Code Mode — The Active Developer

**Purpose:** Write, fix, modernise, and improve mainframe code directly inside your codebase.

**When to use:** When you need to *change* something — fix a bug, add a feature, modernise a program.

| Can Do | Example |
|--------|---------|
| ✅ Implement changes across multiple programs | Add a new copybook field to 35 programs |
| ✅ Run ZCodeScan | Find and fix critical CICS/DB2 issues automatically |
| ✅ Generate data dictionaries | Scan variables, create `.bob/DD.json` |
| ✅ Apply enterprise standards | Add RESP, RESP2, END-CALL automatically |
| ✅ Debug and fix ABENDs | Identify root cause and apply the fix |

```
YOU:  "Add field ACCT-TIER to ACCTDATA copybook and update
       all 35 programs that use it"

BOB:  [Plans → Updates copybook → Updates all 35 programs
       → Verifies consistency]

      "Done. Updated ACCTDATA.cpy and 35 programs.
       No programs were missed."

Time: 8 minutes  (vs 15 hours manually)
```

**Mainframe Analogy:** Z Code Mode is like a **super-powered ISPF editor** — it reads, edits, and verifies changes across your entire PDS library, not just one member at a time.

---

### Z Architect vs Z Code — When to Use Which

```
Z ARCHITECT MODE                    Z CODE MODE
────────────────────────────        ────────────────────────────
✓ "Explain this application"        ✓ "Fix this ABEND"
✓ "What programs call CARDVAL?"     ✓ "Add error handling here"
✓ "Show me the full call chain"     ✓ "Modernise this CICS call"
✓ "What is the impact if I         ✓ "Add the new field to all
  change this copybook?"              programs"
✓ "Document this program"           ✓ "Run ZCodeScan and fix issues"
✓ "Give me an architecture          ✓ "Optimise this batch job"
  overview"

MODE: Read, Analyse, Understand     MODE: Write, Fix, Improve, Build
```

> **Tip for beginners:** Start with **Z Architect** to understand the code, then switch to **Z Code** to change it. This is the safest and most effective workflow.

---

## Key Takeaways

| Mode | When to Use | What it Does |
|------|-------------|--------------|
| **Plan** | Complex tasks needing design | Thinks, plans, designs — limited actions |
| **Agent** | Implementation tasks | Full access — reads, writes, executes |
| **Ask** | Learning, understanding | Read-only — explains, answers questions |
| **Z Architect** | Understand mainframe applications | Reads entire apps, maps dependencies, explains architecture |
| **Z Code** | Develop mainframe code | Writes, fixes, modernises, scans quality |
| **Switching** | Natural — ask or automatic | Bob adapts to what you need |
| **Custom** | Team-specific workflows | Can be created for specialized tasks |

---

*← Previous: What is Context | Next: What is MCP Tools →*
