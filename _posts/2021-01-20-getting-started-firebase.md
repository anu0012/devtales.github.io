---
layout: post
title: Getting started with Firebase Cloud Firestore using Python
cover-img: /assets/img/path.jpg
share-img: /assets/img/path.jpg
tags: [Firebase, Python, Tools and Libraries]
---

Firebase is a mobile platform which can be used to quickly develop high-quality apps and manage its analytics. It is acquired by Google in 2014. 
It provides a lot of features to developers some of these are following:

- Using Cloud Firestore and Cloud Storage we can Sync our data with our app.
- Firebase auth for user authentication
- Firebase hosting for deploying our web app
- Send notifications using Firebase Cloud Messaging.
- Manage web app's performance data using Firebase Analytics
- And many more...

In this article we'll find how we can use a server-side option to read and write data in Cloud Firestore outside the client using Firebase Admin SDK. For this tutorial we'll be using Python. 

Let's start by creating our first project. Firebase is now aquaired by Google so by using our Google account we can sign in into [Firebase](https://console.firebase.google.com/u/0/). 

Now in the Firebase console, we need to click `Add Project`, and then name your Firebase project. Remember the project ID for your Firebase project. 

![alt text](https://www.dropbox.com/s/4nph0oqbr8i9gnq/Screen%20Shot%202019-12-30%20at%2011.44.42%20PM.png?dl=0)

![alt text](https://www.dropbox.com/s/bm7lcai4rszrwuo/Screen%20Shot%202019-12-30%20at%2011.45.13%20PM.png?dl=0)

After creating your first project, you can see a screen like this.

![alt text](https://www.dropbox.com/s/r28blbwkdaio9ym/Screen%20Shot%202019-12-30%20at%2011.47.22%20PM.png?dl=0)

Now we have to get the service account credentials. For that we need to click on the settings icon near `Project Overview` and click on `Project Settings`. Now go to `Service Accounts` tab and click on `Generate new private key` to download the service credentials JSON file.

![alt text](https://www.dropbox.com/s/ek5vdydimhumpf2/Screen%20Shot%202019-12-30%20at%2011.59.44%20PM.png?dl=0)

Now install Firebase Admin SDK using the following command:

`sudo pip install firebase-admin`

Let's get started with coding. First we have to import the libraries and initialize the SDK using our downloaded service account credentials.

```
import firebase_admin
from firebase_admin import credentials

cred = credentials.Certificate("serviceAccountKey.json")
firebase_admin.initialize_app(cred)
```

Now we have to initialize the firestore instance.

`firestore_db = firestore.client()`

Now in the Firebase portal, go to `Datebase` section and click `Create Database` to create a new database.

![alt text](https://www.dropbox.com/s/yoonr86hsjuhzae/Screen%20Shot%202019-12-31%20at%2012.22.13%20AM.png?dl=0)

![alt text](https://www.dropbox.com/s/roklya09g03ziue/Screen%20Shot%202019-12-31%20at%2012.22.29%20AM.png?dl=0)

It will open up a window like this after creating the database. 

![alt text](https://www.dropbox.com/s/ib55gt95isy8jog/Screen%20Shot%202019-12-31%20at%2012.24.21%20AM.png?dl=0)

Now we need to create a collection to store our data. For that, we need to click on `Start Collection` and give a collection name. In the next step, we need to create our first document. We can create a field and its value in it. We can also select the datatype of the field. Firestore supports string, number, boolean, map, array, null, timestamp, geopoint, and reference. 

![alt text](https://www.dropbox.com/s/6u6e8d3tz1c5fei/Screen%20Shot%202019-12-31%20at%2012.25.58%20AM.png?dl=0)

![alt text](https://www.dropbox.com/s/1we7uw65vl96xpc/Screen%20Shot%202019-12-31%20at%2012.33.06%20AM.png?dl=0)

Let's start adding documents through our python code. For that we'll use `.add()` of firestore. 

`firestore_db.collection(u'songs').add({'song': 'Imagine', 'artist': 'John Lennon'})`

It will create a new document in the DB like this:

![alt text](https://www.dropbox.com/s/abs7193jcduaj9c/Screen%20Shot%202019-12-31%20at%201.10.37%20AM.png?dl=0)

Now let's read the documents from our collection. For that we'll use `.get()` method.

```
snapshots = list(firestore_db.collection(u'songs').get())
for snapshot in snapshots:
    print(snapshot.to_dict())
```

Following is the complete code for this tutorial.
```
import firebase_admin
from firebase_admin import credentials, firestore

# initialize sdk
cred = credentials.Certificate("serviceAccountKey.json")
firebase_admin.initialize_app(cred)

# initialize firestore instance
firestore_db = firestore.client()

# add data
firestore_db.collection(u'songs').add({'song': 'Imagine', 'artist': 'John Lennon'})

# read data
snapshots = list(firestore_db.collection(u'songs').get())
for snapshot in snapshots:
    print(snapshot.to_dict())
```

That's all for now. In this blog we learnt the basics of Firebase firestore. It is very easy to use. You should give it a try in your next project. Till then happy coding :) 