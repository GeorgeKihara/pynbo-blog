---
Title: Pymongo in flask
Tags: python, flask, mongodb
Date: 2017-09-22 15:10:00
Slug: pymongo
Summary: A brief demo of pymongo in flask
Author: George Kihara
email: gegohcomp@gmail.com
about_author: <p>A software developer in Nairobi and loves Python. Check out <a href="https://georgekihara.github.io/">home page</a>
---

Pymongo has become one of the easiest ways to store data from python-flask web apps.

I'm sure nobody would want to stress up doing hard stuff if there are other easier means to do them.

I discovered pymongo when i was developing a small website for a project in school, and after discovering how simple it is, i've been using it for my small projects.
After going through this tutorial, I'm hoping you will feel the same.

<h2><b>Prerequisites</b></h2>
So to begin with, make sure you have the PyMongo distribution installed. In the python shell, run the following:

``` python
>>> import pymongo
```
I'm hoping that MongoDB instance is running on the default host and port. So if MongoDb is installed, you can start it:
``` python
$ mongod
```
<h2>Set up connection with Mongoclient</h2>
After the prerequisites, the next step is to create a MongoClient to the running  mongod instance.
```python 
>>> from pymongo import MongoClient
>>>client = MongoClient()
```
You can specify the host and port as follows:
```python
>>> client = MongoClient('localhost', 5000)
#alternatively
>>> client = MongoClient('mongodb://localhost:5000/')
```

Now that we are done with the necessary connections, lets get into the more interesting part:
<h2> Creating a database</h2>
With PyMongo you access databases using attribute style access on MongoClient instances, as follows:
```python
>>> db = client.database1
#or if that does not work use the following
>>> db = client['database1']
```
<h2> Creating a collection</h2>
A collection is a group of documents that are stored in MongoDB, its the equivalent of a table in relational databases. To create the collection:
```python
>>> collection = db.collection1
#using dictionary-style access
>>> collection = db['collecion1']
```

<h2>Documents</h2>
We represent data in MongoDB using JSON-style documents. In PyMongo we use dictionaries to represent documents. For example:
```python
>>> post = {"author": "George",
...         "text": "My first tutorial",
...         "tags": ["mongodb", "python", "pymongo"]}

```
<h2>Inserting a Document</h2>
To insert a document into a collection we can use the insert_one() method:
```python
>>> posts = db.posts
>>> post_id = posts.insert_one(post).inserted_id
>>> post_id
ObjectId('...')
```

<h2>Using <b>find_one()</b></h2>
To perform a query in MongoDB, we can use <b>find_one()</b>. This method will return a single document matching a query or None if there are no matches. For example:
```python
>>> print (posts.find_one())
{u'_id': ObjectId('...'),
 u'author': u'George',
 u'tags': [u'mongodb', u'python', u'pymongo'],
 u'text': u'My first tutorial'}
 ```
