.. _unit-testing-studio:

Studio: Unit Testing
====================

For this studio, you will be writing unit tests to help you find 
errors in the ``BalancedBrackets.cs`` file in the starter code.

Discuss with your fellow students and TA how the given class should behave.
What are some examples of input? What would the desired output be for each input?

Getting Started
---------------

#. Fork and clone the `studio repository <https://github.com/LaunchCodeEducation/csharp-web-dev-lsn5unittesting-studio>`__.
#. In Visual Studio, check out your repository.
#. Write unit tests to find the errors in ``BalancedBrackets.cs``.
   
   a. The tests you write should guide how you revise the sourcecode. Use TDD to 
      first write tests that will work for the desired behavior of ``BalancedBrackets``.
      When your tests fail, correct the class to pass your tests.
   b. The content of your tests is up to you, but you should write at least 12 tests.

      .. admonition:: Tip

         Here's a first test to help get you started: 
         
         Assert that brackets in the correct order, ``"[]"``, return true.

         .. sourcecode:: csharp

            [TestMethod]
            public void OnlyBracketsReturnsTrue() {
               Assert.IsTrue(BalancedBrackets.HasBalancedBrackets("[]"));
            }

.. note::

   ``BalancedBrackets`` is essentially a wrapper class for a method. And 
   because it's only method is static, we don't need to create an instance
   to test ``HasBalancedBrackets()``.

Uploading Your Work
-------------------

Push up your work to save your solution in your remote repository.