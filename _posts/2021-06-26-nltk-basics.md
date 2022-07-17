---
layout: post
title: Handle text data using NLTK
cover-img: /assets/img/path.jpg
share-img: /assets/img/path.jpg
tags: [Python, NLP, Tools and Libraries]
---

NLTK is a python library which is used to process text data. In Natural Lanuguage Processing(NLP) we deal with human language and before feeding such data into our machine learning model we need to do some processing like removing punctuations, extra spaces etc. NLTK library is very handy and useful to perform such tasks. In this tutorial, we'll see how we can use this library to process our data. So let's get started.

### Installation

Let's start with the installation of the library. You can install it by running following command in terminal - `pip install nltk` 
For Anaconda, you can try this `conda install -c anaconda nltk`

NLTK has many grammer corpora and trained models. To download them use this in python terminal - 

```
>>> import nltk
>>> nltk.download()
```

### Tokenization

Tokenization is the process by which we split a sentence into list of words.

```
text = "Hello world, This is NLTK. You can use me for text data."
tokens = nltk.tokenize.word_tokenize(text)
print(tokens)
```

Output: `['Hello', 'world', ',', 'This', 'is', 'NLTK', '.', 'You', 'can', 'use', 'me', 'for', 'text', 'data', '.']`

### Removing Stopwords

'on','the','a','an','and','but','if','or','because','as' etc. known as Stopwords which do not give any important information about the data. Also, by removing these stopwords we can reduce the size of our data which leads to fast processing. Generally we remove such stop words from the data before feeding it to our model. To do this in NLTK we use the following code - 

```
import nltk
from nltk.corpus import stopwords

text = 'Hello world, This is NLTK. You can use me for text data.'
stops = stopwords.words('english')
words = nltk.tokenize.word_tokenize(text)
print(words)
words_without_stopwords = [i for i in words if i not in stops]
print(words_without_stopwords)
```

Following output we get after running this code - 

```
# These are words(tokens) before removal
['Hello', 'world', ',', 'This', 'is', 'NLTK', '.', 'You', 'can', 'use', 'me', 'for', 'text', 'data', '.']

# These are words after removal
['Hello', 'world', ',', 'This', 'NLTK', '.', 'You', 'use', 'text', 'data', '.']
```

As we can see it removed words like `is, can, me`. There are some words which are not their in NLTK stopwords list like `You`. We can manually append it to the list.

### Removing Punctuations

In the previous example, we removed stopwords from our text. But if we see the output it still has unwanted tokens in the form of punctuations. Here we'll see how to get rid of them.

```
import string
text = "Hello world, This is NLTK. You can use me for text data."
text_without_punctuation = "".join([i for i in text if i not in string.punctuation])
print(text_without_punctuation)
```

This will give us following output.
`Hello world This is NLTK You can use me for text data`

### Stemming

Stemming removes morphological affixes from words, and leaves only the root form. NLTK provides two types of stemmers - Snowball Stemmer and Porter Stemmer.

```
text = "I am singing."
stemmer = nltk.PorterStemmer(language = 'english')
w = [stemmer.stem(word) for word in nltk.tokenize.word_tokenize(text)]
print(w)
```

Output: `['I', 'am', 'sing', '.']`

So far we saw how you can clean your text data with NLTK library in just few lines of code. Hope you liked this tutorial. Now it's your turn to get your hands on it. There are so many more features which you can explore [here](http://www.nltk.org/howto/). I'll see you in next blog till then Happy coding :)