# Session-005 — Analysis Case Concept

**Asset:** CM-001
**Asset Name:** Core Concept — Analysis Case
**Status:** Freeze Candidate

---

## 1. Definition

**Analysis Case** is the core business object (Core Business Object) managed by CEAP.

It represents:

> One complete analysis lifecycle around the same business problem, from problem discovery to final conclusion.

Analysis Case is the platform-managed object.
Not a single analysis activity.

---

## 2. Why

Past many platforms managed:

- A single Log
- A single analysis
- A single report

None of these are what the enterprise truly cares about.

What the enterprise truly cares about is:

> Whether a problem was ultimately resolved.

**Example:** "WhatsApp image sending delay abnormal" is a Case.
Not a single Log. Not a single analysis.

---

## 3. Analysis Case Lifecycle

```
Problem Report
    ↓
Case Created
    ↓
Evidence Collection
    ↓
Multiple Analysis Sessions
    ↓
Hypothesis Evolution
    ↓
Root Cause Confirmation
    ↓
Knowledge Extraction
    ↓
Case Closed
```

**Most important:** Analysis Session can happen many times.
Case always has only one.

---

## 4. Analysis Case vs Analysis Session

```
Analysis Case
    ├── Analysis Session #1
    ├── Analysis Session #2
    ├── Analysis Session #3
    └── Analysis Session #N
```

Therefore:

- **Analysis Session** is an Activity.
- **Analysis Case** is a Business Object.

---

## 5. Analysis Case Contents

A complete Analysis Case includes:

```
Case
    ├── Metadata
    ├── Problem Description
    ├── Evidence
    ├── Analysis Sessions
    ├── Findings
    ├── Hypotheses
    ├── Root Cause
    ├── Solution
    └── Knowledge Assets
```

**Note:** Knowledge Assets do not belong to Analysis Session.
They belong to the entire Analysis Case as its final product.

---

## 6. Platform Responsibility

CEAP manages Analysis Cases, not individual reasoning activities.

Therefore, the platform needs to support:

- Multi-expert collaboration
- Multiple analysis rounds
- Multiple test rounds
- Multiple verification versions
- Joint AI and expert participation

All of these occur within the same Analysis Case.

---

## 7. Architecture Consequence

If the platform models around Session:

- Sessions cannot be organized
- Multiple analyses cannot be linked
- Knowledge cannot be uniformly accumulated

Therefore, the platform must model around **Analysis Case**.

---

## 8. Relationship

Current domain relationship:

```
Analysis Case
    ↓
Analysis Session
    ↓
Evidence
    ↓
Reasoning
    ↓
Finding
    ↓
Root Cause
    ↓
Knowledge Assets
```

**Note:** Root Cause is not the end.
Knowledge Assets are the Case's final value output.

---

## 9. Design Constraints

Analysis Case must satisfy:

- One business problem corresponds to one Case.
- One Case can contain unlimited Analysis Sessions.
- One Session belongs to only one Case.
- Knowledge Assets originate from Case, not Session.
- Root Cause can evolve; no requirement for first-analysis certainty.

---

## 10. Freeze Decisions

| ID | Decision | Status |
|----|----------|--------|
| D-019 | Analysis Case is the platform-managed core object | Frozen |
| D-020 | Analysis Session belongs to Analysis Case | Frozen |
| D-021 | Knowledge Assets originate from Analysis Case | Frozen |
| D-022 | Root Cause is not the endpoint; Knowledge Asset is the final output | Frozen |

---

## 11. Self-Review (Active Correction)

I have identified a more important finding than before.

We previously drew:

```
Case
    ↓
Session
    ↓
Evidence
```

While organizing today, I discovered a very important missing concept: **Hypothesis (假设)**.

Because the real expert analysis process is not:

```
Evidence → Root Cause
```

But:

```
Evidence
    ↓
Hypothesis
    ↓
New Evidence
    ↓
Hypothesis Update
    ↓
Evidence
    ↓
Hypothesis Elimination
    ↓
Root Cause
```

That is: **Hypothesis is the bridge connecting Evidence and Reasoning.**

I suggest not rushing to Freeze this conclusion.
Because this is a new architectural discovery (B-type).

If it holds, it will affect the entire CEAP Reasoning Model design.
I suggest making it the key discussion topic for the next Session, rather than writing it into the baseline now.
