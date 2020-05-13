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

   Consider the following Razor code:

   .. sourcecode:: guess
      :linenos:

      <div>
         <h3>Coffee Types</h3>
         @foreach (string coffeeType in ViewBag.coffeeTypes)
         {
            <ol>
               <li>@coffeeType</li>
            </ol>
         }
      </div>

   The final HTML produced is one heading, 4 ordered lists, and 4 coffee names. 
   When this view is rendered, each coffee type is labelled with "1".

   .. sourcecode:: html
      :linenos:

      <div>
         <h3>Coffee Types</h3>
         <ol>
            <li>French Roast</li>
         </ol>
         <ol>
            <li>Espresso</li>
         </ol>
         <ol>
            <li>Kopi Luwak</li>
         </ol>
         <ol>
            <li>Instant</li>
         </ol>
      </div>

   
.. index:: ! var

Nested Loops
------------

Assume you have a collection of different ``CoffeeShop`` objects. Each 
object contains a string field for ``name`` and a field that is a list of 
of the brews available, ``coffeeOptions``. 

Below, we nest loops to display a list of the shop names and their brew 
options.

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


Apart from the nested loops displayed above, here are some other items you may find useful
to note from the example above. 

- Razor comments are seen on lines 3 and 8 in the first 
  code block above. Comments in Razor are nested between ``@*`` and ``*@``.
  You may have noticed the comment block present on the top of a new view file.

.. TODO: I added this note from how ``var`` is used in the older C# text. as im still 
.. poking around with the topics we introduce in the next few lesson, im not sure if this 
.. is needed based on viewmodel/validation usage or potentially the entity framework. that's originally
.. what i was thinking including this bit from the older text but its still a realtively simpler
.. way to deliver this example - showing the using statement requires explaining where the object
.. is defined/ what this looks like as we're in an intermediate step of discussing views+ controllers
.. without models. just keeping this as a todo for now so we can return to this later -carly

- ``ViewBag.coffeeShops`` is a list of ``CoffeeShop`` objects but we've used ``var``
  on line 1 to type the ``coffeeShop`` item. 
  
  In some limited circumstances, we can use the **var** keyword to implicitly type a variable. 
  When this keyword is used, C# still assigns a type to ``coffeeShop`` through inference. It 
  looks and sees that we are assigning ``coffeeShop`` to the value at the list index, which is a 
  ``CoffeeShop`` object. Thus, ``coffeeShop`` is of type ``CoffeeShop``.

  Alternatively, Razor does also allow us to import a custom class, such as ``CoffeeShop``.
  If we wanted to do so, we could import the class or its namespace at the top of 
  the template with a :ref:`using-statement` statement. 

.. admonition:: Warning

   We use ``var`` above to simplify the example and focus on the loop action.
   In general, we recommend that you avoid using ``var`` while you are learning C#. 
   Even after you become more experienced with the language, you will still only
   want to use it sparingly and in specific circumstances. Explicitly
   declaring the type of your variables makes for more readable code, to name 
   only one benefit.


Check Your Understanding
-------------------------

.. admonition:: Question

   What is the HTML outcome you expect from the Razor code below?

   .. sourcecode:: guess
      :linenos:

      <div>
         <h3>Coffee Types</h3>
         <ol>
            @foreach (string coffeeType in ViewBag.coffeeTypes)
            {
               <li>@coffeeType</li>
            }
         </ol>
      </div>

   #. One heading, 4 ordered lists, and 4 coffee names (each name labeled as “1”)?
   #. One heading, one ordered list, and 4 coffee names (with the names labeled "1", "2", "3"…)?
   #. 4 headings, 4 ordered lists, and 4 coffee names (each name labeled as “1”)?
   #. 4 headings, 4 ordered lists, and 16 coffee names (with the names labeled "1", "2", "3"…)?

.. ans: a, One heading, 4 ordered lists, and 4 coffee names (each name labeled as “1”)?

.. admonition:: Question

   What is the HTML outcome you expect from the Razor code below?

   .. sourcecode:: guess
      :linenos:

      @foreach (string coffeeType in ViewBag.coffeeTypes)
      {
         <div>
            <h3>Coffee Types</h3>
            <ol>
               <li>@coffeeType</li>
            </ol>
         </div>
      }

   #. One heading, 4 ordered lists, and 4 coffee names (each name labeled as “1”)?
   #. One heading, one ordered list, and 4 coffee names (with the names labeled "1", "2", "3"…)?
   #. 4 headings, 4 ordered lists, and 4 coffee names (each name labeled as “1”)?
   #. 4 headings, 4 ordered lists, and 16 coffee names (with the names labeled "1", "2", "3"…)?

.. ans: c, 4 headings, 4 ordered lists, and 4 coffee names (each name labeled as “1”)?
