---
title: "Datamask"
---

## What Datamask Is (and Is Not)

Datamask is a **deterministic data-transformation engine** that converts production data into **safe, production-like datasets** for non-production environments such as QA, UAT, staging, analytics, and development.

It is designed for teams that need:
- Realistic datasets for testing and validation
- Preserved relationships and data behavior
- Strong safety guarantees around sensitive information
- A clear, auditable transformation process

Datamask reads data from a trusted source (for example, a database or CSV export), applies **explicit, config-driven transformation rules**, and writes the transformed data to a safe target.  
The source data is never modified.

### What Datamask *is*
- A deterministic transformation layer for non-production data
- Relationship-aware (joins and references continue to work)
- Config-driven (no code changes to define rules)
- Streaming and scalable by design
- Designed with safety-first defaults

### What Datamask *is not*
- Not a production database replica
- Not reversible anonymization or encryption
- Not random synthetic data generation
- Not a one-off masking script or ad-hoc job

Datamask sits intentionally between raw production copies and purely synthetic data, aiming to preserve **usefulness without exposure**.

