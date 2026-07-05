# Key Development Use Cases in Z Code Mode

> Perform complex, time-intensive development tasks by leveraging intelligent partners and automated workflows to achieve faster, more efficient outcomes.

---

## What is Z Code Mode?

Z Code Mode is Bob's **active development** mode. Instead of just analysing, Bob rolls up its sleeves — it writes code, fixes bugs, modernises programs, and resolves issues directly inside your codebase.

```
┌──────────────────────────────────────────────────────────────┐
│                      Z CODE MODE                             │
├──────────────────────────────────────────────────────────────┤
│                                                              │
│  INPUT:  Your task in plain English                          │
│          ("Add error handling to all DB2 calls")             │
│                                                              │
│  BOB:    Plans → Reads files → Makes changes →              │
│          Verifies → Reports                                  │
│                                                              │
│  OUTPUT: Working, standards-compliant code changes          │
│          directly applied to your programs                  │
│                                                              │
└──────────────────────────────────────────────────────────────┘
```

---

## Use Case 1: Execute Complex Coding Tasks

### What it Does
Implement new features by generating, refining, and transforming code aligned to enterprise standards through an agentic chat interface — improving developer productivity, reducing technical debt, and lowering change risk.

### The Problem Without Bob
```
Scenario: You need to add a new field ACCT-TIER to 35 programs.

Manual process:
  Step 1:  Find all programs that use ACCT-MASTER copybook
           → grep through 450 programs (30 mins)
  Step 2:  Update copybook ACCTDATA.cpy with new field
           → 15 mins
  Step 3:  Update each of the 35 programs:
           → Add MOVE statement
           → Add to DB2 SELECT list
           → Add to output record
           → Each program: 20-30 mins
  Total:   35 programs × 25 mins = ~15 hours of repetitive work
  Risk:    Miss one program → production ABEND
```

### With Z Code Mode
```
YOU:  "Add field ACCT-TIER PIC X(2) to the ACCTDATA copybook
       and update all programs that use it to include this
       field in their DB2 SELECT statements and output records."

BOB:  [Plans the task]
      "I'll complete this in 4 steps:
       1. Update ACCTDATA.cpy with the new field
       2. Find all 35 programs using this copybook
       3. Update each program's DB2 SELECT and MOVE statements
       4. Verify consistency across all changes"

      [Executes step by step]
      [Updates ACCTDATA.cpy]
      [Updates PAYMNT01.cbl — added ACCT-TIER to SELECT, MOVE]
      [Updates INTCALC01.cbl — added ACCT-TIER to SELECT, MOVE]
      ... (35 programs)

      "Done. Updated ACCTDATA.cpy and 35 programs.
       All DB2 SELECT statements and MOVE operations updated.
       No programs were missed."

Time: 8 minutes (vs 15 hours manually)
Risk: Zero — Bob checked every program systematically
```

### Real Example — Program Scan & Data Dictionary Generation
```
Bob completed for N932PNRP.cbl:

  Completed Tasks:
  • Scanned N932PNRP.cbl program using scan_program tool
  • Extracted 88 variables from the scanned database
  • Generated comprehensive descriptions for all variables
    based on COBOL naming conventions and program context
  • Created data dictionary file at .bob/DD.json
  • Updated AGENTS.md with data dictionary location
    and synchronisation strategy

  Data Dictionary Details:
  • Location: .bob/DD.json
  • Total Variables: 88
  • Includes descriptions for all working storage, copybook,
    and linkage section variables

  Key Variable Categories:
  • Error handling (MSGQ-*, SCWI-CICS-RESPONSE)
  • Report file operations (RPT-, REPORT-)
  • Destination control (DESTCT-*)
  • Mailbox configuration (MBX-*)
  • Output queue processing (OUTS-*)
  • Communication area fields (N932-*)
  • Working storage fields (WS-*)
```

---

## Use Case 2: Accelerate Code Modernisation Workflows

### What it Does
Align models with Z-specific standards using IBM-curated insights, chat-enabled tools, and application context to deliver intelligent, governance-ready guidance with full architectural awareness for enterprise-scale applications.

### The Problem Without Bob
```
Modernisation tasks that take weeks manually:

  "Analyse impact of modifying the duplicate-email logic"
  → Must read all related programs, understand the flow,
    identify all touch points, write an impact document
  → 3–5 days for an experienced developer

  "Migrate COBOL program from IMS to DB2"
  → Understand current IMS calls
  → Map to equivalent DB2 operations
  → Rewrite all DL/I calls
  → Test each scenario
  → Weeks of work
```

### With Z Code Mode — Impact Analysis Example
```
YOU:  "Create an impact analysis and implementation plan
       to modify the duplicate-email prevention logic
       in this codebase."

BOB:  "I'll start by gathering context about the
       duplicate-email prevention logic. Let me explore
       the project structure and relevant files."

      [Uses Z Understand MCP tool to get project metadata]
      [I want to use a tool on the z-understand-analysis MCP server]
      → z-understand-analysis: get_programs
        "Retrieves all programs in a project. Returns program
         details including program ID, name, type, location,
         and metadata."
      → Finds: N5280UPE.cbl, N5290UPI.cbl
        (the duplicate detection programs)

      "Impact Analysis — Duplicate Email Prevention:

       AFFECTED PROGRAMS (3):
       • N5280UPE.cbl — Core duplicate detection logic
         Change: Add alert trigger on suppression event
       • N5290UPI.cbl — EDI ID include/exclude management
         Change: Pass suppression flag to alerting module
       • ALERTSND.cbl — NEW program required
         Purpose: Send operational alert when duplicate suppressed

       AFFECTED DB2 TABLES (2):
       • DUP_CHECK_APPL — Add ALERT_ENABLED column
       • AUDIT_LOG — Add ALERT_SENT indicator

       IMPLEMENTATION PLAN:
       Phase 1: Add ALERT_ENABLED flag to DUP_CHECK_APPL (1 day)
       Phase 2: Modify N5280UPE to check flag + call ALERTSND (2 days)
       Phase 3: Create ALERTSND program (2 days)
       Phase 4: Testing + regression (3 days)
       Total: ~8 days (vs 3–5 weeks manually)"
```

### Standards Alignment — Automatic
```
Bob knows Z-specific enterprise standards and applies them automatically:

  BEFORE (your existing code — missing standards):
    EXEC CICS READ FILE('CUSTFILE')
         INTO(WS-CUST-RECORD)
         RIDFLD(WS-CUST-ID)
    END-EXEC

  AFTER (Bob modernises to enterprise standards):
    EXEC CICS READ FILE('CUSTFILE')
         INTO(WS-CUST-RECORD)
         RIDFLD(WS-CUST-ID)
         RESP(WS-CICS-RESP)           ← Added RESP
         RESP2(WS-CICS-RESP2)         ← Added RESP2
    END-EXEC
    IF WS-CICS-RESP NOT = DFHRESP(NORMAL)  ← Added check
       PERFORM 9999-CICS-ERROR             ← Added handler
    END-IF
```

---

## Use Case 3: Optimise, Debug, and Improve Code Quality

### What it Does
Improve performance and maintainability through prioritised insights and automated issue resolution — lowering risk, reducing downtime, while enabling faster, higher-quality releases.

### ZCodeScan — Automated Quality Analysis
```
Bob's ZCodeScan identifies critical issues automatically:

YOU:  "Run ZCodeScan on N932PNRP.cbl"

BOB:  "ZCodeScan Critical Issues Fixed in N932PNRP.cbl

       1. Added RESP Options (3 locations)
          Line 73:  EXEC CICS HANDLE ABEND  — Added RESP option
          Line 341: EXEC CICS ASKTIME       — Added RESP option
          Line 343: EXEC CICS FORMATTIME    — Added RESP option

       2. Added NOHANDLE Options (6 locations)
          Line 73:  EXEC CICS HANDLE ABEND
          Line 114: EXEC CICS READ DATASET
          Line 205: EXEC CICS WRITE FILE
          Line 254: EXEC CICS WRITE FILE
          Line 341: EXEC CICS ASKTIME
          Line 343: EXEC CICS FORMATTIME

       3. Added END-CALL Statements (2 locations)
          Line 235: CALL WS-N74BTSIN-PROGRAM
          Line 331: CALL WS-N6RIMCMP-PROGRAM

       Impact:
       • Prevents unhandled CICS abends — improves error handling
       • Ensures proper control flow with explicit END-CALL statements
       • Follows CICS best practices for reliability and maintainability
       • All changes maintain backward compatibility with existing logic"
```

### Performance Optimisation Example
```
YOU:  "This batch job is taking 4 hours. Help me optimise it."

BOB:  [Reads SETLBCH1.cbl and SETLJCL1.jcl]

      "I found 3 major performance issues:

       ISSUE 1 — DB2 query in a loop (critical)
         Line 445: EXEC SQL SELECT * FROM TRANSACTION
                   WHERE ACCT-ID = :WS-ACCT-ID
         This runs once per account — if 500,000 accounts exist,
         that's 500,000 individual DB2 calls.
         FIX: Use a cursor with bulk fetch (array of 1000 rows)
         Estimated saving: 2.5 hours

       ISSUE 2 — Sorting already-sorted data
         Line 892: SORT WORK-FILE ON ACCT-ID
         ACCT-ID is already sorted from the input VSAM file.
         FIX: Remove the SORT step entirely
         Estimated saving: 45 minutes

       ISSUE 3 — Redundant copybook fields in I/O area
         WS-OUTPUT-RECORD is 4,000 bytes but only 800 bytes used
         FIX: Restructure output record to 800 bytes
         Estimated saving: 20 minutes

       Total estimated saving: ~3.5 hours
       New expected runtime: ~30 minutes"
```

### Bug Detection Before Production
```
YOU:  "Review PAYMNT01.cbl for potential issues before release"

BOB:  "Found 4 issues:

       HIGH RISK:
       1. Line 234 — S0C7 risk
          COMPUTE WS-TOTAL = WS-AMT1 + WS-AMT2
          WS-AMT1 is filled from CARD-DATA which can contain
          spaces if card swipe fails. Add NUMERIC check before compute.

       2. Line 456 — Missing SQLCODE check
          EXEC SQL UPDATE ACCT_BALANCE ...
          No SQLCODE check after UPDATE. If DB2 fails silently,
          balance will not update but program returns success.

       MEDIUM RISK:
       3. Line 178 — Hardcoded date
          MOVE '2024-12-31' TO WS-EXPIRY-DATE
          This will cause issues after 2024.

       4. Line 89 — Open cursor never closed
          EXEC SQL OPEN ACCT-CURSOR
          No corresponding CLOSE CURSOR found in program.
          DB2 resource leak."
```

---

## Z Architect vs Z Code Mode — When to Use Which

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
  overview"                         ✓ "Generate unit test cases"

MODE: Read, Analyse, Understand     MODE: Write, Fix, Improve, Build
```

---

## Key Takeaways

| Capability | What Bob Does | Business Value |
|---|---|---|
| **Complex Coding Tasks** | Implements changes across all affected programs | Hours of work done in minutes |
| **Data Dictionary Generation** | Scans programs, extracts & describes all variables | Self-documenting codebase |
| **Modernisation** | Applies Z standards, RESP handling, END-CALL | Governance-ready, compliant code |
| **Impact Analysis** | Full plan before any change is made | Lower risk, no surprise ABENDs |
| **ZCodeScan** | Finds and fixes critical issues automatically | Fewer production incidents |
| **Performance** | Identifies bottlenecks with estimated savings | Faster batch, lower CPU cost |
| **Bug Detection** | Catches S0C7, missing SQLCODE, resource leaks | Quality gates before release |

---

*← Previous: Z Architect Mode | Next: Topic 15 →*
