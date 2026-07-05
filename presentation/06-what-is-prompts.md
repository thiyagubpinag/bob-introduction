# What is Prompts (Roles & Types)

---

## Overview

A **prompt** is simply the text you send to Bob (or any AI). But there's more to it than just typing a question. Understanding how prompts work — including **roles** and **types** — helps you get much better results from Bob.

---

## What is a Prompt?

**Simple Definition:** A prompt is any instruction or question you give to the AI.

```
┌─────────────────────────────────────────┐
│  Prompt = Your input to the AI          │
│                                         │
│  "Explain this COBOL program"           │
│  "Fix the bug on line 45"              │
│  "Write JCL for a DB2 unload"          │
│                                         │
│  All of these are prompts.              │
└─────────────────────────────────────────┘
```

**Mainframe Analogy:** A prompt is like **SYSIN** input to a batch program — it tells the program what to do with what data.

---

## The Three Roles in AI Conversations

Every message in an AI conversation has a **role**. There are three roles:

### 1. System Role (The Instructions)

The **System** message defines WHO Bob is and HOW he should behave. You don't see it — it's set up behind the scenes.

```
┌─────────────────────────────────────────────────┐
│ SYSTEM ROLE (Hidden — set by IBM)               │
├─────────────────────────────────────────────────┤
│ "You are Bob, a highly skilled software         │
│  engineer with extensive knowledge in many      │
│  programming languages, frameworks, design      │
│  patterns, and best practices."                 │
│                                                 │
│ "Follow existing code style and project         │
│  conventions."                                  │
│                                                 │
│ "Produce the minimal change that solves the     │
│  problem."                                      │
└─────────────────────────────────────────────────┘
```

**Mainframe Analogy:** The System role is like the **JOB card + PROC** — it defines the environment, rules, and behavior before any work begins. Just as a PROC sets up DD statements and step parameters, the system role sets up Bob's capabilities and constraints.

**What it controls:**
- Bob's personality and expertise
- Rules Bob must follow
- What Bob can and cannot do
- How Bob should format responses

---

### 2. User Role (That's You)

The **User** message is what YOU type. It's your question, instruction, or task.

```
┌─────────────────────────────────────────────────┐
│ USER ROLE (Your messages)                       │
├─────────────────────────────────────────────────┤
│ "Explain the PROCESS-PAYMENT paragraph"         │
│ "Add validation for the account number field"   │
│ "Why is this JCL failing with JCL ERROR?"       │
└─────────────────────────────────────────────────┘
```

**Mainframe Analogy:** The User role is like **SYSIN** data — it's the input that drives what the program does.

---

### 3. Assistant Role (Bob's Responses)

The **Assistant** message is Bob's response. It's what the AI generates.

```
┌─────────────────────────────────────────────────┐
│ ASSISTANT ROLE (Bob's replies)                  │
├─────────────────────────────────────────────────┤
│ "The PROCESS-PAYMENT paragraph performs three    │
│  main functions: 1) Validates the payment       │
│  amount... 2) Calls the authorization module... │
│  3) Updates the transaction log..."             │
└─────────────────────────────────────────────────┘
```

**Mainframe Analogy:** The Assistant role is like **SYSOUT** — it's the output produced after processing.

---

### How Roles Work Together

```
┌────────────────────────────────────────────────────────┐
│           CONVERSATION STRUCTURE                        │
├────────────────────────────────────────────────────────┤
│                                                        │
│  SYSTEM:    "You are Bob, an expert developer..."      │
│             (Set once, always active)                   │
│                                                        │
│  USER:      "Explain this COBOL paragraph"             │
│  ASSISTANT: "This paragraph reads customer records..." │
│                                                        │
│  USER:      "Now add error handling to it"             │
│  ASSISTANT: "I'll add SQLCODE checking after..."       │
│                                                        │
│  USER:      "Also update the copybook"                 │
│  ASSISTANT: "Done. I've added the new field..."        │
│                                                        │
└────────────────────────────────────────────────────────┘
```

---

## Types of Prompts

Different situations call for different types of prompts. Here are the main types:

### Type 1: Question Prompts (Ask for information)

```
"What does the EVALUATE statement do in COBOL?"
"Why would I get an S0C7 ABEND?"
"What's the difference between COMP and COMP-3?"
```

**Best for:** Learning, understanding, getting explanations.

---

### Type 2: Instruction Prompts (Tell it what to do)

```
"Add error handling after every EXEC SQL statement in this program"
"Refactor this nested IF into an EVALUATE"
"Create a JCL to run program BATCH001 with the TEST region"
```

**Best for:** Getting Bob to take action, make changes, create something.

---

### Type 3: Contextual Prompts (Provide background + ask)

```
"This program processes daily bank transactions. The CALC-INTEREST 
paragraph is running slowly. Suggest optimization approaches."
```

**Best for:** Complex tasks where Bob needs background to give good answers.

---

### Type 4: Refinement Prompts (Adjust previous response)

```
"Make it shorter"
"Add more detail about the error handling"
"Use PERFORM THRU instead of inline PERFORM"
"Also handle the case where the file is empty"
```

**Best for:** Iterating on Bob's output until it matches your needs.

---

### Type 5: Multi-Step Task Prompts (Complex goals)

```
"I need to add a new CUSTOMER-EMAIL field to the system:
1. Add it to the CUSTOMER-RECORD copybook
2. Update the input validation program
3. Modify the DB2 INSERT statement
4. Add it to the report output"
```

**Best for:** Large tasks where you outline the full scope upfront.

---

### Type 6: Example-Based Prompts (Show what you want)

```
"Convert this paragraph to use STRING:

Currently:
    MOVE FIRST-NAME TO WS-OUTPUT(1:20)
    MOVE LAST-NAME TO WS-OUTPUT(21:30)

I want it like:
    STRING FIRST-NAME DELIMITED SPACES
           ' '       DELIMITED SIZE
           LAST-NAME DELIMITED SPACES
           INTO WS-FULL-NAME
    END-STRING"
```

**Best for:** When showing an example is clearer than describing what you want.

---

## Tips for Better Prompts

### ✅ DO:

| Tip | Example |
|-----|---------|
| **Be specific** | "Fix the S0C7 in paragraph CALC-TAX" not "Fix the bug" |
| **Provide context** | "This runs in CICS, not batch" |
| **State the goal** | "I want to add logging for debugging" |
| **Mention constraints** | "Don't change the copybook structure" |
| **Reference files** | "Look at PAYMNT01.cbl line 245" |

### ❌ DON'T:

| Avoid | Why |
|-------|-----|
| "Fix my code" | Too vague — which code? What's wrong? |
| "Make it better" | Better how? Faster? More readable? |
| "Do everything" | Break large tasks into clear steps |
| One-word prompts | "COBOL" — what about COBOL? |

---

## Prompt Structure Formula

For best results, structure complex prompts like this:

```
┌─────────────────────────────────────────────┐
│  CONTEXT   + ACTION    + CONSTRAINTS        │
│                                             │
│  "In the   | Add error | Keep the existing │
│   PAYMENT  | handling  | business logic    │
│   program" | to all    | unchanged and     │
│            | DB2 calls"| use standard      │
│            |           | error copybook"   │
└─────────────────────────────────────────────┘
```

**Example:**
```
"In the BATCH-PROCESS program (BATCHP01.cbl), add validation 
for the ACCOUNT-NUMBER field to check it's numeric and 9 digits. 
If invalid, write an error record to the REJECT-FILE and continue 
processing the next record."
```

This gives Bob:
- **Context:** Which program, which field
- **Action:** What to do (validate)
- **Constraints:** The rules (numeric, 9 digits, how to handle errors)

---

## Key Takeaways

| Concept | Summary |
|---------|---------|
| **Prompt** | Any text input you give to Bob |
| **System Role** | Hidden instructions defining Bob's behavior |
| **User Role** | Your messages (questions, instructions) |
| **Assistant Role** | Bob's responses |
| **Best practice** | Be specific, provide context, state your goal |
| **Prompt types** | Question, Instruction, Contextual, Refinement, Multi-step, Example-based |

---

*← Previous: Introduction to Bob | Next: What is Context →*
