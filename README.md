# 📘 MongoDB Complete Learning Repository

This repository contains **complete MongoDB learning material** including installation guides, commands, examples, aggregation pipelines, indexing, Atlas setup, and advanced topics.

It is designed as a **step-by-step MongoDB roadmap** from beginner to advanced level.

---

## 📂 Repository Structure

```
MongoDB
│
├── 00 Mongo DB Notes
├── 000 YouTube Videos Details
│
├── 01 Mongo DB Installation
│
├── 02 Sample Databases
│
├── 03 Database Commands
│
├── 04 Collection Commands
│
├── 05 Insert Commands
│   ├── 01 Simple Insert
│   ├── 02 Insert with Date and Time
│   └── 03 Insert in Orders
│
├── 06 Find Commands
│   ├── 01 Simple Find
│   ├── 02 Finding With Date and Time
│   ├── 03 Finding with Array
│   ├── 04 Finding With Exists
│   ├── 05 Finding With Operators
│   ├── 06 Finding Count
│   ├── 07 Finding With Limit
│   ├── 08 Finding With Regex
│   ├── 09 Finding With Skip
│   ├── 10 Finding With Sorting
│   ├── 11 Finding With Type
│   ├── 12 Finding Distinct
│   ├── 13 Finding With Projection
│   └── 14 Find With Collation
│
├── 07 Update Commands
│   ├── 01 Simple Update
│   ├── 02 Change Field Type
│   ├── 03 Updating Date and Time
│   ├── 04 Adding and Removing Field
│   ├── 05 Find And Modify
│   ├── 06 Upsert
│   ├── 07 Replace One
│   ├── 08 Increment & Decrement
│   ├── 09 Bulk Writing
│   ├── 10 Find One And Replace
│   ├── 11 Find One And Update
│   └── 99 Deprecated Updates
│
├── 08 Delete Commands
│
├── 09 Indexing Commands
│   ├── 01 Create Index
│   ├── 02 View Index
│   ├── 03 Modify Index
│   ├── 04 Drop Index
│   ├── 05 Hide/Unhide Index
│   ├── 06 Unique Index
│   └── 07 Index Stats
│
├── 10 Aggregation Commands
│   ├── 01 Simple Joins
│   ├── 02 Union
│   ├── 03 Grouping
│   ├── 04 Match Group Sort
│   ├── 05 Bucket
│   ├── 06 Auto Bucket
│   └── 07 Graph Lookup
│
├── 11 Grouping Commands
│
├── 12 Operators
│
├── 13 Join Collections
│
├── 14 Views
│   ├── 01 View Creation
│   ├── 02 View Info
│   └── 03 View Drop
│
├── 15 Custom Validation
│
├── 16 GeoSpatial Queries
│
├── 17 Read & Write Concern
│
├── 18 Retryable Reads & Writes
│
├── 19 Vector Search
│
├── 20 Sharding
│
├── 21 Cursor
│
├── 22 Importing & Exporting
│
├── 23 User Management
│
├── 99 MongoDB Atlas
│   ├── 01 Atlas Creation
│   ├── 02 Atlas Connection
│   └── 03 CRUD Operations
│
└── 100 MongoDB vs SQL
```

---

# 🚀 Topics Covered

## 📌 Basic Topics

* MongoDB Installation
* MongoDB Shell
* Database Commands
* Collection Commands
* Insert Operations
* Find Queries
* Update Queries
* Delete Queries

---

## 📌 Intermediate Topics

* Indexing
* Aggregation Pipeline
* Operators
* Views
* Joins
* Grouping
* Validation Rules

---

## 📌 Advanced Topics

* GeoSpatial Queries
* Sharding
* Read & Write Concern
* Retryable Reads/Writes
* Vector Search
* Cursor Handling

---

## 📌 MongoDB Atlas

* Atlas Account Creation
* Cluster Setup
* Connection Methods
* CRUD Operations

---

# 🧪 Sample Databases

Sample databases are included for practice:

```
02 Sample Databases
```

These databases are used for:

* Insert Examples
* Find Queries
* Aggregations
* Joins
* Indexing Practice

---

# 🛠 Requirements

Install:

* MongoDB Server
* MongoDB Shell (mongosh)
* MongoDB Compass (Optional)

---

# ▶️ Running MongoDB

Start MongoDB:

```bash
mongod
```

Open MongoDB Shell:

```bash
mongosh
```

Show Databases:

```javascript
show dbs
```

Create Database:

```javascript
use ecommerce
```

---

# 📥 Importing Data

Example:

```bash
mongoimport --db ecommerce --collection products --file products.json --jsonArray
```

---

# 📤 Exporting Data

Example:

```bash
mongoexport --db ecommerce --collection products --out products.json --jsonArray
```

---

# 🎯 Learning Path (Recommended Order)

Study folders in this order:

1. Mongo DB Installation
2. Database Commands
3. Collection Commands
4. Insert Commands
5. Find Commands
6. Update Commands
7. Delete Commands
8. Indexing
9. Aggregation
10. Views
11. Atlas
12. Advanced Topics

---

# 🎥 Video References

Video references are available in:

```
000 YouTube Videos Details
```

---

# 👨‍💻 Author

MongoDB Learning Repository
Designed for **MongoDB + MERN Stack Learning**

---

# ⭐ Features

✔ Beginner to Advanced MongoDB
✔ Real Examples
✔ Structured Learning
✔ Atlas Setup
✔ Aggregation Examples
✔ Production Concepts
