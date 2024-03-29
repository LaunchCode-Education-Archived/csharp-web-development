.. _tech-jobs-oo:

Assignment #2: Tech Jobs (Object-Oriented Edition)
==================================================

Introduction
------------

Your apprenticeship at LaunchCode is going well! Only a few weeks in and you’re
regularly making contributions to code that will eventually be used by all
LaunchCode staff.

Your last task was to get the prototype Tech Jobs app in good shape. Now it’s
time to advance the underlying structure of the program.

Your mentor on this project is Sally, one of the developers at LaunchCode. She
regularly supports coders who are just getting started with their careers.

.. figure:: figures/LC-Sally.png
   :scale: 50%
   :alt: Sally's LaunchCode avatar.

After seeing your strong work with your last project, Blake reported that you
performed well and learned quickly. Because of your success, he and Sally feel
comfortable assigning you to a set of tasks that are a notch up in difficulty.

Sally completed some initial work on the project and left you some TODOs.

Learning Objectives
-------------------

In this project, you’ll show that you can:

#. Read and understand code written by others.
#. Work with objects to encapsulate data and methods.
#. Use the generator in Visual Studio to automate routine tasks.
#. Use unit testing and Test-Driven-Development (TDD) to verify and create new
   methods.
#. Apply the concept of inheritance to streamline your classes (the DRY
   idea---Don't Repeat Yourself).

Get the Starter Code
--------------------

#. In **Canvas, Graded Assignment #2: TechJobs (Object-Oriented Edition)** contains a GitHub Classroom assignment invitation link and then set up the project in Visual Studio.  Refer back to the GitHub Classroom instructions from :ref:`assignment0` for details.
#. Open Visual Studio.
#. If the app opens up to an existing project, close it.
#. From the Visual Studio dialog box, open your copy of the starter code.

TechJobs (Object-Oriented Edition)
----------------------------------

Sally has gotten the ball rolling by adding a ``Job`` class, along with classes
to represent the individual properties of a job: ``Employer``, ``Location``,
``PositionType``, and ``CoreCompetency``. She completed the ``Employer`` class,
and she left you the task of filling in the others.

As the team gets closer to deploying the app---and abandoning the test data
they’ve been using---they’ll want an easy way to add and remove jobs via a
user interface. Before that, however, you need to finish shifting the project
to an object-oriented design.

Why Change to Object-Oriented?
------------------------------

Working with data stored as strings in dictionaries and lists isn’t a good
long-term solution, for reasons that we point out below.

The ``Job`` class introduces an object-oriented design to the application. It
contains all of the properties you used in the console version of TechJobs:
``Name``, ``EmployerName``, ``EmployerLocation``, ``JobType``, ``JobCoreCompetency``.
There’s also an ``Id`` property which will be used to uniquely identify ``Job``
objects.

The main difference between the object representation of a job and the
string-based representation is that the values of ``EmployerName``, ``EmployerLocation``,
and the other non-ID properties are no longer strings. Instead, they are classes of
their own.

Job Members
^^^^^^^^^^^

Open the ``Job`` class file. You’ll see the following properties (among other class members):

.. sourcecode:: csharp
   :linenos:

   public string Name { get; set; }
   public Employer EmployerName { get; set; }
   public Location EmployerLocation { get; set; }
   public PositionType JobType { get; set; }
   public CoreCompetency JobCoreCompetency { get; set; }

Of these, only ``Name`` is a string. Sally created classes to represent each of
the other properties. These classes---``Employer``, ``Location``,
``CoreCompetency``, ``PositionType``---have members to hold values and IDs.

So, for example, if you had a ``Job`` instance, you could get the name of the
employer this way:

.. sourcecode:: csharp

   // job is an instance of Job
   string employerName = job.EmployerName.Value;

Additionally, the ``ToString()`` method of the ``Employer`` class is set up to
return whatever the ``value`` field holds. Thus, using one of these objects in another string
context like ``Console.WriteLine`` will print the data stored in ``value``.

.. sourcecode:: csharp

   // Prints the name of the employer
   Console.WriteLine(job.EmployerName);

Why do we go to all of this trouble when we could store this job-related data
as strings? There are a couple of reasons.

Eliminate Duplication of Data
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In our app, we have multiple jobs that have the same value in a given field.
For example, there are multiple jobs with position type “Web - Full Stack”, and
each employer may list several jobs. If we store the values of these fields as
strings directly within each ``Job`` object, that data would be repeated in
several places across the application.

By using objects, we can have a single ``PositionType`` object with value “Web
- Full Stack”. Each job that wants to use that position type holds onto a
reference to the given object. Similarly, we can have one ``Employer`` object
for each employer.

Aside from reducing the amount of raw data / memory that the application uses,
this will allow data to be updated more easily and properly. If we need to
change the name of an employer (e.g. due to a typo or a name change at the
company), we can change it in one place, the single ``Employer`` object that
represents that company.

As you continue to work on the assignment, you will find further ways to streamline the application.

Enable Extension
~~~~~~~~~~~~~~~~

While the four ``Job`` properties represented by objects will primarily be used
for their string values, it’s easy to imagine adding new properties to address
future needs.

For example, it would be useful for an ``Employer`` object to have an address,
a primary contact, and a list of jobs available at that employer.

For a ``Location`` object, useful information includes a list of zip codes
associated with that location, in order to determine the city and state for an
employer or job.

If we were to store these four new properties as strings within the ``Job``
class, extending and modifying this behavior would be much more complicated and
difficult moving forward.

Your Assignment
---------------

Running the Auto-grading Tests
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Before diving into your tasks, review :ref:`Assignment #0: Hello, World! <assignment0>` for details on 
running the auto-grading tests for this assignment. 

This assignment has many more tests than the previous two, so we’ve organized them 
into separate files. The tests are visible in the Project's Solution, but they won't run from there.

.. figure:: figures/Tests-In-Solution-A2OO.png
   :scale: 50%
   :alt: List of projects in the solution.  Auto-grading tests are in "TechJobsOOTest" project.

Each of the one test files, ``TestTaskX``, contains the tests to grade one of the six tasks 
outlined in below (there’s no coding work for your first task, so there is **no** ``TestTask1``). 

In order to run any of the tests, we need to use Visual Studio's ``Test Explorer``.  
Open ``Test Explorer``, but do NOT ``Run All Tests`` at this time.  
Visual Studio will not be able to run many of these tests at this time because you have not 
any written code they are designed to test.  It will only throw errors.  
If you did run ALL the tests, stop the tests by clicking on the red square in ``Test Explorer``.

**Mac Users:** To open ``Test Explorer``, select ``Run Unit Tests`` which can be found at the very bottom of the ``Run`` menu. 
This will try to run all the tests, but you can stop them by clicking on the red square at the top of the test panel. 

.. figure:: figures/Running-Tests-A2OO.png
   :scale: 50%
   :alt: "Run Unit Tests" can be found at the bottom of the "Run" Menu.

This will open your ``Test Explorer`` in a new panel and create a tab on the right side of Visual Studio.  
If ``Test Explorer`` is closed, the tab on the right called ``Tests`` will reopen it for you.

.. figure:: figures/Test-Tab-A2OO.png
   :scale: 50%

**Windows Users:**  Select the ``Test`` (1) menu.  ``Test Explorer`` (3) can be found at the bottom of the menu.
Visual Studio will open your ``Test Explorer`` in a new panel.  Recommend **pinning** that panel into Visual Studio.
If ``Test Explorer`` closes, you can reopen it using the ``Test`` menu and selecting ``Test Explorer`` (3).  
We will not be using ``Run All Tests`` (2) at this time. 

.. figure:: figures/Testing-Windows-A2OO.png
   :alt: "Run All Tests" can be found at the top of the "Test" Menu.

Inside ``Test Explorer``, you should see ``TestTaskX``.  
Each ``TestTaskX`` contains multiple tests.
Select ``TestTask2`` tests.  You should see 8 tests listed by their names.
These are all of the tests that will be run after you complete ``Task 2`` in the instructions below.

.. admonition:: Note

      Upon initial examination of the starter code, you may notice that there ONLY 2 ``TestTaskXs``
      in the ``Test Explorer`` and 6 ``TestTaskXs`` in the ``Solution Explorer``.  
      
      ``TestTask4``, ``TestTask5``, and ``TestTask6`` have all been commented out so that you can run
      the auto-grading unit tests for tasks 2-3. 

To run a *single* group of tests, you will right-click on the name of the Task.  
For example, if you finish Task 5, right-click on ``TestTask5`` and select ``Run`` from the pop-up menu.

.. figure:: figures/Running-Single-Test-A2OO.png
   :scale: 50%
   :alt: 

When you start on one of the tasks below, begin by running only the tests associated with that task. 
As you work on the components of the given tasks, continually re-run the tests to see the 
failing tests gradually turn to passing. When all tests within the file pass, you’re ready to move onto the next task. 
As you expand your codebase, none of your earlier tests should fail.  

Your Tasks
^^^^^^^^^^
The list below provides a general overview of your assigned tasks. Specific
details for each part appear in the following sections, so be sure to read them
carefully as you solve each problem.

#. Review Sally's code in the ``Employer`` class to learn how to assign a
   unique ID.
#. Add properties and custom methods as needed to the ``Location``,
   ``CoreCompetency``, and ``PositionType`` classes.
#. Complete the ``Job`` class using what you learned in steps 1 and 2.
#. Use unit testing to verify the constructors and ``Equals()`` methods for the
   ``Job`` class.
#. Use TDD to design and code a custom ``ToString()`` method for the ``Job``
   class.
#. Use inheritance to DRY the code within ``Employer``, ``Location``,
   ``CoreCompetency``, and ``PositionType``.

Task 1: Explore the ``Employer`` Class
--------------------------------------

Open the ``Employer`` file in Visual Studio and examine the code. In addition to the
three members---``nextId``, ``Id``, and ``Value``---the class includes some methods like ``ToString()`` and ``Equals()``.

You can refer to these examples as you fill in the missing pieces in the other
classes, but for now let's take a closer look at the constructors.

Assign a Unique ID
^^^^^^^^^^^^^^^^^^

One neat trick we can use is to automatically assign each new object a unique
ID number.

.. admonition:: Example

   Examine the two constructors in ``Employer.cs``:

   .. sourcecode:: csharp
      :linenos:

      public class Employer {
         public int Id { get; }
         private static int nextId = 1;
         public string Value { get; set; }

         public Employer ()
         {
            Id = nextId;
            nextId++;
         }

         public Employer (string value) : this()
         {
            Value = value;
         }

         // Additional methods omitted from this code block
      }

#. Line 3 declares the field ``nextId``. Since it is ``static``, its
   changing value is NOT stored within any ``Employer`` object.
#. The first constructor (lines 6 - 10) accepts no arguments and assigns the
   value of ``nextId`` to the ``id`` field. It then increments ``nextId``.
   Thus, every new ``Employer`` object will get a different ID number.
#. The second constructor (lines 12 - 15) assigns the ``value``
   field. It ALSO initializes ``id`` for the object by calling the
   first constructor statement with the ``: this()`` syntax. Including ``: this()`` in
   any ``Employer`` constructor makes initializing ``id`` a default behavior.

.. admonition:: Tip

   By adding ``: this()`` to the signature of the second ``Employer`` constructor, we are using a new technique called constructor chaining.
   For more info on how this chaining technique works, check out this `blog post <https://www.codecompiled.com/csharp/constructor-chaining-c/>`_!

Task 2: Complete the Support Classes
------------------------------------

Sally needs you to build up the remaining classes. In each case, refer to the
``Employer`` class for hints on how to structure your code.

.. admonition:: Warning

   Due to the fact that this code is being auto-graded as you work through it, 
   make sure that you use any and all names for classes, variables, methods, etc provided to you in these directions.

The ``Location`` Class
^^^^^^^^^^^^^^^^^^^^^^

Open the ``Location.cs`` file. Note that the
methods for this class are done, as is the constructor for initializing the
``Id`` property.

Sally left you a ``TODO`` comment with instructions for coding a second
constructor:

#. It should call the first constructor to initialize the ``id`` field.
#. It must also initialize the ``value`` field for a new ``Location`` object.

.. _generator-shortcut:

The ``CoreCompetency`` Class
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Open the class file. In this case, the constructors and custom methods are
ready. Sally needs you to change the ``id`` and ``value`` fields to auto-implemented properties, but NOT ``nextId``.

The ``PositionType`` Class
^^^^^^^^^^^^^^^^^^^^^^^^^^

Open the class file. This time the constructors are done.
Sally's comments direct you to where you need to add the custom methods.

#. Code a ``ToString()`` method that just returns the ``value`` of a
   ``PositionType`` object.
#. Use the *Generate* option again to add the ``Equals()`` and ``GetHashCode()``
   methods. Refer to the :ref:`final section <equals-shortcut>` of the
   "Classes and Objects, Part 2" chapter if you need a quick review.
#. Assume that two ``PositionType`` objects are equal when their ``id`` fields
   match.

Run Your Tests
^^^^^^^^^^^^^^

Run your ``TestTask2`` unit tests.  Refactor your code as needed.  
Do not move onto Task 3 until you have passed all of Task 2's auto-grading unit tests.

.. admonition:: Tip

   Now would be a good time to save, commit, and push your work up to GitHub.

Task 3: Complete the ``Job`` Class
----------------------------------

.. admonition:: Note

   The starter code in the ``Job`` class has been commented out for the rest of the tests to run.
   
   Remove the ``/*`` in **line 6** and ``*/`` in **line 20**.

.. admonition:: Warning

   Due to the fact that this code is being auto-graded as you work through it, 
   make sure that you use any and all names for classes, variables, methods, etc provided to you in these directions.


Now open the ``Job`` file. OOF! There are a lot of fields and properties declared and not much
else.

#. Code a constructor to initialize the ``id`` field with a unique value. This
   constructor should take no parameters.
#. Code a second constructor that takes 5 parameters and assigns values to
   ``name``, ``employerName``, ``employerLocation``, ``jobType``, and
   ``jobCoreCompetency``. Also, this constructor should call the first in order to
   initialize the ``id`` field.
#. Generate the ``Equals()`` and ``GetHashCode()`` methods. Consider two ``Job``
   objects equal when their ``id`` fields match.

Run Your Tests
^^^^^^^^^^^^^^

Run your ``TestTask3`` unit tests.  Refactor your code as needed.  
Do not move onto Task 4 until you have passed all of Task 3's auto-grading unit tests.

.. admonition:: Tip

   Save, commit, and push your work to GitHub.

Task 4: Use Unit Testing to Verify Parts of the ``Job`` Class
--------------------------------------------------------------

.. admonition:: Note

   All of the tests in ``TestTask4`` are commented out right now.
   
   Remove the ``/*`` in **line 1** and ``*/`` in **line 155** to run the ``TestTask4`` tests.

.. admonition:: Warning

   Due to the fact that this code is being auto-graded as you work through it, 
   make sure that you use any and all names for classes, variables, methods, etc provided to you in these directions.

The solution currently contains a testing project called ``TechJobsTests``.  
If you open this project, you will find a class called ``JobTests.cs``. 
You will need to add the appropriate dependency to ``TechJobsTests`` to test the classes in the ``TechJobsOO`` project.
The ``JobTests.cs`` file will hold all of the tests for the ``Job`` class.

Test the Empty Constructor
^^^^^^^^^^^^^^^^^^^^^^^^^^

Each ``Job`` object should contain a unique ID number, and these should also be
sequential integers.

#. In ``JobTests``, define a test called ``TestSettingJobId``.
#. Create two ``Job`` objects using the empty constructor.
   Use ``Assert.AreEqual``, ``Assert.IsTrue``, or ``Assert.IsFalse`` to test that the
   ID values for the two objects are NOT the same and differ by 1.
#. Run the test to verify that your ``Job()`` constructor correctly assigns
   ID numbers.
#. If the test doesn't pass, what should be your first thought?

   a. "I need to fix the unit test."
   b. "I need to fix my ``Job()`` constructor code."

   .. admonition:: Warning

      The answer is NOT "a".

      Your test code *might* be incorrect, but that should not be your FIRST
      thought. TDD begins with writing tests for desired behaviors. If the
      tests fail, that indicates errors in the methods trying to produce the
      behavior rather than in the tests that define that behavior.

Test the Full Constructor
^^^^^^^^^^^^^^^^^^^^^^^^^

Each ``Job`` object should contain six properties---``Id``, ``Name``, ``EmployerName``,
``EmployerLocation``, ``JobType``, and ``JobCoreCompetency``.

#. In ``JobTest``, define a test called
   ``TestJobConstructorSetsAllFields``.
#. Declare and initialize a new ``Job`` object with the following data: ``"Product tester"`` for ``Name``, ``"ACME"`` for ``EmployerName``, ``"Desert"`` for ``JobLocation``, ``"Quality control"`` for ``JobType``, and ``"Persistence"`` for ``JobCoreCompetency``.
#. Use ``Assert`` statements to test that the constructor correctly assigns the value of each field.

Test the ``Equals()`` Method
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Two ``Job`` objects are considered equal if they have the same ``id`` value,
even if one or more of the other fields differ. Similarly, the two objects
are NOT equal if their ``id`` values differ, even if all the other fields are
identical.

#. In ``JobTest``, define a test called ``TestJobsForEquality``.
#. Generate two ``Job`` objects that have identical field values EXCEPT for
   ``id``. Test that ``Equals()`` returns ``false``.

It might seem logical to follow up the ``false`` case by testing to make sure
that ``Equals()`` returns ``true`` when two objects have the same ID. However,
the positive test is irrelevant in this case.

The way you build your ``Job`` class, each ``id`` field gets assigned a unique
value, and the class does not contain a setter for the ``id`` field. You also verified
that each new object gets a different ID when you tested the constructors.
Without modifying the constructors or adding a setter, there is no scenario in
which two different jobs will have the same ID number. Thus, we can skip the
test for this condition.

Run Your Tests
^^^^^^^^^^^^^^

Run your ``TestTask4`` unit tests.  Refactor your code as needed.  
Do not move onto Task 5 until you have passed all of Task 4's auto-grading unit tests.


.. admonition:: Tip

   Time to save, commit, and push your work to GitHub again.

Task 5: Use TDD to Build The ``ToString()`` Method
--------------------------------------------------

.. admonition:: Note

   This tests in ``TestTask5`` are commented out right now.
   
   Remove the ``/*`` in **line 1** and ``*/`` in **line 167** to run the ``TestTask5`` tests.


.. admonition:: Warning

   Due to the fact that this code is being auto-graded as you work through it, 
   make sure that you use any and all names for classes, variables, methods, etc provided to you in these directions.

To display the data for a particular ``Job`` object, you need to implement a
custom ``ToString()`` method. Rather than creating this method and then testing
it, you will flip that process using TDD.

Create First Test for ``ToString()``
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Before writing your first test, consider how we want the method to behave:

#. When passed a ``Job`` object, it should return a string that contains a
   blank line before and after the job information.
#. The string should contain a label for each field, followed by the data
   stored in that field. Each field should be on its own line.

   ::

      ID:  _______
      Name: _______
      Employer: _______
      Location: _______
      Position Type: _______
      Core Competency: _______

#. If a field is empty, the method should add, "Data not available" after
   the label.
#. (Bonus) If a ``Job`` object ONLY contains data for the ``id`` field, the
   method should return, "OOPS! This job does not seem to exist."

We will need three tests to test our ``ToString`` method.  

Test 1: ``TestToStringStartsAndEndsWithNewLine``
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

In ``JobTests``, add a new test called ``TestToStringStartsAndEndsWithNewLine`` to check the first requirement (item 1 in the above list), then run
that test (it should fail).

.. admonition:: Note

   When testing the ``TestToStringStartsAndEndsWithNewLine``, do NOT test this one individually or it will fail.
   You need to test this one by running all ``TestTask5`` tests or the ``Id`` numbers will cause a failure.

Woo hoo! Failure is what we want here! Now you get to fix that.

Code ``ToString()`` to Pass Test 1
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

In the ``Job`` class, create a ``ToString()`` method that passes the first test.
Since the test only checks if the returned string starts and ends with a blank
line, make that happen.

.. admonition:: Tip

   Do NOT add anything beyond what is needed to make the test pass. You will
   add the remaining behaviors for ``ToString()`` as you code each new test.

Test 2: ``TestToStringContainsCorrectLabelsAndData``
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
#. Code a new test for the second required behavior, then run the tests to make
   sure the new one fails.  Call this test ``TestToStringContainsCorrectLabelsAndData``.
#. Modify ``ToString()`` to make the new test pass. Also, make sure that your
   updates still pass all of the old tests.
#. Continue this test-refactor cycle until all of the behaviors we want for
   ``ToString()`` work. Remember to add only ONE new test at a time.

Test 3: ``TestToStringHandlesEmptyField``
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
#. Code your final test for the last required behavior, 
   then run the tests to make sure the new one fails. Call this test ``TestToStringHandlesEmptyField``.
#. Modify ``ToString()`` to make the new test pass.  Also make sure that your updates still pass all the old tests.

Cool! Your ``Job`` class is now complete and operates as desired.

Run Your Tests
^^^^^^^^^^^^^^

Run your ``TestTask5`` unit tests.  Refactor your code as needed.  
Do not move onto Task 6 until you have passed all of Task 5's auto-grading unit tests.

And don't forget to ``add``, ``commit`` and ``push`` the latest version of your code.

Task 6: Refactor to DRY the Support Classes
-------------------------------------------

.. admonition:: Note

   The tests in ``TestTask6`` are commented out right now.
   
   Remove the ``/*`` in **line 1** and ``*/`` in **line 96** to run all of the ``TestTask6`` tests.

.. admonition:: Warning

   Due to the fact that this code is being auto-graded as you work through it, 
   make sure that you use any and all names for classes, variables, methods, etc provided to you in these directions.

Review the code in the ``Employer``, ``Location``, ``CoreCompetency``, and
``PositionType`` classes. What similarities do you see?

There is a fair amount of repetition between the classes. As a good coder,
anytime you find yourself adding identical code in multiple locations you
should consider how to streamline the process.

   DRY = "Don't Repeat Yourself".

Create a Base Class
^^^^^^^^^^^^^^^^^^^

Let's move all of the repeated code into a separate class. We will then have
``Employer``, ``Location``, ``CoreCompetency``, and ``PositionType`` *inherit*
this common code.

#. Create a new class called ``JobField``.
#. Consider the following questions to help you decide what code to put in the
   ``JobField`` class:

   a. What fields do ALL FOUR of the classes have in common?
   b. Which constructors are the same in ALL FOUR classes?
   c. Which custom methods are identical in ALL of the classes?

#. In ``JobField``, declare each of the common class members.
#. Code the constructors.
#. Add in any inherited method overrides.
#. Finally, to prevent the creation of a ``JobField`` object, make this class
   *abstract*.

Extend ``JobField`` into ``Employer``
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Now that you have the common code located in the ``JobField`` file, we can
modify the other classes to reference this shared code. Let's begin with
``Employer``.

#. Modify line 5 to *extend* the ``JobField`` class into ``Employer``.
#. Next, remove any code in ``Employer`` that matches code from ``JobField``
   (e.g. the ``Id`` and ``Value`` properties and the ``nextId`` field are shared).
#. Remove any of the methods that are identical.
#. The empty constructor is shared, but not the second. Replace the two
   constructors with the following:

   .. sourcecode:: csharp
      :lineno-start: 7

      public Employer(string value) : base(value) 
      {
      }

#. Rerun your unit tests to verify your refactored code.

Finish DRYing Your Code
^^^^^^^^^^^^^^^^^^^^^^^

#. Repeat the process above for the ``Location``, ``CoreCompetency``, and
   ``PositionType`` classes.
#. Rerun your unit tests to verify that your classes and methods still work.

Run Your Tests
^^^^^^^^^^^^^^

Run your ``TestTask6`` unit tests.  Refactor your code as needed.  
This is the last set of tests!  Congrats!  
Submit your assignment once you have passed all of Task 6's auto-graded unit tests.

.. admonition:: Tip

   You know you need to do this, but here is the reminder anyway. Save, commit,
   and push your work to GitHub.

Sanity Check
------------

Once you finish all of the tasks outlined above, all that remains is to check
the console display.

Sally has provided some commented-out code in ``TechJobs.cs`` that prints out a small
list of ``Job`` objects. Go ahead and activate this code and run it.
Properly done, your output should look something like:

::
    
   ID: 1
   Name: Product tester
   Employer: ACME
   Location: Desert
   Position Type: Quality control
   Core Competency: Persistence


   ID: 2
   Name: Web Developer
   Employer: LaunchCode
   Location: St. Louis
   Position Type: Front-end developer
   Core Competency: JavaScript


   ID: 3
   Name: Ice cream tester
   Employer: Data not available
   Location: Home
   Position Type: UX
   Core Competency: Tasting ability
    

 
Excellent! You successfully shifted the old console app into a more useful
object oriented configuration.

Now that the new structure is ready, another team member can refactor the
import and display methods from the previous assignment to use the new classes. Once these are ready, our
team will refine the search features and move the app online to provide a
better user interface.

How to Submit
--------------

To turn in your assignment and get credit, follow the
:ref:`submission instructions <submitting-your-work>`.
