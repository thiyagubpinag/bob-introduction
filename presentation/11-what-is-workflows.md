# What is Workflows

---

## Overview

**Workflows** are pre-defined, step-by-step processes that Bob can execute for common, well-understood tasks. While Skills provide instructions, Workflows provide **automated sequences** — a complete pipeline from start to finish.

---

## What Are Workflows?

**Simple Definition:** A Workflow is a repeatable, automated sequence of steps that Bob follows to complete a specific type of task efficiently.

```
┌─────────────────────────────────────────────────────────┐
│              WITHOUT WORKFLOW                            │
├─────────────────────────────────────────────────────────┤
│  You describe each step manually every time             │
│  → Inconsistent results                                 │
│  → May miss steps                                      │
│  → Takes longer                                        │
└─────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────┐
│              WITH WORKFLOW                               │
├─────────────────────────────────────────────────────────┤
│  Bob follows a proven, optimized sequence               │
│  → Consistent results every time                       │
│  → No steps missed                                     │
│  → Fast and efficient                                  │
└─────────────────────────────────────────────────────────┘
```

**Mainframe Analogy:** Workflows are like **JCL PROCs with multiple steps**:
- A multi-step PROC runs SORT → PROCESS → REPORT in sequence
- Each step depends on the previous step's output
- The PROC handles the orchestration automatically

Similarly, a Workflow runs multiple AI steps in sequence, each building on the previous.

---

## How Workflows Differ from Skills

| Aspect | Skills | Workflows |
|--------|--------|-----------|
| **What they are** | Instructions (how-to guide) | Automated sequences (pipeline) |
| **Execution** | Bob follows guidelines | Bob runs a defined pipeline |
| **Flexibility** | Bob adapts instructions to context | Steps are more structured |
| **Analogy** | Recipe book | Assembly line |
| **Mainframe** | COPY PROC (template) | Multi-step JCL job (execution) |

---

## Workflow Structure

```
┌─────────────────────────────────────────────────────────┐
│              WORKFLOW EXECUTION                          │
├─────────────────────────────────────────────────────────┤
│                                                         │
│  TRIGGER: User request matches workflow pattern         │
│           ↓                                             │
│  STEP 1:  [Gather Information]                          │
│           ↓                                             │
│  STEP 2:  [Analyze & Plan]                              │
│           ↓                                             │
│  STEP 3:  [Execute Changes]                             │
│           ↓                                             │
│  STEP 4:  [Validate Results]                            │
│           ↓                                             │
│  STEP 5:  [Report Completion]                           │
│                                                         │
│  Each step uses specific tools and produces             │
│  defined outputs that feed into the next step.          │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

---

## Example Workflows for Mainframe

### Workflow: Code Documentation

```
┌─────────────────────────────────────────────────────────┐
│  WORKFLOW: Document a COBOL Program                      │
├─────────────────────────────────────────────────────────┤
│                                                         │
│  Step 1: READ the program file                          │
│          → Get full source code                         │
│                                                         │
│  Step 2: IDENTIFY structure                             │
│          → List all paragraphs, files, copybooks        │
│                                                         │
│  Step 3: ANALYZE each paragraph                         │
│          → Understand purpose and logic                 │
│                                                         │
│  Step 4: GENERATE documentation                         │
│          → Program overview                             │
│          → Paragraph descriptions                       │
│          → Data flow diagram                            │
│          → File/DB2 dependencies                        │
│                                                         │
│  Step 5: SAVE documentation                             │
│          → Write to markdown file                       │
│          → Add inline comments to code                  │
│                                                         │
│  Step 6: VERIFY completeness                            │
│          → Check all paragraphs documented              │
│          → Ensure accuracy                              │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

**You just say:** "Document PAYMNT01.cbl"  
**Bob executes** all 6 steps automatically.

---

### Workflow: Bug Investigation

```
┌─────────────────────────────────────────────────────────┐
│  WORKFLOW: Investigate ABEND                             │
├─────────────────────────────────────────────────────────┤
│                                                         │
│  Step 1: PARSE the error                                │
│          → Identify ABEND code (S0C7, S0C4, etc.)      │
│                                                         │
│  Step 2: READ the failing program                       │
│          → Load source code into context                │
│                                                         │
│  Step 3: LOCATE the failure point                       │
│          → Find the statement causing the ABEND        │
│                                                         │
│  Step 4: ANALYZE root cause                             │
│          → Trace data flow to the failing field         │
│          → Identify where bad data entered              │
│                                                         │
│  Step 5: PROPOSE fix                                    │
│          → Suggest code changes                         │
│          → Add data validation                          │
│                                                         │
│  Step 6: IMPLEMENT (if approved)                        │
│          → Apply the fix                                │
│          → Add preventive checks                        │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

---

### Workflow: Copybook Impact Analysis

```
┌─────────────────────────────────────────────────────────┐
│  WORKFLOW: Copybook Change Impact Analysis              │
├─────────────────────────────────────────────────────────┤
│                                                         │
│  Step 1: READ the copybook                              │
│          → Understand current structure                 │
│                                                         │
│  Step 2: SEARCH all references                          │
│          → Find every program that COPYs it            │
│                                                         │
│  Step 3: ANALYZE each program                           │
│          → How does each use the changed field?        │
│          → What logic depends on it?                   │
│                                                         │
│  Step 4: GENERATE impact report                         │
│          → List of affected programs                   │
│          → Severity rating for each                    │
│          → Required changes for each                   │
│                                                         │
│  Step 5: PLAN modifications                             │
│          → Ordered list of changes needed              │
│          → Dependencies between changes                │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

---

## Workflow vs. Manual Step-by-Step

### Manual (Without Workflow):
```
YOU: "Read CUSTREC.cpy"
BOB: [reads file]
YOU: "Now find all programs that use it"
BOB: [searches]
YOU: "Now read each one and tell me what uses CUST-NAME"
BOB: [reads each]
YOU: "Now generate a report of changes needed"
BOB: [generates report]
```
**4 prompts, manual orchestration, you drive each step.**

### Workflow (Automated):
```
YOU: "Analyze the impact of changing CUST-NAME in CUSTREC.cpy"
BOB: [Automatically runs all steps]
     "Impact Analysis Complete:
      - 7 programs reference CUSTREC.cpy
      - 4 programs directly use CUST-NAME
      - 2 programs need logic changes
      - Here's the detailed report..."
```
**1 prompt, Bob orchestrates everything.**

---

## Benefits of Workflows

| Benefit | Description |
|---------|-------------|
| **Efficiency** | One prompt triggers a complete process |
| **Consistency** | Same steps executed every time |
| **Completeness** | No steps forgotten or skipped |
| **Quality** | Validated sequence that produces reliable results |
| **Speed** | Bob doesn't need to figure out the approach each time |
| **Reusability** | Same workflow works for any program/copybook |

---

## When Workflows Are Used

| Scenario | Workflow Type |
|----------|--------------|
| "Document this program" | Documentation workflow |
| "Investigate this ABEND" | Bug investigation workflow |
| "What's the impact of this change?" | Impact analysis workflow |
| "Set up a new project" | Project scaffolding workflow |
| "Review this code for issues" | Code review workflow |

---

## Key Takeaways

| Concept | Summary |
|---------|---------|
| **Workflows** | Pre-defined automated sequences for common tasks |
| **Purpose** | Execute complex multi-step tasks with one prompt |
| **Difference from Skills** | Skills = instructions; Workflows = automated pipelines |
| **Benefit** | Consistent, complete, fast results |
| **Trigger** | User request matches a workflow pattern |
| **Analogy** | Multi-step JCL PROC — orchestrated execution |
| **Power** | Turns 10 manual prompts into 1 automated sequence |

---

*← Previous: What is Skills | Next: How Bob is Going to be Helpful →*
