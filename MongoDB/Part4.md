# 📌 MongoDB Aggregation Framework

- **Purpose:** Used for **data aggregation** (calculations, transformations, summaries).  
- Acts as the **NoSQL alternative** to SQL’s `GROUP BY` and other aggregate queries.  

---

## 🔹 Key Concepts

- Aggregation is performed using the **`aggregate()`** method on a collection.  
- Uses **pipeline stages**: documents flow through stages **one by one**.  
- Commonly used for:
  - **Filtering** (`$match`)  
  - **Grouping** (`$group`)  
  - **Projecting** (`$project`)  
  - **Sorting** (`$sort`)  
  - **Joining** (`$lookup`)  


## 🔹 Important Stages
- 1. $match (like WHERE)

### Filters documents based on a condition.

#### Example:
```bash 
db.orders.aggregate([
  { $match: { status: "completed" } }
])


SQL Equivalent:

SELECT * FROM orders WHERE status = 'completed';
```

## 2. $group (like GROUP BY)

- Groups documents by a field and allows aggregate calculations.

#### Example: Total amount per customer
```bash
db.orders.aggregate([
  { $group: { _id: "$customerId", totalAmount: { $sum: "$amount" } } }
])


SQL Equivalent:

SELECT customerId, SUM(amount) as totalAmount
FROM orders
GROUP BY customerId;
```

## 3. $project (like SELECT columns)

- Selects specific fields or reshapes documents.

#### Example:
```bash 
db.orders.aggregate([
  { $project: { _id: 0, customerId: 1, amount: 1 } }
])


SQL Equivalent:

SELECT customerId, amount FROM orders;
```

## 4. $sort, $limit, $skip
```bash
$sort: Sort documents by fields.

{ $sort: { amount: -1 } } // Descending


$limit: Limit number of documents.

{ $limit: 5 }


$skip: Skip N documents.

{ $skip: 10 }


SQL Equivalent:

SELECT * FROM orders ORDER BY amount DESC LIMIT 5 OFFSET 10;
```

## 5. $lookup (like SQL JOIN)

- Performs left outer join with another collection.

#### Example: Join orders with customers
```bash
db.orders.aggregate([
  {
    $lookup: {
      from: "customers",
      localField: "customerId",
      foreignField: "_id",
      as: "customerDetails"
    }
  }
])


SQL Equivalent:

SELECT o.*, c.*
FROM orders o
LEFT JOIN customers c ON o.customerId = c.id;```

# ✅ MongoDB Aggregation Framework: Summary Table

| **Stage**   | **MongoDB Syntax**                                           | **SQL Equivalent** | **Purpose**                     |
|------------|--------------------------------------------------------------|------------------|--------------------------------|
| `$match`   | `{ $match: { field: value } }`                               | `WHERE`          | Filter documents               |
| `$group`   | `{ $group: { _id: "$field", total: { $sum: "$amount" } } }` | `GROUP BY`       | Aggregate calculations         |
| `$project` | `{ $project: { field1: 1, field2: 1 } }`                    | `SELECT columns` | Select/reshape fields          |
| `$sort`    | `{ $sort: { field: 1/-1 } }`                                 | `ORDER BY`       | Sort documents                 |
| `$limit`   | `{ $limit: N }`                                              | `LIMIT N`        | Limit results                  |
| `$skip`    | `{ $skip: N }`                                               | `OFFSET N`       | Skip results                   |
| `$lookup`  | `$lookup`                                                    | `JOIN`           | Join collections               |
```
## 👉 Interview Tip:

- They may ask: “How do you perform JOINs in MongoDB?” → Use $lookup.

- Or: “How to calculate total sales per customer?” → Use $group with $sum.