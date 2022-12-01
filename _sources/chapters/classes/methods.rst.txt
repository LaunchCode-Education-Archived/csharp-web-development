Methods
=======

Calling Methods on Objects
--------------------------

.. index:: method

A **method** is a function that belongs to a class. In C#, all procedures
must be part of a class. Let’s revisit our ``HelloWorld`` class.

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

There is one method in this class, ``SayHello()``. In order to call this
method, we must have an object created from the ``HelloWorld`` class
template. In other words, we must have an instance of ``HelloWorld``.

Here’s how you call methods on an object.

.. sourcecode:: c#

   HelloWorld hello = new HelloWorld();
   hello.SayHello();

It is not possible to call ``SayHello()`` without having a ``HelloWorld``
object. This begins to make more sense when you note that the
``message`` field is used within ``SayHello()``, and unless we are calling
``SayHello()`` on an instantiated object, there will be no ``message``
field available to print.

.. note::

   As mentioned before, class members should have the most restrictive
   level of access possible. This goes for methods as well as fields. For
   example, if you create a utility method that should only be used within
   your class, then it should be ``private``. You can think of ``private``
   methods as those that are not useful *outside* of the class, but that
   can contribute internally to helping the class behave as desired or
   expected.

   On the contrary, ``public`` methods are code that other classes will
   want to use when they implement the class containing those ``public``
   methods. So only make methods ``public`` when you expect other classes
   to use them, and when you are committed to maintaining those methods for
   other calling programs that may use them.

.. index:: ! instance method

.. _instance-methods-part1:

Instance Methods
----------------

So far, we’ve only looked at examples of methods that are relatively
specialized: constructors, getters, and setters. Every class you create
will have these methods. What will make your classes different from each
other, and thus fulfill the purpose of creating each class, are the
specific behaviors that are unique to your classes.

Let’s say we want to add a method in our ``Student`` class that reports the GPA
of a student. This method is an **instance method** since it will belong to
each ``Student`` object created, and will use the data of each such object.

.. sourcecode:: c#
   :linenos:

   public class Student 
   {

      private static int nextStudentId = 1;
      public string Name { get; set; }
      public int StudentId { get; set; }
      public int NumberOfCredits { get; set; }
      public double Gpa { get; set; }

      public Student(string name, int studentId,
            int numberOfCredits, double gpa)
      {
         Name = name;
         StudentId = studentId;
         NumberOfCredits = numberOfCredits;
         Gpa = gpa;
      }

      public Student(string name, int studentId)
        : this(name, studentId, 0, 0) {}

      public Student(string name) 
         : this(name, nextStudentId)
      {
         nextStudentId++;
      }

      public string StudentInfo() 
      {
         return (Name + " has a GPA of: " + Gpa);
      }

   }

We will make use of instance methods more in the next chapter, but now you know the basics of
how to add additional behaviors to our classes.

.. admonition:: Note

   Above, we've added some functionality to increment the ``studtentId`` property, too.

Check Your Understanding
------------------------

.. admonition:: Question

   Fill in the blanks with the appropriate terms.

   - A _____________ gives a class property a field.

   - A _____________ gives a programmer access to the value of a private class property.

   - A _____________ creates a new instance of a class.

   - A _____________ is a method that belongs to each occurrence of a class.

.. ans: setter, getter, constructor, instance method
