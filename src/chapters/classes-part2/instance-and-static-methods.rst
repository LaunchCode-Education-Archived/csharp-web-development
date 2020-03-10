Instance and Static Methods
===========================

We explored configuring *data* within classes with fields and properties. Now
let’s turn our attention back to class *behavior* (methods).

Quick Method Review
--------------------

In the :ref:`last chapter <classes-part1>`, we learned that:

#. A method belongs to a class and performs an action.
#. Methods cannot stand on their own---they must be part of a class.
#. To call a method on an object, use dot notation:

   .. sourcecode:: csharp

      objectName.MethodName(arguments);

#. Access modifiers apply to methods:

   a. ``private`` methods are those that are NOT useful outside of the class but
      contribute internally to helping the class behave as desired or expected.
   b. ``public`` methods contain code that other classes need to use when they
      implement the class containing those methods. Make methods ``public``
      only when you expect other classes to use them, and when you are
      committed to maintaining those methods for other programs.

Let's take a closer look at two different types of methods, both of which we
have used in earlier examples.

.. index:: instance method

.. _instance-methods:

Instance Methods
----------------

As we learned in the last chapter, :ref:`instance methods <instance-methods-part1>` define the behaviors that
are *unique* or *specialized* to each class. Every object created from a class
will carry a copy of these methods.

Instance methods depend on the data stored in an individual object. If two
objects call the same method, the results will vary when the objects contain
different data.

Let’s add a couple more instance methods to our ``Student`` class.

What are the behaviors that our ``Student`` class should have? To start, it
makes sense that when a student takes a class and earns a grade, their data
should be updated accordingly. Additionally, it would be nice to easily
identify the grade level of a student---freshman, sophomore, junior, or senior.

The framework for these new methods is shown in the ``Student`` class below,
but each method is missing some code. Filling in that code is left for you to
do in the chapter exercises.

.. sourcecode:: csharp
   :linenos:

   public class Student {

      private static int nextStudentId = 1;
      public string Name { get; set; }
      private readonly int studentId;
      public int NumberOfCredits { get; set; }
      public double Gpa { get; set; }

      public Student(string name, int sId, int numberOfCredits, double gpa)
      {
         Name = name;
         studentId = sId;
         NumberOfCredits = numberOfCredits;
         Gpa = gpa;
      }

      public Student(string name, int sId)
      {
         Name = name;
         studentId = sId;
         NumberOfCredits = 0;
         Gpa = 0.0;
      }

      public Student(string name)
      {
         Name = name;
         studentId = nextStudentId;
         nextStudentId++;
         NumberOfCredits = 0;
         Gpa = 0.0;
      }

      public string StudentInfo()
      {
         return (Name + " has a GPA of: " + Gpa);
      }

      public void AddGrade(int courseCredits, double grade)
      {
         // Update the appropriate fields: NumberOfCredits, Gpa
      }

      public string GetGradeLevel()
      {
         // Determine the grade level of the student based on NumberOfCredits
      }
   }

.. admonition:: Tip

   When creating your classes, think about the behaviors that you want to
   make available, as well as the access level of those methods.

Static Methods
--------------

We’ve already used static methods quite a bit in this course, all the way back
to our first C# method:

.. sourcecode:: csharp
   :linenos:

   static void Main(string[] args)
   {
      // Code here...
   }

Now let’s examine them in the context of what we’ve recently learned about
classes.

.. index:: ! static methods, ! class methods

Just like static fields, **static methods** belong to the class as a whole, and
not to any of the specific instances of the class. Thus, they are sometimes
also called **class methods**. A static method is essentially the opposite of
an instance method, since the two cases are mutually exclusive.
*Instance methods* rely on each object’s specific data, while *static methods*
must NOT rely on data from a specific object.

We call a static method by preceding it with the class name and using
dot-notation. Here’s an example that we looked at
:ref:`previously <static-methods>`.

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

The call occurs in line 9 of ``HelloMethods/Program.cs``: ``Message.GetMessage("fr")``. We call the static
``GetMessage`` without needing an instance of the ``Message`` class. Instead,
we use the name of the class itself.

.. admonition:: Warning

   It is technically allowed to call a static method using an instance of a
   class: ``myObject.SomeStaticMethod()``. However, best practice recommends
   using the class name instead: ``ClassName.SomeStaticMethod()``. This makes
   it clear to other coders that you are calling a static method.

A method should be static when it does NOT refer to any instance fields of the
containing class (it *may* refer to static fields, however). These methods tend
to be utility-like (e.g. carrying out a calculation, or using or fetching some
external resource).

Accessing Static vs. Instance Fields
------------------------------------

One common error new C# coders encounter is when a *static method* tries to call an *instance variable*.
This is because static methods cannot call instance variables.
Static methods can be called from anywhere (depending on
their access modifier), and they do NOT require us to create an object for a
particular class. However, these methods must be independent of any values
unique to a particular object, such as instance variables.

For example, if we have a ``Circle`` class, then we can define and call a
static ``Area`` method without creating a new object:
``Circle.Area(radius)``. Since the area of a circle is just,
``PI*radius*radius``, we can pass in the argument when we call the method. The
method does not depend on any value stored within a specific ``Circle`` object.

Now let's assume we define a ``Car`` class with an instance variable for
``color``. The value of this field will NOT be the same for every ``Car``
object we create. Thus, trying to call a static method like
``Car.PrintColor()`` results in an error. Since there is no single value for
``color`` that applies to every object, trying to access it from outside of the
class does not work. To print the color of a ``Car`` object, we must call the
method on that specific object: ``myCar.printColor()``.

Instance fields can only be called by instance methods.

.. admonition:: Note

   While static methods cannot access instance variables, an instance method
   CAN access a static variable. Why?


Check Your Understanding
------------------------

.. admonition:: Question

   Assume that we add two methods to a ``Pet`` class---``public String MakeNoise()``
   and ``public static void IncreaseAge()``. Which of the following statements is
   true?

   #. The ``MakeNoise()`` method can be accessed outside of the ``Pet`` class,
      while the ``IncreaseAge()`` method cannot.
   #. Each ``Pet`` object carries a copy of the ``MakeNoise()`` method but NOT
      a copy of the ``IncreaseAge()`` method.
   #. The ``IncreaseAge()`` method can be accessed outside of the ``Pet`` class,
      while the ``MakeNoise()`` method cannot.
   #. Each ``Pet`` object carries a copy of the ``IncreaseAge()`` method but
      NOT a copy of the ``MakeNoise()`` method.

.. The correct answer is "b".

.. admonition:: Question

   Explain why it IS possible for an instance method to access a static field.

.. There is no problem with this because static variables belong to a class and
   can be called from anywhere (depending on the access modifier). Thus, any
   instance method can access them from outside of the class where they are
   defined.
