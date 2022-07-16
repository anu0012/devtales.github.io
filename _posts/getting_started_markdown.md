<b>Title:</b> Getting started with Markdown
<b>Author:</b> Anurag Sharma

<b>Track Category:</b> Development
<b>Subcategory:</b> Document
<b>Tags:</b> Markdown, Tools and Libraries

<b>Read Time:</b>  5 min

[Banner Image](https://www.dropbox.com/s/07sfl1merwu7l7w/ilya-pavlov-OqtafYT5kTw-unsplash.jpg?dl=0)

# Content

Markdown is a markup language which has a plain text formatting syntax. John Gruber developed the Markdown language in 2004 in collaboration with Aaron Swartz on the syntax, with the aim of enabling people to write using an easy-to-read and easy-to-write plain text format, optionally convert it to structurally valid HTML. With it we can quickly write structured content for the web, and convert it to clean, structured HTML. Markdown is used by many popular platforms like Github, Jekyll etc. In Github, README files use this format. Markdown is used to format readme files, for writing messages in online discussion forums, and to create rich text with a plain text editor. In this post we'll see how we can use Markdown to write documents. 

1. Heading 

Mardown allows us to convert our text into heading using `#` By putting it in front of the text, we can convert the text into a heading. There are six different types of headers. 

```
# H1 tag
## H2 tag
### H3 tag
#### H4 tag
##### H5 tag
###### H6 tag
```

2. Emphasis

Text emphasis can be given using Markdown. For example - 

```
**bold**
*italics*
__underscores__
~~strikethrough~~
```

3. Quotes

You can quote a text using `>` 

`> I am a quote.`

4. List

We can create both ordered and unordered lists in Mardown. For unordered we can use `*`, `-` or `+`

```
* UnOrdered list item
* UnOrdered list item
* UnOrdered list item

1. Ordered list item
2. Ordered list item
3. Ordered list item
```

5. Links

We can add link using `[Link](URL)` syntax.

`[Download Link](http://www.example.com)`

6. Images

Image can be added in the markdown document using `![alt text](URL)`

`![Beautiful Scene](https://image.shutterstock.com/image-photo/mountains-during-sunset-beautiful-natural-600w-407021107.jpg)`

7. Code Display

We can display our code blocks in Markdown. Both single line code and blocks of code can be displayed.

```
`var x = "hello world!";`

    ```
    var x = "hello world!";
    alert(example);
    ```
```

8. Break

You can insert a `<br>` tag into a paragraph. Or you can hit enter twice to leave an empty line.

9. Horizontal rules

By using `---` three hyphens or `___` three underscores, we can add horizontal rules in between the text.

10. HTML

HTML is valid in Markdown. We can use HTML tags inside Markdown documents. 

```
<!-- This is a comment -->

<p>I am a paragraph.</p>
```

11. Tables

We can create table in markdown by separating each column with a pipe `|`. We can use `--` to create separator in between rows.

```
| Name | Age |
|--|--|
| James | 25 |
```

12. Emojis

We can even add emoji in markdown. Here is the [link](https://gist.github.com/rxaviers/7360908) to know about all the different emojis supported by markdown.

`:smile:` 

That's all for now. In this article, we tried to learn some basics of Markdown. We saw how we can format words as bold or italic, add images, create lists and more. You can do a lot more with Markdown. Now it is your chance to try it out. You can start with writing your very first Markdown document and get a feel of it. You can use [StackEdit](https://stackedit.io/) for online markdown editing. Best of luck :)
