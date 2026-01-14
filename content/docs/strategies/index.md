---
title: "Strategies"
weight: 4
---

# Strategies

Datamask transforms data through **strategies**.

> [!INFO]
> A strategy is a deterministic rule that defines how a field is converted from its original value into a safe replacement.

Each column in a dataset is mapped to exactly one strategy in the configuration. 

---

## Identity strategies

> These strategies protect fields that represent real people, accounts, or objects while preserving joinability across tables.

### Deterministic token

```yaml
user_id:
  strategy: tokenise
  prefix: "USR_"
```

| Input | Output         |
| ----- | -------------- |
| 101   | USR_A93F18B21 |


---

## Name fields

For human-readable fields, Datamask provides deterministic synthetic identities.

Examples include:

- synthetic names
- initials-only variants

```yaml
name:
  strategy: synthetic_name
```

| Input      | Output  |
| ---------- | ------- |
| Neha Gupta | Ashi Mehta |

**Use when:**

* Names
* Addresses
* User-facing text fields

---

## Email & contact information

Email and contact fields are handled with format-aware strategies.

Examples include:

- deterministic synthetic emails
- masking only the local part while keeping domains
- partial masking for display and testing


```yaml
email:
  strategy: deterministic_email
  params:
    domain: "masked.local"
```


| Input                                       | Output                                                  |
| ------------------------------------------- | ------------------------------------------------------- |
| [neha@example.com](mailto:neha@example.com) | [user_1092@masked.local](mailto:user_1092@masked.local) |

**Use when:**

* Login flows
* User tables
* Systems expecting valid email formats

---

## Phone, card & payment identifiers

Datamask includes strategies specifically for sensitive financial and contact fields:

- keep-last-4 masking
- format-preserving tokens
- Luhn-valid synthetic card numbers

```yaml
phone:
  strategy: mask_keep_last4
card_number:
  strategy: synthetic_card_luhn
  params:
    test_bins: ["411111", "555555"]
```

| Input               | Output              |
| ------------------- | ------------------- |
| 9876543210          | ******3210          |
| 4111 2345 6789 9999 | 4111 1111 2222 3339 |

**Use when:**

* Phone numbers
* Card numbers (display-only)
* Identifiers where suffix is meaningful

---

## Government & regulated IDs

V0 includes format-preserving, deterministic strategies for India-specific identifiers such as:

- PAN
- Aadhaar

These strategies generate values that:

- look valid
- do not collide with real data
- remain stable across runs

```yaml
aadhaar:
  strategy: aadhaar_token
  params:
    format: "9999 9999 9999"
    ensure_no_source_collision: true
```

| Input          | Output         |
| -------------- | -------------- |
| 1234 5678 9012 | 7812 9034 1123 |

---

## Date & time transformations

Time-based fields can be shifted in deterministic or controlled ways:

- fixed offsets
- bounded random shifts
- user-relative timeline shifts


```yaml
created_at:
  strategy: shift_date_user_relative
  params:
    key_column: user_id
    min_days: -10
    max_days: 10
```

**Behaviour:**

* All dates for a given user are shifted consistently
* Different users receive different shifts

**Use when:**

* Activity timelines
* Session histories
* Event streams

---

## Address & location fields

Location data can be safely transformed using:

- synthetic structured addresses
- city or region shuffling

This keeps geographical patterns plausible without revealing real locations.

---

## Structural & pass-through strategies

To make non-sensitive fields explicit and safe by design.


```yaml
amount:
  strategy: preserve

notes:
  strategy: nullify

country_code:
  strategy: static_value
  value: "IN"
```

**Use when:**

* Fields are non-sensitive
* Downstream systems expect fixed values
* Explicitness matters more than masking

---

> [!IMPORTANT]
>This is **not** a comprehensive list of supported strategies. Datamask is still in **development phase**.


