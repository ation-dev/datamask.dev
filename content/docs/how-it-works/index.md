---
title: "How it Works"
weight: 2
---

## How it Works

Datamask is built around a simple idea:

> [!INFO]
> **Humans declare intent. Datamask executes it deterministically.**

Everything else, automation, scale, and safety, is layered on top of that.

---

## High-level flow

Every Datamask run follows the same pipeline, regardless of whether it is run manually or in a CI job:

> [!TIP]
> Input -> Config -> Execution Engine -> Output -> Audit

Each stage has a clear boundary and responsibility.

---

### 1. Inputs

Inputs are always declared in configuration and can include:

- database tables  
- SQL query results  
- CSV files  

Future versions will also support contract and model-based inputs, but the execution model remains the same.

Datamask reads only what is explicitly declared and nothing else.

---

### 2. Configuration as the contract

A Datamask configuration defines:

- what data is allowed to be used  
- how much of it is selected  
- how each field is transformed    
- where the output is written  
- where audit records are stored  

The configuration is versioned, reviewed, and promoted through environments just like application code.

---

### 3. Deterministic execution

When a run starts, Datamask:

1. connects to the declared input source  
2. reads only the scoped data  
3. applies the configured transformation strategies  
4. preserves declared identities and relationships  
5. writes the result to the configured output  

If the same input and the same configuration are used again, the output will be identical. This makes non-production data predictable, reproducible, and debuggable.

---

### 4. Outputs

Datamask can write transformed data to:

- QA, UAT, or staging databases  
- SQL dump files  
- CSV files  

Datamask does not manage environments or retain datasets. It writes to destinations you control.

---

### 5. Audit as a first-class output

Every run produces an audit artifact alongside the data that captures -

- who ran the job  
- when it ran  
- which configuration was used  
- which input schema was processed  
- what scope was touched  
- how many rows were transformed  

The audit can be stored in an append-only or tamper-evident destination and never contains original sensitive values.

---

## Manual and automated runs

Datamask supports two equally important ways of working.

### Manual (human-in-the-loop)

Engineers can run Datamask locally or in a controlled environment to:

- explore data  
- refine configuration  
- preview results  
- validate masking and relationships  


### Automated (pipeline)

Once a configuration is approved, the same Datamask engine can be run in:

- CI pipelines  
- scheduled jobs  
- environment refresh workflows  

The behaviour does not change, only the trigger does.

---

## What makes this different

Datamask does not own your data, your environments, or your workflows.

It provides a **deterministic execution layer** that fits into the systems you already use:

- Git for configuration  
- CI/CD for execution  
- your infrastructure for data  
- your storage for audit  

That is what makes Datamask safe to adopt, easy to automate, and hard to replace.

