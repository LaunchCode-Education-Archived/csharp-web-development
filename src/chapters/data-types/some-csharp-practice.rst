Some C# Practice
================
Example: The TempConv Program
-----------------------------

Let’s go back in time and look at one of our very early Python programs.
Here is a simple Python function to convert a Fahrenheit temperature to
Celsius.

.. code:: python

   def main():
       fahrenheit = int(input("Enter the temperature in F: "))
       celsius = (fahrenheit - 32) * (5.0 / 9.0)
       print("the temperature in C is: ", celsius)

   if __name__ == '__main__':
       main()

Next, lets look at the C# Equivalent.

.. code:: csharp

   using System;

   namespace TempConv
   {
       class Program
       {
           public static void Main(string[] args)
           {
               double fahrenheit;
               double celsius;
               string input;

               Console.WriteLine("Temperature in F:");
               input = Console.ReadLine();
               fahrenheit = double.Parse(input);

               celsius = (fahrenheit - 32) * 5 / 9;
               Console.WriteLine("The Temperature in C is: " + celsius);
               Console.ReadLine();
           }
       }
   }

There are several new concepts introduced in this example. We will look
at them in the following order:

-  ``using`` statement
-  Variable declaration
-  Input/output and the ``Console`` class

using
~~~~~

In C#, you can use any class that is available without having to import
the class - subject to two very important conditions:

1. The C# compiler must know that the class exists
2. You must use the full name of the class

You can think of the ``using`` statement in C# as working a little bit
like the ``from module import xxx`` statement in Python. However, behind
the scenes the two statements actually do very different things.

The first important difference to understand is that the class naming
system in C# is very hierarchical. The *full* name of the ``Console``
class is really ``System.Console``. You can think of this name as having
two parts. The first part, ``System``, is called the **namespace**, and
the last part is the **class. We’ll talk more about the class naming
system a bit later. The second important difference is that it is not
the ``using`` statement’s responsibility to load classes into memory.
That task falls on the**\ assembly**, which is the unit of compiled code
created by Visual Studio (or the C# compiler, more generally).

The ``using`` statement tells the compiler that we are going to use a
shortened version of the class’s name. In this example we are going to
use the class ``System.Console``, but we can refer to it as just
``Console``. We could use the ``System.Console`` class without any
problem and without any import statement provided that we always
referred to it by its full name.

Don’t just trust us, try it yourself! Remove the ``using`` statement and
change ``Console`` to ``System.Console`` in the rest of the code. The
program should still compile and run.

Declaring Variables
~~~~~~~~~~~~~~~~~~~

In the example above, these lines contain variable declarations:

.. code:: csharp

   double fahrenheit;
   double celsius;
   string input;

Specifically we are saying that ``fahrenheit`` and ``celsius`` are going
to reference objects that are of type ``double``. The variable ``input``
will contain a string. This means that if we were to try an assignment
like ``fahrenheit = "xyz"`` the compiler would generate an error because
``"xyz"`` is a string and ``fahrenheit`` is supposed to be a double.

For Python programmers the following error is likely to be even more
common. Suppose we forgot the declaration for ``celsius`` and instead
left that line blank. What would happen if we try to run our program?

.. figure:: build-error.png
   :alt: Build error

   Build error

The compiler detects an error and Visual Studio displays this message.
Were you to look at the error pane, you would see the message: “The name
‘celsius’ does not exist in the current context”.

.. raw:: html

   <aside class="aside-note">

When using an IDE such as Visual Studio, your code is typically checked
by the IDE’s built-in compiler as you write your code. Thus, errors are
usually visually indicated within your code by the IDE as you write your
code, saving you the extra step of having to explicitly compile your
code before finding compiler errors. Nice, huh?

.. raw:: html

   </aside>

The general rule in C# is that you must decide what kind of an object
your variable is going to reference and then you must declare that
variable before you use it. There is much more to say about the static
typing of C# but for now this is enough.

Input / Output and the Console Class
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Console input and output is facilitated by the class ``System.Console``.
We’ll rely heavily on just two methods of this class:
``Console.WriteLine`` and ``Console.ReadLine``.

``Console.WriteLine`` can take parameters of various types, including
``string``, ``char``, ``double``, ``bool``, and others. However, unlike
the ``print`` function in Python, we can only provide it with a single
argument. Thus, we’ll need to manually concatenate strings and other
values, converting types if necessary. As with Python, a newline
character is output after the given message.

.. code:: python

   year = 2017
   print("Hello", "World")
   print("The year is:", year)

.. code:: csharp

   int year = 2017;
   Console.WriteLine("Hello" + "World")
   Console.WriteLine("The year is " + year.ToString());

Similarly, ``Console.ReadLine`` returns input as a string. To convert it
to a desired type, you can generally use the syntax
``[TYPE].Parse(value)``, with ``[TYPE]`` replaced by the given type.
Here’s an example:

.. code:: csharp

   string userInput = Console.ReadLine();
   int year = int.Parse(userInput);

This is very similar to what we did in Python:

.. code:: python

   user_input = input()
   year = int(user_input)