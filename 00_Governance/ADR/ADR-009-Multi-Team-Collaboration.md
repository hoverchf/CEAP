# ADR-009 Multi-Team Collaboration

**Status:** Accepted
**Version:** v1.0
**Created:** 2026-06-27
**Owner:** Chief Architect
**Reviewer:** Project Owner

---

## Context

From **DM-001 §15**: A Case involves multiple teams — Application, Performance, Platform, Protocol. Teams collaborate through Session outputs. Some work is parallel (each team analyzes its own module), some is serial (one Session's output triggers another team's Session).

This document defines the collaboration protocol, Session orchestration, and cross-team data flow.

---

## Decision

### Team Model

```
Analysis Case
    └── Sessions (multi-team)
            ├── Application Team
            │       └── Session #1: Analyze AP Log
            │       └── Session #2: Analyze Investigation result
            ├── Performance Team
            │       └── Session #1: Analyze performance metrics
            ├── Platform Team
            │       └── Session #1: Analyze system layer
            └── Protocol Team
                    └── Session #1: Analyze Modem/Net Log
```

### Collaboration Patterns

#### Pattern 1: Parallel Analysis

```
Application Team Session #1 → Finding: "AP layer normal"
Performance Team Session #1 → Finding: "Performance normal"
Platform Team Session #1 → Finding: "System normal"
Protocol Team Session #1 → Finding: "Network has packet loss"
```

All teams analyze simultaneously. Each produces Findings that are shared in the Case.

#### Pattern 2: Serial Analysis

```
Protocol Team Session #1 → Finding: "Network has packet loss"
    ↓
Triggers Investigation: "Capture WiFi AP configuration"
    ↓
Investigation completes → New Evidence added to Case
    ↓
Protocol Team Session #2 → Analyzes new Evidence
    ↓
Finding: "WiFi AP configuration anomaly"
```

One team's output triggers Investigation → new Evidence → another team's Session.

#### Pattern 3: Cross-Team Dependency

```
Application Team Session #1 → Finding: "AP layer anomaly"
    ↓
Performance Team Session #1 reads Application Team Finding
    ↓
Performance Team Session #1 → Finding: "Performance degradation caused by AP anomaly"
```

Teams can read each other's Findings and incorporate them into their own analysis.

### Session Orchestration

```
Session Orchestrator
    ├── Parallel Scheduler
    │       └── Launches independent Sessions simultaneously
    ├── Dependency Resolver
    │       └── Detects cross-team dependencies
    └── Serial Executor
            └── Chains Sessions based on dependency resolution
```

**Orchestration Rules:**

1. **Independent Sessions** run in parallel (no cross-team dependencies)
2. **Dependent Sessions** run in series (one team's output triggers another)
3. **Investigation-triggered Sessions** wait for Investigation completion
4. **Expert override**: Expert can force serial or parallel execution

### Data Flow

```
Team A Session completes
    ↓
Produces: Findings + Investigation Requests
    ↓
Written to Case Shared Space
    ↓
Team B reads from Case Shared Space
    ↓
Team B Session starts (with Team A's Findings as input)
```

### Team Assignment

| Team | Responsibility | Typical Session Focus |
|------|---------------|----------------------|
| **Application** | AP layer analysis | AP Log, application-level metrics |
| **Performance** | Performance analysis | Performance counters, throughput, latency |
| **Platform** | System layer analysis | OS, kernel, drivers |
| **Protocol** | Network/Signaling analysis | Modem Log, Net Log, protocol state machines |

---

## Consequences

1. Teams can work independently (parallel) when no cross-dependencies exist.
2. Cross-team dependencies are resolved automatically by Session Orchestrator.
3. Expert can override orchestration when needed.
4. All Session outputs are shared in Case Shared Space.

---

## Architecture Decisions

| ID | Decision | Status |
|----|----------|--------|
| D-105 | Teams collaborate through Session outputs, not directly | Frozen |
| D-106 | Parallel sessions run simultaneously when independent | Frozen |
| D-107 | Serial sessions chain based on dependency resolution | Frozen |
| D-108 | Session Orchestrator manages parallel/serial execution | Frozen |
| D-109 | Expert can override orchestration | Frozen |
| D-110 | All Session outputs written to Case Shared Space | Frozen |
| D-111 | Four standard teams: Application, Performance, Platform, Protocol | Frozen |
| D-112 | Investigation completion gates dependent Sessions | Frozen |
| D-113 | Cross-team dependencies detected by Dependency Resolver | Frozen |
| D-114 | Team assignments are flexible (can add/remove teams) | Frozen |

---

## Cross-References

- **DM-001** Domain Model — Multi-Team Collaboration (§15)
- **ADR-001** Analysis Case — Case as container for multi-team sessions
- **ADR-005** Agent Behavior — Agent orchestrates Sessions
- **ADR-008** Structured Output — Each Session produces structured output
- **CM-003** Ubiquitous Language — Team, Session, Investigation definitions
