---
layout: post
title: Getting started with MongoDB
cover-img: /assets/img/path.jpg
share-img: /assets/img/path.jpg
tags: [MongoDB, Tools and Libraries]
---

MongoDB is a general purpose, distributed database built for modern application developers and for the cloud era. It is an open-source database and one of the most popular NoSQL database. MongoDB is easy to scale. It is a document database, which means it stores data in JSON-like documents. It supports arrays and nested objects as values and allows for flexible and dynamic schemas. It has a powerful query language that allows us to filter and sort by any field, irrespective of how nested it may be within a document. MongoDB supports for aggregations and other modern use-cases such as geo-based search, graph search, and text search. It supports all the facilities of relation databases like ACID transactions, joins in queries and more. In this article we'll try to understand the basics of MongoDB. Let's get started.

MongoDB is based on the concept of collection and document. A database contains collections and each collection contains documents. Each document is used to store the data. We can store different fields in the document for example integer value, string value, date etc. MongoDB supports various type of data. It can store string, Integer, Boolean, Double, Arrays, Timestamp, Null, Symbol, Object etc. Each document follows a key-value structure. We don't need to pre-defined schema but we can create fields as it is required. Let us see an example of a mongodb document.

```
{
   _id: ObjectId(9fs71da8012c),
   title: 'MongoDB Document', 
   description: 'It is a MongoDB document',
   url: 'http://www.mongodb.com',
   tags: ['mongodb', 'database', 'NoSQL']
}
```

As we can see in this example, for each field there is one value. We can store arrays also like in the previous example. `_id` field is used to represent a document uniquely. It is same as primary key in relational database. 

Now let us install MongoDB on our machine and gets our hands on it. Go to mongodb website and download the latest release for your operating system. Here is the link to [download](https://www.mongodb.org/downloads) it. Installation can be done using the instructions given on [installation page](https://docs.mongodb.com/manual/installation/).

After installation you can verify it by opening the mongo shell. Go to terminal and run command `mongo`. It will open mongo shell like this:

![alt text](https://www.dropbox.com/s/4186s174wis5vdi/Screen%20Shot%202019-12-24%20at%206.36.21%20PM.png?dl=0)

We can see what all commands we can use by running `help` in the shell. It will show us all the supported commands.

![alt text](https://www.dropbox.com/s/43qs1ida0by11n8/Screen%20Shot%202019-12-24%20at%206.36.42%20PM.png?dl=0)

Let us create a new database. We can do it by typing `use <DATABASE_NAME>` command. It will use this database as current one. Now you can operate on this database. By running `show dbs` command, we can validate whether the database is created or not. It'll display something like this:

![alt text](https://www.dropbox.com/s/ebm3lcz59wzduvs/Screen%20Shot%202019-12-24%20at%206.36.57%20PM.png?dl=0)

We can create a new collection using `db.createCollection('<COLLECTION_NAME>')`

![alt text](https://www.dropbox.com/s/ym1x93iv9ma0gfp/Screen%20Shot%202019-12-24%20at%207.01.06%20PM.png?dl=0)

Let's create a document in this collection. We can do it by `db.<COLLECTION_NAME>.insert({'firstname': 'James', 'lastname': 'Bond'})`

![alt text](https://www.dropbox.com/s/22wjx8avhcphmah/Screen%20Shot%202019-12-24%20at%207.06.30%20PM.png?dl=0)

We can see the statistics of our database using `db.stats()` command. It displays database name, number of documents and collection like this:

```
{
	"db" : "test_db",
	"collections" : 1,
	"views" : 0,
	"objects" : 1,
	"avgObjSize" : 39,
	"dataSize" : 39,
	"storageSize" : 16384,
	"numExtents" : 0,
	"indexes" : 1,
	"indexSize" : 16384,
	"fsUsedSize" : 130330828800,
	"fsTotalSize" : 249199591424,
	"ok" : 1
}
```

To drop a database we can use `db.dropDatabase()` command. It will drop the selected database.
A collection can be drop using `db.COLLECTION_NAME.drop()` command. 

That's all for now. In this article, we tried to learn some basics of MongoDB. It's just a glimpse of it. You can do a lot more with MongoDB. Now it's your turn to try it out.
