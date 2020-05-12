Using a Template
================

Now that we know a little bit about views, we can start talking about how to pass 
data between MVC elements. Models are a key component of this, but for now, we 
will focus on how to pass data between the view and the controller.

.. index:: ! ViewBag

Passing Data to a Template
--------------------------

The controller class contains methods that send data to different templates.
These methods have a structure similar to:

.. sourcecode:: c#
   :linenos:

   public IActionResult ActionMethod()
   {
      // method code here
      
      ViewBag.property = Data;
      return View();
   }

**ViewBag** is an object that passes data into a template. ``Data`` can
be a variable of any type, a number, a collection of some sort, or an object. 
A ``ViewBag`` property is created and given a value as simply as is done on line 5 above. In fact, we can 
just as easily create a second property on ``ViewBag`` as follows:

.. sourcecode:: c#

	ViewBag.anotherNewProperty = someOtherData;

You can think of ``ViewBag`` as like an empty container object who exists for the purpose of carrying
variables from the controller into the view. 

Accessing Data in a Template
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The data assigned to properties on ``ViewBag`` is available inside of Razor templates.
It can be accessed with the syntax ``@ViewBag.propertyName``.

For example, if the controller stores a vegetable name as string in 
``ViewBag.vegetable``, then the template can display that value like so:

.. sourcecode:: html

   <p>@ViewBag.vegetable</p>

Let's say that ``@ViewBag.vegetable`` stores the string "Rutabaga". When the program 
runs, the application interprets ``<p>@ViewBag.vegetable</p>`` as:

.. sourcecode:: html

   <p>Rutabaga</p>

By using ``@ViewBag.vegetable``, we make our webpage *dynamically* display
data within the ``p`` element. Changing the value of ``vegetable`` leads to a
corresponding change in the text in the view after refreshing.

Check Your Understanding
-------------------------

.. admonition:: Question

   Given the code:

   .. sourcecode:: html

      <p>Name: @ViewBag.name</p>

   What will be displayed on the screen if the controller sends in a ``name``
   variable with a value of "Blake"?

   #. Name: name
   #. Blake
   #. Blake: Blake
   #. Name: Blake

.. ans: d, Name: Blake

.. admonition:: Question

   We want a list element to read, "Item name: ______, Price: ______", where
   the blanks need to be filled in with ``name`` and ``price`` values sent from
   the controller.

   Which of the following will produce the desired result?


   #. ``<li>Item name: @ViewBag.name, Price: @ViewBag.price</li>``
   #. ``<li>@ViewBag("Item name: name, Price: price")</li>``
   #. ``<li>@Item name: , @Price = </li>``
   #. ``<li>Item name: @name, Price = @price</li>``

.. ans: a, ``<li>Item name: @ViewBag.name, Price: @ViewBag.price</li>``
