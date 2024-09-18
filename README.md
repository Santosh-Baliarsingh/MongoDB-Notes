
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
  - [Creating Database and Collection](#creating-database-and-collection)
    - [Show All Databases](#show-all-databases)
    - [Create Database](#create-database)
    - [Create a Collection](#create-a-collection)
  - [Create a Document](#create-a-document)
    - [insertOne Method](#insertone-method)
    - [insertMany Method](#insertmany-method)
  - [Read a Document](#read-a-document)
    - [find Method](#find-method)
    - [find Method with Query](#find-method-with-query)
    - [find Method with Projection](#find-method-with-projection)
    - [findOne Method with Query](#findone-method-with-query)
    - [findOne Method with Projection](#findone-method-with-projection)

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

## Creating Database and Collection

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

This query will match "Alice Smith" regardless of the case of "Smith".

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
