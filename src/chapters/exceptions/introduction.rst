
.. - Review what exception objects are

.. Exceptions you have seen
.. - Remind students that they have already seen exceptions in C#

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
figures and good programs account for this uncertainty. Without exceptions in these circumstances, a small typo could 
lead to any number of breaking errors.

Here are some other settings where exceptions are your friends:

- Failure to connect to services external to your application, such as a database or API.
- Failure to read/write from/to a file.
- Failure to convert data, such as trying to convert something like "dog" to an integer. 
- Null pointers. In other words, an object reference -- such as a method parameter or local variable -- that doesn't 
  actually contain an object.

Anytime in your development process that you encounter a situation where there is some level of chance involved, like a
variable dependent on user input or a connection to another service, it is wise to manage that chance with exception handling.

Alternatively, you may want to address the uncertainties in a different fashion. With our temperature app for example, rather than
throwing an exception, we may instead add a conditional statement to inform the user not to attempt to set the Fahrenheit value to 
an unacceptable level. This is perfectly acceptable if the app in production allows for such a message. In your development career,
you will encounter plenty of scenarios where user-directed error messages simply won't be appropriate. For example, what if the value
being set doesn't come directly from a user but from a different method in the program? Or what if managing the variety of errors 
that may arise is outside the scope of the project? In these cases where we do not, or cannot, make up for the edge cases with coded
solutions, we can throw an exception.

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