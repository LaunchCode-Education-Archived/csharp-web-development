Data Types
===========

Static vs. Dynamic Typing
-------------------------

.. index:: ! dynamically typed, ! statically typed

In a **dynamically typed** programming language (like JavaScript or Python), a
variable or parameter can refer to a value of any data type (string, number,
object, etc.) at any time. When the variable is used, the interpreter figures
out what type it is and behaves accordingly.

C# is a **statically typed** language. When a variable or parameter is
declared in a statically typed language, the data type for the value must be
specified. Once the declaration is made, the variable or parameter cannot refer
to a value of any other type.

For example, this is legal in JavaScript, a dynamically typed language:

.. admonition:: Example

   .. sourcecode:: JavaScript
      :linenos:

      let dynamicVariable = "dog";
      console.log(typeof(dynamicVariable));
      dynamicVariable = 42;
      console.log(typeof(dynamicVariable));

   **Output**

   .. sourcecode:: bash

      string
      number

After line 1 executes, ``dynamicVariable`` holds a ``string`` data type. After
line 3 runs, ``dynamicVariable`` becomes a ``number`` type. ``dynamicVariable``
is allowed to hold values of different types, which can be reassigned as
needed when the program runs.

However, the corresponding code in C# will result in a build error:

.. admonition:: Example

   .. sourcecode:: c#
      :linenos:

      string staticVariable = "dog";
      staticVariable = 42;

   **Output**

   .. sourcecode:: bash

      Error CS0029: Cannot implicitly convert type 'int' to 'string' (CS0029) 

The compiler error occurs when we try to assign ``42`` to a variable of type
``string``.

Take-home lesson: *We must declare the type of every variable and parameter in
a statically typed language*. This is done by declaring the data type for the
variable or parameter BEFORE its name, as we did in the example above:
``string staticVariable = "dog"``.

.. admonition:: Note

   We only need to specify the type of a variable or parameter when declaring
   it. Further use of the variable or parameter does not require us to identify
   its type. Doing so will result in an error.

.. admonition:: Warning

   It is allowed in some situations in C# to declare a variable without
   specifying a type by using the keyword ``var``, as in
   ``var x = "dog";``. In this case, C# still assigns a type to ``x``
   through inference. It looks and sees that we are assigning ``x`` the
   value ``"dog"``, which is a ``string``. Thus, ``x`` has type ``string``
   and attempting to assign ``x = 42`` will still result in a build error.

   We recommend avoiding use of ``var`` while you are learning C#. Even
   after you become more experienced with the language you will still only
   want to use it sparingly and in specific circumstances. Explicitly
   declaring the type of your variables makes for more readable code, in
   general.

.. index:: ! type system

Dynamic and static typing are examples of different `type
systems <https://en.wikipedia.org/wiki/Type_system>`__. The **type system** of
a programming language is one of the most important high-level characteristics
that programmers use when discussing the differences between languages. Here
are a few examples of popular languages falling into these two categories:

#. **Dynamic**: Python, Ruby, JavaScript, PHP
#. **Static**: C#, C, C++, Java, TypeScript

Because we need to give plenty of attention to types when writing C# code,
let’s begin by exploring the most common data types in this language.

Built-In Types
--------------

In C#, all of the basic data types are objects --- we'll get into this idea shortly. Though the so-called 
built-in data types also have short names that differ from typical class name
conventions.

We provide here a list of some of the most common types, along with the official .NET class name. 
Recall that .NET gives us a class library with 
object types. We’ll generally prefer to use the short names for
each of these.

.. list-table:: Some Built-In Types in C#
   :header-rows: 1

   * - Short name
     - .NET Class
     - Examples
     - Notes 
   * - ``int``  
     - ``Int32``
     - -5, 1024 
     -
   * - ``float``
     - ``Single`` 
     - 1.212, 3.14 
     -
   * - ``double``
     - ``Double``
     - 3.14159, 2.0
     - Doubles are twice as precise (i.e. can hold much longer decimal numbers than floats) 
   * - ``char``
     - ``Char``
     - ‘a’, ‘!’ 
     - A single Unicode character. Must be enclosed in single quotes ``''`` to be a character; double 
       quotes ``""`` indicate a string 
   * - ``bool``
     - ``Boolean``
     - ``true``, ``false``
     - Note that booleans in C# are not capitalized as they are in Python 

.. admonition:: Warning

   As we will see in a later section, the ``float`` data type sacrifices some
   accuracy for speed of calculation. Thus, evaluating 1.11111 + 3 results in an
   answer of 4.1111097 instead of 4.11111.

   Anytime you need to perform calculations with decimal values, consider using
   the ``double`` type instead of ``float``.

Not all built-in data types in C# are listed here, only the most
commonly used types that beginners are likely to encounter. If you’re
curious, `read more about built-in types in
C# <https://msdn.microsoft.com/en-us/library/ya5y69ds.aspx>`__.

.. index:: ! primitive type

Primitive Types
^^^^^^^^^^^^^^^

The types in the table above are known as **primitive types**. A primitive data type is a basic 
building block of a programming language. Using primitive data types, we
can build more complex data structures.

Non-primitive Types
^^^^^^^^^^^^^^^^^^^

Primitive data types are *immutable* and can be combined to build larger data
structures. One example is forming the ``string`` "LaunchCode" from multiple
``char`` characters (``'L'``, ``'a'``, ``'u'``, etc.).

``string`` is another built-in type in C# and it is also a non-primitive data type. We'll delve into 
how strings work in C# on the next page, as well as other complex data types.


Operations
^^^^^^^^^^

Operators, such as ``+`` and ``*``, are type-dependent.
That is, we can only use them on allowed types, and their effects are
different depending on which types we use them on. The ``+`` operator is
a good example of this. We can use ``+`` to add numeric types together,
such as ``2 + 2`` which results in ``4``. But we can also use it to
concatenate strings: ``"2" + "2"``, for example, which results in
``"22"``. What the operators do depends on the type they are operating
on, and we may not mix types in arbitrary ways (``"2" + 2`` results in a
compiler error).

.. admonition:: Note

   Numeric types such as ``int`` and ``double`` may be freely mixed when
   using numeric operators. Generally, the result of such mixing is that
   the output has the type of the more precise input. For example, the
   following snippet would print out ``System.double``.

   .. sourcecode:: c#

      float a = 2;
      double b = 3;
      Console.WriteLine((a + b).GetType());

.. _reference-variable:

Reference and Value Types
-------------------------

We can group types in C# into two categories: **value types** and
**reference types**. Variables holding value types directly contain
their data, and include numeric types (``int``, ``double``, etc.),
``bool``, and a handful of others that we won’t encounter in this
course. The primitive, built-in types we list above are all value types.

.. index:: ! class

Class Types
^^^^^^^^^^^

A **class** is a template for creating objects. In addition to the built-in 
types provided by .NET, any class in C# defines its own type. A class is a template, 
or blueprint, for creating objects. We’ll have much more to say about classes and objects --- this 
is an object-oriented course, after all. For now, you need to be 
comfortable seeing the basic syntax of class types and class creation.

If we have a class ``Cat`` with a constructor that takes no arguments, we
declare and create a new instance of ``Cat`` using its constructor.

.. sourcecode:: c#

   Cat myCat = new Cat();

#. ``Cat myCat`` declares the variable ``myCat`` and sets it to be of type
   ``Cat``.
#. ``= new Cat()`` initializes the variable with a new ``Cat`` object.
#. Any arguments that are required to build the new ``Cat`` object must be
   included within the parentheses. In this case, there are no required arguments.

This statement creates a new variable that is initialized to
hold a new ``Cat`` object. Note that in C#, we must declare the
variable’s type. Also note that we precede the constructor with the
``new`` keyword. And, as we'll see with all C# statements, the 
declaration ends with a semi-colon.

Variables and parameters that are of the type of a class are said to be
of **reference type** (in contrast to **primitive type**). In plain
English, we would say of the C# example: “``myCat`` is a reference
variable of type ``Cat``.”

As mentioned above, classes define reference types. A variable of a
reference type (such as ``myCat`` above) does not actually store the
object in question. Instead, it stores a **reference** to the object. A
reference is literally a memory address. We visualize references as an
arrow pointing to the object in memory.

Consider this code:

.. sourcecode:: c#

   int catAge = 11;
   Cat myCat = new Cat();
   Cat sameCat = myCat;

Visually, we can represent these three variables as shown here.

.. figure:: figures/references.png
   :alt: Reference Types

   Reference Types

Since ``int`` is a value type, the variable ``catAge`` functions as a
box holding the integer value 11. On the other hand, ``myCat`` is a
reference variable, since it refers to an object of type ``Cat``. The 
variable actually stores the memory address of the object, which we visualize 
as an arrow from the variable box to the object. Instead of holding the actual ``Cat``
data, ``myCat`` stores *directions* for finding the data in memory.

When we assign ``myCat`` to another variable, as in ``Cat sameCat = myCat``,
we do NOT create a second copy of the object or its data. Instead, we make a
second *pointer* to the same memory location.

The distinction between reference types and value types is important,
but can be difficult to wrap your brain around at first. We will see
that reference types are handled differently in essential and important
ways in a lot of different situations.

.. index:: ! boxing, ! unboxing 

Boxing
^^^^^^

As we mention above, all types in C# are treated as objects. Even value types. This can be accomplished 
through processes called boxing and unboxing. Converting from a value type to a reference type is called 
**boxing**, and the reverse process (reference to value) is called **unboxing**. C# is known as a unified 
type system because it implicitly boxes values types to be treated as objects. 


Check Your Understanding
-------------------------

.. admonition:: Question

   Which of the following is NOT a number data type in C#:

   #. ``number``
   #. ``int``
   #. ``float``
   #. ``double``

.. ans: a, ``number``

.. admonition:: Question

   Which of the following terms refers to C#'s behavior of treating all types as objects:

   #. static type system
   #. dynamic type system
   #. reference type system
   #. unified type system

.. ans: d, unified type system
