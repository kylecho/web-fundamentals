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

# DOM Events

# DOM EventListener

# DOM Navigation

# DOM Nodes

# DOM Nodelist
