## Basics

---

### Q1. What is MongoDB?

**Answer ::**
MongoDB is a document database that stores data as BSON documents and is designed for developer productivity and horizontal scaling.

---

### Q2. What is a document in MongoDB?

**Answer ::**
A document is the fundamental data unit represented as a BSON object, analogous to a JSON object with richer types.

---

### Q3. What is a collection?

**Answer ::**
A collection is a grouping of MongoDB documents similar to a table, but without a fixed schema enforced by the database.

---

### Q4. What is BSON and how does it differ from JSON?

**Answer ::**
BSON is a binary representation of JSON-like documents that supports additional data types like dates and ObjectIds for efficient storage and traversal.

---

### Q5. What is an ObjectId?

**Answer ::**
ObjectId is a 12-byte unique identifier used by default for the `_id` field, providing uniqueness and efficient indexing.

---

### Q6. What is mongod vs mongos?

**Answer ::**
mongod is the core database server process, while mongos is the query router used to route operations in sharded clusters.

---

### Q7. What is a namespace in MongoDB?

**Answer ::**
A namespace is the fully qualified name of a collection or index combining database and collection names.

Example:

```
ecommerce.products
```

---

### Q8. What is MongoDB Atlas?

**Answer ::**
MongoDB Atlas is a fully managed multi-cloud database service for deploying, running, and scaling MongoDB.

---

### Q9. What are the main MongoDB capabilities developers start with?

**Answer ::**
Core capabilities include:

* Data modeling
* CRUD
* Aggregations
* Indexing
* Sharding
* Replication
* Official drivers and tools

---

### Q10. Where is the authoritative MongoDB manual?

**Answer ::**
The current stable MongoDB manual is hosted on the MongoDB documentation website and documents versions including 7.0 and above.

---

## CRUD

---

### Q11. What is CRUD in MongoDB?

**Answer ::**
CRUD refers to:

* Create
* Read
* Update
* Delete

operations provided by MongoDB.

---

### Q12. How do find and findOne differ?

**Answer ::**

find():

* Returns multiple matching documents.

findOne():

* Returns a single matching document or null.

---

### Q13. What is an upsert?

**Answer ::**
An upsert is an update operation that inserts a new document if no existing document matches the filter.

---

### Q14. What is projection in queries?

**Answer ::**
Projection specifies which fields to include or exclude in query results to optimize network and processing overhead.

---

### Q15. How do deleteOne and deleteMany differ?

**Answer ::**

deleteOne():

* Removes one document.

deleteMany():

* Removes all matching documents.

---

### Q16. What are common query operators?

**Answer ::**

Comparison operators:

* $gt
* $gte
* $lt
* $lte
* $in

Logical operators:

* $and
* $or
* $not

Element operators:

* $exists
* $type

---

### Q17. What is write concern?

**Answer ::**
Write concern specifies the level of acknowledgment requested from MongoDB for write operations, affecting durability across replica sets.

---

### Q18. What is read preference?

**Answer ::**
Read preference determines which replica set members are eligible to receive read operations such as primary or secondaries.

---

### Q19. What are bulk operations?

**Answer ::**
Bulk operations allow batching multiple insert, update, and delete operations to improve throughput and reduce round trips.

---

### Q20. What does explain do?

**Answer ::**
explain reveals query execution plans and index usage to help diagnose and optimize query performance.

---

## Indexes

---

### Q21. What is an index in MongoDB?

**Answer ::**
An index is a special data structure that stores field values in an ordered B-tree to support efficient queries and sorts.

---

### Q22. Why are indexes important?

**Answer ::**
Indexes reduce the number of documents scanned to satisfy queries and enable fast equality, range, and sorted result retrievals.

---

### Q23. What is the default index?

**Answer ::**
MongoDB automatically creates a unique index on the `_id` field for every collection, which cannot be dropped.

---

### Q24. What is a single-field vs compound index?

**Answer ::**

Single-field index:

* Covers one field.

Compound index:

* Covers multiple fields.

---

### Q25. What is a unique index?

**Answer ::**
A unique index enforces uniqueness for indexed field values to prevent duplicate entries across documents.

---

### Q26. What is a TTL index?

**Answer ::**
A TTL (Time To Live) index automatically expires and removes documents after a defined time period using `expireAfterSeconds`.

---

### Q27. What is a sparse or partial index?

**Answer ::**

Sparse index:

* Includes documents with the indexed field present.

Partial index:

* Indexes documents matching a filter expression.

---

### Q28. What is a text index?

**Answer ::**
A text index supports full-text search on string content with language-specific stemming and scoring capabilities.

---

### Q29. What are geospatial indexes?

**Answer ::**
Geospatial indexes like 2dsphere support queries on geographic data for proximity and spatial relations.

---

### Q30. What are hidden indexes?

**Answer ::**
Hidden indexes exist on disk but are not used by the query planner, enabling safe index testing and rollback planning.

---

---

## Indexes (Continued)

---

### Q31. How do you create an index?

**Answer ::**
Use `db.collection.createIndex({ field: 1 or -1 }, options)` from mongosh or drivers to create an index with optional properties.

---

### Q32. How are index names formed?

**Answer ::**
By default, MongoDB concatenates keys and directions with underscores.

Example:

```
{item:1, quantity:-1}
```

Becomes:

```
item_1_quantity_-1
```

---

### Q33. Do indexes affect writes?

**Answer ::**
Yes, indexes speed reads but add overhead to writes since inserts and updates must also maintain index structures.

---

### Q34. How to view and drop indexes?

**Answer ::**

View indexes:

```
db.collection.getIndexes()
```

Drop index:

```
db.collection.dropIndex("indexName")
```

---

### Q35. What is a covering index?

**Answer ::**
A covering index satisfies a query using only index keys without scanning documents, improving performance for matching projections.

---

## Aggregation

---

### Q36. What is the aggregation pipeline?

**Answer ::**
The aggregation pipeline processes documents through ordered stages to transform, compute, and reshape results.

---

### Q37. What does $match do?

**Answer ::**
`$match` filters input documents by criteria to reduce downstream work and improve pipeline efficiency.

---

### Q38. What does $group do?

**Answer ::**
`$group` aggregates documents by keys and computes accumulations like sums, counts, and averages.

---

### Q39. What does $project do?

**Answer ::**
`$project` shapes the output by including, excluding, computing, or renaming fields.

---

### Q40. What does $sort do?

**Answer ::**
`$sort` orders documents by specified fields.

---

### Q41. What does $lookup do?

**Answer ::**
`$lookup` performs left outer joins across collections, combining related documents.

---

### Q42. What does $unwind do?

**Answer ::**
`$unwind` deconstructs array fields and outputs a document per array element.

---

### Q43. What is $facet used for?

**Answer ::**
`$facet` runs multiple sub-pipelines in parallel on the same input.

---

### Q44. What do $set / $addFields do?

**Answer ::**
`$set` (alias `$addFields`) adds or replaces fields with computed expressions.

---

### Q45. What are $bucket and $bucketAuto?

**Answer ::**

* `$bucket` groups documents into specified ranges
* `$bucketAuto` computes bucket boundaries automatically

---

### Q46. When do pipelines modify data?

**Answer ::**
Aggregations do not modify collections unless using:

* `$out`
* `$merge`

---

### Q47. How does aggregation compare to map-reduce?

**Answer ::**
Aggregation is the preferred higher-performance alternative to map-reduce, which has been deprecated since MongoDB 5.0.

---

### Q48. Can aggregation run on sharded collections?

**Answer ::**
Yes, aggregation pipelines support sharded collections with distributed processing.

---

### Q49. What are pipeline limitations?

**Answer ::**
There are limits on:

* Result sizes
* Memory usage
* Certain stage constraints

---

### Q50. What are expressions and operators in pipelines?

**Answer ::**
Expressions combine constants, field paths, and operators like `$add` to compute values.

---

## Replication

---

### Q51. What is replication in MongoDB?

**Answer ::**
Replication uses a replica set consisting of multiple mongod processes maintaining the same data for redundancy and high availability.

---

### Q52. What are primary and secondary members?

**Answer ::**

Primary:

* Receives writes

Secondary:

* Replicates data
* Can serve reads

---

### Q53. How do elections work?

**Answer ::**
Elections promote an eligible secondary to primary when needed after failures or maintenance.

---

### Q54. What is an arbiter?

**Answer ::**
An arbiter votes in elections without storing data.

---

### Q55. What is the oplog?

**Answer ::**
The oplog is a capped collection of operations on the primary that secondaries replicate.

---

### Q56. How does write concern interact with replication?

**Answer ::**
Write concern values such as `w:majority` require acknowledgment after replication to enough members.

---

### Q57. What are hidden or priority members?

**Answer ::**

Hidden members:

* Replicate data
* Not readable
* Not electable

Priority:

* Controls election likelihood

---

### Q58. What is rollback?

**Answer ::**
Rollback occurs when a former primary rejoins without having replicated its writes to the new primary.

---

### Q59. Why deploy three-member replica sets?

**Answer ::**
Three-member replica sets improve fault tolerance and allow automatic elections.

---

### Q60. How to deploy a replica set?

**Answer ::**

Steps:

1. Deploy mongod instances
2. Configure replication
3. Run:

```
rs.initiate()
```

---

## Sharding

---

### Q61. What is sharding in MongoDB?

**Answer ::**
Sharding distributes data across multiple machines to support large datasets and high throughput.

---

### Q62. What is a shard key?

**Answer ::**
A shard key is an indexed field or fields whose values determine document distribution across shards.

---

### Q63. Range vs hashed sharding?

**Answer ::**

Range sharding:

* Partitions contiguous value ranges

Hashed sharding:

* Distributes values evenly

---

### Q64. What is mongos?

**Answer ::**
mongos is the stateless query router that routes operations to shards.

---

### Q65. What is the primary shard?

**Answer ::**
The primary shard holds unsharded data for a database.

---

### Q66. What is the balancer?

**Answer ::**
The balancer automatically relocates chunks between shards.

---

### Q67. What are zones?

**Answer ::**
Zones associate data ranges with specific shards to enforce data locality.

---

### Q68. How to choose a good shard key?

**Answer ::**

A good shard key:

* High cardinality
* Well distributed
* Used in queries

---

### Q69. Can aggregations and queries span shards?

**Answer ::**
Yes, mongos routes and merges results across shards transparently.

---

### Q70. Do transactions work in sharded clusters?

**Answer ::**
Yes, MongoDB supports distributed transactions across shards.

---

## Transactions

---

### Q71. What are transactions in MongoDB?

**Answer ::**
Transactions provide ACID guarantees across multiple operations and collections.

---

### Q72. When should transactions be used?

**Answer ::**
Use transactions when multi-document atomicity is required.

---

### Q73. How are transactions started and ended?

**Answer ::**

1. Start session
2. Start transaction
3. Commit or abort

---

### Q74. What isolation do transactions provide?

**Answer ::**
Transactions use snapshot isolation semantics.

---

### Q75. Are there limitations to transactions?

**Answer ::**

Limitations include:

* Timeout limits
* Oplog size impacts
* Performance overhead

---

### Q76. How do transactions differ from retryable writes?

**Answer ::**

Retryable writes:

* Single operation retry

Transactions:

* Multiple operations atomic

---

### Q77. How do drivers support transactions?

**Answer ::**
Drivers use sessions with start, commit, and abort APIs.

---

### Q78. Does Mongoose support transactions?

**Answer ::**
Yes, Mongoose provides transaction helpers using sessions.

---

## Change Streams

---

### Q79. What are change streams?

**Answer ::**
Change streams provide a real-time feed of data changes.

---

### Q80. What are resume tokens?

**Answer ::**
Resume tokens allow restarting change streams after interruptions.

---

### Q81. Change stream requirements?

**Answer ::**

Requires:

* Replica set OR
* Sharded cluster

---

### Q82. Change stream use cases?

**Answer ::**

* Event-driven processing
* Cache invalidation
* Search sync
* Audit trails

---

## Schema Design

---

### Q83. Embedding vs referencing?

**Answer ::**

Embed:

* Bounded relationships

Reference:

* Large or shared data

---

### Q84. One-to-many modeling?

**Answer ::**

Options:

* Embedded arrays
* References

---

### Q85. Many-to-many modeling?

**Answer ::**

Use:

* References
* Linking collections

---

### Q86. What is schema validation?

**Answer ::**
Schema validation enforces document structure using `$jsonSchema`.

---

### Q87. Time-series patterns?

**Answer ::**
Time-series collections optimize storage for timestamped data using buckets.

---

### Q88. What is polymorphic schema?

**Answer ::**
Polymorphic schema stores different document structures in one collection.

---

## Performance & Administration

---

### Q89. What is the database profiler?

**Answer ::**
The profiler captures slow operations for performance analysis.

---

### Q90. What is WiredTiger?

**Answer ::**
WiredTiger is the default storage engine providing compression and concurrency.

---

### Q91. What are capped collections?

**Answer ::**
Capped collections are fixed-size collections that overwrite old documents automatically.

---

### Q92. What are time-series collections?

**Answer ::**
Time-series collections optimize inserts and queries for time-stamped data.

---

### Q93. What is collation?

**Answer ::**
Collation specifies language-specific rules for string comparison.

---

### Q94. How does Atlas help with performance?

**Answer ::**
Atlas Performance Advisor recommends indexes and improvements.

---

### Q95. What are typical backup strategies?

**Answer ::**

* Snapshots
* Continuous backups
* Filesystem backups

---

### Q96. What GUI tools are available?

**Answer ::**

Examples:

* MongoDB Compass
* Connectors
* Drivers

---

## Drivers & Ecosystem

---

### Q97. What are MongoDB drivers?

**Answer ::**
MongoDB drivers are language-specific libraries that connect applications to MongoDB.

---

### Q98. How are connection strings used?

**Answer ::**
Connection strings encode server addresses, authentication, TLS, and options.

Example:

```
mongodb://localhost:27017
```

---

### Q99. What is Mongoose?

**Answer ::**
Mongoose is an ODM that provides models, validation, middleware, and transactions for Node.js.

---

### Q100. How do documentation versions work?

**Answer ::**
MongoDB documentation is versioned with stable and version-specific manuals.

---

---