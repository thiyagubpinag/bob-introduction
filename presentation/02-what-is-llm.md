# What is LLM (Large Language Model) & History

---

## Overview

LLM stands for **Large Language Model**. It is the core technology that powers modern AI assistants like IBM Bob. This section explains what an LLM actually is, how it works, and how we got here.

---

## What is a Language Model?

A **Language Model** is a system that has learned patterns in human language by reading enormous amounts of text.

**Simple Definition:** A language model predicts "what comes next" in a sequence of words.

### Example:

```
Input:  "The COBOL program has a bug in the ___"
Model:  Predicts → "PROCEDURE DIVISION" or "WORKING-STORAGE SECTION"
```

It doesn't just guess randomly — it uses **patterns** learned from millions of examples to make intelligent predictions.

---

## What Makes It "Large"?

The "Large" in LLM refers to:

| Aspect | Scale |
|--------|-------|
| **Parameters** | Billions of learned values (like billions of tuning knobs) |
| **Training Data** | Trillions of words from books, code, articles, documentation |
| **Compute** | Thousands of GPUs running for weeks/months |

**Mainframe Analogy:** Think of parameters like entries in a massive **lookup table** (similar to a DB2 table with billions of rows). Each parameter stores a tiny piece of knowledge about language patterns.

---

## How Does an LLM Work? (Simplified)

```
┌─────────────────────────────────────────────────┐
│                   LLM Process                    │
├─────────────────────────────────────────────────┤
│                                                  │
│  1. INPUT: "Explain this COBOL paragraph"        │
│           ↓                                      │
│  2. TOKENIZE: Break text into pieces             │
│           ↓                                      │
│  3. PROCESS: Run through neural network layers   │
│           ↓                                      │
│  4. PREDICT: Generate response word by word      │
│           ↓                                      │
│  5. OUTPUT: "This paragraph reads a file..."     │
│                                                  │
└─────────────────────────────────────────────────┘
```

**Mainframe Analogy:**
- **Tokenize** = Like breaking a COBOL statement into its parts (verb, identifier, literal)
- **Process** = Like running through multiple PERFORM sections, each refining the result
- **Predict** = Like a EVALUATE/WHEN choosing the best output based on conditions

---

## What is a Model?

A **model** is the brain of AI — it is the result of training. Think of it as a giant file full of numbers that encodes everything the AI has learned.

```
┌─────────────────────────────────────────────────────────────┐
│                    WHAT IS A MODEL?                         │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│   TRAINING DATA          TRAINING PROCESS      MODEL       │
│   (billions of words) →  (learns patterns)  →  (the brain) │
│                                                             │
│   Like:                                                     │
│   Source code + manuals → Compiler → Load module (.LOAD)   │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

### Mainframe Analogy

| AI World | Mainframe World |
|---|---|
| Training data | Source code (COBOL, JCL) |
| Training process | Compilation + link-edit |
| Model (the result) | Load module in a PDS |
| Running the model | Executing the load module |
| Model parameters | The machine code instructions inside the load module |

### Model = Millions of Numbers

```
A model is literally a huge file of decimal numbers called parameters:

  GPT (OpenAI)         
  Claude (Anthropic)   
  IBM Granite (IBM)

These numbers are NOT rules someone wrote.
The AI LEARNED them automatically by reading billions of words.

Like: No one wrote the COBOL rules into the model.
      It read millions of COBOL programs and figured out the rules itself.
```

### Different Models for Different Jobs

```
Model Size    Parameters    Good For
──────────    ──────────    ────────────────────────────────
Small         1–7B          Quick answers, simple tasks, runs on laptop
Medium        7–70B         Coding, analysis, most enterprise tasks
Large         70B–1T        Complex reasoning, research, creative writing
```

---


## IBM Granite Models

IBM developed its own family of LLMs called **Granite**:

- **Purpose-built for enterprise** — trained on business and technical content
- **Trained on code** — understands COBOL, JCL, PL/I, Assembler, and more
- **Transparent** — IBM discloses training data sources
- **Governance-ready** — designed for regulated industries (banking, insurance)

Bob uses these enterprise-grade models to understand and assist with mainframe development.

---

## Key Concepts to Remember

### Tokens
LLMs don't read "words" — they read **tokens** (pieces of words):

```
"WORKING-STORAGE" → ["WORK", "ING", "-", "STOR", "AGE"]  (5 tokens)
"PERFORM"         → ["PERFORM"]                           (1 token)
```

### Context Window
The **context window** is how much text the LLM can "see" at once.

**Mainframe Analogy:** Think of it like **WORKING-STORAGE** — it has a fixed size. Everything the AI is considering must fit in this space. Larger context windows = can read bigger programs at once.

### Training vs. Inference
- **Training** = Teaching the model (happens once, takes weeks, costs millions)
- **Inference** = Using the model to answer questions (happens every time you chat)

**Mainframe Analogy:**
- Training = Compiling a COBOL program (done once, produces the load module)
- Inference = Running the load module (done many times, produces output)

---

## Key Takeaways

| Point | Summary |
|-------|---------|
| **LLM** | A system trained on massive text data that understands and generates language |
| **Large** | Billions of parameters, trillions of training words |
| **How it works** | Predicts next words based on learned patterns |
| **History** | Rules → Statistics → Deep Learning → Transformers |
| **IBM Granite** | IBM's enterprise LLM family, trained on code including COBOL |
| **Context Window** | Fixed amount of text the model can consider at once |

---

*← Previous: Why AI is Booming | Next: Gen AI vs Agentic AI →*
