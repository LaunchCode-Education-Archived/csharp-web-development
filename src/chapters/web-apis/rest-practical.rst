REST: Practical Fundamentals
============================

Now that you have an understanding of the more abstract aspects of REST, let's turn our attention to the practical details. The previous article 
covered the following terms in great depth -- below is a practical summary:

   **State**: data that can change (transition) through interactions between an API and its client

   **Representation**: the convertible format that enables state to be transferred and used by the client and API

   **Resource**: the representation of a type of state (as an entity or collection) that the API exposes to its client for interaction

   **Entity**: a single resource that is uniquely identifiable in a collection

   **Collection**: entities of the same resource type treated as a whole

Shapes
------

Shape describes the input or output of an API in terms of its fields and data types. There are no rules for how shapes should be defined. However, the 
goal should be to describe shapes in a way that is easy to understand. For this reason, shapes are typically shown in a way that is similar to the 
representation format. Because we use JSON as the representation format, the 
`JSON data types <https://json-schema.org/understanding-json-schema/reference/type.html>`_ are used. 

You can think of shape like a class definition in an object-oriented codebase:

.. admonition:: Example

   .. sourcecode:: csharp
		:linenos:

      public class CodingEvent {
         public int Id { get; set; }
         public string Title { get; set; }
         public string Description { get; set; }
         public DateTime Date { get; set; }
      }

	The output resource shape of a Coding Event

   .. sourcecode:: bash
		:linenos:

      CodingEvent {
         Id: integer
         Title: string
         Description: string
         Date: string (ISO 8601 date format)
      }

The JSON representation of the resource that the API sends out is then based on the shape. This is like how an object is based on the blueprint of its class:

Here's a Coding Event JSON Representation:


.. admonition:: Example
   
   .. sourcecode:: bash
		:linenos:

      {
         "Id": 1,
         "Title": "Halloween Hackathon!",
         "Description": "A gathering of nerdy ghouls to work on GitHub Hacktoberfest contributions",
         "Date": "2020-10-31"
      }

We can think of inputs as a *partial state* provided by the client during create and update operations. Only some of the fields are included because the 
API is responsible for providing the others.

Consider the following example of an input shape used to create an event. Notice that the ``Id`` field is not included:

.. admonition:: Example

   .. sourcecode:: bash
		:linenos:

      CodingEvent {
         Title: string
         Description: string
         Date: string (ISO 8601 date format)
      }

   Some of the common fields the API is responsible for managing:

   - the unique identifier (``Id``) 
   - the "created on" or "last updated" timestamp
   - links for relationships between resources

.. index:: ! endpoint

Endpoints
---------

An API **endpoint** refers to the HTTP path and method that defines the location of a resource and the action to take on its state.

Endpoints are what an API exposes to its consumers. Each endpoint is made up of a:

- **path**: the noun that identifies the resource
- **method**: the verb, or action, to take on the resource's state

Identifying the Resource
^^^^^^^^^^^^^^^^^^^^^^^^

Paths are used to identify the resource. Recall the hierarchal nature of resources where an entity only exists within a collection. RESTful APIs separate 
the resources they expose into one or more resource entry-points. As the name implies, these entry-points are the start of the hierarchy and identify 
each top-level resource collection.

Let's consider two resources exposed by a RESTful API:

.. admonition:: Example

   The Coding Events API would have the following familiar resources (among others):

   .. list-table:: Resource and corresponding collection entry-point

      * - Resource
        - ``CodingEvent``
        - ``Tag``
      * - Collection entry-point
        - ``/events``
        - ``/tags``

   The name of the path is arbitrary but should follow these rules of thumb to maintain consistency:

   - is lowercase and separated by underscores if necessary
   - adequately describes the resource in as few characters as necessary
   - is a noun (actions are described by the method of the endpoint)

Notice that the entry-points are pluralized. The pluralized path indicates that the state of the resource collection is the subject of the interaction. 

Consider a request to the following endpoint (path and method):

.. list-table:: Identify the Resource
   :header-rows: 1

   * - Path
     - Noun (subject)
   * - ``/collection``
     - Resource collection

.. list-table:: Interact with its State
   :header-rows: 1

   * - HTTP method
     - Verb (action)
   * - ``GET``
     - view representation of the collection

Let's see this in action with our Coding Events API. Using what we have learned so far, we can expect the state of the resource collection to be 
represented in a JSON array, ``[]``:

.. admonition:: Example

	Here is a response from a request to the GET ``/events`` endpoint:

   .. sourcecode:: bash
		:linenos:

      [
         CodingEvent { ... },
         ...
      ]

   The state of the ``CodingEvent`` collection is made up of the collective state of each ``CodingEvent`` entity within it.

.. admonition:: Example

	Here is a response from a request to the GET ``/tags`` endpoint:
   
   .. sourcecode:: bash
      :linenos:

      [
         Tag { ... },
         ...
      ]

   A request to the endpoint of the ``Tag`` collection would include its respective ``Tag`` entity representations (JSON objects).

Suppose we wanted to interact with an individual resource entity. We would need to identify it within its collection. 

The path to identify a resource entity would need to include:

- the collection identifier, or resource entry-point (``/collection``)
- the unique resource entity identifier (``/{entityId}``) within the collection

Because the unique identifier of the entity is variable, we use a path variable (``{entityId}``) to describe it in a generic way.

.. admonition:: Tip

   The hierarchy of collections and entities is similar to directories and files. To identify an entity is like identifying a file within a directory. 
	You need both the directory (collection) name and a sub-path that uniquely identifies the file (entity).

Consider a request to the following endpoint for viewing a single resource entity:

.. list-table:: Identify the Resource
   :header-rows: 1

   * - Path
     - Noun (subject)
   * - ``/collection/{entityId}``
     - Resource entity

.. list-table:: Interact with its State
   :header-rows: 1

   * - HTTP method
     - Verb (action)
   * - ``GET``
     - view representation of a single entity

Let's take another look at our example API:

.. admonition:: Example

   The generic path to identify a ``CodingEvent`` resource would be described as ``/events/{codingEventId}``.
   
   Let's assume a Coding Event exists with an ``Id`` of ``12``.
   
   We could make a request to the ``GET /events/12`` endpoint to read its current state and receive this response:

   .. sourcecode:: bash
		:linenos:

      {
         "Id": 12,
         "Title": "Halloween Hackathon!",
         "Description": "A gathering of nerdy ghouls...",
         "Date": "2020-10-31"
      }

CRUD Operations & HTTP Methods
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

   In a RESTful API the interactions a client takes on a Resource are described using HTTP methods

If the Resource path describes the **noun** (subject) the HTTP method describes the **verb** (action) that is taken on that subject's State. 

As we saw in the previous article, State is something that can be interacted using **CRUD** operations. *By convention*, each of these operations corresponds to an HTTP method:

.. list-table:: HTTP method and corresponding **CRUD** operation
   :stub-columns: 1

   * - HTTP method
     - ``POST``
     - ``GET``
     - ``PUT/PATCH*``
     - ``DELETE``
   * - CRUD operation
     - **C**\reate
     - **R**\ead
     - **U**\pdate
     - **D**\elete

The use case of an API dictates the design of its contract. This includes which actions the client can take on each Resource. In other words, **not every action must be exposed** for each Resource the API manages.

.. admonition:: note

   If a client tries to take an action on a Resource that is not supported by the API they will receive a ``405`` **status code** or ``Method not allowed`` error response.

Endpoint Behavior
=================

Depending on the endpoint the effect of the request can differ. In other words, the **behavior of an endpoint** is dependent on the subject -- an entity or the collection as a whole.

Operating On Collections
------------------------

.. list-table:: Endpoint behaviors for a Resource collection
   :stub-columns: 1

   * - HTTP method
     - ``POST``
     - ``GET``
     - ``PUT/PATCH``
     - ``DELETE``
   * - Behavior with Resource State
     - create a new entity in the collection
     - view the **current** list of all entities in the collection
     - bulk update of entities in the collection
     - remove all entities in the collection

.. admonition:: note

   Exposing the ability to modify or delete *all of the entities in a collection* at once can be risky. In many cases the design of a RESTful API will only support ``GET`` and ``POST`` endpoints for collections. 

Let's consider a request for creating a Resource entity. Recall that this operation acts on **the State of the collection** by adding a new entity to it.

The ``POST`` endpoint of the collection, that the entity belongs to, can be used with a **request body**. This request body is a **representation of the initial State** the client must provide as **an input** to the API. 

Let's take a look at this request in the context of our example API:

.. admonition:: example

   As we saw earlier, the *input shape* for creating a ``CodingEvent`` only **includes the fields the consumer is responsible for**. The ``Id`` field is then managed internally by the API.
   
   We refer to this shape as a ``NewCodingEvent`` to distinguish it from the ``CodingEvent`` Resource shape:

   .. sourcecode:: bash

      NewCodingEvent {
         Title: string
         Description: string
         Date: string (ISO 8601 date format)
      }

   We can describe this request in a shorthand. This shorthand includes the endpoint, input, and outputs:

      ``POST /events (NewCodingEvent) -> 201, CodingEvent``

   After sending this request the response would include:

   - a ``201``, or ``Created``, **status code**
   - a ``Location`` **response header**
   - the representation of the created Resource entity State (including an assigned ``Id`` field)

Operating On Entities
---------------------

.. list-table:: Endpoints behaviors for an individual Resource entity
   :stub-columns: 1

   * - HTTP method
     - ``POST``
     - ``GET``
     - ``PUT/PATCH``
     - ``DELETE``
   * - Behavior with Resource State
     - N/A (created inside a collection)
     - view the **current** entity State
     - update the entity State
     - remove the entity from the collection

.. admonition:: note

   **U**\pdating using ``PUT`` or ``PATCH`` in REST is a choice left to the API designer. This article has a great `breakdown of the subject <https://restfulapi.net/rest-put-vs-post/>`_.

   In this course we will follow the convention that ``PATCH`` is used to **U**\pdate the **State of a Resource entity**. 

When removing a Resource the client is requesting a **transition to an empty State**. This means that both the **request body** and **response body** that are transferred, *the representations of State*, are empty.

We can see this behavior in action with a request to the ``DELETE`` endpoint for a single Resource entity in our example API:

.. admonition:: example

   Let's once again assume a ``CodingEvent`` Resource exists with an ``Id`` of ``12``. If we want to remove this entity we need to issue a request to its **uniquely identified** ``DELETE`` endpoint:

      ``DELETE /events/12 -> 204``
   
   In this shorthand you can see that this request has an *empty request body*. This is the *empty State* we are requesting a transition to. 
   
   The ``204``, or ``No Content``, **status code** in the response indicates that the action was successful *and that the response body is empty*. The API transfers back a *representation of empty State* (no response body) to the client. 

.. admonition:: example

   What would happen if we made another request to the endpoint of a Resource entity that **doesn't exist**, ``DELETE /events/999``?

   We would receive a ``404``, or ``Not Found``, status code that lets us know the **request failed** because of a **client error** (providing an ``Id`` for a nonexistent Resource).

Headers & Status Codes
======================

Another aspect of a RESTful API dictates the usage of HTTP response status codes and HTTP request and response headers. 

Response status codes inform the client on if their request was handled successfully. The response status code and the attached message will include the information the client must change to fix the request.

HTTP headers are used to communicate additional information (**metadata**) about a request or response. We will explore some common HTTP headers and their usage in RESTful design.

Status Codes
------------

   Every RESTful API response includes a **status code** that indicates whether the client's request succeeded or failed

Success Status Codes
^^^^^^^^^^^^^^^^^^^^

When a request is successful the ``2XX`` status codes are used. These codes communicate to the consumer the **type of success** relative to the action that was taken. Below is a list of the common success codes you will encounter:

.. list-table:: Common client success status codes for each action
   :header-rows: 1
   :widths: 20 20 20 40

   * - HTTP method
     - Status code
     - Message
     - Response
   * - ``POST``
     - ``201``
     - ``Created``
     - Resource entity and ``Location`` header
   * - ``GET``
     - ``200``
     - ``OK``
     - Resource entity or collection
   * - ``DELETE``
     - ``204``
     - ``No Content``
     - empty response body

Failure Status Codes
^^^^^^^^^^^^^^^^^^^^

Requests can fail. A failed request is due to either the consumer or a bug in the API. Recall the status code groups that categorized the type of failure:

- **client error**: ``4XX`` status code group
- **server error**: ``5XX`` status code group

Server errors are **not something the consumer can control**. However, client errors indicate that the request can be **reissued with corrections**. Each of these status codes and messages notify the consumer of the changes needed for a success.

Let's look at some of the common client error status codes:

.. list-table:: Common client error status codes
   :header-rows: 1
   :widths: 20 30 50

   * - Status code
     - Message
     - Correction
   * - ``400``
     - ``Bad Request``
     - Client must fix errors in their request body
   * - ``401``
     - ``Unauthorized``
     - Client must **authenticate** first*
   * - ``403``
     - ``Forbidden``
     - An authenticated client is **not allowed** to perform the requested action
   * - ``404``
     - ``Not Found``
     - The path to identify the Resource is incorrect or the Resource does not exist

A bad request will include an error message in its response. The response will indicate **what the client must change** in their request body to succeed. This failure is seen when **C**\reating or **U**\pdating a Resource entity:

.. admonition:: example

   In the Coding Events API, **the State** of a ``CodingEvent`` is **validated** using the following criteria:

   - ``Title``: 10-100 characters
   - ``Description``: less than 1000 characters

   Imagine a client sending a ``PATCH`` request to **U**\pdate the ``CodingEvents`` Resource entity with an ``Id`` of ``6``. 

      ``PATCH /events/6 (PartialCodingEvent) -> CodingEvent``
   
   If their request body contained the following **invalid representation** of partial State (due to a ``Title`` field that is too short):

   .. sourcecode:: bash
      :caption: invalid representation in request to PATCH /events/6 endpoint
   
      {
         "Title": "short"
      }

   The API response would have a ``400`` status code alerting the client that they must **correct their representation**. The response body would be used to communicate which aspects were invalid:

   .. sourcecode:: bash
      :caption: 400 failed response body

      {
         "error": "invalid fields",
         "fields": [
            {
               "Title": "must be between 10 and 100 characters in length"
            }
         ]
      }

   Using the hints in the response the client can fix their request body and reissue the request successfully.

.. admonition:: fun fact

   The ``401``, or ``Unauthorized``, status code actually indicates that the consumer is **not authenticated**. This means the consumer has **not proven their identity** to the API.
   
   The ``403``, or ``Forbidden``, status code is a more accurate description of being **unauthorized**. After authenticating, the consumer's **authorization** can determine if they are allowed or **forbidden** from taking the requested action.

Headers
-------

   In RESTful design **headers** are used to communicate **metadata** about each interaction with a Resource

.. list-table:: Common request/response headers in REST
   :header-rows: 1
   :widths: 20 20 40 20

   * - Request/Response
     - Header
     - Meaning
     - Example
   * - Both
     - ``Content-Type``
     - The attached body has the following media type
     - ``application/json``
   * - Request
     - ``Accept``
     - The client expects the requested Resource representation in the given media type
     - ``application/json``
   * - Response
     - ``Location``
     - The created Resource representation can be found at the given URL value
     - ``/resources/{id}``

.. admonition:: tip

   The ``Authorization`` **request header** is also commonly used. Later in this course we will learn about **authenticating** with an API using this header and a `JWT access token <https://auth0.com/docs/protocols/oidc>`_.

Learning More
=============

These articles have covered the fundamental aspects of the RESTful mental model and practical usage. However, RESTful design is a deep topic that even extends *beyond the web and use of HTTP*! 

If you want to learn more the following links are a good start:

Practical Understanding
-----------------------

- `Craig Dennis: APIs for beginners (YouTube) <https://www.youtube.com/watch?v=GZvSYJDk-us&t=0s>`_
- `REST sub-collections, relationships and links <https://restful-api-design.readthedocs.io/en/latest/relationships.html>`_
- `OpenAPI specification & Swagger REST tools <https://swagger.io/specification/>`_
- The `GitHub API <https://developer.github.com/v3/>`_ and `Stripe (payment processing) API <https://stripe.com/docs/api>`_ are excellent examples of RESTful design (and fantastic documentation)

Deep Understanding
------------------

- the `REST constraints <https://www.restapitutorial.com/lessons/whatisrest.html>`_
- the `The Richardson REST maturity model <https://www.martinfowler.com/articles/richardsonMaturityModel.html>`_
- the original `REST doctoral thesis by Roy Fielding <https://www.ics.uci.edu/~fielding/pubs/dissertation/top.htm>`_