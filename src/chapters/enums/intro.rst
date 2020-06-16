Introduction to Enums
=====================

.. index:: ! enumeration types

Many statically-typed programming languages provide a feature called
**enumeration types**, or **enum types** for short. Enum types are special
classes that should have only one of a set of fixed values, such as days of the
week.

Imagine that we wanted to add a property to ``Event`` to specify which day of the
week an event takes place. You might start by creating a new field:

.. sourcecode:: csharp

   [Required]
   public string DayOfWeek { get; set; }

As defined here, a user could submit any of the following values representing Wednesday:

#. ``"Wednesday"``
#. ``"wednesday"``
#. ``"Wed"``
#. ``"WED"``
#. ``"W"``

Accepting data like this leads to many complications.
For example, searching for all events taking place on Wednesday would need to account for all of these variations.
And what happens if a user misspells "Wednesday"?

.. index:: select

When filling out forms on the web, you are used to seeing dropdown menus with prefilled values restricting the possible inputs.
For example, in the United States, when filling out a shipping address form, a ``select`` element may be used to create a list of the states to insure that users select the correct abbreviation for their state of residence.

Limiting the values that the user can select drastically reduces complexity and
ensures that our application data remains clean and standardized. Enum types
are one way to model fields like this.

Creating an Enum Type
---------------------

Let's see how we can create an enum type, or enum class.

.. admonition:: Note
   
   Recall that a class defines a new *data type*.
   Thus, the term "data type" can be used in place of "class".
   We'll typically call enum classes "enum types" since this is what most C# developers do.

The simplest enum type that we can define to represent days of the week looks
like this:

.. sourcecode:: csharp
   :linenos:

   enum Day
   {
      SUNDAY,
      MONDAY,
      TUESDAY,
      WEDNESDAY,
      THURSDAY,
      FRIDAY,
      SATURDAY
   }

Using the ``enum`` keyword specifies that this class should be an enum type. In
other words, it should only be able to take on one of a fixed set of values.
Within the body of the class, we list the valid values (``SUNDAY``, ``MONDAY``,
etc.). These values are in all-caps because they are *constants*. In fact, the
class above is very similar to this static class:

.. sourcecode:: csharp
   :linenos:

   public class DayStatic
   {
      public const int SUNDAY = 0;
      public const int MONDAY = 1;
      public const int TUESDAY = 2;
      public const int WEDNESDAY = 3;
      public const int THURSDAY = 4;
      public const int FRIDAY = 5;
      public const int SATURDAY = 6;
   }

To refer to Thursday, you can use the value ``DayStatic.THURSDAY``. Recall our
``switch`` :ref:`example from earlier <switch-statements>`.

.. sourcecode:: csharp
   :linenos:

   Console.WriteLine("Enter an integer: ");
   string dayString = Console.ReadLine();
   int dayNum = int.Parse(dayString);

   string day;
   switch (dayNum)
   {
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

This code can be refactored using ``DayStatic``:

.. sourcecode:: csharp
   :linenos:

   Console.WriteLine("Enter an integer: ");
   string dayString = Console.ReadLine();
   int dayNum = int.Parse(dayString);

   string day;
   switch (dayNum)
   {
      case DayStatic.SUNDAY:
         day = "Sunday";
         break;
      case DayStatic.MONDAY:
         day = "Monday";
         break;
      case DayStatic.TUESDAY:
         day = "Tuesday";
         break;
      case DayStatic.WEDNESDAY:
         day = "Wednesday";
         break;
      case DayStatic.THURSDAY:
         day = "Thursday";
         break;
      case DayStatic.FRIDAY:
         day = "Friday";
         break;
      case DayStatic.SATURDAY:
         day = "Saturday";
         break;
      default:
         // in this example, this block runs if none of the above blocks match
         day = "Int does not correspond to a day of the week";
         break;
   }
   Console.WriteLine(day);

In essence, this code represents days of the week as fixed integer values, one
for each day. Enum types are essentially a more robust version of this
approach.

Let's revisit our ``Day`` enum type:

.. sourcecode:: csharp
   :linenos:

   public class DayStatic
   {
      public const int SUNDAY = 0;
      public const int MONDAY = 1;
      public const int TUESDAY = 2;
      public const int WEDNESDAY = 3;
      public const int THURSDAY = 4;
      public const int FRIDAY = 5;
      public const int SATURDAY = 6;
   }

We can declare a variable of type ``Day`` and it will only be allowed to take
on one of the 7 defined values.

.. sourcecode:: csharp
   :linenos:

   // This works
   Day workWeekStart = Day.MONDAY;

   // This does not, throwing a compiler error
   Day workWeekEnd = "Friday";

Enums are important because they provide *type safety* in situations where we
want to restrict possible values. In other words, they eliminate the
possibility of bad, or dirty, values.

Enum Examples
-------------

The world is filled with examples ripe for representation by enums. Here are a
few from both the real world and the world of programming.

.. admonition:: Example

   Months of the year.

   .. sourcecode:: csharp
      :linenos:

      enum Month
      {
         JANUARY,
         FEBRUARY,
         MARCH,
         APRIL,
         MAY,
         JUNE,
         JULY,
         AUGUST,
         SEPTEMBER,
         OCTOBER,
         NOVEMBER,
         DECEMBER
      }

.. admonition:: Example

   Given a model type like our ``Event`` class, enums can represent categories that model objects can fall into.

   .. sourcecode:: csharp
      :linenos:

      enum EventCategory
      {
         CONFERENCE,
         MEETUP,
         WORKSHOP,
         SOCIAL
      }

.. index:: ! log level

.. admonition:: Example

   A common use of enums in programming is to set the log level of an
   application. The **log level** represents the types of log messages that
   should be displayed as the application runs.

   You might only want to see critical error messages when running an application on a production server, but you may want to see many more messages, such as warnings and informational messages, when developing the application locally.

   .. sourcecode:: csharp
      :linenos:

      enum LogLevel
      {
         DEBUG,
         INFO,
         WARNING,
         ERROR
      }

   An application can change the way it logs messages by changing the log level.

Check Your Understanding
------------------------

.. admonition:: Question

   We mentioned above that all classes define a data type.
   Is the inverse of this statement true?
   In other words, do all data types correspond to a class? (*Hint:* Try to think of a data type that is NOT a class.)

   #. Yes, everything in C# is a class.
   #. No, there are data types that do not correspond to a class. (Be sure to provide an example.)

.. ans: b, primitive data types are not classes.

.. admonition:: Question

   Which of the following would NOT be a good choice for an enum type?

   #. States in the US
   #. Shoe sizes (using the American scale)
   #. Price of a gallon of milk
   #. Sections in a bookstore

.. ans: c, Price of a gallon of milk
