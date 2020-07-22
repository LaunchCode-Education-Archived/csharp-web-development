.. index:: ! REST, ! RESTful web services, ! Representational State Transfer

What is REST?
=============

**REST** is an acronym that stands for **REpresentational State Transfer**. **RESTful web services** refer to web technologies that use
this design pattern. REST, as we've mentioned, is an architectural pattern that provides uniformity and predictability to any API 
that adheres to it. The same benefits are experienced by the API consumer. REST is a set of guiding principles for supporting 
the organization of an API's core responsibilities -- managing and transferring data. The REST pattern organizes the external 
interface, or contract, and does not concern itself with the internal implementation of the API.

Adopting the REST specification into the design of an API provides consistency during development and consumption. Much like 
following the patterns of MVC allows other developers to easily understand your code, following REST patterns gives other developers 
the benefit of understanding how your API is structured and behaves. As an added bonus, a REST API also gives the client application 
a base-line understanding on how to interact with your API.

The following sections reference the CodingEvents MVC project we've been creating over the last several lessons to illustrate 
some of the more abstract notions of an alternative CodingEvents API project.


.. admonition:: Tip

   The topics of state and representation are *purposefully abstract* in REST so that they can be applied to any API. Don't get overwhelmed!
   
What is State?
--------------

State is transitional application data that can be viewed or changed by external interaction. Though state is abstract, programmers interact with it 
using CRUD operations. 

Imagine viewing, or reading, the state of an application's data as it transitions through each of the following interactions:

#. **Before creating**: Empty state
#. **After creating**: Initial state
#. **After updating**: New state
#. **After deleting**: Empty state

You can see that the state is defined by how the data exists after its latest interaction. 

.. admonition:: Note

   The concept of state is both the most abstract and most fundamental aspect of REST. 

What is a Representation?
-------------------------

Representation refers to a depiction of state that is usable in a given context. Representations are a way of working with application state across various 
contexts. Think about the difference in representation between the state stored in a database row and an object in your code *representing* that row. First, 
consider how we represent state in a database row. Traditionally, the representation of a row is visualized as a table with columns listing the 
properties and values that make up the state:

.. admonition:: Example

   .. list-table:: CodingEvent State represented as a database row
      :widths: 10 30 30 30
      :header-rows: 1

      * - Id
        - Title
        - Description
        - Date
      * - ``1``
        - ``"Halloween Hackathon"``
        - ``"A gathering of nerdy ghouls to..."``
        - ``2020-10-31``
      
Recall that raw state held in a database row is not usable in the context of our application code. Instead, we use an ORM to represent the state as an 
object that is suitable for our application's object-oriented context. 

The ``ToString()`` method is used to visualize the representation as an object that looks something like this:

.. admonition:: Example

   .. sourcecode:: js
      :linenos:

      CodingEvent {
         Id: 1
         Title: "Halloween Hackathon!"
         Description: "A gathering of nerdy ghouls..."
         Date: 2020-10-31
      }

In both cases, the application state is the same. The difference is in the representation that makes it usable in its context. In REST, state must be 
represented in a way that is portable and compatible with both the client and API. Consider a third representation, JSON. JSON is itself a format that 
provides structure, portability and compatibility. For these reasons, JSON is the standard representation used when transferring state between a client 
application and an API. 

.. admonition:: Example

   The state of a *single* ``CodingEvent`` entity is represented as a single JSON object:

   .. sourcecode:: js
      :linenos:

      {
         "Id": 1,
         "Title": "Halloween Hackathon!",
         "Description": "A gathering of nerdy ghouls...",
         "Date": "2020-10-31"
      }

	Whereas the state of a collection of ``CodingEvents`` is represented by a JSON array of objects.

   .. sourcecode:: js
      :linenos:

      [
         {
            "Id": 1,
            "Title": "Halloween Hackathon!",
            "Description": "A gathering of nerdy ghouls...",
            "Date": "2020-10-31"
         },
         ...
      ]

   Notice that the state here is represented as the collective state of all of the ``CodingEvents`` in the collection.

.. index:: ! JSON serialization, ! JSON sdeerialization

.. admonition:: Tip

   The process of converting an object representation to a JSON representation is called **JSON serialization**.
   
   The inverse process, where JSON is parsed, or converted back to object representation, is called **JSON deserialization**.

Transferring a Representation of State
--------------------------------------

In REST, state is transitioned by interactions between a client and an API. Each transition is driven by transferring a representation of state. A 
RESTful API is designed to be stateless. 

This has the following implications:

- The state of data is maintained by the client application and the database that are on either side of the interface. 
- State transitions are are signals driven by the client and facilitated by the API containing representations of the desired state.

In order to maintain portability between different client and API contexts, we transfer representations of state. These representations can then be 
converted between the *portable representation* (JSON) and the representation that fits a given context (a JavaScript or C# object). Remember, state 
is defined by an application's latest CRUD operation. Because every interaction is initiated by the client, we consider the client to be in control 
of state.

What this means is that the client can:

- Read: request the current representation of state
- Create & Update: transition to a new state by sending a new representation
- Delete: transition to an empty state by requesting its removal

However, it is up the API to define the contract, or **expose**:

- the types of state, or resources, the client can interact with
- which (CRUD) interactions are supported for each resource 

These decisions are what drive the design of the contract. 

.. index:: ! resource entity, ! resource collection
   
Resources
---------

A resource is the representation of a specific type of state that a RESTful API exposes for a client to interact with.

While state is an abstract concept, a resource is something more tangible. In simple terms, a resource is like a type of object that an API allows 
clients to interact with. Resources are categorized as an individual entity or a collection.

	**Entity**: a single resource that is uniquely identifiable in a collection.

   **Collection**: entities of the same resource type treated as a whole.

We refer to the state of a resource in terms of a single entity or the collective state of a collection.

.. admonition:: Note
   
   Initially, a collection's state is just empty. If you were to read the collection's state, it would be represented as an empty JSON array, ``[]``.

In RESTful design, an individual entity only exists as part of a collection. A change to the state of an entity inherently changes the state of 
the collection it is a part of.

When creating an entity, you are operating on the state of the collection. In order to create it, you must know what collection the entity belongs to.

When reading, epdating or deleting an entity, you are directly operating on the state of the entity and indirectly on the state of its collection.

In order to fulfill these operations, you need to know:

- what collection the entity belongs to
- how to uniquely identify the entity within the collection

This hierarchal relationship between collections and the entities within them is an integral aspect of RESTful design. The contract of a RESTful API 
defines the shape, or structure, of its resources along with the hierarchal organization of the endpoints used for interacting with them.

Check Your Understanding
------------------------

.. admonition:: Question

   QUESTION

   a. True

   b. False

.. ans: 

.. admonition:: Question

   QUESTION

   a. A point in our code where the debugger will stop running and provide information about the current state.

   b. A point in our code that we anticipate will result in an exception or error. 

   c. A point in our code where we include a print statement to see what's going on.

   d. A point in our code where we want to throw the computer out of a window because nothing works.

.. ans; 
