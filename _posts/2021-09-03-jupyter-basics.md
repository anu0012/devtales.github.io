---
layout: post
title: Getting started with Jupyter notebook
cover-img: /assets/img/path.jpg
share-img: /assets/img/path.jpg
tags: [Machine Learning, Python, Jupyter, Tools and Libraries]
---

In this blog, we'll discuss a very powerful interactive computing environment Jupyter Notebook that helps us to create documents with live code, interactive plots, markdown text, images, etc. Project Jupyter is a non-profit, open-source software. It came out of the IPython project in 2014, as it evolved to support interactive data science and scientific computing in all programming languages. Jupyter is developed on Github in the open, unanimously from the Jupyter community.

Jupyter Notebook is quite popular amongst the data science community. You can directly run it from the browser, edit it, and export it in different formats such as Python script, HTML page, pdf document, etc. It is a nice way to present any data science project. In this article, we'll see how we can install it in our local machine and start using it for data science projects.

Let's start by installing it in our machine. There are two ways to get started with Jupyter notebooks. One way is by installing [Anaconda](https://anaconda.org/) and another one by directly installing the package using pip. 
In order to install it using Anaconda:

1. We need to download the latest version of [Anaconda](https://www.anaconda.com/download/) for Python 3.
2. Now install it in your local machine by following the instructions on the download page.

Anaconda comes with many pre-installed libraries and tools like pandas, numpy, matplotlib, etc. It helps us to avoid installing different packages separately. 

The next option is to install using pip command. In your local machine, Python has to be installed. If not, you can download it from there [website](https://www.python.org/downloads/). Then open a terminal and run below command:

`pip install jupyter`

And that's it. You have successfully installed Jupyter notebook in your local machine. Let's see how to create our first notebook and save it. In order to open Jupyter, go to the terminal and run `jupyter notebook` command. It'll open a window like this in your browser.

![alt text](https://www.dropbox.com/s/a79qdn0znpaswns/Screen%20Shot%202019-12-15%20at%2010.32.28%20AM.png?dl=0)

This is the Jupyter dashboard where you can find the jupyter notebooks of the current working directory. If you want to launch it from another folder, just change directory in the terminal and run `jupyter notebook` command from there. 
This dashboard shows `http://localhost:8888/tree` as the URL, which means the content is being served from the local machine. You can make yourself familiar with the interface. It's quite simple and self-explanatory. On the right side there is `New` button. By clicking on it you'll see few options like Python 3, Text file, terminal, folder etc.

![alt text](https://www.dropbox.com/s/wdj2mjncti11yt6/Screen%20Shot%202019-12-15%20at%2010.32.49%20AM.png?dl=0)

Click on Python 3 to create a new Jupyter notebook. This new Jupyter Notebook will open in a new tab named as Untitled.ipynb
Every .ipynb file is a text file that describes the contents of our jupyter notebook in a JSON format. Inside the notebook, we'll create `cells` to add code into it. A cell contains the code to be executed by the notebook's kernel. We can execute a cell by `Ctrl + Enter` command or by clicking on the `>| Run` icon on top of the menu bar. As soon as we run it, we can see the output below the cell. 

In the menubar, there is a drop-down, which has `Code` in it as default. If we click on it, we see other options like Markdown, Heading etc. On selecting Markdown, our cell becomes a Markdown cell where we can use Markdown syntax also. On top of the notebook, it has its name. By default, it takes `Untitled`, which can be changed by clicking on it and renaming it. In the second toolbar, there is `Save` icon. By clicking on it, we can save our work. By default, it saves the checkpoint after every 120 seconds.

That's it for now. In the next article, we'll try to discuss some tips and tricks for Jupyter notebooks. :)

