
- Review what exception objects are

Exceptions you have seen
- Remind students that they have already seen exceptions in C#

Exceptions
==========

Like most programming languages, C# includes exceptions and exception handling tooling. Some exception objects
are provided by .NET itself, while others we may encounter from external C# libraries, or write ourselves.
You may see the term "exception" and instinctively groan or roll your eyes. Isn't programming only enjoyable when
it works? Well, yes it is nice when your code performs as you expect and want it to. And in fact, exceptions are a 
vital component of a healthy codebase. As a program user, encountering an exception can provide crucial information 
about proper usage. As a program writer, providing exceptions gives fellow programmers necessary intel on how your 
app should run and be used.

When to Use Exceptions
----------------------

Indeed, we have seen exceptions in C# already. Recall this 
:ref:`temperature example <temp-argument-exception>` where we throw a built-in exception when a 
provided argument falls outside of an acceptable range. Later, we refine our 
:ref:`temperature app <temp-argument-out-of-range-exception>` and throw the more targeted 
``ArgumentOutOfRangeException``. The program provides a plan for what to do in the event
that bad data is passed into a class's field. In this scenario, we can imagine that a user or fellow programmer may 
unintentionally attempt to set a Fahrenheit value outside of the appropriate range.

This is a common reason to include exception handling in your code. User input opens the door to a variety erroneous 
figures and good 

Failure to connect to services external to your application, such as a database or API.
Failure to read/write from/to a file.
Failed attempt to convert data, such as trying to convert something like "dog" to an integer. This happens most often 
when accepting user input.
Null pointers. In other words, an object reference -- such as a method parameter or local variable -- that doesn't 
actually contain an object.

Using exceptions
- Discuss when to use exceptions (unexpected situations, scenarios we do not want to handle ourselves)
- Describe using exceptions to communicate issues to programmers, not users
- Discuss the use of checked vs. unchecked exceptions

How to handle em
- Discuss how to throw an exception in C#
- Summarize some common built-in exceptions C#
- Describe passing exceptions in C#, when do they stop a program
- Demonstrate ``try/catch`` statements in C#


Common Causes
-------------

Best Practices
--------------

The Golden Rules of Handling Exceptions
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Which Types to Catch
^^^^^^^^^^^^^^^^^^^^

Which Types to Throw
^^^^^^^^^^^^^^^^^^^^

How to Avoid Exceptions
^^^^^^^^^^^^^^^^^^^^^^^

Validate User Input
~~~~~~~~~~~~~~~~~~~

Check For null References
~~~~~~~~~~~~~~~~~~~~~~~~~

References
----------
Exceptions and Exception Handling
Exception Hierarchy