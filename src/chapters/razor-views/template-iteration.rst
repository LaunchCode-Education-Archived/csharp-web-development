.. How do we use a for loop?

.. _razor-iteration:

Iterating in a Template
=======================

Let's revisit part of the non-efficient HTML from the introduction, where we
hard-coded coffee options in a list.

.. sourcecode:: html
   :linenos:

   <ol>
      <li>French Roast</li>
      <li>Espresso</li>
      <li>Kopi Luwak</li>
      <li>Instant</li>
   </ol>

If we want to add, remove, or edit the list items, we need to go in and change
the individual tags, which is a poor use of our time. Fortunately, there is a
way to streamline the process.

In C#, we use a :ref:`foreach_loop` to iterate through the items in a data
collection.

.. sourcecode:: c#

   foreach (type item in items) {
      // Code to repeat...
   }

Razor templates allow us to use a ``foreach`` loop to display items in a 
collection.

.. sourcecode:: guess
   :linenos:

   <ol>
      @foreach (type collectionItem in ViewBag.collectionProperty)
      {
         <li>@collectionItem</li>
      }
   </ol>

#. The ``@foreach`` loop is initiated inside of a list element (either ``<ol>`` or ``<ul>``).
#. ``ViewBag.collectionProperty`` represents any collection that has been assigned as a property on ``ViewBag``.
#. ``collectionItem`` represents an individual item or element within the collection.
#. The ``@`` specifies the C# portion of the template.

We can think of this syntax as saying, *"For each item within
ViewBag's property, 'collectionProperty', repeat this HTML tag, but use the current value of
'collectionItem'."*

Let's apply this new concept to the HTML coffee list example. Assume that we store each of
the coffee names as strings in a ``List`` called ``ViewBag.coffeeOptions``.

.. sourcecode:: guess
   :linenos:

   <ol>
      @foreach (string coffeeType in ViewBag.coffeeOptions)
      {
         <li>@coffeeType</li>
      }
   </ol>

Some points to note:

#. ``coffeeOptions`` is accessible to the template because it is a property of the ``ViewBag`` object.
#. In the first pass through the loop, ``coffeeType`` takes the value of the first
   coffee name in the ``coffeeOptions`` list.
#. ``@coffeeType`` displays the value of ``coffeeType`` in the view, so the
   ``li`` element will show the first coffee name.
#. Each successive iteration, ``coffeeType`` takes the next value in the list, and
   Razor adds a new ``<li></li>`` element to display that data.


.. _location-matters:

.. admonition:: Warning

   ``@foreach`` creates one HTML tag for each item in a collection. 
   BE CAREFUL where you place it.

   Consider the following code blocks:

   .. admonition:: Examples

      Option #1:

      .. sourcecode:: guess
         :linenos:

         <div>
            <h3>C# Types</h3>
            <ol>
               @foreach (string coffeeType in ViewBag.coffeeTypes)
               {
                  <li>@coffeeType</li>
               }
            </ol>
         </div>

      Option #2:

      .. sourcecode:: guess
         :linenos:

         <div>
            <h3>C# Types</h3>
            @foreach (string coffeeType in ViewBag.coffeeTypes)
            {
               <ol>
                  <li>@coffeeType</li>
               </ol>
            }
         </div>

      Option #3:

      .. sourcecode:: guess
         :linenos:

         @foreach (string coffeeType in ViewBag.coffeeTypes)
         {
            <div>
               <h3>C# Types</h3>
               <ol>
                  <li>@coffeeType</li>
               </ol>
            </div>
         }

   Which option produces:

   #. One heading, 4 ordered lists, and 4 coffee names (each name labeled as "1")?
   #. One heading, one ordered list, and 4 coffee names (with the names labeled
      1, 2, 3...)?
   #. 4 headings, 4 ordered lists, and 4 coffee names (each name labeled as "1")?

.. index:: ! var

Nested Loops
------------

Assume you have a collection of different ``CoffeeShop`` objects. Each 
object contains a string field for ``name`` and a field that is a list of 
of the brews available, ``coffeeOptions``. 

Below, we use nest loops to display a list of the shop names and their brew 
options using nested loops.

Sample Razor template:

.. sourcecode:: html
   :linenos:

   @foreach (var coffeeShop in ViewBag.coffeeShops)
   {
      @*Each shop name*@
      <p>@coffeeShop.Name</p>
      <ul>
         @foreach(string coffeeType in coffeeShop.CoffeeOptions)
         {
            @*Each coffee type available*@
            <li>@coffeeType</li>
         }
      </ul>
   }

Sample HTML output:

.. sourcecode:: html
   :linenos:

   <p>Central Perk</p>
   <ul>
      <li>Espresso</li>
      <li>Instant</li>
   </ul>

   <p>Brews Brothers</p>
   <ul>
      <li>French Roast</li>
      <li>Kopi Luwak</li>
   </ul>


Apart from the nest loops displayed above, here are ome other items you may find useful
to note from the example above. 

- Razor comments are seen on lines 3 and 8 in the first 
  code block above. Comments in Razor are nested between ``@*`` and ``*@``.
  You may have noticed the comment block present on the top of a new view file.

.. TODO: is this a sufficient note for the use of var here? It feel unfinished but im
at a loss for what else is needed here.

- ``ViewBag.coffeeShops`` is a list of ``CoffeeShop`` objects but we've used ``var``
  on line 1 to type the ``coffeeShop`` item. In some limited circumstances, we can 
  use the **var** keyword to implicitly type a variable.
  Alternatively, Razor does also allow us to import a custom class. such as ``CoffeeShop``.
  Another way to use this list of ``CoffeeShop`` objects would be to import the class
  at the top of the template with a :ref:`using-statement` statement.


Check Your Understanding
-------------------------

Use the three code samples listed in the
:ref:`Location Matters <location-matters>` section to answer the following
questions:

.. admonition:: Question

   Which option produces one heading, 4 ordered lists, and 4 coffee names (each
   name labeled as "1")?

   #. Option 1
   #. Option 2
   #. Option 3

.. Answer = option 2

.. admonition:: Question

   Which option produces one heading, one ordered list, and 4 coffee names
   (with the names labeled 1, 2, 3...)?

   #. Option 1
   #. Option 2
   #. Option 3

.. Answer = option 1

.. admonition:: Question

   Which option produces 4 headings, 4 ordered lists, and 4 coffee names
   (each name labeled as "1")?

   #. Option 1
   #. Option 2
   #. Option 3

.. Answer = option 3
