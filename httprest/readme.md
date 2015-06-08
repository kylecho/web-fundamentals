#HTTP and REST [Link](http://code.tutsplus.com/tutorials/a-beginners-introduction-to-http-and-rest--net-16340)

**Please note that I have omitted considerable amount of sections related to the example application using PHP.**

###REST

REST is a simple way to organize interactions between idependent systems. This has inspired the design of services like the Twitter API due to the fact that REST allows you to interact with minimal overhead with clients as diverse as mobile phones and other websites. REST is not tied to the web, but it was inspired by HTTP. As a result, REST can be used whenever HTTP can.

###HTTP

HTTP is the protocol that allows for sending documents back and forth on the web. A protocol is a set of rules that determines which messages can be exchanged, and which messages are appropriate replies to others.

In HTTP, there are two roles: server and client. In general, the client always initiates the conversation; the server replies. HTTP is text based. Text usage makes it easy to monitor an HTTP exchange.

HTTP messages are made of a header and a body. The body can often remain empty; it contains data that you want to transmit over the network. The header contains metadata, such as encoding information. However, in the case of request, it also contains the important HTTP methods. In the REST style, you will find that header data is often more significant than the body.

###cURL

A helpful way to familiarize yourself with HTTP is to use a dedicated client, such as cURL. cURL is a command line tool that is available on all major operating systems.

`curl -v google.com`

This will display the complete HTTP conversation. Requests are preceded by `>`, while responses are preceded by `<`.

```
* Rebuilt URL to: google.com/
* Hostname was NOT found in DNS cache
*   Trying 74.125.137.100...
* Connected to google.com (74.125.137.100) port 80 (#0)
> GET / HTTP/1.1
> User-Agent: curl/7.37.1
> Host: google.com
> Accept: */*
>
< HTTP/1.1 301 Moved Permanently
< Location: http://www.google.com/
< Content-Type: text/html; charset=UTF-8
< Date: Mon, 08 Jun 2015 21:13:16 GMT
< Expires: Wed, 08 Jul 2015 21:13:16 GMT
< Cache-Control: public, max-age=2592000
* Server gws is not blacklisted
< Server: gws
< Content-Length: 219
< X-XSS-Protection: 1; mode=block
< X-Frame-Options: SAMEORIGIN
< Alternate-Protocol: 80:quic,p=0
<
<HTML><HEAD><meta http-equiv="content-type" content="text/html;charset=utf-8">
<TITLE>301 Moved</TITLE></HEAD><BODY>
<H1>301 Moved</H1>
The document has moved
<A HREF="http://www.google.com/">here</A>.
</BODY></HTML>
* Connection #0 to host google.com left intact
```

###URLS

Each URL identifies a resource. A web page is a type of resource. Consider the example which manages the list of a company's client:

`/clients`

will identify all clients while:

`client/jim`

will identify the client, named "Jim".

In these examples, we did not include the hostname in the URL. However, the hostname is important to ensure that the resource identifier is unique. We often say you send the request for a resource to a host. The host is included in the header separately from the resource path, which comes right on top of the request header:


```
GET /clients/jim HTTP/1.1

Host: example.com
```

Resources are best thought of as nouns. For example, the following is not RESTful:

`/clients/add`

This is because it uses a URL to describe an action. This is a fundamental point in distinguishing RESTful from non-RESTful systems.

URLs should be as precise as needed. This way, URLs act as a complete map of all the data your application handles.

But how do you specify an action? For example how do you tell you want a new client record created instead of retrieved? That is where HTTP verbs come into play.

###HTTP Verbs

Each request specifies a certain HTTP verb, or method, in the request header.

`GET / HTTP/1.1`

means the `GET` method is being used, while:

`DELETE /clients/anne HTTP/1.1`

means the `DELETE` method is being used.

HTTP verbs tell the server what to do with the data identified by the URL. The request can optionally contain additional information in its body, which might be required to perform the operation - for instance, data you want to store with the resource. You can supply this data in cURL with the `-d` option.

If you'd ever created HTML forms, you'll be familiar with two of the most important HTTP verbs: `GET` and `POST`. But there are far more HTTP verbs available. The most important ones for building RESTful API are `GET`, `POST`, `PUT`, and `DELETE`. Other methods are available, such as `HEAD` and `OPTIONS`, but they are more rare. See documentation at [IETF](http://www.ietf.org/rfc/rfc2616.txt).

####GET

`GET` is the simplest type of HTTP request method; the one that browsers use each time you click a link or type a URL into the address bar. It instructs the server to transmit the data identified by the URL to the client. Data should never be modified on the server side as a result of a `GET` request. In this sense, a `GET` request is read-only, but of course, once the client receives the data, it is free to do any operation with it on its own side - for instance, format it for display.

####PUT

A `PUT` request is used when you wish to create or update the resource identified by the URL. For example:

`PUT /clients/robin`

This might create a client, called `Robin` on the server. You will notice that `REST` is completely backend agnostic; there is nothing in the request that informs the server how the data should be created - just that it should. This allows you to easily swap the backend technology if the need should arise. `PUT` requests contain the data to use in updating or creating the resource in the body. In cURL, you can add data to the request with the `-d` switch.

`curl -v -X PUT -d "some text"`

####DELETE

`DELETE` should perform the contrary of `PUT`. It should be used when you want to delete the resource identified by the URL of the request.

`curl -v -X DELETE /clients/anne`

This will delete all data associated with the resource, identified by `/clients/anne`.

####POST

`POST` is used when the processing you wish to happen on the server should be repeated, if the `POST` request is repeated. In addition, `POST` requests should cause processing of the request body as a subordinate of the URL you are posting to.

In plain words:

`POST /clients/`

This should not cause the resouce at `/clients/` itself to be modified, but a resource whose URL starts with `/clients/`. For instance, it should append a new client to the list, with an `id` generated by the server.

`/clients/some-unique-id`

`PUT` requests are used easily instead of `POST` requests, and vice versa. Some systems use only one, some use `POST` for create operations, and `PUT` for update operations, some even use `POST` for updates and `PUT` for creates.

Often, `POST` requests are used to trigger operations on the server, which do not fit into the `Create/Update/Delete` paradigm.

###Classifying HTTP Methods

####Safe and unsafe methods:

Safe methods are those that never modify resources. The only safe methods, from the four listed above is `GET`. The others are unsafe because they may result in a modification of the resources.

####Idempotent methods:

These methods achieve the same result, no matter how many times the request is repeated: they are `GET`, `PUT`, and `DELETE`. The only non idempotent method is `POST`.

`PUT` and `DELETE` being considered idempotent might be surprising, though it is quite easy to explain: repeating a `PUT` method with exactly the same body should modify a resource in a way that it remains identical to the one described in the previous `PUT` request. Nothing will change. Similarly, it makes no sense to delete a resource twice. It follows that no matter how many times a `PUT` or `DELETE` request is repeated, the result should be the same as if it had been done only once.

###Representations

We can sum up what we have learned so far in the following way: the HTTP client and HTTP server exchange information about resources identified by URLs.

We say that the request and response contain a representation of the resource. By representation, we mean information, in a certain format, about the state of the resource or how that state should be in the future. Both the header and the body are pieces of the representation.

The HTTP headers, which contain metadata, are tightly defined by the HTTP spec; they can only contain plain text, and must be formatted in a certain manner.

The body can contain data in any format, and this is where the power of HTTP truly shines. You know that you can send plain text, pictures, HTML, and XML in any human language. Through request metadata or different URLs, you can choose between different representations for the same resource. For example, you might send a webpage to browsers and JSON to applications.

The HTTP response should specify the content type of the body. This is done in the header, in the Content-Type field; for instance:

`Content/Type: application/json`

For simplicity, our example application only sends JSON back and forth, but the application should be architectured in such a way that you can easily change the format of the data, to tailor for different clients or user preferences.

###HTTP Client Libraries

To experiment with the different request methods, you need a client, which allows you to specify which method to use. Unfortunately, HTML forms do not fit the bill, as they only allow you to make GET and POST requests. In real life, APIs are accessed programmatically through a separate client application, or through JavaScript in the browser.

This is the reason why, in addition to the server, it is essential to have good HTTP client capabilities available in your programming language of choice.

A very popular HTTP client library is, again, cURL. You've already been familiarized with the cURL command from earlier in this tutorial. cURL includes both a standalone command line program, and a library that can be used by various programming languages. In particular, cURL is, more often than not, the HTTP client solution of choice for PHP developers. Other languages, such as Python, offer more native HTTP client libraries.

###Response Codes

Headers contain all sort of meta information; for example, the text encoding used in the message body or the MIME type of the body's content. In this case, we are explicitly specifying the HTTP response codes. HTTP response codes standardize a way of informing the client about the result of its request. By default, PHP returns a 200 response code, which means that the response is successful.

The server should return the most appropriate HTTP response code; this way, the client can attempt to repair its errors, assuming there are any. Most people are familiar with the common 404 Not Found response code, however, there are a lot more available to fit a wide variety of situations.

Keep in mind that the meaning of a HTTP response code is not extremely precise; this is a consequence of HTTP itself being rather generic. You should attempt to use the response code which most closely matches the situation at hand. That being said, do not worry too much if you cannot find an exact fit.

Here are some HTTP response codes, which are often used with REST:

* 200 OK - This response code indicates that the request was successful.
* 201 Created - This indicates the request was successful and a resource was created. It is used to confirm success of a PUT or POST request.
* 400 Bad Request - The request was malformed. This happens especially with POST and PUT requests, when the data does not pass validation, or is in the wrong format.
* 404 Not Found - This response indicates that the required resource could not be found. This is generally returned to all requests which point to a URL with no corresponding resource.
* 401 Unauthorized - This error indicates that you need to perform authentication before accessing the resource.
* 405 Method Not Allowed - The HTTP method used is not supported for this resource.
* 409 Conflict - This indicates a conflict. For instance, you are using a PUT request to create the same resource twice.
* 500 Internal Server Error - When all else fails; generally, a 500 response is used when processing fails due to unanticipated circumstances on the server side, which causes the server to error out.

###Conclusion

It's important to remember that HTTP was conceived to communicate between systems, which share nothing but an understanding of the protocol. In general, the less assumptions beyond HTTP you make, the better: this allows the widest range of programs and devices to access your API.

Beyond PHP, you might consider the following:

The various Ruby frameworks ([Rails](http://rubyonrails.org/) and [Sinatra](http://www.sinatrarb.com/))
There's excellent REST support in Python. Plain [Django](http://www.djangoproject.com/) and [WebOb](http://pythonpaste.org/webob), or [Werkzeug](http://werkzeug.pocoo.org/) should work
[node.js](http://nodejs.org/) has excellent support for REST
