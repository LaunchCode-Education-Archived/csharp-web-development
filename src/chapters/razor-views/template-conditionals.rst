Conditionals in a Template
==========================

In addition to iteration, Razor can also add or remove content on a
webpage based on certain conditions. Going back to the coffee example, we could
generate the ordered list ONLY IF ``coffeeOptions`` contains data. If the
list of coffee types is empty, then there is no need to include the ``<ol>`` 
element. Instead, the template could include a ``<p>`` element with text stating 
that there are no options to select.

Display Content ``if/else``
---------------------------

To include conditional logic to display a Razor template element, we use a basic C# ``if`` clause.

The general syntax for including a conditional in Razor is:

.. sourcecode:: guess

   @if (condition)
   {
      // HTML element(s) to add or additional template logic
   }

Above, ``condition`` represents any expression that can be evaluated to ``true`` or ``false`` 
(ie, a boolean).

If ``condition`` evaluates to ``true``, then Razor adds the HTML element to
the webpage and the content is displayed in the view. If ``condition`` is
``false``, then Razor does NOT generate the element, and the content stays
off the page.

Let's look at an example:

.. admonition:: Example

   Assume that ``userSelection`` represents a string property on ``ViewBag``.

   .. sourcecode:: guess
      :linenos:

      @if (ViewBag.userSelection == "Instant")
      {
         <p>Are you sure about that?</p>
      } 
      else if (ViewBag.userSelection == "French Roast")
      {
         <p>Oooh la la!</p>
      } 
      else
      {
         <p>Thanks for your order</p>
      }

The ``@if`` statement in line 1 compares a user's brew choice to the string
``"Instant"``. If they match, then Razor adds the paragraph element to the
view. If they do not match, then the ``<p>`` tag on line 3 is not created and the 
condition on line 5 is evaluated. If that ``else if`` statement is true, then 
a paragraph element with different internal text is added. Lastly, if neither 
of those conditions is met, then the paragraph element with text on line 11 
is rendered. 

.. admonition:: Note

   We don't add an additional ``@`` symbols on lines 5 and 9 in the 
   example above. ``if``, ``else if``, and ``else`` clauses are dependent
   and treated as one C# code block in Razor.

Nesting Logic
^^^^^^^^^^^^^

Just as we can nest loops, we can nest any C# in Razor for advanced control flow.

.. admonition:: Example

   ``coffeeOptions`` is a list property on ``ViewBag``.

   .. sourcecode:: guess
      :linenos:

      @if (ViewBag.coffeeOptions.Count > 1)
      {
         <ol>
            @foreach(string coffeeType in ViewBag.coffeeOptions)
            {
               <li>@coffeeType</li>
            }
         </ol>
      }


The conditional in line 1 checks that ``coffeeOptions`` contains more than one
item. If ``true``, then the ordered list is rendered in the view using a ``@foreach``
loop.

Adding vs. Displaying/Hiding
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

A conditional statement in a Razor template determines if content is *added or not added* to a page. This is
different from deciding if content should be *displayed or hidden*.

*Hidden* content still occupies space on a page and requires some amount of
memory. When ``@if`` evaluates to ``false``, content remains absent from the
page---requiring neither space on the page nor memory. This is an important
consideration when including items like images or videos on your website.

.. _HelloASPDotNET-vid2:

Try It!
-------

The video below provides you some live-coding practice with adding C# logic in Razor
templates. Return to your ``HelloASPDotNET`` project and code along as you watch
the clip.

.. TODO: Add dynamic view video.
.. topic covered: use ViewBag property to display data on template, @foreach, @if

YOUTUBE VIDEO HERE

.. TODO: Create views-dynamic branch.

.. admonition:: Note

   The starter code for this video is found at the 
   `views-static branch <https://github.com/LaunchCodeEducation/HelloASPDotNETDemo/tree/views-static>`__
   of ``HelloASPDotNETDemo``. The final code presented in this video is found on the `views-dynamic branch <TBD>`__.

The text on this page and the previous two provides details for some of the
concepts presented in the clip. Note that these summaries are NOT intended as
a replacement for the walkthrough. To get better at coding, you need to
actually CODE.

Check Your Understanding
------------------------

Assume you have an list of integers called ``numbers``, and you display
the values in an unordered list.

.. sourcecode:: html
   :linenos:

   <ul>
      @foreach(int number in ViewBag.numbers)
      {
         <li>@number</li>
      }
   </ul>

.. admonition:: Question

   You want to display the list only if ``ViewBag.numbers`` contains data. 
   Where is the best spot to put this conditional?

   #. Above line 1
   #. Above line 2 
   #. Above line 3 
   #. Above line 4

.. Answer = a, Above line 1

.. admonition:: Question

   You want to display the list only if ``ViewBag.numbers`` contains data. 
   What is the best way to write this conditional statement?

   #. ``if (numbers.Count)``
   #. ``if (ViewBag.numbers != null)``
   #. ``@if ViewBag.numbers``
   #. ``@if (ViewBag.numbers.Count > 0)``

.. ans: d, ``@if (ViewBag.numbers.Count > 0) {}``
