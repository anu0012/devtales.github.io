---
layout: post
title: Getting started with Puppeteer
cover-img: /assets/img/path.jpg
share-img: /assets/img/path.jpg
tags: [Puppeteer, Tools and Libraries]
---

We all must have heard about Selenium/Web Driver for automation testing. Selenium is focused on cross browser automation. In this article we'll discuss about another library for automation. Puppeteer is mainly focused on testing for Chromium. It’s a very useful tool for automation, testing and scraping web pages. Puppeteer is a Node.js library which provides a high-level API to control Chrome or Chromium over the DevTools protocol. It runs headless by default which means no need to open the browser to use it. This configuration can be changed. Pupperteer comes bundled with the Chromium version it works best with.

Using Puppeteer we can automate a lot of things for example:

 * We can generate screenshots and PDFs of webpages.
 * Crawl a webpage and generate pre-rendered content
 * Automate form submission, keyboard input, UI testing etc.
 * Create an automated testing environment. 
 * Test Chrome Extensions
 * and many more...

Let's get started by installing it in our local machine. By using following command we can install Puppeteer:

`npm i puppeteer`

or 

`yarn add puppeteer`

Puppeteer comes with a latest version of Chromium so when we run this command, it automatically downloads Chromium also.

Let us see how we can use it for some automation.

First we need to import the puppeteer module. 

`const puppeteer = require('puppeteer');`

Then we'll create a browser instance.

`const browser = await puppeteer.launch();`

Now we have to create a page instance and open the desired URL.

```
const page = await browser.newPage();
await page.goto('http://google.com/', {waitUntil: 'networkidle2'});
```

By calling screenshot function we can capture the screenshot of that webpage. In that function we can pass the path where we want to save the output file.

`await page.screenshot({path: 'screenshot.png'});`

Similarly we can save the PDF of that page using .pdf method.

`await page.pdf({path: 'document.pdf', format: 'A4'});`

This is how our complete code looks like:

```
const puppeteer = require('puppeteer');

(async () => {
  const browser = await puppeteer.launch();
  const page = await browser.newPage();
  await page.goto('http://google.com/', {waitUntil: 'networkidle2'});
  await page.pdf({path: 'document.pdf', format: 'A4'});
  await page.screenshot({path: 'screenshot.png'});

  await browser.close();
})();
```

Here is the screenshot of the output:

![alt text](https://www.dropbox.com/s/344hb3yyyxgcbje/Screen%20Shot%202019-12-26%20at%204.28.55%20PM.png?dl=0)

![alt text](https://www.dropbox.com/s/c6rdbqu19wlgyxb/Screen%20Shot%202019-12-26%20at%204.28.35%20PM.png?dl=0)

By default, Puppeteer starts Chromium in headless mode. In order to launch a full version of Chromium, we need to set the headless option when launching a browser:

`const browser = await puppeteer.launch({headless: false});`

In order to open the webpage in incognito mode we can use this:

`const newContext = await browser.createIncognitoBrowserContext();`

We can do event handling with pupeteer. Let's see an example. 

The `Page` class supports various event handling methods like `on, once etc.`

`await page.once('domcontentloaded', () => console.info('DOM loaded'));` 

We can also control mouse and keyboard using this library. See the example below:

```
const puppeteer = require('puppeteer');

(async () => {
  const browser = await puppeteer.launch({headless:false});
  const page = await browser.newPage();
  await page.goto('https://duckduckgo.com/', {waitUntil: 'networkidle2'});
  await page.click('#search_form_input_homepage');
  await page.keyboard.type('Hello world!!!');
  await page.click('#search_button_homepage');
  await page.waitForNavigation();

  await browser.close();
})();
```

In the click function we can pass the id of the element. This example will launch Chromium browser and open the URL. After opening it'll try to find out the given id element and click on it. Then it'll type the text in the input element and click enter to search. Here is how it looks like:

[Image 1](https://www.dropbox.com/s/hspydrg8faevfzo/Screen%20Shot%202019-12-19%20at%2010.25.30%20AM.png?dl=0)
[Image 2](https://www.dropbox.com/s/xoi3pqtp5mx7dsc/Screen%20Shot%202019-12-19%20at%2010.26.03%20AM.png?dl=0)

In essence we learned how we can programmatically control Chrome from Node.js using puppeteer library. Here we discussed very few things about this awesome library but it can do a lot more than this. We can use it for debugging, web scrapping, automation, testing and for fun also :)
I hope you guys must have found this library useful. Now it's your turn to use puppeteer and automate some awesome stuff. :)