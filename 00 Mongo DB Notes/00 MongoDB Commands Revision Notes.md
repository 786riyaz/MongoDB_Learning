# MongoDB Revision Notes (Complete Guide)

This document contains **essential MongoDB shell commands** for revision, including **Database Operations, Collection Operations, CRUD Operations, Indexing, and Aggregation**.

---

# 1. Database Commands

## Show All Databases

```js
show dbs
```

### Description

Displays a list of all databases present in MongoDB.

### Example Output

```
admin
config
local
ecommerce
```

---

## Select / Create Database

```js
use <DatabaseName>
```

### Description

Switches to a database.

If the database does not exist, MongoDB **creates it automatically when data is inserted.**

### Example

```js
use ecommerce
```

---

## Show Current Database

```js
db
```

### Description

Displays the name of the currently selected database.

### Example Output

```
ecommerce
```

---

## Delete Current Database

```js
db.dropDatabase()
```

### Description

Deletes the current database completely.

### Warning

⚠️ This operation is irreversible.

---

# 2. Collection Commands

## Show Collections

```js
show collections
```

### Description

Displays all collections inside the current database.

---

## Create Collection

```js
db.createCollection("<CollectionName>")
```

### Description

Creates a new collection manually.

### Example

```js
db.createCollection("users")
```

---

## Auto Creation (Recommended)

MongoDB automatically creates collections when inserting data.

Example:

```js
db.users.insertOne({name:"Riyaz"})
```

---

## Delete Collection

```js
db.<CollectionName>.drop()
```

### Example

```js
db.users.drop()
```

### Description

Deletes the collection permanently.

---

# 3. Insert Operations

## Insert One Document

```js
db.CollectionName.insertOne({
 name:"Riyaz",
 age:25
})
```

### Description

Inserts a single document.

### Example

```js
db.users.insertOne({
 name:"Riyaz",
 age:25
})
```

---

## Insert Multiple Documents

```js
db.CollectionName.insertMany([
 {name:"Riyaz", age:25},
 {name:"Test", age:25},
 {name:"XYZ", age:25}
])
```

### Description

Inserts multiple documents at once.

---

## Additional Variations

### Insert with Custom _id

```js
db.users.insertOne({
 _id:1,
 name:"Riyaz",
 age:25
})
```

---

### Insert Nested Document

```js
db.users.insertOne({
 name:"Riyaz",
 address:{
   city:"Ahmedabad",
   state:"Gujarat"
 }
})
```

---

### Insert Array

```js
db.users.insertOne({
 name:"Riyaz",
 skills:["NodeJS","MongoDB","React"]
})
```

---

# 4. Find Operations (Read Data)

## Find All Documents

```js
db.CollectionName.find()
```

### Example

```js
db.users.find()
```

---

## Pretty Format Output

```js
db.CollectionName.find().pretty()
```

### Description

Displays formatted output.

---

## Find with Condition

```js
db.CollectionName.find({age:25})
```

---

## Find with Greater Than or Equal

```js
db.CollectionName.find({
 age:{$gte:25}
})
```

---

## Find with Greater Than

```js
db.CollectionName.find({
 age:{$gt:25}
})
```

---

## Find One Document

```js
db.CollectionName.findOne({
 name:"Riyaz"
})
```

---

# Query Operators

## Comparison Operators

| Operator | Meaning            |
| -------- | ------------------ |
| $eq      | Equal              |
| $gt      | Greater Than       |
| $gte     | Greater Than Equal |
| $lt      | Less Than          |
| $lte     | Less Than Equal    |
| $ne      | Not Equal          |
| $in      | Value in Array     |
| $nin     | Not in Array       |

---

## Examples

### Less Than

```js
db.users.find({
 age:{$lt:30}
})
```

---

### Between Range

```js
db.users.find({
 age:{$gte:20,$lte:30}
})
```

---

### IN Operator

```js
db.users.find({
 age:{$in:[20,25,30]}
})
```

---

# 5. Update Operations

## Update One Document

```js
db.CollectionName.updateOne(

 {name:"Riyaz"},     // Filter

 {$set:{age:26}}     // Update

)
```

### Description

Updates only the first matching document.

---

## Update Many

```js
db.users.updateMany(

 {age:25},

 {$set:{status:"active"}}

)
```

---

## Replace Document

```js
db.users.replaceOne(

 {name:"Riyaz"},

 {name:"Riyaz",age:26}

)
```

### Description

Replaces entire document.

---

## Increment Value

```js
db.users.updateOne(

 {name:"Riyaz"},

 {$inc:{age:1}}

)
```

---

## Add Field

```js
db.users.updateOne(

 {name:"Riyaz"},

 {$set:{city:"Ahmedabad"}}

)
```

---

## Remove Field

```js
db.users.updateOne(

 {name:"Riyaz"},

 {$unset:{city:""}}

)
```

---

# 6. Delete Operations

## Delete One

```js
db.CollectionName.deleteOne({
 name:"Riyaz"
})
```

---

## Delete Many

```js
db.CollectionName.deleteMany({
 name:"Riyaz"
})
```

---

## Delete All Documents

```js
db.users.deleteMany({})
```

---

# 7. Count Documents

## Count All

```js
db.CollectionName.countDocuments()
```

---

## Count with Condition

```js
db.CollectionName.countDocuments({
 age:{$gte:25}
})
```

---

## Estimated Count (Fast)

```js
db.users.estimatedDocumentCount()
```

### Description

Faster but approximate count.

---

# 8. Indexing

## Create Index

```js
db.CollectionName.createIndex({
 name:1
})
```

### Description

Creates ascending index.

---

## Descending Index

```js
db.users.createIndex({
 age:-1
})
```

---

## Compound Index

```js
db.users.createIndex({
 name:1,
 age:-1
})
```

---

## Multiple Indexes

```js
db.CollectionName.createIndexes([
 {key:{name:1}},
 {key:{age:-1}}
])
```

---

## Show Indexes

```js
db.users.getIndexes()
```

---

## Drop Index

```js
db.users.dropIndex("name_1")
```

---

# 9. Aggregation Framework

Aggregation is used for **data analysis and transformation.**

---

## Basic Aggregation

```js
db.CollectionName.aggregate([

 {$group:{
   _id:"$city",
   total:{$sum:1}
 }}

])
```

### Description

Counts documents per city.

---

## Match + Sort + Project

```js
db.CollectionName.aggregate([

 {$match:{age:{$gt:20}}},

 {$sort:{age:1}},

 {$project:{
   firstName:1,
   class:1,
   _id:0
 }}

])
```

### Description

1. Filters records
2. Sorts records
3. Selects fields

---

## Category Price Sum Example

```js
db.CollectionName.aggregate([

 { $match: { Category: "Electronics" } },

 { $group: {

     _id: "$Brand",

     totalPrice: {

       $sum: "$Price"

     }

 }}

])
```

### Description

Calculates total price per brand.

---

# 10. Aggregation Operators

## $match

Filters documents.

```js
{$match:{age:{$gt:20}}}
```

---

## $group

Groups documents.

```js
{$group:{
 _id:"$city",
 total:{$sum:1}
}}
```

---

## $sort

Sorts documents.

```js
{$sort:{age:1}}
```

### Values

```
1 = Ascending
-1 = Descending
```

---

## $project

Selects fields.

```js
{$project:{
 name:1,
 age:1,
 _id:0
}}
```

---

# 11. Important Notes

## MongoDB Document Structure

Example:

```js
{
 _id:ObjectId("123"),
 name:"Riyaz",
 age:25
}
```

---

## Collection Naming Best Practice

Recommended:

```
users
products
orders
categories
```

Avoid:

```
UserDataCollectionTable
```

---

# 12. Most Important Commands (Interview)

### Database

```
show dbs
use dbName
db
db.dropDatabase()
```

### Collections

```
show collections
db.createCollection()
db.collection.drop()
```

### CRUD

```
insertOne()
insertMany()

find()
findOne()

updateOne()
updateMany()

deleteOne()
deleteMany()
```

### Aggregation

```
$match
$group
$sort
$project
```

---
