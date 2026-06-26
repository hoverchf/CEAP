# ADR-001 Analysis Session as Core Domain Object

Status

Accepted

---

## Context

Traditional communication problem analysis revolves around logs, videos and tools.

This makes platform capabilities fragmented and difficult to evolve.

The platform requires a single stable domain object that can organize tools, workflows, AI, knowledge and collaboration.

---

## Decision

Analysis Session is defined as the Core Domain Object of CEAP.

The platform manages Analysis Sessions rather than individual logs, parsers or AI agents.

An Analysis Session represents one complete problem analysis process.

Each Analysis Session includes:

- Test Context
- Observation
- Reasoning Process
- Evidence
- Verification
- Root Cause
- Knowledge Output

---

## Consequences

All platform capabilities should be organized around Analysis Sessions.

Examples:

- Log Download
- Timeline Construction
- Evidence Collection
- AI Reasoning
- Knowledge Extraction

are all services supporting Analysis Sessions.

Analysis Session becomes the center of future architecture evolution.