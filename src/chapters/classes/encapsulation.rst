Encapsulation
=============

Our discussion of classes and objects is integral to us using **object-oriented programming**.
Object-oriented programming stands on four pillars: abstraction, encapsulation, inheritance, and polymorphism.

.. index:: ! encapsulation

Encapsulation
-------------

**Encapsulation** is the bundling of related data and behaviors that operate on that data, 
usually with restricted access to internal, non-public data and behaviors.
In object-oriented programming, classes and objects allow us to encapsulate, or isolate, 
data and behavior to only the parts of our program to which they are relevant.
Restricting access allows us to expose only that data and behavior that we want others to be able to use.

Let's take a look at this by developing a new class called ``Student``.

``Student`` Class
-----------------

Fields
^^^^^^

We previously defined a **field** as a variable, or piece of data, that
belongs to a class. For our ``Student`` class, let’s think about the
data that is typically associated with a student (in the sense of a high
school or college student). There are a lot of possibilities, but here
are the most important:

1. Name
2. Student ID
3. Number of credits
4. GPA

In order to declare these fields within our class, we’ll need to
determine the best data type for each. A field may be of any primitive
or object type. In this case, the following types will work best:

1. Name: ``string``
2. Student ID: ``int``
3. Number of credits: ``int``
4. GPA: ``double``

Let’s put these inside of a class. While they may be declared anywhere
within a class, fields should always be declared at the top of the
class. When we’re ready to add methods, we’ll add them below the fields.

.. sourcecode:: c#
   :linenos:

   public class Student 
   {
      string name;
      int studentId;
      int numberOfCredits;
      double gpa;
   }

Like variables within a method, fields may be initialized when they are
declared. For example, we could provide default values for
``numberOfCredits`` and ``gpa`` (default values for ``name`` and
``studentId`` don’t make sense since they should be different for each
student).

.. sourcecode:: c#

   int numberOfCredits = 0;
   double gpa = 0.0;

Class members default to ``private`` if no access modifier is provided. This means 
that our ``Student`` fields are inaccessible to code outside of the ``Student`` class. As a
rule-of-thumb, *fields should always be private unless you have a very,
very, very good reason to not make them so.* As we mention on the previous page, it is 
best practice to think carefully about what access to give fields and methods. So, let’s 
explicitly declare our fields to be private.

.. sourcecode:: c#
   :linenos:

   public class Student 
   {
      private string name;
      private int studentId;
      private int numberOfCredits = 0;
      private double gpa = 0.0;
   }


.. index:: ! accessor, ! getter, ! setter, ! auto-implemented property, ! backing field

Getters and Setters
^^^^^^^^^^^^^^^^^^^

In order to provide access to private fields, **getter and setter methods** 
are used. Getters and setters do what you might guess: get and
set a given field. If we make the getter and/or setter method for a
given property public, then others will be able to access or modify the
field in that way.

.. admonition:: Note

   Getter setter methods are also often called **accessors**.

Here is a getter/setter pair for ``name`` (you can imagine how the
others would be written).

.. sourcecode:: c#
   :linenos:

   private string name;

   public string Name
   {
      get { return name; }
      set { name = value; }
   }

Here, within ``get`` and ``set``, ``name`` refers to the private field 
that stores the value of the property. In ``set``, the special variable 
``value`` will contain the value that the user is trying to set within the property.

We can then get or set the value of ``Name`` anywhere else (since it's public) 
using dot-notation:

.. sourcecode:: c#
   :linenos:

   Student josh = new Student();

   // set the Name
   josh.Name = "Josh";

   // get the Name
   Console.WriteLine(josh.Name);

When you use properties in this way, the get/set methods are called implicitly when 
assigning or reading the property.

An astute question to ask at this point would be, “Why make the fields
private if you’re just going to allow people to get and set them
anyway!?” Great question. There are lots of reasons to use getters and
setters to control access. Here are just a few:

1. Getters and setters allow you to implement behavior that happens every time a
   field is accessed (get) or changed (set). For example, you may want track the 
   number of times a change is made to a field. With a private field and setter
   method, this can be done simply by incrementing a counter variable (e.g. ``i++``.)
   With a publicly available field, the steps to track its changes would be much more diffuse,
   if not error-prone.
2. You can perform validation within a setter. For example, we might
   want to ensure that a student’s name contains only certain
   characters, or that their student ID is positive.
3. You can use different access modifiers on getters and setters for the
   same field, based on desired usage. For example, you might want to
   allow anyone to be able to read the value of a field, but only
   classes within the same assembly to modify it. You could do this with
   a public getter and an internal setter, but not as a field
   without getters and setters, which could only be public to everyone
   or internal to everyone.

.. admonition:: Note

   One of the four fields in our ``Student`` class is a prime candidate for 
   the scenario described in item 3. Which one do you think it is?

To set access levels on accessors so that they are different than the access 
level of the property, use an access modifier next to ``get`` or ``set``. Here's 
how we would make ``Name`` readable by everyone, but modifiable only by code within 
the class's assembly. Note that the get accessor does not have an access modifier in 
front of it and therefore it will have the same public access as the property ``Name``.

.. sourcecode:: c#
   :linenos:

   private string name;

   public string Name
   {
      get { return name; }
      internal set { name = value; }
   }

.. _temp-argument-exception:

As an example of setter validation, let’s take a short detour to look at a
``Temperature`` class. A valid temperature can only be so low (“absolute
zero”), so we wouldn’t want to allow somebody to set an invalid value.
In ``set``, we throw an exception if an invalid value is provided (we'll 
cover exceptions in detail :ref:`later <exceptions>`, but for now note that they are ways of 
signaling errors).

.. sourcecode:: c#
   :linenos:

   public class Temperature 
   {

      private double fahrenheit;

      public double Fahrenheit
      {
         get
         {
            return fahrenheit;
         }

        set
        {
            double absoluteZeroFahrenheit = -459.67;

            if (value < absoluteZeroFahrenheit) 
            {
               throw new ArgumentException("Value is below absolute zero");
            }

            fahrenheit = value;
         }
      }
   }

Properties
^^^^^^^^^^

A **property** in C# is a characteristic that users can set. 
Most often, properties will correspond directly to a private backing field, 
but they don't have to. Let’s look at an example of a
property that doesn’t directly correspond to a field. If we wanted to
add a ``Celsius`` property to the ``Temperature`` class above, we might
do it as follows:

.. sourcecode:: c#
   :linenos:

   public double Celsius
   {
      get { return (Fahrenheit - 32) * 5.0 / 9.0; }
      set { Fahrenheit = value * 9.0 / 5.0 + 32; }
   }

Since there’s a link between ``Fahrenheit`` and ``Celsius``, we want to make
sure that when one is updated, so is the other. In this case, we only
store one field value (``fahrenheit``) and make the appropriate
calculation when getting or setting the ``Celsius`` property.

Auto-Implemented Properties
~~~~~~~~~~~~~~~~~~~~~~~~~~~

If a field has both a public getter and setter, and no additional logic is needed, 
we can use the shorthand:

.. sourcecode:: c#

   public string Name { get; set; }

This is referred to as an **auto-implemented property**. When a property is auto-implemented,
the compiler creates a private field that can only be accessed through the property's get and 
set accessors.

Note that in this example, the private field is ``name`` (lowercase) 
while the property is ``Name``. Since C# identifiers are case-sensitive, these are 
two distinct members. ``name`` is referred to as a **backing field**, and it stores 
the value of the property.

.. admonition:: Warning

   If you were to try to use the same identifier for both the backing field and 
   the property, you'll see a *StackOverflowException* due to infinite recursion 
   -- i.e., the property would infinitely call itself!

Using properties, getters/setters, and fields, we can *encapsulate* the information 
we need in our student class.

Check Your Understanding
------------------------

.. admonition:: Question

   What is a method that is used to give a private field a value?

   a. getter
   b. method
   c. property
   d. setter

.. ans: d, A setter is a method that gives a private field a value.
