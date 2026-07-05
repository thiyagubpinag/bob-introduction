# What is Skills

---

## Overview

**Skills** are specialized instruction sets that Bob can activate to handle specific types of tasks. Think of them as "expert knowledge modules" that Bob loads on demand — giving it focused expertise for particular scenarios.

---

## What Are Skills?

**Simple Definition:** A Skill is a set of detailed, step-by-step instructions that tell Bob exactly how to handle a specific type of task.

```
┌─────────────────────────────────────────────────────────┐
│                    WITHOUT SKILL                         │
├─────────────────────────────────────────────────────────┤
│  Bob uses general knowledge to attempt the task         │
│  (May miss specific steps or conventions)               │
└─────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────┐
│                    WITH SKILL ACTIVATED                  │
├─────────────────────────────────────────────────────────┤
│  Bob loads specialized instructions                     │
│  → Follows exact steps                                  │
│  → Knows specific conventions                           │
│  → Produces consistent, high-quality output             │
└─────────────────────────────────────────────────────────┘
```

**Mainframe Analogy:** Skills are like **COPY PROC** (cataloged procedures) in JCL:
- A PROC contains pre-defined steps for a specific job type
- You don't write the steps each time — you just call the PROC
- The PROC ensures consistency and best practices

Similarly, a Skill contains pre-defined instructions for a specific task type. Bob activates it when needed.

---

## How Skills Work

```
┌─────────────────────────────────────────────────────────┐
│              SKILL ACTIVATION FLOW                       │
├─────────────────────────────────────────────────────────┤
│                                                         │
│  1. You request a task                                  │
│     "Create a new MCP server for our DB2 catalog"       │
│                                                         │
│  2. Bob identifies the relevant skill                   │
│     → "build-mcp-server" skill matches                  │
│                                                         │
│  3. Bob activates the skill                             │
│     → Loads detailed instructions into context          │
│                                                         │
│  4. Bob follows the skill's step-by-step guide          │
│     → Scaffolds project structure                       │
│     → Implements the correct API pattern                │
│     → Registers the server properly                     │
│                                                         │
│  5. Result: Consistent, complete output                 │
│     → Following all best practices defined in skill     │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

---

## Available Skills in Bob

| Skill Name | What It Does | When It's Used |
|------------|-------------|----------------|
| `build-mcp-server` | Guides building a custom MCP server from scratch | When you need to create a new tool server |
| `configure-mcp` | Helps add or troubleshoot MCP server connections | When setting up or fixing tool connections |
| `create-skill` | Guides creating new custom skills | When you want to teach Bob new specialized tasks |
| `create-mode` | Guides creating custom operational modes | When you need a specialized mode |
| `xlsx-insights` | Analyzes Excel workbook data | When working with spreadsheet data |

---

## Anatomy of a Skill

A Skill is a structured document that contains:

```
┌─────────────────────────────────────────────────────────┐
│              SKILL STRUCTURE                             │
├─────────────────────────────────────────────────────────┤
│                                                         │
│  ┌───────────────────┐                                  │
│  │    METADATA       │  Name, description, triggers     │
│  └───────────────────┘                                  │
│           ↓                                             │
│  ┌───────────────────┐                                  │
│  │  PREREQUISITES    │  What's needed before starting   │
│  └───────────────────┘                                  │
│           ↓                                             │
│  ┌───────────────────┐                                  │
│  │   STEP-BY-STEP    │  Detailed instructions           │
│  │   INSTRUCTIONS    │  for executing the task          │
│  └───────────────────┘                                  │
│           ↓                                             │
│  ┌───────────────────┐                                  │
│  │  BEST PRACTICES   │  Conventions and patterns        │
│  └───────────────────┘                                  │
│           ↓                                             │
│  ┌───────────────────┐                                  │
│  │   VALIDATION      │  How to verify success           │
│  └───────────────────┘                                  │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

---

## Real-World Example

### Without a Skill:
```
YOU: "Create a custom MCP server for our DB2 catalog"

BOB (no skill): "Here's a basic Node.js server structure... 
     [May miss specific API patterns, registration steps, 
      or auth requirements]"
```

### With Skill Activated:
```
YOU: "Create a custom MCP server for our DB2 catalog"

BOB (skill activated): 
     [Loads build-mcp-server skill instructions]
     "I'll create this following the MCP server specification:

     1. Scaffolding the project with correct structure
     2. Using the v2 registerTool API pattern
     3. Implementing DB2 query tools with proper error handling
     4. Adding authentication configuration
     5. Registering the server in your config
     6. Testing the connection

     Let me start..."
```

---

## Custom Skills for Your Team

Your team can create **custom skills** specific to your mainframe environment:

### Example Custom Skills:

| Custom Skill | Purpose |
|-------------|---------|
| `cobol-program-creation` | Step-by-step guide for creating new COBOL programs following your team's standards |
| `jcl-review` | Checklist for reviewing JCL before submission |
| `db2-migration` | Steps for migrating DB2 table structures |
| `abend-diagnosis` | Systematic approach to diagnosing common ABENDs |
| `copybook-change` | Process for safely changing copybooks and updating dependents |

### Example: Custom COBOL Skill

```markdown
# Skill: cobol-program-creation

## Steps:
1. Create program with standard IDENTIFICATION DIVISION headers
2. Include company-standard comment block
3. Add required COPY statements (ERROR-HANDLING, LOGGING)
4. Structure PROCEDURE DIVISION with standard paragraphs:
   - 0000-MAIN
   - 1000-INITIALIZE
   - 2000-PROCESS
   - 3000-TERMINATE
   - 9000-ERROR-HANDLER
5. Include standard file status checking
6. Add DISPLAY statements for batch logging
7. Validate against team coding standards
```

When this skill is active, Bob **always** follows these steps when creating a COBOL program — ensuring consistency across your team.

---

## Skills vs. Regular Prompts

| Aspect | Regular Prompt | With Skill |
|--------|---------------|------------|
| **Instructions** | You provide them each time | Pre-defined, always consistent |
| **Completeness** | May forget steps | All steps guaranteed |
| **Standards** | You must mention them | Built into the skill |
| **Reusability** | One-time | Used every time the task type occurs |
| **Team consistency** | Varies by person | Same process for everyone |

---

## Key Takeaways

| Concept | Summary |
|---------|---------|
| **Skills** | Specialized instruction sets for specific tasks |
| **Purpose** | Ensure consistent, complete, high-quality output |
| **Activation** | Loaded on-demand when a matching task is detected |
| **Built-in** | Bob comes with skills for common development tasks |
| **Custom** | Teams can create their own skills for their standards |
| **Analogy** | Like cataloged PROCs — pre-defined steps called by name |
| **Benefit** | Consistency + Completeness + Best practices enforced |

---

*← Previous: What is MCP Tools | Next: What is Workflows →*
