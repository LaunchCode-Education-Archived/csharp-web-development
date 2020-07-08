A Primer on Lambda Expressions
==============================

Before diving into relationships in EF, we need to introduce a new concept.

.. index:: ! lambda expression

A **lambda expression** is an *inline* function defined using the symbol ``=>``. This symbol is sometimes called a "fat arrow," and lambda expressions are sometimes called "fat arrow functions." The most basic syntax for creating a lambda expression is:

::

   argument => return expression

The left-hand side of the expression consists of the arguments to be passed into the function, and the right-hand side states the return expression. There are more complicated ways to write a lambda expression, but we will only use this one.

Lambda expressions can seem confusing until you see them in action. We will look at some below.

.. index:: ! Select

``Select`` Example
------------------

The ``Select`` method for arrays can be used to create a new array with elements that are *transformations* of elements of an initial array.

.. admonition:: Example

   .. sourcecode:: csharp
      :linenos:

      using System;
      using System.Linq;

      class MainClass {
         public static void Main (string[] args) {
            int[] nums = {1, 2, 3, 4};
            var doubledNums = nums.Select(x => 2*x);
            Console.WriteLine(string.Join(" ", doubledNums));
         }
      }

   **Output**

   :: 

      2 4 6 8

Let's look at line 7 in more detail.

.. sourcecode:: csharp
   :lineno-start: 7

   var doubledNums = nums.Select(x => 2*x);

The ``Select`` method takes a lambda expression as a parameter. The lambda expression is ``x => 2*x``. This is a function that takes a single element of the ``nums`` array, as represented by x on the left side of the expression, and returns the results of multiplying each of those array elements by 2. We can think of the execution of ``Select`` as follows:

#. ``Select`` begins by creating an empty array. This array will be returned at the end of the method.
#. It then loops over ``nums``.
#. Within the loop, each entry of ``nums`` is passed into the lambda expression.
#. The return value of the lambda expression is appended to the new array.
#. At the end of the loop, ``Select`` returns the new array of transformed values.

.. index:: ! Where

``Where`` Example
------------------

The array method ``Where`` can be used to *filter* elements of an array. In this case, ``Where`` takes a lambda expression that returns a boolean. If the boolean value is ``true`` then the value is included in the returned array. Otherwise, the value is NOT included in the returned array.

.. admonition:: Example

   Given an array of integers, we can use ``Where`` to filter out all of the odds, keeping only evens. Recall that a number ``x`` is even if ``x % 2`` is zero, and is odd otherwise.

   .. sourcecode:: csharp
      :linenos:

      using System;
      using System.Linq;

      class MainClass {
         public static void Main (string[] args) {
            int[] nums = {1, 2, 3, 4};
               var evens = nums.Where(x => (x % 2 == 0));
               Console.WriteLine(string.Join(" ", evens));
         }
      }

   **Output**

   ::

      2 4

In this example, the flow of execution of ``Where`` on line 7 is similar to that of ``Select`` above. The main difference is that instead of *transforming* every element of ``nums``, it is filtered based on the lambda expression ``x => (x % 2 == 0)``.

.. admonition:: Note

   While the examples we have given use arrays, the ``Select`` and ``Where`` methods work with most collection types. More generally, you'll find various specialized methods that use lambdas whenever you encounter a specialized collection type (such as ``DbSet``, as we'll soon see).

Check Your Understanding
------------------------

.. admonition:: Question

   Suppose you have an array of first names, ``firstNames``, of people each with the last name Smith. What lambda expression would you pass to ``Select`` in the following code so that each name is appended by its surname?

   .. sourcecode:: csharp

      var smiths = firstNames.Select(_______);

   #. ``x => "Smith"``
   #. ``x => x + " Smith"``
   #. ``x => x + lastName``
   #. ``x => x == "Smith``

.. ans: b. x => x + " Smith"

.. admonition:: Question

   Given an array of numbers, ``nums``, what lambda expression would you pass to ``Where`` in the following code so that the resulting array consists of only the numbers greater than 42?

   .. sourcecode:: csharp

      var bigNums = nums.Where(______);

   #. ``x => x > 42``
   #. ``x => x == 42``
   #. ``x => 42``
   #. ``x => x < 42``

.. ans: x => x > 42