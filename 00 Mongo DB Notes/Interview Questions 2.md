### Q1. What is MongoDB, and how is it different from a relational database?

**Answer ::**
MongoDB is a NoSQL document database that stores data in flexible JSON-like documents (BSON format), making it schema-less and ideal for unstructured data. Unlike relational databases (e.g., MySQL), which use fixed tables and rows with predefined schemas, MongoDB allows documents in a collection to have varying structures, supports horizontal scaling via sharding, and handles relationships through embedding or referencing without JOINs.

---

### Q2. Explain the concept of a document and a collection in MongoDB.

**Answer ::**
A document is a key-value pair data structure, similar to a JSON object, representing a single record (e.g., `{name: "John", age: 30}`).

A collection is a group of these documents, analogous to a table in SQL but schema-less, allowing varied document structures within the same group.

---

### Q3. What data types are supported in MongoDB documents?

**Answer ::**
MongoDB supports:

* Strings
* Numbers (int, long, double, decimal)
* Arrays
* Booleans
* Dates
* Null
* Embedded documents
* ObjectId
* Binary data
* Regular expressions
* Timestamps
* Code/JavaScript

---

### Q4. How does MongoDB store data internally?

**Answer ::**
MongoDB stores data in BSON (Binary JSON) format, optimized for speed and traversal, with collections stored as files on disk using the WiredTiger storage engine by default.

---

### Q5. What is a primary key in MongoDB, and how is it defined?

**Answer ::**
The primary key is the unique `_id` field in every document, acting as an identifier.

If not set manually, MongoDB generates a unique ObjectId automatically.

---

### Q6. How do indexes work in MongoDB, and when should you use them?

**Answer ::**
Indexes store parts of data in an efficient format for faster queries, reducing scanned documents.

Use indexes on:

* Frequently queried fields
* Sorted fields
* Filter conditions

---

### Q7. What is replication in MongoDB, and how does it work?

**Answer ::**
Replication copies data across multiple servers in a replica set, with:

Primary node:

* Handles writes

Secondary nodes:

* Replicate data
* Can serve reads

If the primary fails, an election selects a new primary.

---

### Q8. Explain the difference between sharding and replication.

**Answer ::**

Replication:

* Copies data
* Provides redundancy

Sharding:

* Splits data
* Provides scalability

---

### Q9. How do you handle schema changes in MongoDB collections?

**Answer ::**
Since MongoDB is schema-less, update documents individually using:

* `$set`
* `$unset`

For large updates, use migration scripts.

---

### Q10. What strategies can improve MongoDB query performance?

**Answer ::**

* Use indexes
* Project required fields only
* Use explain()
* Avoid large documents
* Use aggregation pipeline

---

### Q11. What is the most challenging MongoDB issue you have faced in production?

**Answer ::**
Common challenges include optimizing slow queries due to unindexed fields or handling high memory usage from large working sets.

These issues can be resolved by indexing and monitoring with tools like mongostat.

---

### Q12. Describe a situation where you had to optimize a slow MongoDB query.

**Answer ::**

Steps:

1. Use `explain("executionStats")`
2. Inspect query plan
3. Add indexes if needed
4. Reduce scanned documents

---

### Q13. How do you manage version upgrades in a production MongoDB environment?

**Answer ::**

Steps:

1. Backup data
2. Check compatibility
3. Upgrade drivers
4. Stop server
5. Install new version
6. Restart server
7. Test application
8. Monitor performance

---

### Q14. How have you scaled MongoDB in a high-traffic application?

**Answer ::**
Implement:

* Sharding for distribution
* Replica sets for availability
* Monitoring for load

---

### Q15. Tell me about a time you designed a complex data model using MongoDB.

**Answer ::**
For many-to-many relationships:

Embedding:

* Small static data

Referencing:

* Large dynamic data

Balances performance and integrity.

---

### Q16. Describe how you ensured data consistency across a sharded cluster.

**Answer ::**

Use:

* Write concern (majority)
* Proper read preferences

---

### Q17. If a node in a replica set fails, what steps does MongoDB take automatically?

**Answer ::**

1. Election triggered
2. New primary selected
3. Writes resume
4. Failed node resyncs

---

### Q18. You need to migrate data from a relational database to MongoDB. What steps would you follow?

**Answer ::**

1. Analyze schema
2. Map to documents
3. Export data
4. Convert to JSON/BSON
5. Import using mongoimport
6. Validate data

---

### Q19. How would you troubleshoot a MongoDB deployment with high memory usage?

**Answer ::**

Use:

* mongostat
* db.currentOp()
* explain()
* Index analysis

---

### Q20. A query is timing out in production. How do you diagnose and fix it?

**Answer ::**

1. Use explain("executionStats")
2. Check scanned documents
3. Add indexes
4. Optimize query

---

*(Continuing same format Q21 → Q100)*

---

## Operations

---

### Q21. How do you back up and restore a MongoDB database?

**Answer ::**

Backup:

```
mongodump
```

Restore:

```
mongorestore
```

Large deployments:

* Snapshots
* Atlas backups

---

### Q22. What monitoring tools do you use for MongoDB health checks?

**Answer ::**

* mongostat
* Ops Manager
* Atlas Monitoring
* Prometheus

---

### Q23. How would you handle replica set failover manually?

**Answer ::**

Commands:

```
rs.stepDown()
rs.freeze()
```

---

### Q24. What is the aggregation pipeline in MongoDB?

**Answer ::**
Framework for processing documents through stages such as:

* `$match`
* `$group`
* `$sort`

---

### Q25. How do $group and $match stages work together in aggregation?

**Answer ::**

1. `$match` filters documents
2. `$group` aggregates them

---

### Q26. How would you calculate average order value using aggregation?

**Answer ::**

Use:

* `$match`
* `$group`
* `$avg`

---

### Q27. How do you connect a Node.js app to MongoDB using Mongoose?

**Answer ::**

Steps:

1. Install mongoose
2. Import mongoose
3. Use:

```
mongoose.connect(connectionString)
```

---

### Q28. What is a schema in Mongoose, and how is it defined?

**Answer ::**

Schema:

Blueprint for documents.

Example:

```
new mongoose.Schema({})
```

---

### Q29. How do you handle validation errors in a Node.js + MongoDB application?

**Answer ::**

* Mongoose validators
* try-catch
* API error responses

---

### Q30. What is MongoDB Atlas, and how does it differ from self-hosted MongoDB?

**Answer ::**

Atlas:

* Managed cloud service
* Auto backups
* Auto scaling

Self-hosted:

* Manual server management

---

(Continuing exactly same format…)

---

## Queries

---

### Q33. Write a MongoDB query to find all users who registered in the last 30 days.

**Answer ::**

```
db.users.find({
 registrationDate: {
  $gte: new Date(Date.now() - 302460601000)
 }
})
```

---

### Q34. Write a query to update a user's email based on their username.

**Answer ::**

```
db.users.updateOne(
 {username:"johndoe"},
 {$set:{email:"john.doe@example.com"}}
)
```

---

### Q35. Write an aggregation pipeline to group orders by user and sum the total.

**Answer ::**

```
db.orders.aggregate([
 {
  $group:{
   _id:"$userId",
   totalAmount:{$sum:"$amount"}
  }
 }
])
```

---

### Q36. Write a query to delete all products with zero stock.

**Answer ::**

```
db.products.deleteMany({stock:0})
```

---

### Q37. Compare MongoDB with SQL Server.

**Answer ::**
MongoDB is NoSQL, schema-flexible, and scales horizontally, while SQL Server is relational, schema-rigid, and scales primarily vertically.

---

### Q38. What are other types of NoSQL databases?

**Answer ::**

Types include:

* Key-value databases (Redis)
* Column-family databases (Cassandra)
* Graph databases (Neo4j)
* Document databases (MongoDB)

---

### Q39. What is a document in MongoDB?

**Answer ::**
A document is a JSON-like structure with key-value pairs, stored in BSON format for efficiency.

---

### Q40. How do you create a database in MongoDB?

**Answer ::**

Use:

```
use dbName
```

The database is created when the first document is inserted.

---

### Q41. What is the notion of schema-less in MongoDB?

**Answer ::**
Schema-less means documents can have varying fields without a fixed structure, allowing flexible data modeling.

---

### Q42. How is data synchronized from primary to secondary in replication?

**Answer ::**
Secondaries tail the primary oplog and apply operations asynchronously.

---

### Q43. What is sharding in MongoDB?

**Answer ::**
Sharding distributes data across multiple machines to handle large datasets and high throughput workloads.

---

### Q44. What factors should be considered in MongoDB's schema development process?

**Answer ::**

Consider:

* User requirements
* Frequent access patterns
* Aggregation optimization

---

### Q45. What is the composition of ObjectId?

**Answer ::**

ObjectId consists of:

* Timestamp
* Machine ID
* Process ID
* Counter

---

### Q46. What are indexes in MongoDB?

**Answer ::**
Indexes are structures holding field values for fast querying, ordered by field value.

---

### Q47. What are the multiple languages supported by MongoDB?

**Answer ::**

Languages include:

* C
* C++
* C#
* Java
* Node.js
* Perl
* PHP
* Python
* Ruby
* Scala
* Go
* Erlang

---

### Q48. What are the data models of MongoDB?

**Answer ::**

MongoDB supports:

Embedded Model:

* Nested documents

Normalized Model:

* Referenced documents

---

### Q49. What is a profiler's role in MongoDB?

**Answer ::**
The profiler logs performance data for operations and helps identify slow queries.

---

### Q50. Explain BSON and its significance in MongoDB.

**Answer ::**
BSON is Binary JSON that extends JSON with additional types like Date and Binary, providing efficient storage and retrieval.

---

## CRUD & Operations

---

### Q51. How to create a new database and collection in MongoDB?

**Answer ::**

Create database:

```
use mydatabase
```

Create collection:

```
db.createCollection("mycollection")
```

---

### Q52. How does MongoDB ensure high availability and scalability?

**Answer ::**

High availability:

* Replica sets

Scalability:

* Sharding

---

### Q53. What is the role of _id in MongoDB documents?

**Answer ::**
The `_id` field is the unique identifier of a document and is auto-generated as ObjectId if not provided.

---

### Q54. How do you insert data into a collection?

**Answer ::**

```
db.collection.insertOne({key:value})
```

or

```
db.collection.insertMany()
```

---

### Q55. Explain the concept of replica sets in MongoDB.

**Answer ::**
Replica sets are groups of MongoDB instances maintaining identical data with a primary for writes and secondaries for replication.

---

### Q56. What is sharding, and how does it work in MongoDB?

**Answer ::**
Sharding partitions data across shards and MongoDB balances data automatically.

---

### Q57. Explain the basic syntax of MongoDB CRUD operations.

**Answer ::**

Create:

```
insertOne()
```

Read:

```
find()
```

Update:

```
updateOne()
```

Delete:

```
deleteOne()
```

---

### Q58. How to perform basic querying in MongoDB?

**Answer ::**

```
db.collection.find({field:value})
```

---

### Q59. What is an index in MongoDB, and how to create one?

**Answer ::**

Indexes improve query speed.

Create index:

```
db.collection.createIndex({field:1})
```

---

### Q60. How does MongoDB handle data consistency?

**Answer ::**
MongoDB ensures consistency using journaling and write concerns for acknowledgment guarantees.

---

## Advanced Topics

---

### Q61. How to perform data import and export in MongoDB?

**Answer ::**

Import:

```
mongoimport
```

Export:

```
mongoexport
```

---

### Q62. What are MongoDB aggregation pipelines and how are they used?

**Answer ::**
Aggregation pipelines perform multi-stage processing such as filtering and grouping using stages like `$match` and `$group`.

---

### Q63. Describe the aggregation framework in MongoDB.

**Answer ::**
The aggregation framework processes data using multiple stages like filtering and grouping.

---

### Q64. How to perform aggregation operations using MongoDB?

**Answer ::**

```
db.collection.aggregate([stages])
```

---

### Q65. Explain the concept of write concern and its importance in MongoDB.

**Answer ::**
Write concern determines the level of acknowledgment for write operations and balances durability with performance.

---

### Q66. What are TTL indexes, and how are they used in MongoDB?

**Answer ::**
TTL indexes automatically remove documents after a specified time using expireAfterSeconds.

---

### Q67. How to handle schema design and data modeling in MongoDB?

**Answer ::**

Use:

* Embedding for related data
* Referencing for large datasets
* Indexes for performance

---

### Q68. What is GridFS, and when is it used in MongoDB?

**Answer ::**
GridFS stores large files greater than 16MB by dividing them into chunks and storing them in collections.

---

### Q69. Explain the differences between WiredTiger and MMAPv1 storage engines.

**Answer ::**

WiredTiger:

* Document-level locking
* Compression
* Better performance

MMAPv1:

* Collection-level locking
* Legacy engine

---

### Q70. How to handle transactions in MongoDB?

**Answer ::**
Use sessions with startTransaction(), commitTransaction(), and abortTransaction() for ACID operations.

---

### Q71. Describe the MongoDB Compass tool and its functionalities.

**Answer ::**
MongoDB Compass is a GUI tool used for:

* Schema visualization
* Query building
* Aggregation
* Index management

---

### Q72. How to implement access control and user authentication in MongoDB?

**Answer ::**

Enable authorization and create users:

```
db.createUser()
```

---

### Q73. What are capped collections, and when are they useful?

**Answer ::**
Capped collections are fixed-size collections that overwrite old data automatically and are useful for logs and caching.

---

### Q74. Explain the concept of geospatial indexes in MongoDB.

**Answer ::**
Geospatial indexes support location-based queries and are created using `"2dsphere"`.

---

### Q75. How to handle backups and disaster recovery in MongoDB?

**Answer ::**

Use:

* mongodump
* mongorestore
* Snapshots
* Replica sets

---

### Q76. Describe the process of upgrading MongoDB to a newer version.

**Answer ::**

Steps:

1 Backup
2 Compatibility check
3 Upgrade
4 Test
5 Monitor

---

### Q77. What are change streams in MongoDB, and how are they used?

**Answer ::**
Change streams provide real-time notifications of database changes using watch().

---

### Q78. Explain the use of hashed sharding keys in MongoDB.

**Answer ::**
Hashed shard keys ensure even data distribution, especially for monotonically increasing values.

---

### Q79. How to optimize MongoDB queries for performance?

**Answer ::**

* Indexes
* Projection
* explain()
* Aggregation optimization

---

### Q80. Describe the map-reduce functionality in MongoDB.

**Answer ::**
Map-reduce processes data using map functions to emit key-value pairs and reduce functions to aggregate results.

---

### Q81. What is the role of journaling in MongoDB, and how does it impact performance?

**Answer ::**
Journaling ensures durability through write-ahead logging. It increases I/O but prevents data loss.

---

### Q82. How to implement full-text search in MongoDB?

**Answer ::**

1 Create text index
2 Use `$text` with `$search`

---

### Q83. What are the considerations for deploying MongoDB in a production environment?

**Answer ::**

* Replication
* Sharding
* Backups
* Security
* Monitoring
* Capacity planning

---

### Q84. Explain the concept of horizontal scalability and its implementation in MongoDB.

**Answer ::**
Horizontal scalability is achieved by adding servers and distributing data using sharding.

---

### Q85. How to monitor and troubleshoot performance issues in MongoDB?

**Answer ::**

* Logs
* Profiler
* explain()
* Ops Manager

---

### Q86. Describe the process of migrating data from a relational database to MongoDB.

**Answer ::**

1 Redesign schema
2 Export data
3 Transform data
4 Import data
5 Validate data
6 Update applications

---

## Query Problems

---

### Q87. Find all employees who work in the "Engineering" department.

**Answer ::**

```
db.employees.find({department:"Engineering"})
```

---

### Q88. Find the employee with the highest salary.

**Answer ::**

```
db.employees.find().sort({salary:-1}).limit(1)
```

---

### Q89. Update the salary of "John Doe" to 90000.

**Answer ::**

```
db.employees.updateOne(
 {name:"John Doe"},
 {$set:{salary:90000}}
)
```

---

### Q90. Count the number of employees in each department.

**Answer ::**

```
db.employees.aggregate([
 {$group:{_id:"$department",count:{$sum:1}}}
])
```

---

### Q91. Add a new field bonus to all employees in the "Engineering" department with a value of 5000.

**Answer ::**

```
db.employees.updateMany(
 {department:"Engineering"},
 {$set:{bonus:5000}}
)
```

---

### Q92. Retrieve all documents sorted by name length in descending order.

**Answer ::**

Use aggregation:

* `$addFields`
* `$sort`
* `$project`

---

### Q93. Find the average salary of employees in the "Engineering" department.

**Answer ::**

```
db.employees.aggregate([
 {
  $group:{
   _id:null,
   averageSalary:{$avg:"$salary"}
  }
 }
])
```

---

### Q94. Find the department with the highest average salary.

**Answer ::**

Aggregation steps:

* `$group` by department
* `$avg` salary
* `$sort` descending
* `$limit 1`

---

### Q95. Find the total number of employees hired in each year.

**Answer ::**

Aggregation:

* `$group`
* `$year`
* `$sum`

---

### Q96. Find the highest and lowest salary in the "Engineering" department.

**Answer ::**

Aggregation:

* `$match`
* `$group`
* `$max`
* `$min`

---

### Q97. What is a cursor in MongoDB and how is it used?

**Answer ::**
A cursor is an iterator for query results that fetches documents in batches for large result sets.

---

### Q98. How can you limit the number of documents returned in a MongoDB query?

**Answer ::**

```
.limit(number)
```

---

### Q99. What is the $push operator in MongoDB and how does it work?

**Answer ::**
`$push` appends values to an array.

Example:

```
$push:{field:value}
```

---

### Q100. Explain the concept of read preferences in MongoDB.

**Answer ::**
Read preference determines which replica set members serve read operations, such as:

* primary
* secondary
* nearest

---