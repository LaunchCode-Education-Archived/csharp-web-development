Exercises: Interfaces and Polymorphism
=======================================

As a new C# coder, it might take you some time to recognize when to use interfaces.

To help overcome this, let's consider a common occurrence---sorting a
``List`` of objects.

#. If the list contains ``string`` or numerical entries, then sorting the list
   is :ref:`trivial <listsort>`:

   .. sourcecode:: csharp

      listName.Sort();

#. However, if the elements are custom objects (like ``Cat``), then sorting the
   list becomes more complicated. This is because the objects may contain
   multiple fields, any of which could be used as a sorting option. For
   ``Cat`` objects, this could include ``name``, ``age``, or ``mass``.

Getting Started
---------------

Fork and clone the `starter code <https://github.com/LaunchCodeEducation/csharp-web-dev-lsn7interfaces>`_ and open up Visual Studio to get started!

You will practice implementing interfaces by playing around with a small ice
cream store. It consists of a refrigerated display ``Case``, which contains
a collection of ice cream ``Flavor`` objects and a selection of ``Cone``
objects.

.. admonition:: Tip

   Did you notice the abstract ``Ingredient`` class? This gets extended by
   ``Flavor`` and ``Cone`` to help streamline the code.

Sorting Flavors by Name
-----------------------

To display a menu for your customers, you need to sort the ice cream flavors
alphabetically by the ``name`` field. Fortunately, the ``IComparer``
interface helps you solve the sorting-objects-by-field problem.

.. admonition:: Tip

   Before proceeding, make sure you have read the section on the :ref:`IComparer interface <icomparer>`!

Create a Sorting Class
^^^^^^^^^^^^^^^^^^^^^^

#. Create a new class called ``FlavorComparer`` and have it implement the
   ``IComparer`` interface:

   .. sourcecode:: csharp

      public class FlavorComparer : IComparer<Flavor>

#. Notice that Visual Studio flags a couple of errors that you need to fix:

   a. Add the namespace ``System.Collections.Generic``.

#. To start sorting, we need a ``Compare()`` method. Add the following code to create one:

   .. sourcecode:: csharp
      :linenos:

      public int Compare(Flavor x, Flavor y)
      {
         return string.Compare(x.Name, y.Name);
      }

   This returns an integer (-1, 1, or 0) depending on
   which ``Flavor`` object ``x`` or ``y`` comes first, alphabetically.

Sorting the ``Flavors`` List
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

In the ``Main`` method in ``Program.cs``, we declare ``menu`` that contains everything in the ``Case``
as well as specific ``availableFlavors`` and ``availableCones`` collections.

.. sourcecode:: csharp
   :lineno-start: 10

   Case menu = new Case();
   List<Flavor> availableFlavors = menu.Flavors;
   List<Cone> availableCones = menu.Cones;

#. To sort the ``availableFlavors`` list, first create a new ``FlavorComparer``
   object.

   .. sourcecode:: csharp
      :lineno-start: 13

      FlavorComparer comparer = new FlavorComparer();

#. Next, call the ``Sort`` method on ``availableFlavors`` and pass the ``comparer``
   object as the argument.

   .. sourcecode:: csharp
      :lineno-start: 15

      availableFlavors.Sort(comparer);

#. Iterating through the ``availableFlavors`` list with a loop before and after the sort shows
   the results. (The output below displays just the ``name`` fields).

   ::

      Before:                 After:

      Vanilla                 Chocolate
      Chocolate               Red Velvet
      Red Velvet              Rocky Road
      Rocky Road              Strawberry Sorbet
      Strawberry Sorbet       Vanilla

.. admonition:: Tip

   Instead of declaring and initializing the ``comparer`` object, we could
   combine steps 1 and 2 by using a single statement:

   .. sourcecode:: csharp

      availableFlavors.Sort(new FlavorComparer());

Sorting Cones by Cost
----------------------

Now let's sort our ``availableCones`` list by cost, from least expensive to most
expensive.

#. Create the new class ``ConeComparer``.
#. Follow the example above to implement the ``IComparer`` interface and
   evaluate ``Cone`` objects by cost.
   Since comparing two numbers is different from comparing strings, try getting the difference between the two numbers. If the difference is positive, then we know the first number is greater. If the difference is negative, then we know that the second number is greater.
#. In the ``Main()`` method, sort the ``availableCones`` list, then print the elements to the screen
   to verify the results.

   ::

      Before:           After:

      Waffle: $1.25        Bowl: $0.05
      Sugar: $0.75         Wafer: $0.50
      Wafer: $0.50         Sugar: $0.75
      Bowl: $0.05          Waffle: $1.25

.. admonition:: Tip

   Remember that the ``cost`` field is of type ``double`` and ``Compare()`` has a return type of type ``int``!

Bonus Mission
-------------

Modify ``FlavorComparer`` to sort ``Flavor`` objects by the number of allergens, from lowest to highest.

Next Steps
----------

In these exercises, you practiced implementing existing interfaces. In the
studio activity, you will design and implement your own.
