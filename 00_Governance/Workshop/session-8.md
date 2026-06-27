# Session-008 — Investigation Concept

**Context:** I believe we have entered the **Domain Modeling** phase. Today we are not just writing documents — we are refining domain objects.

Just now your question made me realize: we are missing one object, and I believe its importance exceeds even Evidence.

---

## New Domain Object: Investigation (调查)

This is something I just derived.

I believe **Evidence Collection** is not a good modeling object.

**Why?**

For example, needing a Server Log.
The expert would not say: "Go collect Evidence."
The expert would say: **"Go investigate the Server."** or **"Get another Log."** or **"Run another test."**

So what really happens is:

> **Investigation (调查)**, not Evidence Collection.

---

## Reorganizing the Entire Process

**Example:**

1. User reports: WhatsApp image sending is slow.
2. Case is created.
3. Session1: reviews Log, Video.
4. Observation: RTT is normal.
5. Observation: Image encoding time is very long.
6. Hypothesis: possibly a Client encoding issue.
7. But evidence is insufficient.
8. Session ends.
9. Output: **Investigation Request** — "Get CPU Profile."
10. Real world: test re-executed.
11. Result: CPU Profile obtained → new Evidence.
12. Enters Case.
13. Session2 begins.

So what really happens:

```
Session
    ↓
Investigation Request
    ↓
Investigation
    ↓
Evidence
    ↓
Session
```

This closed loop is more accurate than Evidence Collection.

- **Evidence Collection** emphasizes action.
- **Investigation** emphasizes business.

**Investigation purpose:** verify a hypothesis.
**Evidence:** just the result of Investigation.

---

## New Domain Model

```
Analysis Case
    ├── Evidence
    ├── Investigation
    ├── Analysis Session
    ├── Observation
    ├── Finding
    ├── Root Cause
    └── Knowledge Assets
```

- Investigation is not analysis.
- Evidence is not analysis.
- Session is the only analysis.

---

## Another Discovery: Observation is Not Produced by Session

Observation is actually the **expert's interpretation of Evidence**.

**Example:**

- Evidence: RTT = 20ms
- Observation: RTT is normal.

This is produced by a **person**, not by facts.

So now we finally separate three things:

```
Evidence    =  Fact (事实)
    ---------
Observation =  Interpretation (解释)
    ---------
Finding     =  Conclusion (结论)
```

**Real example:**

- Evidence: TCP Retransmission = 3%
- Observation: Retransmission rate is slightly elevated.
- Finding: Network has minor packet loss.
- Root Cause: WiFi AP anomaly.

These four layers must never be mixed.

Many past analysis reports were all written as "Finding."
Actually, they mixed Evidence, Observation, and Conclusion.
That is why AI could never learn from them.

---

## Proposed Principle (Not Frozen Yet)

From now on in CEAP:

> Every object must belong to one of four categories:

| Type | Objective? | Example |
|------|-----------|---------|
| Evidence | Objective fact | RTT=20ms, Log, Video, PCAP |
| Observation | Observation of fact | RTT normal, retransmission slightly high |
| Finding | Reasoning conclusion | Network has anomaly |
| Decision | Next action | Capture Server Log, close Case |

This classification has enormous value.
Because it completely separates: **fact, interpretation, reasoning, decision.**

---

## Self-Review (Biggest Gain Today)

I suggest not continuing to write assets for now.
Because I believe we have entered the core of CEAP Domain Model.

I suggest the next round we specifically establish:

> **CM-000 Ubiquitous Language (统一领域语言)**

Define all core concepts clearly:

- Case
- Session
- Evidence
- Investigation
- Observation
- Hypothesis
- Finding
- Root Cause
- Decision
- Knowledge Asset

Once this domain language is frozen, all future assets (PC-001, knowledge model, AI Agent, database, API) will automatically unify.
