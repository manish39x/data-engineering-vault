# Design: [System Name]

**Date:** YYYY-MM-DD
**Difficulty level:** (junior / mid / senior framing)

## 1. Requirements (clarify first, always)
- Data volume / velocity / variety:
- Batch or real-time:
- Freshness SLA:
- Who consumes this, and how:

## 2. Scale Estimation (show the math)
- Rows/day:
- GB/day:
- Peak throughput:

## 3. High-Level Architecture
[Diagram — even ASCII or a description of boxes/arrows is fine]

Ingestion → Storage → Processing → Serving

| Stage | Tool chosen | Why |
|---|---|---|
| | | |

## 4. Deep Dive (1-2 tricky components)
[Where would an interviewer push? Dedup, late data, schema evolution, exactly-once, skew...]

## 5. Failure Modes & Recovery
[What breaks, how you'd detect it, how you'd recover]

## 6. Cost & Operational Complexity
[This is what separates mid/senior answers from junior ones — always include it]

## 7. What I'd change at 10x / 100x scale
