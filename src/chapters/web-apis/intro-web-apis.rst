.. index:: ! API, ! application programming interface, ! web API, REST

Web APIs
========

An **API**, or **application programming interface**, is a set of rules that allow one application to communicate with another application. **Web APIs** 
are how applications communicate with other applications over a network. Throughout the remainder of this chapter, we will explore web APIs and a pattern 
for organizing them called REST. REST is an application design pattern, not unlike MVC. **REST**, however, relies on an abstract concept called 
*application state* that we'll cover in more detail on the following pages.
Here, we dive into what differentiates all web APIs from MVC applications.

MVC Without the V
-----------------

Web APIs are actually similar to MVC web applications but for one major distinction: Web APIs are not concerned with the presentation of data. A web API 
encompasses the model and controller aspects of MVC, but is not responsible for the view layer. In a web API, the view, or presentation of data, is decoupled 
from the model and controller that manage and transfer data. This separation leads to the development of two different applications, a client (front-end)
and a web API (back-end). 

The separation between client and web API provides the following benefits:

- Client applications can be developed to operate on a range of platforms (web, mobile, CLI, GUI, etc).
- Client and web API applications can be developed by different, specialized programming teams.
- Client and web API applications can be hosted on separate infrastructure.

.. admonition:: Note

   Client applications involve User Interface (UI) and User Experience (UX) development.

Client Interacts With Data
^^^^^^^^^^^^^^^^^^^^^^^^^^

Despite being separated from each other, the client application still relies on interactions with application data through the web API. A front-end client 
must ultimately present data to an end-user. This means the client must request a representation of the data from the web API. After the client receives the 
representation, it is parsed, styled and rendered to the user. 

.. admonition:: Note

   A web API interacts with, or *is consumed by*, a client application. This process involves transferring data representations and instructions 
   like creating, reading, updating and deleting.

Responsibilities of a Web API
-----------------------------

The chief responsibility of a web API is to exchange representations of data with a corresponding client application. APIs are also gatekeepers, maintaining 
rules about how end-users may interact with application data.

.. index:: ! server-side rendering, client-side rendering

Data Delivery
^^^^^^^^^^^^^

Think about how a view works in MVC. 

#. Data is injected into a template file, 
#. That template is rendered in HTML in the browser when a controller action method is invoked,
#. The data is sent back to the user

We call this approach **server-side rendering**. A client application and web API work in a similar way. However, instead of injecting the data into a 
template on the server, data is transferred over the network through AJAX requests made by the client.

When a client application receives data, it injects that data into its HTML using JavaScript. This all occurs from within a browser. This approach is 
called **client-side rendering** because the web API only sends data, the HTML is assembled on the user's end.

.. admonition:: Example

   Consider requesting the ``/events`` path of your MVC project. The response is an HTML presentation of the data. In other words, the 
   data is already included in the presentation.

   **MVC**: ``GET /events -> HTML with data``

   In a web API analog, an ``/events`` path would return just the underlying data. 

   **Web API**: ``GET /events -> just data``

   It is then the client application's responsibility to integrate the received data into its presentation.

Management of Data
^^^^^^^^^^^^^^^^^^

A web API manages data by modeling objects that line up with the underlying business data. This is actually the same process we saw in MVC. Our models 
are class files that drive the interactions in our codebase. Web APIs often take advantage of ORMs just like MVC applications do. If you have underlying 
classes that map to a database, you can easily make data available for use within a web API codebase.

Transference of Data
^^^^^^^^^^^^^^^^^^^^

Beyond managing data, a web API also handles transferring data. A client application will make a request for some data. Our web API must contain controller 
files that can handle the requests. As a part of handling the request, the controller file must understand the request, access the requested data, package 
the data in an accepted format, and send the package as a response to the client application.

.. _client-api-transfer:

Here's an overview of the steps to transfer data between a web API and client application:

#. A request for data comes from a client application to the API.
#. A controller file in the API catches the request.
#. The controller determines if the request is valid.
#. The controller transfers data from the database to an object, via the ORM.
#. The controller transforms the object into a package the client application can work with.
#. The controller responds to the client with the packaged data.


.. index:: ! data presentation, ! data representation

Representation of Data
----------------------

Presentation vs Representation
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

As mentioned above, the client application presents the data to the end-user. However, the client relies on consuming a representation of data from the 
web API. **Presentation** is the rendered combination of data and visual styling intended for end-users. The client application needs to know what format the 
data is in so that it can be transformed into a human readable presentation (HTML/CSS). A web API packages data into a format the client application 
accepts. This format is called the **representation** of the data. The client application team and the web API team must agree to the underlying data format. 
A best practice is to use a universal representation widely accepted by client applications.

Universal Representation
^^^^^^^^^^^^^^^^^^^^^^^^

It is necessary to adopt a universal representation because web APIs and client applications may be written in two different programming languages. Your 
web API may be written in C#/ASP.NET but the client application may be written using JavaScript and React. While there are many languages and frameworks 
available in web development, they all support the creation and parsing of JSON. JSON is a standard in web development because it is simple to process in 
any language, compatible with HTTP, and seamlessly represents the structure of data objects.

JSON
~~~~

JSON is currently a universal representation of data accepted by client applications. This means our web API packages data 
requested by a client application as JSON. The web API also transfers this JSON in its communication with a client application.

Let's revisit the last two steps from our web API work flow :ref:`above <client-api-transfer>`:

5. The controller transforms the object into a JSON representation.
6. The controller responds to the client with the JSON representation.

.. admonition:: Tip

   `XML <https://developer.mozilla.org/en-US/docs/Web/XML/XML_introduction>`_ is another popular data format. It is now used less commonly than 
   JSON for web API-to-client communications.

In the next section, we will discuss exactly how a client application makes a request and how a web API responds.

.. index:: ! state

HTTP as The Language of Web APIs
--------------------------------

HTTP is the protocol used for communication between a web API and a client application. Web APIs communicate over a network. The most common protocol of 
the internet is HTTP, so it comes as no surprise that HTTP is the language of web APIs. Similarly, our MVC applications use HTTP as the protocol for an 
end-user to access the application. HTTP also facilitates the communication between a client application and a web API.

.. admonition:: Tip

   We will refer to web APIs as APIs going forward, since the web prefix is implied.

Here's a refresher on `the basics of HTTP <https://education.launchcode.org/intro-to-professional-web-dev/chapters/http/index.html>`__:

- Is a stateless request/response protocol.
- Requests and responses may include HTTP bodies.
- Responses always contain a three digit HTTP status code.
- Requests and responses always include HTTP headers.


We call HTTP a *stateless protocol*. State can be a complex concept that refers to a number of things. We'll explore some aspects of it in more depth on the 
next page. In the context of HTTP, think of **state** as information about application data that is transferred via HTTP bodies, HTTP status codes, 
and HTTP headers.

Bodies
^^^^^^

An HTTP body can contain a large number of different media types, 
known as `MIME types <https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/MIME_types/Common_types>`_. A MIME type is associated with the 
HTTP header ``Content-Type``. This header instructs the recipient of the HTTP request/response on what MIME type the HTTP body contains. We've seen a 
``Content-Type: text/html`` HTTP header before. Here's a simple example of it:

.. sourcecode:: html
   :linenos:

   <!DOCTYPE html>
   <html>
      <head>
         <title>My Web Page</title>
         content
      </head>
      <body>
         content
      </body>
   </html>

This is the header for HTML documents and is used throughout the web. APIs send representations of data in the format of JSON requiring the header 
``Content-Type`` to be ``application/json``. This allows us to pass the state of the data as the HTTP body.

.. sourcecode:: json
   :linenos:

   {
      "title": "An Astronaut's Guide to Life on Earth",
      "author": "Chris Hadfield",
      "ISBN": 9780316253017,
      "year_published": 2013,
      "subject": ["Hadfield, Chris", "Astronauts", "Biography"],
      "available": true
   }

The HTTP body may include JSON that represents the data being passed between an API and client application. Remember, not all requests/responses include 
HTTP bodies.

Status Codes
^^^^^^^^^^^^

The next HTTP component that transfers state is the HTTP status code. The HTTP status code is included as a part of every HTTP response. The status code 
is the API's way of telling the client application how their initial request was handled. 
`HTTP response status codes <https://developer.mozilla.org/en-US/docs/Web/HTTP/Status>`_ are a part of the HTTP spec and their usage goes beyond API 
design. However, many of their codes have been adopted as a standard within API design.

.. list-table:: Common HTTP status codes in API design
   :widths: 25 20 60
   :header-rows: 1

   * - Status Code Group
     - Commonly Used
     - Description
   * - 2XX
     - 200, 201, 204
     - request was successful 
   * - 3XX
     - 301, 302
     - request was redirected
   * - 4XX
     - 400, 401, 403, 404, 405
     - client error
   * - 5XX
     - 500, 502, 504
     - server error

Headers
^^^^^^^

The final HTTP component that transfers state are the HTTP headers. Any `number of headers <https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers>`_ 
can be included in a request or response. We saw the ``Content-Type`` header above. This is the header that informs the API (request header) or client 
application (response header) of the format of the data included in the body. 

.. admonition:: Tip

   A client can specify which ``Content-Type`` they want to receive in the API response using the ``Accept`` request header.

API Design
----------

The design of an API is a contract that defines how the client and API interact with data. The API is responsible for upholding the data management and 
transfer behaviors of the contract. The client application is responsible for consuming (via AJAX requests) an API according to the contract.

As long as both sides of the interface (the client and API logic) uphold the contract, then front and back-end teams can operate independently. This 
provides the following freedoms:

- Front-end developers can choose, or change, the internal styling, libraries, frameworks and design patterns.
- Back-end developers can choose, or change, the internal server language, libraries, frameworks and design patterns.
- Both sides can choose, or change, their external hosting infrastructure at any time without affecting the other.
- Both sides can make and deploy changes to their code bases at any time, without needing to coordinate with, or wait for, the other.

Only when a change must be made to either the client AJAX requests or API behavior do the two teams need to communicate and agree upon a new contract. Up next,
we discuss how following the REST pattern of API design offers consistency and simplicity in application development.

Check Your Understanding
------------------------

.. admonition:: Question

   True or False: Web API programmers must be knowledgeable in HTML/CSS/Javascript to create a client application.

   a. True

   b. False

.. ans: b, An API is view-agnostic so its programmers are not responsible for creating a corresponding client application.

.. admonition:: Question

   Match the class of HTTP response codes to the approximate definition:

   ``2XX``, ``3XX``, ``4XX``, ``5XX``

   a. Request is valid, but server cannot receive and accept it.

   b. Request received and accepted.

   c. Due to the request containing an error, it cannot be received.

   d. Another action needs to be done to fulfill request.


.. ans: 2xx: b. Request received and accepted, 3xx: d. Another action needs to be done to fulfill request., 4xx: c. Due to the request containing an error, it cannot be received., 5xx: a. Request is valid, but server cannot receive and accept it.
