# Session-007 — Architecture Refactoring

**Status:** Architectural Correction (not new content)

---

## Context

I discovered a problem in our current model.

Currently we have:

```
Analysis Case
    ↓
Analysis Session
    ↓
Evidence
    ↓
Finding
    ↓
Root Cause
    ↓
Knowledge Asset
```

**The problem:** Evidence is not the next layer of Session.
Rather: **Evidence is an asset of Case.**
Session only:

- **Consumes** Evidence
- **Produces** Evidence (this was wrong — corrected in Session-008)

**Example:**

- First analysis produces: Wireshark Log, Video
- Second analysis produces: Server Log, DB Log
- Third analysis produces: Trace

So Evidence is continuously growing. It is not unique to any Session.

---

## Proposed Model Change

```
Analysis Case
    ├── Evidence
    ├── Analysis Session
    ├── Findings
    ├── Hypotheses
    ├── Root Cause
    └── Knowledge Assets
```

Session and Evidence are no longer parent-child.
They are peers under Case.

### Session's True Input/Output

```
Evidence
    ↓
Analysis Session
    ↓
Session Output
    ├── New Evidence
    ├── Findings
    ├── Hypotheses
    ├── Decisions
    └── Next Actions
```

These outputs return to Analysis Case.

This supports multiple Sessions sharing the same Evidence:

```
Case
    ├── Evidence #1
    ├── Evidence #2
    ├── Evidence #3

Session1: uses Evidence1, Evidence2
Session2: uses Evidence2, Evidence3
Session3: reuses Evidence1
```

This is the real analysis process.

---

## Second Correction: Observation vs Finding

We have been saying "Finding."
Today I believe: **Finding is not the final object.**

The true platform object should be called: **Observation (观察)**.

**Why?**

- **Finding** easily understood as "already determined."
- Actually, often the expert only **discovers** that "RTT is getting longer."
- This is an **Observation**, not a Finding.

**Finding** should represent a conclusion after reasoning.

Therefore:

```
Evidence
    ↓
Observation
    ↓
Reasoning
    ↓
Finding
```

This is much more accurate than `Evidence → Finding`.

### New Reasoning Model

```
Evidence
    ↓
Observation
    ↓
Hypothesis
    ↓
Reasoning
    ↓
Finding
    ↓
Root Cause
```

Root Cause may still be updated.

---

## Two Major Discoveries Today (Not Frozen Yet)

### B-001

- Evidence belongs to Analysis Case.
- Session consumes and produces Evidence.

### B-002

- Observation and Finding must be strictly distinguished.
- **Observation:** observed fact.
- **Finding:** reasoning conclusion.

---

## Self-Review

I believe this is the most important model correction we have discussed so far.
Because it completely separates:

- **Fact (事实)** and
- **Conclusion (结论)**

This is a common principle of all reasoning systems (scientific research, fault analysis, medical diagnosis).

**Suggestion:** Do not freeze these two findings immediately.
They will affect:

- Evidence Model
- Reasoning Model
- Knowledge Model
- AI Agent

I suggest completing CM-003 Evidence first, then doing a full domain model review before deciding whether to formalize them as baseline content. This ensures model stability and avoids local optimizations affecting overall consistency.
