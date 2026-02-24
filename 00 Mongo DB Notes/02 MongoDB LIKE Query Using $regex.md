# MongoDB LIKE Query Using $regex

To create a **"LIKE" query in MongoDB**, similar to SQL's `LIKE` operator, you can use MongoDB's **`$regex` operator**, which allows pattern matching using regular expressions.

This is the primary way to perform **"like" searches** in MongoDB.

---

## Basic Syntax for a "LIKE" Query in MongoDB

```js
db.collection.find({
  "field": {
    $regex: /pattern/,
    $options: 'i'
  }
});
````

### Parameters

* **field**
  The field in the document to search.

* **pattern**
  The regex pattern to match.
  Example: `"text"` to match any occurrence of `"text"`.

* **$options: 'i'**
  Makes the search **case-insensitive** (optional).

---

## Examples

### 1. Find documents where the `name` field contains "m" anywhere (case-insensitive)

```js
db.users.find({
  name: {
    $regex: /m/,
    $options: 'i'
  }
});
```

---

### 2. Find documents where the `position` field contains "developer" (case-sensitive)

```js
db.employee.find({
  position: {
    $regex: "developer"
  }
});
```

---

### 3. Find documents where the `name` starts with "B"

```js
db.employee.find({
  name: {
    $regex: "^B"
  }
});
```

---

### 4. Find documents where the `name` ends with "e"

```js
db.employee.find({
  name: {
    $regex: "e$"
  }
});
```

---

## Notes

* MongoDB **regex queries allow more advanced and flexible pattern matching** than SQL `LIKE`.

* Regex is **case-sensitive by default**.

* Using the following option enables case-insensitive search:

```js
$options: 'i'
```

* **`$regex` is the closest equivalent to SQL's LIKE operation in MongoDB.**

* This method is widely used for **filtering document fields using substring or pattern matching** similar to **LIKE queries in SQL databases.**

---

## SQL LIKE vs MongoDB Regex Comparison

| SQL LIKE                           | MongoDB Regex                                  |
| ---------------------------------- | ---------------------------------------------- |
| `LIKE '%text%'`                    | `{ field: { $regex: /text/ } }`                |
| `LIKE 'text%'`                     | `{ field: { $regex: /^text/ } }`               |
| `LIKE '%text'`                     | `{ field: { $regex: /text$/ } }`               |
| `LIKE '%text%' (case-insensitive)` | `{ field: { $regex: /text/, $options: 'i' } }` |

---

## Summary

MongoDB does not have a direct `LIKE` operator like SQL. Instead, the **`$regex` operator** is used to perform pattern matching queries.

It provides:

* Substring search
* Prefix search
* Suffix search
* Case-insensitive search
* Advanced pattern matching

```