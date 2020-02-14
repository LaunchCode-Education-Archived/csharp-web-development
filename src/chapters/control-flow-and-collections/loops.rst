Loops
=====

.. index:: ! for loop

``for`` Loop
-------------

In C#, we write a definite loop (aka a **for loop**) as:

.. sourcecode:: csharp
   :linenos:

   for (int i = 0; i < 10; i++ ) {
      Console.WriteLine(i);
   }

**Output:**

.. sourcecode:: bash

   0
   1
   2
   3
   4
   5
   6
   7
   8
   9

.. note::

   You may not be familiar with the expression ``i++`` since it is not
   found in all languages. The ``++`` is an increment operator that has the same
   effect as ``i += 1``. In this example, since the ``++`` comes after
   ``i``, we call it a postfix increment operator. There is also a ``--``
   decrement operator in C#. For more information, see the documentation on 
   `Arithmetic Operators <https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/operators/arithmetic-operators>`__.


The C# ``for`` loop gives you explicit control over the starting, stopping,
and stepping of the loop variable inside the parentheses. You can think of it
this way:

.. sourcecode:: csharp
   :linenos:

   for (start clause; stop clause; step clause) {
      statement1
      statement2
      ...
   }

If you want to start at 100, stop at 0 and count backward by 5, the loop is written as:

.. sourcecode:: csharp
   :linenos:

   for (int i = 100; i >= 0; i -= 5) {
      Console.WriteLine(i);
   }

**Output:**

.. sourcecode:: bash

   100
   95
   90
   ...

.. index:: ! foreach loop

``foreach`` Loop
------------------

C# also provides a syntax to iterate over any sequence or collection, such as an array: 

.. sourcecode:: csharp
   :linenos:

   int nums[] = {1, 1, 2, 3, 5, 8, 13, 21};

   foreach (int i in nums) {
      Console.WriteLine(i);
   }

Here, the loop variable moves through the items in the array of integers, ``nums[]``. The syntax
here uses the word, ``in``. This type of loop is known as a **foreach loop**.

.. tip::

   When considering this structure, it can be helpful to read the code sample above to yourself
   as "For each integer in array ``nums``...".

This loop version also works with a string, where we
can convert the string to an Array of characters:

.. sourcecode:: csharp
   :linenos:

   string msg = "Hello World";

   foreach (char c in msg.ToCharArray()) {
      Console.WriteLine(c);
   }

As you see, to iterate through a string in this way, C# requires an extra string method,
``.ToCharArray()``, to convert the string to an Array of characters.

.. index:: ! while loop

``while`` Loop
--------------

C# also supports the **while loop**, or indefinite loop.
A ``while`` loop in C#:

.. sourcecode:: csharp
   :linenos:

   int i = 0;
   while (i < 3) {
      i++;
   }

.. index:: ! do-while loop

``do-while`` Loop
-----------------

C# adds an additional, if seldom used, variation of the ``while`` loop
called the **do-while loop**. The ``do-while`` loop is very similar to
``while``, except that the condition is evaluated at the end of the loop
rather than the beginning. This ensures that a loop *will be executed at
least one time*. In some situations, the ``do-while`` loop is preferable, because it avoids an additional assignment prior to the loop.

For example:

.. sourcecode:: csharp
   :linenos:

   do {
      Console.WriteLine("Hello, World");
   } while (false);

**Output:**

.. sourcecode:: bash

   Hello, World

Above, the message prints despite the condition never being met.

Break Statements in Loops
-------------------------

There are instances where you may want to terminate a loop if a given
condition is met. In these instances, the ``break`` statement comes in
handy. For example, say you want to loop through an Array of integers
to search for a given value. Once that number is found, you want to quit
the loop. You can do the following:

.. sourcecode:: csharp
   :linenos:

   int[] someInts = {1, 10, 2, 3, 5, 8, 10};
   int searchTerm = 10;
   foreach (int oneInt in someInts) {
      if (oneInt == searchTerm) {
         Console.WriteLine("Found it!");
         break;
      }
   }

In the code above, instead of the ``for`` loop iterating through all the
integers in the array, it will stop after it finds the first matching
instance. So once it finds the first ``10`` in the array, it prints "Found
it!" and then terminates the loop. If the ``break`` statement weren’t
there, the loop would continue and when it found the second ``10``, it
would print "Found it!" a second time.

Note that the ``break`` statement terminates the innermost loop that it
is contained within. So if you have nested loops and use a ``break``
statement within the innermost loop, then it will only terminate that
loop and not the outer one. If a ``break`` is present in the outer loop,
it --- and any other block nested within it --- is terminated when the
``break`` runs.

.. index:: ! continue

Continue Statements in Loops
----------------------------

The **continue** statement is similar to, but importantly different
from, the ``break`` statement. Like ``break``, it interrupts the normal
flow of control of the loop. But unlike ``break``, the ``continue``
statement only terminates the *current iteration* of the loop. So the
loop will continue to run from the top (as long as the boolean
expression that controls the loop is still true) after a ``continue``
statement. Here is an example:

.. sourcecode:: csharp
   :linenos:

   int[] someInts = {1, 10, 2, 3, 5, 8, 10};
   int searchTerm = 10;
   foreach (int oneInt in someInts) {
      if (oneInt == searchTerm) {
         Console.WriteLine("Found it!");
         continue;
      }
      Console.WriteLine("Not here");
   }

The above program will print "Not here" on every iteration of the
``for`` loop *except* where the number has been found. So the output
looks like this:

.. sourcecode:: bash

   Not here
   Found it!
   Not here
   Not here
   Not here
   Not here
   Found it!

Because of the ``continue`` statement, the final print statement in the
for loop is skipped. If the ``continue`` statement weren’t there, the
output would look like this instead (notice the extra "Not here"
printouts):

.. sourcecode:: bash

   Not here
   Found it!
   Not here
   Not here
   Not here
   Not here
   Not here
   Found it!
   Not here

Check Your Understanding
-------------------------

.. admonition:: Question

   .. sourcecode:: csharp
      :linenos:

      char[] chars = {'p', 'l', 'r', 's', 't'};

      for (<loop-statement>) {
         Console.WriteLine(i);
      }

   What does the missing <loop-statement> need to be to print each item in ``chars``?

   #. ``char i : chars``
   #. ``char i : chars[]``
   #. ``char i in chars``
   #. ``char i in chars[]``

.. ans: ``char i : chars``

.. admonition:: Question

   .. sourcecode:: csharp
      :linenos:

      do {
         Console.WriteLine("Hello world!");
      } while (3 < 2);

   How many times does the message print and why?

   #. 0 --- The ``while`` condition is never true.
   #. 1 --- The print statement is evaluated before the conditional.
   #. infinite times --- 3 is less than 2, and the condition is never changed in the loop.

.. ans: 1 --- The print statement is evaluated before the conditional.
