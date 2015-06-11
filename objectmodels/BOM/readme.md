#The Browser Object Model [Link](http://www.w3schools.com/js/js_window.asp)

The Browser Object Model (BOM) allows JavaScript to "talk to" the browser. There are no official standards for the Browser Object Model.

###The Window Object

* The `window` object is supported by all browsers. It represents the browser's window.
* All global Javascript object, functions, and variables automatically become members of the window object.
* Global variables are properties of the window object.
* Global functions are methods of the window object.
* Even the document object (of the HTML DOM) is aproperty of the window object: `window.document.getElementById("header");`
* is the same as: `document.getElementById("header");`

###The Global Scope

###Window Relationships and Frames

###Window Position

###Window Size

Three different properties can be used to determine the size of the browser window (the browser viewport, NOT including toolbars and scrollbars).

For IE, Chrome, Firefox, Opera, and Safari:

* `window.innerHeight` - the inner height of the browser window
* `window.innerWidth` - the inner width of the browser window
* `window.open()` - open a new window
* `window.close()` - close the current window
* `window.moveTo()` - move the current window
* `window.resizeTo()` - resize the current window

###Navigating and Opening Windows

###Intervals and Timeouts

With JavaScript, it is possible to execute some code at specified time-intervals. This is called timing events.

* `window.setInterval(callback, millisecond)` - will wait a specified number of milliseconds, and then execute a specified function, and it will continue to execute the function, once at every given time-interval.

* `window.setTimeout(callback, millisecond)` - will wait the specified number of milliseconds, and then execute the specified function.

* `window.clearInterval()` - is used to stop further executions of the function specified either in the setInterval() method or setTimeout().

It is preferred using setTimeout instead of setInterval.

###System Dialogs

JavaScript has three kind of popup boxes: Alert box, Confirm box, and Prompt box.

* `window.alert()` - used if you want to make sure information comes through to the user.
* `window.confirm()` - used if you want the user to verify or accept something. If the user clicks "OK", the box returns true, or if the user clicks "Cancel", the box returns false
* `window.prompt()` - used if you want the user to input a value before entering a page.

###The Location Object

The `window.location` object can be used to get the current page (URL) and to redirect the browser to a new page.

* `window.location` - object can be written without the window prefix.
* `window.location.href` - returns the href (URL) of the current page
* `window.location.hostname` - returns the domain name of the web host
* `window.location.pathname` - returns the path and filename of the current page
* `window.location.protocol` - returns the web protocol used (http:// or https://)
* `window.location.assign` - loads a new document

###Query String Arguments

###Manipulating the Location



#The Navigator Object

The `window.navigator` object contains information about the visitor's browser.

The `window.navigator` object can be written without the window prefix.

Some examples:

* `navigator.appName` - returns the name of the browser
* `navigator.appCodeName` - returns the codename of the browser
* `navigator.platform` - returns the platform of the browser (operating system)
* `navigator.cookieEnabled` - returns true if cookies are enabled, otherwise false
* `navigator.product` - returns the product of the browser
* `navigator.appVersion` - returns version information about the browser
* `navigator.userAgent` - returns version information about the browser
* `navigator.language` - returns the browser's language
* `navigator.javaEnabled()` - returns true if Java is enabled

###Ditecting Plug-ins

###Registering Handlers



#The Screen Object

The `window.screen` object contains information about the user's screen.

The `window.screen` object can be written without the window prefix.

Properties:

* `screen.width` - returns the width of the visitor's screen in pixels.
* `screen.height` - returns the height of the visitor's screen in pixels.
* `screen.availWidth` - returns the width of the visitor's screen, in pixels, minus interface features like the Windows Taskbar.
* `screen.availHeight` - returns the height of the visitor's screen, in pixels, minus interface features like the Windows Taskbar.
* `screen.colorDepth` - returns the number of bits used to display one color. All modern computers use 24 bit or 32 bit hardware for color resolution.
* `screen.pixelDepth` - returns the pixel depth of the screen. For modern computers, Color Depth and Pixel Depth are equal.

#The History Object

The `window.history` object contains the browsers history.

The `window.history` object can be written without the window prefix. To protect the privacy of the users, there are limitations to how JavaScript can access this object.

Some methods:

* `history.back()` - same as clicking back in the browser
* `history.forward()` - same as clicking forward in the browser
