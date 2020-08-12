---
layout:     post
title:      JavaScript Study Notes
date:       2020-08-12
summaries:  Study notes about interactive web pages with JavaScript
categories: JavaScript Web
---

## What is JavaScript?

A programming language used to make web pages interactive.

### Two formats:

- Client-side: execution on a local browser
- Server-side: execution on a server

**HTML**: controls content and structure of the webpage (content)

**CSS**: controls the style and layout of the webpage (presentation)

**JavaScript**: adds dynamic behaviour and interactivity to the webpage (behaviour)

## Rules for Variable Names

- You can declare a variable using `var` or `let` keyword.
- Case sensitive, e.g. `var abc` is diﬀerent from `var ABC`
- Begin with a letter (not a number), underscore (_), or dollar sign ($), e.g. `var worm` NOT `var 123worm`
- Spaces are not allowed e.g. `var trojan horse` is NOT valid
- Cannot use a reserved word (i.e. words taken by the JavaScript language) e.g. `var function` is NOT valid
- Names should be meaningful. e.g. `var silly` NOT `var a`, `var b`, `var c`;

![1.png](https://i.loli.net/2020/08/12/WJOxqzw61UrQuId.png)

## Alert Box

Often used if you want to make sure information gets through to the user

```jsx
alert('Stay with me');
```

![img](https://static.edusercontent.com/files/xHE3ptHc6e6NV9QvEVZkP7To)

## Confirm Box

Often use if you want the user to verify or accept something

```jsx
var result = confirm("Do you accept the terms and conditions?");
```

![img](https://static.edusercontent.com/files/9jGKcGXvWQ1wbLMrBlLz0mBD)

## Prompt Box

Often used if you want the user to input a value before entering a page

```jsx
var name = prompt("What's your name");
```

# Arrays

```jsx
// Regular array
var planets = new Array(); // Create an empty Array object.
planets[0] = "Mercury";   // Start populating the Array.
planets[1] = "Venus";
planets[2] = "Earth";    // Add further elements to the same Array.
console.log(planets);

// Condensed array
var planets = new Array("Mercury", "Venus", "Earth");
console.log(planets);

// Literal array
var planets = ["Mercury", "Venus", "Earth"];
planets[3] = "Mars";    // Add further elements to the same Array.
console.log(planets);
```

# Reference JS to HTML

```jsx
<script src="URL"></script>
```

## Placement of JavaScript in a HTML page

JavaScript is usually written inside the `<head>` tag. However, JavaScript is parsed and interpreted as soon as it is loaded by the browser. This means if your JavaScript is within the `<head>` tag, your JavaScript file can delay the rendering of your page.

Occasionally, you need to immediately load JavaScript, especially if it is responsible for creating page content. This is why CSS should be in the head, because you do want them to load immediately. Usually, you want the browser to load the page first and the script at the end. If this is the case, the script should be placed at the bottom, before the closing `<body>` tag.

```html
<!doctype html>
<html>
	<head>
		<title>A Web Page Title</title>
		<script src="URL" type="text/javascript">
			// JavaScript Goes Here
		</script>
	</head>

	<body>
		<script src="URL" type="text/javascript">
			// JavaScript can go here too
		</script>
	</body>
</html>
```

**unobtrusive model** → completely separate JS from HTML.

Similar to linking CSS, there are three ways to reference JavaScript to your HTML page: **externally; internally; and inline.**

## The Differences between While loop and For loop

- A `while` loop must initialise a counting variable outside the loop (used to break out of the loop eventually).
- The `while` loop must increment this counting variable manually, otherwise the loop will never end.
- In a for loop, all of this is done inside one conditional statement.

# Functions

When we are writing JavaScript to perform any significant amount of processing, we will sometimes have the same group of statements (or code) appear multiple times. **Functions** allow us to define these **repeated codes** just **once**. When we need to run the function, we just **"call"** it (or run it by yelling out its name). This makes maintaining the code easier as we only have one place where the particular series of statements occur rather than repetitions of the same code. Any changes to that one block will automatically apply to each place where the function is called.

Using functions also allows us to **modularise** our approach to writing the code. When we are writing the code that calls the function, we can thus assume that the function will perform its task without having to concern ourselves with how it does works. In this way, you are also isolating any repeated errors the functions may have. If you modularise out the function, and check that it works, then you know for sure that in your full complete code with HTML and CSS, it is not the function that carries the error, but something else.

You have actually called some functions already. These include `alert()`, `prompt()` and `parseInt()`. The implementation details of all these functions are hidden from you; all you know is that you must pass it some parameters (like a `String`) and it will perform its function.

# Parameters v.s. Arguments

To elaborate on what we mean by parameters, a parameter is the variable which is part of the function's signature (function declaration). An argument is an expression used when calling the method.

Consider the following code:

```jsx
function laugh(times, speed) {
	// do something
}

function riot() {
	var dude = 1;
	laugh(dude, 2.0);
}
```

Here, `times` and `speed` are the parameters, and `dude` and `2.0` are the arguments.

# Anonymous Functions

**Anonymous functions** are functions that are **dynamically** declared at **runtime**. They are called anonymous functions because they are not given a name in the same way as normal functions. Anonymous functions are declared with just the **function operator**. Remembering a function is declared in the regular way using the function statement:

```jsx
function eatCake(){
	alert("So delicious and moist");
}
```

Here’s the same function declared dynamically using just the function operator:

```jsx
var eatCakeAnon = function(){
	alert("So delicious and moist");
};
```

- Anonymous functions as used above can help make code more concise when declaring a function that will only be used in one place.
- Rather than having to declare the function and then use it, you can do both in one step.
- If the function you need is very short, it’s often convenient to declare it when you call the function you want to pass it to.

![2.png](https://i.loli.net/2020/08/12/PTLYSEe3aGAu7yK.png)

## Local Scope

- When a variable is declared using the `var`/`let` keyword, it is only available for use INSIDE of that function.
- If you use `let` keyword it is only available to use in the immediate parent curly brace in which it resides in. This is not true for `var` keyword.
- In case of var keyword you see no error because the scope of a variable is not limited to the immediate if statement block if declared using var keyword

```jsx
//Using var keyword
if (true) {
  var x = 2;
}
console.log(x); // x is 5

//Using let keyword
if (true) {
  let y = 5;
}
console.log(y);  // ReferenceError: y is not defined
```

## Global scope

- Variables that are declared inside a function without the `var` keyword are not local to the function.
- In-fact, if you assign a value to a variable that has not been declared, it will automatically become a global variable. For example, a = 12 will creates an undeclared global variable. This is not a recommended practice.
- JavaScript will traverse from the innermost function scope to the outermost scope to find where the variable was previously defined. If the variable was not previously defined, it will be defined in the global scope, which can have extremely unexpected consequences. This means that any code, anywhere, can reference this variable without restriction.
- Variables of global scope are usually defined outside any functions.

```jsx
var greeting = "Bye";

var sayHello = function(){
   var greeting = "Hello";
   console.log(greeting);
};

sayHello(); // logs 'Hello'
console.log(greeting); // logs 'Bye'
```

- The lifetime of a JavaScript variable starts when it is declared.
- Local variables are deleted when the function is completed.
- In a web browser, global variables are deleted when you close the browser window (or tab), but remains available to new pages loaded into the same window.

# DOM Structure

The `Document Object Model (DOM)` is a programming interface for HTML documents. It represents the page as a tree-structure. It defines a standard way for generic access to programs (adding, deleting and manipulating) of all styles, attributes and elements in a document.The DOM represents the document as `nodes` and `objects`. That way, programming languages can connect to the page.

DOM is an object-oriented representation of the web page.

A Web page itself is a document. It can be either displayed in the browser window or as the HTML source. But it is the same document in both cases. The `Document Object Model (DOM)` represents that same document so it can be manipulated. The DOM is an object-oriented representation of the web page, which can be modified with a scripting language such as JavaScript. It is important to note that the DOM represents the raw structure of our content, which means it has to be created before the content is displayed on the screen.

### Hierarchical structure

The best way to think of the DOM is a huge tree with a trunk that represents the document and its branches representing the different elements on the page. Every part of the tree is called a node:

- ***Document*** **node:** the document itself
- ***Element*** **node:** mark-up tags e.g. HTML, div
- ***Attribute*** **node:** HTML attributes
- ***Text*** **node:** strings of text within HTML elements

The nodes in the tree have a hierarchical relationship to each other. The terms parent, child, and sibling are used to describe the relationships. Parent nodes have children. Children on the same level are called siblings.

- The top node is called the **root**
- Every node has exactly one parent, except the root (which has no parent)
- A node can have any number of children
- Siblings are nodes with the same parent

The following diagram displays the general DOM tree of a web document where the root of the tree (first parent) is the browser window object. An object has properties and methods (or actions of the object). Everything in a document and everything in the browser window is an object e.g. window, document, form and buttons. The DOM defines these objects and properties of all HTML elements, and the methods to access them.

![12.png](https://i.loli.net/2020/08/12/Sfy84Wi7szokHgK.png)
![10.png](https://i.loli.net/2020/08/12/jmz2MfHYltUobkL.png)

# How your Webpage loads

**1**. The browser loads a document, which includes mark-up written in HTML and style written in CSS.

2. As the browser loads your page, it also creates an internal model of your document that contains all the elements of your HTML mark-up.

![11.png](https://i.loli.net/2020/08/12/HJg9CYdTzX48lDi.png)

3. After the browser has loaded your page, it loads your JavaScript code of which interacts with your page through the DOM tree.

Using JavaScript, you can interact with your page by manipulating the DOM, reacting to user or browser-generated events, or make use of all the new APIs (Application Programming Interface). APIs provides a set of objects, methods and properties that we can use to access all the functionality of the HTML/CSS/JavaScript technologies (kind of like a reference guide). The APIs give you access to things like audio, video, 2D drawing and local storage.

# Event Handlers

There are 3 ways to assign event handlers:

1. HTML attribute: `onclick="...".`
2. DOM property: `elem.onclick =` function.
3. Methods: `elem.addEventListener(event, handler[, phase])` to add, `removeEventListener` to remove.

```jsx
// click to change from greetings to hi
<h1 onclick="this.innerHTML = 'Hi!'">Greetings</h1>

// click to call displayData()
<button onclick="displayData()">Display Data</button>w

onclick=processOption(testDropDown.value)
onclick="processOption(testDropDown.value)"
onclick='processOption(testDropDown.value)'
```

# EventListener

The fundamental problem of the ways mentioned in the previous page to assign handlers is that it is not possible to assign multiple handlers to one event.

To solve this issue, an alternative way of managing handlers is using `addEventListener()` and `removeEventListener()`.

The `addEventListener()` method has the following properties:

- The `addEventListener()` method attaches an event handler to the specified element.
- The `addEventListener()` method attaches an event handler to an element without overwriting existing event handlers.
- You can add many event handlers to one element.
- You can add many event handlers of the same type to one element, i.e two `"click"` events.
- You can add event listeners to any DOM object not only HTML elements. i.e the window object.
- The `addEventListener()` method makes it easier to control how the event reacts to bubbling.
- When using the `addEventListener()` method, the JavaScript is separated from the HTML markup, for better readability and allows you to add event listeners even when you do not control the HTML markup.

### Syntax

```jsx
element.addEventListener(event, function, useCapture);
```

- The first parameter is the type of the event (like `"click"` or `"mousedown"`).
- The second parameter is the function we want to call when the event occurs.
- The third parameter is a `boolean` value specifying whether to use event bubbling or event capturing. This parameter is optional.

### Add an Event Handler to an Element

```jsx
<h1 id="header1">Greetings</h1>

// alert "Hi!" when user click on an element
var element=document.getElementById("header1");
element.addEventListener("click", function(){ this.innerHTML = 'Hi!'; });
```

### Add Many Event Handlers to the Same Element

```jsx
<h1 id="header1">Greetings</h1>

var element=document.getElementById("header1");
element.addEventListener("mouseover", myFunction);
element.addEventListener("click", mySecondFunction);
element.addEventListener("mouseout", myThirdFunction);

function myFunction() {
	this.innerHTML = 'Hi!';
}
```

### Add an Event Handler to the Window Object

```jsx
<h1 id="demo">Greetings</h1>

// change text when user resize the window
window.addEventListener("resize", function(){
	document.getElementById("demo").innerHTML = "sometext";
});
```

## Event Bubbling or Event Capturing?

There are two ways of event propagation in the HTML DOM, **bubbling** and **capturing**.

**Event propagation** is a way of defining the *element order* when an event occurs. If you have a `<p>` element inside a `<div>` element, and the user clicks on the `<p>` element, which element's `"click"` event should be handled first?

In bubbling the inner most element's event is handled first and then the outer: the `<p>` element's click event is handled first, then the `<div>` element's click event.

In capturing the outer most element's event is handled first and then the inner: the `<div>` element's click event will be handled first, then the `<p>` element's click event.

With the `addEventListener()` method you can specify the propagation type by using the `useCapture` parameter:

```jsx
addEventListener(event, function, useCapture);

// to remove
element.removeEventListener("mousemove", myFunction);
```

The default value is false, which will use the bubbling propagation, when the value is set to true, the event uses the capturing propagation.

## Setting and Getting Content

In order to manipulate the DOM with JavaScript, we need to be able to select individual elements.

```jsx
// id are unique, return a single element
var first = document.getElementById("primary");

// return an array of elements
var second = document.getElementsByTagName("h1");
var third = document.getElementsByName("username");
var fourth = document.getElementsByClassName("odd");

// HTML object collections, return a list of all <p> elements with class="classname"
var fifth = document.querySelectorAll("p.classname");
```

The selection of HTML elements by HTML object collections have been discussed in JavaScript DOM HTML `Collection` and `Nodelist`.

We can also create new elements using the `createElement` method. The following creates a new `h1` element.

```jsx
var first = document.createElement("h1");
first.textContent="Welcome";
document.body.appendChild(first);
```

Once we have access to individual elements from the DOM, we can use the textContent, innerHTML and value properties to get and set text, HTML, and values. These three things might seem like the same thing, but they’re not. Text is a textual (no HTML) representation of the inner content for all regular elements; values are for form elements; and HTML is the same as text, but includes mark-up.

```jsx
<div id="divAlert">
	  <div id="divText"></div>
	  <div id="divHtml"></div>
	  <h1>Input Box:</h1>
	  <input type="text" id="txtTest" name="txtTest" value="Hello" />
</div>

document.addEventListener("DOMContentLoaded", function() {
   // Getting content-----------------

	 // textContent displayed no text in the console because there is no text inside the div tag
   console.log("Text: " + document.getElementById("divAlert").textContent)

	 // innerHTML of the same tag returned the mark-up that was nested inside the selector
   console.log("HTML: " + document.getElementById("divAlert").innerHTML);

	 // value returned the value of the input text
	 console.log("Value: " + document.getElementById("divAlert").value);


   // Setting content-----------------

	 // textContent interprets HTML tags as plain text
   document.getElementById("divText").textContent = "<em><strong>A dynamically set text</strong></em>";

	 // innerHTML interprets HTML tags as HTML code
   document.getElementById("divHtml").innerHTML = "<em><strong>A dynamically set HTML string</strong></em>";

   // value interprets HTML tags as plain text, as applicable for input elements
	 document.getElementById("txtTest").value = "<em><strong>A dynamically set value</strong></em>";
});
```

![3.png](https://i.loli.net/2020/08/12/EhtVnIGs6wNK3j9.png)

Noticing the difference between textContent and innerHTML, this tells us when we are extracting form data from the user, it is best to use textContent and not innerHTML. This is particularly true if a user enters dangerous scripts to hack or destroy content; you don’t want it to be interpreted as scripts, but non-destructive plain text.

## Manipulating Attributes

```jsx
<a href="https://www.google.com" id="aGoogle1">Google Link</a>
<a href="https://www.it.usyd.edu.au" id="aUsyd1">Usyd IT Link</a>

document.addEventListener("DOMContentLoaded", function(){
    // Setting the attribute
    document.getElementById("aGoogle1").setAttribute("href", "https://www.google.com.au");

		// Getting the attribute
		console.log(document.getElementById("aGoogle1").getAttribute("href"));
});

// Traversal
ELEMENT.firstChild();
ELEMENT.lastChild();
ELEMENT.childNodes(); // Return an array of all children
ELEMENT.parentNode();
```

## Inserting Content

```jsx
<a id="appending" href="#">Append</a>
<a id="prepending" href="#">Prepend</a>
<ol id="olList">
   <li>Existing Item</li>
</ol>

document.addEventListener("DOMContentLoaded", function(){
		// ELEMENT.appendChild(newElement);
		// click append link, "Append Item" is insert after the last list item
    document.getElementById("appending").onclick = function(){
        var item1 = document.createElement("li");
        item1.textContent = "Append Item";
        document.getElementById("olList").appendChild(item1);
    };

		// ELEMENT.insertBefore(newElement, existingElement);
		// click prepend link, "Prepend Item" is inserted before the first list item
    document.getElementById("prepending").onclick = function(){
		    var item1 = document.createElement("li");
        item1.textContent = "Prepend Item";
        var list = document.getElementById("olList");
        list.insertBefore(item1, list.firstChild);
    };
});
```

## Removing Content

```jsx
<ul id="container">
    <li id="us">Google.com</li>
    <li id="au">Google AU</li>
    <li id="uk">Google UK</li>
</ul>
<a id="removeAll" href="#">Remove all</a>

document.addEventListener("DOMContentLoaded", function(){
    // click individual list item will remove that item
		document.getElementById("us").onclick = function(){
        var item = document.getElementById("us");
        item.parentNode.removeChild(item);
    });

    document.getElementById("au").onclick = function(){
        var item = document.getElementById("au");
        item.parentNode.removeChild(item);
    });

    document.getElementById("uk").onclick = function(){
        var item = document.getElementById("uk");
        item.parentNode.removeChild(item);
    });

		// click "remove all" link, the entire list will be removed
    document.getElementById("removeAll").onclick = function(){
        var item = document.getElementById("container");
        while (item.firstChild){
           item.removeChild(item.firstChild);
        }
    });
});

// item.removeChild(item.childNodes[0]);
// item.replaceChild(replaceElement, item.childNodes[0]);
```

## HTML Collection

An `HTMLCollection` is a collection of HTML elements. `HTML Collection` items can be accessed by their name, id, or index number

```jsx
function CollectionFunction() {
	 var pCollection = document.getElementsByTagName("p");
	 for (var i = 0; i < pCollection.length; i++) {
			 pCollection[i].style.color = "green";
	 }
}
```

## Node List

A `NodeList` is a collection of document nodes. `NodeList` items can only be accessed by their index number. It can also contain attribute nodes and text nodes.

```jsx
function NodeListFunction() {
	 var pNodeList = document.querySelectorAll("h2");
	 for (var i = 0; i < pNodeList.length; i++) {
			 pNodeList[i].style.backgroundColor = "green";
	 }
}
```

HTML Collection VS Node List

- Both `HTMLCollection` object and `NodeList` object are an array-like list (collection) of objects, not an array!
- Both have a length property defining the number of items in the list (collection).
- Both provide an index (0, 1, 2, 3, 4, ...) to access each item like an array.
- Cannot use array methods like valueOf(), pop(), push(),  join() or Node.childNodes() on an `HTMLCollection` or a `Nodelist`.

## JavaScript Object-Oriented Programming

An object is a thing, or entity. Objects have properties and methods. **Properties** are attributes of the object. **Methods** are the actions of an object.

In JavaScript, an object is an HTML element such as a: `window`, `document`, `form`, `button`,etc…

- **Properties**: `document.URL`, `document.title`
- **Methods**: `document.write()`

## Window Properties

The window object represents the browser window. Note the location property (it's very useful).

- `defaultStatus` - Reflects the default message displayed in the window's status bar.
- `document` - Contains information on the current document, and provides methods for displaying HTML output to the user.
- `locationbar` - Represents the browser window's location bar.
- `location` - Contains information on the current URL
- `name` - A unique name used to refer to this window.
- `status` - Specifies a priority or transient message in the window's status bar
- `statusbar` - Represents the browser window's status bar.
- `toolbar` - Represents the browser window's toolbar.

```jsx
<script>
		function windowProperty() {
				alert("Window Location: " + window.location);
		}
</script>
<b>Window Properties: </b>
<input type="button" value="Find Out URL" name="buttonWP" onclick="windowPreperty()">
```
![4.png](https://i.loli.net/2020/08/12/zK53BQ1eojPD8GI.png)

## Window Methods

- `alert` - Displays an Alert dialog box with a message and an OK button.
- `close` - Closes the specified window.
- `confirm` - Displays a Confirm dialog box with the specified message and OK and Cancel buttons.
- `open` - Opens a new web browser window.
- `print` - Prints the contents of the window or frame.
- `prompt` - Displays a Prompt dialog box with a message and an input field.
- `find` - Finds the specified text string in the contents of the specified window.
- `forward` - Loads the next URL in the history list.

```jsx
function windowMethod() {
		var selfdestruct = window.confirm("do you want to self destruct this window?");
		if (selfdestruct == true) {
		   window.close();
		} else {
		   window.alert("Window is still operational");
		}
}
```

## Document Properties

- `alinkColor` - A string that specifies the `ALINK` attribute.
- `anchors` - An array containing an entry for each anchor in the document.
- `bgColor` - A string that specifies the `BGCOLOR` attribute. `document.bgColor` is deprecated in DOM Level 2 HTML. The recommended alternative is CSS style `background-color` which can be accessed through the DOM with `document.body.style.backgroundColor`. Another alternative is `document.body.bgColor`, although this is also deprecated in HTML 4.01 in favour of the CSS alternative.
- `cookie` - Specifies a cookie.
- `fgColor` - A string that specifies the `TEXT` attribute.
- `lastModified` - A string that specifies the date the document was last modified.
- `linkColor` - A string that specifies the `LINK` attribute.
- `links` - An array containing an entry for each link in the document.
- `referrer` - A string that specifies the URL of the calling document.
- `title` - A string that specifies the contents of the `TITLE` tag.
- `URL` - A string that specifies the complete `URL` of a document.
- `vlinkColor` - A string that specifies the `VLINK` attribute.

```jsx
// change the background color from yellow to orange by clicking the button
<script>
     function documentProperty() {
       window.alert("The document background color is changing to Orange");
       document.body.style.backgroundColor="Orange";
     }
</script>
</head>
 <body style="background-color:yellow;">
     <h1>Testing Document Properrties</h1>
		 <p>
		     <b>Document Properties :</b>
		     <input type="button" value="Change Background Color" name="buttonWP" onclick="documentProperty()">
     </p>
</b
```

## Document Methods

- `close` - Closes an output stream and forces data to display.
- `open` - Opens a stream to collect the output of `write` or `writeln` methods.
- **`write`** - Writes one or more HTML expressions to a document in the specified window.
- **`forms`** - An array a containing an entry for each form in the document.

```jsx
document.write("Document Title: " + document.title + "<br>");
```

# HTML Form

`<form>` tags are a container tag holding all form elements such as text boxes, drop-down boxes and submit buttons. Forms are essentially made up of two things: `label` and `input tags`.

- The input element is some element that the user can enter in the information. The type attribute specifies the type of the input e.g. text, password, radio, checkbox, submit.
- Labels are the input’s corresponding text in order to indicate what information the input element is looking for.
- Creating forms essentially involve specifying these two things: the input element and its corresponding label text.
- To relate the `label` and `input` together, the for attribute of the `label` tag should be equal to the `id` attribute of the related input tag.

![5.png](https://i.loli.net/2020/08/12/ah1QBrAjqEPtCcH.png)

```jsx
<form action="redirectURL" method="post/get">
	 <!-- Collection of Fields -->
   <fieldset>
       <legend>Caption for Fieldset</legend>
       <label for="firstName">Name</label>
       <input type="text" name="firstName" />

       <input type="password" />
       <input type="checkbox" checked="checked" />
       <input type="radio" name="radioGroupName" checked="checked" />
       <input type="submit" value="Send" />
       <input type="reset" />
       <input type="hidden" />
   </fieldset>

   <!-- HTML5 Input types -->
   <input type="color" />
   <input type="date" />
   <input type="datetime" />
   <input type="email" />
   <input type="number" />
   <input type="search" />
   <input type="time" />
   <input type="url" />

   <!-- Drop Down List -->
   <select>
       <option>Firefox</option>
       <option selected="selected">Chrome</option>
       <option>Safari</option>
   </select>

   <!-- Large text box -->
   <textarea name="comment" rows="60" cols="20"></textarea>

</form>
```

- You can divide each form section by a `<fieldset>`
- The action attribute of the form specifies the location of where the information will be sent to. In this case, when the user clicks the submit button, the page will be redirected to `submit.htm`
- The method attribute of the form specifies how data will be sent to the server. The value can only be `get` or `post`
- The first element inside the form is a text field to capture a name: `<input id="nameFirst" name="nameFirst" placeholder="Jane" required="" autofocus="" type="text" />`where
    - `<input>` specifies an input element used to collect user input.
    - `name` specifies the name of the input element
    - `placeholder` represents a short hint (a word or short phrase) intended to aid the user with data entry
    - `required` specifies an element must be filled out before it can be submitted
    - `autofocus` specifies an element should be focused on when the page is first loaded
    - `type` determines which input element is used.
    - In our example text refers to a single-line textbox. Other types include number, email, file, etc.
- The third form element is a *drop down box*, useful in limiting user choices and keeping data consistent
- Drop down boxes need to enclose selection choices (data elements) with the `<select></select>` Inside the `<select></select>` tags are the individual selection choices using the `<option></option>` tags (similar to how an ordered list `<ol>` requires individual list items `<li>`)Each selection choice should be given a value and a display text. `<option>I don't study</option>`

# JS OOP Form

![6.png](https://i.loli.net/2020/08/12/FGX8f7UaL5VOSyD.png)

```jsx
<select size="1" name="choice">
		<option value="earth">earth</option>
		<option value="mars">mars</option>
		<option value="moon">moon</option>
</select>

// choice.value --> choice is the name of select
<input type="button" value="Process Option" name="buttonDropDown" onclick="processDropDown(choice.value)">

function processDropDown(selected) {
     alert("The drop down value is: " + selected);
}
```

```jsx
<form name="textboxForm" action="index.html" onSubmit="processTextBox(firstname,lastname)">
   First name is: <input type="text" name="firstname"><br />
   Last name is: <input type="text" name="lastname"><br />
   <input type="submit" value="Submit" name="buttonSubmit">
   <input type="reset" value="Reset" name="buttonReset">
</form>

function processTextBox(fname,lname) {
   alert("The full name is " + fname.value + " " +lname.value );
}
```

# JavaScript Form Validation

JavaScript can be applied to validate HTML form. Primarily, the purpose of data validation is to ensure correct user input. The following type of validation are common:

- Check empty fields - if the field is required, the user must fill in that field.

    ```jsx
    function validateForm() {
    		// customer is form id, nameFirst is input id
    		var x = document.forms["customer"]["nameFirst"].value;
    		if (x == "") {
    				alert("Name must be filled out");
    				return false;
    		}
    }
    ```

- Date validation - if the user has entered the correct date.
- Numeric field/ text field validation - The user has entered the correct type of data and in a correct format. For example, numbers in age field, a specific format for phone number.

    ```jsx
    function validateForm() {
    		// customer is form id, numOfVehicles is input id
    		var numOfV = document.forms["customer"]["numOfVehicles"].value;
    		if (numOfV== "" || isNaN(numOfV)) {
    				// If isN is Not a Number
    				alert("Number of Vehicle is not a number");
    				return false;
    		} else {
    				return true;
    		}
    }
    ```

Validation can be defined by many different methods and deployed in many different ways.

- **Server-side validation**: It is performed by a web server, after input has been sent to the server.
- **Client side validation**: It is performed by a web browser, before the input is sent to a web server.

# JavaScript Event Driven Programming

JavaScript uses an event-driven programming model where functions or actions are triggered off by **pre-defined** events (i.e. to provide more interactiveness to users).

![7.png](https://i.loli.net/2020/08/12/iMeCUQ8lZA6cvF9.png)

### On Submit Event

```jsx
<form name="form1" action="submit.html" onsubmit="somefunction(someText.value)">
		<p>First Name:
				<input type="text" name="someText">
		</p>

		<p>
				<input type="submit" value="Submit" name="B1">
				<input type="reset" value="Reset" name="B2">
		</p>
</form>

function somefunction(someText.value) { alert(); }
```

![8.png](https://i.loli.net/2020/08/12/PbUlMVRFWm6prYy.png)

### On Change Event

```jsx
<p>first name:
		<input type="text" name="firstname" onchange="displayName(firstname.value,lastname.value)">
</p>
<p>last name:
		<input type="text" name="lastname" onchange="displayName(f1)">
</p>
<p>full name:
		<input type="text" name="fullname">
</p>

// form name is f1, input name is fullname
function displayName(fname,lname) {
		document.f1.fullname.value = fname + " " + lname;
}

function displayName(someForm) {
		document.f1.fullname.value = someForm.firstname.value + " " + someForm.lastname.value;
}
```

# JavaScript Web Storage

The main problem with HTTP as the main transport layer of the Web is that it is stateless. This means that when you use an application and then close it, its state will be reset the next time you open it. This is why, as a developer, you need to store the state of your interface somewhere. Remembering states have the advantage of “remember-me” session management or remembering user preference/personalisation (web storage can).

Cookies were invented early in the web’s history, primarily to store small amounts of data (4 KB) on the server-side. Cookies pass EVERY request to the server, making it very slow. Further, the data it sends is generally unencrypted (without SSL - Secure Sockets Layer) and thus exploitable by XSS (Cross-site scripting).

In response, HTML5 offers two new objects for storing data, this time, on the client-side, more suitable for large amounts of data (up to 10 MB). The advantage of web storage is that it does not pass every request, it only passes when asked. This means we can store large amounts of data, client-side, to read and write as we like without affecting website performance. Thus, web storage is more secure and efficient with a higher capacity option.

The new capabilities brought by HTML5 may seem to make cookies outdated. However, cookies and web storage are two very different things. Web storage does not replace cookies, but rather, an alternative. Deciding to use web storage means you have to take care of data exchange between the client and the server if you want to manipulate data on the server. Cookies, on the other hand, are always available on the server and can be read and written freely.

## The Storage

Items are stored as strings in key-value pairs. There are two objects for storing data on the client:

- `localStorage` – stores data with no time limit
- `sessionStorage` – stores data for one session

Some of the storage methods are outlined below:

- `clear` - Removes all key/value pairs from web storage
- `getItem(key)` - Retrieves the current value associated with the web storage key
- `removeItem(key)` - Deletes a key/value pair from the web storage collection
- `setItem(key)` - Sets a key/value pair

```jsx
document.addEventListener("DOMContentLoaded", function() {

	   document.getElementById("submitMe").onclick = function() {
					 // Extract a value from an input element
		       var name = document.getElementById("name1").value;
		       var secret = document.getElementById("secret").value;

					 // Ensure execution only if the user enters correct input
		       if ((name.length != 0) && (secret.length != 0)) {
				      // Set storage with name "nameOfStupid"
		         localStorage.setItem("nameOfStupid",name);
		         localStorage.setItem("secret",secret);

		         // Get storage from "nameOfStupid" in order to display to user
		         response = document.getElementById("response");
		         response.innerHTML = "<h4>Ha ha " + localStorage.getItem('nameOfStupid') + ", I know your secret: " + localStorage.getItem('secret') + "</h4>";
			     }
		 };

		 document.getElementById("clearMe").onclick = function() {
			     // Clear storage
			     localStorage.clear();
			     document.getElementById("response").innerHTML("<h4>You jerk!</h4>");
		 };

		 // When the page loads, ensure any secret is displayed to the user (Get)
		 var storedName = localStorage.getItem('nameOfStupid');
		 var storedSecret = localStorage.getItem('secret');
		 if ((storedName != null) && (storedSecret != null)){
			     response = document.getElementById("response");
			     response.innerHTML = "<h4>Ha ha " + localStorage.getItem('nameOfStupid') + ", I know you're secret: " + localStorage.getItem('secret') + "</h4>";
		 }
}
```

Essentially, in order to save an item to storage you must give it a name and assign it a value, similar to your variables. Also similar to your variable, in order to retrieve storage items for use, call the `getItem()` method with the storage variable name as the parameter. Notice that we used a shortcut to setting storage:

```jsx
var newCount = parseInt(localStorage.getItem("pagecount") + 1;
localStorage.setItem("pagecount", newCount);

// OR shortcut:
localStorage.pagecount = newCount
```

Remember, data is stringified when it is written to storage i.e. if you input an integer and read it back from storage, it is of a string data type. You must therefore force this input back into an integer via `parseInt()`.

Note that before you can process the form data or process previously saved storage, you must validate that the user information is correct and exists. We did this by:

- Checking the input is not empty: `name.length != 0`
- Checking previously saved storage is not empty: `storedSecret != null`

```jsx
/* Set/Get storage */
localStorage["name"] = "Homer";
var localVal = localStorage["name"];

// Alternatively
sessionStorage.setItem("name", "Homer");
sessionStorage.getItem("name");

/* Remove an storage item */
localStorage.removeItem('key')
sessionStorage.removeItem('key')

/* Clear storage */
localStorage.clear();
sessionStorage.clear();

// Make images load faster
var imageObject = new Image("http://www.google.com/logo.gif");
localStorage.setItem("image", imageObject);

// Storing Objects
var car = {};
car.wheels = 4;
car.doors = 2;
car.sound = "vroom";
car.name = "Lightning McQueen";
localStorage.setItem('car', JSON.stringify(car));
localStorage.getItem(JSON.parse(localStorage.getItem('car')));
```

Web Storage Advantage

- Simplicity → Several APIs are available on web, allowing developers to assign values for SessionStorage and LocalStorage.
- Sufficient Data
    - Large amount of space allotted, around 5-10MB of data
    - Storage includes components ranging from session details to temporary offline files.
    - You can synchronize this data to your server as well.
- Database Storage → Structured data can be saved in user-side using SQL DB.
- But Security → is no better than Cookies, it is advised to not to keep sensitive information through Local Storage, web storage are always available on the server and can be read and written freely

![9.png](https://i.loli.net/2020/08/12/LsmKIrHwfi24bRO.png)

# Cookies

- Cookie are small text files stored on your computer by a website.
- A Cookie file contains the following fields in a name/ value pair format
    - Name
    - Content
    - Domain
    - Path
    - Send For
    - Expiry Date
- Cookies are stored in the document.cookie object

### Cookies in Interactive Site

- Create cookie variables for every piece of information that you want to store. e.g. userid, password, user information
- You can retrieve this stored information using the getCookie function.
- You can use a maximum of 20 Cookie per domain.
- Cookie file cannot exceed 4KB (4000 characters)
- Client-server constantly passing cookies (and vice versa)
- Data generally unencrypted

```jsx
function setCookie(NameOfCookie, cvalue, expiredays){
    var d = new Date();

    // expiredays convert to expiredate
    d.setTime(d.getTime() + (expiredays * 24 * 60 * 60 * 1000));

    // convert date to strings
    var expires = "expires=" + d.toGMTString();

    // store into cookies
    document.cookie = NameOfCookie + "=" + cvalue + "; " + expires;
}

function getCookie(NameOfCookie) {
    if (document.cookie.length > 0) {

        // separate the cookie key before = sign
        begin = document.cookie.indexOf(NameOfCookie + "=");
        if (begin != -1) {
            begin += NameOfCookie.length + 1;

            // search for ;  start at begin
            end = document.cookie.indexOf(";", begin);
            if (end == -1) {
                end = document.cookie.length;
            }

            // decode the encode string
            return unescape(document.cookie.substring(begin, end));
        }
    }
    return null;
}

function  delCookie(NameOfCookie) {
    // in order to delete a cookie, set the expires date to something in the past
    if (getCookie(NameOfCookie)) {
        document.cookie = NameOfCookie + "=" + "; expires=Thu, 01-Jan-70 00:00:01 GMT";
    }
}
```

### Cookies Limitation

- Privacy
    - any website you browse can store cookies in our web browser, unless you have not turned off cookie feature.
    - Cookies provide mechanism to track browsing history and other details of the user.
- Size limit → Cookies can store only a small amount of data
- Speed
    - It requires a noticeable amount of data traffic. Hence, cookies can slow down your web application.
    - Submitted data are transferred to the server without any kind of data-encryption features, hence, this can make issues with privacy.
