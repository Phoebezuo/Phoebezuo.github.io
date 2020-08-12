---
layout:     post
title:      HTML and CSS Study Notes
date:       2020-08-12
summary:    Study notes about web skeletons and skins
categories: Web HTML CSS
---

# Components of the Web

The World Wide Web (WWW) is a collection of HTML documents. The links between web pages are called **hyperlinks** (links) and allows you to navigate the web.

1. **HTTP:** the protocol of the web that allows browsers to communicate with servers
2. **Servers:** computers that host the files (usually webpages) that make up the web
3. **Internet:** the world’s largest computer network
4. **Browser:** a program that runs on your computer to display files found on the web

# History of HTML and web browsers

In 2004, the W3C was developing XHTML2, which was to replace XHTML1 and HTML4 as the primary mark-up language for the web. Frustrated with this direction, the WHATWG started its own specification, Web Applications 1.0. The W3C finally adopted the WHATWG specification in 2007 and renamed it HTML5.

The actual specifications and what’s actually in it, continues to be the most confusing aspect of HTML5. There is so much conflicting information out there that it is hard to differentiate what is part of HTML5, and what is not. HTML5’s primary focus was on facilitating the development of applications. This includes making it easier for designers to make web and mobile applications, serve videos and add interactive content.

It is important to learn the basic principles and syntax of HTML before you use an HTML Web Authoring Tool like Dreamweaver. This unit will provide you with the knowledge and capabilities to develop more advanced websites, as well as to be able to properly understand its inner workings. You do not need to learn the entire language in detail, but you do need to understand the basic concepts of mark-up languages such as HTML.

# What is HTML5?

*HTML5* is latest revision of the *HTML* (Hyper Text Mark-up Language) used to create richer and more semantic documents on the World Wide Web.

- *HTML* is the language of your browser that makes it possible to present information on the Internet
- The purpose of the browser is thus to read *HTML* code and interpret them into visible pages
- The primary purpose of *HTML* is to control the content and structure of a webpage
- *HTML* is not a programming language, it is a mark-up language. Mark-up is semantically categorising text in a document. You mark-up text the same way you do in Microsoft Word with: headings; bullets; and emphasised text.

HTML is made up of:

- Text content, which is what you see
- Mark-up, which is what that content looks like or how it is arranged
- References to other documents e.g. images and videos
- Links to other pages

Unlike previous versions of *HTML*, *HTML5* has the ability to retain backwards compatibility with previous versions of HTML. This means that implementing *HTML5* will not cause older pages to fail.

HTML has nothing to do with fancy presentation and layout of a page. Thus, at this point, you should not even be thinking about what and how your page should look like. Rather, you should be concentrating on your content and grouping content thematically together.

- The browser does not display HTML tags, but uses tags (or mark-up) to interpret the content of the page.
- The **.htm** or **.html** files created are called source files, and the code that it contains is called source code.

### Mark-up / Tag Guidelines

- **HTML** files contain a set of tags e.g. ***<head></head>***, ***<title></title>***, ***<em></em>***
- Tags are **case insensitive**, but the convention is to write them in lowercase
- All HTML tags are enclosed in angled brackets: ‘<’ and ‘>’
- Tag elements often come in **pairs**. That is, you have a beginning tag and an ending tag e.g. ***<html></html>***. Beginning tags mark the start of a tag element and closing tags mark the end of a tag element i.e. a paragraph starts here (<p>) and ends here (</p>)
- Some tags do not need to be closed as browses are smart; it is obvious to the browser that once a new tag starts, the unclosed tag must have ended. After all, certain tags cannot be nested inside other tags. E.g. <p>, <html> and <body>

### About the Tags

- ***DOCTYPE*** declares the type of document you are writing. If this tag is missing, the browser will try to guess the type. Including the ***DOCTYPE*** is good practice for backward compatibility with older browsers. ***DOCTYPE html*** indicates the document is type ***HTML5***
- ***<html>*** tells the browser this is the start of an HTML document and ***</html>*** tells the browser this is the end of the HTML document
- ***<head>*** represents an area for heading information e.g. title and meta information (data about data). Heading information is not displayed in the browser window except the title.
- ***<title>*** contains the title of your document. The title is displayed in the browser's caption:
- ***<body>*** contains text that will be displayed in the browser
- **<*h1>***, ***<h2>***, **<h3>** represent headings. ***<h1>*** is the largest heading and ***<h6>*** is the smallest heading
- ***<ol>*** defines an ordered (numbered) list. Inside the ***<ol>*** tag, you need to mark the individual list item element by using the ***<li>*** tag (list items)
- ***<ul>*** is similar to ***<ol>*** except it defines an unordered list. This means individual ***<li>*** tags will define bulleted list items
- ***<p>*** is a paragraph tag with an automatic line break afterwards
- ***<em>*** defines text to be emphasised (the browser default displays this tag with an italic effect)
- ***<strong>*** mark-up important text (the browser default displays this tag with a bold effect)
- Notice we can also have a nesting of tags to define an emphasised and important text. This is common in HTML: ***<strong><em>* ...*</strong></em>***

# HTML Attributes

You can specify more options to your mark-up by defining attributes to your tags. We still have our opening and closing tag as before, but now we also have this new thing called an attribute. Attributes have a name and a corresponding value (inside double quotes).

```html
SYNTAX: <tag attribute="value">content</tag>
```

### **IDs and Classes**

The attributes that apply to all mark-up are the id and class attributes. IDs are unique names which identify a *single* element e.g. <h1 id=**"motto"**>. Classes are unique names which identify a *group* of elements e.g. <p class=**"welcome"**>, <h1 class=**"welcome"**>. Tags may have multiple attributes. <ol id=**"wishList"** class=**"alpha"**>

IDs and classes should add meaning to your code. They should help you quickly gather the overall content from a distant glance. You should not assign IDs and classes based on how you want them to look like (e.g. red, leftSide), but by semantics.

# Creating Hyperlinks

An example of a tag with additional attributes is the anchor tag **<a>** (or hyperlinks). Hyperlinks allow webpages to connect to each other. Hyperlinks can link to: pages outside the current website; pages within the current website; and links to other anchors on the current webpage.

```html
SYNTAX: <a href="URL">Hyperlink Text</a>
```

- <a> tells you where the link should begin and </a> indicates where the link ends
- Any text between these two tags act as the hyperlink text
- The attribute href defines the path of where the hyperlink will link to

### Link to Another Document

```html
<a href="http://www.google.com">Click here to go to Google</a>
<a href="firstpage.htm">Click to open a file in the current directory</a>
```

### Bookmark Inside a Document

The **id** attribute can also specify the name of an **anchor**, used to create a **bookmark** inside an HTML document. **Bookmark IDs** (just like IDs and class attributes in general) are not displayed in the browser. To link to this bookmark, use the **href** attribute and specify the ID of the bookmark as the corresponding value, preceded with a **#** symbol.

```html
<a id="topAnchor">top</a>
<a href="#topAnchor">Click to scroll back to the top</a>
```

# Referencing Images

Images are not technically *inserted* into a webpage, rather images are *linked* to webpages. We use the image tag ***<img>*** to create a holding space for the image.

```html
SYNTAX: <img src="URL" alt="TEXT" />
```

- The ***<img>*** tag has a src (source) attribute whose value is the path of the image location to be downloaded
- It is good practice to include an alt (alternate) attribute whose value is the text to be displayed if the user for some reason cannot view the image. If the image is moved or the requested URL is missing, this is the fall back text that is displayed. The text associated with the alt attribute is also the text picked up by search engines, crawlers and reading software used by blind people (screen readers) to access the web.

When you load a webpage, the browser gets the image from the web server and inserts it into the page for you. This is different from using MS Word. In MS Word, when you insert an image into Word, the image becomes a ‘part’ of the document. When you save a Word file, all you need to keep track of is that one Word file, knowing that the images you inserted will be there when you open it next time no matter where you move the Word file. With an HTML page, since you are only *referencing* the images, you have to make sure the image you are linking to always stay in the same spot in relation to the webpage.

- <img> tags are examples of tags with no content inside them (void tags). Thus, the tag can be simplified: <img />
- In the example, "computer.gif", means that the browser will look for the image named "computer.gif" **in the same folder (or directory) as the HTML document itself**
- This image path is an example of a partial *(relative)* You can also specify the full *(absolute)* path to the URL e.g. src=**"home/Users/{yourUserName}/Downloads/Files/computer.gif"**

![1.png](https://i.loli.net/2020/08/12/R2YcIBpVWlEu75v.png)

# Referencing Multimedia

The new mostly used media element in HTML5 is digital audio, which uses the ***<audio>*** tag. This tag is not included in the previous version of HTML. The ***<src>*** tag references a digital audio asset file name, and the ***<controls>*** tag adds the audio transport user interface feature. The following table shows the ***<audio>*** tag parameters supported in HTML5:

[Untitled](https://www.notion.so/5fcf6bf05d4743099f1759cf49e80702)

The last two parameters are not recommended for use unless absolutely necessary. The reason for this is that the autoplay bothers many users, and an autobuffer takes up system resources that may not even be used if the user chooses not to hit the transport play button.

When referencing multimedia elements, the source elements are referenced using their own source tags. There can be more than one source tag. This source tag provides a fallback mechanism if the browser does not support the first specified format.

```html
<audio controls>
		<source src="happybirthday/happybirthday.ogg" type="audio/ogg" />
		<source src="happybirthday/happybirthday.mp3" type="audio/mp3" />
		<source src="happybirthday/happybirthday.acc" type="audio/acc" />
		Your browser does not support the audio element.
</audio>
```

### Explanation

- The presence of any ***<audio>*** attributes has an implicit "true" value so you do not need to type: <audio controls=**"true"**>. Similarly, the absence of any attributes indicates an implicit "false". For example, the inclusion (true scenario) of the controls attribute tells the browser to display default audio controls such as play, pause, and volume. If this attribute is excluded (false scenario), no controls will be displayed.
- This ***true/false*** attribute can similarly be applied for other audio attributes e.g. autoplay.
- The ***<audio>*** element allows multiple ***<source>*** elements (or audio file paths) in case the browser does not support the first specified format.
- The browser will try to use the first recognised format. If this does not work, it will try the second format under ***<source>***. If this still doesn’t work, it will try the third format in the list and so on until finally it will display the alternative error text message.
- Fallback error text can be written anywhere, as long as it is between audio tags.
- Browser does not load each file and see if it works. Rather, it looks at the type attribute and compare it to its own browser specification to see if it supports the specified codec.
- The controls look different in different browsers.
- Only MP3, WAV, and Ogg audio are supported by the ***HTML5*** standard.

### Referencing Video

Videos can be referenced similar to audio elements using ***<video>*** tag. The following table presents the ten parameters for ***<video>*** tag. The last four parameters in the table are less frequently utilized.

[Untitled](https://www.notion.so/2c3fd6fd80754c43a64ebb121fa74317)

```html
<video controls poster="card/poster.jpg">
		<source src="card/card.ogg" type="video/ogg" />
		<source src="card/card.mp4" type="video/mp4" />
		<source src="card/card.webm" type="video/webm" />
		Your browser does not support the video element.
</video>
```

### Explanation

- The poster attribute specifies an image to be displayed when the video is first loaded. It is a good idea to always do this because the default black screen is not always a good representation of your video.
- Notice how similar the attributes and syntax are compared to audios.
- Only MP4, WebM, and Ogg video are supported by the HTML5 standard.

### Example using  HTML to change style

```html
<!-- Change the background colour of the page to blue -->
<body style="background-color:blue;">

<!-- Change size of picture to a height of 150 pixels -->
<a href="http://www.it.usyd.edu.au"><img src="coffee.jpg" alt="Coffee" height="150"></a>
```

# HTML Text Formatting in Details

When you created your first HTML page you have noticed you can format your texts in different format. Here there are some more details about text formatting in HTML.

## Lists

There are three types of lists available in HTML.

Ordered List: ***<ol>*** defines an ordered (numbered) list. Inside the ***<ol>*** tag, you need to mark the individual list item element by using the ***<li>*** tag (list items)

![3.png](https://i.loli.net/2020/08/12/HPC5bXUSYNQWn1l.png)

```html
<ol>
		<li>Tea
				<ul><li>The most refreshing drink.</li></ul>
		</li>

		<li>Coffee
				<ul><li>Want to have when you are sleepy.</li></ul>
		</li>

		<li>Water
				<ul><li>Life saver!</li></ul>
		</li>
</ol>
```

Unordered List: ***<ul>*** is similar to ***<ol>*** except it defines an unordered list. This means individual ***<li>*** tags will define bulleted list items

![2.png](https://i.loli.net/2020/08/12/e2nEYkw78yaKqXp.png)

```html
<ul>
		<li>Tea
				<ul><li>The most refreshing drink.</li></ul>
		</li>

		<li>Coffee
				<ul><li>Want to have when you are sleepy.</li></ul>
		</li>

		<li>Water
				<ul><li>Life saver!</li></ul>
		</li>
</ul>
```

Description List: ***<dl>*** defines a description list. The idea behind the description list is to set up a set of items and their related descriptions. ***<dt>*** wrapped up in ***<dl>*** defines description term, and each description is wrapped in a ***<dd>** which is* description definition element.

![4.png](https://i.loli.net/2020/08/12/KIrtG68bOuqEnJw.png)

```html
<dl>
		<dt>Tea</dt>
		<dd>The most refreshing drink.</dd>

		<dt>Coffee</dt>
		<dd>Want to have when you are sleepy.</dd>
		
		<dt>Water</dt>
		<dd>Life saver!</dd>
</dl>
```

## Quotations

HTML has the options to mark up quotations as block and inline quotation. Block quotations are intended for a long block of quotations. On the other hand, the inline quotation is intended for short quotations which do do not need any paragraph break.

```html
<blockquote>This is a blockquote</blockquote>
<q>This is an inline quotation.</q>
```

## Other Text Formatting

- Abbreviations: <abbr> - is used to wrap around an abbreviation or acronym.
- <address> - wraps around any contact details.
- <sup></sup>and <sub></sub>: To format texts and numbers as superscript and subscript.
- <code>: For marking up generic pieces of computer code.
- <pre></pre>: For retaining whitespace (generally code blocks)
- <var>: For specifically marking up variable names.
- <kbd>: For marking up keyboard (and other types of) input entered into the computer.
- <samp>: For marking up the output of a computer program.
- <time>: For marking up times and dates in a machine-readable format.

### Example to jump to bottom

```html
<p><a href="#bottom">Click here</a> to go to the bottom of the page</p>

<!-- INSERT A LARGE AMOUNT OF TEXT HERE -->

<p>This is the bottom of the page.</p>
<h2><a id="bottom">The bottom of the page</a></h2>
```

# Structural Semantics

In HTML, there are structural elements that define the structure of a webpage document, written inside the body tag. Below are two of the many visualisations. How you intend to structure your page may of course, differ from this structure.

![5.png](https://i.loli.net/2020/08/12/18SDOCdB2VFY9mA.png)

### **<header>**

The header tag is for introductory information about a section or an entire webpage. This can include a logo and/or a slogan that sits atop most pages, or a headline introducing a section.

### **<nav>**

The nav element represents a section with the *major* links to other pages within a website or to parts within the page (primary navigation).

### **<section>**

section is a generic grouping of related content. That is, a grouping of content that relate to the same information, thematically.

### **<article>**

The article element wraps a section of content that forms an *independent* part of a document or site e.g. a magazine, newspaper article, or blog entry. If certain content can be or will be syndicated or republished, it should reside in the article tag, as opposed to the section tag.

### **<aside>**

The aside element represents a portion of a page which can stand alone e.g. sidebars, related posts, tag clouds, pull quotes or annotations.

### **<footer>**

footer mark up the foot of, not only the current page, but each section contained in the page.

Remember, HTML is about content. This means just because you grouped content under aside does not mean it will appear as a right hand sidebar when you load the page. Making it appear on the right hand side is about style, which is not HTML’s responsibility. The purpose of structural tags is to ensure semantic content. This aids in communication with search engines and screen readers so that they can easily understand your content for the purposes of ranking pages and translating them to useful things, especially for the visually impaired.

### **div Tag Detour**

- The div (division) tag is a generic block level element
- All it really does for us is allow us to group elements together for easy reading and formatting at a block-by-block basis
- It is up to us authors to add any meaning to it at all. This is achieved through the use of meaningful and descriptive class and id attributes

### Notice the differences between these mark-ups:

<section> -> *groups **related** content together*

<article> -> *wraps **independent** content that can be **syndicated***

<div> -> *groups **any** elements together for **styling** purposes*

```html
<!DOCTYPE html>
<html>
   <head>
       <title>Title of document goes here</title>
   </head>

   <body>
       Visible text goes here...
   </body>
</html>

Basic Tags
<h1>Largest Heading</h1>
<h2> . . . </h2>
<h3> . . . </h3>
<h4> . . . </h4>
<h5> . . . </h5>
<h6>Smallest Heading</h6>
<p id="IDname" class="className">This is a paragraph</p>

<em>Emphasised Text</em>
<strong>Important Text</strong>
<a href="http://www.example.com">Link goes here</a>

<!-- Unordered List -->
<ul>
   <li>Item</li>
   <li>Item</li>
</ul>

<!-- Ordered List -->
<ol>
   <li>Item</li>
   <li>Item</li>
</ol>

<!-- Description List --> 
<dl>
	 <dt>Item</dt>
	 <dd>Description</dd>
</dl>

<!-- Images -->
<img src="URL" alt="Alternate Text" />
 
<!-- Audio -->
<audio>
   <source src="URL" type="audio/mp3" />
   <!—More source elements -->
   Fallback text
</audio>

<!-- Video -->
<video>
   <source src="URL" type="video/mp4" />
   <!—More source elements -->
   Fallback text
</ video >

<!-- Semantics -->
<article>Groups independent elements</article>
<aside>Standalone element</aside>
<footer>Foot information</footer>
<header>Introductory information</header>
<nav>Primary navigation</nav>
<section>Grouping of related elements</section>
<div>Group block elements </div>
```

# CSS What is it?

In short, CSS is putting some skin onto your web skeleton (HTML) for styling purposes.

An important element of web design and usability is to design a website with a consistent look and feel. A quick way to achieve this is through the use of Cascading Style Sheets (CSS). **CSS allows you to control the style and layout** of your website all at once. You can define a style for each HTML element and apply it to as many web pages as you want. To make a global change, simply change the stylesheet file, and all elements in the web are updated automatically.

CSS is a style sheet language that controls the presentation of mark-up language documents. Visually, think of HTML as a structure of a new building; you can see the structure as it is being built, but you do not really know what the building is going to look like. CSS on the other hand, serves as the skin of the building and determines what the outside of the building can look like. By separating structure and presentation in this way, you can change how things look by changing the CSS files or by changing the underlying HTML structure

- **HTML**: controls content and structure of the webpage (content)
- **CSS**: controls the style and layout of the webpage (presentation)

CSS is not a mark-up language, but a style sheet language. This means that CSS consists of a collection of formatting rules that identify the elements you want to control and the properties you wish to set.

# CSS Syntax

```css
selector {
   property: value;
}
```

A **style** is a definition for a particular look and feel, i.e. fonts, colours, sizes, etc. A **style** is made up of three parts: a **selector**; **properties/attribute**; and corresponding **values**

- The selector selects the elements you want to style
- The property and value are linked by a colon
- Each property and value pair is separated by a semi-colon

Curly braces are used to enclose all properties and values. You can have one or more properties/value definitions inside the selector

# CSS Selector

### Type Selectors

Used to style the look of existing HTML tags

```css
/* all h1, h2 and h3 tags will have an Arial font of size 40px */
h1, h2, h3 {
		font-family: Arial;
		font-size: 40px;
}

div {
	  background: rgba(0, 128, 0, 0.3) /* Green background with 30% opacity */
}

div {
		background-color: green;
	  opacity: 0.3;
}
```

### Universal Selectors

Used to style any single element of any type (basically, it selects all elements). To use this selector, define an asterisk, " * "

```css
/* all HTML tags will have a blue font colour */
* {
   color: blue;
}
```

### Class Selectors

Used to style a group of elements defined by the same class. To use this selector, define a dot, "." followed by the class attribute e.g. .centre

```css
/* any paragraphs with a class "quote" will have a grey background colour and a bold effect */
p.quote {
   background-color: #BBB;
   font-weight: bold;
}
```

### ID Selectors

Used to style a single, unique element identified by their ID. To use this selector, define a hash, "#" followed by the ID (similar to the hyperlink bookmark)

```css
/* tags that have an id "mainContent" will have a purple colour and centred text */
#mainContent {
   color: rgb(100, 50, 200);
   text-align: center;
}
```

### Attribute Selectors

Used to style an element using the presence of a given attribute or attribute value. To use this selector, specify a pair of square brackets. Within the square brackets, identify an attribute, followed by an equals sign, followed by a value in quotation marks.

```css
/* any hyperlinks with a href attribute will be set to uppercase and italicised */
a[href]{
   text-transform: uppercase;
   font-style: italic;
}

/* all images with an alternate equalling "computer" will have a 200px width and 150px height */
img[alt = "computer"]{
   width: 200px;
   height: 150px;
}
```

### Pseudo-Class Selectors

Used to style certain elements, but characterised by special states. To use this selector, define a colon, " : ", followed by the pseudo-class name. **Do not leave a space between the selector and the state, otherwise the style will not be applied.**

```css
/* when a hyperlink is moused over, the font will transition to an underline and small capitalisation state */
a:hover {
   font-variant: small-caps;
   text-decoration: underline;
}

/* use text-decoration: none; to remove underline */
```

All HTML elements can have a hover state. The anchor tag however, has further special states:

:**link** to style links to unvisited pages,

:**visited** to style links to visited pages,

:**active** to style the active link.

[CSS Selectors](https://www.notion.so/488f430fdf1c432e8220cbb079ab0b2d)

## Rendering Engines

Each browser has their own rendering engines that parse your code and determine how to display everything. That's why browsers render pages differently – rendering engines. Every browser has its own rendering engine that it uses to parse (or analyse) your code and determines how it is supposed to display. Since most browsers are developed independently of each other, there are multiple rendering engines. Each one has slightly different parsers, preferences and policies that determine how your content is rendered. As a designer, take note of the rendering engines for the more common browsers:

These rendering engines are still being developed and older versions of these browsers will have older rendering engines. For this reason, designers should test their webpage not only in multiple browsers, but also in different versions.

# CSS Reset and Normalize

If any CSS styles are not declared, then they either have a zero value or take the browser default value (typically not zero). During testing, if you notice that your webpage does not display exactly the same in different browsers, it is most likely that the browser default CSS properties are being applied.

To avoid cross-browser style inconsistency, you must reset any browser default.

Eric Meyer has created a CSS Reset file to remove all browser defaults so you do not have to do it every time you create a webpage. Make sure to include this in all your HTML files as an external link before applying your own styles (you will learn how to do this later).

- Why is normalize.css useful?
    - aligns some base styles
    - provides better cross-browser consistency in the default styling of HTML elements
    - preserves useful defaults

# CSS Making/Linking

There are three ways to apply CSS to your HTML page:

- **External style sheets:** used when the same style is applied to many pages
- **Internal style sheets:** used when a single document has additional unique elements that need styling
- **Inline style sheets:** mixes content with presentation. Use sparingly!

**We recommend that you use external style sheets wherever possible to adhere to good coding style and HTML5 standards.** Thus, little time will be spent on internal and inline styles.

In your HTML file, you need to link your CSS file with the following line in between the head tags

```css
<link rel="stylesheet" href="URL">
```

- The <link> tag allows the page to link to the external style sheet
- rel specifies the relationship between the current document and the linked document. In this case, the relationship is a **"stylesheet"**
- href refers to the path of the external style sheet

Remember, to remove browser defaults to ensure browser consistency for webpages look. To ensure that you need to reference a reset.css file to all your HTML documents. Make sure to include the reset.css file before all the other CSS files you plan to use since styles are rendered in the order they are linked. This means that the last specified CSS file will override any styles you specified at the beginning.

# CSS Cascading Order

The term cascade refers to how styles are applied to pages. Styles are applied to pages in the order they are found.

If more than one style is specified for an HTML element, the browser will select which styles to apply by following the Cascading Order. Generally, all styles “cascade” into a virtual style sheet by following the order (from lowest to highest priority):

1. Browser default
2. External style sheet
3. Internal style sheet (in the head section)
4. Inline style (inside an HTML element)

**Or more simply, the last rule wins.**

This means that if you applied the same property-value twice, the last specified will take priority.

# CSS Typography Font

Typography is the design and use of typefaces and fonts, including their proportions and spacing. Typography is about the space, the style and the text display. There are two main groups of CSS properties that control typography styles: font and text.

The font CSS property group dictates general font characteristics such as font-style and font-weight. The text CSS property group deals with the characters, spaces, words and paragraphs. For example, the text-indent property indents the first line of a text block. The letter-spacing property controls the spaces between a text block.

[Font](https://www.notion.so/86e58b5ff27a430ebc51d0910d311d29)

### Web Fonts

Web fonts refer to the technique of having the browser download and install fonts that are requested in the page using the @font-face syntax. This allows web authors to apply any font without worrying about if they are installed on the client's machine or not.

```css
/* Referencing the font */
@font-face {
   font-family: myFirstFont;
   src: url('Sansation_Light.ttf');
   src: url('Sansation_Light.eot);
}

/* Using the font */
a {
   font-family: myFirstFont;
}
```

Essentially, you make a font-face rule by giving the font a name for the font-family property. Next, include a font file somewhere on your server and refer to it (via the src attribute). Font files can have multiple fallback src files if the first format is not supported by the browser.

To then use the referenced font, the font-family attribute can be applied to a CSS selector.

[CSS Typography Text](https://www.notion.so/fb43727709944c118edcc5764f20d88d)

# CSS Box Model

In **CSS**, every **HTML** element is made up of nested boxes: **margin**, **border**, **padding**, and **content.** This is termed the box model, where every single HTML element is considered a rectangular box. This allows us to place a border around elements and space elements in relation to other elements.

![7.png](https://i.loli.net/2020/08/12/zNeVaxEr2TDIw5l.png)

- **Margin:** defines the whitespace with respect to 'surrounding' elements. Margins are transparent and thus, will not obstruct elements behind it.
- **Border:** outlines the visible portion of the element.
- **Padding:** defines the whitespace between the border and content. Padding is transparent. The easiest way to think of this is to think of a box with something fragile inside it that you need to ship. You, therefore, need to add some padding material inside the box to keep the product from touching the box. That is padding.
- **Content:** where all your text and images appear.

Note that there is a difference between the content width and the total width of the element:

![6.png](https://i.loli.net/2020/08/12/paHX16ntmjNOI2T.png)

This means when you assign a width to a tag element, this is just the content width. Further, you actually add to the overall width of the tag by setting a margin, border or padding width.

- ***The total width of an element is calculated as**:*
    - Total element width = width + left padding + right padding + left border + right border + left margin + right margin
- ***The total height of an element is calculated as:***
    - Total element height = height + top padding + bottom padding + top border + bottom border + top margin + bottom margin

# CSS Box Model Padding

## Syntax

**Margin**, **border** and **padding** have similar syntax in terms of whitespace. You can either manipulate its individual CSS properties, or use the shorthand notation. In the following, we will use padding as an example, but remember that this can equally be applied to margin and border.

## Individual Properties

padding-top, padding-right, padding-bottom, padding-left, specified in pixels or percentages

[Shorthand Notation](https://www.notion.so/79628ac462e2464fadd0d6c2b9412b6f)

# CSS Box Model Margin Considerations

## Margin Considerations

There is one aspect of margins that tends to trip up designers. **Unlike horizontal elements, vertical elements collapse.** That means if you have two elements loaded on top of the other, only one of the margin element will be applied. 

For example, consider a **heading1** with a **10px bottom margin**, and a paragraph with a **10px top margin**. In this case, there will only be a margin of 10px worth of space between them, not 20px. If the values are not the same, the higher value will be applied.

![8.png](https://i.loli.net/2020/08/12/U9gXNBhmTpil8kO.png)

![21.png](https://i.loli.net/2020/08/12/qw7NdfIjWcs4hxP.png)

# CSS Box Model Border

![9.png](https://i.loli.net/2020/08/12/tBSX4zr9F7JyPNx.png)

This top/right/bottom/left syntax can similarly be applied to the border’s color and weight property (e.g. border-left-weight, border-bottom-color). Putting these three attributes together, we have the shorthand notation to control these properties: border-weight, border-style, border-color. 

```css
border-top: 1px solid black;
border-style: dotted;
```

The important thing to remember about the border is that they do affect the overall width of an element. Border widths begin at the edge of padding width and extend outward. It is easy to forget about that typical 1px border on an element. This is often the culprit for breaking layout or causing elements to shift unexpectedly. Be sure to account for border widths when planning layout.

```css
/* Total width = 1px + 20px + 200px + 20px + 1px = 242 */
p {
	   padding: 20px;
	   border: 1px solid black;
	   width: 200px;
}
```

# CSS Box Model Centring a Block or Image

```css
/* cneter text */
p,h1, h2 {
		text-align: center;
}

/* center img */
img {
		display: block;
		margin-left: auto;
		margin-right: auto;
}
```

# CSS Box Model Centring a Document

To control your webpage so that the styles do not jerk into weird positions when you change browser widths, you need to fix the width of your webpages. To do this, you will need to add an automatic margin and a fixed width (recommended 1200px) to the body tag.

```css
body {
	   width: 1200px;
	   margin: 0 auto; /* set right and left to auto, element is centred */
}
```

This does not centre align all your text and images. It centres the page in the middle of a giant canvas (which is your browser window).

### The Alternative CSS Box Model

The **Alternative CSS Box model** is another option for Standard Box Model. It has been introduced to eradicate the inconvenience of adding up all the border and padding width to get the real size of the box. This model takes the width of the visible box on the page as width. As a result, the content area width is that width of the visible box minus the width for the padding and border.

```css
/* The browser takes the border box as the area defined by any size you set. */
.box { 
	  box-sizing: border-box; 
}
```

If you want all of your elements to use the alternative box model, and this is a common choice among developers, set the box-sizing property on the element, then set all other elements to inherit that value, as seen in the snippet below.

```css
html {
	  box-sizing: border-box;
}

*, *::before, *::after {
	  box-sizing: inherit;
}
```

### Example about box sizing

![10.png](https://i.loli.net/2020/08/12/eUnM4IBZ1ArlgcN.png)

```html
<section>
		<article class="box-standard">
				<header>
						<h2>header 1</h2>
				</header>

				<p>paragraph 1</p>
		</article>
		
		<article class="box-standard box-alternate">
				<header>
						<h2>header 2</h2>
				</header>

				<p>paragraph 2</p>
				<p>paragraph 3</p>
		</article>
</section>
```

```css
.firstpara {
			margin-top:10px;
}

.secondpara{
		padding:10px;
}

.thirdpara{
		padding:10px;
		border: 1px solid blue;
		width: 200px;
}

.box-standard {
		width: 300px;
		height: 160px;
		margin: 10px;
		padding: 15px;
		border: 1px solid blue;
}

.box-alternate {
		box-sizing: border-box;
}
```

### Example about border-box

![32.png](https://i.loli.net/2020/08/12/nDHCAOli5638f1X.png)

```css
p {
		padding: 5px;
		color: blue; 
		width: 200px;
		border: 1px solid blue;
}

.box { 
		box-sizing: border-box; 
}

<p class=box>Lorem ipsum dolor sit amet.Vestibulum pretium purus orci, eget malesuada nunc iaculis non. Nullam mollis feugiat risus, id egestas diam. </p>
```

### Example about padding and margin

All the padding and margin properties can have the following values:

- *length* - specifies a margin in px, pt, cm, etc.
- *%* - specifies a margin in % of the width of the containing element
- inherit - specifies that the margin should be inherited from the parent element

But margin properties can have `auto` property, which is the browser calculates the margin.

![35.png](https://i.loli.net/2020/08/12/Fp5hXUNMTvaic3e.png)

Notice that your div tag has moved down by an invisible white 10px top margin. These extra white coloured spaces are the margins. Note this whitespace difference between margin (whitespace in relation to surrounding elements) and padding (whitespace outside current elements).

```html
<div>
		<p>
			I'm a paragraph inside a div.
		</p>
</div>
<div>
		<p>
			I'm another paragraph inside a second div.
		</p>
</div>
```

```css
div {
		background-color: #9933FF;
		padding: 10px; /* purple background */
		margin: 10px; /* white space*/
		border: 1px solid green;
}

div {
	  padding: 25px 50px 75px; /* top is 25px, right and left are 50px, bottom is 75px */
}
```

![33.png](https://i.loli.net/2020/08/12/nphJBx6wEj1AMKa.png)

### Example on Padding

Here, the <div> element is given a width of 300px. However, the actual width of the <div> element will be 350px (300px + 25px of left padding + 25px of right padding):

```css
div {
	  width: 300px;
	  padding: 25px;
}
```

To keep the width at 300px, no matter the amount of padding, you can use the box-sizing property. This causes the element to maintain its width; if you increase the padding, the available content space will decrease.

```css
div {
	  width: 300px;
	  padding: 25px;
	  box-sizing: border-box;
}
```

# CSS Display

**The CSS *display*** property is an important property to control the webpage layout. Every *HTML* element has a default display value depending on what type of element it is. The default display value for most elements is ***block*** or ***inline***.

## Block-level Elements

A ***block-level*** element always starts **on a new line and takes up the full width available in the container**.

## Inline Elements

An ***inline*** element **does not start on a new line and only takes up as much width as necessary**. Examples of inline elements:

- <span>
- <a>
- <img>

## Display:flex

The flex option establishes the outer display type as block, but the inner display type is changed to flex. Flexbox is a one-dimensional layout method for laying out items in rows or columns. Items flex to fill additional space and shrink to fit into smaller spaces.

## Display: none;

*display: none;* is commonly used with *JavaScript* to hide and show elements without deleting and recreating them.

The *<script>* element uses *display: none;* as default.

## Override The Default Display Value

It is possible to override a default display value of any element. For example,

```css
p {
  display: inline;
}
```

### Difference between display: none and visibility: hidden

Hiding an element can be done by setting the *display* property to *none* and *visibility* property as hidden. However, the difference is the hidden property will only hide the element and will use the same space for the element as before.

### Example between display: none and visibility: hidden

![11.png](https://i.loli.net/2020/08/12/MZSbf19kKpieTsB.png)

```html
<h2>Display none</h2>
<p class="hidden-none">Testing Display none</p>
<p>Normal display</p>

<h2>Visibility Hidden</h2>
<p class="hidden-visibility">Testing visibility hidden</p>
<p>Normal display</p>
```

```css
.hidden-none {
		display: none;
}

.hidden-visibility {
		visibility: hidden;
}
```

### Example to see display: block

![12.png](https://i.loli.net/2020/08/12/oQvONDEKyqpYaS3.png)

```html
<h2>Changing Block to Inline and vice-versa</h2>
<p>I am a paragraph with <span class="block">wrapped</span> elements</p>
```

```css
.block {
		display: block;
		border: 1px solid red;
		padding: 2em;
}
```

### Example between inline and flex display

![13.png](https://i.loli.net/2020/08/12/bFJatxKcDljnBi7.png)

```html
<h2>An inline list</h2>
<ul>
    <li class="inline">Item 1</li>
    <li class="inline">Item 2</li>
    <li class="inline">Item 3</li>
</ul>

<h2>Testing flex display</h2>
<ul class="flex-display">
    <li>Item 1</li>
    <li>Item 2</li>
    <li>Item 3</li>
</ul>
```

```css
ul {
		border: 1px solid blue;
		padding: 2em;
}

li {
		border: 1px solid red;
		padding: 2em;
}

.flex-display {
		display: flex;
		list-style: none; /* no bullut point */
} 

.inline {
		display: inline;
}
```

### True or false

- Setting the visibility property to hidden will only hide the element and will use the same space for the element as before. (True)
- <img> is a block-level element. (True)
- The display:none and visibility:hidden hide the elements in exact same way. (False)
- The following style will make the paragraphs start on a new line. p { display: inline; } (False)
- A inline-level element always starts on a new line and takes up the full width available. (False)
- The <script> element uses display: none; as default. (True)
- An inline element does not start on a new line and only takes up as much width as necessary. (True)

# CSS Positions Schemes Intro

There are four common types of CSS positioning schemes:

- Normal flow
- Relative positioning
- Absolute positioning
- Fixed positioning

## Normal Flow

**position: static;**

Normal flow is when you do nothing on a page layout (default layout of your browser). It takes the content in the order it is found in the **HTML** and stacks it, one element after the other one element right on top of another other. **Block-level elements** (heading, paragraphs, sectional elements e.g. div, article, section) take their own space in the document flow and are stacked one on top of another.

**Inline elements** (e.g. img, a,) appear inside the block-level elements and they stack themselves based on the flow of line boxes. Think of how the lines of a paragraph are stacked; this is essentially the flow of inline elements. That is, they are stacked as wide as they can.

# CSS Position Schemes: Relative

Here, elements are still considered a part of normal document flow, but you can offset the element from its normal position using the top, right, bottom or left offset values.

![14.png](https://i.loli.net/2020/08/12/2tRP5Kh6bUeiJ3E.png)

```css
.box1 {
   position: relative;
   left: 100px;
   top: 50px;
}
```

Note that using this method creates a hole where the element would normally be found.

# CSS Position Schemes: Absolute

Here, elements are actually removed from normal document flow and repositioned based on top, right, bottom or left offset values. Elements are placed relative to the nearest positioned-attribute ancestor.

![15.png](https://i.loli.net/2020/08/12/plDBFXneZ6qRcCG.png)

```css
.box1 {
   position: absolute;
   left: 100px;
   top: 50px;
}
```

Any element below the absolute positioned element moves up in its place. Where they get tricky is where the element gets positioned. Essentially, an absolute positioned element looks to the nearest parent element that has a positioning property. If there are no elements positioned above it, it simply looks at the body tag, and thus offsets relative within the body tag.

Relying on the body tag does not always give the desired result. 

![16.png](https://i.loli.net/2020/08/12/6DdxjTEKROzHQ1U.png)

```css
.quote {
   position: absolute;
   left: 40px;
   top: 20px;
}

/* see the difference with and without this code */
.content {
   position: relative;
   left: 40px;
   top: 20px;
}
```

This is because your actual desired parent element (the content block) is not a positioned element, thus the quote block positions the quote with the body tag as the parent. To rectify this, you must qualify the content element as a positioned element. This is achieved by setting the containing block to have a position: relative property-value. 

- Trying to create layouts purely based on relative positioning will give you a lot to keep track of. That is, it would be very difficult to remember where everything was supposed to be normally so that you can offset it correctly. Even then, if you change one element, then the whole layout flexes and changes since everybody is responding to everything else. Thus, relative positioning is not going to be used to create entire layouts, rather, mainly to do two things:
    - provide slight tweaks to your layout when you need to offset an element in a specific direction (e.g. up a little bit, or left a little bit)
    - provide a positioning value for containing elements.
- When designing layouts, you thus need to consider what elements you are going to set as the containing block to contain the other positioned elements. That is, absolute position elements require a containing block (relative position statement). If you don't provide it one, it will use the outer block of the document (the body of your document).

# CSS Position Schemes: Fixed

If you want an element to always be present, no matter whether you resize or scroll through the page, you need to set the position property to fixed:

![17.png](https://i.loli.net/2020/08/12/hIvgdFBGfEHVoMA.png)

```css
.ad {
   position: fixed;
   left: 100px;
   top: 50px;
}
```

# CSS Stacking Context

Although we tend to regard a webpage as a two-dimensional entity, the box model is positioned in **three dimensions**. The third dimension is the **z-axis**, which is perpendicular to the screen and each box has an associated stack level. Positioned elements, after all, can overlap.

By default, positioned elements are stacked on top of each other based on where they are encountered in the source order, with the last object being on top. A box with a higher stack level is rendered "in front of" a box with a lower stack level. That is, it is rendered closer to a user. A stack level can also be negative. The stack level is specified via the z-index property.

![18.png](https://i.loli.net/2020/08/12/pfTZ9l7hUs1Sky2.png)

```css
header, aside {
   z-index: 1;
}
 

.content {
   z-index: 2;
}

 
.quote {
   z-index: 3;
}
```

Each stacking index does not need to be incremented by 1 or 1000 for each level. It’s just a number; the index needs only be larger or smaller than each respective index.

# CSS Positioning Float

How floats actually work changes based on the elements being floated. Essentially, it is an element that is shifted to the left or to the right of its current position, removed from the normal document flow. Remember that in the normal document flow, block-level elements stack on top of each other and can be referred to as boxes. If you apply the following code:

![19.png](https://i.loli.net/2020/08/12/JBuAjQRpoZeKUEG.png)

```css
.box1 {
   float: right;
}
```

If you actually floated box1 to the left, the surrounding elements will still move up because box1 is removed from the normal document flow.

![22.png](https://i.loli.net/2020/08/12/V3L9S7rx4JglKt2.png)

```css
.box1 {
   float: left;
}
```

### Inline Boxes

When you float the image to the left, what happens is the paragraph wraps around the image instead of going underneath it. Any inline element will wrap around floated elements if they have enough room.

![20.png](https://i.loli.net/2020/08/12/ab53fTGkivSExuN.png)

```css
img {
   float: left;
}
```

# CSS Positioning Clear

However, based on the way floats work, any remaining content on the page will move up and underneath the floated elements. By using the clear property, you can tell the browser to stop floating elements and go back to normal document flow

```css
footer {
   clear: both;
}
```

## 2 Column Layout

Your typical two-column layout can, therefore, be obtained by using floats:

```css
/* method 1 */
aside {
   float: left;
} 

.content {
   float: right;
}

/* method 2 */
aside {
   float: left;
   margin-right: 20px;
} 

.content {
   float: left;
}

/* method 3 */
#container {
   width: 960px;
   margin: 20px auto;
}
 
#content {
   float: left;
   width: 620px;
} 

#sidebar {
   float: left;
   width: 340px;
}
 
#footer {
   clear: both;
}
```

## 3 Column Layout

```css
#container {
   width: 960px;
   margin: 0 auto;
}
 
#leftSidebar {
   float: left;
   width: 240px;
}

#content {
   float: left;
   width: 480px;
}
 
#rightSidebar {
   float: left;
   width: 240px;
}

#footer {
   clear: both;
}
```

### Make nav horizontally or vertically

![23.png](https://i.loli.net/2020/08/12/E1gDzZGWFHOi85w.png)

![24.png](https://i.loli.net/2020/08/12/OIcKuJAbTVCyN2n.png)

```css
/* horizontally centered */
nav ul li {
		display: inline-block; /* horizontally */
		padding: 5px 0px; /* centered */
		margin: 0px 5px; /* centered */
}

/* vertically to left */
nav {
    float: left; /* vertically to left */
    height: 540px;
}
ul li {
    padding: 0px 10px 5px 5px;
		margin: 20px 10px; 
		text-align: left; /* align with nav */
}
```

# CSS Responsive Web Design Intro

## Background

Responsive web design is rapidly evolving idea, especially as websites need to adapt to the growing number of mobile devices and their relatively small screens. What we have dealt with so far involved multiple fixed width layouts, but of course, the dream is: one website for all sizes. If a website can respond to the user’s preference of device, this would eliminate the need for a different design and development phase for each new gadget on the market.

As designers, if you don't design for all the ways that people can consume or interact with your content, you are failing to address a significant amount of your audience. In terms of smart phones and tablets, those audiences are just too big to ignore anymore.

## Responsive Design in a Nutshell

The basic idea of responsive web design is that **a website’s design and development should "respond" to the user’s behaviour and environment**. This includes **screen size**, **platform**, **orientation** and **device**. These devices can include: desktops; tablets; mobiles; and television. Generally, this responsiveness can mean things like:

- Adapting layout to suit different screen sizes
- Resizing images to suit screen resolution
- Serving lower bandwidth images to mobile devices
- Simplifying or hiding elements for mobile devices
- Providing finger-friendly links and buttons for mobile users
- Detecting and responding to mobile features such as geolocation and device orientation

Essentially, responsive design practices consists of **flexible grids**, **layouts**, **images** and **intelligent use of CSS media queries**.

## Flexible Layouts

Flexible layouts are essentially any layouts that use relative measurements to allow the layout to resize under different conditions.

[Untitled](https://www.notion.so/1b98be90b4a24df782bf6eef3343a96c)

As you can see, in today’s multi-device world, the idea of developing sites that respond to medium makes a lot of sense. You cannot control how your audience comes to your site or make them use a browser of your choosing, and fixed at a specific width. The good thing is that there are only a handful of different ranges most people will fall into. Thus, you can create several designs, each to work well with one range of device, browser and resolution. Next, it is up to you to respond to users’ environment.

## HTML Structure

For best designs, you need to start thinking modular. That is, you need to think of the different parts of your design such as main content, sidebar, header and navigation, not as pieces that must stay in the same place relative to one another, but as modules that can be reorganised, resized and shuffled.

The crucial part is identifying groups of elements that must stay together for any layout. For example, navigation links must stay together otherwise they will make no sense. This will make it easier to adapt for different viewport (window) sizes. In the next three diagrams, we visualise the typical structure for desktops, tablets, and mobile devices respectively.

![25.png](https://i.loli.net/2020/08/12/wX9aUjnuiNdTSm1.png)

# Viewport

The viewport is the user's visible area of a web page. It varies with the device, and will be smaller on a mobile phone than on a computer screen.

You can set the viewport as follows:

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1" />
```

- A *<meta>* viewport element gives the browser instructions on how to control the page's dimensions and scaling.
- The *width=device-width* part sets the width of the page to follow the screen-width of the device (which will vary depending on the device).
- The *initial-scale=1.0* part sets the initial zoom level when the page is first loaded by the browser. Simply it disables the initial scale, thus ensuring that when the page is first displayed, it is fully zoomed in.
- *maximum-scale = 1* ensures that there is always a 1:1 ratio between the page’s CSS pixel and the device’s screen pixels. This is important when a device switches to landscape orientation and you want the width to increase accordingly.

# Media Types

Media types allow you to specify how documents will be presented in different media. This includes documents displayed on screens, or on paper.

[Untitled](https://www.notion.so/52cf1979979147b792f62c2180a4fde2)

### @media Rule

The @media rule allows different style rules for different media in the same style sheet. An example usage:

```css
@media screen {
   div #mainContent {
       font-family: verdana;
       font-size: 14px;
	 }
}

@media screen, print {
   div #mainContent {
       font-weight: bold;
	 }
}
```

Alternatively, media types can be specified within the link tag

```html
<link rel="stylesheet" media="screen" href="style320.css"/>
```

# Media Queries

CSS media queries are the key trick for responsive design. The purpose of media queries is to apply different CSS rules to achieve different layouts for a specified viewport (window) width. It is essentially a block of ***if*** conditions to tell the browser how to render the page for a specified viewport width. Example of a media query syntax:

```css
@media media-type and (media-feature-rule) {
	  /* CSS rules go here */
}
```

- A **media type**, which tells the browser what kind of media this code is for (e.g. print, or screen). Media types are optional; if you do not indicate a media type in your media query then the media query will default to being for all media types.
- A **media expression**, which is a rule, or test that must be passed for the contained CSS to be applied.
- A **set of CSS rules** that will be applied if the test passes and the media type is correct.

### Ways to Insert Media Queries

Just like CSS, there are three ways to implement media queries (and thus media types)

### **@import rule**

Within the main CSS style sheet, reference the other style sheets using the import rule:

```css
@import url(style600min.css) screen and (min-width: 600px);
```

Note: Chaining media queries (eg. using min-width). More chaining is possible.

### Media Queries in Style Sheets

Media queries can also be placed directly into style sheets:

```css
#nav {
   float: right;
}

#nav ul {
   list-style: none;
}

@media screen and (min-width: 480px) and (orientation: portrait) {
   #nav li {
       float: right;
       margin: 0 0 0 .5em;
       border:1px solid #000000;
   }
}

@media screen and (min-width: 768px) {
   #nav {
       width: 200px;
   }

   #nav li {
       float: left;
       margin: 0 0 0 .5em;
       border: none;
   }
}
```

### Linked Style Sheet

Media queries can also be included in a linked style sheet’s media attribute:

```html
<link rel="stylesheet" media="screen and (max-device-width: 800px)" href="style768.css"/>
```

[Media Feature Rules](https://www.notion.so/c33d26fddc5f4cc4892c3b5fccb75fe9)

All the above queries, except for orientation, accept a min/max prefix. This will set a maximum/ minimum browser/device width that a certain set of styles would apply to.

The set of pixel widths that this course recommends you target are as follow. Of course, they should only serve as a starting point. Generally, catering for three different range of widths is sufficient

- 320px
- 480px
- 600px
- 768px
- 900px
- 1200px

### Which to Use

Imported style sheets have the advantage of being conditionally downloaded according to media attribute. The disadvantage is the lack of browser/device support relative to the other options.

If organisational benefits outweigh the efficiency lost, linking separate style sheets should be used. This is also suitable for devices that do not switch orientation or for screens whose browser width cannot be changed manually.

If you are dealing with devices that can switch orientation, placing media queries all in the **one** style sheet may be best. Because devices can switch orientation instantly, if two media queries were placed in separate style sheets, the website would have to call each style sheet file every time the user switched orientations. Placing it all in the one style sheet would be more efficient. Further, if the design is meant for a standard computer screen with a resizable browser, placing all media queries in one style sheet would be best.

In this course, we recommend you to use media queries in your style sheets.

### Problems with Media Queries

There are two main problems with CSS media queries.

1. If you use only media queries, the browser will still download the scripts associated with the application, even if your element is hidden
2. Even though images may be hidden from low resolution devices, the browser still downloads the full-source variants

### Solving the CSS Issue

To remedy the two main problems of CSS media queries, JavaScript is needed to read out the media queries and from there, decide whether to download the complicated mapping script, and whether to download the low-source or full-source image (or even no image at all). To fire JavaScript when a media query is triggered:

```jsx
if (screen.width > 600) {
      // download complicated script
      // swap in full-source images for low-source ones
}    
// OR
if (document.documentElement.clientWidth < 900) {
      // scripts
}
```

### Media Query Browser Support

Of course, not all devices support all of the CSS3 media query options. For this reason, you have been provided with a **respond.js** file to act as a back-up for older browsers, in particular, IE8 and below. The good thing about this script is that it can be compressed down to as little as 1 KB and can parse CSS files fairly fast without needing any additional libraries.

However, **respond.js** was never meant to be a full-featured solution. Its purpose is to provide the bare minimum for responsive layouts to work. It supports only min-width and max-width queries. **css3-mediaqueries.js** provdies more complex queries.

# Flexible Grids

The meaning of a flexible grid is to add a breakpoint in the style to change the design at the point where it requires. As a result you don't need to target every possible device size and design layout for it.

In the early days of responsive design the only available option was using float. The basic idea is to transform pixel-based absolute widths to percentage-based relative measurements. The general rule to apply is: 

```html
Target/Context=Result (The rule is first proposed by Marcotte)
```

![26.png](https://i.loli.net/2020/08/12/yIijxN4sYv5uVKJ.png)

For example if our target column size is 300 pixels, and the context (or container) it is in is 960 pixels, we divide 300 by 960 to get a value we can use in our CSS, after moving the decimal point two places to the right.

### Example on 2 Column Layout Response Design

![27.png](https://i.loli.net/2020/08/12/hwprf45eWgtNcMu.png)

```html
<section class=col1>
    <article>
        <header>
		        <h2>Explore Our World Your Way</h2>
        </header>
        <p>Explore Australia is the best way to explore our wonderful country! Come find out why our tours are so good!</p>
    </article>
    <article>
        <header>
            <h2>Must See Attractions</h2>
        </header>
        <p>No matter which state you're in, Australia is filled with cultural must-see attractions from the Opera House to Uluru.</p>
    </article>
</section>

<aside class=col2>
    <h2>NSW Climb</h2>
    <p>See the City from above in a mind-blowing Harbour Bridge Climb</p>
</aside>
```

```css
/* only width > 600px, using following css rules */
@media screen and (min-width: 600px) {
    .col1 {
        width: 31.24999999%;
        float: left;
    }
    .col2 {
        width: 64.58333331%;
        float: right;
    }
}
```

# CSS Responsive Web Design Modern layout technologies

There are other modern technologies that are responsive by default. These methods are Mutilple-column layout, Flexbox, and Grid.

### Multiple-column Layout

You can use **column-count** and **column-width** attributes to make your content responsive to the device needs. The attribute **column-count** indicates how many columns the webpage content will be split into. The browser then changes the size of the columns accordingly.

```css
.container { 
		column-count: 2;
}
```

On the other hand, if you specify a column-width, the browser will create as many columns of that width will fit into the container. Then it will share out the remaining space between all the columns. Therefore the number of columns will change according to how much space there is.

```css
.container { 
		column-width: 12em; 
}

/* px -> absolute dimension, em -> relative dimension */
```

![28.png](https://i.loli.net/2020/08/12/umADsePUk48FVzg.png)

### Flex box

The Flex box method allows the flex items to shrink and distribute space between them according to the space in their container, as their initial behaviour. The **flex-grow** and **flex-shrink** attributes control the behaviour of the items behave when they encounter more or less space around them. 

- No floats
- Responsive and mobile friendly
- Positioning child elements is MUCH easier
- Flex container's margins do not collapse with the margins of its contents
- Order of elements can easily be changed without editing the source HTML

![29.png](https://i.loli.net/2020/08/12/w4HSnIRYO1tsbBa.png)

```css

/* the flex items will each take an equal amount of space in the flex container, using the shorthand of flex: 1 */
.container { 
	  display: flex; 
} 

.item { 
	  flex: 1; 
}
```

![30.png](https://i.loli.net/2020/08/12/G7BWM2LiwPChtUX.png)

### Grid

In the Grid Layout, the distribution of space is maintained through **fr** unit. 

```css
/* the three 1 fr will create three columns taking equal space from the container */
.container { 
  display: grid; 
  grid-template-columns: 1fr 1fr 1fr; 
}
```

![31.png](https://i.loli.net/2020/08/12/n3mJsMFSKYldg2j.png)

```css
/* when width >= 600px, divide into two column with 1:2, gap 5% */
@media screen and (min-width: 600px) {
    .wrapper {
		    display: grid;
		    grid-template-columns: 1fr 2fr;
		    column-gap: 5%;
		}
}
```

# CSS Responsive Web Design Fluid Images

No matter how perfect you build your liquid or elastic layout, it is not going to work if you do not make the content within it flexible too. Text is easy, it wraps by default. Images are a little tricky. There are a number of techniques for creating fluid images:

- Foreground images that scale with the layout
- Creating sliding composite images
- Hiding and revealing portions of images

### Dynamically Scaling Images

### Fluid

For a liquid image, setting the image’s width to a percentage value will constrains the image’s dimension:

```css
img {
   width: 50%;
}
```

Note that the **height** attribute is not necessary; the browser determines the **height** that will be proportionately constrained.

### Elastic

If you want the image to scale with the text size, then just like elastic designs, change the **width** value to an **em** value:

```css
img {
   width: 20em;
}
```

To ensure that the browser always scales the image down, not up, you can set a maximum width an image can scale to:

```css
img {
   width: 20em;
   max-width: 500px;
}
```

### Sliding Composite Images

This technique creates what appears to be a single image out of multiple pieces that slide over and away from each other. To achieve this, you will need a nested block element to place each as a background image:

```html
<div id="outer">
		<div id="inner"></div>
</div>
```

Since the divs are empty, you will need dimensions to prevent them from collapsing entirely as well as to create flexible behaviour:

```css
#outer {
   width: 100%;
   max-width: 1000px;
   height: 300px;
   background: url(skyline.jpg) no-repeat;
}

#inner {
   position: absolute;
   top: 50px;
   right: 50px;
   width: 100px;
   height: 250px;
   background: url(ufo.png) no-repeat;
}
```

### Switching Sizes

The two new attributes of <img> tag **srcset** and **sizes** help the browser to pick the right images by proving several sources of images. Here is an example:

```html
<img srcset="cat-480w.jpg 480w, cat-800w.jpg 800w"
     sizes="(max-width: 600px) 480px, 800px"
     src="cat-800w.jpg" alt="A Cat">
```

**srcset** defines the following parts:

- An image filename
- A space
- The actual width of the image, uses **w** unit.

**sizes** defines the following parts:

- A media viewport size
- A space
- The width of the slot the image will fill when the media condition is true

As a result with the **srcset** and **sizes** attribute of **<img>** tag set, the browser will work as follows:

1. The browser will first look at device's width
2. Then it will work out to see which one in the media condition defined in sizes is true.
3. Then it will take that slot size and load the image referenced in **srcset** which matches closely.
4. If the browser does not support the **srcset** attribute, it will use the as usual **src** attribute to load the image.

### Solving Art Direction Problem

The **art direction problem** is the method to change the image displayed to suit different image display sizes. The <picture> element allows to solve this issue.

```html
<picture>
	  <source media="(max-width: 799px)" srcset="a-cat-480w.jpg">
	  <source media="(min-width: 800px)" srcset="cat-800w.jpg">
	  <img src="acat-800w.jpg" alt="A cat">
</picture>
```

The explanation of <picture> tag:

- The elements include a media attribute that contains a media condition.
- The srcset attributes contain the path to the image to display.
- You must provide an **<img>** element, with **src** and **alt** attribute, otherwise no images will appear. This provides a default case while none of the media condition are true and a workaround for browsers that do not support the **<picture>** element.

### Filament’s Group Solution

The Filament’s Group technique involves resizing images proportionately, but shrinks image resolution on smaller devices so that large images do not waste space unnecessarily on small screens.

### Example on Not Stretching Image

```css
div {
	  width: 100%;
	  height: 400px;
	  background-image: url('img_flowers.jpg');
	  background-size: cover;
}
```

# CSS Responsive Web Design Overall Solution

The responsive design that this course will take is to separate desktop rendering and mobile rendering. For widths between 900px and 1200px (approximately), designs will have a rather normal development process (that you are used to), with the addition of CSS queries. Anything less than 900px wide will trigger a fluid layout. All the while, both designs will be responsive. That is, **fixed widths for large and medium screens**, **but fluid widths for smaller screens.**

```jsx
// jsPair.js
document.addEventListener(“DOMContentLoaded”, function() {
   (window).bind("resize", resizeWindow);

   function resizeWindow(e){
       var newWindowWidth = $(window).width();
 
       if (newWindowWidth < 600) { // Mobile
           $("link[rel=stylesheet]").attr({href : "../css/mobile.css"});            
       } else if (newWindowWidth < 1024) { // iPad
           $("link[rel=stylesheet]").attr({href : "../css/ipad.css"});
       } else {
           $("link[rel=stylesheet]").attr({href : "../css/styles.css"});
       }
   });

});
```

```css
/* default sytle */
#container {
   width: 1200px;
   margin: 0 auto;
   padding: 20px 0;
   text-align: left;
}

header nav {
   float: right;
   margin: 24px 0 0 0;
}
 
#content {
   float: left;
   width: 900px;
   margin-right: 20px;
}
 
#content article {
   background: #FFF;
   margin: 0 0 30px 0;
   padding: 20px;
}

#sidebar {
   float: left;
   width: 280px;
}
 
#sidebar aside {
   background: #FFF;
   margin: 0 0 30px 0;
   padding: 20px;
}
```

```css
/* width < 1200px viewport */
@media (max-width: 1200px) {
		#container{
		      width: 960px;
		}
		
		#content {
		     width: 700px;
		}
			
		#sidebar {
		     width: 240px;
		}
}
```

```css
/* ipad in landscape */
@media (max-device-width: 1024px) and (orientation: landscape) {
		#container {
				width: 768px;
		}
		
		#content {
				width: 540px;
		}
		
		#sidebar {
				width: 208px;
		}
		
		header nav {
				float: none;
				clear: both;
		}
		
		header nav ul {
				width: 100%;
		}
		
		#content article img {
				float: none;
				margin: 0 0 10px 0;
				width: 100%;
		}
}
```

```css
/* ipad in portrait */
@media (max-device-width: 1024px) and (orientation: portrait) {
		#container {
				width: 600px;
		}
		
		#content {
				float: none;
				width: 600px;
				margin: 0 0 12px 0;
		}
		
		#sidebar {
				float: none;
				width: 600px;
		}

		header nav ul {
				width: 100%;
		}  
}
```

```css
@media (max-width: 600px) {
		#container, #content {
				float: none;
				width: inherit;
		}
		
		#content {
				margin: 0;
		}
		
		#sidebar,#banner {
				display: none;
		}
		
		header nav {
				float: none;
				clear: both;
		}
		 
		header nav ul {
				width: 100%;
		}
		
		header nav ul li {
				float: none;
				display: block;
				width: 100%;
				font-size: 14px;
				text-align: left;
				border-bottom: 1px solid #938A78;
		}
		
		#content article img {
				display: none;
		}
		
		#sidebar aside {
				background: #A79F91;
				color: #FFF;
				float: left;
				width: 250px;
				min-height: 170px;
				margin-right: 20px;
				padding: 20px;
		}
}
```

![34.png](https://i.loli.net/2020/08/12/AK6FOQL8E4MDV2o.png)

```html
<!-- left hand side, for desktop takes 25%, for tablet takes 25% -->
<div class="col-desktop-25 col-tablet-25 menu">
    <ul>
        <li>The Flight</li>
        <li>The City</li>
    </ul>
</div>

<!-- middle content, for desktop takes 50%, for tablet takes 75% -->
<div class="col-desktop-50 col-tablet-75">
    <h1>The City</h1>
</div>

<!-- right hand side, for desktop takes 25%, for tablet takes 100% -->
<div class="col-desktop-25 col-tablet-100">
    <h2>What?</h2>
    <p>Chania is a city on the island of Crete.</p>
</div>
```

```css
/* For mobile phones: */
[class*="col-"] {
    width: 100%;
}

/* For tablets: */
@media only screen and (min-width: 600px) {
    .col-tablet-25 { width: 25%; }
    .col-tablet-50 { width: 50%; }
    .col-tablet-75 { width: 75%; }
    .col-tablet-100 { width: 100%; }
}

/* For desktop: */
@media only screen and (min-width: 768px) {
    .col-desktop-25 { width: 25%; }
    .col-desktop-50 { width: 50%; }
    .col-desktop-75 { width: 75%; }
    .col-desktop-100 { width: 100%; }
}
```