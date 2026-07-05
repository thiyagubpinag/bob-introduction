# What is MCP Tools

---

## Overview

**MCP** stands for **Model Context Protocol**. MCP Tools are **external capabilities** that Bob can use to interact with the outside world — reading files, editing code, running commands, searching your project, and connecting to external services. They are the "hands" that allow Bob to take action.

---

## What Are Tools?

Without tools, an AI can only generate text. **With tools**, Bob can:

```
┌─────────────────────────────────────────────────────────┐
│          WITHOUT TOOLS           WITH TOOLS (Bob)       │
├─────────────────────────────────────────────────────────┤
│                                                         │
│  "Here's how to fix it:       [Reads the file]          │
│   change line 45 to..."       [Edits line 45]           │
│                                [Saves the file]          │
│  (You do it manually)         [Verifies the fix]        │
│                                "Done. Fixed."            │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

**Mainframe Analogy:** Tools are like **utility programs** that a JCL job calls:
- SORT is a tool for sorting data
- IDCAMS is a tool for managing VSAM files  
- IEBGENER is a tool for copying datasets

Bob has its own "utility programs" (tools) for different operations.

---

## What is MCP (Model Context Protocol)?

**MCP** is a standardized way for AI assistants to connect to external tools and services.

**Mainframe Analogy:** MCP is like **CICS's interface** to external systems:
- Just as CICS uses EXEC CICS LINK to call other programs
- Bob uses MCP to call external tools
- The protocol standardizes HOW the communication works

```
┌───────────────┐         ┌─────────────────┐
│               │   MCP   │                 │
│     BOB       │◄───────►│   MCP SERVER    │
│  (AI Agent)   │Protocol │  (Tool Provider)│
│               │         │                 │
└───────────────┘         └─────────────────┘
                                   │
                                   ▼
                          ┌─────────────────┐
                          │  External Tools  │
                          │  - File system   │
                          │  - Databases     │
                          │  - APIs          │
                          │  - Services      │
                          └─────────────────┘
```

---

## Bob's Built-In Tools

Bob comes with a set of built-in tools for development work:

### File Operations

| Tool | What It Does | Mainframe Equivalent |
|------|-------------|---------------------|
| `read_file` | Reads file contents | Like a READ statement |
| `write_file` | Creates/overwrites files | Like WRITE to a new dataset |
| `apply_diff` | Makes precise edits to files | Like a targeted file update |
| `insert_content` | Adds lines at a specific position | Like INSERT in a file |
| `search_and_replace` | Finds and replaces text | Like a CHANGE command in ISPF |

### Search Operations

| Tool | What It Does | Mainframe Equivalent |
|------|-------------|---------------------|
| `grep` | Searches file contents by pattern | Like SRCHFOR in ISPF |
| `glob` | Finds files by name pattern | Like listing by dataset mask |
| `FindSymbol` | Finds code symbols (functions, paragraphs) | Like a cross-reference listing |
| `FindReferencingSymbols` | Finds where something is used | Like XREF in compiler listing |
| `list_files` | Shows directory contents | Like LISTCAT |

### Execution

| Tool | What It Does | Mainframe Equivalent |
|------|-------------|---------------------|
| `execute_command` | Runs terminal commands | Like JCL EXEC PGM= |

---

## How Bob Uses Tools (Example)

When you say: *"Find all programs that use the CUSTOMER-RECORD copybook"*

Bob's tool usage:

```
Step 1: Bob thinks → "I need to search for COPY CUSTOMER-RECORD"

Step 2: Bob calls tool:
        grep(pattern="COPY.*CUSTOMER-RECORD", include="*.cbl")

Step 3: Tool returns:
        PAYMNT01.cbl:15:  COPY CUSTOMER-RECORD.
        BATCH03.cbl:22:   COPY CUSTOMER-RECORD.
        REPORT05.cbl:8:   COPY CUSTOMER-RECORD.

Step 4: Bob responds:
        "3 programs use the CUSTOMER-RECORD copybook:
         1. PAYMNT01.cbl (line 15)
         2. BATCH03.cbl (line 22)
         3. REPORT05.cbl (line 8)"
```

---

## MCP Server Architecture

MCP Servers are services that provide additional tools beyond Bob's built-in set:

```
┌─────────────────────────────────────────────────────────┐
│                    BOB's TOOL ECOSYSTEM                  │
├─────────────────────────────────────────────────────────┤
│                                                         │
│  ┌──────────────────────────────────┐                   │
│  │      BUILT-IN TOOLS              │                   │
│  │  read_file, write_file, grep,    │                   │
│  │  execute_command, etc.           │                   │
│  └──────────────────────────────────┘                   │
│                                                         │
│  ┌──────────────────────────────────┐                   │
│  │      MCP SERVER: Git             │                   │
│  │  git_commit, git_diff,           │                   │
│  │  git_log, git_branch             │                   │
│  └──────────────────────────────────┘                   │
│                                                         │
│  ┌──────────────────────────────────┐                   │
│  │      MCP SERVER: Database        │                   │
│  │  query_db2, list_tables,         │                   │
│  │  describe_table                  │                   │
│  └──────────────────────────────────┘                   │
│                                                         │
│  ┌──────────────────────────────────┐                   │
│  │      MCP SERVER: Custom          │                   │
│  │  (Your team's specific tools)    │                   │
│  └──────────────────────────────────┘                   │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

---

## Why MCP Matters

### Extensibility
MCP allows Bob to be **extended** with new capabilities without changing Bob itself:

- Need Bob to access your DB2 catalog? → Add a DB2 MCP server
- Need Bob to interact with Endevor? → Add an Endevor MCP server
- Need Bob to check your CI/CD pipeline? → Add a pipeline MCP server

### Standardization
MCP provides a **standard interface** — any tool built to the MCP spec works with Bob. This means:
- Your team can build custom tools
- Third parties can provide tools
- All follow the same protocol

---

## Real-World Example: Multi-Tool Task

**Task:** "Add a new DATE-OF-BIRTH field to the customer record and update all programs"

Bob uses MULTIPLE tools in sequence:

```
┌─────────────────────────────────────────────────────────┐
│ TOOL CHAIN EXECUTION                                    │
├─────────────────────────────────────────────────────────┤
│                                                         │
│ 1. grep("COPY CUSTOMER-RECORD")                         │
│    → Find all programs using the copybook               │
│                                                         │
│ 2. read_file("COPYBOOK/CUSTREC.cpy")                   │
│    → Read the current copybook                          │
│                                                         │
│ 3. apply_diff("COPYBOOK/CUSTREC.cpy")                  │
│    → Add DATE-OF-BIRTH field to copybook                │
│                                                         │
│ 4. read_file("PAYMNT01.cbl")                           │
│    → Read first affected program                        │
│                                                         │
│ 5. apply_diff("PAYMNT01.cbl")                          │
│    → Update program to handle new field                 │
│                                                         │
│ 6. [Repeat 4-5 for each affected program]              │
│                                                         │
│ 7. execute_command("build")                             │
│    → Verify everything compiles                         │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

---

## Tool Safety

Bob's tools have **safety controls**:

| Safety Feature | Description |
|---------------|-------------|
| **Mode restrictions** | Ask Mode can't use editing tools |
| **Confirmation** | Destructive operations may ask for confirmation |
| **Scoped access** | Tools only access your workspace |
| **Audit trail** | All tool usage is visible in the conversation |
| **Reversible** | Changes can be undone (git, undo) |

---

## Key Takeaways

| Concept | Summary |
|---------|---------|
| **Tools** | Capabilities that let Bob take actions (not just talk) |
| **MCP** | Standard protocol for connecting tools to AI |
| **Built-in** | File operations, search, code analysis, command execution |
| **MCP Servers** | Extensible — add new tools via MCP servers |
| **Safety** | Tools are scoped, mode-restricted, and auditable |
| **Power** | Bob chains multiple tools to complete complex tasks |
| **Analogy** | Tools = Utility programs (SORT, IDCAMS) called by JCL |

---

*← Previous: What is Modes | Next: What is Skills →*
