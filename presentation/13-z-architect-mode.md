# Key Application Analysis Use Cases in Z Architect Mode

> Combining application metadata with multi-model intelligence to deliver context-aware insights that maximise developer productivity and business value.

---

## What is Z Architect Mode?

Z Architect mode is Bob's **analysis and understanding** mode. Instead of writing or editing code, Bob reads your entire application — across hundreds of programs — and gives you deep, architecture-level insights.

```
┌──────────────────────────────────────────────────────────────┐
│                    Z ARCHITECT MODE                          │
├──────────────────────────────────────────────────────────────┤
│                                                              │
│  INPUT:  Your entire application (programs, copybooks,       │
│          JCL, DB2 schemas, CICS maps, metadata)             │
│                                                              │
│  BOB:    Reads everything → builds a complete mental map     │
│          of your application                                 │
│                                                              │
│  OUTPUT: Architecture insights, dependency maps,            │
│          business-aware explanations                        │
│                                                              │
└──────────────────────────────────────────────────────────────┘
```

---

## Use Case 1: Understand Applications Across the Enterprise

### What it Does
Enterprise-scale metadata spans hundreds of programs to provide full application visibility — enabling architecture-aware, model-driven insights that improve accuracy, eliminate blind spots, and drive business-aware understanding.

### The Problem Without Bob
```
Scenario: You join a bank project. The payment system has:
  - 450 COBOL programs
  - 120 copybooks
  - 80 JCL procedures
  - 35 DB2 tables
  - No documentation written since 1998

New developer's reality:
  Week 1:  Reading programs one by one — no idea of the big picture
  Month 1: Understands 10 programs — 440 still unknown
  Month 6: Finally understands the core flow — but still has blind spots
  Year 1:  Reasonably confident — but tribal knowledge gaps remain
```

### With Z Architect Mode
```
YOU:  "Give me a complete overview of the payment system.
       What programs exist, how do they connect, what DB2
       tables do they use, and what is the main business flow?"

BOB:  [Scans all 450 programs, 120 copybooks, 35 DB2 tables]

      "The payment system has 3 main subsystems:

       1. PAYMENT INTAKE (12 programs)
          Entry point: PAYMNT01 → validates card details
          Calls: CARDVAL, LIMITCHK, FRAUDSCR
          DB2 tables: CARD_MASTER, ACCT_LIMIT, FRAUD_RULES

       2. PAYMENT PROCESSING (28 programs)
          Core: PAYPRC01 → orchestrates the transaction
          Calls: AUTHREQ, BALUPD, FEECALC, AUDITLOG
          DB2 tables: TRANSACTION, BALANCE, FEE_SCHEDULE

       3. SETTLEMENT (15 programs)
          Batch: SETLBCH1 runs nightly via SETLJCL1
          Produces: DAILY_SETTLEMENT_REPORT
          Feeds: RECON system via VSAM file SETLFILE

       Key dependency: COPYBOOK CARDDATA is used by 87 programs.
       Changing it will impact the entire system."

Time taken: 3 minutes (vs 6 months manually)
```

### Real Example — Duplicate Mail Checking System
```
Bob analysed DUPCHTBL.cpy and reported:

  Database Tables (DUPCHTBL.cpy)
  Three DB2 tables manage duplicate checking:

  1. DUP_CHECK_APPL  — Application-level config
                       (mailslot, send/recv, app ID, checking flag)
  2. DUP_CHECK_EMAIL — Email addresses for notifications
                       (maintained by NS28DUPE.cbl)
  3. DUP_CHECK_ID    — Specific EDI IDs to include/exclude
                       (maintained by NS29OUPI.cbl)

  Key Features identified:
  • Independent tracking: Sender and receiver maintain separate configs
  • Flexible filtering: All/Exclude/Include modes for EDI ID matching
  • Email notifications: Multiple addresses per mailslot/application
  • Deadlock handling: Automatic retry with configurable limits
  • Audit trail: All checks update audit records with late-update flag
```

---

## Use Case 2: Visualise Application Structure and Dependencies

### What it Does
In-depth, comprehensive analysis of applications, programs, and their dependencies — enabling teams to quickly understand system structure, uncover hidden connections, and confidently navigate large codebases.

### The Problem Without Bob
```
Common questions that take DAYS to answer manually:

  "Which programs call CARDVAL subroutine?"
  → Must grep through 450 programs manually

  "If I change copybook CARDDATA, what breaks?"
  → Must check every COPY statement across all programs

  "What is the call chain from the CICS transaction to DB2?"
  → Must trace PERFORM/CALL chains through multiple programs

  "Which programs write to the SETTLEMENT VSAM file?"
  → Must check all file definitions and WRITE statements
```

### With Z Architect Mode — Dependency Visualisation
```
YOU:  "Show me the full dependency map for PAYMNT01.cbl"

BOB:  "Here is the complete dependency map:

       PAYMNT01.cbl
       ├── CALLS (subprograms)
       │   ├── CARDVAL.cbl   → validates card number format
       │   ├── LIMITCHK.cbl  → checks credit limit (calls DB2)
       │   └── FRAUDSCR.cbl  → fraud scoring (calls FRAUDDB2)
       │
       ├── COPYBOOKS used
       │   ├── CARDDATA.cpy  → card record layout (shared by 87 programs)
       │   ├── ACCTDATA.cpy  → account record layout
       │   └── ERRMSGS.cpy   → standard error messages
       │
       ├── DB2 TABLES accessed
       │   ├── CARD_MASTER    → SELECT only
       │   ├── ACCT_LIMIT     → SELECT only
       │   └── AUDIT_LOG      → INSERT only
       │
       ├── CICS MAPS
       │   └── PAYMAP01       → input screen for payment details
       │
       └── JCL that runs this
           └── PAYMNT.proc    → called by DAILY_PAY_JOB"
```

### Architecture Comparison Diagrams
Bob can generate **current vs proposed** architecture diagrams:

```
9.1 Current Architecture — Duplicate Detection Flow:
  [Duplicate arrives] → [Check DUP_CHECK_APPL] → [Found?]
                                                     ├── YES → [Suppress]
                                                     └── NO  → [Process]

9.2 Proposed Architecture — Duplicate Detection Flow with Alert:
  [Duplicate arrives] → [Check DUP_CHECK_APPL] → [Found?]
                                                     ├── YES → [Suppress]
                                                     │         + [ALERT sent]  ← NEW
                                                     └── NO  → [Process]

9.3 Gap Analysis:
  Current: Silent suppression — operations team never knows
  Proposed: Alert on suppression — full visibility
  Impact: 3 programs need changes (NS28DUPE, NS29OUPI, ALERTSND)
```

---

## Use Case 3: Generate Business-Aware Outputs

### What it Does
Enterprise-specific data dictionaries embed domain context to enable business-aware insights, reduce hallucinations, and accelerate alignment across teams with less SME dependency.

### The Problem — Cryptic Variable Names
```
Mainframe programs written in the 1980s–1990s used short,
cryptic names due to character limits:

  VO-FILE     → What is this?
  WS-MSGQ     → Message queue? Which one?
  DESTCT-*    → Destination control?
  MBX-*       → Mailbox?
  RPT-REPORT  → Which report?

Without context, even experienced developers guess wrong.
AI without a data dictionary makes the same mistakes.
```

### Without a Data Dictionary
```
YOU:  "Explain what this program does"

BOB:  "This program performs inventory/stock validation
       and calculation by cross-referencing data from
       multiple files.
       • VO-FILE: Voucher/order transaction file"

❌ WRONG — VO-FILE is actually a FLIGHT RECORDS file
           This is an aviation system, not an inventory system
```

### With a Data Dictionary
```
YOU:  "Explain what this program does"
      [Data dictionary loaded: Aviation Management System]

BOB:  "This is a Flight/Aviation Management System program
       that processes and calculates flight statistics for pilots.
       The program aggregates distance across multiple flights
       to produce pilot-specific metrics.

       • VO-FILE: Reads FLIGHT records (pilot voyage logs)
       • WS-MSGQ: Message queue for flight dispatch notifications
       • DESTCT-*: Destination control variables (arrival airports)
       • MBX-*: Mailbox identifiers for pilot communications"

✅ CORRECT — Business context = accurate, useful output
```

### What Bob Generates as Output
```
For each program, Bob can produce:

  1. BUSINESS SUMMARY
     "This program calculates monthly interest for savings accounts.
      It reads all active accounts from ACCT_MASTER, applies the
      applicable interest rate from RATE_TABLE, and writes results
      to INTEREST_JOURNAL for overnight batch posting."

  2. TECHNICAL SUMMARY
     "INTCALC01.cbl — 1,247 lines, batch program
      Input:  ACCT-MASTER (VSAM KSDS), RATE-TABLE (DB2)
      Output: INTEREST-JOURNAL (sequential), AUDIT-LOG (DB2)
      Logic:  PERFORM CALC-INTEREST VARYING WS-IDX..."

  3. IMPACT ANALYSIS
     "Changing field ACCT-RATE-CODE in ACCTDATA.cpy will impact:
      • 34 programs that COPY ACCTDATA
      • 8 JCL jobs that process these programs
      • 2 DB2 stored procedures that reference the field"
```

---

## Key Takeaways

| Capability | What Bob Does | Business Value |
|---|---|---|
| **Enterprise Understanding** | Reads 100s of programs at once | Full application visibility in minutes |
| **Dependency Mapping** | Traces all calls, copybooks, DB2, JCL | Impact analysis before any change |
| **Architecture Diagrams** | Current vs proposed flow comparison | Clear communication across teams |
| **Business-Aware Output** | Uses data dictionaries for context | Accurate explanations, less SME dependency |
| **Blind Spot Elimination** | Surfaces hidden connections | No more surprise ABENDs from unknown dependencies |

---

*← Previous: Introduction to Bob | Next: Z Code Mode →*
