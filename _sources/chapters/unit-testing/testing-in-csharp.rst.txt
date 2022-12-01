Testing in C#
=============

.. index:: ! automated testing, ! unit testing, ! MSTest

Testing your code is a crucial practice for every developer. 
**Automated testing** ensures that your code works as expected every 
time it runs. Tests also function as internal documentation, giving a 
fellow programmer instructions on how to properly execute your classes 
and methods. While these purposes are the same for C# as any other language, 
the implementation of tests will look a bit different.

This course covers **unit testing** in C# with a test framework called
**MSTest**. Unit testing is based on breaking down the codebase into its 
smallest building blocks, individual statements and methods, and testing 
those building blocks.

.. tip::

   If you would like to review the benefits of automated testing, take a peek
   at
   `this section <https://education.launchcode.org/intro-to-professional-web-dev/chapters/unit-testing/why-test.html>`__
   in another LaunchCode text.

Why We Test
-----------

.. index:: ! refactor, ! test-driven development, ! TDD

Refactoring
^^^^^^^^^^^

When we **refactor** code, we rewrite it without adding new features. Refactoring can 
increase efficiency at runtime, but it may also mean inadvertently introducing some bugs in the process.
Unit tests verify the most basic functionality of your code, thus safeguarding against 
bugs introduced in refactoring. 

Imagine this common workflow: 

#. You practice **test-driven development (TDD)**, writing your tests to stipulate 
   how your class's code should behave.

#. You write your class's code to pass the tests. 

#. Later, a stakeholder in the project requests that you refactor your code using 
   different syntax.

The features of the application will be the same, but the implementation of those features will change.
Because the changes in implementation do not effect change in the application features, unit tests can 
help with refactoring the codebase. If your tests continue
to pass after the refactor, you can move on, knowing you have not 
inadvertently introduced a bug. Writing tests just once provides innumerable 
benefits for the whole lifetime of the codebase.

Documentation
^^^^^^^^^^^^^

In addition to assisting with refactoring, unit tests serve as vital documentation 
for fellow programmers. Again, because unit tests address the most fundamental tasks of your classes,
they serve as live-code use-cases. You may also have an 
external documentation directory with examples of how to run your
project, or perhaps you have been writing comments within your code
to best communicate with your teammates about your changes. Both of
these are great choices and should be done when possible. However, these choices 
also require more forethought to maintain. Each time you update
your code, you might not remember to update the documentation and 
comments. With unit testing, however, you have a more obvious reminder
that a change has been made if a previously-passing test fails.

.. _testing-best-practices:

Testing Best Practices
----------------------

Below are some best practices to keep in mind when writing unit tests, in any language.

#. The AAAs

   The AAAs of unit testing refers to the pattern to follow when 
   writing your unit tests. 

   a. Arrange the variables your test requires
   b. Act on the methods your test requires
   c. Assert the anticipated comparison of the expected and actual values

#. Deterministic

   *Every* time a test is run, it should produce the same outcome. 
   A test that passes only most of the time is a worthless test.

#. Relevant

   Group tests by related class and function.

#. Meaningful

   There is no need to test trivial code. For example, unless a getter or setter contains some 
   additional functionality, you do not need to write a test for those methods. 

Check Your Understanding
------------------------

.. admonition:: Question

   True or False: Comments are the best tool to make your code readable.

.. ans: False, comments are helpful but can be used in tandem with other forms of documentation, including unit tests.

.. admonition:: Question

   Unit tests are a form of:

   #. Manual testing
   #. Automated testing
   #. Integration testing
   #. Documentation testing

..  ans: Automated testing
