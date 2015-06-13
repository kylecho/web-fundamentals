#The Document Object Model [Link](http://www.w3.org/DOM/)

With the HTML DOM, JavaScript can access and change all the elements of an HTML documents. When a page is loaded, the browser creates a Document Object Model of the page.

The DOM is a W3C standard. The DOM defines a standard for accessing documents:
"The W3C Document Object Model (DOM) is a platform an language-neutral interface that allows programs and scripts to dynamically access and update the content, structure, and style of document."

The W3C DOM standard is separated into 3 different parts:

* Core DOM - standard model for all document types
* XML DOM - standard model for XML documents
* HTML DOM - standard model for HTML documents

The HTML DOM is a standard object model and programming interface for HTML. It defines:

* The HTML elements as objects
* The properties of all HTML elements
* The methods to access all HTML elements
* The events for all HTML elements

In other words, the HTML DOQM is a standard for how to get, change, add, or delete HTML elements.

###The HTML DOM is constructed as a tree of Objects:

```
                          Document
                             |
                        Root element:
                           <html>
                             |
    +------------------------+-------------------------+
    |                                                  |
 Element:                                           Element:
 <head>                                              <body>
    |                                                  |
    |                                           +--------------+
 Element:            Attribute: +----------+ Element:       Element:
 <title>               "href"                  <a>            <h1>
    |                                           |               |
  Text:                                       Text:          Text:
"My title"                                  "My link"     "My header"

```

With the object model, JavaScript gets all the power it needs to create dynamic HTML:

* JavaScript can change all the HTML elements in the page
* JavaScript can change all the HTML attributes in the page
* JavaScript can change the CSS in the page
* JavaScript can remove existing HTML elements and attributes
* JavaScript can add new HTML elements and attributes
* JavaScript can react to all existing HTML events in the page
* JavaScript can create new HTML events in the pageq

# DOM Methods

HTML DOM methods are actions you can perform (on HTML Elements).

HTML DOM properties are values (of HTML Elements) that you can set or change.

### The DOM Programming Interface

The HTML DOM can be accessed with JavaScript (and with other programming languages). In the DOM, all HTML elements are defined as objects. A property is a value you can get or set (like changing the content of an HTML element), and a method is an action you can do (like add or deleting an HTML element).

The following example changes the content (the innerHTML) of the <p> element with id="demo" when the button is clicked.
```
<!DOCTYPE html>
<html>
<head>
	<title>Example</title>
</head>
<body>

<p id="demo"></p>
<input type="button" value="Show" onclick="fillText()">

<script type="text/javascript">

var fillText = function(){
	document.getElementById("demo").innerHTML = "Hello World!";
};

</script>

</body>
</html>
```

* `getElementById` - will access an HTML element by the id of the element.
* `innerHTML` - will get the content of an element. It is useful for getting or replacing the content of HTML elements.

# DOM Document

In the HTML DOM, the document object represents your web page. The document object is the owner of all other objects in your web page. If you want to access objects in an HTML page, you always start with accessing the document object. Below are some examples of how you can use the document object to access and manipulate HTML.

###Finding HTML Elements

* `document.getElementById()` - Find an element by element id
* `document.getElementsByTagName()` - Find elements by tag name
* `document.getElementsByClassName()` - Find elements by class name

###Adding and Deleting Elements

* `document.createElement()` - Create an HTML element
* `document.removeChild()` - Remove an HTML element
* `document.appendChild()` - Add an HTML element
* `document.replaceChild()` - Replace an HTML element
* `document.write(text)` - Write into the HTML output stream

###Adding Event Handlers

* `document.getElementById(id).onclick = function(){code}` - Adding event handler code to an onclick event

###Finding HTML Objects

The first HTML DOM Level 1 (1998), defined 11 HTML objects, object collections, and properties. These are still valid in HTML5.

Later, in HTML DOM Level 3, more objects, collections, and properties were added.

```
  Property                Description                                                     DOM
----------------------------------------------------------------------------------------------
* document.anchors        Returns all <a> elements that have a name attribute             1
* document.applets        Returns all <applet> elements (Deprecated in HTML5)             1
* document.body           Returns the <body> element                                      1
* document.cookie         Returns the document's cookie                                   1
* document.domain         Returns the domain name of the document server                  1
* document.images         Returns all <img> elements                                      1
* document.forms          Returns all <form> elements                                     1
* document.links          Returns all <area> and <a> elements that have a href attribute  1
* document.referrer       Returns the URI of the referrer (the linking document)          1
* document.title          Returns the <title> element                                     1
* document.URL            Returns the complete URL of the document                        1
* document.baseURI        Returns the absolute base URI of the document                   3
* document.doctype        Returns the document's doctype                                  3
* document.documentElement Returns the <html> element                                     3
* document.documentMode   Returns the mode used by the browser                            3
* document.documentURI    Returns the URI of the document                                 3
* document.domConfig      Obsolete. Returns the DOM configuration                         3
* document.embeds         Returns all <embed> elements                                    3
* document.head           Returns the <head> element                                      3
* document.implementation Returns the DOM implementation                                  3
* document.inputEncoding  Returns the document's encoding (character set)                 3
* document.lastModified   Returns the date and time the document was updated              3
* document.readyState     Returns the (loading) status of the document                    3
* document.scripts        Returns all <script> elements                                   3
* document.strictErrorChecking Returns if error checking is enforced                      3
```

# DOM Elements

###Finding HTML Elements

Often, with JavaScript, you want to manipulate HTML elements.

To do so, you have to find the elements first. There are a couple of ways to do this:

* The example finds the element with id="intro":
`var x = document.getElementById("intro");`

* This example finds all <p> elements:
`var x = document.getElementsByTagName("p");`

* This example finds the element with id="main", and then finds all <p> elements inside "main":
```
var x = document.getElementById("main");
var y = x.getElementsByTagName("p");
```

* This example returns a list of all elements with class="intro":
`var x = document.getElementsByClassName("intro");`

If you want to find all HTML elements that matches a specified CSS selector (id, class, names, types, attributes, values of attributes, etc), use the `querySelectorAll()` method.

* This example returns a list of all <p> elements with class="intro":
`var x = document.querySelectorAll("p.intro");`

* This example finds the form element with id="frm1", in the forms collection, and displays all element values:
```
var x = document.forms["frm1"];
var text = "";
var i;
for (i = 0; i < x.length; i++) {
	test += x.elements[i].value + "<br>";
}
document.getElementById("demo").innerHTML = text;
```
The following HTML objects (and object collections) are also accessible:

```
document.anchors
document.body
document.documentElement
document.embeds
document.forms
document.head
document.images
document.links
document.scripts
document.title
```

# DOM HTML

* `document.write()` - can be used to write directly to the HTML output stream:

Below example will display "Hello World!".
```
<!DOCTYPE <!DOCTYPE html>
<html>
<head>
	<title>Example</title>
</head>
<body>

<script>
document.write("Hello World!");
</script>

</body>
</html>
```
* `document.getElementById(id).innerHTML = "some content"` - will change the content of the element:

```
<html>
<body>

<p id="p1">Hello World!</p>

<script>
document.getElementById("p1").innerHTML = "New text!";
</script>

</body>
</html>
```

This example changes the content of an `<h1>` element:

```
<!DOCTYPE html>
<html>
<body>

<h1 id="header">Old Header</h1>

<script>
var element = document.getElementById("header");
element.innerHTML = "New Header";
</script>

</body>
</html>
```

`document.getElementById(id).attribute = "new value"` - will change the value of an HTML attribute:

```
<!DOCTYPE html>
<html>
<body>

<img id="myImage" src="smiley.gif">

<script>
document.getElementById("myImage").src = "landscape.jpg";
</script>

</body>
</html>
```

# DOM CSS

The HTML DOM allows JavaScript to change the style of HTML elements.

`document.getElementById(id).style.property="new style"` - will change the style of an HTML element:

The following example changes the style of a `<p>` element:

```
<!DOCTYPE html>
<html>
<head>
	<title>Example</title>
</head>
<body>

<p id="p2">Hello World!</p>

<script>
document.getElementById("p2").style.color = "blue";
</script>

</body>
</html>
```

The HTML DOM allows you to execute code when an event occurs.

Events are generated by the browser when "things happen" to HTML elements:

* An element is clicked on
* The page has loaded
* Input fields are changed

This example changes the style of the HTML element with id="id1", when the user clicks a button:

```
<!DOCTYPE html>
<html>
<head>
	<title>Event Example</title>
</head>
<body>

<h1 id="id1">My Heading 1</h1>

<button type="button"
onclick="document.getElementById('id1').style.color='red'">
Click Me!</button>

</body>
</html>
```

Visibility:

```
<!DOCTYPE html>
<html>
<head>
	<title>Visibility Example</title>
</head>
<body>

<p id="p1">This is a text.</p>

<input type="button" value="Hide text"
onclick="document.getElementById('p1').style.visibility='hidden'">
<input type="button" value="Show text"
onclick="document.getElementById('p1').style.visibility='visible'">

</body>
</html>
```

# DOM Events

###Reacting to Events

A JavaScript can be executed when an event occurs, like when a user clicks on an HTML element.

To execute code when a user clicks on an element, add JavaScript code to an HTML event attribute:

`onclick=JavaScript`

Example of HTML events:

* When a user clicks the mouse
* When a web page has loaded
* When an image has been loaded
* When the mouse moves over an element
* When an input field is changed
* When an HTML form is submitted
* When a user strokes a key

In this example, the content of `<h1>` element is changed when a user clicks on it:

```
<!DOCTYPE html>
<html>
<head>
	<title>Click Event Example</title>
</head>
<body>

<h1 onclick="this.innerHTML='H1 is clicked!'">Click on this text!</h1>

</body>
</html>
```

In this example, a function is called from the event handler:

```
<!DOCTYPE html>
<html>
<head>
	<title>Event Handler Example</title>
</head>
<body>

<h1 onclick="changeText(this)">Click on this text!</h1>

<script>
function changeText(id) {
	id.innerHTML = "The element has been changed!";
}
</script>

</body>
</html>
```

### HTML Event Attributes

To assign events to HTML elements you can use event attributes.

In this example, an onclick event is assigned to a button element with a function named displayDate:

`<button onclick="displayDate()">Try it</button>`

### Assign Events Using the HTML DOM

The HTML DOM allows you to assign events to HTML elements using JavaScript:

```
<script>
document.getElementById("myBtn").onclick = displayDate;
</script>
```

### The onload and onunload Events

The onload and onunload events are triggered when the user enters or leaves the page.

The onload event can be used to check the visitor's browser type and browser version, and load the proper version of the web page based on the information.

The onload and onunload events can be used to deal with cookies.

`<body onload="checkCookies()">`

### The onchange Event

The onchange event are often used in combination with validation of input fields.

Below is an example of how to use the onchange. The upperCase() function will be called when a user changes the content of an input field.

`<input type="text" id="fname" onchange="upperCase()">`

### The onmouseover and onmouseout Events

The onmouseover and onmouseout events can be used to trigger a function when the user mouses over, or out of, an HTML element.

### More Examples

* `onmousedown` - triggered when mouse button is clicked
* `onmouseup` - triggered when the mouse button is released
* `onclick` - triggered when the mouse click is completed

# DOM EventListener

### The addEventListener() method

Add an event listener that fires when a user clicks a button:

`document.getElementById("myBtn").addEventListener("click", displayDate);`

The addEventListener() method attaches an event handler to an element without overwriting existing event handlers.

* You can add many event handlers to one element.
* You can add many event handlers of the same type to one element, i.e. two "click" events.
* You can add event listeners to any DOM object not only HTML elements. i.e. the window object.
* The addEventListener() method makes it easier to control how the event reacts to bubbling.

When using the addEventListener() method, the JavaScript is separated from the HTMl markup, for better readability and allows you to add event listeners even when you do not control the HTML markup.

You can easily remove an event listener by using the removeEventListener() method.

### Syntax

`element.addEventListener(event, function, useCapture)`

* The first parameter is the type of the event (like "click" or "mousedown")
* The second parameter is the function we want to call when the event occurs
* The third parameter is a boolean value specifying whether to use event bubbling or even capturing. This parameter is optional.

Note that you don't use the "on" prefix for the event; use "click" instead of "onclick".

### Add an Event Handler to an Element

Alert "Hello World!" when the user clicks on an element:

`element.addEventListener("click", function(){ alert("Hello World!"); });`

You can also refer to an external "named" function:

```
element.addEventListener("click", myFunc);

function myFunc() {
	alert("Hello World!");
}
```

### Add Many Event Handlers to the Same Element

The addEventListener() method allows you to add many events to the same element, without overwriting existing events:

```
element.addEventListener("click", myFunction);
element.addEventListener("click", mySecondFunction);
```

You can add events of different types to the same element:

```
element.addEventListener("mouseover", myFunction);
element.addEventListener("click", mySecondFunction);
element.addEventListener("mouseout", myThirdFunction);
```
### Add an Event Handler to the Window Object

The addEventListener() method allows you to add event listeners on any HTML DOM object such as HTML elements, the HTML document, the window ojbect, or other object that supports events, like the xmlHttpRequest object.

Add an event listener that fires when a user resizes the window:
```
window.addEventListener("resize", function(){
	document.getElementById("demo").innerHTML = sometext;
});
```

### Passing Parameters

When passing parameter values, use an "anonymous function" that calls the specified function with the parameters:

```
element.addEventListener("click", function(){
	myFunction(p1, p2);
});
```

### Event Bubbling or Event Capturing

There are two ways of event propagation in the HTML DOM, bubbling and capturing.

Event propagation is a way of defining the element order when an event occurs. If you have a <p> element inside a <div> element, and the user clicks on the <p> element, which element's "click" event should be handled first?

In bubbling the inner most element's event is handled first and then the outer: the <p> element's click event is handled first, then the <div> element's click event.

In capturing the outer most element's event is handled first and then the inner: the <div> element's click event will be handled first, then the <p> element's click event.

With the addEventListener() method you can specify the propagation type by using the "useCapture" parameter:

addEventListener(event, function, useCapture);
The default value is false, which will use the bubbling propagation, when the value is set to true, the event uses the capturing propagation.

```
document.getElementById("myP").addEventListener("click", myFunction, true);
document.getElementById("myDiv").addEventListener("click", myFunction, true);
```

### The removeEventListener() method

The removeEventListener() method removes event handlers that have been attached with the addEventListener() method:

`element.removeEventListener("mousemove", myFunction);`

# DOM Navigation

### Node

A node is a basic unit used in computer science. Nodes are devices or data points on a larger network. Devices such as a personal computer, cell phone, or printer are nodes. When defining nodes on the internet, a node is anything that has an IP address. Nodes are individual parts of a larger data structure, such as linked lists and tree data structures. Nodes contain data and also may link to other nodes. Links between nodes are often implemented by pointers.

### Nodes and trees

Nodes are often arranged into tree structures. These structures are binary trees.

A node represents the information contained in a single structure. These nodes may contain a value or condition, or possibly serve as another independent data structure. Nodes are represented by a single parent node. The highest point on a tree structure is called a root node, which does not have a parent node, but serves as the parent or 'grandparent' of all of the nodes below it in the tree. The height of a node is determined by the longest path from root node to the furthest leaf node, and the height of the tree is equal to the height of the root node. Node depth is determined by the distance between that particular node and the root node. The root node is said to have a depth of zero. Data can be discovered along these network paths. An IP address uses this kind of system of nodes to define its location in a network.

Definitions

* Child: A child node is a node extending from another node. For example, a computer with internet access could be considered a child node of a node representing the internet. The inverse relationship is that of a parent node. If node C is a child of node A, then A is the parent node of C.
* Degree: the degree of a node is the number of children of the node.
* Depth: the depth of node A is the length of the path from A to the root node. The root node is said to have depth 0.
* Edge: the connection between nodes.
* Forest: a set of trees.
* Height: the height of node A is the length of the longest path through children to a leaf node.
* Internal node: a node with at least one child.
* Leaf node: a node with no children.
* Root node: a node distinguished from the rest of the tree nodes. Usually, it is depicted as the highest node of the tree.
* Sibling nodes: these are nodes connected to the same parent node.

### DOM Nodes

According to the W3C HTML DOM standard, everything in an HTML document is a node:

* The entire document is a document node
* Every HTML element is an element node
* The text inside HTML elements are text nodes
* Every HTML attribute is an attribute node
* All comments are comment nodes

Node Types

Different W3C World Wide Web Consortium node types and descriptions:

* Document - represents the entire document (the root-node of the DOM tree)
* DocumentFragment - represents a "lightweight" Document object, which can hold a portion of a document
* DocumentType - provides an interface to the entities defined for the document
* ProcessingInstruction - represents a processing instruction
* EntityReference - represents an entity reference
* Element - represents an element
* Attr - represents an attribute
* Text - represents textual content in an element or attribute
* CDATASection - represents a CDATA section in a document (text that will NOT be parsed by a parser)
* Comment - represents a comment
* Entity - represents an entity
* Notation - represents a notation declared in the DTD

### Node Relationships

The nodes in the node tree have a hierarchical relationship to each other. The terms parent, child, and sibling are used to describe the relationships.

* In a node tree, the top node is called the root (or root node)
* Every node has exactly one parent, except the root (which has no parent)
* A node can have a number of children
* Siblings (brothers or sisters) are nodes with the same parent

```
<html>
    
  <head>
    <title>DOM Tutorial</title>
  </head>

  
  <body>
    <h1>DOM Lesson one</h1>
    <p>Hello world!</p>
  </body>

</html>


//Visual Notation

Root element     parentNode
  <html><-----------------+
    |                     |
    |                     |
    |                     |                   
    |   firstChild        |              ---+ childNodes to <html>
    +----------------->Element:             | and sibligs to each other
    |                  |<head>^             |
    |                  |      |             |
    |          nextsibling  previoussibling |
    |                  |      |             |
    |                  |      |             |
    |   lastChild      ^      |             |
    +----------------->Element:             |
                        <body>              |
                                         ---+
```

From the HTML above you can read:

* `<html>` is the root node
* `<html>` has no parents
* `<html>` is the parent of `<head>` and `<body>`
* `<head>` is the first child of `<html>`
* `<body>` is the last child of `<html>`

and:

* `<head>` has one child: `<title>`
* `<title>` has one child (a text node): "DOM Tutorial"
* `<body>` has two children: `<h1>` and `<p>`
* `<h1>` has one child: "DOM Lesson one"
* `<p>` has one child: "Hello world!"
* `<h1>` and `<p>` are siblings

### Navigating Between Nodes

You can use the following node properties to navigate between nodes with JavaScript:

* `parentNode`
* `childNodes[nodenumber]`
* `firstChild`
* `lastChild`
* `nextSibling`
* `previousSibling`

### Text Node

In this example: <title>DOM Tutorial</title>, the element node <title> does not contain text. It contains a `text node` with the value "DOM Tutorial".

The value of the text node can be accessed by the node's `innerHTML` property, or the `nodeValue`.

###Child Nodes and Node Values

In addition to the `innerHTML` property, you can also use the `childNodes` and `nodeValue` properties to get the content of an element.

The following example collects the node value of an <h1> element and copies it into a <p> element:

```
<!DOCTYPE html>
<html>
<head>
	<title>Node Example</title>
</head>
<body>

<h1 id="intro">My First Page</h1>
<p id="demo">Hello!</p>

<script>
var myText = document.getElementById("intro").childNodes[0].nodeValue;
document.getElementById("demo").innerHTML = myText;
</script>

</body>
</html>
```

For the above example, using `firstChild` property is the same as using `childNodes[0]`.

### DOM Root Nodes

There are two special properties that allow access to the full document:

* `document.body` - The body of the document
* `document.documentElement` - The full document

### The nodeName Property

The nodeName property specifies the name of a node:

* nodeName is read-only
* nodeName of an element node is the same as the tag name
* nodeName of an attribute node is the attribute name
* nodeName of a text node is always #text
* nodeName of the document node is always #document

Note: nodeName always contains the uppercase tag name of an HTML element.

### The nodeValue Property

The nodeValue property specifies the value of a node:

* nodeValue for element node is undefined
* nodeValue for text nodes is the text itself
* nodeValue for attribute nodes is the attribute value

### The nodeType Property

The nodeType property returns the type of node. nodeType is read-only.

The most important node types are:

```
Element type                           NodeType
-----------------------------------------------------------------------
Element                                1
Attribute                              2
Text                                   3
Comment                                8
Document                               9
```

# DOM Nodes

# DOM Nodelist
