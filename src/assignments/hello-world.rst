.. _assignment0:

Assignment #0: Hello, World!
============================

The purpose of this initial assignment is to familiarize yourself with the process of running the autograding tests and submitting your work via GitHub Classroom. Even if you are familiar with GitHub Classroom, this assignment will contain several new items that are specific to working with C# assignments.

Getting Started
---------------

Let's set up the assignment on our computer and learn about its basic structure.

First, find Assignment #0 in Canvas and click on the invitation link. After accepting the assignment on the Github Classroom page, go to your assignment repository on GitHub.

Follow the instructions to :ref:`clone your repository <clone-csharp-project>` and open it in Visual Studio.

When the solution opens, check out what the repository contains in the *Solution Explorer* on the left. You will find two projects within the solution.

.. admonition:: Note

   If you do not see the *Solution Explorer*, you can open it by selecting *View*, then *Solution Explorer*.

Open up the ``SayHelloClass`` class in the ``HelloWorldAutograded`` project. This is where you will work on your code.

Now, turn your attention to ``Program.cs`` in the ``HelloWorldAutograded`` project. We have given you some code that will output the string returned by the ``SayHello()`` function in ``SayHelloClass``.

To run the program, do the following:

#. **Mac Users**: Hit the *Run* button at the top right-hand corner of the window or right-click on the ``HelloWorldAutograded`` project and select *Run Project*.
#. **Windows Users**: Click on the solid green triangle next to the name of the ``HelloWorldAutograded`` project. You can also press F5 to run the project.

When the program runs, Visual Studio will open a pane and display program output. Currently, the program has no output. You'll fix that in a bit.

Running the Autograding Script
------------------------------

For this unit, we encourage you to run the autograding tests yourself *before* you push your code.
This will make it quicker and easier to know whether or not your code is correct. Let's learn how to run the tests.

In the *Solution Explorer*, navigate to the test class, ``AutogradingTests``, in the project ``HelloWorldTests``.
For each assignment, there will be a test project, which contains all of the autograding tests and may have more than one class.

A test is a single method in a test file that has ``[TestMethod]`` just above it. A test file may have multiple tests. To run just one test, you can right-click on the test method name and select *Run Test*.
To run all of the auto-grading tests (in this case, there is only one), you should do the following:

#. **Mac Users**: Select *Run* from the top menu and select *Run Unit Tests*. After you first run the tests, you can also right-click on the project name and selecting *Run Project*.
#. **Windows Users**: Right-click on the project name and select *Run Tests*. You can also select *Run All Tests* in the *Test* menu tab. 

When Visual Studio runs the tests, it opens a pane to display test results. At the left, we see that the test has failed. We can expand the tree to see each of the individual tests (again, in this case there is only one). Selecting one of the tests shows its results to the right. 

In this case, the test expected our code to output ``Hello, World!``. Instead, it provided no output at all.

.. admonition:: Warning

   The autograding tests are VERY exacting.
   A difference of just one character will result in a failed test.
   The tests are also case-sensitive. You'll need to pay attention to detail in order complete your assignments.

When your code is correct, Visual Studio will display a green checkmark indicating passing tests.

Your Task
---------

Your task is simple: make the program print out the string ``"Hello, World!"``.
Edit the code in the ``SayHelloClass`` class, within the ``SayHello()`` method. When your code is correct, running the tests will display passing results.

.. _submitting-your-work:

Submitting Your Work
--------------------

Once you get all of the tests to pass, open up Visual Studio's *Terminal* pane. Then you should commit and push your code to GitHub.

Visit your assignment repository page. Near the top right, you'll see a green checkmark indicating that GitHub has graded your assignment as passing. If you see a red X, then your assignment is not yet correct.

This process will be the same for all of your assignments in this unit. Revisit this page as needed to review instructions on running tests in C# projects.