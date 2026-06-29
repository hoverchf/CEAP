# ADR-006 Data Layer Specification

**Status:** Accepted
**Version:** v1.0
**Created:** 2026-06-27
**Owner:** Chief Architect
**Reviewer:** Project Owner

---

## Context

From **AR-001 §2.1**: Data Layer manages Evidence collection, upload, storage, download, and platform adaptation. From **BS-001**: Low-value manual work (upload/download/log viewing) is the #1 pain point.

A single Case involves ~10GB of data (AP Log + Modem Log + Net Log + Video + Excel + Test Cases + Background). Transmission is a bottleneck. Data transfer and analysis should proceed in parallel.

---

## Decision

### Data Layer Architecture

```
┌─────────────────────────────────────────────────────┐
│                   Data Layer                         │
├─────────────────────────────────────────────────────┤
│  Data Collector → Upload Manager → Storage Service   │
│                                                     │
│  Storage Service → Download Manager (on-demand)      │
│                                                     │
│  Platform Adapter Layer (MTK / Qualcomm / ...)       │
└─────────────────────────────────────────────────────┘
```

### Module Design

#### 1. Data Collector

**Purpose:** Collect raw data from test devices.

| Field | Detail |
|-------|--------|
| **Data Types** | AP Log, Modem Log, Net Log, Screen Recording, Excel, Test Case Docs, Background Materials |
| **Platforms** | MTK, Qualcomm |
| **Collection Trigger** | Test team executes test case → manual or automated collection |

#### 2. Upload Manager

**Purpose:** Upload collected data to server with reliability guarantees.

| Feature | Design |
|---------|--------|
| **Resumable Upload** | Breakpoint resume for large files |
| **Compression** | Compress before upload to reduce transfer time |
| **Parallel Upload** | Upload multiple files concurrently |
| **Progress Tracking** | Real-time upload progress for test team visibility |
| **SDK Integration** | Phase 5 — replace manual Web upload with SDK integration |

#### 3. Storage Service

**Purpose:** Persistent storage of Case Evidence.

| Feature | Design |
|---------|--------|
| **Storage Size** | ~10GB per Case |
| **Storage Type** | Cloud storage (current) |
| **Hot/Cold Tiering** | Not implemented — all data stored equally; future: cold tier for closed Cases |
| **Retention** | Indefinite — Cases may be re-analyzed; no automatic deletion |
| **Access Pattern** | Read-heavy during analysis; write-heavy during upload |

#### 4. Download Manager

**Purpose:** Download Evidence to local for analysis.

| Feature | Design |
|---------|--------|
| **On-Demand Download** | Download only annotated sections, not full dataset |
| **Granularity** | By module (e.g., "only AP Log") and by time range (e.g., "14:00-14:30") |
| **Parallel Download** | Download multiple segments concurrently |
| **Analysis-Ready** | Download starts while upload is still in progress (parallel pipeline) |

#### 5. Platform Adapter Layer

**Purpose:** Adapt platform-specific log tools for automated access.

| Adapter | Target | Current Status |
|---------|--------|---------------|
| **MTK Adapter** | MTK platform log viewer | Graphical tool — needs automation |
| **Qualcomm Adapter** | Qualcomm platform log viewer | Graphical tool — needs automation |

**Design Principle:**
```
┌─────────────────────────────────────────────┐
│           Platform Adapter Layer             │
├─────────────────────────────────────────────┤
│  MTK Adapter │ Qualcomm Adapter │ Others... │
├─────────────────────────────────────────────┤
│        Common Log Parser Interface          │
├─────────────────────────────────────────────┤
│  AP Log │ Modem Log │ Net Log │ Others     │
└─────────────────────────────────────────────┘
```

- Each platform tool accessed via plugin
- Plugins implement Common Log Parser Interface
- New platform = new plugin, no core engine changes
- Automation method: API if available, UI automation if not

---

## Data Lifecycle

```
[1] Data Collection (Investigation)
    Test team executes test → collects AP Log + Modem Log + Net Log + Video
    ↓
[2] Data Upload
    ~10GB uploaded to server (compressed, resumable)
    ↓
[3] Data Storage
    Storage Service persists all data
    ↓
[4] Data Annotation
    Test team marks key areas → expert knows what to focus on
    ↓
[5] Data Download (On-Demand)
    R&D downloads only relevant segments
    ↓
[6] Data Consumption
    Agent reads Evidence via Harness
    ↓
[7] New Investigation (if needed)
    Expert requests more data → back to [1]
```

---

## Consequences

1. Data transfer and analysis proceed in parallel, reducing wait time.
2. On-demand download reduces unnecessary data transfer.
3. Platform adapter plugin architecture isolates platform-specific complexity.
4. SDK integration (Phase 5) will eliminate manual upload workflow.

---

## Architecture Decisions

| ID | Decision | Status |
|----|----------|--------|
| D-081 | Data transfer and analysis proceed in parallel | Frozen |
| D-082 | On-demand download by module and time range | Frozen |
| D-083 | Upload supports breakpoint resume and compression | Frozen |
| D-084 | Platform adapters use plugin architecture with Common Log Parser Interface | Frozen |
| D-085 | MTK and Qualcomm adapters cover all current scenarios | Frozen |
| D-086 | Adapter automation via API (preferred) or UI automation (fallback) | Frozen |
| D-087 | Storage uses cloud storage, no hot/cold tiering initially | Frozen |
| D-088 | Data retained indefinitely (Cases may be re-analyzed) | Frozen |
| D-089 | SDK integration deferred to Phase 5 | Frozen |
| D-090 | Data annotation by test team enables on-demand download targeting | Frozen |

---

## Cross-References

- **AR-001** Architecture Design — §2.1 Data Layer module design
- **BS-001** Current State — Challenge 1 (low-value manual work), Challenge 2 (tool fragmentation)
- **DM-001** Domain Model — Evidence entity definition
- **CM-003** Ubiquitous Language — Evidence, Investigation definitions
- **ADR-003** Evidence-Driven Analysis — Evidence immutability
