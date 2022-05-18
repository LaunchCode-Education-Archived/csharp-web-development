Exercises: Web APIs and REST
============================

We've created a CodingEvents API application `here <https://github.com/LaunchCodeEducation/coding-events-api/tree/1-sqlite>`__. Before we ask you to 
fork and clone this, let's first think conceptually about the kinds of requests a client application could make to this API.

The API
-------

This branch of ``coding-events-api`` starts by only exposing a single resource, ``CodingEvent``, and four endpoints for interacting with it.
The ``CodingEvent`` resource is analogous to the ``Event`` model class we created in our CodingEvents MVC application.

The Resource
^^^^^^^^^^^^

The shape of the ``CodingEvent`` resource describes the general form of its properties and value types:

.. sourcecode:: bash
   :linenos:

   CodingEvent {
      Id: integer
      Title: string
      Description: string
      Date: string (ISO 8601 date format)
   }


In our case, the ``CodingEvent`` shape is just the properties and types (translated to portable 
`JSON types <https://json-schema.org/understanding-json-schema/reference/type.html>`_) defined in a ``CodingEvent`` model class in ``coding-events-api``.

.. sourcecode:: csharp
   :linenos:

   public class CodingEvent {
      public int Id { get; set; }
      public string Title { get; set; }
      public string Description { get; set; }
      public DateTime Date { get; set; }
   }

An example of a real ``CodingEvent`` JSON response to a ``GET`` request would look like this:

.. sourcecode:: bash
   :linenos:

   {
      "id": 1,
      "title": "Consuming the Coding Events API With Postman",
      "description": "Learn how to use Postman to interact with the Coding Events API!",
      "date": "2020-07-24"
   }

Notice how this JSON is just a representation of an instance of the ``CodingEvent`` model class. The data shape has been converted from a C# object 
representation to a JSON string representation so it can be transported over HTTP. Recall that we perform this 
conversion, or serialization, so that our API can output data in a portable format that is language-agnostic.

The Endpoints
^^^^^^^^^^^^^

This branch of the API has four endpoints: 

#. :ref:`GET Coding Events<get_coding_events>`
#. :ref:`GET a Single Coding Event<get-single-coding-event>`
#. :ref:`Create a Coding Event<create_coding_event>`
#. :ref:`Delete a Coding Event<delete_coding_event>`

.. _get_coding_events:

We'll ask you to consider some details of how to describe these endpoints.

Remember, an endpoint is made up of a path (to the resource) and a method (action to take on the 
resource). Because we only have one resource, each of our endpoints share a common entry-point path of ``/api/events``. Request and response bodies are all 
in JSON, or more specifically, they have a ``Content-Type`` header value of ``application/json``.


.. _web-api-exercises: 

GET Coding Events
~~~~~~~~~~~~~~~~~

Making a ``GET`` request to the entry-point of a resource should return a representation of the state of the collection. In our case, this representation 
is a JSON array with ``CodingEvent`` elements:

.. sourcecode:: bash
   :linenos:

   [
      CodingEvent { ... },
      ...
   ]

If the current state of the collection is empty, then we will just get back an empty JSON array:

.. sourcecode:: bash

   []

.. admonition:: Question

   Using our endpoint shorthand, how would we describe this action?

   Some items to consider:

   #. What is the HTTP request type being used?
   #. What is the resource path being requested?
   #. Is there a request body being sent? What is included in it?
   #. If the request is successful, what information can we expect to be included in the response?


.. _get-single-coding-event:

:ref:`Check your solutions<web-api-ex-1>`

GET a Single Coding Event
~~~~~~~~~~~~~~~~~~~~~~~~~

If you want to view the representation of a single entity, you need to provide information to uniquely identify it in the collection. Since the 
entry-point represents the collection, it can be followed by an ``Id`` value in the path to look inside the collection and return just the corresponding 
entity.

When describing entity endpoints, we use a path variable notation, ``{variableName}``, to symbolize where the value needs to be put in the path. 

If an entity with the given ``codingEventId`` is found, we will get a single ``CodingEvent`` JSON object back. If it is not found, we will receive a 
response with a ``404`` status code to indicate the failed lookup.

.. _create_coding_event:

.. admonition:: Question

   Using our endpoint shorthand, how would we describe this action?

   Some items to consider:

   #. What is the HTTP request type being used?
   #. What is the resource path being requested?
   #. Is there a request body being sent? What is included in it?
   #. If the request is successful, what information can we expect to be included in the response?
   #. If the request contains an error, what information can we expect to be included in the response?



Create a Coding Event
~~~~~~~~~~~~~~~~~~~~~

Think about what it means to create an entity. You need to provide the required data and the collection it belongs to. When we want to create a 
``CodingEvent``, we are asking the API to change the state of the collection (the list of entities) so our path must be ``/api/events``. Recall that the 
"C" in CRUD stands for "create". Putting the resource and the action together, we know we 
need to ``POST`` to the ``/api/events`` endpoint. Finally, as part of our request, we will need to send a request body containing the data 
required to create the entity.

The shape of the ``NewCodingEvent`` describes the JSON body that the endpoint expects:

.. sourcecode:: bash
   :linenos:

   NewCodingEvent {
      Title: string
      Description: string
      Date: string (ISO 8601 date format)
   }

When making a request, you would need to send a JSON body like this to satisfy the general shape:

.. sourcecode:: bash
   :linenos:

   {
      "Title": "Halloween Hackathon!",
      "Description": "A gathering of nerdy ghouls to work on GitHub Hacktoberfest contributions",
      "Date": "2020-10-31"
   }

.. admonition:: Note

   We only provide the user editable fields, not the unique ``Id`` which the API handles internally when saving to the database.

Recall that when a ``POST`` request is successful, the API should respond with the ``201``, or *Created*, HTTP status code. As part of the ``2XX`` 
HTTP success status codes, it indicates a particular type of successful response with a special header.

One of the REST conventions states that when an entity is created, the response should include both this status and the ``Location`` header that provides 
the URL of the new entity:

.. sourcecode:: bash

   Location=<server origin>/api/events/<new entity Id>

As an example:

.. sourcecode:: bash

   Location=http://localhost:5000/api/events/1

You can then issue a ``GET`` request to the ``Location`` header value and view the new entity. 


If the request fails because of a client error, then it will respond with a ``400`` status code and a message about what went wrong. In the case of 
``CodingEvent`` entities, the following validation criteria must be met:

- ``Title``: 10-100 characters
- ``Description``: less than 1000 characters

.. _delete_coding_event:
 
.. admonition:: Question

   Using our endpoint shorthand, how would we describe this action?

   Some items to consider:

   #. What is the HTTP request type being used?
   #. What is the resource path being requested?
   #. Is there a request body being sent? What is included in it?
   #. If the request is successful, what information can we expect to be included in the response?
   #. If the request contains an error, what information can we expect to be included in the response?



Delete a Coding Event
~~~~~~~~~~~~~~~~~~~~~

Deleting a ``CodingEvent`` resource is an operation on a single entity. Just like the endpoint for getting a single entity, this endpoint requires a 
``codingEventId`` path variable. When a resource is deleted, a RESTful API should respond with a ``204`` status code. Similar to the ``201`` status, this 
code indicates a success with no response body or special headers. 

If you attempt to delete a resource that doesn't exist (with an incorrect ``codingEventId``), then the endpoint will respond with an expected ``404`` 
status and message.

.. admonition:: Question

   Using our endpoint shorthand, how would we describe this action?

   Some items to consider:

   #. What is the HTTP request type being used?
   #. What is the resource path being requested?
   #. Is there a request body being sent? What is included in it?
   #. If the request is successful, what information can we expect to be included in the response?
   #. If the request contains an error, what information can we expect to be included in the response?


Install Postman
---------------

Now that we've explored working with those endpoints, we're almost ready to start running the API and test sending those requests. 
You'll need to :ref:`install Postman <postman-installation>` to work with this lesson's studio and practice running these requests.
