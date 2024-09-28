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
    - [MongoDB Query Selectors](#mongodb-query-selectors)
    - [Projection Operators](#projection-operators)
    - [MongoDB Cursor Methods](#mongodb-cursor-methods)
  - [Update a Document](#update-a-document)
    - [updateOne Method](#updateone-method)
    - [updateMany Method](#updatemany-method)
    - [Updating Multiple Fields with `$set`](#updating-multiple-fields-with-set)
    - [Increment and Decrement Values With `$inc` Operator](#increment-and-decrement-values-with-inc-operator)
    - [`$min`, `$max`, and `$mul` in MongoDB](#min-max-and-mul-in-mongodb)
    - [Getting Rid of Fields with `$unset` Operator](#getting-rid-of-fields-with-unset-operator)
    - [`$rename` Operator in MongoDB](#rename-operator-in-mongodb)
    - [`upsert` Option in MongoDB](#upsert-option-in-mongodb)
    - [Adding Matched Array Elements With `$and` Operator](#adding-matched-array-elements-with-and-operator)
    - [Adding Elements to an Array With `$push`](#adding-elements-to-an-array-with-push)
    - [Updating a Matched Array Element With `$.`](#updating-a-matched-array-element-with-)
    - [Updating All Array Elements With `$[]`](#updating-all-array-elements-with-)
    - [Finding and Updating Specific Fields](#finding-and-updating-specific-fields)
    - [Removing Elements from an Array With `$pull`](#removing-elements-from-an-array-with-pull)
    - [UnderStanding `$addToSet`](#understanding-addtoset)
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
  - [3. Working with Indexes](#3-working-with-indexes)
    - [What are Indexes and Why do we use them?](#what-are-indexes-and-why-do-we-use-them)
    - [Why Use Indexes?](#why-use-indexes)
    - [Creating an Index](#creating-an-index)
    - [Removing Indexes](#removing-indexes)
    - [Creating Compound Indexes](#creating-compound-indexes)
    - [Using Indexes for Sorting](#using-indexes-for-sorting)
    - [Default Index](#default-index)
    - [Understanding Partial Filter Expressions](#understanding-partial-filter-expressions)
    - [Time to Live (TTL) Index in MongoDB](#time-to-live-ttl-index-in-mongodb)
    - [Understanding Covered Queries](#understanding-covered-queries)
    - [How MongoDB Rejects a Query Plan](#how-mongodb-rejects-a-query-plan)
    - [Multi-Key Indexes in MongoDB](#multi-key-indexes-in-mongodb)
    - [Text Indexes in MongoDB](#text-indexes-in-mongodb)
    - [Text Indexes and Sorting in MongoDB](#text-indexes-and-sorting-in-mongodb)
    - [Combining Text Index with Other Indexes in MongoDB](#combining-text-index-with-other-indexes-in-mongodb)
    - [Excluding Words in Text Index Queries in MongoDB](#excluding-words-in-text-index-queries-in-mongodb)
    - [Setting the Default Language and Using Weights in MongoDB Text Indexes](#setting-the-default-language-and-using-weights-in-mongodb-text-indexes)
    - [Building Indexes in MongoDB](#building-indexes-in-mongodb)
    - [Importing JSON to MongoDB Shell](#importing-json-to-mongodb-shell)
    - [More Details](#more-details)
  - [4. Geospatial Data in MongoDB](#4-geospatial-data-in-mongodb)
    - [Adding GeoJSON Data](#adding-geojson-data)
    - [Creating a Geospatial Index](#creating-a-geospatial-index)
    - [Querying GeoJSON Data](#querying-geojson-data)
    - [Finding Places Inside a Certain Area With `$geoWithin`](#finding-places-inside-a-certain-area-with-geowithin)
    - [Finding Out if a User is Inside a Specific Area with `$geoIntersects`](#finding-out-if-a-user-is-inside-a-specific-area-with-geointersects)
    - [Finding Places Within Certain Radius With `$centerSphere`](#finding-places-within-certain-radius-with-centersphere)
  - [5. Understanding Aggregation Framework](#5-understanding-aggregation-framework)
    - [Transforming BirthDate Using `$dateToString`](#transforming-birthdate-using-datetostring)
    - [Transforming BirthDate Using `$convert`](#transforming-birthdate-using-convert)
    - [Understanding `$isoWeekYear` Operator](#understanding-isoweekyear-operator)
    - [`$group` Vs `$project`](#group-vs-project)
    - [Pushing Elements Into Newly Created Arrays](#pushing-elements-into-newly-created-arrays)
    - [Understanding `$unwind` Stage](#understanding-unwind-stage)
    - [Eliminating Duplicate Values](#eliminating-duplicate-values)
    - [Using Projection With Arrays](#using-projection-with-arrays)
    - [Getting The Length Of An Array](#getting-the-length-of-an-array)
    - [Using `$filter` Operator](#using-filter-operator)
    - [Applying Multiple Operations To Array](#applying-multiple-operations-to-array)
    - [Understanding `$bucket`](#understanding-bucket)
    - [Writing Pipeline Results Into a New Collection](#writing-pipeline-results-into-a-new-collection)
    - [Working With `$geoNear` Stage](#working-with-geonear-stage)
  - [6. Working With Numbers](#6-working-with-numbers)
    - [1. **32-bit Integer (`NumberInt`):**](#1-32-bit-integer-numberint)
    - [2. **64-bit Integer (`NumberLong`)**](#2-64-bit-integer-numberlong)
    - [3. **Double (`NumberDouble`)**](#3-double-numberdouble)
    - [4. **Decimal (`NumberDecimal`)**](#4-decimal-numberdecimal)
  - [7. Performance , Fault Tolerancy And Deployment](#7-performance--fault-tolerancy-and-deployment)
    - [Understanding Capped Collections](#understanding-capped-collections)
    - [What are Replica Sets?](#what-are-replica-sets)
    - [Understanding Sharding](#understanding-sharding)
    - [Deploying a MongoDB server using MongoDB Atlas](#deploying-a-mongodb-server-using-mongodb-atlas)
  - [8. Transaction](#8-transaction)
    - [Use Cases for Transactions in MongoDB](#use-cases-for-transactions-in-mongodb)
  - [9. Introduction Of Stitch](#9-introduction-of-stitch)
    - [What is Stitch?](#what-is-stitch)

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
  
### MongoDB Query Selectors

***Comparison Operators:***

1. `$eq` (Equal): Matches values that are equal to a specified value.

   ```javascript
   { "age": { "$eq": 25 } }
   ```

   This query selects all documents where the `age` field is equal to 25.

2. `$ne` (Not Equal): Matches all values that are not equal to a specified value.

   ```javascript
   { "age": { "$ne": 25 } }
   ```

   This query selects all documents where the `age` field is not equal to 25.

3. `$gt` (Greater Than): Matches values that are greater than a specified value.

   ```javascript
   { "age": { "$gt": 25 } }
   ```

   This query selects all documents where the `age` field is greater than 25.

4. `$gte` (Greater Than or Equal): Matches values that are greater than or equal to a specified value.

   ```javascript
   { "age": { "$gte": 25 } }
   ```

   This query selects all documents where the `age` field is greater than or equal to 25.

5. `$lt` (Less Than): Matches values that are less than a specified value.

   ```javascript
   { "age": { "$lt": 25 } }
   ```

   This query selects all documents where the `age` field is less than 25.

6. `$lte` (Less Than or Equal): Matches values that are less than or equal to a specified value.

   ```javascript
   { "age": { "$lte": 25 } }
   ```

   This query selects all documents where the `age` field is less than or equal to 25.

***Logical Operators:***

1. `$and`: Joins query clauses with a logical AND returns all documents that match the conditions of both clauses.

   ```javascript
   { "$and": [ { "age": { "$gt": 25 } }, { "age": { "$lt": 50 } } ] }
   ```

   This query selects all documents where the `age` field is greater than 25 and less than 50.

2. `$or`: Joins query clauses with a logical OR returns all documents that match the conditions of either clause.

   ```javascript
   { "$or": [ { "age": { "$lt": 20 } }, { "age": { "$gt": 50 } } ] }
   ```

   This query selects all documents where the `age` field is either less than 20 or greater than 50.

3. `$not`: Inverts the effect of a query expression and returns documents that do not match the query expression.

   ```javascript
   { "age": { "$not": { "$gt": 25 } } }
   ```

   This query selects all documents where the `age` field is not greater than 25.

***Element Operators***

1. `$exists`: Matches documents that have the specified field.

   ```javascript
   { "nickname": { "$exists": true } }
   ```

   This query selects all documents that have the `nickname` field.

2. `$type`: Selects documents if a field is of the specified type.

   ```javascript
   { "age": { "$type": "int" } }
   ```

  This query selects all documents where the `age` field is of type integer.

***Evaluation Operators:***

1. `$regex`: Selects documents where values match a specified regular expression.

   ```javascript
   { "name": { "$regex": "^A" } }
   ```

   This query selects all documents where the `name` field starts with the letter "A".

2. `$mod`: Performs a modulo operation on the value of a field and selects documents with a specified result.

   ```javascript
   { "age": { "$mod": [4, 0] } }
   ```

   This query selects all documents where the `age` field divided by 4 has a remainder of 0.

3. `$text`: Performs text search.

   ```javascript
   { "$text": { "$search": "coffee" } }
   ```

   This query selects all documents that contain the `word` "coffee".

4. `$where`: Matches documents that satisfy a JavaScript expression.

   ```javascript
   { "$where": "this.age > 25" }
   ```

   This query selects all documents where the `age` field is greater than 25.

***Array Operators:***

1. `$in`: Matches any of the values specified in an array.

   ```javascript
   { "age": { "$in": [20, 25, 30] } }
   ```

   This query selects all documents where the `age` field is either 20, 25, or 30.

2. `$nin`: Matches none of the values specified in an array.

   ```javascript
   { "age": { "$nin": [20, 25, 30] } }
   ```

   This query selects all documents where the `age` field is not 20, 25, or 30.

3. `$all`: Matches arrays that contain all elements specified in the query.

   ```javascript
   { "tags": { "$all": ["red", "blue"] } }
   ```

   This query selects all documents where the `tags` array contains both "red" and "blue".

4. `$size`: Selects documents if the array field is of the specified size.

   ```javascript
   { "tags": { "$size": 3 } }
   ```

   This query selects all documents where the `tags` array has 3 elements.

5. `$elemMatch`: Matches documents that contain an array field with at least one element that matches all the specified query criteria.

   ```javascript
   { "results": { "$elemMatch": { "product": "xyz", "score": { "$gte": 8 } } } }
   ```

   This query selects all documents where the `results` array contains an element with product equal to "xyz" and score greater than or equal to 8.

### Projection Operators

1. `$`: Projects the first element in an array that matches the query condition.

   ```javascript
   db.collection.find(
     { "grades": { "$elemMatch": { "score": { "$gt": 80 } } } },
     { "grades.$": 1 }
   )
   ```

   This query returns the first element in the `grades` array that has a `score` greater than 80.

2. `$elemMatch`: Projects the first element in an array that matches the specified `$elemMatch` condition.

   ```javascript
   db.collection.find(
     { "grades": { "$elemMatch": { "score": { "$gt": 80 } } } },
     { "grades": { "$elemMatch": { "score": { "$gt": 80 } } } }
   )
   ```

   This query returns the first element in the `grades` array that has a `score` greater than 80.

3. `$meta`: Projects the document's score assigned by the `$meta` textScore.

   ```javascript
   db.collection.find(
     { "$text": { "$search": "coffee" } },
     { "score": { "$meta": "textScore" } }
   )
   ```

   This query returns documents that match the text search for "coffee" and includes a `score` field with the text search score.

4. `$slice`: Limits the number of elements projected from an array. Supports both positive and negative values.

   ```javascript
   db.collection.find(
     {},
     { "comments": { "$slice": 5 } }
   )
   ```

   This query returns the first 5 elements in the `comments` array.

### MongoDB Cursor Methods

1. `find()`: Initiates a query and returns a cursor to the documents that match the query.

   ```javascript
   db.users.find({ isActive: true });
   ```

   ***Explanation:*** Finds all documents where isActive is true.

2. `sort()`: Sorts the documents in the cursor.

   ```javascript
   db.users.find().sort({ age: 1 });
   ```

   ***Explanation:*** Sorts the documents by the age field in ascending order.

3. `limit()`: Limits the number of documents returned by the cursor.

   ```javascript
   db.users.find().limit(5);
   ```

   ***Explanation:*** Limits the result to 5 documents.

4. `skip()`: Skips a specified number of documents in the cursor.

   ```javascript
   db.users.find().skip(2);
   ```

   ***Explanation:*** Skips the first 2 documents in the result set.

5. `count()`: Returns the count of documents that match the query.

   ```javascript
   db.users.find({ isActive: true }).count();
   ```

   ***Explanation:*** Counts the number of documents where isActive is true.

6. `forEach()`: Iterates over the cursor and applies a function to each document.

   ```javascript
   db.users.find().forEach(function(doc) { printjson(doc); });
   ```

   ***Explanation:*** Prints each document in the result set in JSON format.

7. `map()`: Applies a function to each document in the cursor and returns an array of the results.

   ```javascript
   db.users.find().map(function(doc) { return doc.name; });
   ```

   ***Explanation:*** Returns an array of the name field from each document.

8. `toArray()`:Converts the cursor to an array.

   ```javascript
   db.users.find().toArray();
   ```

   ***Explanation:*** Explanation: Converts the result set to an array.

9. `explain()`: Provides information on the query plan.

   ```javascript
   db.users.find({ isActive: true }).explain("executionStats");
   ```

   ***Explanation:*** Provides detailed information about how MongoDB executed the query.

10. `projection()`: Specifies the fields to return in the documents.

    ```javascript
    db.users.find({}, { name: 1, age: 1 });
    ```

    ***Explanation:*** Returns only the name and age fields in the result set.

11. `batchSize()`: Applies a function to each document in the cursor and returns an array of the results.

    ```javascript
    db.users.find().batchSize(100);
    ```

    ***Explanation:*** Sets the batch size to 100 documents.

12. `maxTimeMS()`: Specifies a time limit for processing operations on a cursor.

    ```javascript
    db.users.find().maxTimeMS(5000);
    ```

    ***Explanation:***  Limits the query execution time to 5000 milliseconds (5 seconds).

13. `hasNext()`: Returns true if the cursor has more documents.

    ```javascript
    var cursor = db.users.find();
    while (cursor.hasNext()) {
    printjson(cursor.next());
    }
    ```

    ***Explanation:***  Iterates over the cursor and prints each document if there are more documents.

14. `next()`: Returns the next document in the cursor.

    ```javascript
    var cursor = db.users.find();
    if (cursor.hasNext()) {
    printjson(cursor.next());
    }
    ```

    ***Explanation:*** Prints the next document in the cursor if it exists.

15. `itcount()`: Returns the number of documents in the cursor.

    ```javascript
    db.users.find().itcount();
    ```

    ***Explanation:*** Counts the number of documents in the result set.

16. `pretty()`: Formats the output of the cursor for readability.

    ```javascript
    db.users.find().pretty();
    ```

    ***Explanation:*** Formats the result set in a more readable JSON format.

17. `max()`:Specifies an exclusive upper bound for a specific index in order to constrain the results of a query.

    ```javascript
    db.users.find().max({ age: 30 });
    ```

    ***Explanation:*** Limits the result set to documents where the age field is less than 30.

18. `min()`: Specifies an inclusive lower bound for a specific index in order to constrain the results of a query.

    ```javascript
    db.users.find().min({ age: 20 });
    ```

    ***Explanation:***  Limits the result set to documents where the age field is greater than or equal to 20.

19. `hint()`: Forces MongoDB to use a specific index for the query.

    ```javascript
    db.users.find({ age: { $gt: 25 } }).hint({ age: 1 });
    ```

    ***Explanation:***  Forces the query to use the index on the age field.

20. `comment()`: Adds a comment to the query to help with profiling and debugging.

    ```javascript
    db.users.find({ isActive: true }).comment("Find active users");
    ```

    ***Explanation:***  Adds a comment to the query for easier identification in logs and profiling.

***Resources for More Details:***

For more detailed information, refer to the official MongoDB documentation:

- **Find Method**: [find Method](https://docs.mongodb.com/manual/reference/method/db.collection.find/)
- **Cursors**: [Iterate a Cursor](https://docs.mongodb.com/manual/tutorial/iterate-a-cursor/)
- **Query Operator Reference**: [Query Operator Reference](https://docs.mongodb.com/manual/reference/operator/query/)

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

### Updating Multiple Fields with `$set`

The `$set` operator in MongoDB is used to update the value of one or more fields in a document. If the specified field does not exist, `$set` will add the field with the specified value.

***Example:***

Suppose we have a collection named `userData` and we want to update the `age` and `city` fields for a user with a specific `_id`.

```javascript
db.userData.updateOne(
  { _id: ObjectId('66ea6dbbadd143d6bfc73bf9') },
  {
    $set: {
      age: 31,
      city: 'San Francisco'
    }
  }
)
```

***Verifying the Update:***

To verify that the fields have been updated, you can use the `find` command:

```javascript
db.userData.find({ _id: ObjectId('66ea6dbbadd143d6bfc73bf9') })
```

***Expected Output:***

```javascript
{
  _id: ObjectId('66ea6dbbadd143d6bfc73bf9'),
  name: 'Jane Doe',
  age: 31,
  email: 'jane.doe@example.com',
  city: 'San Francisco'
}
```

### Increment and Decrement Values With `$inc` Operator

The `$inc` operator in MongoDB is used to increment or decrement the value of a field by a specified amount. If the field does not exist, `$inc` will create the field and set it to the specified value.

***Example:***

Suppose we have a collection named `userData` and we want to increment and decrement the `age` field for a user with a specific `_id`.

**Incrementing Age:**

```javascript
db.userData.updateOne(
  { _id: ObjectId('66ea6dbbadd143d6bfc73bf9') },
  {
    $inc: {
      age: 1
    }
  }
)
```

***Expected Output:***

```javascript
{
  _id: ObjectId('66ea6dbbadd143d6bfc73bf9'),
  name: 'Jane Doe',
  age: 32, // Assuming the initial age was 31
  email: 'jane.doe@example.com',
  city: 'San Francisco'
}
```

**Decrementing age:**

```javascript
db.userData.updateOne(
  { _id: ObjectId('66ea6dbbadd143d6bfc73bf9') },
  {
    $inc: {
      age: -1
    }
  }
)
```

***Expected Output:***

```javascript
{
  _id: ObjectId('66ea6dbbadd143d6bfc73bf9'),
  name: 'Jane Doe',
  age: 30, // Assuming the initial age was 31
  email: 'jane.doe@example.com',
  city: 'San Francisco'
}
```

### `$min`, `$max`, and `$mul` in MongoDB

MongoDB provides several operators to update fields in documents. Here, we will discuss the `$min`, `$max`, and `$mul` operators.

**`$min` Operator:**

The `$min` operator updates the value of the field to a specified value if the specified value is less than the current value of the field.

***Example:***

Suppose we have a collection named `userData` and we want to update the `age` field to a minimum value of 25 for a user with a specific `_id`.

```javascript
db.userData.updateOne(
  { _id: ObjectId('66ea6dbbadd143d6bfc73bf9') },
  {
    $min: {
      age: 25
    }
  }
)
```

***Explanation:***

- `$min:` This operator is used to update the field to the specified value if the specified value is less than the current value.

- `{ age: 25 }:` This sets the age field to 25 if the current age is greater than 25.

***Expected Output:***

**If the initial age was 30:**

```javascript
{
  _id: ObjectId('66ea6dbbadd143d6bfc73bf9'),
  name: 'Jane Doe',
  age: 25, // Updated to 25 because 25 < 30
  email: 'jane.doe@example.com',
  city: 'San Francisco'
}
```

**`$max` Operator:**

The `$max` operator updates the value of the field to a specified value if the specified value is greater than the current value of the field.

***Example:***

Suppose we have a collection named `userData` and we want to update the `age` field to a maximum value of 35 for a user with a specific `_id`.

```javascript
db.userData.updateOne(
  { _id: ObjectId('66ea6dbbadd143d6bfc73bf9') },
  {
    $max: {
      age: 35
    }
  }
)
```

***Explanation:***

- `$max:` This operator is used to update the field to the specified value if the specified value is greater than the current value.

- `{ age: 35 }:` This sets the age field to 35 if the current age is less than 35.

***Expected Output***

**If the initial age was 30:**

```javascript
{
  _id: ObjectId('66ea6dbbadd143d6bfc73bf9'),
  name: 'Jane Doe',
  age: 35, // Updated to 35 because 35 > 30
  email: 'jane.doe@example.com',
  city: 'San Francisco'
}
```

**`$mul` Operator:**

The `$mul` operator multiplies the value of the field by a specified value.

***Example:***

Suppose we have a collection named `userData` and we want to multiply the `age` field by 2 for a user with a specific `_id`.

```javascript
db.userData.updateOne(
  { _id: ObjectId('66ea6dbbadd143d6bfc73bf9') },
  {
    $mul: {
      age: 2
    }
  }
)
```

***Explanation***

- `$mul:` This operator is used to multiply the field by the specified value.

- `{ age: 2 }:` This multiplies the age field by 2.

***Expected Output:***

**If the initial age was 30:**

```javascript
{
  _id: ObjectId('66ea6dbbadd143d6bfc73bf9'),
  name: 'Jane Doe',
  age: 60, // Updated to 60 because 30 * 2 = 60
  email: 'jane.doe@example.com',
  city: 'San Francisco'
}
```

### Getting Rid of Fields with `$unset` Operator

The `$unset` operator in MongoDB is used to remove a field from a document. If the field does not exist, `$unset` does nothing.

***Example:***

***Suppose we have a collection named `userData` and we want to remove the `city` field for a user with a specific `_id`.***

```javascript
db.userData.updateOne(
  { _id: ObjectId('66ea6dbbadd143d6bfc73bf9') },
  {
    $unset: {
      city: ""
    }
  }
)
```

After running this command, the document with `_id: ObjectId('66ea6dbbadd143d6bfc73bf9')` will have its `city` field removed.

***Verify the Update:***

```javascript
db.userData.find({ _id: ObjectId('66ea6dbbadd143d6bfc73bf9') })
```

***Expected Output***

**If the initial document was:**

```javascript
{
  _id: ObjectId('66ea6dbbadd143d6bfc73bf9'),
  name: 'Jane Doe',
  age: 30,
  email: 'jane.doe@example.com',
  city: 'San Francisco'
}
```

**The updated document will be:**

```javascript
{
  _id: ObjectId('66ea6dbbadd143d6bfc73bf9'),
  name: 'Jane Doe',
  age: 30,
  email: 'jane.doe@example.com'
}
```

### `$rename` Operator in MongoDB

The `$rename` operator in MongoDB is used to rename a field in a document. If the field does not exist, `$rename` does nothing.

***Example:***

Suppose we have a collection named `userData` and we want to rename the `city` field to `location` for a user with a specific `_id`.

```javascript
db.userData.updateOne(
  { _id: ObjectId('66ea6dbbadd143d6bfc73bf9') },
  {
    $rename: {
      city: "location"
    }
  }
)
```

After running this command, the document with `_id: ObjectId('66ea6dbbadd143d6bfc73bf9')` will have its `city` field renamed to `location`.

***Expected Output:***

```javascript
{
  _id: ObjectId('66ea6dbbadd143d6bfc73bf9'),
  name: 'Jane Doe',
  age: 30,
  email: 'jane.doe@example.com',
  location: 'San Francisco' // Renamed from 'city' to 'location'
}
```

### `upsert` Option in MongoDB

he `upsert` option in MongoDB is used in update operations to insert a new document if no document matches the query criteria. If a document matches the query criteria, it will be updated.

***ExampleL***

Suppose we have a collection named `userData` and we want to update the `age` field for a user with a specific `_id`. If the user does not exist, we want to insert a new document with the specified `_id` and `age`.

```javascript
db.userData.updateOne(
  { _id: ObjectId('66ea6dbbadd143d6bfc73bf9') },
  {
    $set: {
      age: 30
    }
  },
  { upsert: true }
)
```

- If a document with `_id: ObjectId('66ea6dbbadd143d6bfc73bf9')` exists, its `age` field will be updated to 30.

- If no such document exists, a new document will be inserted with `_id: ObjectId('66ea6dbbadd143d6bfc73bf9')` and `age:` 30.

***Expected Output:***

**If the document was updated:**

```javascript
{
  _id: ObjectId('66ea6dbbadd143d6bfc73bf9'),
  age: 30
}
```

**If the document was Inserted:**

```javascript
{
  _id: ObjectId('66ea6dbbadd143d6bfc73bf9'),
  age: 30
}
```

### Adding Matched Array Elements With `$and` Operator

The `$and` operator in MongoDB is used to join query clauses with a logical AND. It returns documents that match all the conditions specified in the `$and` array.

***Example:***

Suppose we have a collection named `userData` and we want to find users who are older than 25 and live in `San Francisco`.

```javascript
db.userData.find({
  $and: [
    { age: { $gt: 25 } },
    { city: "San Francisco" }
  ]
})
```

**Explanation:**

1. **Collection:** userData is the collection we are querying.
2. **Query:**

- `$and:` : This operator is used to combine multiple conditions.
- `[ { age: { $gt: 25 } }, { city: "San Francisco" } ]:` This array contains the conditions that must all be met for a document to be returned.
  
- `{ age: { $gt: 25 } }:` This condition specifies that the `age` field must be greater than 25.
  
- `{ city: "San Francisco" }:` This condition specifies that the `city` field must be `San Francisco`.

***After running this query, MongoDB will return documents where the age field is greater than 25 and the `city` field is `San Francisco`.***

***Verifying the Query***

To verify the query, you can use the `find` command:

```javascript
db.userData.find({
  $and: [
    { age: { $gt: 25 } },
    { city: "San Francisco" }
  ]
})
```

***Expected Output:***

If the collection contains the following documents:

```javascript
[
  { _id: ObjectId('1'), name: 'Alice', age: 30, city: 'San Francisco' },
  { _id: ObjectId('2'), name: 'Bob', age: 20, city: 'San Francisco' },
  { _id: ObjectId('3'), name: 'Charlie', age: 35, city: 'Los Angeles' }
]
```

The query will return:

```javascript
[
  { _id: ObjectId('1'), name: 'Alice', age: 30, city: 'San Francisco' }
]
```

### Adding Elements to an Array With `$push`

To add elements to an array within a document, you can use the `$push` operator in MongoDB. This operator appends a specified value to an array.

***Example:***

Consider the following document in the `users` collection:

```javascript
{
  _id: ObjectId('1'),
  name: 'Alice',
  hobbies: [
    { name: 'reading', frequency: 3 },
    { name: 'swimming', frequency: 2 }
  ]
}
```

**Update Query:**

To add a new hobby, `cycling`, with a `frequency` of `1` to the `hobbies` array, you can use the following query:

```javascript
db.users.updateOne(
  { _id: ObjectId('1') },
  {
    $push: {
      hobbies: { name: 'cycling', frequency: 1 }
    }
  }
)
```

***Explanation:***

- `db.users.updateOne:` This function updates a single document in the users collection.

- **Query Part:** `{ _id: ObjectId('1') }`
  
  - This part of the query finds the document where `_id` is `ObjectId('1')`.

- **Update Part:** `$push: { hobbies: { name: 'cycling', frequency: 1 } }`
  
  - The `$push` operator is used to add a new element to the `hobbies` array.
  
  - `{ name: 'cycling', frequency: 1 }` specifies the new element to be added to the array.

**Expected Output:**

After running the update query, the document will be updated as follows:

```javascript
{
  _id: ObjectId('1'),
  name: 'Alice',
  hobbies: [
    { name: 'reading', frequency: 3 },
    { name: 'swimming', frequency: 2 },
    { name: 'cycling', frequency: 1 }
  ]
}
```

### Updating a Matched Array Element With `$.`

To update a specific element in an array within a document, you can use the `$` positional operator. This operator identifies the first array element that matches the query condition.

***Example:***

**Consider the following document in the `users` collection:**

```javascript
{
  _id: ObjectId('1'),
  name: 'Alice',
  hobbies: [
    { name: 'reading', frequency: 3 },
    { name: 'swimming', frequency: 2 },
    { name: 'cycling', frequency: 1 }
  ]
}
```

**Update Query:**

To update the `frequency` of the `swimming` hobby to `4`, you can use the following query:

```javascript
db.users.updateOne(
  { _id: ObjectId('1'), 'hobbies.name': 'swimming' },
  { $set: { 'hobbies.$.frequency': 4 } }
)
```

**Explanation:**

- `db.users.updateOne:` This function updates a single document in the `users` collection.

- Query Part: `{ _id: ObjectId('1'), 'hobbies.name': 'swimming' }`
  
  - This part of the query finds the document where `_id` is `ObjectId('1')` and there is an element in the `hobbies` array with the `name` equal to `swimming`.

- Update Part: `{ $set: { 'hobbies.$.frequency': 4 } }`

  - The `$set` operator is used to update the value of a field.
  
  - The `$` positional operator is used to identify the first element in the array that matches the query condition `('hobbies.name': 'swimming')`.
  
  - `hobbies.$.frequency` specifies that the `frequency` field of the matched `hobbies` array element should be updated to `4`.

***Expected Output:***

After running the update query, the document will be updated as follows:

```javascript
{
  _id: ObjectId('1'),
  name: 'Alice',
  hobbies: [
    { name: 'reading', frequency: 3 },
    { name: 'swimming', frequency: 4 },
    { name: 'cycling', frequency: 1 }
  ]
}
```

***The frequency of the swimming hobby has been updated from 2 to 4.***

### Updating All Array Elements With `$[]`

To update all elements in an array within a document, you can use the `$[]` positional operator. This operator allows you to update all elements in an array that match the query condition.

***Example:***

Consider the following document in the `users` collection:

```javascript
{
  _id: ObjectId('1'),
  name: 'Alice',
  hobbies: [
    { name: 'reading', frequency: 3 },
    { name: 'swimming', frequency: 2 },
    { name: 'cycling', frequency: 1 }
  ]
}
```

**Update Query:**

To update the `frequency` of all hobbies to `5`, you can use the following query:

```javascript
db.users.updateOne(
  { _id: ObjectId('1') },
  { $set: { 'hobbies.$[].frequency': 5 } }
)
```

**Explanation:**

- `db.users.updateOne:` This function updates a single document in the `users` collection.
  
- **Query Part:** `{ _id: ObjectId('1') }`
  
  - This part of the query finds the document where `_id` is `ObjectId('1')`.
  
- **Update Part:** `{ $set: { 'hobbies.$[].frequency': 5 } }`
  
  - The `$set` operator is used to update the value of a field.
  
  - The `$[]` positional operator is used to identify all elements in the array.
  
  - `hobbies.$[].frequency` specifies that the `frequency` field of all elements in the `hobbies` array should be updated to `5`.

**Expected Output:**

After running the update query, the document will be updated as follows:

```javascript
{
  _id: ObjectId('1'),
  name: 'Alice',
  hobbies: [
    { name: 'reading', frequency: 5 },
    { name: 'swimming', frequency: 5 },
    { name: 'cycling', frequency: 5 }
  ]
}
```

### Finding and Updating Specific Fields

To find a document and update specific fields, you can use the `findOneAndUpdate` method in MongoDB. This method allows you to find a document based on a query and update specific fields in that document.

***Example:***

Consider the following document in the `users` collection:

```javascript
{
  _id: ObjectId('1'),
  name: 'Alice',
  age: 30,
  city: 'San Francisco',
  hobbies: [
    { name: 'reading', frequency: 3 },
    { name: 'swimming', frequency: 2 },
    { name: 'cycling', frequency: 1 }
  ]
}
```

**Find and Update Query:**

To find the document where `name` is `Alice` and update the `age` to 31 and the `frequency` of the `swimming` hobby to `4`, you can use the following query:

```javascript
db.users.findOneAndUpdate(
  { name: 'Alice' },
  {
    $set: {
      age: 31,
      'hobbies.$[elem].frequency': 4
    }
  },
  {
    arrayFilters: [{ 'elem.name': 'swimming' }],
    returnNewDocument: true
  }
)
```

**Explanation:**

- `db.users.findOneAndUpdate:` This function finds a single document in the `users` collection and updates it.
  
- **Query Part:** `{ name: 'Alice' }`
  
  - This part of the query finds the document where `name` is `Alice`.

- **Update Part:** `$set: { age: 31, 'hobbies.$[elem].frequency': 4 }`
  
  - The `$set` operator is used to update the value of fields.
  
  - `age:` 31 updates the `age` field to `31`.
  
  - `'hobbies.$[elem].frequency': 4` updates the `frequency` field of the matched element in the `hobbies` array to `4`.

- **Array Filters:** `arrayFilters: [{ 'elem.name': 'swimming' }]`

  - This specifies that the update should only apply to elements in the `hobbies` array where the `name` is `swimming`.
  
- **Options:** `returnNewDocument: true`
  
  - This option ensures that the updated document is returned.

**Expected Output:**

After running the find and update query, the document will be updated as follows:

```javascript
{
  _id: ObjectId('1'),
  name: 'Alice',
  age: 31,
  city: 'San Francisco',
  hobbies: [
    { name: 'reading', frequency: 3 },
    { name: 'swimming', frequency: 4 },
    { name: 'cycling', frequency: 1 }
  ]
}
```

***Note: You can use the updateMany method if you want to update multiple documents that match a query. Here’s how you can use updateMany to update specific fields in all matching documents.***

### Removing Elements from an Array With `$pull`

To remove elements from an array within a document, you can use the `$pull` operator in MongoDB. This operator removes all array elements that match a specified condition.

***Example:***

Consider the following document in the `users` collection:

```javascript
{
  _id: ObjectId('1'),
  name: 'Alice',
  hobbies: [
    { name: 'reading', frequency: 3 },
    { name: 'swimming', frequency: 4 },
    { name: 'cycling', frequency: 1 }
  ]
}
```

***Note: `frequency` is a field within each object in the `hobbies` array. It represents how often the user engages in a particular hobby.***

**Update Query:**

To remove the `swimming` hobby from the `hobbies` array, you can use the following query:

```javascript
db.users.updateOne(
  { _id: ObjectId('1') },
  {
    $pull: {
      hobbies: { name: 'swimming' }
    }
  }
)
```

**Explanation:**

- `db.users.updateOne:` This function updates a single document in the `users` collection.
  
- **Query Part:** `{ _id: ObjectId('1') }`
  
  - This part of the query finds the document where _id is ObjectId('1').

- **Update Part:$pull:** `{ hobbies: { name: 'swimming' } }`
  
  - The `$pull` operator is used to remove elements from the `hobbies` array.
  
  - `{ name: 'swimming' }` specifies the condition to match elements to be removed from the array.

**Expected Output:**

After running the update query, the document will be updated as follows:

```javascript
{
  _id: ObjectId('1'),
  name: 'Alice',
  hobbies: [
    { name: 'reading', frequency: 3 },
    { name: 'cycling', frequency: 1 }
  ]
}
```

### UnderStanding `$addToSet`

The `$addToSet` operator in MongoDB is used to add an element to an array only if the element does not already exist in the array. This ensures that there are no duplicate values in the array.

- **Purpose:** The `$addToSet` operator adds a value to an array only if the value is not already present in the array.

- **Use Case:** It is useful when you want to maintain a unique set of elements in an array.

***Example:***

Consider the following document in the `users` collection:

```javascript
{
  _id: ObjectId('1'),
  name: 'Alice',
  hobbies: [
    { name: 'reading', frequency: 3 },
    { name: 'swimming', frequency: 4 }
  ],
  tags: ['active', 'outdoor']
}
```

**Update Query:**

To add a new tag, `indoor`, to the `tags` array only if it does not already exist, you can use the following query:

```javascript
db.users.updateOne(
  { _id: ObjectId('1') },
  {
    $addToSet: {
      tags: 'indoor'
    }
  }
)
```

**Explanation:**

- **db.users.updateOne:** This function updates a single document in the users collection.

- **Query Part:** `{ _id: ObjectId('1') }`
  
  - This part of the query finds the document where _id is ObjectId('1').

- **Update Part:** `$addToSet: { tags: 'indoor' }`
  
  - The `$addToSet` operator is used to add the value `'indoor'` to the `tags` array only if it does not already exist in the array.

**Expected Output:**

After running the update query, the document will be updated as follows:

```javascript
{
  _id: ObjectId('1'),
  name: 'Alice',
  hobbies: [
    { name: 'reading', frequency: 3 },
    { name: 'swimming', frequency: 4 }
  ],
  tags: ['active', 'outdoor', 'indoor']
}
```

***Note: If the `tags` array already contained `'indoor'`, the array would remain unchanged.***

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

## 3. Working with Indexes

### What are Indexes and Why do we use them?

- `Indexes` in MongoDB are special data structures that store a small portion of the data set in an easy-to-traverse form. They are used to improve the speed of data retrieval operations on a database table at the cost of additional space and slower writes.
  
- Without `indexes`, MongoDB must perform a collection scan, i.e., scan every document in a collection, to select those documents that match the query statement.

### Why Use Indexes?

1. **Performance Improvement:** Indexes significantly improve query performance by reducing the amount of data MongoDB needs to scan.

2. **Efficient Sorting:** Indexes can also be used to efficiently sort query results.

3. **Uniqueness:** Unique indexes ensure that the indexed fields do not store duplicate values.

***Example:***

Consider a collection `users` with documents that have the following structure:

```javascript
{
  "name": "John Doe",
  "age": 30,
  "email": "john.doe@example.com"
}
```

### Creating an Index

To create an index on the `email` field, you can use the following command:

```javascript
db.users.createIndex({ email: 1 })
```

This command creates an ascending index on the `email` field.

**Query with Index:**

When you query the `users` collection by email, MongoDB can use the index to quickly locate the documents:

```javascript
db.users.find({ email: "john.doe@example.com" })
```

***Note:Without the `index`, MongoDB would need to scan every document in the `users` collection to find the matching document.***

***Summary:***

`Indexes` are crucial for optimizing query performance in MongoDB. They allow for faster data retrieval and efficient sorting, making them an essential tool for managing large datasets.

### Removing Indexes

To remove the index on the `email` field, you can use the following command:

```javascript
db.users.dropIndex({ email: 1 })
```

***Expected Output:***

```javascript
{
  "nIndexesWas": 2, // Number of indexes before the drop operation
  "ok": 1,          // Status of the operation (1 indicates success)
}
```

### Creating Compound Indexes

`Compound indexes` are indexes that include more than one field. They are useful for queries that need to filter or sort on multiple fields. By creating a compound index, MongoDB can use the index to optimize queries that involve any prefix of the fields in the index.

***Example:***

Suppose you have a collection `orders` with documents that include `customerId` and `orderDate` fields. You can create a compound index on these fields to optimize queries that filter by `customerId` and sort by `orderDate`.

To create a compound index on the `customerId` and `orderDate` fields, use the following command:

```javascript
db.orders.createIndex({ customerId: 1, orderDate: 1 })
```

***Note:***

- This index will not be as efficient for queries that only filter by `orderDate` because the index is structured to prioritize `customerId` first.
  
- By using `compound indexes`, you can significantly improve the performance of your queries, especially when dealing with large datasets.

### Using Indexes for Sorting

Indexes can also be used to optimize sorting operations in MongoDB. When you create an index on a field or a set of fields, MongoDB can use that index to sort the results of a query efficiently.

***Example:***

Suppose you have a collection `products` with documents that include `category` and `price` fields. You can create an index on these fields to optimize queries that sort by `category` and `price`.

To create an index on the `category` and `price` fields, use the following command:

```javascript
db.products.createIndex({ category: 1, price: -1 })
```

in the above example

- **category: 1** specifies an ascending order for the `category` field.

- **price: -1** specifies a descending order for the `price` field.

***Explanation:***

The index `{ category: 1, price: -1 }` can be used to optimize the following types of queries:

1. Queries that sort by `category` and `price`:

   ```javascript
   db.products.find().sort({ category: 1, price: -1 })
   ```

2. Queries that filter by `category` and sort by `price`:

   ```javascript
   db.products.find({ category: "electronics" }).sort({ price: -1 })
   ```

By using indexes for sorting, you can significantly improve the performance of your queries, especially when dealing with large datasets. MongoDB can quickly locate the sorted order of documents using the index, avoiding the need for an in-memory sort operation.

### Default Index

- In MongoDB, every collection has a default index on the `_id field`.
  
- This index is created automatically when the collection is created and ensures that each document in the collection has a unique identifier.

***Example:***

Suppose you have a collection `users`. When you insert documents into this collection, MongoDB automatically creates an index on the `_id` field:

```javascript
db.users.insertMany([
  { _id: 1, name: "Alice", age: 30 },
  { _id: 2, name: "Bob", age: 25 },
  { _id: 3, name: "Charlie", age: 35 }
])
```

***Explanation:***

The default index on the `_id` field can be used to optimize the following types of queries:

1. Queries that filter by `_id`:

   ```javascript
   db.users.find({ _id: 1 })
   ```

2. Queries that sort by `_id`:

   ```javascript
   db.users.find().sort({ _id: 1 })
   ```

By using the default index, MongoDB can quickly locate documents by their unique identifier and efficiently sort documents based on the `_id` field.

**`getIndexes()` Method:**

The getIndexes() method in MongoDB is used to list all the indexes on a collection. This can be useful to verify which indexes exist and to understand how queries might be optimized.

```javascript
db.users.getIndexes()
```

The `getIndexes()` method returns an array of documents, where each document describes an index on the collection. Each document includes fields such as the index key, the index name, and other index options.

### Understanding Partial Filter Expressions

Partial filter expressions in MongoDB allow you to create indexes on a subset of documents in a collection. This can be useful for optimizing queries that only need to access a specific subset of documents, reducing the index size and improving performance.

**Creating an Index with a `PartialFilterExpression`:**

To create an index with a partial filter expression, you can use the `createIndex` method and specify the `partialFilterExpression` option.

```javascript
db.users.createIndex(
   { age: 1 },
   { partialFilterExpression: { age: { $gt: 18 } } }
)
```

In this example, an index is created on the `age` field, but only for documents where the `age` field is greater than 18.

**Applying the Partial Index:**

Once you have created a partial index, MongoDB will automatically use it for queries that match the partial filter expression. You don't need to do anything special in your query to use the partial index.

**Example Query Utilizing the Partial Index:**

Assuming you have created the partial index on the `age` field for documents where `age` is greater than 18, as shown earlier:

```javascript
db.users.createIndex(
   { age: 1 },
   { partialFilterExpression: { age: { $gt: 18 } } }
)
```

You can run a query that will utilize this partial index:

```javascript
db.users.find({ age: { $gt: 18 } })
```

In this query, MongoDB will use the partial index to quickly find documents where the `age` field is greater than 18, improving the query performance.

***Note:***  If you run a query that does not match the partial filter expression, MongoDB will not use the partial index. For example:

```javascript
db.users.find({ age: { $lte: 18 } })
```

In this case, MongoDB will not use the partial index because the query condition does not match the partial filter expression `(age > 18)`.

### Time to Live (TTL) Index in MongoDB

A `Time to Live (TTL)` index in MongoDB is a special type of index that allows you to automatically delete documents from a collection after a certain period of time. This is particularly useful for data that is only relevant for a limited period, such as session information, logs, or temporary data.

**Creating a TTL Index:**

To create a TTL index, you need to specify the field on which the TTL index will be created and the expiration time in seconds. The field must be of the BSON date type.

***Example:***

Let's create a TTL index on a collection named `sessions` where documents should expire 3600 seconds (1 hour) after the `createdAt` field.

```javascript
// Insert a document with a createdAt field
db.sessions.insertOne({
  sessionId: "abc123",
  userId: "user1",
  createdAt: new Date()
});

// Create a TTL index on the createdAt field with an expiration time of 3600 seconds
db.sessions.createIndex(
  { "createdAt": 1 },
  { expireAfterSeconds: 3600 }
);
```

***Explanation:***

1. **Insert a Document:** We insert a document into the `sessions` collection with a `createdAt` field set to the current date and time.

2. **Create a TTL Index:** We create a TTL index on the `createdAt` field with an expiration time of 3600 seconds. MongoDB will automatically delete documents from the `sessions` collection when the `createdAt` field is older than 3600 seconds.

***Notes:***

- The TTL index works in the background and may not delete expired documents immediately after they expire. The background task that removes expired documents runs every 60 seconds.

- The field used for the TTL index must be of the BSON date type. If the field is not a date, the TTL index will not work as expected.

By using TTL indexes, you can efficiently manage and clean up your collections without manual intervention.

### Understanding Covered Queries

- A covered query is a query in MongoDB where all the fields in the query are part of an index, and the fields returned in the results are also part of the same index.

- This means that MongoDB can fulfill the query using only the index, without having to read the actual documents from the collection. Covered queries are efficient because they reduce the amount of data that needs to be read and processed.

***Benefits of Covered Queries***

1. **Performance:** Since the query can be satisfied using only the index, it reduces the I/O operations needed to fetch documents from the collection.

2. **Efficiency:** Covered queries can be faster because they avoid scanning the entire collection and only access the index.

3. **Reduced Load:** By using indexes, covered queries can reduce the load on the database, leading to better overall performance.

***Example***

Let's consider a collection named `users` with documents that have the fields `username`, `email`, and `age`.

1. **Create an Index:** Create a compound index on the `username` and `email` fields.

   ```javascript
   db.users.createIndex({ username: 1, email: 1 });
   ```

2. Covered Query: Perform a query that only uses the fields in the index and returns only those fields.

   ```javascript
   // Query to find a user by username and email, returning only the   username and email fields
    db.users.find(
    { username: "johndoe", email: "johndoe@example.com" },
    { username: 1, email: 1, _id: 0 }
    ).explain("executionStats");
   ```

***Explanation***

1. **Create an Index:** We create a compound index on the `username` and `email` fields. This index will be used to cover the query.

2. **Covered Query:** The query searches for a user by `username` and `email`, and it only returns the `username` and `email` fields. The `_id` field is excluded from the results using `{ _id: 0 }`.

**Output of `explain()`**

The output of the `explain()` method will show that the query is a covered query. Look for the following indicators:

- **IXSCAN:** Indicates that the query used an index scan.
- **Index Only:** The `indexOnly` field in the explain output will be `true`, indicating that the query was covered by the index.

```javascript
{
  "queryPlanner": {
    "winningPlan": {
      "stage": "PROJECTION_COVERED",
      "inputStage": {
        "stage": "IXSCAN",
        "indexName": "username_1_email_1",
        "keyPattern": { "username": 1, "email": 1 },
        "indexOnly": true
      }
    }
  },
  "executionStats": {
    "executionSuccess": true,
    "nReturned": 1,
    "totalKeysExamined": 1,
    "totalDocsExamined": 0
  }
}
```

***Summary:***

- **Covered Query:** A query where all fields in the query and the results are part of an index.
- **Benefits:** Improved performance, efficiency, and reduced load on the database.
- **Example:** Create a compound index and perform a query that uses only the indexed fields.

Covered queries are a powerful feature in MongoDB that can significantly enhance query performance by leveraging indexes effectively.

### How MongoDB Rejects a Query Plan

MongoDB uses a query optimizer to evaluate multiple query plans and select the most efficient one. The optimizer generates several candidate plans and executes them to determine their performance. Plans that do not meet certain criteria or perform poorly are rejected.

***Example:***

Let's consider a collection named `products` with documents that have the fields `name`, `category`, and `price`.

1. **Indexes:** Create multiple indexes on the products collection.

   ```javascript
   db.products.createIndex({ name: 1 });
   db.products.createIndex({ category: 1 });
   db.products.createIndex({ price: 1 });
   ```

2. **Query:** Perform a query that could use multiple indexes.

   ```javascript
   db.products.find({ category: "electronics", price: { $lt: 1000 } }).explain("executionStats");
   ```

***Explanation:***

1. **Indexes:** We create three separate indexes on the name, category, and price fields.

2. **Query:** The query searches for products in the electronics category with a price less than 1000. This query can potentially use the category index, the price index, or a combination of both.

***Query Plan Evaluation:***

When the query is executed, MongoDB's query optimizer evaluates multiple candidate plans:

1. **Candidate Plans:** The optimizer generates candidate plans using different indexes and combinations of indexes.

2. **Execution:** The optimizer executes the candidate plans to gather performance statistics.

3. **Plan Selection:** The optimizer selects the most efficient plan based on the execution statistics.

***Output of `explain()`:***

The output of the explain() method will show the winning plan and the rejected plans.

```javascript
{
  "queryPlanner": {
    "winningPlan": {
      "stage": "FETCH",
      "inputStage": {
        "stage": "IXSCAN",
        "indexName": "category_1",
        "keyPattern": { "category": 1 },
        "indexBounds": {
          "category": ["[\"electronics\", \"electronics\"]"]
        }
      }
    },
    "rejectedPlans": [
      {
        "stage": "FETCH",
        "inputStage": {
          "stage": "IXSCAN",
          "indexName": "price_1",
          "keyPattern": { "price": 1 },
          "indexBounds": {
            "price": ["[MinKey, 1000)"]
          }
        }
      }
    ]
  },
  "executionStats": {
    "executionSuccess": true,
    "nReturned": 10,
    "totalKeysExamined": 10,
    "totalDocsExamined": 10
  }
}
```

***Explanation of Output***

- **Winning Plan:** The winning plan uses the `category` index to fetch documents.
  
- **Rejected Plans:** The rejected plans include a plan that uses the `price` index. This plan was rejected because it was less efficient than the winning plan.

**Summary:**

- **Query Optimizer:** MongoDB's query optimizer evaluates multiple candidate plans and selects the most efficient one.

- **Candidate Plans:** The optimizer generates and executes candidate plans using different indexes.

- **Plan Selection:** The optimizer selects the winning plan based on execution statistics and rejects less efficient plans.

### Multi-Key Indexes in MongoDB

- A multi-key index in MongoDB is an index that allows you to index fields that contain arrays.
  
- When you create a multi-key index on a field that contains an array, MongoDB creates separate index entries for each element of the array. This allows you to efficiently query documents based on the elements of the array.

***Example:***

Let's consider a collection named `orders` with documents that have the fields `orderId`, `customerName`, and `items` (where `items` is an array of product names).

1. **Insert Documents:** Insert sample documents into the orders collection.

   ```javascript
   db.orders.insertMany([
   { orderId: 1, customerName: "Alice", items: ["apple", "banana", "orange"] },
   { orderId: 2, customerName: "Bob", items: ["banana", "grape"] },
   { orderId: 3, customerName: "Charlie", items: ["apple", "grape", "watermelon"] }
    ]);
   ```

2. **Create a Multi-Key Index:** Create a multi-key index on the items field.

   ```javascript
   db.orders.createIndex({ items: 1 });
   ```

3. **Query Using the Multi-Key Index:** Perform a query to find orders that contain a specific item.

   ```javascript
   // Query to find orders that contain the item "apple"
   db.orders.find({ items: "apple" }).explain("executionStats");
   ```

***Explanation:***

1. **Insert Documents:** We insert three documents into the `orders` collection. Each document has an `items` field that contains an array of product names.

2. **Create a Multi-Key Index:** We create a multi-key index on the `items` field. MongoDB will create separate index entries for each element in the `items` array.

3. **Query Using the Multi-Key Index:** We perform a query to find orders that contain the item "apple". The multi-key index allows MongoDB to efficiently find documents where the `items` array contains "apple".

***Output of `explain()`***

The output of the `explain()` method will show that the query used the multi-key index.

```javascript
{
  "queryPlanner": {
    "winningPlan": {
      "stage": "FETCH",
      "inputStage": {
        "stage": "IXSCAN",
        "indexName": "items_1",
        "keyPattern": { "items": 1 },
        "indexBounds": {
          "items": ["[\"apple\", \"apple\"]"]
        }
      }
    }
  },
  "executionStats": {
    "executionSuccess": true,
    "nReturned": 2,
    "totalKeysExamined": 2,
    "totalDocsExamined": 2
  }
}
```

***Explanation:***

- **Winning Plan:** The winning plan uses the `items` multi-key index to fetch documents.

- **Index Scan:** The `IXSCAN` stage indicates that the query used an index scan on the `items` index.

- **Index Bounds:** The `indexBounds` field shows that the query searched for the item "apple" within the `items` array.

***Summary:***

- **Multi-Key Index:** An index that allows you to index fields containing arrays, creating separate index entries for each element.

- **Example:** Create a multi-key index on the `items` field of the `orders` collection and query for documents containing a specific item.

- **Efficiency:** Multi-key indexes enable efficient querying of documents based on array elements, improving query performance.

Multi-key indexes are a powerful feature in MongoDB that allow you to efficiently query documents with array fields, making them essential for handling complex data structures.

### Text Indexes in MongoDB

Text indexes in MongoDB allow you to perform text search queries on string content within your documents. They are particularly useful for searching large collections of text data, such as articles, blog posts, or product descriptions.

**Creating a Text Index:**

To create a text index, you use the `createIndex` method with the `text` index type. You can create a text index on a single field or multiple fields.

***Example:***

Let's consider a collection named `articles` with documents that have the fields `title` and `content`.

1. **Insert Documents:** Insert sample documents into the articles collection.

   ```javascript
   db.articles.insertMany([
   { title: "Introduction to MongoDB", content: "MongoDB is a NoSQL database that offers high performance and scalability." },
   { title: "Advanced MongoDB Queries", content: "Learn how to perform advanced queries in MongoDB, including text search and aggregation." },
   { title: "MongoDB Indexing", content: "Indexing in MongoDB improves query performance by allowing efficient data retrieval." }
   ]);
   ```

2. **Create a Text Index:** Create a text index on the title and content fields.

   ```javascript
   db.articles.createIndex({ title: "text", content: "text" });
   ```

3. **Query Using the Text Index:** Perform a text search query to find articles that contain specific keywords.

   ```javascript
   // Query to find articles that contain the keyword "MongoDB"
   db.articles.find({ $text: { $search: "MongoDB" } }).explain("executionStats");
   ```

***Explanation:***

1. **Insert Documents:** We insert three documents into the articles collection. Each document has a title and content field containing text data.

2. **Create a Text Index:** We create a text index on the title and content fields. This allows MongoDB to perform text search queries on these fields.

3. **Query Using the Text Index:** We perform a text search query to find articles that contain the keyword "MongoDB". The $text operator is used to specify the text search query.

**Output of `explain()`:**

The output of the explain() method will show that the query used the text index.

```javascript
{
  "queryPlanner": {
    "winningPlan": {
      "stage": "TEXT",
      "indexName": "title_text_content_text",
      "inputStage": {
        "stage": "FETCH"
      }
    }
  },
  "executionStats": {
    "executionSuccess": true,
    "nReturned": 3,
    "totalKeysExamined": 3,
    "totalDocsExamined": 3
  }
}
```

***Explanation of Output:***

- **Winning Plan:** The winning plan uses the `TEXT` stage, indicating that the query used a text index.

- **Index Name:** The `indexName` field shows the name of the text index used for the query.

- **Execution Stats:** The `executionStats` section provides details about the query execution, including the number of documents returned and examined.

***Summary***

- **Text Index:** An index that allows you to perform text search queries on string content within your documents.

- **Example:** Create a text index on the `title` and `content` fields of the `articles` collection and perform a text search query.

- **Efficiency:** Text indexes enable efficient text search queries, improving the performance of search operations on large collections of text data.

Text indexes are a powerful feature in MongoDB that allow you to efficiently search and retrieve documents based on text content, making them essential for applications that require full-text search capabilities.

### Text Indexes and Sorting in MongoDB

When using text indexes in MongoDB, you can perform text search queries and sort the results. However, there are some limitations and considerations to keep in mind when combining text search with sorting.

***Example:***

Let's continue with the `articles` collection from the previous example, which has a text index on the `title` and content `fields`.

1. **Insert Documents:** Insert sample documents into the `articles` collection.

   ```javascript
   db.articles.insertMany([
   { title: "Introduction to MongoDB", content: "MongoDB is a NoSQL database that offers high performance and scalability.", date: new Date("2023-01-01") },
   { title: "Advanced MongoDB Queries", content: "Learn how to perform advanced queries in MongoDB, including text search and aggregation.", date: new Date("2023-02-01") },
   { title: "MongoDB Indexing", content: "Indexing in MongoDB improves query performance by allowing efficient data retrieval.", date: new Date("2023-03-01") }
   ]);
   ```

2. **Create a Text Index:** Create a text index on the title and content fields.

   ```javascript
   db.articles.createIndex({ title: "text", content: "text" });
   ```

3. **Query Using the Text Index and Sort by Date:** Perform a text search query to find articles that contain specific keywords and sort the results by the date field.

   ```javascript
   // Query to find articles that contain the keyword "MongoDB" and sort by date in descending order
   db.articles.find({ $text: { $search: "MongoDB" } }).sort({ date: -1 }).explain("executionStats");
   ```

***Explanation:***

1. **Insert Documents:** We insert three documents into the articles collection. Each document has a `title`, `content`, and `date` field.

2. **Create a Text Index:** We create a text index on the `title` and `content` fields. This allows MongoDB to perform text search queries on these fields.

3. **Query Using the Text Index and Sort by Date:** We perform a text search query to find articles that contain the keyword "MongoDB" and sort the results by the date field in descending order. The `sort` method is used to specify the sorting order.

**Output of `explain()`**

The output of the explain() method will show that the query used the text index and sorted the results.

```javascript
{
  "queryPlanner": {
    "winningPlan": {
      "stage": "SORT",
      "sortPattern": { "date": -1 },
      "inputStage": {
        "stage": "TEXT",
        "indexName": "title_text_content_text",
        "inputStage": {
          "stage": "FETCH"
        }
      }
    }
  },
  "executionStats": {
    "executionSuccess": true,
    "nReturned": 3,
    "totalKeysExamined": 3,
    "totalDocsExamined": 3
  }
}
```

***Explanation of Output:***

- **Winning Plan:** The winning plan includes a `SORT` stage, indicating that the results were sorted by the `date` field.

- **Text Index:** The `TEXT` stage shows that the query used the text index.

- **Execution Stats:** The `executionStats` section provides details about the query execution, including the number of documents returned and examined.

***Consideration:***

- **Sort Order:** When combining text search with sorting, MongoDB may need to perform an in-memory sort if the sort order is not supported by an index. This can impact performance for large result sets.

- **Index Usage:** To optimize performance, consider creating compound indexes that include the text index fields and the sort fields.

***Summary:***

- **Text Index:** Allows you to perform text search queries on string content within your documents.

- **Sorting:** You can combine text search with sorting, but be aware of potential performance impacts.

Text indexes and sorting are powerful features in MongoDB that enable efficient text search and result ordering, making them essential for applications that require full-text search capabilities with sorted results.

### Combining Text Index with Other Indexes in MongoDB

- When you need to perform text search queries and also sort or filter by other fields, you can create compound indexes that include both text index fields and other fields.

- This can help optimize performance by allowing MongoDB to use the index for both the text search and the sorting/filtering operations.

***Example:***

Let's continue with the `articles` collection, which has documents with the fields `title`, `content`, and `date`.

1. Insert Documents: Insert sample documents into the articles collection.

   ```javascript
   db.articles.insertMany([
   { title: "Introduction to MongoDB", content: "MongoDB is a NoSQL database that offers high performance and scalability.", date: new Date("2023-01-01") },
   { title: "Advanced MongoDB Queries", content: "Learn how to perform advanced queries in MongoDB, including text search and aggregation.", date: new Date("2023-02-01") },
   { title: "MongoDB Indexing", content: "Indexing in MongoDB improves query performance by allowing efficient data retrieval.", date: new Date("2023-03-01") }
   ]);
   ```

2. **Create a Compound Text Index:** Create a compound index that includes the text index fields and the date field.

   ```javascript
   db.articles.createIndex(
   { title: "text", content: "text", date: 1 }
   );
   ```

3. **Query Using the Compound Text Index:** Perform a text search query to find articles that contain specific keywords and sort the results by the date field.

   ```javascript
   // Query to find articles that contain the keyword "MongoDB" and sort by date in descending order
   db.articles.find({ $text: { $search: "MongoDB" } }).sort({ date: -1 }).explain("executionStats");
   ```

***Explanation:***

1. **Insert Documents:** We insert three documents into the `articles` collection. Each document has a `title`, `content`, and `date` field.

2. **Create a Compound Text Index:** We create a compound index that includes the `title` and `content` fields as a text index and the `date` field as a regular index. This allows MongoDB to use the index for both text search and sorting by date.

3. **Query Using the Compound Text Index:** We perform a text search query to find articles that contain the keyword "MongoDB" and sort the results by the date field in descending order. The `sort` method is used to specify the sorting order.

**Output of `explain()`**

The output of the `explain()` method will show that the query used the compound text index and sorted the results.

```javascript
{
  "queryPlanner": {
    "winningPlan": {
      "stage": "SORT",
      "sortPattern": { "date": -1 },
      "inputStage": {
        "stage": "TEXT",
        "indexName": "title_text_content_text_date_1",
        "inputStage": {
          "stage": "FETCH"
        }
      }
    }
  },
  "executionStats": {
    "executionSuccess": true,
    "nReturned": 3,
    "totalKeysExamined": 3,
    "totalDocsExamined": 3
  }
}
```

**Explanation of Output:**

- **Winning Plan:** The winning plan includes a `SORT` stage, indicating that the results were sorted by the `date` field.

- **Text Index:** The `TEXT` stage shows that the query used the compound text index.

- **Execution Stats:** The `executionStats` section provides details about the query execution, including the number of documents returned and examined.

***Summary***

- **Compound Text Index:** Allows you to combine text search with sorting or filtering by other fields.

- **Efficiency:** Compound text indexes enable efficient text search queries with sorting or filtering, improving query performance.

By creating compound text indexes, you can optimize your MongoDB queries to handle both text search and additional sorting or filtering requirements, making your application more efficient and responsive.

### Excluding Words in Text Index Queries in MongoDB

MongoDB's text search feature allows you to exclude certain words from your search results using the `-` (minus) operator. This can be useful when you want to filter out documents that contain specific terms.

***Example***

Let's continue with the `articles` collection, which has documents with the fields `title`, `content`, and `date`.

1. **Insert Documents:** Insert sample documents into the articles collection.

   ```javascript
   db.articles.insertMany([
   { title: "Introduction to MongoDB", content: "MongoDB is a NoSQL database that offers high performance and scalability.", date: new Date("2023-01-01") },
   { title: "Advanced MongoDB Queries", content: "Learn how to perform advanced queries in MongoDB, including text search and aggregation.", date: new Date("2023-02-01") },
   { title: "MongoDB Indexing", content: "Indexing in MongoDB improves query performance by allowing efficient data retrieval.", date: new Date("2023-03-01") },
   { title: "SQL vs NoSQL", content: "This article compares SQL and NoSQL databases, highlighting their differences and use cases.", date: new Date("2023-04-01") }
   ]);
   ```

2. **Create a Text Index:** Create a text index on the `title` and `content` fields.

   ```javascript
   db.articles.createIndex({ title: "text", content: "text" });
   ```  

3. **Query Using the Text Index and Exclude Words:** Perform a text search query to find articles that contain specific keywords but exclude certain words.

   ```javascript
   // Query to find articles that contain the keyword "MongoDB" but exclude the word "NoSQL"
   db.articles.find({ $text: { $search: "MongoDB -NoSQL" } }).explain("executionStats");
   ```

**Explanation:**

- **Insert Documents:** We insert four documents into the `articles` collection. Each document has a `title`, `content`, and `date` field.
  
- **Create a Text Index:** We create a text index on the `title` and `content` fields. This allows MongoDB to perform text search queries on these fields.
  
- **Query Using the Text Index and Exclude Words:** We perform a text search query to find articles that contain the keyword "MongoDB" but exclude the word "NoSQL". The `-` (minus) operator is used to exclude the word "NoSQL" from the search results.

**Output of `explain()`**

The output of the `explain()` method will show that the query used the text index and excluded the specified word.

```javascript
{
  "queryPlanner": {
    "winningPlan": {
      "stage": "TEXT",
      "indexName": "title_text_content_text",
      "inputStage": {
        "stage": "FETCH"
      }
    }
  },
  "executionStats": {
    "executionSuccess": true,
    "nReturned": 2,
    "totalKeysExamined": 2,
    "totalDocsExamined": 2
  }
}
```

**Explanation Of Output:**

- **Winning Plan:** The winning plan uses the `TEXT` stage, indicating that the query used the text index.

- **Text Index:** The `indexName` field shows the name of the text index used for the query.

- **Execution Stats:** The `executionStats` section provides details about the query execution, including the number of documents returned and examined.

***Summary***

- **Excluding Words:** Use the `-` (minus) operator in text search queries to exclude specific words from the search results.

- **Efficiency:** Excluding words in text search queries allows you to refine your search results and improve the relevance of the returned documents.

By using the `-` (minus) operator in text search queries, you can exclude unwanted terms and obtain more precise search results, making your application more effective and user-friendly.

### Setting the Default Language and Using Weights in MongoDB Text Indexes

MongoDB allows you to set a default language for text indexes and assign weights to different fields to influence the relevance of search results. This can help you fine-tune your text search queries to better match your application's requirements.

**Setting the Default Language:**

By default, MongoDB uses `English` for text indexes. You can change the default language by specifying the `default_language` option when creating the text index.

**Using Weights:**

Weights allow you to assign different levels of importance to different fields in a text index. Fields with higher weights will have a greater impact on the relevance score of search results.

***Example:***

Let's continue with the articles `collection`, which has documents with the fields `title`, `content`, and `date`.

1. **Insert Documents:** Insert sample documents into the articles collection.

   ```javascript
   db.articles.insertMany([
   { title: "Introduction to MongoDB", content: "MongoDB is a NoSQL database that offers high performance and scalability.", date: new Date("2023-01-01") },
   { title: "Advanced MongoDB Queries", content: "Learn how to perform advanced queries in MongoDB, including text search and aggregation.", date: new Date("2023-02-01") },
   { title: "MongoDB Indexing", content: "Indexing in MongoDB improves query performance by allowing efficient data retrieval.", date: new Date("2023-03-01") },
   { title: "SQL vs NoSQL", content: "This article compares SQL and NoSQL databases, highlighting their differences and use cases.", date: new Date("2023-04-01") }
   ]);
   ```

2. **Create a Text Index with Default Language and Weights:** Create a text index on the title and content fields, set the default language to Spanish, and assign weights to the fields.

   ```javascript
   db.articles.createIndex(
   { title: "text", content: "text" },
   {
    default_language: "spanish",
    weights: { title: 10, content: 5 }
   }
   );
   ```

3. **Query Using the Text Index:** Perform a text search query to find articles that contain specific keywords.

   ```javascript
   // Query to find articles that contain the keyword "MongoDB"
   db.articles.find({ $text: { $search: "MongoDB" } }).explain("executionStats");
   ```

**Explanation:**

1. **Insert Documents:** We insert four documents into the `articles` collection. Each document has a `title`, `content`, and `date` field.

2. **Create a Text Index with Default Language and Weights:** We create a text index on the `title` and `content` fields. We set the default language to Spanish and assign weights to the fields (`title` has a weight of 10, and `content` has a weight of 5). This means that matches in the `title` field will be considered more relevant than matches in the `content` field.

3. **Query Using the Text Index:** We perform a text search query to find articles that contain the keyword "MongoDB". The query will use the text index with the specified default language and weights.

**Output Of explain():**

The output of the `explain()` method will show that the query used the text index with the specified default language and weights.

```javascript
{
  "queryPlanner": {
    "winningPlan": {
      "stage": "TEXT",
      "indexName": "title_text_content_text",
      "inputStage": {
        "stage": "FETCH"
      }
    }
  },
  "executionStats": {
    "executionSuccess": true,
    "nReturned": 3,
    "totalKeysExamined": 3,
    "totalDocsExamined": 3
  }
}
```

***Explanation Of Output:***

- **Winning Plan:** The winning plan uses the `TEXT` stage, indicating that the query used the text index.

- **Text Index:** The `indexName` field shows the name of the text index used for the query.

- **Execution Stats:** The `executionStats` section provides details about the query execution, including the number of documents returned and examined.

**Summary:**

- **Default Language:** You can set the default language for text indexes using the `default_language` option.

- **Weights:** Assign weights to different fields in a text index to influence the relevance of search results.
  
- **Example:** Create a text index on the `title` and `content` fields of the `articles` collection, set the default language to Spanish, and assign weights to the fields.

By setting the default language and using weights in text indexes, you can fine-tune your text search queries to better match your application's requirements, improving the relevance and accuracy of search results.

### Building Indexes in MongoDB

Indexes in MongoDB are special data structures that store a small portion of the collection's data set in an easy-to-traverse form. The index stores the value of a specific field or set of fields, ordered by the value of the field. Indexes support the efficient execution of queries in MongoDB.

**Types of Indexes:**

1. **Single Field Index:** Indexes on a single field.
2. **Compound Index:** Indexes on multiple fields.
3. **Multikey Index:** Indexes on array fields.
4. **Text Index:** Indexes for text search.
5. **Geospatial Index:** Indexes for geospatial queries.
6. **Hashed Index:** Indexes that use a hash of the field value.

***Example***

Let's consider a collection named `products` with documents that have the fields `name`, `category`, and `price`.

1. **Insert Documents:** Insert sample documents into the `products` collection.

   ```javascript
   db.products.insertMany([
   { name: "Laptop", category: "Electronics", price: 1000 },
   { name: "Smartphone", category: "Electronics", price: 500 },
   { name: "Tablet", category: "Electronics", price: 300 },
   { name: "Headphones", category: "Accessories", price: 100 },
   { name: "Charger", category: "Accessories", price: 20 }
   ]);
   ```

2. **Create a Single Field Index:** Create an index on the `name` field.

   ```javascript
   db.products.createIndex({ name: 1 });
   ```

3. **Create a Compound Index:** Create an index on the `category` and `price` fields.

   ```javascript
   db.products.createIndex({ category: 1, price: -1 });
   ```

4. **Create a Multikey Index:** Create an index on the `tags` field, which is an array.

   ```javascript
   db.products.insertMany([
   { name: "Laptop", tags: ["electronics", "computer"] },
   { name: "Smartphone", tags: ["electronics", "mobile"] }
   ]);

   db.products.createIndex({ tags: 1 });
   ```

5. **Create a Text Index:** Create a text index on the `description` field.

   ```javascript
   db.products.insertMany([
   { name: "Laptop", description: "A high-performance laptop for all your computing needs." },
   { name: "Smartphone", description: "A smartphone with the latest features and technology." }
   ]);

   db.products.createIndex({ description: "text" });
   ```
  
6. **Create a Geospatial Index:** Create a geospatial index on the `location` field.

   ```javascript
   db.products.insertMany([
   { name: "Store1", location: { type: "Point", coordinates: [40.7128, -74.0060] } },
   { name: "Store2", location: { type: "Point", coordinates: [34.0522, -118.2437] } }
   ]);

   db.products.createIndex({ location: "2dsphere" });
   ```

7. **Create a Hashed Index:** Create a hashed index on the `userId` field.

   ```javascript
   db.products.insertMany([
   { name: "Laptop", userId: "user123" },
   { name: "Smartphone", userId: "user456" }
   ]);

   db.products.createIndex({ userId: "hashed" });
   ```

**Explanation:**

1. **Insert Documents:** We insert sample documents into the `products` collection.

2. **Single Field Index:** We create an index on the `name` field to support efficient queries on product names.

3. **Compound Index:** We create an index on the `category` and `price` fields to support efficient queries that filter by category and sort by price.

4. **Multikey Index:** We create an index on the `tags` field, which is an array, to support efficient queries on tags.

5. **Text Index:** We create a text index on the `description` field to support text search queries.

6. **Geospatial Index:** We create a geospatial index on the `location` field to support geospatial queries.

7. **Hashed Index:** We create a hashed index on the `userId` field to support efficient equality queries on user IDs.

***Summary***

- **Single Field Index:** Indexes on a single field.
- **Compound Index:** Indexes on multiple fields.
- **Multikey Index:** Indexes for text search.
- **Geospatial Index:** Indexes for geospatial queries.
- **Hashed Index:** Indexes that use a hash of the field value.

By creating appropriate indexes, you can significantly improve the performance of your MongoDB queries, making your application more efficient and responsive.

### Importing JSON to MongoDB Shell

You can import JSON data into MongoDB using the `mongoimport` tool, which is a part of the MongoDB Database Tools. This tool allows you to import data from JSON, CSV, or TSV files into a MongoDB collection.

**Example:**

Let's assume you have a JSON file named `products.json` with the following content:

```javascript
[
  { "name": "Laptop", "category": "Electronics", "price": 1000 },
  { "name": "Smartphone", "category": "Electronics", "price": 500 },
  { "name": "Tablet", "category": "Electronics", "price": 300 },
  { "name": "Headphones", "category": "Accessories", "price": 100 },
  { "name": "Charger", "category": "Accessories", "price": 20 }
]
```

***Steps to Import JSON Data:***

1. **Open Command Prompt:** Open the Command Prompt or Terminal on your machine.

2. **Run `mongoimport` Command:** Use the `mongoimport` command to import the JSON file into a MongoDB collection.

   ```javascript
   mongoimport --db mydatabase --collection products --file products.json --jsonArray
   ```

**Explanation:**

- `--db mydatabase:` Specifies the database to import the data into (mydatabase).

- `--collection products:` Specifies the collection to import the data into (products).

- `--file products.json:` Specifies the path to the JSON file (products.json).

- `--jsonArray:` Indicates that the input file contains an array of JSON documents.

**Verifying the Import:**

After running the `mongoimport` command, you can verify that the data has been imported successfully by querying the products collection in the MongoDB shell.

1. **Open MongoDB Shell:** Open the MongoDB shell by running the `mongosh` command.

   ```javascript
   mongosh
   ```

2. **Switch to the Database:** Switch to the database where the data was imported.

   ```javascript
   use mydatabase
   ```

3. **Query the Collection:** Query the products collection to verify the imported data.

   ```javascript
   db.products.find().pretty()
   ```

***Expected Output:***

The output should display the documents imported from the JSON file:

```javascript
{
  "_id": ObjectId("..."),
  "name": "Laptop",
  "category": "Electronics",
  "price": 1000
}
{
  "_id": ObjectId("..."),
  "name": "Smartphone",
  "category": "Electronics",
  "price": 500
}
{
  "_id": ObjectId("..."),
  "name": "Tablet",
  "category": "Electronics",
  "price": 300
}
{
  "_id": ObjectId("..."),
  "name": "Headphones",
  "category": "Accessories",
  "price": 100
}
{
  "_id": ObjectId("..."),
  "name": "Charger",
  "category": "Accessories",
  "price": 20
}
```

**Summary:**

- **`mongoimport` Tool:** Use the mongoimport tool to import JSON data into MongoDB.

- **Command:** Run the `mongoimport` command with appropriate options to specify the database, collection, and JSON file.

- **Verification:** Verify the imported data by querying the collection in the MongoDB shell.

By following these steps, you can easily import JSON data into MongoDB and ensure that it has been imported correctly.

### More Details

For more information, refer to the official MongoDB documentation:

- **Partial Filter Expressions:** [Partial Filter Expressions](https://docs.mongodb.com/manual/core/index-partial/)
- **Supported Default Languages:** [Text Search Languages](https://docs.mongodb.com/manual/reference/text-search-languages/#text-search-languages)
- **Using Different Languages in the Same Index:** [Create a Text Index for a Collection in Multiple Languages](https://docs.mongodb.com/manual/tutorial/specify-language-for-text-index/#create-a-text-index-for-a-collection-in-multiple-languages)

## 4. Geospatial Data in MongoDB

- Geospatial queries in MongoDB allow you to store and query data that represents geographical locations.
  
- MongoDB supports various geospatial data types and queries, including 2D and 2DSphere indexes for different types of geospatial data.

### Adding GeoJSON Data

- GeoJSON is a format for encoding a variety of geographic data structures using JavaScript Object Notation (JSON).

- It supports various types of geometries such as `Point`, `LineString`, `Polygon`, etc.

**Example of GeoJSON Data:**

```javascript
{
  "type": "Point",
  "coordinates": [20.295390834883428, 85.82182190544279]
}
```

**Inserting GeoJSON Data into MongoDB:**

```javascript
// Insert GeoJSON data into a collection
db.places.insertOne({
  name: "Central Park",
  location: {
    type: "Point",
    coordinates: [20.295390834883428, 85.82182190544279]
  }
});
```

***Expected Output:***

```javascript
{
  acknowledged: true,
  insertedId: ObjectId('66f2e417278fc89d9ec73bf8')
}
```

***Verify the Data***

```javascript
db.places.find()
```

***Expected Output:***

```javascript
[
  {
    _id: ObjectId('66f2e417278fc89d9ec73bf8'),
    name: 'Central Park',
    location: { type: 'Point', coordinates: [ 20.295390834883428, 85.82182190544279] }
  }
]
```

### Creating a Geospatial Index

```javascript
// Create a 2dsphere index on the location field
db.places.createIndex({ location: "2dsphere" });
```

The selected code creates a geospatial index on the `location` field of the places collection in MongoDB.

**Breakdown:**

1. **Collection:** `db.places`

   - This specifies the collection on which the index is being created. In this case, it is the `places` collection.

2. **createIndex Method:** `createIndex({ location: "2dsphere" })`

   - The `createIndex` method is used to create an index on a specified field or fields in a collection.

3. **Index Specification:** `{ location: "2dsphere" }`

   - This specifies the field to be indexed and the type of index to be created. Here, the `location` field is being indexed with a `2dsphere` index.

**2dsphere Index:**

- **Purpose:** A `2dsphere` index supports queries that calculate geometries on an Earth-like sphere. It is used for storing and querying GeoJSON data, which includes points, lines, and polygons.

- **Usage:** This type of index is essential for performing geospatial queries, such as finding documents near a specific point, within a certain distance, or within a specific polygon.

### Querying GeoJSON Data

```javascript
// Find places near a specific point
db.places.find({
  location: {
    $near: {
      $geometry: {
        type: "Point",
        coordinates: [20.295390834883428, 85.82182190544279]
      },
      $maxDistance: 5000 // 5 kilometers
    }
  }
});
```

**Breakdown:**

1. **Collection:** `db.places.find()`

   - This specifies that we are querying the `places` collection.

2. **Query Condition:** `{ location: { $near: { ... } } }`

   - This condition is used to find documents where the `location` field is near a specified point.

3. **`$near Operator:`** `$near: { $geometry: { ... }, $maxDistance: 5000 }`

   - The `$near` operator is used to find documents that are close to a specified point. It requires a `$geometry` subfield and can optionally include a `$maxDistance` subfield.

4. **`$geometry Subfield:`** `{ $geometry: { type: "Point", coordinates: [20.295390834883428, 85.82182190544279] } }`

   - The `$geometry` subfield specifies the type of the geometry and its coordinates. In this case, it is a `Point` with coordinates `[20.295390834883428, 85.82182190544279]` (longitude , latitude).

5. **`$maxDistance Subfield:`** `$maxDistance: 5000`

   - The `$maxDistance` subfield specifies the maximum distance from the point, in meters. Here, it is set to `5000` meters (5 kilometers).

This query finds all documents in the `places` collection where the `location` field is within 5 kilometers of the point with coordinates `[20.295390834883428, 85.82182190544279]`. The `location` field must be indexed with a `2dsphere` index for this query to work efficiently.

### Finding Places Inside a Certain Area With `$geoWithin`

To find places within a certain area, you can use the `$geoWithin` operator in MongoDB. This operator allows you to specify a GeoJSON polygon that represents the area of interest.

**Example of a Polygon:**
A polygon is defined by an array of coordinates that form a closed loop. Here is an example of a GeoJSON polygon:

```javascript
{
  "type": "Polygon",
  "coordinates": [
    [
      [85.82182190544279, 20.295390834883428],
      [85.82282190544279, 20.295390834883428],
      [85.82282190544279, 20.296390834883428],
      [85.82182190544279, 20.296390834883428],
      [85.82182190544279, 20.295390834883428]
    ]
  ]
}
```

**Inserting GeoJSON Data into MongoDB:**

```javascript
// Insert GeoJSON data into a collection
db.places.insertMany([
  { name: "Place 1", location: { type: "Point", coordinates: [85.82182190544279, 20.295390834883428] } },
  { name: "Place 2", location: { type: "Point", coordinates: [85.82282190544279, 20.295390834883428] } },
  { name: "Place 3", location: { type: "Point", coordinates: [85.82282190544279, 20.296390834883428] } }
]);
```

**Creating a Geospatial Index:**

```javascript
// Create a 2dsphere index on the location field
db.places.createIndex({ location: "2dsphere" });
```

**Querying GeoJSON Data to Find Places Within a Specified Area:**

```javascript
// Define the polygon representing the area
const polygon = {
  type: "Polygon",
  coordinates: [
    [
      [85.82182190544279, 20.295390834883428],
      [85.82282190544279, 20.295390834883428],
      [85.82282190544279, 20.296390834883428],
      [85.82182190544279, 20.296390834883428],
      [85.82182190544279, 20.295390834883428]
    ]
  ]
};

// Find places within the specified polygon
db.places.find({
  location: {
    $geoWithin: {
      $geometry: polygon
    }
  }
});
```

***Expected Output:***

```javascript
[
  { "_id": ObjectId("..."), "name": "Place 1", "location": { "type": "Point", "coordinates": [85.82182190544279, 20.295390834883428] } },
  { "_id": ObjectId("..."), "name": "Place 2", "location": { "type": "Point", "coordinates": [85.82282190544279, 20.295390834883428] } },
  { "_id": ObjectId("..."), "name": "Place 3", "location": { "type": "Point", "coordinates": [85.82282190544279, 20.296390834883428] } }
]
```

### Finding Out if a User is Inside a Specific Area with `$geoIntersects`

To determine if a user is inside a specific area, you can use the `$geoIntersects` operator in MongoDB. This operator allows you to specify a GeoJSON polygon that represents the area of interest and check if a user's location intersects with that polygon.

**Example of a Polygon:**

A polygon is defined by an array of coordinates that form a closed loop. Here is an example of a GeoJSON polygon:

```javascript
{
  "type": "Polygon",
  "coordinates": [
    [
      [85.82182190544279, 20.295390834883428],
      [85.82282190544279, 20.295390834883428],
      [85.82282190544279, 20.296390834883428],
      [85.82182190544279, 20.296390834883428],
      [85.82182190544279, 20.295390834883428]
    ]
  ]
}
```

**Inserting User Location Data into MongoDB:**

```javascript
// Insert user location data into a collection
db.users.insertOne({
  name: "User 1",
  location: { type: "Point", coordinates: [85.82182190544279, 20.295390834883428] }
});
```

**Creating a Geospatial Index:**

```javascript
// Create a 2dsphere index on the location field
db.users.createIndex({ location: "2dsphere" });
```

**Query to Check if User is Inside the Specified Area Using `$geoIntersects`:**

```javascript
// Define the polygon representing the area
const polygon = {
  type: "Polygon",
  coordinates: [
    [
      [85.82182190544279, 20.295390834883428],
      [85.82282190544279, 20.295390834883428],
      [85.82282190544279, 20.296390834883428],
      [85.82182190544279, 20.296390834883428],
      [85.82182190544279, 20.295390834883428]
    ]
  ]
};

// Find users whose locations intersect with the specified polygon
db.users.find({
  location: {
    $geoIntersects: {
      $geometry: polygon
    }
  }
});
```

**Expected Output:**

```javascript
[
  {
    _id: ObjectId('66f2f15f278fc89d9ec73bf9'),
    name: 'User 1',
    location: {
      type: 'Point',
      coordinates: [ 85.82182190544279, 20.295390834883428 ]
    }
  }
]
```

### Finding Places Within Certain Radius With `$centerSphere`

To find places within a certain radius using the MongoDB shell, you can use the $geoWithin operator along with the **` $centerSphere`** operator. Here's how you can do it:

**Example:**

Assume you have a collection named `places` with documents that include a `location` field containing GeoJSON data for points.

```javascript
{
  "_id": 1,
  "name": "Place 1",
  "location": {
    "type": "Point",
    "coordinates": [85.82182190544279, 20.295390834883428]
  }
},
 {
    "_id": 2,
    "name": "Place 2",
    "location": {
      "type": "Point",
      "coordinates": [85.82282190544279, 20.296390834883428]
    }
  }
```

**Create Geospatial Index:**

```javascript
db.places.createIndex({ location: "2dsphere" });
```

**Query to Find Places Within a Certain Radius:**

```javascript
const center = [85.82182190544279, 20.295390834883428]; // Center point coordinates
const radiusInMeters = 1000; // Radius in meters
const radiusInRadians = radiusInMeters / 6378100; // Convert meters to radians (Earth's radius in meters)

db.places.find({
  location: {
    $geoWithin: {
      $centerSphere: [center, radiusInRadians]
    }
  }
}).pretty();
```

Uses `$geoWithin` and `$centerSphere` to find places within the specified radius from the center point.

**Expected Output:**

```javascript
[
  {
    "_id": 1,
    "name": "Place 1",
    "location": {
      "type": "Point",
      "coordinates": [85.82182190544279, 20.295390834883428]
    }
  },
  {
    "_id": 2,
    "name": "Place 2",
    "location": {
      "type": "Point",
      "coordinates": [85.82282190544279, 20.296390834883428]
    }
  }
]
```

The output will include all documents from the `places` collection that have a `location` field within the specified radius from the center point.

**For more information, refer to the Official docs:**

- **Geospatial Queries:** [official MongoDB documentation](https://docs.mongodb.com/manual/geospatial-queries/)
  
- **Geospatial Query Operators:** [Geospatial Query Operators](https://docs.mongodb.com/manual/reference/operator/query-geospatial/).

## 5. Understanding Aggregation Framework

**What is Aggregation Framework in MongoDB:**

- The Aggregation Framework in MongoDB is a powerful tool for performing data processing and transformation operations on collections of documents.
  
- It allows you to perform complex queries and transformations on your data in a pipeline fashion, where each stage of the pipeline processes the input and passes the result to the next stage.

**Key Concepts:**

1. **Pipeline:** A sequence of stages where each stage transforms the documents as they pass through.

2. **Stages:** Each stage in the pipeline performs an operation on the input documents. Common stages include:

   - `$match:` Filters documents to pass only those that match the specified condition(s).
  
   - `$group:` Groups input documents by a specified identifier expression and applies the accumulator expressions.
  
   - `$project:` Reshapes each document in the stream, such as by adding, removing, or renaming fields.
  
   - `$sort:` Sorts the documents.

   - `$limit:` Limits the number of documents.
  
   - `$skip:` Skips over a specified number of documents.
  
   - `$unwind:` Deconstructs an array field from the input documents to output a document for each element.

**Use Cases:**

- Data transformation and reshaping.
  
- Calculating aggregated values like sums, averages, and counts.
  
- Filtering and sorting data.
  
- Joining data from multiple collections.

**Example:**

We'll use a collection named `orders` with the following documents:

```javascript
[
  { "_id": 1, "cust_id": "A123", "status": "A", "amount": 100, "items": ["item1", "item2"] },
  { "_id": 2, "cust_id": "B456", "status": "B", "amount": 200, "items": ["item3"] },
  { "_id": 3, "cust_id": "A123", "status": "A", "amount": 150, "items": ["item1", "item4"] },
  { "_id": 4, "cust_id": "C789", "status": "C", "amount": 300, "items": ["item2", "item3"] },
  { "_id": 5, "cust_id": "A123", "status": "B", "amount": 50, "items": ["item4"] }
]
```

***Common MongoDB aggregation stages with examples***

1. `$match:`***Filters documents to pass only those that match the specified condition(s).***

   ```javascript
   db.orders.aggregate([
   { $match: { status: "A" } }
   ])
   ```

   **Explanation:** This stage filters documents where the `status` is "A".

   **Expected Output:**

   ```javascript
   [
    { "_id": 1, "cust_id": "A123", "status": "A", "amount": 100, "items": ["item1", "item2"] },
    { "_id": 3, "cust_id": "A123", "status": "A", "amount": 150, "items": ["item1", "item4"] }
   ]
   ```

2. `$group:`***Groups input documents by a specified identifier expression and applies the accumulator expressions.***

   ```javascript
    db.orders.aggregate([
    { $group: { _id: "$cust_id", totalAmount: { $sum: "$amount" } } }
    ])
   ```

   **Explanation:**This stage groups documents by `cust_id` and calculates the total amount for each customer.

   **Expected Output:**

   ```javascript
   [
   { "_id": "A123", "totalAmount": 300 },
   { "_id": "B456", "totalAmount": 200 },
   { "_id": "C789", "totalAmount": 300 }
   ]
   ```

3. `$sort:`***Sorts all input documents and returns them in the specified order.***

   ```javascript
   db.orders.aggregate([
   { $sort: { amount: -1 } }
   ])
   ```

   **Explanation:** This stage sorts documents by the `amount` field in descending order.

   ```javascript
   [
   { "_id": 4, "cust_id": "C789", "status": "C", "amount": 300, "items": ["item2", "item3"] },
   { "_id": 2, "cust_id": "B456", "status": "B", "amount": 200, "items": ["item3"] },
   { "_id": 3, "cust_id": "A123", "status": "A", "amount": 150, "items": ["item1", "item4"] },
   { "_id": 1, "cust_id": "A123", "status": "A", "amount": 100, "items": ["item1", "item2"] },
   { "_id": 5, "cust_id": "A123", "status": "B", "amount": 50, "items": ["item4"] }
   ]
   ```

4. `$project:`***Passes along the documents with only the specified fields.***

   ```javascript
   db.orders.aggregate([
   { $project: { cust_id: 1, amount: 1, _id: 0 } }
   ])
   ```

   **Explanation:** This stage includes only the `cust_id` and `amount` fields in the output documents.

   **Expected Output:**

   ```javascript
   [
   { "cust_id": "A123", "amount": 100 },
   { "cust_id": "B456", "amount": 200 },
   { "cust_id": "A123", "amount": 150 },
   { "cust_id": "C789", "amount": 300 },
   { "cust_id": "A123", "amount": 50 }
   ]
   ```

5. `$unwind:`***Deconstructs an array field from the input documents to output a document for each element.***

   ```javascript
   db.orders.aggregate([
   { $unwind: "$items" }
   ])
   ```
  
   **Explanation:** This stage outputs a document for each element in the `items` array.

   **Expected Output:**

   ```javascript
   [
   { "_id": 1, "cust_id": "A123", "status": "A", "amount": 100, "items": "item1" },
   { "_id": 1, "cust_id": "A123", "status": "A", "amount": 100, "items": "item2" },
   { "_id": 2, "cust_id": "B456", "status": "B", "amount": 200, "items": "item3" },
   { "_id": 3, "cust_id": "A123", "status": "A", "amount": 150, "items": "item1" },
   { "_id": 3, "cust_id": "A123", "status": "A", "amount": 150, "items": "item4" },
   { "_id": 4, "cust_id": "C789", "status": "C", "amount": 300, "items": "item2" },
   { "_id": 4, "cust_id": "C789", "status": "C", "amount": 300, "items": "item3" },
   { "_id": 5, "cust_id": "A123", "status": "B", "amount": 50, "items": "item4" }
   ]
   ```

6. `$limit:`***Limits the number of documents passed to the next stage in the pipeline.***

   ```javascript
   db.orders.aggregate([
   { $limit: 3 }
   ])
   ```

   **Explanation:** This stage limits the output to 3 documents.

   **Expected Output:**

   ```javascript
   [
   { "_id": 1, "cust_id": "A123", "status": "A", "amount": 100,  "items": ["item1", "item2"] },
   { "_id": 2, "cust_id": "B456", "status": "B", "amount": 200, "items": ["item3"] },
   { "_id": 3, "cust_id": "A123", "status": "A", "amount": 150, "items": ["item1", "item4"] }
   ]
   ```

7. `$skip:`***Skips over a specified number of documents.***

   ```javascript
   db.orders.aggregate([
    { $skip: 2 }
   ])
   ```

   **Explanation:** This stage skips the first 2 documents.

   **Expected Output:**

   ```javascript
   [
   { "_id": 3, "cust_id": "A123", "status": "A", "amount": 150, "items": ["item1", "item4"] },
   { "_id": 4, "cust_id": "C789", "status": "C", "amount": 300, "items": ["item2", "item3"] },
   { "_id": 5, "cust_id": "A123", "status": "B", "amount": 50, "items": ["item4"] }
   ]
   ```

8. `$lookup:`***Performs a left outer join to another collection in the same database to filter in documents from the "joined" collection for processing.***

   ```javascript
   db.orders.aggregate([
   {
    $lookup: {
      from: "customers",
      localField: "cust_id",
      foreignField: "cust_id",
      as: "customer_info"
    }
   }
   ])
   ```

   **Explanation:** This stage joins the `orders` collection with the `customers` collection based on the `cust_id` field.

   **Expected Output:**

   ```javascript
   [
   {
    "_id": 1,
    "cust_id": "A123",
    "status": "A",
    "amount": 100,
    "items": ["item1", "item2"],
    "customer_info": [
      { "cust_id": "A123", "name": "Alice", "address": "123 Main St" }
    ]
   },
   {
    "_id": 2,
    "cust_id": "B456",
    "status": "B",
    "amount": 200,
    "items": ["item3"],
    "customer_info": [
      { "cust_id": "B456", "name": "Bob", "address": "456 Elm St" }
    ]
   },
   {
    "_id": 3,
    "cust_id": "A123",
    "status": "A",
    "amount": 150,
    "items": ["item1", "item4"],
    "customer_info": [
      { "cust_id": "A123", "name": "Alice", "address": "123 Main St" }
    ]
   },
   {
    "_id": 4,
    "cust_id": "C789",
    "status": "C",
    "amount": 300,
    "items": ["item2", "item3"],
    "customer_info": [
      { "cust_id": "C789", "name": "Charlie", "address": "789 Oak St" }
    ]
   },
   {
    "_id": 5,
    "cust_id": "A123",
    "status": "B",
    "amount": 50,
    "items": ["item4"],
    "customer_info": [
      { "cust_id": "A123", "name": "Alice", "address": "123 Main St" }
    ]
   }
   ]
   ```

9. `$addFields:`***Adds new fields to documents.***

   ```javascript
   db.orders.aggregate([
   { $addFields: { discount: { $multiply: ["$amount", 0.1] } } }
   ])
   ```

   **Explanation:** This stage adds a `discount` field to each document, which is 10% of the `amount`.

   **Expected Output:**

   ```javascript
   [
   { "_id": 1, "cust_id": "A123", "status": "A", "amount": 100, "items": ["item1", "item2"], "discount": 10 },
   { "_id": 2, "cust_id": "B456", "status": "B", "amount": 200, "items": ["item3"], "discount": 20 },
   { "_id": 3, "cust_id": "A123", "status": "A", "amount": 150, "items": ["item1", "item4"], "discount": 15 },
   { "_id": 4, "cust_id": "C789", "status": "C", "amount": 300, "items": ["item2", "item3"], "discount": 30 },
   { "_id": 5, "cust_id": "A123", "status": "B", "amount": 50, "items": ["item4"], "discount": 5 }
   ]
   ```

10. `$count:`***Counts the number of documents that are input to the stage.***

    ```javascript
    db.orders.aggregate([
    { $count: "totalOrders" }
    ])
    ```

    **Explanation:**This stage counts the total number of documents and outputs a document with the count.

    **Expected Output:**

    ```javascript
    [
    { "totalOrders": 5 }
    ]
    ```

11. `$facet:`***Processes multiple aggregation pipelines within a single stage on the same set of input documents.***

    ```javascript
    db.orders.aggregate([
    {
     $facet: {
      "groupByStatus": [
        { $group: { _id: "$status", count: { $sum: 1 } } }
      ],
      "totalAmount": [
        { $group: { _id: null, total: { $sum: "$amount" } } }
      ]
     }
    }
    ])
    ```

    **Explanation:** This stage runs two pipelines: one groups documents by status and counts them, and the other calculates the total amount.

    **Expected Output:**

    ```javascript
    [
    {
    "groupByStatus": [
      { "_id": "A", "count": 2 },
      { "_id": "B", "count": 2 },
      { "_id": "C", "count": 1 }
     ],
    "totalAmount": [
      { "_id": null, "total": 800 }
     ]
    }
    ]
    ```

12. `$out:`***Writes the resulting documents of the aggregation pipeline to a specified collection.***

    ```javascript
    db.orders.aggregate([
    { $match: { status: "A" } },
    { $out: "filtered_orders" }
    ])
    ```

    **Explanation:**  This stage writes the documents with `status` "A" to a new collection named `filtered_orders`.

    **Expected Output:**

    ```javascript
    [
    { "_id": 1, "cust_id": "A123", "status": "A", "amount": 100, "items": ["item1", "item2"] },
    { "_id": 3, "cust_id": "A123", "status": "A", "amount": 150, "items": ["item1", "item4"] }
    ]
    ```

13. `$replaceRoot:`***Replaces the input document with the specified document.***

    ```javascript
    db.orders.aggregate([
    { $replaceRoot: { newRoot: "$items" } }
    ])
    ```

    **Explanation:** This stage replaces the input document with the `items` array.

    **Expected Output:**

    ```javascript
    [
    ["item1", "item2"],
    ["item3"],
    ["item1", "item4"],
    ["item2", "item3"],
    ["item4"]
    ]
    ```

14. `$sample:`***Randomly selects the specified number of documents from its input.***

    ```javascript
    db.orders.aggregate([
    { $sample: { size: 2 } }
    ])
    ```

    **Explanation:** This stage randomly selects 2 documents from the input.

    **Expected Output:**

    ```javascript
    [
    { "_id": 3, "cust_id": "A123", "status": "A", "amount": 150, "items": ["item1", "item4"] },
    { "_id": 1, "cust_id": "A123", "status": "A", "amount": 100, "items": ["item1", "item2"] }
    ]
    ```

15. `$redact:`***Restricts the content of the documents based on information stored in the documents themselves.***

    ```javascript
    db.orders.aggregate([
    { $redact: { $cond: { if: { $eq: ["$status", "A"] }, then: "$$KEEP", else: "$$PRUNE" } } }
    ])
    ```

    **Explanation:** This stage keeps documents with `status` "A" and prunes others.

    **Expected Output:**

    ```javascript
    [
    { "_id": 1, "cust_id": "A123", "status": "A", "amount": 100, "items": ["item1", "item2"] },
    { "_id": 3, "cust_id": "A123", "status": "A", "amount": 150, "items": ["item1", "item4"] }
    ]
    ```

### Transforming BirthDate Using `$dateToString`

We'll use the `$project` stage to transform the `birthdate` field into a more readable format.

**Example:**

Let's assume we have a collection named `users` with the following documents:

```javascript
db.users.insertMany([
  { "_id": 1, "name": "Alice", "birthdate": ISODate("1990-01-01T00:00:00Z") },
  { "_id": 2, "name": "Bob", "birthdate": ISODate("1985-05-15T00:00:00Z") },
  { "_id": 3, "name": "Charlie", "birthdate": ISODate("1992-12-20T00:00:00Z") }
])
```

**Aggregation Pipeline:**

We will use the `$project` stage to transform the `birthdate` field into a string format `YYYY-MM-DD`.

```javascript
db.users.aggregate([
  {
    $project: {
      name: 1,
      birthdate: {
        $dateToString: { format: "%Y-%m-%d", date: "$birthdate" }
      }
    }
  }
])
```

**Explanation:**

- **$project:** This stage reshapes each document in the stream, including only the `name` and a transformed `birthdate` field.
  
- **$dateToString:** This operator converts the `birthdate` field to a string format `YYYY-MM-DD`.

**Expected Output:**

```javascript
[
  { "_id": 1, "name": "Alice", "birthdate": "1990-01-01" },
  { "_id": 2, "name": "Bob", "birthdate": "1985-05-15" },
  { "_id": 3, "name": "Charlie", "birthdate": "1992-12-20" }
]
```

### Transforming BirthDate Using `$convert`

Using `$convert` is another way to transform the birthdate field, but it serves a different purpose. `$convert` is used to change the data type of a field.whereas `$dateToString` is specifically designed to format dates as strings.

**Example:**

```javascript
db.users.insertMany([
  { "_id": 1, "name": "Alice", "birthdate": "1990-01-01" },
  { "_id": 2, "name": "Bob", "birthdate": "1985-05-15" },
  { "_id": 3, "name": "Charlie", "birthdate": "1992-12-20" }
])
```

**Aggregation Pipeline Using `$convert`:**

We will use the `$project` stage to convert the `birthdate` field from a string to a date.

```javascript
db.users.aggregate([
  {
    $project: {
      name: 1,
      birthdate: {
        $convert: { input: "$birthdate", to: "date" }
      }
    }
  }
])
```

**Explanation:**

- **$project:** This stage reshapes each document in the stream, including only the `name` and a converted `birthdate` field.

- **$convert:** This operator converts the `birthdate` field from a string to a date object.

**Expected Output:**

```javascript
[
  { "_id": 1, "name": "Alice", "birthdate": ISODate("1990-01-01T00:00:00Z") },
  { "_id": 2, "name": "Bob", "birthdate": ISODate("1985-05-15T00:00:00Z") },
  { "_id": 3, "name": "Charlie", "birthdate": ISODate("1992-12-20T00:00:00Z") }
]
```

***When to Use $convert:***

- **$convert** is useful when you need to change the data type of a field, for example, converting a string to a date or a number to a string.

***When to Use $dateToString:***

- **$dateToString** is specifically for formatting date fields into string representations.

### Understanding `$isoWeekYear` Operator

The `$isoWeekYear` operator in MongoDB is used to extract the ISO week-numbering year from a date. The ISO week-numbering year is the year that contains the Thursday of the week.

**Example:**

Let's assume we have a collection named `events` with the following documents:

```javascript
db.events.insertMany([
  { "_id": 1, "name": "Event A", "date": ISODate("2023-01-01T00:00:00Z") },
  { "_id": 2, "name": "Event B", "date": ISODate("2023-06-15T00:00:00Z") },
  { "_id": 3, "name": "Event C", "date": ISODate("2023-12-31T00:00:00Z") }
])
```

**Aggregation Pipeline:**

We will use the `$project` stage to add a new field `isoWeekYear` that contains the ISO week-numbering year of the `date` field.

```javascript
db.events.aggregate([
  {
    $project: {
      name: 1,
      date: 1,
      isoWeekYear: { $isoWeekYear: "$date" }
    }
  }
])
```

**Explanation:**

- **$project:** This stage reshapes each document in the stream, including only the name, date, and a new field `isoWeekYear`.

- **$isoWeekYear:** This operator extracts the ISO week-numbering year from the `date` field.

**Expected Output:**

```javascript
[
  { "_id": 1, "name": "Event A", "date": ISODate("2023-01-01T00:00:00Z"), "isoWeekYear": 2022 },
  { "_id": 2, "name": "Event B", "date": ISODate("2023-06-15T00:00:00Z"), "isoWeekYear": 2023 },
  { "_id": 3, "name": "Event C", "date": ISODate("2023-12-31T00:00:00Z"), "isoWeekYear": 2023 }
]
```

### `$group` Vs `$project`

The `$group` and `$project` stages in MongoDB's aggregation framework serve different purposes. Here's a detailed comparison:

**`$group` Operator:**

- **Purpose:** The `$group` stage is used to group documents by a specified key and perform aggregate operations like sum, average, count, etc., on the grouped data.

**Syntax:**

```javascript
{
  $group: {
    _id: <expression>, // Group by this field
    <field1>: { <accumulator1>: <expression1> },
    <field2>: { <accumulator2>: <expression2> },
    // Additional fields and accumulators
  }
}
```

**Example:**

```javascript
db.sales.aggregate([
  {
    $group: {
      _id: "$productId",
      totalSales: { $sum: "$amount" },
      averageSales: { $avg: "$amount" }
    }
  }
])
```

**Explanation:** This groups the documents by `productId` and calculates the total and average sales for each product.

**`$project` Operator:**

- **Purpose:** The `$project` stage is used to include, exclude, or add new fields to the documents in the aggregation pipeline. It reshapes each document in the stream.

**Syntax:**

```javascript
{
  $project: {
    <field1>: <expression1>,
    <field2>: <expression2>,
    // Additional fields and expressions
  }
}
```

**Example:**

```javascript
db.users.aggregate([
  {
    $project: {
      name: 1,
      birthdate: 1,
      birthYear: { $year: "$birthdate" }
    }
  }
])
```

**Explanation:** This includes the `name` and `birthdate` fields in the output and adds a new field `birthYear` that contains the year extracted from the `birthdate`.

**Key Differences:**

- **Grouping vs. Reshaping:**
  
  - `$group` is used for grouping documents and performing aggregate calculations.
  
  - `$project` is used for reshaping documents by including, excluding, or adding new fields.

- **Output Structure:**
  
  - `$group` changes the structure of the output documents based on the grouping key.
  
  - `$project` maintains the structure of the input documents but can modify the fields.

- **Use Cases:**
  
  - Use `$group` when you need to aggregate data, such as summing sales or counting occurrences.
  
  - Use `$project` when you need to transform the data, such as formatting dates or computing new fields.

**Combined Example:**

You can use both `$group` and `$project` in the same aggregation pipeline to first group the data and then reshape the grouped results.

```javascript
db.sales.aggregate([
  {
    $group: {
      _id: "$productId",
      totalSales: { $sum: "$amount" },
      averageSales: { $avg: "$amount" }
    }
  },
  {
    $project: {
      productId: "$_id",
      totalSales: 1,
      averageSales: 1,
      _id: 0
    }
  }
])
```

**Explanation:** This pipeline first groups the sales by `productId` and calculates the total and average sales. Then, it reshapes the output to include `productId`, `totalSales`, and `averageSales`, while excluding the `_id` field.

### Pushing Elements Into Newly Created Arrays

To push elements into a newly created array in MongoDB, you can use the `$push` operator within the `$group` stage. This is useful when you want to collect values from multiple documents into an array for each group.

**Example:**

Let's assume we have a collection named `sales` with the following documents:

```javascript
db.sales.insertMany([
  { "_id": 1, "productId": "A", "amount": 100, "date": ISODate("2023-01-01T00:00:00Z") },
  { "_id": 2, "productId": "A", "amount": 150, "date": ISODate("2023-01-02T00:00:00Z") },
  { "_id": 3, "productId": "B", "amount": 200, "date": ISODate("2023-01-01T00:00:00Z") },
  { "_id": 4, "productId": "B", "amount": 250, "date": ISODate("2023-01-03T00:00:00Z") }
])
```

**Aggregation Pipeline:**

We will use the `$group` stage to group the documents by `productId` and push the `amount` and date fields into a newly created array called `salesDetails`.

```javascript
db.sales.aggregate([
  {
    $group: {
      _id: "$productId",
      totalSales: { $sum: "$amount" },
      averageSales: { $avg: "$amount" },
      salesDetails: {
        $push: {
          amount: "$amount",
          date: "$date"
        }
      }
    }
  },
  {
    $project: {
      productId: "$_id",
      totalSales: 1,
      averageSales: 1,
      salesDetails: 1,
      _id: 0
    }
  }
])
```

**Explanation:**

- **$group:** This stage groups the documents by `productId` and calculates the total and average sales. It also creates a new array `salesDetails` that contains the `amount` and `date` fields for each sale.
  
- `_id:` "$productId": Groups by productId.
  
- `totalSales: { $sum: "$amount" }:` Calculates the total sales for each product.
  
- `averageSales: { $avg: "$amount" }:` Calculates the average sales for each product.
  
- `salesDetails: { $push: { amount: "$amount", date: "$date" } }:` Pushes the amount and date fields into the salesDetails array.

- **Project:** This stage reshapes the output to include `productId`, `totalSales`, `averageSales`, and `salesDetails`, while excluding the `_id` field.

**Expected Output:**

```javascript
[
  {
    "productId": "A",
    "totalSales": 250,
    "averageSales": 125,
    "salesDetails": [
      { "amount": 100, "date": ISODate("2023-01-01T00:00:00Z") },
      { "amount": 150, "date": ISODate("2023-01-02T00:00:00Z") }
    ]
  },
  {
    "productId": "B",
    "totalSales": 450,
    "averageSales": 225,
    "salesDetails": [
      { "amount": 200, "date": ISODate("2023-01-01T00:00:00Z") },
      { "amount": 250, "date": ISODate("2023-01-03T00:00:00Z") }
    ]
  }
]
```

### Understanding `$unwind` Stage

- The `$unwind` stage in MongoDB's aggregation framework is used to deconstruct an array field from the input documents to output a document for each element of the array.

- This is useful when you need to work with individual elements of an array as separate documents.

**How $unwind Works:**

- **Input:** A document with an array field.

- **Output:** Multiple documents, each containing one element from the array field.

**Syntax:**

```javascript
{
  $unwind: {
    path: <arrayFieldPath>,
    includeArrayIndex: <string>, // Optional
    preserveNullAndEmptyArrays: <boolean> // Optional
  }
}
```

- **path:** The field path to the array that you want to unwind.

- **includeArrayIndex:** Optional. The name of a new field to hold the array index of the unwound element.

- **preserveNullAndEmptyArrays:** Optional. If true, if the array is null, missing, or empty, the input document is included in the output with the array field set to null.

**Example:**

Let's assume we have a collection named `orders` with the following documents:

```javascript
db.orders.insertMany([
  { "_id": 1, "customer": "Alice", "items": ["apple", "banana", "orange"] },
  { "_id": 2, "customer": "Bob", "items": ["grape", "melon"] },
  { "_id": 3, "customer": "Charlie", "items": [] }
])
```

**Aggregation Pipeline:**

We will use the `$unwind` stage to deconstruct the `items` array field.

```javascript
db.orders.aggregate([
  {
    $unwind: "$items"
  }
])
```

***Explanation:***

**$unwind:** This stage deconstructs the `items` array field, outputting a document for each element in the array.

**Expected Output:**

```javascript
[
  { "_id": 1, "customer": "Alice", "items": "apple" },
  { "_id": 1, "customer": "Alice", "items": "banana" },
  { "_id": 1, "customer": "Alice", "items": "orange" },
  { "_id": 2, "customer": "Bob", "items": "grape" },
  { "_id": 2, "customer": "Bob", "items": "melon" }
]
```

**Using Optional Parameters:**

You can use the optional parameters `includeArrayIndex` and `preserveNullAndEmptyArrays` to customize the behavior of `$unwind`.

**Example:**

```javascript
db.orders.aggregate([
  {
    $unwind: {
      path: "$items",
      includeArrayIndex: "itemIndex",
      preserveNullAndEmptyArrays: true
    }
  }
])
```

***Explanation:***

- **path:** Specifies the items array field to unwind.

- **includeArrayIndex:** Adds a new field itemIndex that contains the index of the unwound element.

- **preserveNullAndEmptyArrays:** If true, includes documents with null or empty arrays in the output.

**Expected Output:**

```javascript
[
  { "_id": 1, "customer": "Alice", "items": "apple", "itemIndex": 0 },
  { "_id": 1, "customer": "Alice", "items": "banana", "itemIndex": 1 },
  { "_id": 1, "customer": "Alice", "items": "orange", "itemIndex": 2 },
  { "_id": 2, "customer": "Bob", "items": "grape", "itemIndex": 0 },
  { "_id": 2, "customer": "Bob", "items": "melon", "itemIndex": 1 },
  { "_id": 3, "customer": "Charlie", "items": null, "itemIndex": null }
]
```

### Eliminating Duplicate Values

To eliminate duplicate values in MongoDB, you can use the `$group` stage in the aggregation pipeline along with the
`$first` or `$addToSet` operators. Here are a few methods to achieve this:

**Method 1: Using `$group` and `$first`**

This method groups documents by a specified key and uses the `$first` operator to retain the first document in each group.

**Example:**

Let's assume we have a collection named `users` with the following documents:

```javascript
db.users.insertMany([
  { "_id": 1, "name": "Alice", "email": "alice@example.com" },
  { "_id": 2, "name": "Bob", "email": "bob@example.com" },
  { "_id": 3, "name": "Alice", "email": "alice@example.com" }
])
```

**Aggregation Pipeline:**

We will use the `$group` stage to eliminate duplicate documents based on the `email` field.

```javascript
db.users.aggregate([
  {
    $group: {
      _id: "$email",
      name: { $first: "$name" },
      email: { $first: "$email" }
    }
  }
])
```

**Explanation:**

- **$group:** Groups documents by the `email` field.

- **$first:** Retains the first document in each group for the `name` and `email` fields.

**Expected Output:**

```javascript
[
  { "_id": "alice@example.com", "name": "Alice", "email": "alice@example.com" },
  { "_id": "bob@example.com", "name": "Bob", "email": "bob@example.com" }
]
```

**Method 2: Using `$group` and `$addToSet`:**

This method groups documents by a specified key and uses the `$addToSet` operator to create an array of unique values.

**Example:**

```javascript
db.users.insertMany([
  { "_id": 1, "name": "Alice", "email": "alice@example.com" },
  { "_id": 2, "name": "Bob", "email": "bob@example.com" },
  { "_id": 3, "name": "Alice", "email": "alice@example.com" }
])
```

**Aggregation Pipeline:**

We will use the `$group` stage to eliminate duplicate documents based on the `email` field and create an array of unique names.

```javascript
db.users.aggregate([
  {
    $group: {
      _id: "$email",
      names: { $addToSet: "$name" },
      email: { $first: "$email" }
    }
  }
])
```

**Explanation:**

- **$group:** Groups documents by the `email` field.

- **$addToSet:** Creates an array of unique `name` values for each group.

- **$first:** Retains the first `email` value in each group.

**Expected Output:**

```javascript
[
  { "_id": "alice@example.com", "names": ["Alice"], "email": "alice@example.com" },
  { "_id": "bob@example.com", "names": ["Bob"], "email": "bob@example.com" }
]
```

**Method 3: Using `distinct` Command:**

The `distinct` command can be used to retrieve distinct values for a specified field.

**Example:**

Let's assume we have a collection named `users` with the following documents:

```javascript
db.users.insertMany([
  { "_id": 1, "name": "Alice", "email": "alice@example.com" },
  { "_id": 2, "name": "Bob", "email": "bob@example.com" },
  { "_id": 3, "name": "Alice", "email": "alice@example.com" }
])
```

We will use the `distinct` command to retrieve unique email addresses.

```javascript
db.users.distinct("email")
```

**Expected Output:**

```javascript
[
  "alice@example.com",
  "bob@example.com"
]
```

### Using Projection With Arrays

- In MongoDB, projection is used to specify which fields to include or exclude in the returned documents.

- When working with arrays, you can use projection to include or exclude specific elements of the array or to reshape the array.

**Example: Including Specific Fields in an Array:**

Let's assume we have a collection named `orders` with the following documents:

```javascript
db.orders.insertMany([
  {
    "_id": 1,
    "customer": "Alice",
    "items": [
      { "product": "apple", "quantity": 10, "price": 1.5 },
      { "product": "banana", "quantity": 5, "price": 1.0 }
    ]
  },
  {
    "_id": 2,
    "customer": "Bob",
    "items": [
      { "product": "grape", "quantity": 20, "price": 2.0 },
      { "product": "melon", "quantity": 2, "price": 3.0 }
    ]
  }
])
```

**Projection to Include Specific Fields in an Array:**

We will use projection to include only the `product` and `quantity` fields in the `items` array.

```javascript
db.orders.find(
  {},
  {
    customer: 1,
    "items.product": 1,
    "items.quantity": 1
  }
)
```

**Explanation:**

- **customer: 1:** Includes the customer field in the output.

- **"items.product": 1:** Includes the product field within the items array.

- **"items.quantity": 1:** Includes the quantity field within the items array.

**Expected Output:**

```javascript
[
  {
    "_id": 1,
    "customer": "Alice",
    "items": [
      { "product": "apple", "quantity": 10 },
      { "product": "banana", "quantity": 5 }
    ]
  },
  {
    "_id": 2,
    "customer": "Bob",
    "items": [
      { "product": "grape", "quantity": 20 },
      { "product": "melon", "quantity": 2 }
    ]
  }
]
```

**Projection to Exclude Specific Fields in an Array:**

We will use projection to exclude the `price` field in the `items` array.

```javascript
db.orders.find(
  {},
  {
    "items.price": 0
  }
)
```

**Explanation:**

- **"items.price": 0:** Excludes the `price` field within the `items` array.

**Expected Output:**

```javascript
[
  {
    "_id": 1,
    "customer": "Alice",
    "items": [
      { "product": "apple", "quantity": 10 },
      { "product": "banana", "quantity": 5 }
    ]
  },
  {
    "_id": 2,
    "customer": "Bob",
    "items": [
      { "product": "grape", "quantity": 20 },
      { "product": "melon", "quantity": 2 }
    ]
  }
]
```

**Projection to Include Specific Array Elements:**

We will use projection to include only the first element of the `items` array.

```javascript
db.orders.find(
  {},
  {
    customer: 1,
    items: { $slice: 1 }
  }
)
```

**Explanation:**

- **customer: 1:** Includes the `customer` field in the output.

- **items: { $slice: 1 }:** Includes only the first element of the `items` array.

**Expected Output:**

```javascript
[
  {
    "_id": 1,
    "customer": "Alice",
    "items": [
      { "product": "apple", "quantity": 10, "price": 1.5 }
    ]
  },
  {
    "_id": 2,
    "customer": "Bob",
    "items": [
      { "product": "grape", "quantity": 20, "price": 2.0 }
    ]
  }
]
```

### Getting The Length Of An Array

- To get the length of an array in MongoDB, you can use the `$size` operator within the `$project` stage of an aggregation pipeline.

- The `$size` operator returns the number of elements in an array.

**Example:**

Let's assume we have a collection named `orders` with the following documents:

```javascript
db.orders.insertMany([
  {
    "_id": 1,
    "customer": "Alice",
    "items": ["apple", "banana", "orange"]
  },
  {
    "_id": 2,
    "customer": "Bob",
    "items": ["grape", "melon"]
  },
  {
    "_id": 3,
    "customer": "Charlie",
    "items": []
  }
])
```

**Aggregation Pipeline:**

We will use the `$project` stage to add a new field `itemsCount` that contains the length of the `items` array.

```javascript
db.orders.aggregate([
  {
    $project: {
      customer: 1,
      itemsCount: { $size: "$items" }
    }
  }
])
```

**Explanation:**

- **$project:** This stage reshapes each document in the stream, including only the `customer` field and a new field `itemsCount`.

- **$size:** This operator returns the number of elements in the `items` array.

**Expected Output:**

```javascript
[
  { "_id": 1, "customer": "Alice", "itemsCount": 3 },
  { "_id": 2, "customer": "Bob", "itemsCount": 2 },
  { "_id": 3, "customer": "Charlie", "itemsCount": 0 }
]
```

**Using $size in a Query:**

You can also use the `$size` operator in a query to match documents where the array has a specific length.

**Example:**

Let's find documents where the `items` array has exactly 2 elements.

```javascript
db.orders.find({
  items: { $size: 2 }
})
```

**Expected Output:**

```javascript
[
  { "_id": 2, "customer": "Bob", "items": ["grape", "melon"] }
]
```

### Using `$filter` Operator

- The `$filter` operator in MongoDB is used to filter elements of an array based on a specified condition. It allows you to project only the elements of an array that match the given criteria.

**Example:**

Let's find documents where the `items` array contains elements that start with the letter `"g"`.

```javascript
db.orders.aggregate([
  {
    $project: {
      customer: 1,
      items: {
        $filter: {
          input: "$items",
          as: "item",
          cond: { $regexMatch: { input: "$$item", regex: /^g/ } }
        }
      }
    }
  }
])
```

**Exaplanation:**

1. **$project:** This stage is used to include or exclude fields from the documents.

2. **customer: 1:** This includes the `customer` field in the output.

3. **items:** This field is projected using the `$filter` operator.

4. **$filter:** The operator takes three parameters:

- **input:** The array to filter (`$items`).

- **as:** The variable name for each element in the array (`item`).

- **cond:** The condition to apply to each element. Here, `$regexMatch` is used to check if the element starts with the letter "g".

**Expected Output:**

```javascript
[
  { "_id": 1, "customer": "Alice", "items": ["grape"] },
  { "_id": 2, "customer": "Bob", "items": ["grape"] }
]
```

### Applying Multiple Operations To Array

In MongoDB, you can use the `aggregate pipeline` to apply multiple operations to an array. The `aggregate pipeline` allows you to perform a sequence of operations on your data, such as filtering, projecting, grouping, and sorting.

**Example:**

Suppose you have a collection `students` with the following documents:

```javascript
[
  {
    "_id": 1,
    "name": "Alice",
    "scores": [85, 92, 78]
  },
  {
    "_id": 2,
    "name": "Bob",
    "scores": [89, 94, 81]
  },
  {
    "_id": 3,
    "name": "Charlie",
    "scores": [95, 88, 84]
  }
]
```

***You want to calculate the `average score` for each student and then `filter` out students with an average score below `90`.***

**Aggregation Pipeline:**

```javascript
db.students.aggregate([
  {
    "$project": {
      "name": 1,
      "averageScore": { "$avg": "$scores" }
    }
  },
  {
    "$match": {
      "averageScore": { "$gte": 90 }
    }
  }
])
```

**Explanation:**

- **$project:** This stage reshapes each document in the stream, such as by adding new fields or removing existing fields. In this case, we are calculating the average score for each student using the $avg operator and including the `name` field.

- **$match:** This stage filters the documents to pass only the documents that match the specified condition. Here, we are filtering out students whose average score is less than 90.

**Expected Output:**

```javascript
[
  {
    "_id": 2,
    "name": "Bob",
    "averageScore": 88
  },
  {
    "_id": 3,
    "name": "Charlie",
    "averageScore": 89
  }
]
```

### Understanding `$bucket`

The `$bucket` stage in MongoDB's aggregation framework allows you to group documents into buckets based on a specified expression. This is useful for categorizing data into ranges.

**Example:**

Suppose you have a collection `students` with the following documents:

```javascript
[
  {
    "_id": 1,
    "name": "Alice",
    "scores": [85, 92, 78]
  },
  {
    "_id": 2,
    "name": "Bob",
    "scores": [89, 94, 81]
  },
  {
    "_id": 3,
    "name": "Charlie",
    "scores": [95, 88, 84]
  }
]
```

***You want to categorize students based on their average scores into different buckets.***

**Aggregation Pipeline:**

```javascript
db.students.aggregate([
  {
    "$project": {
      "name": 1,
      "averageScore": { "$avg": "$scores" }
    }
  },
  {
    "$bucket": {
      "groupBy": "$averageScore",
      "boundaries": [0, 80, 90, 100],
      "default": "Other",
      "output": {
        "count": { "$sum": 1 },
        "students": {
          "$push": {
            "name": "$name",
            "averageScore": "$averageScore"
          }
        }
      }
    }
  }
])
```

**Explanation:**

1. **$project:** This stage reshapes each document in the stream, such as by adding new fields or removing existing fields. In this case, we are calculating the average score for each student using the $avg operator and including the `name` field.

2. **$bucket:** This stage categorizes documents into specified buckets based on the `averageScore` field.

- `groupBy:` The field to group by, in this case, `averageScore`.
  
- `boundaries:` The boundaries for the buckets. Here, we have three buckets: [0, 80), [80, 90), and [90, 100).
  
- `default:` The bucket for values that do not fit into the specified boundaries.
  
- `output:` The fields to include in the output. Here, we are counting the number of students in each bucket and pushing the `name` and `averageScore` of each student into an array.

**Expected Output:**

```javascript
[
  {
    "_id": 0,
    "count": 1,
    "students": [
      {
        "name": "Alice",
        "averageScore": 85
      }
    ]
  },
  {
    "_id": 80,
    "count": 2,
    "students": [
      {
        "name": "Bob",
        "averageScore": 88
      },
      {
        "name": "Charlie",
        "averageScore": 89
      }
    ]
  }
]
```

### Writing Pipeline Results Into a New Collection

Let's consider we have a collection `orders` with documents representing different orders and their total amounts. We want to calculate the total sales and the number of orders for each customer and write the results into a new collection called `customerSales`.

**Product Data:**

```javascript
[
  {
    "_id": 1,
    "customerId": "C001",
    "amount": 100
  },
  {
    "_id": 2,
    "customerId": "C002",
    "amount": 200
  },
  {
    "_id": 3,
    "customerId": "C001",
    "amount": 150
  },
  {
    "_id": 4,
    "customerId": "C003",
    "amount": 300
  },
  {
    "_id": 5,
    "customerId": "C002",
    "amount": 250
  }
]
```

**Aggregation Pipeline:**

```javascript
db.orders.aggregate([
  {
    "$group": {
      "_id": "$customerId",
      "totalSales": { "$sum": "$amount" },
      "orderCount": { "$sum": 1 }
    }
  },
  {
    "$out": "customerSales"
  }
])
```

**Explanation:**

1. **$group:** This stage groups documents by the customerId field and calculates the total sales and the number of orders for each customer.

   - `_id:` The field to group by, in this case, `customerId`.
  
   - `totalSales:` The total sales amount for each customer, calculated using the `$sum` operator on the `amount` field.
  
   - `orderCount:` The number of orders for each customer, calculated using the `$sum` operator with a value of 1 for each document.

2. **$out:** This stage writes the results of the aggregation pipeline to a specified collection. In this case, the results are written to the `customerSales` collection.

***The result of the above aggregation pipeline will be written to the customerSales collection. You can then query this collection to see the results:***

```javascript
db.customerSales.find().pretty()
```

**Expected Output:**

```javascript
[
  {
    "_id": "C001",
    "totalSales": 250,
    "orderCount": 2
  },
  {
    "_id": "C002",
    "totalSales": 450,
    "orderCount": 2
  },
  {
    "_id": "C003",
    "totalSales": 300,
    "orderCount": 1
  }
]
```

### Working With `$geoNear` Stage

- The `$geoNear` stage in MongoDB's aggregation framework is used to perform geospatial queries.
  
- It returns documents based on their proximity to a specified point. This stage must be the first stage in the pipeline.

**Example:**

Suppose you have a collection `places` with documents representing different places and their locations. Each document contains a `location` field with GeoJSON coordinates.

```javascript
[
  {
    "_id": 1,
    "name": "Place A",
    "location": { "type": "Point", "coordinates": [40.7128, -74.0060] }
  },
  {
    "_id": 2,
    "name": "Place B",
    "location": { "type": "Point", "coordinates": [34.0522, -118.2437] }
  },
  {
    "_id": 3,
    "name": "Place C",
    "location": { "type": "Point", "coordinates": [37.7749, -122.4194] }
  }
]
```

**Aggregation Pipeline with `$geoNear:`**

```javascript
db.places.aggregate([
  {
    "$geoNear": {
      "near": { "type": "Point", "coordinates": [40.730610, -73.935242] },
      "distanceField": "distance",
      "maxDistance": 1000000,
      "spherical": true
    }
  }
])
```

1. **$geoNear:** This stage performs a geospatial query to find documents near a specified point.

   - `near:` The point from which to calculate distances. This should be a GeoJSON point.
  
   - `distanceField:` The field in which to store the calculated distance.
  
   - `maxDistance:` The maximum distance from the `near` point to include in the results, in meters.
  
   - `spherical:` If true, the query will use spherical geometry to calculate distances.

***The result of the above aggregation pipeline will return documents sorted by their proximity to the specified point `[40.730610, -73.935242]`.***

***Expected Output:***

```javascript
[
  {
    "_id": 1,
    "name": "Place A",
    "location": { "type": "Point", "coordinates": [40.7128, -74.0060] },
    "distance": 7452.7
  }
]
```

**For more information, refer to the Official docs:**

- **Official Aggregation Framework:** [Official Aggregation Framework](https://docs.mongodb.com/manual/core/aggregation-pipeline/)
  
- **Learn more about $cond:** [Learn more about $cond](<https://docs.mongodb.com/manual/reference/operator/aggregation/cond/>).

## 6. Working With Numbers

### 1. **32-bit Integer (`NumberInt`):**

- **Description**: Represents a 32-bit signed integer.
  
  - **Example**:
  
     ```javascript
     var int32 = NumberInt(123);
     db.collection.insert({ value: int32 });
     ```

  - **Output**:
  
     ```javascript
     { "_id" : ObjectId("..."), "value" : NumberInt(123) }
     ```

  - **Explanation**: Use `NumberInt` when you need to store small integer values that fit within the 32-bit range (-2,147,483,648 to 2,147,483,647).

### 2. **64-bit Integer (`NumberLong`)**

- **Description**: Represents a 64-bit signed integer.
  
  - **Example**:
  
     ```javascript
     var int64 = NumberLong(123456789012345);
     db.collection.insert({ value: int64 });
     ```

  - **Output**:
  
     ```javascript
     { "_id" : ObjectId("..."), "value" : NumberLong("123456789012345") }
     ```

  - **Explanation**: Use `NumberLong` for larger integer values that exceed the 32-bit range.

### 3. **Double (`NumberDouble`)**

- **Description**: Represents a double-precision 64-bit IEEE 754 floating point.
  
  - **Example**:
  
     ```javascript
     var double = NumberDouble(123.45);
     db.collection.insert({ value: double });
     ```

  - **Output**:

     ```json
     { "_id" : ObjectId("..."), "value" : 123.45 }
     ```

  - **Explanation**: Use `NumberDouble` for floating-point numbers that require double precision.

### 4. **Decimal (`NumberDecimal`)**

- **Description**: Represents a 128-bit high-precision decimal.

  - **Example**:
  
     ```javascript
     var decimal = NumberDecimal("12345.6789012345678901234567890123456789");
     db.collection.insert({ value: decimal });
     ```

  - **Output**:

     ```json

     { "_id" : ObjectId("..."), "value" : NumberDecimal("12345.6789012345678901234567890123456789") }
     ```

  - **Explanation**: Use `NumberDecimal` for high-precision decimal values, which are crucial for applications requiring exact decimal representation, such as financial calculations.

**Summary:**

- **NumberInt:** `32-bit integer`, suitable for small integers.

- **NumberLong:** `64-bit integer`, suitable for large integers.

- **NumberDouble:** `64-bit floating-point`, suitable for double precision floating-point numbers.

- **NumberDecimal:** `128-bit decimal`, suitable for high-precision decimal values.

**For more information, refer to the Official docs:**

- [Difference between decimal, float and double in .NET](https://stackoverflow.com/questions/618535/difference-between-decimal-float-and-double-in-net)

- [Number Ranges](https://social.msdn.microsoft.com/Forums/vstudio/en-US/d2f723c7-f00a-4600-945a-72da23cbc53d/can-anyone-explain-clearly-about-float-vs-decimal-vs-double-?forum=csharpgeneral)

- [Model Monetary Data in MongoDB](https://docs.mongodb.com/manual/tutorial/model-monetary-data/)

## 7. Performance , Fault Tolerancy And Deployment

**Performance:**

1. **Indexes:** Use indexes to improve query performance.

2. **Sharding:** Distribute data across multiple servers.

3. **Replication:** Use replica sets to ensure high availability.
  
4. **Schema Design:** Optimize schema design for read and write operations.

5. **Aggregation:** Use the aggregation framework for complex data processing.

**Fault Tolerance:**

1. **Replica Sets:** Use replica sets to provide redundancy and high availability.

2. **Automatic Failover:** MongoDB automatically fails over to a secondary replica if the primary fails.

3. **Backup and Restore:** Regularly back up your data and test your restore process.

**Deployment:**

1. **Standalone:** Single MongoDB instance for development or testing.

2. **Replica Set:** Multiple MongoDB instances for high availability.

3. **Sharded Cluster:** Distribute data across multiple shards for horizontal scaling.

4. **Cloud Deployment:** Use MongoDB Atlas for managed cloud deployment.

### Understanding Capped Collections

- `Capped collections` in MongoDB are fixed-size collections that support high-throughput operations by maintaining insertion order.

- They are useful for scenarios where you need to store a fixed amount of data, such as logs or cache data, and automatically discard the oldest entries when the collection reaches its size limit.

**Key Features of Capped Collections:**

1. **Fixed Size:** The size of a capped collection is specified when it is created.

2. **Insertion Order:** Documents are stored in the order they are inserted.

3. **Automatic Overwrite:** When the size limit is reached, the oldest documents are automatically overwritten by new ones.

4. **High Performance:** Capped collections provide high performance for insert operations.

**Example:**

```javascript
// Create a capped collection with a maximum size of 1MB and a maximum of 1000 documents
db.createCollection("logs", { capped: true, size: 1048576, max: 1000 });

// Insert a document into the capped collection
db.logs.insert({ message: "This is a log message", timestamp: new Date() });

// Query the capped collection
db.logs.find();
```

**Use Cases:**

- **Logging:** Store application logs where only the most recent logs are needed.

- **Caching:** Store temporary data that can be overwritten when the collection reaches its size limit.

- **Time-Series Data:** Store time-series data where only the most recent data points are relevant.

### What are Replica Sets?

- `Replica sets` in MongoDB are a group of mongod instances that maintain the same data set, providing redundancy and high availability.

- A `replica set` consists of multiple data-bearing nodes and optionally one arbiter node. Replica sets are the basis for all production deployments of MongoDB.

**Key Features of Replica Sets::**

1. **Redundancy:** Multiple copies of data are maintained to ensure data availability.

2. **Automatic Failover:** If the primary node fails, an election process selects a new primary from the secondaries.

3. **Read Scaling:** Secondary nodes can be used to distribute read operations.

4. **Data Consistency:** Replica sets ensure that all nodes have the same data.

**Example:**

***Step 1: Start multiple MongoDB instances with the --replSet option.***

```javascript
//Start three MongoDB instances on different ports
mongod --replSet rs0 --port 27017 --dbpath /data/db1
mongod --replSet rs0 --port 27018 --dbpath /data/db2
mongod --replSet rs0 --port 27019 --dbpath /data/db3
```

***Step 2: Connect to one of the instances and initiate the replica set.:***

```javascript
// Connect to the MongoDB instance
mongo --port 27017

// Initiate the replica set
rs.initiate({
  _id: "rs0",
  members: [
    { _id: 0, host: "localhost:27017" },
    { _id: 1, host: "localhost:27018" },
    { _id: 2, host: "localhost:27019" }
  ]
});
```

***Step 3: Check the status of the replica set to ensure it is configured correctly.***

```javascript
// Check the status of the replica set
rs.status();
```

**Use Cases:**

- **High Availability:** Ensure that your application remains available even if one or more nodes fail.

- **Disaster Recovery:** Protect against data loss by maintaining multiple copies of data.

- **Read Scaling:** Distribute read operations across secondary nodes to improve performance.

### Understanding Sharding

1. `Sharding` in MongoDB is a method for distributing data across multiple servers or clusters.

2. It allows MongoDB to handle large datasets and high-throughput operations by horizontally scaling the database.

3. `Sharding` is particularly useful for applications with large amounts of data and high query rates.

**Key Concepts of Sharding::**

1. **Shard:** A single MongoDB instance or replica set that holds a subset of the sharded data.

2. **Shard Key:** A field or fields used to distribute the data across shards. The choice of shard key is crucial for balanced distribution.

3. **Config Servers:** Store metadata and configuration settings for the sharded cluster.

4. **Mongos:** A routing service that directs queries to the appropriate shard(s).

**Example:**

***Step 1: Start the config servers that store metadata for the sharded cluster.***

```javascript
//Start three config servers
mongod --configsvr --replSet configReplSet --port 27019 --dbpath /data/configdb1
mongod --configsvr --replSet configReplSet --port 27020 --dbpath /data/configdb2
mongod --configsvr --replSet configReplSet --port 27021 --dbpath /data/configdb3
```

***Step 2: Connect to one of the config servers and initiate the replica set.***

```javascript
// Connect to the config server
mongo --port 27019

// Initiate the config server replica set
rs.initiate({
  _id: "configReplSet",
  configsvr: true,
  members: [
    { _id: 0, host: "localhost:27019" },
    { _id: 1, host: "localhost:27020" },
    { _id: 2, host: "localhost:27021" }
  ]
});
```

***Step 3: Start the shard servers that will store the actual data.***

```javascript
// Start shard servers
mongod --shardsvr --replSet shardReplSet1 --port 27022 --dbpath /data/shard1
mongod --shardsvr --replSet shardReplSet2 --port 27023 --dbpath /data/shard2
```

***Step 4: Start the mongos instance that will route queries to the appropriate shards.***

```javascript
// Start mongos
mongos --configdb configReplSet/localhost:27019,localhost:27020,localhost:27021 --port 27017
```

***Step 5: Connect to the mongos instance and add the shards to the cluster.***

```javascript
// Connect to mongos
mongo --port 27017

// Add shards to the cluster
sh.addShard("shardReplSet1/localhost:27022");
sh.addShard("shardReplSet2/localhost:27023");
```

***Step 6: Enable sharding on a specific database and collection.***

```javascript
// Enable sharding on the database
sh.enableSharding("myDatabase");

// Shard the 'users' collection on the 'userId' field
sh.shardCollection("myDatabase.users", { userId: 1 });
```

**Use Cases:**

- **Large Datasets:** Distribute large datasets across multiple servers to manage storage and performance.

- **High Throughput:** Handle high query rates by distributing the load across multiple shards.

- **Geographically Distributed Data:** Store data closer to users by distributing shards across different geographic locations.

### Deploying a MongoDB server using MongoDB Atlas

- Deploying a MongoDB server using MongoDB Atlas, especially the free tier `M0`, is a straightforward process.

- MongoDB Atlas is a fully managed cloud database service that simplifies the deployment, management, and scaling of MongoDB databases. Below are the steps to deploy a MongoDB server using MongoDB Atlas free tier:

**Step 1: Sign Up for MongoDB Atlas:**

1. Go to the [MongoDB Atlas website](https://www.mongodb.com/products/platform/atlas-database).

2. Click on "Start Free" and sign up for an account.

**Step 2: Create a New Cluster:**

1. After signing in, click on "Build a Cluster".

2. Choose the free tier option (M0 Sandbox).

3. Select your preferred cloud provider and region.

4. Click "Create Cluster".

**Step 3: Configure Cluster:**

1. Wait for the cluster to be created (this may take a few minutes).

2. Once the cluster is ready, click on "Collections" to create a new database and collection.

**Step 4: Add a Database User:**

1. Go to the "Database Access" tab.

2. Click on "Add New Database User".

3. Enter a username and password.

4. Assign the user appropriate roles (e.g., "Read and write to any database").

5. Click "Add User".

**Step 5: Whitelist IP Address:**

1. Go to the "Network Access" tab.

2. Click on "Add IP Address".

3. You can either add your current IP address or allow access from anywhere (0.0.0.0/0) for development purposes.
  
4. Click "Confirm".

**Step 6: Connect to Your Cluster:**

1. Go back to the "Clusters" tab.

2. Click on "Connect" for your cluster.

3. Choose "Connect Your Application".

4. Copy the connection string provided.

**Step 7: Connect Using MongoDB Shell or Application:**

1. Using MongoDB Shell:

   ```javascript
   mongo "your-connection-string"
   ```

   ***Note:*** Replace `your-connection-string` with the connection string you copied, and make sure to replace `<password>` with the password for your database user.

2. Using a Node.js Application

   ```javascript
   const { MongoClient } = require('mongodb');
   const uri = "your-connection-string";
   const client = new MongoClient(uri, { useNewUrlParser: true, useUnifiedTopology: true });

   async function run() {
   try {
    await client.connect();
    console.log("Connected to MongoDB Atlas");
    // Perform operations
    } finally {
    await client.close();
    }
    }
    run().catch(console.dir);
   ```

***Note:*** Replace `your-connection-string` with the connection string you copied, and make sure to replace `<password>` with the password for your database user.

***This setup provides a fully managed, cloud-based MongoDB instance suitable for development and testing purposes.***

***For more information refer to Official Docs:***

- [Official Docs on Replica Sets](https://docs.mongodb.com/manual/replication/)
  
- [Official Docs on Sharding](https://docs.mongodb.com/manual/sharding/)

## 8. Transaction

- In MongoDB, a `transaction` is a sequence of one or more operations that are executed as a single unit of work. Transactions ensure that the operations are atomic, consistent, isolated, and durable (ACID).

- This means that either all the operations in the transaction are applied, or none of them are.

### Use Cases for Transactions in MongoDB

- **Multi-Document Operations:** When you need to update multiple documents in a single operation to ensure data consistency.

- **Cross-Collection Operations:** When operations span multiple collections and you need to ensure that all changes are applied atomically.

- **Complex Business Logic:** When implementing complex business logic that requires multiple steps, transactions ensure that either all steps are completed or none are.

- **Financial Applications:** Ensuring that financial transactions are processed correctly and consistently.

**Example:**

***how to perform a transaction in the MongoDB shell:***

```javascript
// Start a session.
const session = db.getMongo().startSession();

// Start a transaction.
session.startTransaction();

try {
  // Get the collections.
  const coll1 = session.getDatabase('test').getCollection('example1');
  const coll2 = session.getDatabase('test').getCollection('example2');

  // Perform operations within the transaction.
  coll1.insertOne({ name: 'Alice' });
  coll2.insertOne({ name: 'Bob' });

  // Commit the transaction.
  session.commitTransaction();
  print('Transaction committed.');
} catch (error) {
  // Abort the transaction in case of an error.
  session.abortTransaction();
  print('Transaction aborted due to an error:', error);
} finally {
  // End the session.
  session.endSession();
}
```

***This above example demonstrates how to start a session, perform operations within a transaction, and commit or abort the transaction based on whether an error occurs.***

***For more information refer to official docs***

- [Official Docs on Transactions](https://docs.mongodb.com/manual/core/transactions/)

## 9. Introduction Of Stitch

### What is Stitch?

- MongoDB `Stitch` is a backend-as-a-service (BaaS) provided by MongoDB.

- It allows developers to build applications faster by providing a suite of backend services and features, such as:

1. **Serverless Functions:** Write and deploy functions that run in response to database changes, HTTP requests, or scheduled intervals.

2. **Data Access Rules:** Define fine-grained access control rules for your data.

3. **Authentication:** Integrate various authentication providers like Google, Facebook, and custom JWT.

4. **Mobile Sync:** Synchronize data between your mobile application and MongoDB Atlas.

5. **Third-Party Services:** Integrate with other services like AWS, Twilio, and more.

***Note:***

**`Stitch`** has been rebranded as **`MongoDB Realm`**, which continues to offer these features along with additional capabilities for mobile and web application development.

***Example:***

let's build a simple `CRUD (Create, Read, Update, Delete) application` using `MongoDB Stitch` (now MongoDB Realm) for a `Note app`. Here's a step-by-step guide:

**1. Set Up MongoDB Realm:**

- **Create a MongoDB Atlas Cluster:** If you don't have one, create a MongoDB Atlas cluster.

- **Create a Realm App:** Go to the Realm section in MongoDB Atlas and create a new Realm app.

- **Configure Authentication:** Enable anonymous authentication for simplicity.

- **Create a MongoDB Service:** Link your Realm app to your MongoDB Atlas cluster.

***Note:- MongoDB Realm (App Services) typically requires at least an M2 or higher tier cluster. for M0 (free tier) it's not available***

**2. Define the Schema:**

Create a collection named `notes` in your MongoDB Atlas cluster with the following schema:

```javascript
{
  "title": "string",
  "content": "string",
  "createdAt": "date"
}
```

**3. Set Up Data Access Rules:**

Define rules to allow read and write access to the `notes` collection.

**4. Create Functions:**

Create serverless functions for each `CRUD` operation.

**Create Note:**

```javascript
exports = async function createNote(title, content) {
  const collection = context.services.get("mongodb-atlas").db("your_db_name").collection("notes");
  const result = await collection.insertOne({
    title: title,
    content: content,
    createdAt: new Date()
  });
  return result.insertedId;
};
```

**Read Note:**

```javascript
exports = async function readNotes() {
  const collection = context.services.get("mongodb-atlas").db("your_db_name").collection("notes");
  return await collection.find({}).toArray();
};
```

**Update Note:**

```javascript
exports = async function updateNote(id, title, content) {
  const collection = context.services.get("mongodb-atlas").db("your_db_name").collection("notes");
  const result = await collection.updateOne(
    { _id: BSON.ObjectId(id) },
    { $set: { title: title, content: content, updatedAt: new Date() } }
  );
  return result.modifiedCount;
};
```

**Delete Note:**

```javascript
exports = async function deleteNote(id) {
  const collection = context.services.get("mongodb-atlas").db("your_db_name").collection("notes");
  const result = await collection.deleteOne({ _id: BSON.ObjectId(id) });
  return result.deletedCount;
};
```

**5. Frontend Integration:**

Use the `Realm Web SDK` to integrate these functions into your frontend application.

**HTML:**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Note Taking App</title>
</head>
<body>
  <h1>Note Taking App</h1>
  <div id="notes"></div>
  <button onclick="createNote()">Create Note</button>
  <script src="https://unpkg.com/realm-web/dist/bundle.iife.js"></script>
  <script src="app.js"></script>
</body>
</html>
```

**JavaScript (app.js):**

```javascript
const app = new Realm.App({ id: "your-realm-app-id" });

async function login() {
  const credentials = Realm.Credentials.anonymous();
  await app.logIn(credentials);
}

async function createNote() {
  const title = prompt("Enter note title:");
  const content = prompt("Enter note content:");
  const result = await app.currentUser.callFunction("createNote", title, content);
  alert(`Note created with ID: ${result}`);
  loadNotes();
}

async function loadNotes() {
  const notes = await app.currentUser.callFunction("readNotes");
  const notesDiv = document.getElementById("notes");
  notesDiv.innerHTML = "";
  notes.forEach(note => {
    const noteDiv = document.createElement("div");
    noteDiv.innerHTML = `<h2>${note.title}</h2><p>${note.content}</p>`;
    notesDiv.appendChild(noteDiv);
  });
}

login().then(loadNotes);
```

***This setup allows you to perform CRUD operations on notes using MongoDB Realm, providing a backend service for your note app.***

***For more information refer Official Docs:***

- [MongoDB Realm documentation](https://www.mongodb.com/docs/atlas/device-sdks/)
