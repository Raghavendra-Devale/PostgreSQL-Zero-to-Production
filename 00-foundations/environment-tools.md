# PostgreSQL Environment & Tools

> Learning notes through checkpoint **01.21**.  
> Practice environment: PostgreSQL 18.3 on Windows.  
> Real-world database used for exploration: Botiq.

---

## 01.1 — PostgreSQL Environment Verification

Verified:

- PostgreSQL client/server version: **18.3**
- `psql --version` → PostgreSQL 18.3
- `pg_config --version` → PostgreSQL 18.3
- PostgreSQL 18 Windows service: **Running**
- PostgreSQL 14 Windows service: **Stopped**
- Host: `localhost`
- Port: `5432`
- `psql -U postgres` connection: successful
- Server: 64-bit Windows build

### Client vs Server

- **PostgreSQL server** is the running database service.
- **psql** is the command-line client.
- A connection uses host, port, database, role, and authentication.

---

## 01.2 — PostgreSQL Mental Model

```text
PostgreSQL Server
├── Database
│   └── Schema
│       ├── Table
│       ├── View
│       ├── Function
│       └── Sequence
└── ...
```

Roles are identities with role attributes and object privileges.

A connection joins the client, role, and selected database.

---

## 01.13 — Database vs Schema

### Database

A logical container inside a PostgreSQL server.

Example:

```text
PostgreSQL Server
├── botiq
├── nextrole
├── job_platform
└── economy_service
```

### Schema

A namespace/container for database objects inside a database.

Example:

```text
botiq
└── public
    ├── customers
    ├── orders
    └── payments
```

### Mental model

**Database → Schema → Table**

For database `botiq`, schema `public`, table `orders`:

- Database = `botiq`
- Schema = `public`
- Table = `orders`
- Schema-qualified table name = `public.orders`

---

## 01.14 — Roles, Users & Permissions

A PostgreSQL **role** represents an identity used for authentication and authorization.

### Authentication vs Authorization

- Authentication → **Who are you?**
- Authorization → **What are you allowed to do?**

### Roles observed

```text
postgres
botiq_mcp_readonly
```

`postgres` is a superuser with powerful administrative attributes.

`botiq_mcp_readonly` can log in and is not a superuser.

### Role attributes vs object privileges

```text
Role attributes
        !=
Object privileges
```

A role can have `LOGIN` while still having restricted table privileges.

### Privilege layers

```text
Database
  └── CONNECT
       ↓
Schema
  ├── USAGE
  └── CREATE
       ↓
Table
  ├── SELECT
  ├── INSERT
  ├── UPDATE
  └── DELETE
```

### GRANT / REVOKE

```sql
GRANT SELECT ON TABLE public.orders TO app_reader;
REVOKE SELECT ON TABLE public.orders FROM app_reader;
```

Important Botiq finding:

`botiq_mcp_readonly` had database `CONNECT`, schema `USAGE`, and schema `CREATE` permissions in the inspected environment. Therefore the role name alone does not prove that the role is globally read-only.

---

## 01.15 — Connections & Sessions

A PostgreSQL connection is the communication channel between a client and the PostgreSQL server.

Observed session:

```text
Database     → postgres
Role         → postgres
Server       → ::1
Port         → 5432
Backend PID  → session-specific PID
```

`::1` is the IPv6 loopback address used for a local connection.

Useful session inspection:

```sql
SELECT
    current_database(),
    current_user,
    inet_server_addr(),
    inet_server_port(),
    pg_backend_pid();
```

Useful monitoring view:

```sql
SELECT
    pid,
    usename,
    datname,
    client_addr,
    state
FROM pg_stat_activity
WHERE datname IS NOT NULL;
```

---

## 01.16 — psql Basics

### Important commands

| Command | Purpose |
|---|---|
| `\l` | List databases |
| `\c database` | Connect/switch database |
| `\conninfo` | Show current connection |
| `\dn` | List schemas |
| `\dt` | List tables |
| `\du` | List roles |
| `\d table` | Describe an object |
| `\d+ table` | Detailed object description |
| `\df` | List functions |
| `\?` | psql command help |
| `\h SELECT` | SQL command help |
| `\q` | Quit psql |

### Prompt states

```text
postgres=#  → ready for a new command
postgres-#  → unfinished input
```

Use `Ctrl+C` to cancel unfinished input.

Use `\q` to leave `psql`.

### `\d` vs `\d+`

`\d table` shows table structure, columns, types, defaults, indexes, and constraints.

`\d+ table` adds more storage/details such as access method and storage information.

---

## 01.17 — Botiq Database Exploration

Connected using:

```text
\c botiq
```

Verified:

- Database: `botiq`
- Host: `localhost`
- Port: `5432`
- Role: `postgres`
- Schema: `public`

The inspected Botiq schema contained **44 tables**.

Examples:

- `botiq_customer`
- `botiq_order`
- `botiq_order_item_w`
- `botiq_partner`
- `botiq_payments`
- `users`
- `organization`

### Safe exploration rule

Botiq is for real-world investigation. Destructive experiments belong in a separate PostgreSQL lab database.

### Table metadata observed

#### `botiq_customer`

Primary key:

```sql
PRIMARY KEY (org_id, customer_id)
```

Important columns:

- `customer_id`
- `org_id`
- `customer_name`
- `contact_number`
- `enabled`
- `deleted`
- `created_date`
- `updated_date`

#### `botiq_order`

Primary key:

```sql
PRIMARY KEY (org_id, order_id)
```

Important columns:

- `order_id`
- `org_id`
- `customer_id`
- `order_status`
- `payment_status`
- `order_amount`
- `advance_amount`
- `due_amount`
- `order_date`
- `due_date`

#### `botiq_payments`

Primary key:

```sql
PRIMARY KEY (payment_id)
```

Important columns:

- `payment_id`
- `org_id`
- `user_id`
- Razorpay identifiers
- `amount_in_paise`
- `status`
- `created_at`
- `verified_at`

### Foreign-key verification

The Botiq `public` schema was checked for declared foreign keys and returned **0 rows**.

Therefore:

- Similar column names do not prove a foreign key.
- The apparent customer/order relationship is not enforced by a declared FK in the inspected schema.
- Relationships must be verified through actual constraints, not assumptions.

---

## 01.18 — Safe Data Inspection

Basic exploratory query:

```sql
SELECT *
FROM public.botiq_customer
LIMIT 10;
```

More targeted:

```sql
SELECT
    customer_id,
    org_id,
    customer_name,
    contact_number
FROM public.botiq_customer
ORDER BY customer_id
LIMIT 10;
```

### Composite-key observation

The data showed that `customer_id` is not globally unique:

```text
(7,  1)  → Mk
(36, 1)  → Darshan
(6,  1)  → Suraj
(1,  1)  → Mohan JN
```

Therefore the combination:

```text
(org_id, customer_id)
```

is needed to identify the customer row.

Orders showed the same pattern with:

```text
(org_id, order_id)
```

### NULL

A blank value displayed by psql can represent SQL `NULL`.

```text
NULL → absent/unknown value
0    → actual numeric zero
```

---

## 01.19 — NULL, WHERE, and Basic Predicates

Basic filtering:

```sql
SELECT ...
FROM ...
WHERE condition;
```

Examples:

```sql
WHERE org_id = 7
WHERE org_id = 7 AND enabled = true
WHERE org_id = 7 OR org_id = 36
WHERE order_amount IS NULL
WHERE order_amount IS NOT NULL
WHERE order_status = 'Pending'
```

### NULL rule

Do not use:

```sql
WHERE column = NULL
WHERE column <> NULL
```

Use:

```sql
WHERE column IS NULL
WHERE column IS NOT NULL
```

---

## 01.20 — Comparison Operators & Ranges

Operators practiced:

| Operator | Meaning |
|---|---|
| `=` | Equal |
| `<>` | Not equal |
| `>` | Greater than |
| `<` | Less than |
| `>=` | Greater than or equal |
| `<=` | Less than or equal |
| `BETWEEN` | Inclusive range |
| `IN` | Match one of several values |

Examples:

```sql
WHERE order_amount > 1000
WHERE order_amount BETWEEN 500 AND 1000
WHERE org_id IN (1, 6, 7)
WHERE order_status <> 'Pending'
```

`BETWEEN` includes both endpoints.

Key lesson:

> Choosing the correct operator is not enough; apply it to the correct column.

---

## 01.21 — AND, OR, and Parentheses

### AND

Both conditions must be true.

```sql
WHERE order_status = 'Pending'
  AND order_amount > 1000
```

### OR

At least one condition must be true.

```sql
WHERE order_status = 'Pending'
   OR order_status = 'Started'
```

### Parentheses

When mixing `AND` and `OR`, use parentheses to make the intended logic explicit.

```sql
WHERE (org_id = 2 OR org_id = 7)
  AND order_status = 'Pending'
```

### IN as a cleaner OR

```sql
WHERE org_id IN (2, 7, 36)
```

instead of:

```sql
WHERE org_id = 2
   OR org_id = 7
   OR org_id = 36
```

### Example reasoning

```sql
WHERE (org_id = 2 OR org_id = 7)
  AND order_amount > 1000
  AND order_status <> 'Delivered'
```

Meaning:

> Orders from org 2 or 7, with amount greater than 1000, whose status is NOT Delivered.

---

# Progress

## Practiced

- [x] PostgreSQL 18.3 environment verification
- [x] psql basics
- [x] Roles/users and permissions
- [x] Database vs schema
- [x] Connections and sessions
- [x] Botiq schema exploration
- [x] Composite-key reasoning
- [x] SELECT
- [x] WHERE
- [x] LIMIT
- [x] NULL
- [x] Comparison operators
- [x] BETWEEN
- [x] IN
- [x] AND / OR / parentheses

## Pending

- [ ] pgAdmin
- [ ] PostgreSQL configuration basics
- [ ] Dump/restore
- [ ] Safe Botiq learning DB restore/verification
- [ ] Separate PostgreSQL lab database
- [ ] Environment mastery test

## Next

**01.22 — ORDER BY, sorting, and controlling result order**
