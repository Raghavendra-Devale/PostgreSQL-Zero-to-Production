
## 1️⃣ Basic / Fresher-Level Questions

### Q1. What is data?

**Expected Answer:**

> Data is raw facts or values that represent real-world entities, such as names, numbers, dates, or identifiers, which by themselves do not carry meaning until processed.

---

### Q2. Give examples of data in a backend application.

**Expected Answer:**

> User details, product prices, order IDs, timestamps, payment amounts, and status flags are examples of data in backend applications.

---

### Q3. Is data the same as information?

**Expected Answer:**

> No. Data is raw facts, while information is meaningful insight derived after processing data.

---

## 2️⃣ Intermediate-Level Questions

### Q4. Why can’t backend applications rely only on variables to store data?

**Expected Answer:**

> Variables store data in memory, which is temporary. When the application restarts or crashes, all variable data is lost. Backend applications need persistent storage to retain data long-term.

---

### Q5. What does data persistence mean?

**Expected Answer:**

> Data persistence means storing data in a way that it survives application restarts, crashes, and deployments, usually by storing it on disk using databases.

---

### Q6. Where does data live in a full-stack application?

**Expected Answer:**

> Data is collected by the frontend, processed and validated by the backend, and permanently stored in the database, which acts as the single source of truth.

---

## 3️⃣ Advanced / Senior-Level Questions

### Q7. Why do senior engineers say “data is more important than code”?

**Expected Answer:**

> Code can be rewritten or redeployed, but data often represents real-world history and business transactions. Losing or corrupting data can be irreversible, so data integrity is critical.

---

### Q8. What kind of data should NOT be persisted?

**Expected Answer:**

> Temporary or derived data such as UI state, cache values, session data, or values that can be recalculated should not be persisted permanently.

---

### Q9. What problems arise if data is not persisted properly?

**Expected Answer:**

> Data loss, inconsistent state, inability to recover after crashes, incorrect business operations, and loss of user trust.

---

## 4️⃣ Trick / Conceptual Questions (Interview Traps)

### Q10. If data is important, why not store everything permanently?

**Expected Answer:**

> Persisting everything increases storage cost, complexity, and maintenance overhead. Only business-critical data should be persisted; temporary or derived data should be handled differently.

---

### Q11. Is caching the same as persisting data?

**Expected Answer:**

> No. Caching is temporary and optimized for speed, while persistence ensures durability and long-term storage.