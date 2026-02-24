# Mongoose Model & Document Methods Reference

Complete reference for **Mongoose Model Methods and Document Instance Methods** including behavior, validation, middleware, and examples.

---

# Table of Contents

1. Create Operations
2. Read Operations
3. Update Operations
4. Delete Operations
5. Indexes and Utilities
6. Document Instance Methods
7. Query Builders
8. Middleware & Validation Behavior
9. Version Key Behavior
10. Most Used Methods Quick List

---

# 1. Create Operations

## 1.1 Model.create()

Creates one or more documents.

### Syntax

```js
Model.create(docs, options)
```

### Parameters

| Parameter | Description                |
| --------- | -------------------------- |
| docs      | Object or Array of objects |
| options   | Optional settings          |

### Features

* Inserts one or many documents
* Runs validation
* Runs middleware (pre/post save)
* Faster than save() for bulk inserts

### Example

```js
await User.create({
  name: "Riyaz",
  age: 25
});
```

### Multiple Documents

```js
await User.create([
 {name:"A"},
 {name:"B"}
]);
```

---

## 1.2 new Model().save()

Creates or updates a document.

### Syntax

```js
const doc = new Model(data)
await doc.save(options)
```

### Behavior

| Case          | Action          |
| ------------- | --------------- |
| isNew = true  | Insert document |
| isNew = false | Update document |

### Features

* Runs validation
* Runs middleware
* Tracks modified fields
* Performs minimal update

### Example

```js
const user = new User({
 name:"Riyaz"
})

await user.save()
```

---

# 2. Read Operations

Query builders return a **Query Object**

Example:

```js
const users = await User.find()
```

---

## 2.1 Model.find()

Find multiple documents.

### Syntax

```js
Model.find(filter, projection, options)
```

### Example

```js
User.find({age:20})
```

---

## 2.2 Model.findOne()

Find first matching document.

### Syntax

```js
Model.findOne(filter, projection, options)
```

### Example

```js
User.findOne({name:"Riyaz"})
```

---

## 2.3 Model.findById()

Shortcut for `_id`.

### Syntax

```js
Model.findById(id, projection, options)
```

Equivalent to:

```js
Model.findOne({_id:id})
```

---

## 2.4 Model.exists()

Check if document exists.

### Syntax

```js
Model.exists(filter)
```

### Example

```js
User.exists({email:"a@gmail.com"})
```

Returns:

```
null or {_id}
```

---

## 2.5 Model.countDocuments()

Count matching documents.

### Syntax

```js
Model.countDocuments(filter)
```

### Example

```js
User.countDocuments({age:20})
```

---

## 2.6 Model.estimatedDocumentCount()

Fast estimated count.

### Syntax

```js
Model.estimatedDocumentCount()
```

### Notes

* Uses metadata
* Faster
* Not exact

---

## 2.7 Model.distinct()

Get unique values.

### Syntax

```js
Model.distinct(field, filter)
```

### Example

```js
User.distinct("city")
```

---

## 2.8 Model.aggregate()

Aggregation Pipeline.

### Syntax

```js
Model.aggregate(pipeline, options)
```

### Example

```js
User.aggregate([
 { $match:{age:20} }
])
```

---

# 3. FindOneAnd Variants

Usually return a document.

---

## 3.1 findOneAndUpdate()

### Syntax

```js
Model.findOneAndUpdate(filter, update, options)
```

### Example

```js
User.findOneAndUpdate(
 {name:"Riyaz"},
 {$set:{age:30}},
 {new:true}
)
```

---

## 3.2 findOneAndReplace()

Replace full document.

```js
Model.findOneAndReplace(filter,replacement,options)
```

---

## 3.3 findOneAndDelete()

```js
Model.findOneAndDelete(filter,options)
```

---

## 3.4 findOneAndRemove()

Alias for delete.

```js
Model.findOneAndRemove(filter,options)
```

---

## 3.5 findByIdAndUpdate()

Shortcut.

```js
Model.findByIdAndUpdate(id,update,options)
```

Equivalent:

```js
Model.findOneAndUpdate({_id:id})
```

---

## 3.6 findByIdAndDelete()

```js
Model.findByIdAndDelete(id,options)
```

---

## 3.7 findByIdAndRemove()

Alias.

```js
Model.findByIdAndRemove(id,options)
```

---

# 4. Update Operations

Bulk-style updates.

### Important

These **DO NOT run save middleware**

---

## 4.1 updateOne()

Update first match.

### Syntax

```js
Model.updateOne(filter,update,options)
```

### Validation

Enable manually:

```js
{runValidators:true}
```

### Example

```js
User.updateOne(
 {name:"Riyaz"},
 {$set:{age:28}},
 {runValidators:true}
)
```

---

## 4.2 updateMany()

Update many.

```js
Model.updateMany(filter,update,options)
```

---

## 4.3 replaceOne()

Replace entire document.

```js
Model.replaceOne(filter,replacement,options)
```

---

## 4.4 bulkWrite()

Batch operations.

```js
Model.bulkWrite(operations,options)
```

### Example

```js
User.bulkWrite([
 {
  insertOne:{
   document:{name:"A"}
  }
 },
 {
  updateOne:{
   filter:{name:"A"},
   update:{$set:{age:20}}
  }
 }
])
```

---

# 5. Delete Operations

---

## 5.1 deleteOne()

Delete first match.

```js
Model.deleteOne(filter,options)
```

---

## 5.2 deleteMany()

Delete multiple.

```js
Model.deleteMany(filter,options)
```

---

## 5.3 remove()

Legacy.

```js
Model.remove(filter)
```

### Note

Use instead:

```
deleteOne()
deleteMany()
```

---

# 6. Indexes and Utilities

---

## 6.1 createIndexes()

Build indexes.

```js
Model.createIndexes()
```

---

## 6.2 ensureIndexes()

Older alias.

```js
Model.ensureIndexes()
```

---

## 6.3 syncIndexes()

Sync schema indexes with DB.

```js
Model.syncIndexes()
```

---

## 6.4 listIndexes()

List indexes.

```js
Model.listIndexes()
```

---

## 6.5 discriminator()

Inheritance models.

```js
Model.discriminator(name,schema,options)
```

---

## 6.6 hydrate()

Convert object → Document.

```js
Model.hydrate(obj)
```

No DB call.

---

## 6.7 startSession()

Transactions.

```js
Model.startSession()
```

---

## 6.8 watch()

Change Streams.

```js
Model.watch(pipeline,options)
```

---

# 7. Document Instance Methods

Methods on document object.

---

## 7.1 doc.save()

Insert or update.

```js
doc.save(options)
```

### Features

* Full validation
* Middleware
* Minimal update

---

## 7.2 doc.updateOne()

Update document.

```js
doc.updateOne(update,options)
```

### Notes

* No save middleware
* Use runValidators

---

## 7.3 doc.deleteOne()

Delete document.

```js
doc.deleteOne()
```

---

## 7.4 doc.validate()

Run validation.

```js
doc.validate()
```

---

## 7.5 doc.validateSync()

Sync validation.

```js
doc.validateSync()
```

---

## 7.6 doc.toObject()

Convert to plain object.

```js
doc.toObject()
```

---

## 7.7 doc.toJSON()

Convert to JSON.

```js
doc.toJSON()
```

---

## 7.8 doc.populate()

Populate references.

```js
doc.populate("user")
```

---

## 7.9 Change Tracking

### isNew

```js
doc.$isNew
```

---

### isModified

```js
doc.isModified("name")
```

---

### markModified

```js
doc.markModified("field")
```

---

# 8. Middleware & Validation Behavior

## save()

Runs:

* Validators
* pre save middleware
* post save middleware

```
doc.save()
Model.create()
```

---

## update()

Does NOT run save middleware.

```
updateOne()
updateMany()
findOneAndUpdate()
```

---

## Enable Validation in Update

```
runValidators:true
```

Example:

```js
Model.updateOne(
 {},
 {},
 {runValidators:true}
)
```

---

# 9. Version Key Behavior

Default version field:

```
__v
```

---

## Auto Increment

Increments automatically on:

```
save()
```

---

## Does NOT Increment Automatically

```
updateOne()
updateMany()
findOneAndUpdate()
```

Must handle manually.

---

# 10. Most Used Methods (Quick List)

## Create

```
Model.create()
new Model().save()
```

---

## Read

```
Model.find()
Model.findOne()
Model.findById()
```

---

## Update

```
Model.updateOne()
Model.updateMany()
Model.findOneAndUpdate()
Model.findByIdAndUpdate()
```

---

## Delete

```
Model.deleteOne()
Model.deleteMany()
Model.findOneAndDelete()
Model.findByIdAndDelete()
```
