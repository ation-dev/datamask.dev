---
title: "Datamask"
weight: 1
---

## Overview

**Datamask is a deterministic execution plane for non-production data. It exists to solve a problem every engineering team eventually hits:**

> [!IMPORTANT]
> *We need production-like data in QA, UAT, and staging without exposing real production data.*


---

## What Datamask *does*

Datamask takes declared inputs, such as databases/tables, SQL queries, or files, and transforms them into safe, stable, production-like datasets for non-production environments.
It does this through an explicit, reviewable configuration contract that defines:

- what data is allowed to be used
- how each field is transformed
- where outputs are written
- where audit records are stored  

Every run produces:

- a transformed dataset
- and a verifiable audit artifact describing exactly what happened

> [!INFO]
> The same input and the same configuration will always produce the same output.

---

## What Datamask *is not*

Datamask is not a UI-first data platform. It is not an autonomous AI system. It does not own your data or move it into a vendor-managed environment.
Datamask runs inside your infrastructure and executes exactly what you declare, and can be executed manually via CLI or a CI job. 

---

## Determinism - as a core 

Most data masking and synthetic data tools optimise for realism and convenience. That is useful, until your test data changes and your tests start failing for no reason.

Datamask optimises for repeatability, meaning - 

- bugs can be reproduced on the same dataset weeks later
- regression tests don’t flake with unpredicted data
- QA and developers see the same data for the same datamask config
- investigations are explainable

When production data changes, you can refresh your non-production datasets without losing stability.

This makes Datamask suitable for:

- regulated systems
- financial workflows
- migration projects
- long-running test environments

where unpredictability is not acceptable.

---

## Who Datamask is for

- backend and platform engineering teams
- QA and UAT environments
- data-heavy or regulated systems
- companies with strict security and audit requirements

