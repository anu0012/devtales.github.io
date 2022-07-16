<b>Title:</b> Caching in Python applications
<b>Author:</b> Anurag Sharma

<b>Track Category:</b> Development
<b>Subcategory:</b> Programming
<b>Tags:</b> Python, Language, Tools and Libraries

<b>Read Time:</b>  10 min

[Banner Image](https://www.dropbox.com/s/622zq50qi1h6rcl/markus-spiske-qjnAnF0jIGk-unsplash.jpg?dl=0)

# Content

In web application, many times we have to use the same data again and again or some calculations have to be performed again when we visit some page. If we recompute them again or access the data from some slow database it can hamper the performance of our application. To overcome this problem we can use `Caching` method. It may sound a fancy term but I am sure you must have used one or more of the following methods to achieve Caching. Let's discuss how we can implement it in our applications. In two ways we can store cache data - one at Client side and another at Server Side.

1. Client Side Caching -

### Python Dictionary

We can use a python dictionary to get the data in constant time instead of recomputing it. It has linear time complexity O(1). Let's see its example -

```
phonebook = dict()
phonebook['James'] = 9453852201
phonebook['Rahul'] = 5956983692

print(phonebook['James'])
```

### Session in Flask

Flask provides a session object which is nothing but a dictionary. Here you can store data which is required quite frequently for your application. Let's see how to implement it -

```
from flask import Flask, session, redirect, url_for, escape, request
app = Flask(__name__)
app.secret_key = 'random_string’

@app.route('/')
def index():
   	if 'username' in session:
   		username = session['username']
   		return "Already logged in"
   	else:
   		return "Not logged in."

@app.route('/login', methods = ['GET', 'POST'])
def login():
   if request.method == 'POST':
      session['username'] = request.form['username']
      return redirect(url_for('index'))
   else:
   	  return render_template('login.html')
```

2. Server Side Caching -

So far we've discussed about client side data storage. Now take a scenario of a e-commerce shopping cart where you put some items in the cart and close the website. Later when you come back to complete the purchase you are supposed to see the same cart items. A user will not want to again fill the cart. For this purpose, we have to store the data in the server side using cache memory instead of some session variable at client side. There are many databases to achieve this method like Redis, Memcache, MongoDB etc.

### Redis

Redis is a cloud based key/value storage. We can store our application data on Redis memory which we want to retrieve frequently. Redis is easy to implement and fast. You can find more details at [this](https://redis.io)

For python implementation, we need to install the redis-server in our local machine using following command.

`pip install redis`

`pip install redis-server`

In production environment, you can leverage the benefits of docker as it has already the redis image implemented there. Apart from this, we can also use cloud based alternatives like Google Cloud Platform or Microsoft Azure. They also provide Redis instances.

After installing `redis-server` we need to run it in the terminal using - 

`redis-server`

To leverage Redis in our web application(in this case Flask) we'll use `Flask-Session` library.

`pip install flask-session` 

Following is the implementation of redis session.

```
import os
from flask import Flask, session, flash
import redis
from flask_session import Session

app = Flask(__name__)
# Configuration Variables
app.config["DEBUG"] = True

conn_redis =redis.from_url('redis://localhost:6379')
sess = Session()
sess.init_app(app)

# to set a value
session['key'] = 'value'

# to get a value
session,get('key')
```

Flask-Session extends the Flask `session` object so it'll work the same way like we see earlier. We just need to configure it using the above code.

That's all for now. I hope you like this blog. Try to utilize one of these methods to improve the performance of your web application. Happy coding :)
