# MongoDB Notes

## Resources
- **MongoDB Lecture**: [Link](https://www.youtube.com/watch?v=c2M-rlkkT5o)
- **MongoDB Documentation**: [Link](https://www.mongodb.com)

---

## Databases Basics
- **Show all databases**: `show dbs`
- **Use or create a database**: `use <database_name>`
- **Create a collection in a database**: `db.createCollection("<collection_name>")`
- **Drop a database**: `db.dropDatabase()`

---

## Insert
- **Insert one document**:
  ```
  db.students.insertOne({name: "Ayush Prem", age: 20, sgpa: 8.45})
  ```
  Example response:
  ```
  {
    acknowledged: true,
    insertedId: ObjectId('67705f5640d9ecdc674eeb86')
  }
  ```

- **Find all documents**:
  ```
  db.students.find()
  ```

  Example response:
  ```
  [
    {
      _id: ObjectId('67705f5640d9ecdc674eeb86'),
      name: 'Ayush Prem',
      age: 20,
      sgpa: 8.45
    }
  ]
  ```

- **Insert multiple documents**:
  ```
  db.students.insertMany([
    {name: "prem", age: 19, sgpa: 7.84},
    {name: "kumar", age: 18, sgpa: 8.12},
    {name: "gupta", age: 15, percentage: 93.4}
  ])
  ```

---

## Data Types
- **String**: `{name: "Ayush Prem"}`
- **Integer**: `{age: 20}`
- **Floating-point**: `{sgpa: 8.45}`
- **Boolean**: `{intern: false}`
- **Date Objects**: `{learningDate: new Date("2024-12-29")}`
- **Null**: `{girlfriend: null}`
- **Arrays**: `{courses: ["maths", "dsa", "stats"]}`
- **Nested Documents**: `{address: {street: "22B, Baker Street", city: "Central London"}}`

---

## Sorting and Listing
- **Sort documents**:
  ```
  db.students.find().sort({name: 1}) // Ascending
  db.students.find().sort({name: -1}) // Descending
  ```
- **Limit results**:
  ```
  db.students.find().limit(1)
  ```
- **Sort and limit**:
  ```
  db.students.find().sort({age: -1}).limit(1)
  ```

---

## Find
- **Find a document**:
  ```
  db.students.find({name: "Ayush Prem"})
  ```
- **Retrieve specific fields**:
  ```
  db.students.find({}, {name: true})
  ```
- **Exclude the `_id` field**:
  ```
  db.students.find({}, {_id: false, name: true})
  ```

---

## Update
- **Set a field**:
  ```
  db.students.updateOne({name: "Ayush Prem"}, {$set: {intern: true}})
  ```
- **Unset a field**:
  ```
  db.students.updateOne({name: "Ayush Prem"}, {$unset: {intern: ""}})
  ```
- **Update multiple documents**:
  ```
  db.students.updateMany({}, {$set: {intern: false}})
  ```
- **Set a field if it doesn’t exist**:
  ```
  db.students.updateMany({intern: {$exists: false}}, {$set: {intern: true}})
  ```

---

## Delete
- **Delete one document**:
  ```
  db.students.deleteOne({name: "gupta"})
  ```
- **Delete multiple documents**:
  ```
  db.students.deleteMany({intern: true})
  ```
- **Delete documents based on field existence**:
  ```
  db.students.deleteMany({percentage: {$exists: true}})
  ```

---

## Comparison Operators
- **Not equal**:
  ```
  db.students.find({name: {$ne: "Ayush Prem"}})
  ```
- **Less than**:
  ```
  db.students.find({age: {$lt: 20}})
  ```
- **Less than or equal to**:
  ```
  db.students.find({age: {$lte: 20}})
  ```
- **Greater than**:
  ```
  db.students.find({age: {$gt: 15}})
  ```
- **Greater than or equal to**:
  ```
  db.students.find({age: {$gte: 15}})
  ```
- **Between values**:
  ```
  db.students.find({sgpa: {$gte: 8, $lte: 10}})
  ```
- **Within an array**:
  ```
  db.students.find({name: {$in: ["Ayush Prem", "prem"]}})
  ```
- **Not in an array**:
  ```
  db.students.find({name: {$nin: ["Ayush Prem", "prem"]}})
  ```

---

## Logical Operators
- **AND**:
  ```
  db.students.find({$and: [{sgpa: {$gte: 8}}, {age: {$gte: 18}}]})
  ```
- **OR**:
  ```
  db.students.find({$or: [{sgpa: {$gte: 8}}, {age: {$gte: 18}}]})
  ```
- **NOR**:
  ```
  db.students.find({$nor: [{sgpa: {$gte: 8}}, {age: {$gte: 18}}]})
  ```
- **NOT**:
  ```
  db.students.find({age: {$not: {$gte: 20}}})
  ```

---

## Indexes
- **Use linear search**:
  ```
  db.students.find({name: "kumar"}).explain("executionStats")
  ```
- **Create an index**:
  ```
  db.students.createIndex({name: 1})
  ```
- **Search with B-tree index**:
  ```
  db.students.find({name: "kumar"}).explain("executionStats")
  ```
- **Get indexes**:
  ```
  db.students.getIndexes()
  ```
- **Drop an index**:
  ```
  db.students.dropIndex("name_1")
  ```

---

## Collections
- **Show collections**:
  ```
  show collections
  ```
- **Create a capped collection**:
  ```
  db.createCollection("teachers", {
    capped: true,
    size: 10000000, // in bytes
    max: 100, // max number of documents
    autoIndexId: false
  })
  ```

