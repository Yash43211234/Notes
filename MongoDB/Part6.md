# 📌 MongoDB Transactions

- **Definition:** Transactions allow multiple operations on one or more documents/collections to be executed **atomically**—all succeed or all fail.  
- **Support:** MongoDB supports **multi-document transactions** starting from **v4.0**, making it closer to SQL databases in terms of **ACID compliance**.  

---

## 🔹 1. SQL Transactions (ACID)

| **Property**   | **Description**                                               |
|----------------|---------------------------------------------------------------|
| Atomicity      | All operations in a transaction succeed or fail together     |
| Consistency    | Database remains in a valid state after transaction          |
| Isolation      | Transactions do not interfere with each other               |
| Durability     | Changes persist even after a crash                            |


### BEGIN TRANSACTION;

```bash
UPDATE Accounts SET balance = balance - 100 WHERE id = 1;
UPDATE Accounts SET balance = balance + 100 WHERE id = 2;

COMMIT; -- or ROLLBACK in case of error
```
## 🔹 2. MongoDB Transactions (Multi-Document)

- **Note:** Single-document operations are **atomic by default** in MongoDB.  
- Multi-document operations require **transactions** to ensure atomicity across multiple collections or documents.  

### Example (JavaScript / Node.js)
```javascript
const session = client.startSession();

try {
  session.startTransaction();

  db.accounts.updateOne({ _id: 1 }, { $inc: { balance: -100 } }, { session });
  db.accounts.updateOne({ _id: 2 }, { $inc: { balance: 100 } }, { session });

  session.commitTransaction();
} catch (error) {
  session.abortTransaction();
} finally {
  session.endSession();
}

## 🔹 3. Comparison with SQL Transactions

| **Feature**   | **SQL**                                       | **MongoDB**                                         |
|---------------|-----------------------------------------------|----------------------------------------------------|
| Atomicity     | Multi-row transactions by default            | Multi-document transactions supported from v4.0  |
| Isolation     | Serializable / Repeatable Read / Read Committed | Snapshot isolation (default)                      |
| Consistency   | Strong ACID                                  | ACID across multiple documents within a replica set |
| Durability    | Persistent after commit                      | Persistent after commit if write concern is satisfied |
| Use Case      | Banking, ERP, financial apps                 | Banking, multi-step updates across collections   |

---

## 🔹 4. Important Notes

- **Transactions are costly** → affect performance. Use only when needed.  
- Prefer **atomic single-document operations** for better performance.  
- Works across **replica sets** and **sharded clusters** (MongoDB 4.2+ supports sharded cluster transactions).  

### ✅ Interview Tips
- **Are MongoDB operations atomic?**  
  Single-document operations are **atomic by default**; multi-document operations require **transactions**.

