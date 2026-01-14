---
title: "Principles"
weight: 5
---

# Principles

Datamask is built on a small set of non-negotiable principles.

These are not product features, but the rules that shape how the Datamask is designed, operated, and trusted.

---

## Configuration is the contract

Datamask does nothing implicitly.

Every run is governed by a configuration that declares:

- what data is allowed to be accessed  
- how much of it is selected  
- how each field is transformed  
- where outputs are written  
- where audit records are stored  

If something is not declared, it does not happen.

This makes every dataset:
- reviewable  
- reproducible  
- and safe to approve  

---

## Determinism over convenience

Datamask is designed so that:

> **The same input and the same configuration always produce the same output.**

This allows teams to:
- reproduce bugs  
- compare environments  
- refresh datasets without breaking tests  
- and reason about their data  

Convenience features never override this property.

---

## Explicit scope and bounded access

Datamask only reads:
- the tables  
- queries  
- or files  
that are explicitly declared in configuration.

There is no “scan everything” mode, keeping the blast radius small and makes approvals possible in regulated environments.

---

## Humans approve intent

Datamask may assist by:
- detecting likely sensitive fields  
- suggesting transformation strategies  
- generating draft configurations  

But it never executes anything without an explicit, human-approved configuration.

---

## Data never leaves your infrastructure

Datamask runs inside environments you control.

It does not:
- upload source data  
- require internet access  
- or route data through a vendor platform  

This allows Datamask to be deployed in:
- private VPCs  
- regulated environments  
- or even air-gapped networks  

---

## Audit is a first-class output

Every run produces an audit artifact that records:

- who ran the job  
- when it ran  
- which configuration was used  
- what data was touched  
- and how much was transformed  

If a dataset cannot be explained, it cannot be trusted.

---

## Fail-fast built-in

If Datamask encounters:

- a schema change  
- a missing rule  
- a constraint violation  
- or an unsafe condition  

it fails fast rather than producing broken or misleading data

---

## Built to integrate, not replace

Datamask is designed to fit into:

- Git for configuration  
- CI/CD for execution  
- existing secret managers  
- existing databases and storage  

It does not attempt to replace your data platforms, pipelines, or governance tools. It provides a reliable execution layer for non-production data.

---

