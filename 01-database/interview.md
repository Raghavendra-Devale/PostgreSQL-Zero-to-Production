
## 1️⃣ Basic / Fresher-Level Questions

### Q1. What is a database?

**Expected Answer:**

> A database is a system that stores data permanently and allows applications to read and modify data safely, even with multiple users and system failures.

---

### Q2. Why do we need databases in applications?

**Expected Answer:**

> Databases are needed to persist data, handle multiple users, enforce structure, and prevent data loss or corruption.

---

### Q3. Can we store application data in files instead of a database?

**Expected Answer:**

> Files can store data, but they do not handle concurrency, data consistency, recovery, or large-scale querying efficiently, which databases provide.

---

## 2️⃣ Intermediate-Level Questions

### Q4. What problems arise if we use files instead of a database?

**Expected Answer:**

> File-based storage can lead to data corruption, race conditions, slow searching, lack of rollback, and loss of data during crashes or partial writes.

---

### Q5. What does it mean when we say a database is a “system”?

**Expected Answer:**

> A database is a system because it actively manages data access, enforces rules, handles concurrent operations, and ensures data correctness and recovery.

---

### Q6. Where does the database fit in a full-stack application?

**Expected Answer:**

> The database sits behind the backend and stores the final validated data permanently. It acts as the single source of truth for the application.

---

## 3️⃣ Advanced / Scenario-Based Questions

### Q7. Why do backend systems trust the database more than application memory?

**Expected Answer:**

> Application memory is temporary and can be lost on restart, whereas databases provide durable, consistent, and recoverable storage.

---

### Q8. What happens if an application crashes while updating data?

**Expected Answer:**

> A database ensures that incomplete operations are rolled back or safely completed, preventing partial or corrupted data states.

---

### Q9. Why is understanding databases critical for backend developers?

**Expected Answer:**

> Because backend developers are responsible for data correctness, consistency, and reliability. Poor database usage can cause permanent data issues.

---

## 4️⃣ Trick / Conceptual Questions

### Q10. Is a database only about storing data?

**Expected Answer:**

> No. A database also manages concurrency, enforces constraints, provides recovery, and ensures correctness of data operations.

---

### Q11. Should every piece of data be stored in a database?

**Expected Answer:**

> No. Only business-critical data should be stored. Temporary or derived data can be kept in memory or cache.

---