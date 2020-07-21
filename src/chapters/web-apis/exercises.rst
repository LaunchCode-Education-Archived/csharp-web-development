Exercises!!
===========

.. todo: reorg here? this section "The API", down to the "Summary" section can be introduced independent of pulling down the repo. 
potentially create exercises that ask students to write the endpoint shorthands to get prepped for the studip where they ping these endpoints?

The API
-------

This branch of the API starts by only exposing a single resource and four endpoints for interacting with it.

CodingEvent Resource
^^^^^^^^^^^^^^^^^^^^

.. todo: show this in the running app schema 

The shape of the ``CodingEvent`` resource describes the general form of its properties and value types:

.. sourcecode:: bash
   :linenos:

   CodingEvent {
      Id: integer
      Title: string
      Description: string
      Date: string (ISO 8601 date format)
   }

.. todo: note that this is the equivalent of the Event model class 

In our case, the ``CodingEvent`` shape is just the properties and types (translated to portable 
`JSON types <https://json-schema.org/understanding-json-schema/reference/type.html>`_) defined in the ``CodingEvent`` model class.

.. sourcecode:: csharp
   :linenos:

   public class CodingEvent {
      public int Id { get; set; }
      public string Title { get; set; }
      public string Description { get; set; }
      public DateTime Date { get; set; }
   }

An example of a real ``CodingEvent`` JSON response would look like this:

.. sourcecode:: bash
   :linenos:

   {
      "id": 1,
      "title": "Consuming the Coding Events API With Postman",
      "description": "Learn how to use Postman to interact with the Coding Events API!",
      "date": "2020-07-24"
   }

Notice how this JSON is just a representation of an instance of the ``CodingEvent`` model class. 

It has been converted from a C# object representation to a JSON string representation so it can be transported over HTTP. Recall that we perform this 
conversion, or serialization, so that our API can output data in a portable format that is language-agnostic.

Endpoints
^^^^^^^^^

This branch of the API has four endpoints: 

- GET Coding Events
- GET Single Coding Event
- Create a Coding Event
- Delete a Coding Event

Remember an endpoint is made up of a path (to the resource) and a method (action to take on the 
resource). They all share a common entry-point path of ``/api/events``. Request and response bodies are all in JSON, or more 
specifically, they have a ``Content-Type`` header value of ``application/json``.

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

In more terse terms, we can describe this endpoint as:

``GET /api/events -> CodingEvent[]``

GET Single Coding Event
~~~~~~~~~~~~~~~~~~~~~~~

If you want to view the representation of a single entity, you need to provide information to uniquely identify it in the collection. Since the 
entry-point represents the collection, it can be followed by an ``Id`` value in the path to look inside the collection and return just the corresponding 
entity.

When describing entity endpoints, we use a path variable notation, ``{variableName}``, to symbolize where the value needs to be put in the path. 

We can describe this ``CodingEvent`` entity endpoint in shorthand as:

``GET /api/events/{codingEventId} -> CodingEvent``

If an entity with the given ``codingEventId`` is found, we will get a single ``CodingEvent`` JSON object back. If it is not found, we will receive a 
response with a ``404`` status code to indicate the failed lookup.

Create a Coding Event
~~~~~~~~~~~~~~~~~~~~~

Think about what it means to create an entity. You need to provide the required data and the collection it belongs to. When we want to create a 
``CodingEvent``, we are asking the API to change the state of the collection (the list of entities) so our path must be ``/api/events``. Recall that the 
"C" in CRUD stands for "create" and corresponds to the ``POST`` HTTP method in a RESTful API. Putting the resource and the action together, we know we 
need to ``POST`` to the ``/api/events`` endpoint. Finally, as part of our ``POST`` request, we will need to send a request body containing the data 
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

You could then issue a ``GET`` request to the ``Location`` header value and view the new entity. In shorthand format, this endpoint can be described as:

``POST /api/events (NewCodingEvent) -> 201, CodingEvent``

If the request fails because of a client error, then it will respond with a ``400`` status code and a message about what went wrong. In the case of 
``CodingEvent`` entities, the following validation criteria must be met:

- ``Title``: 10-100 characters
- ``Description``: less than 1000 characters

Delete a Coding Event
~~~~~~~~~~~~~~~~~~~~~

Deleting a ``CodingEvent`` resource is an operation on a single entity. Just like the endpoint for getting a single entity, this endpoint requires a 
``codingEventId`` path variable. When a resource is deleted, a RESTful API should respond with a ``204`` status code. Similar to the ``201`` status, this 
code indicates a success with no response body or special headers. 

The deletion endpoint can be described in shorthand as:

``DELETE /api/events/{codingEventId} -> 204``

If you attempt to delete a resource that doesn't exist (with an incorrect ``codingEventId``), then the endpoint will respond with an expected ``404`` 
status and message.

Summary
~~~~~~~

Two endpoints at the ``CodingEvents`` entry-point path, ``/api/events``, to interact with the collection as a whole:

- **list Coding Events**: ``GET /api/events -> CodingEvent[]``
- **create a Coding Event**: ``POST /api/events (NewCodingEvent) -> 201, CodingEvent``

And two that require a sub-path variable, ``/events/{codingEventId}``, to interact with a single entity:

- **delete a Coding Event**: ``DELETE /api/events/{codingEventId} -> 201, CodingEvent``
- **find single Coding Event**: ``GET /api/events/{codingEventId} -> CodingEvent``