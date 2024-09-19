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
 {$set : {profile :{city : 'Somewhere in the world' , pet :'cats'}}})
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
use your_database_name // //  replace your_database_name with actual database name
db.your_collection_name.deleteMany({}) // // replace your_collection_name with actual collection name
```

Expected Output:

```sh
{ acknowledged: true, deletedCount: 5 }
```
