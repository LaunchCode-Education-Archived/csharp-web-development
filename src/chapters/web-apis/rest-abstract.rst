===========================
REST: Abstract Fundamentals
===========================

In this article we will explore a pattern for organizing the behavior of an API. REST is an **architectural pattern** that provides *uniformity and predictability* to any API that adheres to it. The same benefits are experienced by the API consumer.

   REST is a set of guiding principles for supporting the organization of an API's core responsibilities -- managing and transferring data.
   
   Its pattern organizes the **external interface** (contract) and does not concern itself with the *internal implementation* of the API . 

In this course we will only be consuming a REST API, not creating one. For this reason we will focus on the external fundamentals of REST. Although we will not be designing or implementing a RESTful API, learning how to use one will form a foundation that empowers further learning. 

What is REST?
=============

   **RE**\presentational **S**\tate **T**\ransfer

.. admonition:: tip

   The topics of State and Representation are *purposefully abstract* in REST so that they can be applied to any API. Don't get overwhelmed!
   
What is State?
==============

   Transitional data that can be viewed or changed by external interaction

While State is abstract you can "interact" with it using **CRUD** (Create, Read, Update, Delete) operations. 

Imagine viewing, or **R**\eading, the State as it *transitions* through each of the following interactions:

#. **before Creating**: empty State
#. **after Creating**: initial State
#. **after Updating**: new State
#. **after Deleting**: empty State

You can see that the State is defined by how the data exists **after its latest interaction**. 

.. admonition:: note

   The concept of State is both the most abstract and most fundamental aspect of REST. All of the following sections will reference the Coding Events MVC project you created to illustrate the concepts in a more relatable way. 

What is a Representation?
=========================

   A depiction of State that is usable in a given context

Representations are a way of working with State in different contexts. Think about the difference in Representation between the State stored in a database row and an object in your code *representing* that row. 

First, consider how we *represent* State in a database row. Traditionally the *Representation of a row* is visualized as a table with columns listing the properties and values that make up the State:

.. admonition:: example

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
      
Recall that the raw State held in a database row was not *usable in the context of our application code*. Instead we used an ORM to *represent the State as an object* that was suitable for our application's object-oriented context. 

The ``toString()`` method is used to visualize the *Representation as an object* that looks something like this:

.. admonition:: example

   .. sourcecode:: js
      :caption: CodingEvent State represented as an object

      CodingEvent {
         Id: 1
         Title: "Halloween Hackathon!"
         Description: "A gathering of nerdy ghouls..."
         Date: 2020-10-31
      }

In both cases the **State was the same**. The difference was in the **Representation that made it usable in its context**. 

   In REST, State must be **represented** in a way that is **portable and compatible** with both the client and API.

Consider a third Representation -- JSON. Recall that JSON is a format that provides *structure, portability and compatibility*. For these reasons JSON is the standard Representation used when transferring State between a client application and an API. 

.. admonition:: example

   The State of a *single* ``CodingEvent`` **entity** would be represented as a *single JSON object*:

   .. sourcecode:: js
      :caption: CodingEvent State represented as a JSON object

      {
         "Id": 1,
         "Title": "Halloween Hackathon!",
         "Description": "A gathering of nerdy ghouls...",
         "Date": "2020-10-31"
      }

   Whereas the State of a **collection** of ``CodingEvents`` would be represented by a *JSON array of objects*.

   .. sourcecode:: js
      :caption: The State of a collection of CodingEvents represented as a JSON array

      [
         {
            "Id": 1,
            "Title": "Halloween Hackathon!",
            "Description": "A gathering of nerdy ghouls...",
            "Date": "2020-10-31"
         },
         ...
      ]

   Notice that the State here is represented as the *collective State* of all the ``CodingEvents`` in the list.

.. admonition:: tip

   The process of converting an object Representation to a JSON Representation is called **JSON serialization**.
   
   The inverse process where JSON is parsed, or converted back to an object Representation, is called **JSON deserialization**.

Transferring a Representation of State
======================================

   In REST, **State** is **transitioned** by interactions between a client and an API.
   
   Aside from **D**\eleting, all other interactions involve **transferring** a **Representation of State**.
   
A RESTful API is designed to be stateless. This has the following implications:

- The State of data is maintained by the client application and the database that are on either side of the *interface*. 
- Its transitions are driven by the client and facilitated by the API which send or receive representations of the desired State.

In order to maintain portability between the different client and API contexts we transfer Representations of State. These Representations can then be converted between the *portable Representation* (JSON) and the representation that fits the context (a JavaScript or C# object).

Recall that State is defined by its latest interaction. Because every interaction is initiated by the client we consider the **client to be in control of State**.

What this means is that the client can:

- **R**\ead: *request the current* Representation of State
- **C**\reate & **U**\pdate: *transition to a new State* by sending a new Representation of State
- **D**\elete: *transition to an empty State* by requesting its removal

However, it is up the API to define the contract, or **expose**:

- the types of State, or **resources**, the client can interact with
- which (CRUD) interactions are *supported* for each resource 

These decisions are what drive the design of the contract. 
   
Resources
=========

   **Resource**: the Representation of a *specific type of State* that a RESTful API *exposes* for a *client to interact* with

While State is an abstract concept, a **resource** is something more *tangible*. In simple terms, a **resource is like a type of object** that an API allows clients to interact with. Resources are categorized as an individual **entity** or a **collection**.

   **Entity**: a single resource that is **uniquely identifiable in a collection**

   **Collection**: entities of the same resource type **treated as a whole**

We refer to **the State of a resource** in terms of a single entity or the *collective State* of a collection.

.. admonition:: note
   
   Initially a collection's State is just *empty*.
   
   If you were to **R**\ead the collection's State it would be *represented* as an empty JSON array, ``[]``.

In RESTful design an individual entity **only exists as part of a collection**.

   A change to the State of an entity inherently changes the State of the collection it is a part of.

When **C**\reating an entity you are operating on the **State of the collection**. In order to create it you must know:

- what collection the entity belongs to

When **R**\eading, **U**\pdating or **D**\eleting an entity you are *directly operating* on the **State of the entity** and *indirectly* on the State of its collection.

In order to fulfill these operations you need to know:

- what collection the entity belongs to
- how to uniquely identify the entity within the collection

This hierarchal relationship between collections and the entities within them is an integral aspect of RESTful design. The contract of a RESTful API defines the **shape**, or structure, of its resources along with the hierarchal organization of the **endpoints** used for interacting with them.
