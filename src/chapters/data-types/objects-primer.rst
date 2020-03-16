Objects and Methods, A Primer
=============================

There is a lot to say about objects in C# that we'll cover in due time. Here, we highlight some introductory 
concepts of how C# works as an object-oriented programming language.

.. index:: object

Objects
-------

In C#, **objects** are structures that have a *state* and a set of
*behaviors*. The state of an object includes properties/data that the coder can
define and modify. Behaviors are actions that run when requested, and they can
be used to evaluate, manipulate, or return data.

As we've said several times now, every variable in C# refers to an object.

The ``string`` data type is an object. For
``string language = "C#"``, the data would be the characters. The
:ref:`string manipulation <string-methods>` section gives several of the
behaviors available to the ``language`` object. For example,
``language.length()`` returns the value ``4``, which tells us how many
characters are present in the string.

An :ref:`array <array>` is also an example of an object. It contains *data*, which are the values
stored as the individual elements. The *behaviors* are methods not unlike those listed in the 
string manipulation table that perform actions related to the elements in the array. We haven't 
provided an array methods table, but you can explore array methods in 
`the docs <https://docs.microsoft.com/en-us/dotnet/api/system.array?view=netframework-4.8#methods>`__.

.. index:: ! method, ! static

.. _static-methods:

Static Methods
--------------

In pure object-oriented languages like C# and Java, we don’t have
functions in the sense you may be used to. Functions may not be declared
outside of a class. Within the context of a class, functions are
referred to as **methods**. We’ll adopt this terminology from now on.

We’ll dive into learning about classes and objects in C# soon enough,
but first let’s learn a little about **static methods**, which behave
somewhat similarly to stand-alone functions. A static method is one that 
can be called without creating an object instance of the class to which it belongs.

.. admonition:: Example

   Define the class ``Cat`` and include the ``static`` keyword before the
   ``makeNoise`` method name:

   .. sourcecode:: c#
      :linenos:

      public class Cat {
         public static void MakeNoise(String[] args) {
            // some code
         }
      }

   Since ``makeNoise`` is ``static``, we do NOT need to create a ``Cat`` object to
   access it.

   Instead of doing this:

   .. sourcecode:: c#
      :linenos:

      Cat myCat = new Cat();     // Create a new Cat object.
      myCat.MakeNoise("purr");   // Call the MakeNoise method.

   We can call the method directly:

   .. sourcecode:: c#
      :linenos:

      Cat.MakeNoise("roar");

Until we get further into object oriented programming, every method you write
should use the ``static`` keyword. Leaving off ``static`` will prevent or
complicate the process of calling the methods you defined.

We will explore exactly what ``static`` does in more detail in later lessons.

.. _hello-methods:

``HelloMethods``
----------------

Let’s examine two classes in C# to explore defining and using methods. Open the 
``HelloMethods`` project in ``csharp-web-dev-lsn1datatypes``.

The first class is defined in the ``HelloMethods/Program.cs`` file, and it has a
``Main`` method. The second class is defined in a separate ``HelloMethods/Message.cs``
file, and it contains a ``GetMessage`` method that we want to call from within
``Main``.

.. admonition:: Examples

   ``HelloMethods/Program.cs``:

   .. sourcecode:: c#
      :linenos:

      using System;

      namespace HelloMethods
      {
         public class Program
         {
            public static void Main(string[] args)
            {
                  string message = Message.GetMessage("fr");
                  Console.WriteLine(message);
                  Console.ReadLine();
            }
         }
      }

   ``HelloMethods/Message.cs``:

   .. sourcecode:: c#
      :linenos:

      namespace HelloMethods
      {
         public class Message
         {
            public static string GetMessage(string lang)
            {
                  if (lang.Equals("sp")) {
                     return "Hola Mundo";
                  }
                  else if (lang.Equals("fr"))
                  {
                     return "Bonjour le monde";
                  }
                  else
                  {
                     return "Hello World";
                  }
            }
         }
      }


We won’t explore every new aspect of this example, but rather will focus
on the two methods.

#. The ``Main`` method in the ``HelloMethods/Program.cs`` class has the same structure as
   that of our :ref:`temperature conversion example <temp-conversion>`.
#. Take a look at the ``Message`` class. Note that it does NOT have a ``Main``
   method, so it can’t be run on its own. Code within the ``Message`` class
   must be called from elsewhere in order to execute.
#. The ``Message`` class contains the ``GetMessage`` method. Like ``Main``, it
   has the ``static`` keyword. Unlike ``Main``, ``GetMessage`` has a return
   type of ``string`` instead of ``void``.
#. ``GetMessage`` takes a single ``string`` parameter, ``lang``.

Since C# is statically typed, each method must declare its return type -
that is, the data type of what it will return - along with the type of
each parameter. One consequence of this that may not be immediately
obvious is that methods in C# may not return different types of data.
For example, we would not be able to replace the last ``return``
statement of ``GetMessage`` with something like ``return 42;``. This
would be flagged as a compiler error.

``Main`` Methods
^^^^^^^^^^^^^^^^

In a C# project, only one ``Main`` method is allowed. When the project is
compiled and run, the ``Main`` method indicates what should be executed,
and if there were multiple ``Main`` methods this would be ambiguous.

Public Methods
^^^^^^^^^^^^^^

.. index:: ! public

Finally, let’s note how a static method is called. The first line of
``Main`` in the ``Program`` class is:

.. sourcecode:: c#

   Message.GetMessage("fr");

To call a static method, we must use the name of the class in which it is
defined, followed by ``.``, followed by the name of the method.

.. sourcecode:: c#

   ClassName.methodName(arguments);

We are able to call this method from another class because it is
declared to be ``public``. If we wanted to restrict the method from
being called by another class, we could instead use the ``private``
modifier. We’ll explore *access modifiers* in more depth in coming
lessons.

.. admonition:: Note

   As you have been following along with these examples, you may have noticed
   that each class file, for example ``Message.cs`` and
   ``Program.cs``, is named exactly the same as the class it holds
   (``Message`` and ``Program``, respectively).

   There is *NOT* a rule in C# dictating that a file must be named the same as the class it contains, 
   but it is considered best practice.

Try It
^^^^^^^
Poke around with the ``HelloMethods`` project in Visual Studio and experiment with the
following:

#. Figure out how to alter the ``HelloMethods`` code to change the message
   returned.
#. Add another "Hello, World" language option.
#. Change one ``public`` keyword to ``private`` to see what happens. Repeat for
   each occurrence of ``public``.

Check Your Understanding
-------------------------

.. admonition:: Question

   Which of the following defines a method that takes an integer as a parameter
   and returns a string value?

   #. ``public static void MethodName(string parameterName)``
   #. ``public static void MethodName(int parameterName)``
   #. ``public static int MethodName(string parameterName)``
   #. ``public static string MethodName(int parameterName)``

.. ans: d, ``public static string MethodName(int parameterName)``

.. admonition:: Question

   True/False: A C# program may contain more than one ``Main`` method, as long as at least one of those 
   methods is marked ``private``.

   #. True
   #. False

.. ans: False, a C# project may only contain one main method

