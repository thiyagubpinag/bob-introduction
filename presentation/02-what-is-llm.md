# What is LLM (Large Language Model)

---

## Overview

LLM stands for **Large Language Model**. It is the core technology that powers modern AI assistants like IBM Bob. This section explains what an LLM actually is and how it works.

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

## How We Got Here

AI didn't appear overnight. It went through four distinct eras over 60+ years. Understanding this journey shows *why* today's LLMs are so powerful.

```
─────────────────────────────────────────────────────────────────────────────
  1960s–1980s         1990s–2000s         2010s              2017–Today
  ───────────         ───────────         ─────              ──────────
  ERA 1               ERA 2               ERA 3              ERA 4
  RULE-BASED          STATISTICAL         NEURAL             TRANSFORMER
  AI                  AI                  NETWORKS           LLMs
  ───────────         ───────────         ─────              ──────────
  Humans write        AI learns           AI learns          AI learns
  every rule          probabilities       patterns via       relationships
  by hand             from data           deep layers        across context
  ───────────         ───────────         ─────              ──────────
  "IF input           "Word X is          Multi-layer        Attention
  contains ERROR      followed by         networks           mechanism
  THEN respond        word Y 40%          detect             understands
  with message Z"     of the time"        features           full context
  ───────────         ───────────         ─────              ──────────
  Fragile.            Better, but         Much better,       Breakthrough.
  Breaks on           context-free.       slow to train.     GPT, Granite,
  anything new.       Limited scope.      Limited scale.     Claude, etc.
─────────────────────────────────────────────────────────────────────────────
```

### Era 1 — Rule-Based AI (1960s–1980s)

```
HOW IT WORKED:
  Human experts wrote thousands of IF/THEN rules:
    IF message contains "error" AND system = "payment"
    THEN respond with "Check SQLCODE and retry transaction"

MAINFRAME PARALLEL:
  Like writing a massive EVALUATE statement with thousands of WHEN clauses.
  Every possible situation had to be anticipated and coded manually.

THE PROBLEM:
  Real language has infinite variations. Rules couldn't keep up.
  "Payment failed" and "the payment did not go through" mean the same
  thing — but rule-based systems treated them as completely different.
```

### Era 2 — Statistical AI (1990s–2000s)

```
HOW IT WORKED:
  Instead of rules, AI counted patterns in real text:
    "What word usually comes after EXEC SQL?"
    → SELECT (45%), INSERT (30%), UPDATE (20%), DELETE (5%)

  Used these probabilities to predict and generate text.

MAINFRAME PARALLEL:
  Like building a frequency table in WORKING-STORAGE — counting
  how often each word follows another across millions of documents.

THE PROBLEM:
  Still context-free. Each word predicted independently.
  "The bank approved the loan" vs "The river bank flooded" —
  statistical AI couldn't tell "bank" meant different things.
```

### Era 3 — Neural Networks / Deep Learning (2010s)

```
HOW IT WORKED:
  Multiple layers of processing, each extracting higher-level patterns:
    Layer 1: Recognizes individual characters
    Layer 2: Recognizes words
    Layer 3: Recognizes phrases
    Layer 4: Recognizes meaning and intent

  Inspired by how the human brain processes information.

MAINFRAME PARALLEL:
  Like a multi-step batch job where each step refines the data:
    STEP1 (tokenize) → STEP2 (parse) → STEP3 (analyse) → STEP4 (respond)
  Each step builds on the output of the previous one.

THE PROBLEM:
  Still struggled with long-range context.
  "The account was opened in 1995. It was closed in [?]"
  Deep learning lost track of "account" by the time it reached the end.
```

### Era 4 — Transformers & LLMs (2017–Today)

```
HOW IT WORKED:
  Google researchers published "Attention is All You Need" (2017).
  The Transformer architecture introduced the ATTENTION MECHANISM:

  → Every word can "attend to" every other word simultaneously
  → Long-range dependencies are handled natively
  → Scales to billions of parameters efficiently

  This enabled GPT, BERT, IBM Granite, Claude, and all modern LLMs.

MAINFRAME PARALLEL:
  Like a DB2 JOIN that connects every field to every other field
  in the document simultaneously — instead of reading sequentially
  line by line like a COBOL READ loop.

THE BREAKTHROUGH:
  "The account that was opened in New York in 1995 by the customer
   who moved to Chicago was finally closed."

  A Transformer understands "it" = the account, not Chicago or the customer.
  Previous methods could not reliably do this.
```

### The Timeline in One View

```
  1956  ──  Term "Artificial Intelligence" coined (Dartmouth Conference)
  1966  ──  ELIZA: First chatbot (rule-based, pattern matching)
  1980s ──  Expert Systems peak — thousands of hand-coded rules
  1990s ──  Statistical NLP — learning from text corpora
  2003  ──  Neural language models introduced
  2012  ──  Deep Learning breakthrough (ImageNet)
  2017  ──  Transformer architecture published ("Attention is All You Need")
  2018  ──  BERT (Google) — bidirectional language understanding
  2019  ──  GPT-2 (OpenAI) — first large-scale generative model
  2020  ──  GPT-3 — 175B parameters, human-like text generation
  2022  ──  ChatGPT launches — AI goes mainstream
  2023  ──  IBM Granite released — enterprise-grade, code-aware LLMs
  2024  ──  Agentic AI (Bob) — LLMs that plan, act, and use tools
```

**Mainframe context:** COBOL has been around since 1959. The mainframe systems your programs run on are older than most of these AI milestones. The difference now is that AI has *finally* caught up to the complexity of the systems mainframe developers work with every day.

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
| **Era 1 — Rules** | 1960s–1980s: humans coded every IF/THEN by hand — fragile |
| **Era 2 — Statistics** | 1990s–2000s: AI learned word probabilities — context-free |
| **Era 3 — Neural** | 2010s: deep layers extracted meaning — slow, limited scale |
| **Era 4 — Transformer** | 2017–today: attention mechanism, full context, massive scale |
| **IBM Granite** | IBM's enterprise LLM family, trained on code including COBOL |
| **Context Window** | Fixed amount of text the model can consider at once |

---

*← Previous: Why AI is Booming | Next: Gen AI vs Agentic AI →*
