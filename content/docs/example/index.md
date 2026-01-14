---
title: "Sample"
weight: 3
---

## Sample

This section shows what Datamask takes, how it is configured, and what it produces.

---

## The scenario

Two tables, 'customer' & 'orders', linked via 'customer_id' are provided as input (sql query). 


## End-to-end
{{< tabs >}}

{{% tab "Input" %}}


### customer

| customer_id | name             | email                        | phone        |
|------------:|------------      |------------------------      |--------------|
| 101         | Alicia Reynolds  | alicia.reynolds@company.com  | +91-98123456 |
| 102         | Kevin White      | kevin.white@company.com      | +91-98234567 |

### orders

| order_id | customer_id |  amount | created_at |
| -------: | ----------: | ------: | ---------- |
|     9001 |         101 | 1200.00 | 2024-11-01 |
|     9002 |         102 |  450.00 | 2024-11-02 |

{{% /tab %}}

{{% tab "Config" %}}

```yaml
run:
  mode: query # or table

source:
  type: postgres
  url: "postgresql://prod-snapshot:5432/app"
  username: "readonly"
  # Password resolve at runtime via env / vault / secret manager.
  passwordRef: "DATAMASK_SOURCE_DB_PASSWORD"

input:
  sqlFile: "queries/customer_orders.sql"
  # sql: "SELECT ..." # optional for very small queries

  # mode: table
  # tables: ["customers", "orders"]

output:
  type: postgres
  url: "postgresql://uat-db:5432/app"
  username: "datamask"
  passwordRef: "DATAMASK_OUTPUT_DB_PASSWORD"

audit:
  enabled: true
  path: "audits/run-2024-11-15/"

tables:
  customers:
    rowPercentage: 0.5 # regenerate 50% of rows
    columns:
      customer_id:
        strategy: deterministic_token
        params:
          secret: "CUSTOMER_ID"
          prefix: "CUST_"
          length: 12

      name:
        strategy: synthetic_name

      email:
        strategy: deterministic_token
        params:
          secret: "EMAIL"
          prefix: "email_"
          length: 16
          suffix: "@example.test"

      phone:
        strategy: keep_last4

  orders:
    rowPercentage: 0.5 # generate 50% of the number of rows. 
    columns:
      order_id:
        strategy: deterministic_token
        params:
          secret: "ORDER_ID"
          prefix: "ORD_"
          length: 12

      customer_id:
        strategy: preserve # keep as-is so joins stay valid

      amount:
        strategy: preserve

      created_at:
        strategy: preserve

## for more data generation strategies, contact us. 

```

{{% /tab %}}

{{% tab "CLI" %}}

```bash
datamask run --config config/config.yaml
```

{{% /tab %}}

{{% tab "Output" %}}

### customer (masked)

| customer_id   | name      | email                                               | phone    |
| ----------:   | --------- | --------------------------------------------------- | -------- |
| CUST_K93F2Q8A | Emma Brown| [cust.k93f@example.test](mailto:cust101@example.test) | 98120000 |
| CUST_JA82KQ9M | Bob Smith | [cust.ja82@example.test](mailto:cust102@example.test) | 98230000 |

### orders (relationships unchanged)

| order_id   | customer_id |  amount | created_at |
| -------:   | ----------: | ------: | ---------- |
| ORD_82KF9  | CUST_K93F2Q8A | 1200.00 | 2024-11-01 |
| ORD_28QZ11 | CUST_JA82KQ9M |  450.00 | 2024-11-02 | 

**What to notice**

* Primary keys preserved
* Foreign keys still join correctly

{{% /tab %}}

{{% tab "Audit" %}}

```json
{
  "jobId": "run_20250106_101233",
  "executedBy": "qa-user@company.com",
  "startedAt": "2025-01-06T10:12:33Z",
  "completedAt": "2025-01-06T10:13:09Z",
  "tables": {
    "users": 2,
    "orders": 2
  }
}
```

{{% /tab %}}

{{< /tabs >}}

---

## SQL lives outside config

```sql
SELECT
  c.customer_id,
  c.name,
  c.email,
  c.phone,
  o.order_id,
  o.amount,
  o.created_at
FROM customers c
JOIN orders o
  ON c.customer_id = o.customer_id
WHERE o.created_at >= '2024-11-01';
```

---

## What this shows

From a small configuration, Datamask produces:

- a safe, production-like dataset
- preserved relationships
- and a full audit trail

This same model applies whether two or hundred tables are processed. 
