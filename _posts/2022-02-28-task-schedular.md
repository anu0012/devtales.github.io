---
layout: post
title: Task Scheduling with Python
cover-img: /assets/img/path.jpg
share-img: /assets/img/path.jpg
tags: [Python, Schedular, Tools and Libraries]
---

We run many tasks in our day to day work that can be done through automation instead of doing it repetitively. A task schedular allows you to run your task after a particular period of time. The scheduler can be scheduled to perform a task at the given time. It can be weekends or daily. Scheduling can be useful to fetch the data from a database or to store some data periodically. Scheduling can also be used to train machine learning models as the new data comes. Let's see how we can achieve it using python.

Python provides a generic schedular module named `schedule.` By using this module, we can easily run our script after a fixed time. You can install it using the following command - 

`pip install schedule`

Let's see an example -

``` 
import schedule
import io
import sys
import time
import pickle
import os
import json
from urllib.request import urlopen
from datetime import date

today = date.today()

URL = 'https://api.exchangerate-api.com/v4/latest/USD'

def wait_for_internet_connection():
    while True:
        try:
            ### Random url to check for internet connection
            response = urlopen('http://216.58.192.142',timeout=1)
            return
        except Exception as e:
            ### Logs can be captured
            pass

def job():
    print("Loading...")
    response = urlopen(URL,timeout=5).read()
    response.decode('utf8').replace("'", '"')
    inr_rate = json.loads(response)['rates']['INR']
    file = open('output.txt','a') 
    file.write(today.strftime("%d/%m/%Y") + ' - ' + str(inr_rate) + '\n')
    file.close() 

schedule.every().day.at("10:30").do(job)            ### Everyday at 10:30
#schedule.every(5).seconds.do(job)                  ### Every 5 seconds
#schedule.every().sunday.at("10:30").do(job)        ### Every Sunday at 10:30

while 1:
	wait_for_internet_connection()
	schedule.run_pending()
	time.sleep(1)
```

You can save this file as `script.py`. In this example, we are calling a REST API to get the conversion rate from USD to INR. We created a `wait_for_internet_connection` function to check for network connectivity otherwise, our script may cause an error and stop abruptly.  

`run_pending()` function runs all jobs that are scheduled to run. We have to keep it in a loop so that it can be running all the time.
Suppose we want to get the conversion of day to day basis and want to run it at a fixed time, we can achieve this by `every()` function of schedule module. 

`schedule.every().day.at("10:30").do(job)`

This function takes an input which is the job needs to be performed. Once the machine time reaches the scheduled time, it calls the `do` function which performs the job.

`at(time_str)` function takes a time string in HH:MM format.

To keep this script running, we need to open a terminal or console and run it `python script.py` Now just leave it running.

That's it. This script will execute the function based on your machine time when it reaches the given time period.

There are many other libraries also which can be used to perform scheduling. The only disadvantage of this approach is that in order to run the script in the background we have to keep our machine ON all the time. For production tasks, we can either build our own server and perform scheduling there or we can use some third party cloud-based services. 

That's all for now. Now it's your turn to try scheduling for your routine tasks. Happy coding :)