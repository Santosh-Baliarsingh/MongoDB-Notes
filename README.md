<!-- markdownlint-disable MD033 -->
# MongoDB Reference

 ***I have recently started learning MongoDB and am compiling my notes here for reference. If you find this information useful, feel free to use it as a resource.***

## Table of Contents

- [MongoDB Reference](#mongodb-reference)
  - [Table of Contents](#table-of-contents)
  - [What is MongoDB?](#what-is-mongodb)
  - [Key Features of MongoDB](#key-features-of-mongodb)
  - [Differences Between MongoDB and Relational Databases](#differences-between-mongodb-and-relational-databases)
  - [MongoDB Data Model](#mongodb-data-model)
    - [BSON Data Types](#bson-data-types)
    - [Example BSON Document](#example-bson-document)
  - [Installation](#installation)
    - [Windows](#windows)
    - [macOS](#macos)
    - [Ubuntu](#ubuntu)
  - [Open MongoDB Shell](#open-mongodb-shell)
    - [Expected Output](#expected-output)
  - [Shell vs Driver](#shell-vs-driver)
    - [MongoDB Shell](#mongodb-shell)
    - [MongoDB Driver](#mongodb-driver)
  - [Understanding Databases, Collections, and Documents](#understanding-databases-collections-and-documents)
    - [Databases](#databases)
    - [Collections](#collections)
    - [Documents](#documents)
    - [Example](#example)
  - [Differences Between JSON and BSON Format](#differences-between-json-and-bson-format)
  - [Default Storage Engines Used by Different Databases](#default-storage-engines-used-by-different-databases)
  - [1. Creating Database and Collection](#1-creating-database-and-collection)
    - [Show All Databases](#show-all-databases)
    - [Create Database](#create-database)
    - [Create a Collection](#create-a-collection)
  - [Create a Document](#create-a-document)
    - [insertOne Method](#insertone-method)
    - [insertMany Method](#insertmany-method)
    - [Create a Document with Custom `_Id`](#create-a-document-with-custom-_id)
    - [Ordered Inserts](#ordered-inserts)
    - [Unordered inserts](#unordered-inserts)
    - [Write Concern and Journaling in MongoDB](#write-concern-and-journaling-in-mongodb)
    - [What is Atomictiy?](#what-is-atomictiy)
  - [Read a Document](#read-a-document)
    - [find Method](#find-method)
    - [find Method with Query](#find-method-with-query)
    - [find Method with Projection](#find-method-with-projection)
    - [findOne Method with Query](#findone-method-with-query)
    - [findOne Method with Projection](#findone-method-with-projection)
    - [find Method and Cursor Object](#find-method-and-cursor-object)
  - [Update a Document](#update-a-document)
    - [updateOne Method](#updateone-method)
    - [updateMany Method](#updatemany-method)
  - [Delete a Document](#delete-a-document)
    - [deleteOne Method](#deleteone-method)
    - [deleteMany Method](#deletemany-method)
  - [Embedded Documents and Arrays](#embedded-documents-and-arrays)
    - [Embedded Document](#embedded-document)
    - [Arrays of Data](#arrays-of-data)
  - [Accessing Structured Data](#accessing-structured-data)
    - [Query Objects](#query-objects)
    - [Query Arrays](#query-arrays)
    - [Query Array of Objects](#query-array-of-objects)
  - [Resetting Database](#resetting-database)
    - [Delete a Database](#delete-a-database)
    - [Delete a Collection](#delete-a-collection)
    - [Delete a Specific Document](#delete-a-specific-document)
    - [Delete all Documents](#delete-all-documents)
    - [Statistics about the Database](#statistics-about-the-database)
  - [2. Schemas and Relations](#2-schemas-and-relations)
    - [Why do we use Schemas?](#why-do-we-use-schemas)
    - [Structuring Documents](#structuring-documents)
    - [Data Types](#data-types)
  - [Understanding Relations](#understanding-relations)
    - [One-to-One Relationship - Embedding](#one-to-one-relationship---embedding)
    - [One-to-One Relationship - Referencing](#one-to-one-relationship---referencing)
    - [One-to-Many Relationship - Embedding](#one-to-many-relationship---embedding)
    - [One-to-Many Relationship - Referencing](#one-to-many-relationship---referencing)
    - [Many-to-Many Relationship - Embedding](#many-to-many-relationship---embedding)
    - [Many-to-Many Relationship - Referencing](#many-to-many-relationship---referencing)
  - [Schema Validation](#schema-validation)
    - [Define a Schema](#define-a-schema)
    - [Create the Collection with Validation](#create-the-collection-with-validation)
    - [Insert Document](#insert-document)
    - [Handle Validation Errors](#handle-validation-errors)

## What is MongoDB?

MongoDB is a NoSQL database that provides high performance, high availability, and easy scalability. Unlike traditional relational databases, MongoDB uses a flexible, JSON-like document structure, which means data can be stored in a more natural and less rigid format.

## Key Features of MongoDB

- **Document-Oriented Storage**: Data is stored in flexible, JSON-like documents.
- **Schema-less**: No predefined schema, allowing for dynamic changes to the data structure.
- **Scalability**: Supports horizontal scaling through sharding.
- **High Performance**: Optimized for read and write operations.
- **High Availability**: Built-in replication and failover mechanisms.

## Differences Between MongoDB and Relational Databases

| Feature        | MongoDB                                           | Relational Databases                                   |
| -------------- | ------------------------------------------------- | ------------------------------------------------------ |
| Data Model     | Document-oriented (JSON-like)                     | Table-based (rows and columns)                         |
| Schema         | Schema-less                                       | Fixed schema                                           |
| Scalability    | Horizontal (sharding)                             | Vertical (scaling up)                                  |
| Transactions   | Limited support (multi-document)                  | Full ACID transactions                                 |
| Query Language | MongoDB Query Language (MQL)                      | SQL                                                    |
| Joins          | No joins, uses embedded documents or linking      | Supports joins                                         |
| Performance    | Optimized for large-scale data                    | Can be slower for large-scale data                     |
| Storage        | BSON format                                       | Various formats (e.g., InnoDB, MyISAM)                 |
| Indexing       | Supports indexing                                 | Supports indexing                                      |
| Flexibility    | High flexibility                                  | Less flexibility                                       |
| Use Cases      | Big data, real-time analytics, content management | Transactional systems, complex queries, data integrity |

## MongoDB Data Model

MongoDB stores data in a flexible, JSON-like format called BSON (Binary JSON). BSON extends the JSON model to provide additional data types, ordered fields, and efficient encoding and decoding.

### BSON Data Types

- **String**: UTF-8 string.
- **Integer**: 32-bit or 64-bit integer.
- **Boolean**: `true` or `false`.
- **Double**: 64-bit floating point.
- **Date**: Date and time in milliseconds since the Unix epoch.
- **Array**: Ordered list of values.
- **Object**: Embedded document.
- **Null**: Null value.
- **ObjectId**: Unique identifier for documents.
- **Binary Data**: Binary data.
- **Code**: JavaScript code.
- **Regular Expression**: Regular expression.

### Example BSON Document

```json
{
  "_id": { "$oid": "507f1f77bcf86cd799439011" },
  "name": "John Doe",
  "age": 29,
  "isActive": true,
  "createdAt": { "$date": "2021-01-01T00:00:00Z" },
  "scores": [85, 92, 88],
  "address": {
    "street": "123 Main St",
    "city": "Anytown",
    "zip": "12345"
  }
}
```

## Installation

### Windows

1. **Download the MongoDB Installer**
   - Go to the [MongoDB Download Center](https://www.mongodb.com/try/download/community).
   - Select the version you want to install and download the `.msi` installer.

2. **Run the Installer**
   - Double-click the downloaded `.msi` file.
   - Follow the installation prompts. Choose "Complete" setup type.
   - **Note**: Make sure to install MongoDB Compass during the installation process. MongoDB Compass is a graphical interface for MongoDB. If you skip this step, you can manually install it from the [MongoDB Compass Download Page](https://www.mongodb.com/try/download/compass).

3. **Add MongoDB to the System Path**
   - Open the Start Menu, search for "Environment Variables", and select "Edit the system environment variables".
   - In the System Properties window, click on the "Environment Variables" button.
   - In the Environment Variables window, find the "Path" variable in the "System variables" section, select it, and click "Edit".
   - Click "New" and add the path to the MongoDB `bin` directory (e.g., `C:\Program Files\MongoDB\Server\<version>\bin`).

4. **Start MongoDB**
   - Open Command Prompt as an administrator.
   - Run the following command to start the MongoDB server:
  
     ```shell
     mongod
     ```

   - You should see output similar to the following:

     ```shell
     {"t":{"$date":"2023-10-01T12:00:00.000+00:00"},"s":"I",  "c":"CONTROL",  "id":12345, "ctx":"main","msg":"MongoDB starting","attr":{"pid":1234,"port":27017,"dbPath":"/data/db","architecture":"64-bit","host":"localhost"}}
     {"t":{"$date":"2023-10-01T12:00:00.000+00:00"},"s":"I",  "c":"STORAGE",  "id":12345, "ctx":"initandlisten","msg":"Initializing the storage engine"}
     {"t":{"$date":"2023-10-01T12:00:00.000+00:00"},"s":"I",  "c":"NETWORK",  "id":12345, "ctx":"initandlisten","msg":"Waiting for connections","attr":{"port":27017,"bindIp":"127.0.0.1"}}
     ```

### macOS

1. **Install MongoDB**
   - Tap the MongoDB Homebrew formulae:
  
     ```shell
     brew tap mongodb/brew
     ```

   - Install MongoDB:
  
     ```shell
     brew install mongodb-community@<version>
     ```

2. **Start MongoDB**
   - Start the MongoDB server:

     ```shell
     brew services start mongodb/brew/mongodb-community
     ```

   - For more details, visit the [MongoDB Installation Guide for macOS](https://www.mongodb.com/docs/manual/tutorial/install-mongodb-on-os-x/).

### Ubuntu

1. **Import the Public Key**
   - Open Terminal and run:
  
     ```shell
     wget -qO - https://www.mongodb.org/static/pgp/server-4.4.asc | sudo apt-key add -
     ```

2. **Create a List File for MongoDB**
   - Run the following command to create the list file:
  
     ```shell
     echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/4.4 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.4.list
     ```

3. **Reload the Local Package Database**
   - Run:
  
     ```shell
     sudo apt-get update
     ```

4. **Install MongoDB Packages**
   - Run:
  
     ```shell
     sudo apt-get install -y mongodb-org
     ```

5. **Start MongoDB**
   - Run:
  
     ```shell
     sudo systemctl start mongod
     ```

   - For more details, visit the [MongoDB Installation Guide for Ubuntu](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-ubuntu/).

## Open MongoDB Shell

To open the MongoDB shell on a Windows machine, follow these steps:

1. **Open Command Prompt**:
   - Press `Win + R`, type `cmd`, and press `Enter`.

2. **Navigate to the MongoDB bin directory**:
   - Use the `cd` command to change the directory to where MongoDB is installed. For example:
  
     ```sh
     cd C:\Program Files\MongoDB\Server\<version>\bin
     ```

3. **Start the MongoDB shell**:
   - Run the following command:
  
     ```sh
     mongosh
     ```

This will open the MongoDB shell, and you can start interacting with your MongoDB instance.

### Expected Output

When you run the `mongosh` command, you should see output similar to the following:

```sh
Current Mongosh Log ID: 615a1b2e3f4b5c6d7e8f9g0h
Connecting to: mongodb://localhost:27017
Using MongoDB: 7.0.12
Using Mongosh: 2.3.1

For mongosh info see: https://docs.mongodb.com/mongodb-shell/

test>

```

## Shell vs Driver

### MongoDB Shell

The MongoDB Shell (`mongosh`) is an interactive JavaScript interface to MongoDB. It allows you to connect to a MongoDB instance, run queries, and perform administrative operations directly from the command line. It is primarily used for:

- Running ad-hoc queries
- Performing administrative tasks
- Interacting with the database in a REPL (Read-Eval-Print Loop) environment

### MongoDB Driver

A MongoDB Driver is a library that allows your application to connect to and interact with a MongoDB database programmatically. Drivers are available for various programming languages such as Python, Java, Node.js, and more. They are primarily used for:

- Integrating MongoDB with your application
- Performing database operations from within your application code
- Handling database connections and operations in a more structured and automated way

## Understanding Databases, Collections, and Documents

### Databases

In MongoDB, a database is a container for collections. Each database has its own set of files on the file system. A single MongoDB server can have multiple databases, each serving different applications or purposes.

### Collections

A collection is a group of MongoDB documents. It is the equivalent of a table in relational databases. Collections do not enforce a schema, meaning documents within a collection can have different fields. Collections are used to organize documents into logical groups.

### Documents

A document is a record in a MongoDB collection. It is a data structure composed of field and value pairs, similar to JSON objects. Documents are the basic unit of data in MongoDB and can contain nested documents and arrays. Each document has a unique identifier called `_id`.

### Example

Here is an example to illustrate the relationship between databases, collections, and documents:

- **Database**: `users`
  - **Collection**: `userData`
    - **Document**:
  
      ```json
      {
        "_id": "1",
        "name": "John Doe",
        "email": "john.doe@example.com",
        "age": 30
      }
      ```

In this example:

- `users` is the database.
- `userData` is a collection within `users`.
- The JSON object is a document within the `userData` collection.

Understanding these core concepts is essential for working effectively with MongoDB.

## Differences Between JSON and BSON Format

| Feature       | JSON                                             | BSON                                              |
| ------------- | ------------------------------------------------ | ------------------------------------------------- |
| Data Format   | Text-based (human-readable)                      | Binary format (machine-readable)                  |
| Size          | Larger due to text encoding                      | Smaller due to binary encoding                    |
| Speed         | Slower to parse and generate                     | Faster to parse and generate                      |
| Data Types    | Limited data types (e.g., string, number, array) | Richer data types (e.g., int, long, date, binary) |
| Use Case      | Data interchange format                          | Storage and network transfer in MongoDB           |
| Readability   | Easy to read and write                           | Not human-readable                                |
| Efficiency    | Less efficient for storage and transmission      | More efficient for storage and transmission       |
| Support       | Widely supported across various platforms        | Specifically designed for MongoDB                 |
| Compression   | No built-in compression                          | Supports built-in compression                     |
| Extensibility | Limited extensibility                            | Extensible with custom data types                 |

## Default Storage Engines Used by Different Databases

| Database             | Default Storage Engine                      |
| -------------------- | ------------------------------------------- |
| MongoDB              | WiredTiger                                  |
| MySQL                | InnoDB                                      |
| PostgreSQL           | PostgreSQL's own storage engine             |
| SQLite               | SQLite's own storage engine                 |
| MariaDB              | InnoDB (or Aria for certain configurations) |
| Microsoft SQL Server | SQL Server's own storage engine             |
| Oracle Database      | Oracle's own storage engine                 |

## 1. Creating Database and Collection

### Show All Databases

To list all databases in MongoDB, use `show` command in the MongoDB shell:

```sh
test> show dbs
```

Expected Output

```sh
admin   0.000GB
config  0.000GB
local   0.000GB
```

Note:

These are the default databases created by MongoDB:

- **admin:** Used for administrative purposes.
- **config:** Used internally by MongoDB for sharding.
- **local:** Used for storing data specific to a single server.

### Create Database

To create a new database in MongoDB, use `use` command in the MongoDB shell:

```sh
test> use users
```

after creating the database you'll switch to the new database but you won't be able to see the new database in all databases

```sh
admin   0.000GB
config  0.000GB
local   0.000GB
```

### Create a Collection

To create a collection in MongoDB, you can use the `db.createCollection()` method. make sure first switch to the Database
where you want to create the collection using `use` command

```javascript
users> db.createCollection("userData");
```

Expected Output:

```sh
{ ok: 1 }
```

Alternatively, you can create a collection implicitly by inserting a document into a non-existent collection.

## Create a Document

### insertOne Method

The `insertOne` method inserts a single document into a collection.

Syntax:

```javascript
db.collection.insertOne(documents, options)
```

- **documents:** The document to be inserted.
- **options:**  Additional options for the insert operation.

First, switch to the database where you want to create the document. If the database does not exist, MongoDB will create it for you.

Example:

```javascript
test> use users
```

then use the following command to create a document:

```javascript
users> db.userData.insertOne( {
  name: "John Doe",
  age: 30,
  email: "john.doe@example.com"
  })
```

Expected Output:

```sh
{
  acknowledged: true,
  insertedId: ObjectId('66e9b91d2af455ba16c73bf8')
}
```

- **acknowledged: true**: This indicates that the insert operation was acknowledged by the MongoDB server, meaning the server has successfully received and processed the request.
  
- **insertedId: ObjectId('66e9b91d2af455ba16c73bf8')**: This is the unique identifier (ObjectId) assigned to the newly inserted document. The ObjectId is a 12-byte identifier typically used by MongoDB to uniquely identify documents within a collection.

### insertMany Method

The `insertMany` method inserts multiple documents into a collection at once.

Syntax:

```javascript
db.collection.insertMany(documents, options)
```

- **documents:** An array of documents to be inserted.
- **options:**  Additional options for the insert operation.

Example:

```javascript
users> db.userData.insertMany([
  {
    name: "Jane Doe",
    age: 25,
    email: "jane.doe@example.com"
  },
  {
    name: "Alice Smith",
    age: 28,
    email: "alice.smith@example.com"
  },
  {
    name: "Bob Johnson",
    age: 35,
    email: "bob.johnson@example.com"
  }
])
```

Expected Output:

```sh
{
  "acknowledged": true,
  "insertedIds": [
    ObjectId("66e9b91d2af455ba16c73bf9"),
    ObjectId("66e9b91d2af455ba16c73bfa"),
    ObjectId("66e9b91d2af455ba16c73bfb")
  ]
}
```

### Create a Document with Custom `_Id`

In MongoDB, you can specify your own `_id` value when inserting a document. If you do not provide an `_id`, MongoDB will automatically generate one for you.

***Example:***

Suppose you want to create a document of hobbies.

```javascript
db.hobbies.insertMany([
  {
    _id : 'sports',
    name : 'Sports'
  },
  {
    _id : 'cooking',
    name : 'Cooking'
  },
  {
    _id : 'reading',
    name : 'Reading'
  },
])
```

***Expected Output:***

```javascript
{
  acknowledged: true,
  insertedIds: { '0': 'sports', '1': 'cooking', '2': 'reading' }
}
```

***lets check the collection:***

```javascript
hobby> db.hobbies.find()

[
  { _id: 'sports', name: 'Sports' },
  { _id: 'cooking', name: 'Cooking' },
  { _id: 'reading', name: 'Reading' }
]
```

***Note:*** Here we use `sports` as an `_id`  because we know that this will be unique, we will not have `sports` twice in this collection, so we can absolutely use sports as an `ID` here and the same  for `cooking` and `reading`.

### Ordered Inserts

If you try to insert a new document with an `_id` that already exists in the collection, MongoDB will throw a duplicate key error, and the insertion will fail. This is because the `_id` field must be unique for each document in a collection.

***Example:**

let add some new hobbies:

```javascript
db.hobbies.insertMany([
  {
    _id : 'coding',
    name : 'Coding'
  },
  {
    _id : 'cooking', // already exists in the document
    name : 'Cooking'
  },
  {
    _id : 'singing',
    name : 'Singing'
  },
])
```

***Expected Output:***

```javascript
Uncaught:
MongoBulkWriteError: E11000 duplicate key error collection: hobby.hobbies index: _id_ dup key: { _id: "Cooking" }
Result: BulkWriteResult {
  insertedCount: 1,
  matchedCount: 0,
  modifiedCount: 0,
  deletedCount: 0,
  upsertedCount: 0,
  upsertedIds: {},
  insertedIds: { '0': 'Coding' }
}
Write Errors: [
  WriteError {
    err: {
      index: 1,
      code: 11000,
      errmsg: 'E11000 duplicate key error collection: hobby.hobbies index: _id_ dup key: { _id: "Cooking" }',
      errInfo: undefined,
      op: { _id: 'Cooking', name: 'Cooking' }
    }
  }
]
```

***lets check our hobbies collection:***

```javascript
db.hobbies.find()
```

***Expected Output:***

```javascript
[
  { _id: 'Sports', name: 'Sports' },
  { _id: 'Cooking', name: 'Cooking' },
  { _id: 'Reading', name: 'Reading' },
  { _id: 'Coding', name: 'Coding' } // new element Added 
]
```

***Explanation:**

- It fails after `{ _id: 'Coding', name: 'Coding' }` element. This is the default behaviour of MongoDB.

- This is called an `Ordered insert` operation. inserts simply means that every element you insert is processed standalone.

- but if one fails, it cancels the entire insert operation. but it does not `rollback` the elements that is already inserted.
  
- Often you want that behaviour but sometimes you don't and for this you can override the behaviour.

### Unordered inserts
  
***let's Override***

***Example:***

```javascript
db.hobbies.insertMany(
  [
    {
      _id: "coding",
      name: "Coding",
    },
    {
      _id: "cooking",
      name: "Cooking",
    },
    {
      _id: "singing",
      name: "Singing",
    },
  ],
  {
    ordered: false,
  }
)
```

***Note:***

- When using `ordered : false`, MongoDB will continue to insert the remaining documents even if one or more documents cause an error (e.g., duplicate key error).
  
- By default the `ordered` option is set to `true`

***Expected Output:***

```javascript
Uncaught:
MongoBulkWriteError: E11000 duplicate key error collection: hobby.hobbies index: _id_ dup key: { _id: "Coding" }
Result: BulkWriteResult {
  insertedCount: 1,
  matchedCount: 0,
  modifiedCount: 0,
  deletedCount: 0,
  upsertedCount: 0,
  upsertedIds: {},
  insertedIds: { '2': 'Singing' }
}
Write Errors: [
  WriteError {
    err: {
      index: 0,
      code: 11000,
      errmsg: 'E11000 duplicate key error collection: hobby.hobbies index: _id_ dup key: { _id: "Coding" }',
      errInfo: undefined,
      op: { _id: 'coding', name: 'Coding' }
    }
  },
  WriteError {
    err: {
      index: 1,
      code: 11000,
      errmsg: 'E11000 duplicate key error collection: hobby.hobbies index: _id_ dup key: { _id: "Cooking" }',
      errInfo: undefined,
      op: { _id: 'cooking', name: 'Cooking' }
    }
  }
]
```

***Explanation:***

- If the `hobbies` collection already contains a document with `_id: "coding"` and `_id: "cooking"`, the insertion of the first and second document will fail due to a duplicate key error.
  
- However, because `ordered` is set to `false`, MongoDB will still attempt to insert the remaining documents.

***lets Check :***

```javascript
db.hobbies.find()
```

***Expected Output:***

```javascript
[
  { _id: 'Sports', name: 'Sports' },
  { _id: 'Cooking', name: 'Cooking' }, // already exists
  { _id: 'Reading', name: 'Reading' },
  { _id: 'Coding', name: 'Coding' }, // already exists
  { _id: 'Singing', name: 'Singing' } // new element Added
]
```

### Write Concern and Journaling in MongoDB

**Write Concern:**

Write concern in MongoDB specifies the level of acknowledgment requested from MongoDB for write operations. It allows you to control the trade-off between performance and durability.

**Levels of Write Concern:**

1. **w: 0** - No acknowledgment is requested from the server.

2. **w: 1** - Acknowledgment that the write operation has been written to the standalone mongod or the primary of a replica set.
  
3. **w: "majority"** - Acknowledgment that the write operation has been written to the majority of the nodes in the replica set.
  
4. **w: `<number>`** - Acknowledgment that the write operation has been written to a specified number of nodes.

**Journaling:**

Journaling is a feature that ensures data durability by recording write operations in a journal file before applying them to the database. This ensures that in the event of a crash or power failure, MongoDB can recover and restore the database to a consistent state.

**How Journaling Works:**

1. **Write Operation:** When a write operation (insert, update, delete) is performed, MongoDB writes the operation to the journal file.

2. **Journal Commit Interval:** MongoDB commits the journal file to disk at regular intervals (default is 100 milliseconds).

3. **Apply to Data Files:** After the journal file is committed, the write operation is applied to the database data files.

**Benefits of Journaling:**

- **Data Durability:** Ensures that write operations are not lost in case of a crash.

- **Crash Recovery:** Allows MongoDB to recover to a consistent state after a crash by replaying the journal files.

***Example:***

***Insert a document into the users collection with write concern and journaling***

```javascript
db.users.insertOne(
  { name: 'John Doe', age: 30 },
  { writeConcern: { w: "majority", j: true, wtimeout: 5000 } }
)
```

***Explanation:***

- The document `{ name: 'John Doe', age: 30 }` is inserted into the `users` collection.

- The write concern `{ w: "majority", j: true, wtimeout: 5000 }` ensures that the write operation is acknowledged only after it has been written to the majority of the nodes and the journal, within 5000 milliseconds (5 seconds).

**Summary:**

- **Write Concern:** Specifies the level of acknowledgment requested from MongoDB for write operations. In the example, `{ w: "majority", j: true, wtimeout: 5000 }` ensures the write is acknowledged by the majority of nodes and written to the journal within 5 seconds.

- **Journaling:** Ensures data durability by recording write operations in a journal file. This helps MongoDB recover to a consistent state in case of a crash.

### What is Atomictiy?

Atomicity refers to the concept that a series of operations within a transaction are treated as a single unit. This means that either all operations within the transaction are executed successfully, or none of them are. If any operation within the transaction fails, the entire transaction is rolled back, ensuring that the database remains in a consistent state.

**Atomicity in MongoDB:**

- In MongoDB, atomicity is guaranteed at the document level. This means that single-document operations (inserts, updates, and deletes) are atomic.
  
- For multi-document transactions, MongoDB provides support for transactions in replica sets and sharded clusters starting from version 4.0.
  
***Example:***

***Insert a Document***

```javascript
// Insert a document into the users collection
db.users.insertOne({ name: 'John Doe', age: 30 })
```

***Update the Document Atomically***

```javascript
// Update the user's name and age atomically
db.users.updateOne(
  { name: 'John Doe' }, // Filter
  { $set: { name: 'Jane Doe', age: 31 } } // Update
)
```

***Explanation:***

- The document `{ name: 'John Doe', age: 30 }` is inserted into the `users` collection.

- The `updateOne` operation updates the user's `name` to `'Jane Doe'` and `age` to `31` atomically. This means that both fields are updated together, and if the operation fails, neither field is updated.

***Summary***

Atomicity ensures that a series of operations within a transaction are treated as a single unit. In MongoDB, single-document operations are atomic by default, and multi-document transactions are supported in replica sets and sharded clusters starting from version 4.0. This guarantees that either all operations within the transaction are executed successfully, or none of them are, maintaining the consistency of the database.

## Read a Document

### find Method

The `find` method in MongoDB is used to query documents from a collection. It returns a cursor to the documents that match the query criteria.

Syntax:

```javascript
db.collection.find(query, projection)
```

- **query:** Specifies the selection criteria using query operators.
- **projection:** Specifies the fields to return in the documents that match the query criteria.

Show all documents use `find` without any query

Example:

```javascript
users> db.userData.find()
```

Expected Output:

```sh
[
  {
    _id: ObjectId('66ea6dbbadd143d6bfc73bf9'),
    name: 'Jane Doe',
    age: 25,
    email: 'jane.doe@example.com'
  },
  {
    _id: ObjectId('66ea6dbbadd143d6bfc73bfa'),
    name: 'Alice Smith',
    age: 28,
    email: 'alice.smith@example.com'
  },
  {
    _id: ObjectId('66ea6dbbadd143d6bfc73bfb'),
    name: 'Bob Johnson',
    age: 35,
    email: 'bob.johnson@example.com'
  }
]
```

- ***Note:*** By default, the `find()` method returns documents in a compact JSON format, which can be difficult to read, especially when dealing with documents that have many fields or nested structures.
- Using `pretty()` makes the output more human-readable by adding line breaks and indentation. This is particularly useful when you are inspecting documents directly in the MongoDB shell or when you want to present query results in documentation.
  
Syntax:

```javascript
users> db.userData.find().pretty()
```

### find Method with Query

To find all documents in the `userData` collection where the `age` is greater than 25.

Example:

```javascript
users> db.userData.find({ age: { $gt: 25 } })
```

Expected Output:

```sh
[
  {
    _id: ObjectId('66ea6dbbadd143d6bfc73bfa'),
    name: 'Alice Smith',
    age: 28,
    email: 'alice.smith@example.com'
  },
  {
    _id: ObjectId('66ea6dbbadd143d6bfc73bfb'),
    name: 'Bob Johnson',
    age: 35,
    email: 'bob.johnson@example.com'
  }
]
```

- ***Note:*** If the query does not match any documents in the collection, the `find()` method will return an empty result set or nothing.
  
Example:

```javascript
users> db.userData.find({name : 'Santosh'})
```

Expected Output:

```sh
[]
```

### find Method with Projection

To find all documents in the `userData` collection where the `age` is greater than 25, but only return the `name` and `age` fields.

Example:

```javascript
users> db.userData.find({ age: { $gt: 25 } }, { name: 1, age: 1, _id: 0 })
```

Expected Output:

```sh
[ 
  { name: 'Alice Smith', age: 28 },
  { name: 'Bob Johnson', age: 35 } 
]
```

This query will return all documents where the `age` field is greater than 25, but only include the `name` and `age` fields in the result, excluding the `_id` and `email` field.

### findOne Method with Query

The `findOne` method in MongoDB is used to retrieve a single document from a collection that matches the specified query criteria. If multiple documents match the query, it returns the first document according to the natural order of the documents in the collection.

Syntax:

```javascript
db.collection.findOne(query, projection)
```

- **query** Specifies the selection criteria using query operators.
- **projection** Specifies the fields to return in the document that matches the query criteria.

***Example:***

To find a single document in the `userData` collection where the `name` is `"Alice Smith"`:

```javascript
users> db.userData.findOne({ name: "Alice Smith" })
```

Expected Output:

```sh
{
  _id: ObjectId('66ea6dbbadd143d6bfc73bfa'),
  name: 'Alice Smith',
  age: 28,
  email: 'alice.smith@example.com'
}
```

- ***Note:*** 💡 MongoDB queries are case-sensitive by default.
- for example if you change `'Smith'` to `'smith'` in your query then you'll get `null` as an output.

Example:

```javascript
users> db.userData.findOne({ name: "Alice smith" })
```

Expected Output:

```sh
null
```

This indicates that no documents in the `userData` collection match the query criteria because `"smith"` does not match `"Smith"`.

***With Regular Expression***

If you want to perform a case-insensitive search, you can use a `regular expression` with the `i` option for case insensitivity:

Example:

```javascript
users> db.userData.findOne({ name: { $regex: /^Alice smith$/i } })
```

Expected Output:

```sh
{
  _id: ObjectId('66ea6dbbadd143d6bfc73bfa'),
  name: 'Alice Smith',
  age: 28,
  email: 'alice.smith@example.com'
}
```

This query will match `"Alice Smith"` regardless of the case of `"Smith"`.

### findOne Method with Projection

To find a single document in the `userData` collection where the `name` is `"Alice Smith"`, but only return the `name` and `age` fields.

```javascript
users> db.userData.findOne({ name: "Alice Smith" }, { name: 1, age: 1, _id: 0 })
```

Expected Output:

```sh
{
  "name": "Alice Smith",
  "age": 28
}
```

### find Method and Cursor Object

The `find()` method returns a `cursor` object, which is a pointer to the result set of the query. The cursor allows you to iterate over the documents one by one.

***Common Cursor Methods:***

- **forEach():** Iterates over each document in the cursor.
- **toArray():** Converts the cursor to an array of documents.
- **next():** Retrieves the next document in the cursor.
- **hasNext():** Checks if there are more documents in the cursor.
  
Example:

***lets create a new database called ninja and a collection name ninjas***

```javascript
test> use ninja // create a new database and switch into it
```

***Create new collection name ninjas and add some data 👇🏻***
<details>

  <summary>Click to expand the Command</summary>

  ```javascript
  ninja> db.ninjas.insertMany([
    {
      "name": "Naruto Uzumaki",
      "age": 30
    },
    {
      "name": "Neji Hyuga",
      "age": 27
    },
    {
      "name": "Uchiha Sasuke",
      "age": 35
    },
    {
      "name": "Kakshi Hatake",
      "age": 28
    },
    {
      "name": "Madara Uchiha",
      "age": 30
    },
    {
      "name": "Minato Namikaze",
      "age": 27
    },
    {
      "name": "Kushina Uzumaki",
      "age": 26
    },
    {
      "name": "Hinata Hyuga",
      "age": 25
    },
    {
      "name": "Sakura Haruno",
      "age": 29
    },
    {
      "name": "Hashirama Senju",
      "age": 41
    },
    {
      "name": "Tsunade Senju",
      "age": 48
    },
    {
      "name": "Jiraiya",
      "age": 39
    },
    {
      "name": "Orochimaru",
      "age": 22
    },
    {
      "name": "Kabuto Yakushi",
      "age": 44
    },
    {
      "name": "Itachi Uchiha",
      "age": 41
    },
    {
      "name": "Shisui Uchiha",
      "age": 35
    },
    {
      "name": "Kisame Hoshigaki",
      "age": 27
    },
    {
      "name": "Deidara",
      "age": 35
    },
    {
      "name": "Sasori",
      "age": 53
    },
    {
      "name": "Hidan",
      "age": 68
    },
    {
      "name": "Kakuzu",
      "age": 38
    }
  ])
  ```

  </details>

***let see all the docments from ninjas collection***

```javascript
ninja> db.ninjas.find()
```

Expected Output:

<details>
<summary>Click to expand the Output</summary>

```javascript
[
  {
    _id: ObjectId('66eafaad654ecb3e79c73c0d'),
    name: 'Naruto Uzumaki',
    age: 30
  },
  {
    _id: ObjectId('66eafaad654ecb3e79c73c0e'),
    name: 'Neji Hyuga',
    age: 27
  },
  {
    _id: ObjectId('66eafaad654ecb3e79c73c0f'),
    name: 'Uchiha Sasuke',
    age: 35
  },
  {
    _id: ObjectId('66eafaad654ecb3e79c73c10'),
    name: 'Kakshi Hatake',
    age: 28
  },
  {
    _id: ObjectId('66eafaad654ecb3e79c73c11'),
    name: 'Madara Uchiha',
    age: 30
  },
  {
    _id: ObjectId('66eafaad654ecb3e79c73c12'),
    name: 'Minato Namikaze',
    age: 27
  },
  {
    _id: ObjectId('66eafaad654ecb3e79c73c13'),
    name: 'Kushina Uzumaki',
    age: 26
  },
  {
    _id: ObjectId('66eafaad654ecb3e79c73c14'),
    name: 'Hinata Hyuga',
    age: 25
  },
  {
    _id: ObjectId('66eafaad654ecb3e79c73c15'),
    name: 'Sakura Haruno',
    age: 29
  },
  {
    _id: ObjectId('66eafaad654ecb3e79c73c16'),
    name: 'Hashirama Senju',
    age: 41
  },
  {
    _id: ObjectId('66eafaad654ecb3e79c73c17'),
    name: 'Tsunade Senju',
    age: 48
  },
  {
    _id: ObjectId('66eafaad654ecb3e79c73c18'),
    name: 'Jiraiya',
    age: 39
  },
  {
    _id: ObjectId('66eafaad654ecb3e79c73c19'),
    name: 'Orochimaru',
    age: 22
  },
  {
    _id: ObjectId('66eafaad654ecb3e79c73c1a'),
    name: 'Kabuto Yakushi',
    age: 44
  },
  {
    _id: ObjectId('66eafaad654ecb3e79c73c1b'),
    name: 'Itachi Uchiha',
    age: 41
  },
  {
    _id: ObjectId('66eafaad654ecb3e79c73c1c'),
    name: 'Shisui Uchiha',
    age: 35
  },
  {
    _id: ObjectId('66eafaad654ecb3e79c73c1d'),
    name: 'Kisame Hoshigaki',
    age: 27
  },
  {
    _id: ObjectId('66eafaad654ecb3e79c73c1e'),
    name: 'Deidara',
    age: 35
  },
  {
    _id: ObjectId('66eafaad654ecb3e79c73c1f'),
    name: 'Sasori',
    age: 53
  },
  { _id: ObjectId('66eafaad654ecb3e79c73c20'), name: 'Hidan', age: 68 }
]
Type "it" for more
```

after enter `it` you'll see

```javascript
[
  {
    _id: ObjectId('66eafaad654ecb3e79c73c21'),
    name: 'Kakuzu',
    age: 38
  }
]
```

</details>

- ***Note:*** The `it` command is a feature shown in the shell. lets say we have 1 million documents then it would take long time most importantly it would send a lots of data over the wire.
  
- so instead of that, it gives us back `cursor` object which is an object with a lot of metadata behind it that allows us to cycle through the results and that is what that `it` command did.
  
- `it` basically used that cursor to fetch the next bunch of data.
  
***Use toArray() method***

```javascript
ninja> db.ninjas.find().toArray()
```

If you execute the above command you'll see all the data without `it`

***Use forEach() method***

Example:

```javascript
ninja> const cursor = db.ninjas.find({ age: { $gt: 45 } });

cursor.forEach(doc => {
    printjson(doc);
});
```

***Or***

```javascript
ninja> db.ninjas.find({ age: { $gt: 45 } }).forEach((ninja) => {
    printjson(ninja);
});
```

This example retrieves documents from the `ninjas` collection where the `age` field is greater than 45 and prints each document.

Expected Output:

```sh
{
  _id: ObjectId('66eafaad654ecb3e79c73c17'),
  name: 'Tsunade Senju',
  age: 48
}
{
  _id: ObjectId('66eafaad654ecb3e79c73c1f'),
  name: 'Sasori',
  age: 53
}
{
  _id: ObjectId('66eafaad654ecb3e79c73c20'),
  name: 'Hidan',
  age: 68
}
```

- ***Note:*** Cursor is generally more efficient and flexible, especially when dealing with large datasets. It allows for better memory management, lazy evaluation, and more control over the query execution process.

- Cursors provide methods to control the execution of the query, such as sort(), limit(), and skip(), allowing for more flexible and efficient data retrieval.

## Update a Document

### updateOne Method

The `updateOne` method in MongoDB is used to update a single document that matches the specified filter criteria. If multiple documents match the filter, only the first matching document will be updated.

Syntax:

```javascript
db.collection.updateOne(filter, update, options)
```

- **filter:** Specifies the selection criteria for the document to update.
- **update:** Specifies the modifications to apply.
- **options:** Optional. Additional options for the update operation.

Example:

```javascript
users> db.userData.updateOne(
  { name: "Alice Smith" }, // filter
  { $set: { age: 29 } }    // update
)
```

in this example:

- `{ name: "Alice Smith" }` is the filter criteria to find the document.
- `{ $set: { age: 29 } }` is the update operation that sets the age field to 29.
- The `$set` operator in MongoDB is used to update the value of a field in a document without affecting other fields.

Expected Output:

```sh
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 1,
  modifiedCount: 1,
  upsertedCount: 0
}
```

- ***Note:*** you can update a document using any filter criteria, including the document's `_id` or other fields.

Example:

```javascript
users> db.userData.updateOne(
  { _id: ObjectId("60c72b2f9af1f2d9d8e8b456") }, // filter by _id
  { $set: { age: 30 } }                         // update
)
```

Expected Output:

```sh
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 1,
  modifiedCount: 1,
  upsertedCount: 0
}
```

### updateMany Method

The `updateMany` method in MongoDB is used to update multiple documents that match the specified filter criteria. Unlike `updateOne`, which updates only the first matching document, `updateMany` updates all documents that match the filter.

Syntax:

```javascript
db.collection.updateMany(filter, update, options)
```

- **filter:** Specifies the selection criteria for the documents to update.
- **update:** Specifies the modifications to apply.
- **options:** Optional. Additional options for the update operation.

**Suppose you want to `update` all documents in the collection:**

Example:

```javascript
users> db.userData.updateMany(
  {}, // filter to match all documents
  { $set: { city: "New York" } } // update to add the city field
)
```

Expected Output:

```sh
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 3,
  modifiedCount: 3,
  upsertedCount: 0
}
```

Now if you want to check whether the `city` field has been updated or not, you can use following command

```javascript
users> db.userData.find()
```

Expected Output:

```sh
[
  {
    _id: ObjectId('66ea6dbbadd143d6bfc73bf9'),
    name: 'Jane Doe',
    age: 30,
    email: 'jane.doe@example.com',
    city: 'New York'
  },
  {
    _id: ObjectId('66ea6dbbadd143d6bfc73bfa'),
    name: 'Alice Smith',
    age: 29,
    email: 'alice.smith@example.com',
    city: 'New York'
  },
  {
    _id: ObjectId('66ea6dbbadd143d6bfc73bfb'),
    name: 'Bob Johnson',
    age: 35,
    email: 'bob.johnson@example.com',
    city: 'New York'
  }
]
```

- ***Note:*** If you want to add certain field to all documents, you can use an empty filter `{}` to match all documents.

**Suppose you want to `update` a single document.**

Example:

```javascript
users> db.users.updateMany(
  { city: "New York" }, // filter
  { $set: { age: 30 } } // update
)
```

Expected Output:

```sh
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 3,
  modifiedCount: 3,
  upsertedCount: 0
}
```

## Delete a Document

### deleteOne Method

The `deleteOne` method in MongoDB is used to delete a single document that matches the specified filter criteria. If multiple documents match the filter, only the first matching document will be deleted.

Syntax:

```javascript
db.collection.deleteOne(filter, options)
```

- **filter:** Specifies the selection criteria for the document to delete.
- **options:** Optional. Additional options for the delete operation.

Example:

```javascript
users> db.userData.deleteOne({ name: "Alice Smith" })
```

Expected Output:

```sh
{
  acknowledged: true,
  deletedCount: 1
}
```

***Check if document successfully deleted from collection***

```javascript
users> db.userData.find()
```

Expected Output:

```sh
[
    {
    _id: ObjectId('66ea6dbbadd143d6bfc73bf9'),
    name: 'Jane Doe',
    age: 20,
    email: 'jane.doe@example.com',
    city: 'New York'
  },
  {
    _id: ObjectId('66ea6dbbadd143d6bfc73bfb'),
    name: 'Bob Johnson',
    age: 20,
    email: 'bob.johnson@example.com',
    city: 'New York'
  },
]
```

***Suppose you want to delete a document `name : 'Jane Doe'` from the collection with mismatch filter criteria. lets see what happens***

Example:

```javascript
users> db.userData.deleteOne({ name: "jane doe" }) // name in lower-case
```

Expected Output:

```sh
{
  acknowledged: true,
  deletedCount: 0
}
```

- **acknowledged:** This field indicates whether the delete operation was acknowledged by the MongoDB server. A value of true means that the server has acknowledged the request.
  
- **deletedCount:** This field indicates the number of documents that were deleted as a result of the operation. A value of 0 means that no documents matched the filter criteria, so no documents were deleted.

***Check whether the specified document has been deleted from the collection or not.***

```javascript
users> db.userData.find()
```

Expected Output:

```sh
[
    {
    _id: ObjectId('66ea6dbbadd143d6bfc73bf9'),
    name: 'Jane Doe',
    age: 20,
    email: 'jane.doe@example.com',
    city: 'New York'
  },
  {
    _id: ObjectId('66ea6dbbadd143d6bfc73bfb'),
    name: 'Bob Johnson',
    age: 20,
    email: 'bob.johnson@example.com',
    city: 'New York'
  },
]
```

Document with field `name : 'Jane Doe'` still exists in the collection!

### deleteMany Method

The `deleteMany` method in MongoDB is used to delete multiple documents that match the specified filter criteria.

Syntax:

```javascript
db.collection.deleteMany(filter, options)
```

- **filter:** Specifies the selection criteria for the document to delete.
- **options:** Optional. Additional options for the delete operation.

Example:
To delete all documents where the city is `"New York"`:

```javascript
users> db.userData.deleteMany({ city: "New York" })
```

Expected Output:

```sh
{
  acknowledged: true,
  deletedCount: 3
}
```

***Check whether all the documents with field `city : 'New York'` has been deleted from the collection or not.***

```javascript
users> db.userData.find()
```

Expected Output:

```sh
you'll see nothing in output.
```

## Embedded Documents and Arrays

Embedded documents in MongoDB are a way to store related data within a single document structure. This is useful for representing complex data relationships and can improve read performance by reducing the need for joins or multiple queries.

**Key Points:**

- **Structure:** Embedded documents are nested within a parent document.

- **Atomicity:**  Updates to a single document, including its embedded documents, are atomic.

- **Schema Design:** Useful for one-to-many relationships where the "many" side is not too large.

**Benefits:**

- **Performance:** Faster read operations since related data is stored together.
  
- **Atomic Updates:** Changes to the document, including embedded documents, are atomic.

- **Simplified Queries:**  Easier to query related data without needing joins.

**Considerations:**

- **Document Size:** MongoDB documents have a size limit of 16MB.

- **Data Duplication:**  Embedding can lead to data duplication if not designed carefully.

### Embedded Document

An embedded document in MongoDB is a document that is nested within another document. This is useful for representing complex data structures.

Example:

Consider a `userData` collection where each `user` has a profile embedded within the `user` document.

```javascript
users> db.userData.updateMany({} ,
 {$set : {profile :{city : 'Somewhere in the world' , pet :'cat'}}})
```

Expected Output:

```sh
[
  {
    _id: ObjectId('66eaf00854470240e2c73bff'),
    name: 'Jane Doe',
    age: 25,
    email: 'jane.doe@example.com',
    profile: {
      city: 'Somewhere in the world',
      pet : 'cat'
    }
  },
  {
    _id: ObjectId('66eaf00854470240e2c73c00'),
    name: 'Alice Smith',
    age: 28,
    email: 'alice.smith@example.com',
    profile: {
      city: 'Somewhere in the world',
      pet : 'cat'
    }
  },
  {
    _id: ObjectId('66eaf00854470240e2c73c01'),
    name: 'Bob Johnson',
    age: 35,
    email: 'bob.johnson@example.com',
    profile: {
      city: 'Somewhere in the world',
      pet : 'cat'
    }
  }
]
```

### Arrays of Data

Arrays in MongoDB are used to store multiple values in a single field. This is useful for representing lists of related data.

Example:

Consider a `userData` collection where each user has multiple addresses stored in an array.

```javascript
users> db.userData.insertOne({name : 'John Doe' , age : 27 , 
       email : 'johndoe@mail.com' , 
       addresses: 
       [
         {
           street: "123 Main St",
           city: "New York",
           state: "NY",
           zip: "10001"
         },
         {
          street: "456 Elm St",
          city: "Boston"
          state: "MA",
          zip: "02110"
         }
       ]
})
```

Expected Output:

```sh
 {
    _id: ObjectId('66eb1a25654ecb3e79c73c22'),
    name: 'John Doe',
    age: 27,
    email: 'johndoe@mail.com',
    addresses: [
      {
        street: '123 Main St',
        city: 'New York',
        state: 'NY',
        zip: '10001'
      },
      {
        street: '456 Elm St',
        city: 'Boston',
        state: 'MA',
        zip: '02110'
      }
    ]
  }
```

Summary:

- **Embedded Document:** A single nested document within a parent document.
- **Array of Data:** A field that contains multiple values, each of which can be a simple value or a complex document.

## Accessing Structured Data

### Query Objects

**If document looks like this** 👇🏻

```javascript
[
  {
    _id: ObjectId('66eaf00854470240e2c73bff'),
    name: 'Jane Doe',
    age: 25,
    email: 'jane.doe@example.com',
    profile: {
      city: 'Somewhere in the world',
      pet : 'cat'
    }
  },
  {
    _id: ObjectId('66eaf00854470240e2c73c00'),
    name: 'Alice Smith',
    age: 28,
    email: 'alice.smith@example.com',
    profile: {
      city: 'Somewhere in the world',
      pet : 'dog'
    }
  },
  {
    _id: ObjectId('66eaf00854470240e2c73c01'),
    name: 'Bob Johnson',
    age: 35,
    email: 'bob.johnson@example.com',
    profile: {
      city: 'Somewhere in the world',
      pet : 'tiger'
    }
  }
]
```

***We should use the following command:***

```javascript
db.collection.find({ // replace 'collection' with the name of your collection
  'profile.pet': 'cat'
})
```

***Note:*** when you are using `.` notation make sure to wrap the entire term with quotation mark.

Expected Output:

```sh
{
    _id: ObjectId('66eaf00854470240e2c73bff'),
    name: 'Jane Doe',
    age: 25,
    email: 'jane.doe@example.com',
    profile: {
      city: 'Somewhere in the world',
      pet : 'cat'
    }
  }
```

### Query Arrays

**If document looks like this:** 👇🏻

```javascript
[
  {
    _id: ObjectId('66eaf00854470240e2c73bff'),
    name: 'Jane Doe',
    age: 25,
    email: 'jane.doe@example.com',
    hobbies: ["Sports" , "Cooking" , "Reading"]
  },
  {
    _id: ObjectId('66eaf00854470240e2c73c00'),
    name: 'Alice Smith',
    age: 28,
    email: 'alice.smith@example.com',
    hobbies: ["Reading" , "Coding" , "Dancing"]
  },
  {
    _id: ObjectId('66eaf00854470240e2c73c01'),
    name: 'Bob Johnson',
    age: 35,
    email: 'bob.johnson@example.com',
    hobbies: ["Sports" , "Painting" , "Dancing"]
  },
]
```

***We should use the following command:***

```javascript
db.collection.find({ // replace 'collection' with the name of your collection
  hobbies: "Sports"
})
```

Expected Output:

```sh
{
    _id: ObjectId('66eaf00854470240e2c73bff'),
    name: 'Jane Doe',
    age: 25,
    email: 'jane.doe@example.com',
    hobbies: ["Sports" , "Cooking" , "Reading"]
  },
   {
    _id: ObjectId('66eaf00854470240e2c73c01'),
    name: 'Bob Johnson',
    age: 35,
    email: 'bob.johnson@example.com',
    hobbies: ["Sports" , "Painting" , "Dancing"]
  },
```

### Query Array of Objects

**If document looks like this:** 👇🏻

```javascript
[
 {
    _id: ObjectId('66eb1a25654ecb3e79c73c22'),
    name: 'John Doe',
    age: 27,
    email: 'johndoe@mail.com',
    addresses: [
      {
        street: '123 Main St',
        city: 'New York',
        state: 'NY',
        zip: '10001'
      }
    ]
  },
 {
    _id: ObjectId('68eb1a25654ecb3e79c73c29'),
    name: 'Jane Doe',
    age: 20,
    email: 'janedoe@mail.com',
    addresses: [
      {
        street: '456 Elm St',
        city: 'Boston',
        state: 'MA',
        zip: '02110'
      }
    ]
  }
]  
```

***We should use the following command:***

```javascript
db.collection.find({ //  // replace 'collection' with the name of your collection
  addresses: {
    $elemMatch: {
      street: '456 Elm St'
    }
  }
})
```

***Note:*** The `$elemMatch` operator in MongoDB is used to match documents that contain an array field with at least one element that matches all the specified query criteria. It is particularly useful when you need to query nested arrays or when you need to apply multiple conditions to elements within an array.

Explanation:

- **addresses:** Specifies the array field to search within.

- **$elemMatch:** Ensures that at least one element in the `addresses` array matches the specified criteria.

- **{ street: '456 Elm St' }:** The criteria that the element in the array must match.

Expected Output:

```sh
{
    _id: ObjectId('68eb1a25654ecb3e79c73c29'),
    name: 'Jane Doe',
    age: 20,
    email: 'janedoe@mail.com',
    addresses: [
      {
        street: '456 Elm St',
        city: 'Boston',
        state: 'MA',
        zip: '02110'
      }
    ]
  }
```

## Resetting Database

***Check all database:***

```javascript
test> show dbs
```

### Delete a Database

```javascript
use your_database_name // switch to desired database replace your_database_name with actual database name
db.dropDatabase()
```

Expected Output:

```sh
{ ok: 1, dropped: 'your_database_name' }
```

***Check if a database has a collection or not:***

```javascript
use your_database_name // replace your_database_name with actual database name
db.getCollectionNames()
```

Expected Output:

```sh
['userData']
```

***Check if a database has a specific collection or not:***

```javascript
use your_database_name // replace your_database_name with actual database name
db.getCollectionNames().include('your_collection_name') // replace your_collection_name with actual collection name
```

Expected Output:

```sh
true
```

***Note:***  `true` if the collection exists and `false` if it does not.

### Delete a Collection

```javascript
use your_database_name //  replace your_database_name with actual database name
db.your_collection_name.drop() // replace your_collection_name with actual collection name
```

Expected Output:

```sh
true
```

### Delete a Specific Document

```javascript
use your_database_name //  replace your_database_name with actual database name
db.your_collection_name.deleteOne({ your_query }) // replace your_collection_name with actual collection name
```

Expected Output:

```sh
{ acknowledged: true, deletedCount: 1 }
```

### Delete all Documents

Suppose you have 5 documents are there in a collection

```javascript
use your_database_name  //  replace your_database_name with actual database name
db.your_collection_name.deleteMany({})  // replace your_collection_name with actual collection name
```

Expected Output:

```sh
{ acknowledged: true, deletedCount: 5 }
```

### Statistics about the Database

The `db.stats()` command in MongoDB provides statistics about the database. It returns an overview of the database's storage and usage, including information such as the number of collections, the size of the data, the storage size, and more.

Example:

```javascript
db.stats()
```

Expected Output:

```javascript
{
  "db": "myDatabase",
  "collections": 5,
  "views": 0,
  "objects": 1000,
  "avgObjSize": 45.6,
  "dataSize": 45600,
  "storageSize": 81920,
  "numExtents": 0,
  "indexes": 10,
  "indexSize": 16384,
  "scaleFactor": 1,
  "fsUsedSize": 104857600,
  "fsTotalSize": 2147483648,
  "ok": 1
}
```

***Key Fields:***

- **db:** The name of the database.
- **collections:** The number of collections in the database.
- **views:** The number of views in the database.
- **object:** The number of documents in the database.
- **avgObjSize:** The average size of each document.
- **dataSize:** The total size of the data in the database.
- **storageSize:** The total amount of storage allocated for the database.
- **indexes:** The number of indexes in the database.
- **indexSize:** The total size of all indexes.
- **fsUsedSize:** The amount of filesystem space used by the database.
- **fsTotalSize:** The total amount of filesystem space available.
- **ok:**  Indicates if the command was successful (1 for success).

## 2. Schemas and Relations

### Why do we use Schemas?

Using `schemas` helps maintain a consistent and reliable data structure, making your application more robust and easier to manage.

### Structuring Documents

1. **Use Schemas (Even in a Schema-less Database)**
   - **Consistency**: Use libraries like Mongoose to define schemas at the application level, ensuring consistent data structure.
   - **Validation**: Enforce data types, required fields, and constraints to maintain data integrity.

2. **Embed Data When Appropriate**
   - **Related Data**: Embed related data within a single document if it is frequently accessed together. This can improve read performance.
   - **Example**: Store user profile information and their addresses in the same document.

3. **Reference Data When Necessary**
   - **Normalization**: Use references for data that is accessed independently or has a many-to-many relationship. This helps avoid data duplication.
   - **Example**: Store user IDs in an orders collection to reference user details stored in a separate users collection.

4. **Optimize for Read and Write Patterns**
   - **Access Patterns**: Design your schema based on how your application reads and writes data. Optimize for the most common queries.
   - **Example**: If you frequently need to access user posts, consider embedding posts within the user document.

5. **Use Indexes**
   - **Performance**: Create indexes on fields that are frequently queried to improve read performance.
   - **Example**: Index the `email` field in a users collection to speed up user lookups by email.

6. **Avoid Deeply Nested Documents**
   - **Complexity**: Limit the depth of nested documents to avoid complexity and performance issues.
   - **Example**: Instead of deeply nesting comments within posts, consider a separate comments collection with references to post IDs.

7. **Consider Document Size**
   - **Limits**: Be aware of MongoDB's document size limit (16MB). Design your schema to avoid exceeding this limit.
   - **Example**: For large datasets, consider splitting data into multiple documents or collections.
  
8. **Use Appropriate Data Types**
   - **Efficiency**: Use the most appropriate data types for your fields to optimize storage and performance.
   - **Example**: Use `Date` for timestamps, `Number` for numerical values, and `String` for text.
  
```javascript
 {
    name: "Jane Doe",
    email: "jane.doe@example.com",
    age: 25,
    createdAt: new Date()
  },
  {
    name: "Alice Smith",
    email: "alice.smith@example.com",
    age: 28,
    createdAt: new Date()
  }
```

### Data Types

MongoDB supports various data types, including:

1. **String:** Used to store text data. Strings must be UTF-8 valid.

   ```javascript
    { "name": "John Doe" }
   ```

2. **Integer:** Used to store numerical values. MongoDB provides both 32-bit and 64-bit integers.

   ```javascript
   { "age": 30 }
   ```  

3. **Boolean:** Used to store a boolean (true/false) value.

   ```javascript
   { "isActive": true }
   ```  

4. **Double:** Used to store floating-point values.

   ```javascript
   { "height": 5.9 }
   ```

5. **Min/Max Keys:** Used to compare a value against the lowest and highest BSON elements.

   ```javascript
   { "minKey": { "$minKey": 1 }, "maxKey": { "$maxKey": 1 } }
   ```

6. **Arrays:** Used to store arrays or lists of values.

   ```javascript
   { "tags": ["mongodb", "database", "NoSQL"] }
   ```

7. **Timestamp:** Used to store a specific point in time.

   ```javascript
   { "createdAt": { "$timestamp": { "t": 1627847267, "i": 1 } } }
   ```

8. **Object:** Used to store embedded documents.

   ```javascript
   { "address": { "street": "123 Main St", "city": "Anytown" } }
   ```

9. **Null:** Used to store a null value.

   ```javascript
   { "middleName": null }
   ```

10. **Symbol:** Generally used for languages that support a specific symbol type.

    ```javascript
    { "symbol": { "$symbol": "symbolValue" } }
    ```

11. **Date:** Used to store the current date or time in UNIX time format.

    ```javascript
    { "birthdate": { "$date": "1990-01-01T00:00:00Z" } }
    ```

12. **Object ID:** Used to store the document’s ID.

    ```javascript
    { "_id": { "$oid": "507f1f77bcf86cd799439011" } }
    ```

13. **Binary Data:** Used to store binary data.

    ```javascript
    { "binaryData": { "$binary": { "base64": "aGVsbG8gd29ybGQ=", "subType": "00" } } }
    ```

14. **Code:** Used to store JavaScript code for execution on the server.

    ```javascript
    { "code": { "$code": "function() { return 'Hello, world!'; }" } }
    ```

15. **Regular Expression:** Used to store regular expressions.
  
    ```javascript
    { "regex": { "$regex": "pattern", "$options": "i" } }
    ```

16. **Decimal128:** Used to store high-precision decimal values.
  
    ```javascript
    { "decimalValue": { "$numberDecimal": "9.99" } }
    ```

17. **JavaScript (with scope):** Used to store JavaScript code that includes a scope.
  
    ```javascript
    { "codeWithScope": { "$code": "function() { return x; }", "$scope": { "x": 1 } } }
    ```

## Understanding Relations

In MongoDB, relationships between data can be represented in two main ways: `embedding` and `referencing`.

1. **Embedding:** This involves storing related data within a single document. This is useful when you have a one-to-few relationship and the related data is not expected to grow indefinitely.

2. **Referencing:** This involves storing related data in separate documents and linking them using references. This is useful for one-to-many or many-to-many relationships where the related data can grow significantly.

### One-to-One Relationship - Embedding

**Example:**

***Consider a scenario where each user has one profile.***

```javascript
{
  "_id": ObjectId("507f1f77bcf86cd799439011"),
  "name": "John Doe",
  "email": "john.doe@example.com",
  "profile": {
    "age": 30,
    "address": "123 Main St"
  }
}
```

**Advantages:**

- **Performance:** Faster read operations since all related data is in a single document.

- **Atomicity:** Updates to the document are atomic.
  
**Disadvantages:**

- **Document Size:** If the embedded document grows too large, it can exceed the BSON document size limit (16MB).

- **Duplication:** If the embedded data is used in multiple places, it can lead to data duplication.
  
### One-to-One Relationship - Referencing

***Note:*** Referencing involves storing related data in separate documents and linking them using references. This is useful for `one-to-one`, `one-to-many`, or `many-to-many` relationships where the related data can grow significantly.

**Example:**

***Consider the same scenario where each user has one profile, but stored in separate collections.***

**User Document:**

```javascript
{
  "_id": ObjectId("507f1f77bcf86cd799439011"),
  "name": "John Doe",
  "email": "john.doe@example.com",
  "profile_id": ObjectId("507f191e810c19729de860ea")
}
```

**Profile Document:**

```javascript
{
  "_id": ObjectId("507f191e810c19729de860ea"),
  "age": 30,
  "address": "123 Main St"
}
```

***Explanation:***

- The `user` document contains a reference to the `profile` document using the `profile_id` field.
  
- The `profile_id` field in the `user` document references the `_id` field in the profile document, establishing a one-to-one relationship between the two collections.

**Advantages:**

- **Flexibility:** Easier to manage and update large or frequently changing data.
  
- **Normalization:** Reduces data duplication.
  
**Disadvantages:**

- **Performance:** Requires additional queries to fetch related data, which can slow down read operations.
  
- **Complexity:** More complex to manage and maintain relationships between documents.

**Summary:**

- **Embedding** is suitable for small, tightly coupled data that doesn't change frequently.
  
- **Referencing** is better for large, loosely coupled data that changes frequently or is shared across multiple documents.
  
### One-to-Many Relationship - Embedding

**Example:**

***Consider a scenario where a blog post has multiple comments. Each post can have many comments, and embedding the comments within the post document is a good approach.***

```javascript
{
  "_id": ObjectId("507f1f77bcf86cd799439011"),
  "title": "My Blog Post",
  "content": "This is the content of the blog post.",
  "comments": [
    {
      "author": "John Doe",
      "comment": "Great post!"
    },
    {
      "author": "Jane Smith",
      "comment": "Thanks for sharing."
    }
  ]
}
```

### One-to-Many Relationship - Referencing

**Example:**

***Consider a scenario where a blog post has multiple comments, but stored in separate collections.***

**Post Document:**

```javascript
{
  "_id": ObjectId("507f1f77bcf86cd799439011"),
  "title": "My Blog Post",
  "content": "This is the content of the blog post."
}
```

**Comment Document:**

```javascript
{
  "_id": ObjectId("507f191e810c19729de860ea"),
  "post_id": ObjectId("507f1f77bcf86cd799439011"),
  "author": "John Doe",
  "comment": "Great post!"
}
```

***Explanation:***

- The `comment` document contains a reference to the `post` document using the `post_id` field.
  
- The `post_id` field in the comment document references the `_id` field in the `post` document, establishing a one-to-many relationship between the two collections.

### Many-to-Many Relationship - Embedding

**Example:**

***Consider a scenario where students can enroll in multiple courses, and each course can have multiple students. Embedding this relationship can be complex and is generally not recommended, but for simplicity, let's consider embedding student references within the course document.***

**Course Document:**

```javascript
{
  "_id": ObjectId("507f1f77bcf86cd799439011"),
  "course_name": "Database Systems",
  "students": [
    {
      "_id": ObjectId("507f191e810c19729de860ea"),
      "name": "John Doe"
    },
    {
      "_id": ObjectId("507f191e810c19729de860eb"),
      "name": "Jane Smith"
    }
  ]
}
```

### Many-to-Many Relationship - Referencing

**Example:**

***Consider the same scenario where students can enroll in multiple courses, but stored in separate collections with a linking collection.***

**Student Document:**

```javascript
{
  "_id": ObjectId("507f191e810c19729de860ea"),
  "name": "John Doe"
}
```

**Course Document:**

```javascript
{
  "_id": ObjectId("507f1f77bcf86cd799439011"),
  "course_name": "Database Systems"
}
```

**Enrollment Document (Linking Collection):**

```javascript
{
  "_id": ObjectId("507f191e810c19729de860ec"),
  "student_id": ObjectId("507f191e810c19729de860ea"),
  "course_id": ObjectId("507f1f77bcf86cd799439011")
}
```

***Explanation:***

- The `enrollment` document contains references to both the `student` and `course` documents using the `student_id` and `course_id` fields.
  
- This establishes a many-to-many relationship between the `students` and `courses` collections.

**Summary:**

- **Embedding:** is generally not recommended for many-to-many relationships due to complexity and potential document size issues.
  
- **Referencing:** with a linking collection is better for managing many-to-many relationships, providing flexibility, normalization, and scalability.

## Schema Validation

`Schema validation` in MongoDB ensures that the data inserted into a collection adheres to a specific structure. This is useful for maintaining data integrity and consistency.

***Example:***

### Define a Schema

The schema for a note might include fields like `title`, `content`, `created_at`, and `tags`.

### Create the Collection with Validation

```javascript
db.createCollection("notes", {
  validator: {
    $jsonSchema: {
      bsonType: "object",
      required: ["title", "content", "created_at"],
      properties: {
        title: {
          bsonType: "string",
          description: "must be a string and is required"
        },
        content: {
          bsonType: "string",
          description: "must be a string and is required"
        },
        created_at: {
          bsonType: "date",
          description: "must be a date and is required"
        },
        tags: {
          bsonType: "array",
          items: {
            bsonType: "string"
          },
          description: "must be an array of strings"
        }
      }
    }
  }
});
```

Expected Output:

```sh
{ ok: 1 }
```

### Insert Document

```javascript
db.notes.insertOne({
  title: "Meeting Notes",
  content: "Discuss project milestones and deadlines.",
  created_at: new Date(),
  tags: ["meeting", "project"]
});
```

Expected Output:

```sh
[
  {
    _id: ObjectId('66ed9b02f10872978ec73bfd'),
    title: 'Meeting Notes',
    content: 'Discuss project milestones and deadlines.',
    created_at: ISODate('2024-09-20T15:55:46.385Z'),
    tags: [ 'meeting', 'project' ]
  }
]
```

### Handle Validation Errors

If you try to insert a document that does not conform to the schema, MongoDB will throw a validation error.

For example, if you try to insert a document with a `title` field that is a `number` instead of a `string`, the operation will fail.

```javascript
db.notes.insertOne({
  title: 12345,  // Invalid type
  content: "Discuss project milestones and deadlines.",
  created_at: new Date(),
  tags: ["meeting", "project"]
});
```

Expected Output:

```javascript
Uncaught:
MongoServerError: Document failed validation
Additional information: {
  failingDocumentId: ObjectId('66ed9b44f10872978ec73bfe'),
  details: {
    operatorName: '$jsonSchema',
    schemaRulesNotSatisfied: [
      {
        operatorName: 'properties',
        propertiesNotSatisfied: [
          {
            propertyName: 'title',
            description: 'must be a string and is required',
            details: [
              {
                operatorName: 'bsonType',
                specifiedAs: { bsonType: 'string' },
                reason: 'type did not match',
                consideredValue: 12345,
                consideredType: 'int'
              }
            ]
          }
        ]
      }
    ]
  }
}
```

***Error Breakdown:***

1. **Error Type:** `MongoServerError`
   - **This indicates that the error occurred on the MongoDB server.**

2. **Error Message:** `Document failed validation`
   - **This means that the document did not meet the schema validation rules defined for the collection.**

3. **Additional Information:**
   - **failingDocumentId:** `ObjectId('66ed9b44f10872978ec73bfe')`
     - **This is the unique identifier of the document that failed validation.**
   - **details:**
     - **operatorName:** `$jsonSchema`
       - **Indicates that the validation was performed using a JSON schema.**
     - **schemaRulesNotSatisfied:**
       - **An array of rules that the document did not satisfy.**

4. **Schema Rules Not Satisfied:**
   - **operatorName:** `properties`
     - **Indicates that the validation failed at the properties level.**
   - **propertiesNotSatisfied:**
     - **An array of properties that did not meet the validation criteria.**

5. **Property Details:**
   - **propertyName:** `title`
     - **The name of the property that failed validation.**
   - **description:** `must be a string and is required`
     - **The validation rule that the `title` property must be a string and is required.**
   - **details:**
     - **operatorName:** `bsonType`
       - **Indicates that the validation rule is based on BSON type.**
     - **specifiedAs:** `{ bsonType: 'string' }`
       - **The expected BSON type for the `title` property is a string.**
     - **reason:** `type did not match`
       - **The reason for the validation failure is that the type did not match the expected type.**
     - **consideredValue:** `12345`
       - **The value that was considered for the `title` property.**
     - **consideredType:** `int`
       - **The actual type of the considered value, which is an integer.**

***Resources for More Details:***

- **The MongoDB Limits:** [https://docs.mongodb.com/manual/reference/limits/](https://docs.mongodb.com/manual/reference/limits/)
- **The MongoDB Data Types:** [https://docs.mongodb.com/manual/reference/bson-types/](https://docs.mongodb.com/manual/reference/bson-types/)
- **More on Schema Validation:** [https://docs.mongodb.com/manual/core/schema-validation/](https://docs.mongodb.com/manual/core/schema-validation/)
