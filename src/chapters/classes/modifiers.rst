Modifiers in C#
===============

.. index:: ! access level, ! access modifier, ! public, ! private, ! default access, ! assembly, ! world-level

.. _access-modifiers:

Access Modifiers
----------------

For fields in classes, the **access level** determines who can get or set
the value of the field. For methods, the **access level** determines who can
call the method. The access level of a class member is determined by an
**access modifier**.

We’ve encountered access modifiers so far in our code. In our examples, you
frequently see the keyword, **public**. ``public`` makes the field or method to
be accessible by anyone working with our code. Another common access modifier
is **private**, which restricts access to fields or methods so they can only be
used within the class. Two additional access modifiers are available in C#,
though they are used much less often than ``public`` and ``private``.

.. admonition:: Example

   Let's take another look at our ``HelloWorld`` class from the last section,
   but with one small change.

   .. sourcecode:: c#
      :linenos:

      public class HelloWorld 
      {

         string message = "Hello World";

         void SayHello() 
         {
            Console.WriteLine(message);
         }

      }

   In this ``HelloWorld`` class, we omit the ``public`` access modifier in lines
   4 and 6. Doing this implicitly gives the message field and the ``SayHello()``
   method **default access**.

We should avoid giving everything default access when creating classes in C#
and instead think carefully about what level of access each field and method
should have.

The table below details whether or not information can be accessed at different
levels based on the access modifier. For example, a field with the ``private``
access modifier can be accessed within the class, but cannot be accessed
outside the class at the assembly or world-level. In C#, an **assembly** refers
to a grouping of classes and other resources that form a particular unit of an application.
**World-level** is the level of the whole application and contains all of the packages and 
classes. While we will discuss later how to decide which access modifier to use for different
scenarios, you should save this table now as reference for those conversations.

.. _access-modifier-table:

.. list-table:: Is information accessible at certain levels with certain access modifiers?
   :widths: auto
   :header-rows: 1

   + - Modifier
     - Class
     - Assembly
     - World
   + - ``public``
     - Yes
     - Yes
     - Yes
   + - ``protected``
     - Yes
     - No
     - No
   + - ``internal`` (default for classes)
     - Yes
     - Yes
     - No
   + - ``protected internal`` 
     - Yes
     - Yes
     - No
   + - ``private`` (default for class members)
     - Yes
     - No
     - No

.. note::

   If you would like to learn more about access modifiers, you should check out the `documentation <https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/access-modifiers>`_ on the subject.

Let's take a look at our ``HelloWorld`` class again and add some access
modifiers.

.. admonition:: Example

   .. sourcecode:: c#
      :linenos:

      public class HelloWorld 
      {

         private string message = "Hello World";

         public void SayHello() 
         {
            Console.WriteLine(message);
         }

      }

Since ``message`` only needs to be used by ``SayHello()``, we declare it to be
``private``. Since we want ``SayHello()`` to be usable by anybody else, we
declare it to be ``public``.

.. admonition:: Note

   In C#, you should always use the most restrictive access modifier
   possible. Minimizing access to class members allows code to be
   refactored more easily in the future, and hides details of how you
   implement your classes from others.

   This makes your code more modular and modifiable. Each public member
   that you expose is another field or property that can be referenced
   directly elsewhere in any program using your class. Thus, changing any
   such field in your code could potentially break any code referencing
   such members. The fewer public members, the more you can change your
   code without breaking stuff elsewhere.


Check Your Understanding
------------------------

.. admonition:: Question

   For this question, refer to the code block below.

   .. sourcecode:: c#
      :linenos:

      public class Greeting 
      {

         string name = "Jess";

         public void SayHello() 
         {
            Console.WriteLine("Hello " + this.name + "!");
         }
      }

   What access modifier would you give ``name``?

   a. no access modifier
   b. ``public``
   c. ``private``
   d. ``protected``

.. ans: c, private.


