
## Topic 0: What is Data?

### 1. What is Data (Beginner Explanation)

Data is **raw facts or values** that describe something in the real world.

Examples:

* A person’s name
* A user’s age
* A product price
* A transaction amount
* A timestamp

By itself, data does not explain anything.
It only **represents reality**.

---

### 2. Data vs Information

* **Data** → raw, unprocessed facts
* **Information** → meaning derived from data

Example:

* Data: `5000, 2 Jan 2026, SUCCESS`
* Information: “A payment of ₹5000 was successful on 2 Jan 2026”

Databases primarily store **data**.
Business logic converts data into **information**.

---

### 3. Why Data Must Be Persisted

Data stored in:

* Variables
* Objects
* Memory is **temporary**.
When:

* Application restarts
* Server crashes
* Deployment happens

➡️ All in-memory data is lost.

Real applications cannot afford this.

Therefore, data must be **persisted** (stored permanently).

---

### 4. Persistence (Key Concept)

**Persistence** means:

> Data survives program restarts, crashes, and deployments.

Persistent data is stored in:

* Databases
* Disk-based storage

This is mandatory for:

* Users
* Orders
* Payments
* Logs
* Audit history

---

### 5. Full-Stack Developer Perspective

In a full-stack system:

* Frontend → collects data
* Backend → validates and processes data
* Database → stores data permanently

The database acts as the **single source of truth**.

Code can change.
Servers can be replaced.
**Data must remain correct for years.**

---

### 6. Why Variables Are Not Enough

Variables fail because:

* They exist only in memory
* They disappear on restart
* They cannot handle multiple users safely
* They cannot scale for large data

This limitation is what led to the invention of **databases**.

---

### 7. Real-World Example

If a banking application stores balances only in variables:

* Restart → all balances lost
* System becomes unusable

Therefore:

* Balances are stored as data
* Data is persisted in a database
* Backend reads and updates this data safely

---

### 8. Senior-Level Insight

Experienced engineers treat:

* **Data as more important than code**

Because:

* Code bugs can be fixed
* Lost or corrupted data is often irreversible

This mindset drives careful database design.

---

### 9. When NOT to Persist Data

Not all data needs persistence:

* Temporary UI state
* Cache values
* Derived values that can be recalculated

Persistent storage is reserved for **business-critical data**.

---