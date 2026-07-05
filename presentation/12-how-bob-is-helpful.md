# How Bob is Going to be Helpful

---

## Overview

Now that you understand Bob's architecture — prompts, context, modes, tools, skills, and workflows — let's tie it all together. This section shows **concrete scenarios** of how Bob helps mainframe developers in their daily work, from simple questions to complex multi-day projects.

---

## Daily Development Tasks

### Morning: Understanding Code You Didn't Write

**Scenario:** You've been assigned to maintain a program written 15 years ago by someone who left the company.

```
YOU: "Explain BATCH-RECONCILE.cbl — give me a high-level overview 
      and then detail the key paragraphs"

BOB: [Reads the entire 3,000-line program]

     "## Program Overview
     BATCH-RECONCILE is a daily batch program that reconciles 
     transaction totals between the POSTING system and the GL system.

     ## Key Paragraphs:
     • 1000-INITIALIZE: Opens 3 files, reads control record
     • 2000-PROCESS-RECORDS: Main loop comparing posting vs GL entries
     • 2500-HANDLE-MISMATCH: Writes discrepancies to exception file
     • 3000-GENERATE-REPORT: Creates summary report for operations
     • 9000-ABEND-HANDLER: Centralized error handling with rollback

     ## Dependencies:
     • Copybooks: POSTREC, GLREC, CTRLREC
     • DB2 Tables: POSTING_DAILY, GL_SUMMARY
     • Input Files: POSTING.DAILY.EXTRACT, GL.DAILY.EXTRACT
     • Output: RECONCILE.EXCEPTIONS, RECONCILE.REPORT"
```

**Time saved:** 2-3 hours of manual code reading → 30 seconds.

---

### Mid-Morning: Writing New JCL

**Scenario:** You need JCL to run a new step in an existing job stream.

```
YOU: "Create a JCL step to unload the CUSTOMER table from DB2 
      for customers with ACCT_STATUS = 'ACTIVE', sort by ACCT_NUM, 
      and write to CUST.ACTIVE.EXTRACT with LRECL=200"

BOB: [Generates complete JCL]

     //UNLOAD   EXEC PGM=DSNTIAUL,REGION=4M
     //STEPLIB  DD  DSN=DB2.SDSNLOAD,DISP=SHR
     //SYSPRINT DD  SYSOUT=*
     //SYSREC00 DD  DSN=CUST.ACTIVE.EXTRACT,
     //             DISP=(NEW,CATLG,DELETE),
     //             SPACE=(CYL,(50,10),RLSE),
     //             DCB=(RECFM=FB,LRECL=200,BLKSIZE=0)
     //SYSIN    DD  *
       SELECT * FROM CUSTOMER
       WHERE ACCT_STATUS = 'ACTIVE'
       ORDER BY ACCT_NUM
     /*
     //*
     //SORT     EXEC PGM=SORT
     //SORTIN   DD  DSN=CUST.ACTIVE.EXTRACT,DISP=SHR
     //SORTOUT  DD  DSN=CUST.ACTIVE.SORTED,
     //             DISP=(NEW,CATLG,DELETE),
     //             SPACE=(CYL,(50,10),RLSE),
     //             DCB=(RECFM=FB,LRECL=200,BLKSIZE=0)
     //SYSIN    DD  *
       SORT FIELDS=(1,10,CH,A)
     /*
```

**Time saved:** 20-30 minutes of manual JCL writing → 1 minute.

---

### Afternoon: Debugging an ABEND

**Scenario:** Your batch job failed with S0C7 in production last night.

```
YOU: "BATCH-PROCESS job ABENDed S0C7 at offset X'0024A6' 
      in program CUSTUPD1. The failing statement is in 
      paragraph 2500-CALC-BALANCE. Help me find the issue."

BOB: [Reads CUSTUPD1.cbl]
     [Analyzes paragraph 2500-CALC-BALANCE]

     "## Root Cause Analysis

     The S0C7 (Data Exception) occurs at line 487:
     
     ```cobol
     COMPUTE WS-NEW-BALANCE = WS-CURRENT-BAL + WS-TRANS-AMT
     ```

     The issue: WS-TRANS-AMT is populated from the input file at 
     line 312 without validation. When the input record has spaces 
     in the amount field (positions 45-55), the MOVE to WS-TRANS-AMT 
     (PIC S9(9)V99 COMP-3) succeeds but leaves non-numeric data.

     ## Fix:
     Add validation before the COMPUTE:
     
     ```cobol
     IF WS-TRANS-AMT IS NUMERIC
         COMPUTE WS-NEW-BALANCE = WS-CURRENT-BAL + WS-TRANS-AMT
     ELSE
         MOVE 'INVALID AMOUNT' TO WS-ERROR-MSG
         PERFORM 9000-ERROR-HANDLER
     END-IF
     ```

     ## Prevention:
     Add input validation in paragraph 2000-READ-INPUT after the 
     MOVE at line 312."
```

**Time saved:** 1-2 hours of dump analysis → 2 minutes.

---

## Weekly Tasks

### Code Reviews

```
YOU: "Review NEWPROG01.cbl for coding standards issues, 
      potential bugs, and performance concerns"

BOB: [Reads the program]

     "## Code Review Findings:

     ### Critical Issues:
     1. Line 234: DB2 SELECT without SQLCODE check — will crash on NOT FOUND
     2. Line 567: COMPUTE without ON SIZE ERROR — potential data truncation

     ### Standards Violations:
     3. Line 45: WORKING-STORAGE fields not prefixed with WS-
     4. Line 112: Paragraph names don't follow ####-VERB-NOUN pattern
     5. Line 300: Missing INITIALIZE before first use of WS-WORK-AREA

     ### Performance Concerns:
     6. Line 400: DB2 SELECT inside PERFORM loop — consider cursor instead
     7. Line 234: SELECT * — specify only needed columns

     ### Suggestions:
     8. Add file status checking after every file operation
     9. Consider adding a record counter for batch logging
     
     Shall I fix any of these?"
```

---

### Impact Analysis for Change Requests

```
YOU: "We need to add 'CUSTOMER-EMAIL PIC X(50)' to the CUSTREC 
      copybook. What's the impact?"

BOB: [Searches entire project for COPY CUSTREC]
     [Reads each affected program]
     [Analyzes usage patterns]

     "## Impact Analysis: Adding CUSTOMER-EMAIL to CUSTREC

     ### Affected Programs (7 total):
     | Program | Uses CUSTREC | Impact Level | Changes Needed |
     |---------|-------------|--------------|----------------|
     | CUSTUPD1 | Input/Update | HIGH | Add field to UPDATE SQL |
     | CUSTRPT2 | Report | MEDIUM | Add to report layout |
     | CUSTINQ3 | Display | MEDIUM | Add to screen map |
     | BATCH001 | Extract | LOW | Increase LRECL |
     | BATCH002 | Load | HIGH | Add INSERT column |
     | ONLINE01 | Inquiry | LOW | No logic change |
     | MAINT001 | Maintenance | HIGH | Add update screen |

     ### Additional Changes Needed:
     - DB2 DDL: ALTER TABLE CUSTOMER ADD EMAIL VARCHAR(50)
     - BMS Map: Update CUSTINQ screen
     - JCL: Update LRECL from 350 to 400 in 3 DD statements
     - Test data: Add email values to test files

     ### Estimated Effort: 3-4 developer days
     
     Shall I start implementing the changes?"
```

---

## Monthly/Project Tasks

### Program Modernization

```
YOU: "Help me refactor LEGACY01.cbl — it has one 2,000-line 
      paragraph. Break it into logical, maintainable sections."

BOB: [Reads the program]
     [Identifies logical blocks within the giant paragraph]
     [Plans the refactoring]

     "I've analyzed the 2000-PROCESS paragraph. It contains 
      6 distinct logical operations mixed together. Here's my 
      refactoring plan:

      Current: One 2,000-line paragraph
      Proposed: 6 focused paragraphs + orchestrator

      2000-PROCESS (orchestrator - 20 lines)
        ├── 2100-VALIDATE-INPUT (lines 1-180 → 180 lines)
        ├── 2200-LOOKUP-CUSTOMER (lines 181-450 → 270 lines)
        ├── 2300-CALCULATE-CHARGES (lines 451-820 → 370 lines)
        ├── 2400-APPLY-DISCOUNTS (lines 821-1100 → 280 lines)
        ├── 2500-UPDATE-DATABASE (lines 1101-1600 → 500 lines)
        └── 2600-GENERATE-OUTPUT (lines 1601-2000 → 400 lines)

      All business logic preserved. Shall I proceed?"

YOU: "Yes, do it."

BOB: [Refactors the entire program]
     [Preserves all business logic]
     [Adds paragraph-level comments]
     "Done. Refactored into 6 paragraphs. All logic preserved."
```

---

### Documentation Generation

```
YOU: "Generate complete documentation for all programs 
      in the PAYMENTS subsystem"

BOB: [Identifies all payment programs]
     [Reads each one]
     [Generates comprehensive documentation]

     Creates:
     - System overview document
     - Program-by-program documentation
     - Data flow diagrams
     - Copybook field descriptions
     - JCL job stream documentation
     - Dependency matrix
```

---

## How Bob Helps Different Roles

| Role | How Bob Helps |
|------|---------------|
| **Junior Developer** | Explains legacy code, teaches COBOL patterns, catches mistakes |
| **Senior Developer** | Speeds up routine tasks, handles bulk changes, generates docs |
| **Team Lead** | Impact analysis, code reviews, project planning |
| **Operations** | JCL debugging, ABEND analysis, job stream documentation |
| **Business Analyst** | Code-to-English translation, business rule extraction |

---

## The Multiplier Effect

Bob doesn't just save time — it **multiplies your effectiveness**:

```
┌─────────────────────────────────────────────────────────┐
│          DEVELOPER PRODUCTIVITY WITH BOB                 │
├─────────────────────────────────────────────────────────┤
│                                                         │
│  Understanding Code:     3 hours  →  5 minutes    (36x) │
│  Writing JCL:            30 min   →  2 minutes    (15x) │
│  Debugging ABENDs:       2 hours  →  10 minutes   (12x) │
│  Code Reviews:           1 hour   →  5 minutes    (12x) │
│  Impact Analysis:        4 hours  →  15 minutes   (16x) │
│  Documentation:          2 days   →  2 hours      (8x)  │
│  Refactoring:            3 days   →  3 hours      (8x)  │
│                                                         │
│  Average Productivity Multiplier: ~10x                  │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

---

## Key Takeaways

| Scenario | Bob's Value |
|----------|-------------|
| **Understanding legacy code** | Instant explanations of any program |
| **Writing new code** | Generates correct COBOL/JCL/SQL in seconds |
| **Debugging** | Pinpoints bugs without dump analysis |
| **Code reviews** | Systematic, thorough, consistent review |
| **Impact analysis** | Finds all dependencies automatically |
| **Documentation** | Auto-generates comprehensive docs |
| **Refactoring** | Restructures code while preserving logic |
| **Knowledge transfer** | Always-available expert mentor |

---

*← Previous: What is Workflows | Next: Pros of Bob →*
