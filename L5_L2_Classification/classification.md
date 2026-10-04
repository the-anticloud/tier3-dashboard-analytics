# L5 Narrow / L2 General Classification — dashboard-analytics
**Platform:** Anticloud | **PAX:** 27B | **IP:** USPTO pending 2026, Anticloud FZ LLE
**Domain:** Sovereign web dashboard: real-time visualization of Anticloud metrics and AIOSS chain

## L5 Narrow
dashboard-analytics specializes in sovereign web dashboard: real-time visualization of anticloud metrics and aioss chain within the Anticloud sovereign deployment boundary. All operations stay local — no cloud services, no external APIs, no data exfiltration. The narrow scope ensures deterministic, auditable behavior that PAX 27B can reason about precisely.

## L2 General
L2 General means dashboard-analytics is available to all 9 Anticloud tiers without per-tier configuration. The same API serves hospital, defense, robotics, and research deployments.

## PAX Integration
PAX 27B powers the natural language query bar in the dashboard: 'Show me inference throughput for TIER_7 projects this week' triggers PAX to generate the correct analytics query.

## AIOSS Audit Relevance
Every dashboard session (view hash + time range + metrics snapshot hash) is AIOSS-chained: H_n = SHA3-256(H_{n-1} || entry_hash_n || timestamp_n).
Tamper-evident, offline-verifiable, zero cloud dependency.

## Regulatory / Compliance
GDPR Art. 25 (dashboard data local only), ISO 27001 A.12.1
