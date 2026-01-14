---
title: "Roadmap"
weight: 7
---

# Vision & Roadmap

Datamask is being built to become the **execution plane for non-production data**.

The long-term vision is simple:

> [!Important]
> **Any dataset used outside production should be safe, explainable, and reproducible, regardless of where it comes from.**

---

## The long-term vision

Over time, teams will need non-production data from many sources:

- production databases  
- staging systems  
- API contracts  
- canonical domain models  
- synthetic generators  

Datamask is designed to sit underneath all of them as the **governed execution layer** that:

- enforces scope and safety  
- preserves relationships  
- produces stable outputs  
- and records exactly what happened  

No matter how data is generated, it must still be executed safely.

---

## How Datamask evolves

Datamask grows in **capability**, not in **control**.

---

### V0: Deterministic masking core 

> [!TIP]
> Provide a deployable, reliable engine for production-derived non-production data.

This phase delivers:

- database table and SQL-query inputs  
- CSV input and output  
- deterministic tokenisation and core synthetic strategies  
- relationship-safe masking  
- schema-aware output enforcement  
- audit artifacts for every run  
- CLI and container-based execution  

This enables teams to:
- create stable QA and UAT environments  
- refresh them safely  
- and reproduce bugs with confidence  

---

### V1: Assisted configuration & enterprise safety 

> [!TIP]
> Reduce setup friction and strengthen enterprise-grade controls.

This phase adds:

- PII auto-discovery and field classification (advisory, not automatic)  
- suggested masking strategies
- auto-generated draft configurations for review  
- preview and diff modes  
- stronger audit integrity  

This makes Datamask easier to adopt while preserving its contract-driven model.

---

### V2: Contract-aware validation 

> [!TIP]
> Make Datamask aware of how data is meant to look, not just how it is stored.

This phase adds:

- support for API and schema contracts (OpenAPI, JSON Schema)  
- validation of outputs against those contracts  
- canonical shape enforcement across datasets  
- incremental refresh controls  

This allows non-production data to stay compatible with real application interfaces and expectations.

---

### V3: Synthetic and augmented data modes 

> [!TIP]
> Allow safe data generation even when production data is missing or incomplete.

This phase introduces:

- contract-driven synthetic dataset generation  
- model-based relational data synthesis  
- controlled augmentation of existing datasets  

These capabilities run through the **same deterministic execution engine** and obey the same safety and audit rules.

---

