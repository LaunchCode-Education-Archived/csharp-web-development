Conditionals
============

Control flow statements in C#, conditionals and loops, are very
straightforward.

.. index:: ! if statement

``if`` Statements
-----------------

Let’s consider an **if statement** with no ``else`` clause.

In C#, this pattern is simply written as:

.. sourcecode:: csharp
   :linenos:

   if (condition)
   {
      statement1
      statement2
      ...
   }

You can see that in C#, the curly braces define a block.
Parentheses around the condition are required.

.. index:: ! else clause

``if else``
-----------

Adding an **else clause**, we have:

.. sourcecode:: csharp
   :linenos:

   if (condition)
   {
      statement1
      statement2
      ...
   }
   else
   {
      statement1
      statement2
      ...
   }

.. index:: ! else if

``else if``
-----------

An **else if** construction in C#:

.. sourcecode:: csharp
   :linenos:

   Console.WriteLine("Enter a grade: ");
   string gradeString = Console.ReadLine();
   int grade = int.Parse(gradeString);
   if (grade < 60) 
   {
         Console.WriteLine('F');
   } 
   else if (grade < 70)
   {
         Console.WriteLine('D');
   } 
   else if (grade < 80)
   {
         Console.WriteLine('C');
   }
   else if (grade < 90)
   {
         Console.WriteLine('B');
   }
   else
   {
         Console.WriteLine('A');
   }

.. index:: ! switch, ! case, ! break

.. _switch-statements:

``switch`` Statements
---------------------

C# also supports a **switch** statement that acts something like an
``else if`` statement under certain conditions, called **cases**. The
``switch`` statement is not used very often, and we generally recommend you
avoid using it. It is not as powerful as the ``else if`` model because the
``switch`` variable can only be compared for equality with a very small class
of types.

Here is a quick example of a ``switch`` statement:

.. sourcecode:: csharp
   :linenos:

   Console.WriteLine("Enter an integer: ");
   string dayString = Console.ReadLine();
   int dayNum = int.Parse(dayString);

   string day;
   switch (dayNum) {
      case 0:
         day = "Sunday";
         break;
      case 1:
         day = "Monday";
         break;
      case 2:
         day = "Tuesday";
         break;
      case 3:
         day = "Wednesday";
         break;
      case 4:
         day = "Thursday";
         break;
      case 5:
         day = "Friday";
         break;
      case 6:
         day = "Saturday";
         break;
      default:
         // in this example, this block runs if none of the above blocks match
         day = "Int does not correspond to a day of the week";
         break;
   }
   Console.WriteLine(day);


Note that each case ends with a ``break`` statement.
We will look at why this is in the following section. 

In the example above, here's the output if a user enters the number ``4``.

::

   Enter an integer:
   4
   Thursday

And the output if that user enters ``10``? Below:

::

   Enter an integer: 
   10
   Int does not correspond to a day of the week


Here's how the above example looks using the ``else if`` construction:

.. sourcecode:: csharp
   :linenos:

   Console.WriteLine("Enter an integer: ");
   string dayString = Console.ReadLine;
   int dayNum = int.Parse(dayString);

   string day;
   if (dayNum == 0)
   {
      day = "Sunday";
   }
   else if (dayNum == 1)
   {
      day = "Monday";
   }
   else if (dayNum == 2)
   {
      day = "Tuesday";
   }
   else if (dayNum == 3)
   {
      day = "Wednesday";
   }
   else if (dayNum == 4)
   {
      day = "Thursday";
   }
   else if (dayNum == 5)
   {
      day = "Friday";
   }
   else if (dayNum == 6)
   {
      day = "Saturday";
   }
   else
   {
      day = "Int does not correspond to a day of the week";
   }
   Console.WriteLine(day);

.. index:: ! fallthrough

Fallthrough
^^^^^^^^^^^

Many C-based languages utilize switch statements.
However, not all languages share the same behavior when it comes to **fallthrough**.
Fallthrough is what happens when a ``break`` statement is omitted and is described in detail in this article on `switch statements <https://en.wikipedia.org/wiki/Switch_statement#Fallthrough>`_.
In C#, you can take advantage of fallthrough behavior in specific circumstances with blank cases.
If the behavior we want matches for two cases, then we can take advantage of this fallthrough action.

.. admonition:: Example

   We want to use a switch statement to tell us if it is the weekend or a weekday. Here is how we might modify the switch statement from above and make use of fallthrough.

   .. sourcecode:: csharp
      :linenos:

      Console.WriteLine("Enter an integer: ");
      string dayString = Console.ReadLine;
      int dayNum = int.Parse(dayString);

      string weekZone;
      switch (dayNum) {
         case 0:
            weekZone = "Weekend";
            break;
         case 1:
         case 2:
         case 3:
         case 4:
         case 5:
            weekZone = "Week Day";
            break;
         case 6:
            weekZone = "Weekend";
            break;
         default:
            // in this example, this block runs if none of the above blocks match
            weekZone = "Int does not correspond to a day of the week";
            break;
      }
      Console.WriteLine(day);
   
   Because we want to set the value of ``weekZone`` to ``"Week Day"`` for cases 1-5, we omit the ``break`` statements and any other code.

Check Your Understanding
-------------------------

.. admonition:: Question

   When does fallthrough occur in C#?

   #. Omitting an ``else`` clause from a conditional.
   #. Omitting an ``else`` clause from switch statement.
   #. Omitting a ``default`` case from a ``switch`` statement.
   #. Omitting a ``break`` line from a ``switch`` statement.

.. ans: Omitting a break line from a switch statement.

.. admonition:: Question

   .. sourcecode:: csharp
      :linenos:

      Console.WriteLine("Are you a space cadet? yes or no");
      string response = Console.ReadLine();

      switch (response) {
         case "yes":
            Console.WriteLine("Greetings cadet.");
         case "no":
            Console.WriteLine("Greetings normie.");
         default:
            Console.WriteLine("Are you an alien?");
      }

   Given the code above, what prints if the user enters ``no`` after the prompt?

   #. 
   
      .. sourcecode:: bash
      
         Greetings cadet.
   #. 
   
      .. sourcecode:: bash
      
         Greetings normie.

   #. .. sourcecode:: bash
   
         Greetings normie.
         Are you an alien?
   #. 
   
      .. sourcecode:: bash
      
         Greetings cadet.
         Greetings normie.

   #. The program doesn't work as written.

.. ans:  The program doesn't work as written.
