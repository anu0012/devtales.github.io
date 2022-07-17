---
layout: post
title: Asynchronous Tasks with Redis Queue
cover-img: /assets/img/path.jpg
share-img: /assets/img/path.jpg
tags: [Python, Redis Queue, Language, Tools and Libraries]
---

Many of us might have faced some problem while handling long-running tasks in our web application. It could be uploading an image file, applying some filter in it and show it on the screen once done, or It could be to related to report generation from an uploaded excel file. In either case, if the task is taking significant amount of time, you can't hold the UI and let the user wait for long. The solution is to run such task in the background and inform the user once they are done either using a notification or by sending an email. We'll see how we can do that using Redis Queue. For this tutorial, we'll be using Python Flask framework as backend and [Redis Queue](https://python-rq.org/) library for queueing jobs and processing them in the background with the help of workers. Don't worry I'll explain all the terminologies like workers, queues etc. in the later part of the blog.

A worker is a Python process that typically runs in the background and exists solely as a work horse to perform lengthy or blocking tasks that you don’t want to perform inside web processes.

A `Queue` is a data structure that follows first-in-first-out method. That means the first task to be enter will be the first one to be executed.

In this example we'll send a POST request to the back-end server and store the task in the queue which will be handled by the Redis Worker. Once the task is completed the worker will send a response to the server that the task is completed.

### Installation

We can install the redis queue library for python from this command - 

`pip install rq`

[Official Website](https://python-rq.org)

We also need to install redis server in our machine using following command - 

`pip install redis-server`

After installing redis-server we need to run it in a terminal window before running our flask app - 

`redis-server`

It'll look something like this.

![redis-server](https://www.dropbox.com/s/zt4j06jzg03f2dz/redis-server.png?dl=0)

### Getting started

Now Let's start with creating a worker.

```
import os
import redis
from rq import Worker, Queue, Connection

listen = ['default']
conn_redis =redis.from_url('redis://localhost:6379')

if __name__ == '__main__':
    with Connection(conn_redis):
        worker = Worker(list(map(Queue, listen)))
        worker.work()
```

We need to save it as worker.py and run it in a terminal `python3 worker.py` This code will start the connection to our worker.

It'll look something like this.

![worker](https://www.dropbox.com/s/vwozwv214gx1c47/worker.png?dl=0)

Here we can see all the jobs running and completed.

Now we need to write end-points for our flask application.

```
import os
from flask import Flask, session, flash
import redis
import time
from rq import Queue
from rq.job import Job
from worker import conn_redis

q = Queue(connection=conn_redis,default_timeout=7200)

app = Flask(__name__)
# Configuration Variables
app.config["DEBUG"] = True

def background_work():
    time.sleep(10)
    return True

@app.route('/')
def home():
    from app import background_work
    job = q.enqueue_call(
        func=background_work,)
    return 'ok'

@app.route('/get/')
def get():
    print(q.jobs)
    return str(len(q))

if __name__ == '__main__':
	port = int(os.environ.get('PORT',9090))
	app.run(host='0.0.0.0',port=port)
```

In this code, we created a `Queue` instance which will be connected to out redis connection url. We created two endpoints one is index `/` where we can create jobs and put them in job queue using `enqueue` method. This enqueue method takes a function as a parameter which is the background task we need to perform. It can be image upload/report generation or some other high computational task. We can also pass some arguments to our method like this `q.enqueue_call(func=background_work,args=(param1,param2...))`

Now save this file as app.py and let's run our application in a terminal using `python3 app.py` 

In the browser if we open `0.0.0.0:9090` then it'll hit out end-point and create a job task by calling background_work function. This function sleeps for 10 sec. and then it is completed. So we can create more such tasks by refreshing our browser page multiple times. In the worker, it'll look like this - 

![jobs list](https://www.dropbox.com/s/5sk1w5w6hz0qqhn/tasklist.png?dl=0)

Now if we go to `0.0.0.0:9090/get` we can see the number of jobs enqueued in our job queue. After each 10 sec. this number gets reduce by one.
We can put some notification/email to be send to the end user once their job is done. 

That's it. You have built your first job queue. Now try to integrate it in your app and explore some of its features. I hope you like this article. Happy coding :)