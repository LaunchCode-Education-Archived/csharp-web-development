.. _tech-jobs-console:

Assignment #1: Tech Jobs (Console Edition)
===========================================

Introduction
------------

Congratulations! Based on your hard work and strong coding skills, you have
been brought on as an apprentice to the LaunchCode Tech Team. You will be
paired with a mentor to help you get comfortable and continue learning.

The Company Team at LaunchCode works with employer partners to match qualified
programmers with apprenticeships. They asked for a new tool to be built to
help them easily manage data for currently available jobs. Over the next few
weeks, you will help them build this application alongside mentors from the
Tech Team.

This first project will be a simple proof-of-concept prototype. It won't be
pretty or have lots of features, but it will give you a chance to work through
some initial concepts and get feedback from LaunchCode staff.

Your mentor on this project is Blake.

.. figure:: figures/LC-Blake.png
   :scale: 50%
   :alt: LaunchCode mentor image.

Learning Objectives
--------------------

In this project, you will show that you can:

#. Read and understand code written by others.
#. Use core C# syntax (methods, variables, loops, conditionals).
#. Utilize ``List`` and ``Dictionary`` collection types.
#. Work with console I/O via the ``Console`` class.
#. Work with data types and arrays.

TechJobs (Console Edition)
---------------------------

The app you must help design is a simple console (i.e. command-line) prototype
of the new TechJobs app. It will allow LaunchCode staff to browse and search
listings of open jobs by employer partners.

The prototype process gives everybody a chance to work out some initial ideas
without investing a ton of time into developing a finished product. Once
everybody likes the prototype, the Tech Team will begin work toward a
full-fledged application.

Your Assignment
----------------

Blake created a console application and started to fill in some features. His
code allows users to search job listings by one of several fields. It can also
display lists of all of the values of a given field in the system (e.g. all
employers, or all locations).

Blake has now handed the task off to you. You must add a couple of features and
then get feedback from the Company Team.

After you work through the tasks Blake has laid out for you, tackle one
or more of the :ref:`bonus missions <tech-jobs-console-bonus-missions>`.

Getting Started
----------------

In Canvas, **Graded Assignment #1: TechJobs Console** contains a GitHub Classroom assignment invitation link and then set up the project in Visual Studio. Refer back to the GitHub Classroom instructions from :ref:`assignment0` for details. 

Before diving in and starting to code, make sure you understand what the code
you've been given does. Since you're starting with a functioning---albeit
unfinished---program, go ahead and run it to get an idea of how it works. To do
this, right-click on the project that contains the ``TechJobs`` class and select *Run Project*.

.. admonition:: Warning

   The application will run until you force it to quit, re-prompting time
   after time. To kill it, press the "stop" icon in the Run pane. We'll learn precisely how the program manages to work this way below.

Let's explore the code by starting with the source of the data our program is
providing access to.

The Data File: ``jobs_data.csv``
---------------------------------

Our simple app doesn't connect to a database. If the prototype proves
useful and we continue development, we'll add that functionality later.
But for now, we've been given a CSV (comma-separated values) file from
the Company Team at LaunchCode that contains some recent jobs. This file
was exported from an Excel spreadsheet into this format, which is easy
for programs to read in.

If CSV files are new to you, don't worry, they're easy to understand.
CSV files are conceptually similar to simple spreadsheets in that they
organize data in rows and columns. The major difference is that they
don't have the ability to carry out calculations the way spreadsheets
do, and you can easily open, read, and edit them in plain text editors.

Open up ``jobs_data.csv``, which is in the project. You'll see that the first line is:

.. sourcecode:: bash

   name,employer,location,position type,core competency

While it isn't required, the first line of a CSV file often represents
the column names. We have 5 names here, which indicates that each of our
rows in the CSV file should have 5 fields. In this file format, a **row**
corresponds to a new line. So each line below the first will constitute
a row of data, or a record.

Have a look at the data below line 1, and ask yourself the following
questions:

#. Which fields match up with which column names above?
#. Why do some lines/rows (e.g. line 10) have more commas than others, if
   commas are supposed to separate columns?
#. What role do the double-quotes play in lines 10 and 79?

The TechJobs Class
-------------------

The ``TechJobs`` class contains the method that will drive our
program's functionality. It contains three methods:

#. ``RunProgram()`` - The main application runner.
#. ``GetUserSelection()`` - A utility method that displays a menu of choices and
   returns the user's selection.
#. ``PrintJobs()`` - This is meant to print a list of jobs to the console in a
   nicely formatted manner, but hasn't been implemented yet. This will be part
   of your job.

Let's look at each of these.

The ``RunProgram()`` Method
^^^^^^^^^^^^^^^^^^^^^^^^^^^ 

The logic within ``RunProgram()`` presents menus in turn, and based on the
user's choice, takes appropriate action.

It begins by declaring two local variables: ``actionChoices`` and
``columnChoices``. These contain information relating to the menus that
we'll display, and we'll look at them in more detail later.

Next, we notice a ``while loop`` that starts ``while (true)``. While we usually
want to avoid creating infinite loops, we have a good reason for doing so in
this case! We want our application to continually run until the user decides
they want to quit. The simplest way to do this is to loop forever. When the
user wants to quit our app, they can enter ``x`` at the initial ``View jobs by`` prompt. 

.. admonition:: Note

   There are two ways to stop a running app. Either option works so you can pick the one that works best for you!
   
   #. Use the IDE.  Click Visual Studio's *Stop* icon.  The light red square that replaces the green *Run* triangle once an app is running.
   #. Use the terminal. Press *ctrl+C* (a widely-known command to kill a console application). This will work in any terminal context, and not just for our console program in Visual Studio

The ``RunProgram()`` method can be summarized as follows:

#. Present the user with choices on how to view data: *list* or *search*.
#. Based on that choice, prompt them for the column to apply the choice to. In
   the case of a search, we also ask for a search term.
#. Carry out the request to the ``JobData`` class via one of its public
   methods.
#. Display the results of the request.
#. Repeat.

``RunProgram()`` simulates a *query* to an external source:

#. We ask the method for data that originates from a non-C# source.
#. The method parses and filters that data.
#. The method presents the data in a useful manner.

The ``GetUserSelection()`` Method
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The ``GetUserSelection()`` method takes in a string to display above the
menu, to provide context for what they are being asked. It also takes in
a ``Dictionary`` with string keys and string values. How is this used? What
will this ``Dictionary`` contain when the method runs?

To figure this out, right-click on the method name and select *Find (All)
References*. This will open a pane and display each location in the program
where ``GetUserSelection()`` is called. The first such usage is the first
line of the main ``while loop``:

.. sourcecode:: csharp

   string actionChoice = GetUserSelection("View Jobs", actionChoices);

What is this ``Dictionary`` named ``actionChoices``? If we look a few lines
above, we see:

.. sourcecode:: csharp
   :lineno-start: 13

   // Top-level menu options
   Dictionary<string, string> actionChoices = new Dictionary<string, string>();
   actionChoices.Add("search", "Search");
   actionChoices.Add("list", "List");

If you recall how the program worked when you ran it, the first menu
that you chose had two options, *Search* and *List*, which seem to
correspond to the entries in ``actionChoices``. This is, in fact, the
case. This is the data that is used to generate the first menu we see
when running the program.

The second usage of ``GetUserSelection()`` is a few lines below:

.. sourcecode:: csharp
   :lineno-start: 39

   string columnChoice = GetUserSelection("List", columnChoices);

This references ``columnChoices``, which is declared at the top of
``RunProgram()`` and has a similar structure to ``actionChoices`` (they're the
same data type and are used in calls to the same method, so this
shouldn't be surprising). Most of the entries in ``columnChoices``
correspond to columns in the jobs data set, but there's one additional
entry with key/value pair ``"all"``/ ``"All"``. These entries will help
us present to the user the options for searching our data, which will
correspond to searching within a given column, or searching all columns
at once.

The keys in ``actionChoices`` and ``columnChoices`` represent the
*internal* strings we'll use to refer to these options (e.g. when representing
the user's menu choice, or querying data). The values in the ``Dictionary`` represent the
*external* way that these are represented to the user.

Within ``GetUserSelection()`` itself, most of the code is within a
``do-while loop``. A `do-while
loop <https://www.tutorialsteacher.com/csharp/csharp-do-while-loop>`__
is similar to a ``while`` loop, but the conditional check is at the
*end* of the loop's code block. This has the net consequence that the
loop's code block *always runs at least once*. At the end of the block's
execution, we check a condition to determine if we should run the block
again. This nicely mimics the behavior of simple menu-driven
applications.

Within this loop, menu options are printed to the screen, and user input
is collected. If the input is valid, it returns the choice as a ``string``
to the caller. This ``string`` corresponds to the chosen key (from
``choices``, which will be either ``actionChoices`` or
``columnChoices``) of the item the user selected. If invalid, it
re-prompts the user.

The local variable ``choiceKeys`` is used to easily enumerate the
``choices`` ``Dictionary``. In other words, it gives us a simple way to
provide an ordering to ``choices``, which doesn't have an ordering of
its own.

The ``JobData`` Class
---------------------

The ``JobData`` class is responsible for importing the data from the CSV
file and parsing it into a C#-friendly format, that is, into
``Dictionary`` and ``List`` form. Look toward the bottom of the class
and you will see a method named ``LoadData()``, which does just what it
advertises. After parsing the file data, it stores the data in the
private property ``AllJobs`` which is of type
``List<Dictionary<string, string>>``.

.. admonition:: Note

   We haven't covered static properties and methods in-depth yet. For this
   assignment, know simply that they allow us to use properties and methods
   of a class without creating an object from that class. For example, we
   can call ``JobData.FindAll()`` from the ``TechJob`` class.

   If you want to create a new method in ``JobData``, or add a property, be
   sure to declare it as ``static``.

Let's look more closely at the data type of ``AllJobs``. It purports to
be a ``List`` that stores ``Dictionary`` objects which have
``string`` keys and ``string`` values. If we were to represent some of
this data visually, using ``[]`` for a ``List`` and ``{}`` for a collection of
key/value pairs (i.e., a ``Dictionary``), it would look like this:

.. sourcecode:: csharp
   :linenos:

   [
       {
           "name": "Junior Data Analyst",
           "employer": "Lockerdome",
           "location": "Saint Louis",
           "position type": "Data Scientist / Business Intelligence",
           "core competency": "Statistical Analysis"
       },
       {
           "name": "Junior Web Developer",
           "employer": "Cozy",
           "location": "Portland",
           "position type": "Web - Back End",
           "core competency": "Ruby"
       },
       ...
   ]

If you look at the ``LoadData()`` method you'll see a lot of unfamiliar code.
Blake wrote this essential piece of code for you, and while you won't have to
modify it, it will be useful to have an idea of how it works. Read
through the code until you feel like you can describe its functionality
at a basic level.

.. index:: overloading

There are three more methods in ``JobData``, each of which is public
(and ``static``, per our earlier note): 
- ``FindAll()``
- ``FindAll(string)``
- ``FindByColumnAndValue(string, string)``. 

Note: there are two methods named ``FindAll()``, but this is allowed in
C# via a feature called **overloading**. Overloading happens when
multiple methods have the same name, but they each have different input
parameters (also called argument lists). Read more about
`overloading <https://www.geeksforgeeks.org/c-sharp-method-overloading//>`__.

Here are some questions to ask yourself while reading this code:

#. What is the data type of a "job" record?
#. Why does ``FindAll(string)`` return something of type ``List<string>``
   while ``FindByColumnAndValue(string, string)`` and ``FindAll()`` return
   something of type ``List<Dictionary<string, string>>``?
#. Why is ``LoadData()`` called at the top of each of these four methods? Does
   this mean that we load the data from the CSV file each time one of them
   is called?

Your Tasks
-----------

Before diving into your tasks, review :ref:`assignment0` for details on running the autograding tests for this assignment. This assignment has multiple tests, and we highly recommend the following workflow:

#. Write the code for the task, verifying manually that it works by running the ``TechJobsConsoleAutograded`` project.
#. When you think you've completed a task, run the individual test that corresponds to the task. 
#. If the test fails, review the test output and go back to your code to try to fix it.
#. Once the single test passes, run *all* of the tests to make sure you didn't break any tests that previously passed.
#. Repeat this process until all tests pass. 

Now we'll outline the tasks for your first apprenticeship assignment.

Implement ``PrintJobs()``
^^^^^^^^^^^^^^^^^^^^^^^^^

When trying out the program, and later when reading the code, you
hopefully noticed that there's some work to do in the ``PrintJobs()``
method. As it stands, it currently just prints a message:
``"PrintJobs is not implemented yet"``.

Complete this method. It should print out jobs *in this precise format*:

.. sourcecode:: bash

   *****
   position type: Data Scientist / Business Intelligence
   name: Sr. IT Analyst (Data/BI)
   employer: Bull Moose Industries
   location: Saint Louis
   core competency: Statistical Analysis
   *****

   *****
   position type: Web - Back End
   name: Ruby specialist
   employer: LaunchCode
   location: Saint Louis
   core competency: Javascript
   *****

For the autograding script to correctly grade your code, you'll need to match this format *exactly*. In particular, note the number of asterisks surrounding each listing, and the blank line between listings.

If there are no results, it should print ``No results``. Again, you should use this *exact* message.

.. admonition:: Warning

   To create new lines for your output, use ``Environment.NewLine``.  

Using the ``Environment.NewLine``  will allow the autograding unit tests pass regardless of your operating system.  ``\n`` is a new line in Mac OS, but will be read as ``\r\n`` in Windows.    Read about the differences in line breaks `here <https://dev.to/pieter/why-windows-uses-rn-newlines-instead-of-n-126l>`_.  Read more about how ``Environment.NewLine`` `works <https://www.dotnetperls.com/newline>`_.

.. admonition:: Tip

   To do this, you'll need to iterate over a ``List`` of jobs. Each
   job is itself a ``Dictionary``. While you can get each of the items out of
   the ``Dictionary`` using the known keys (``employer``, ``location``, etc.),
   think instead about creating a nested loop to loop over each
   ``Dictionary``. If a new field is added to the job records, this approach
   will print out the new field without any updates to ``PrintJobs()``.

Test this method before moving on to your next step:

#. Save your changes.
#. Run the project.
#. Select "1" to list the jobs, and then "0" to list them all.
#. Make sure the printout matches the styling above.
#. Test that it prints a descriptive message if no jobs are found by selecting
   "0" to search and then "3" to search for a location. Then enter a location
   that is not in the data (e.g. "Cancun"). Your message should be displayed.

Create Method ``FindByValue()``
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

At this stage, the application will allow users to search a *given
column* of the data for a given string. Your next task is to enable a
search that looks for the search term in *all* of the columns.

In the ``JobData`` class, find the method ``FindByValue()``. This method has been outlined
for you but contains none of the code needed to work (you should leave the ``LoadData()`` call as the first line of the method, however). Here are a few observations:

#. The code that you write should not contain duplicate jobs. So, for
   example, if a listing has position type "Web - Front End" and name
   "Front end web dev" then searching for "web" should not include the
   listing twice.
#. As with ``PrintJobs()``, you should write your code in a way that if a
   new column is added to the data, your code will automatically search
   the new column as well.
#. You should NOT write code that calls ``FindByColumnAndValue()`` once
   for each column. Rather, utilize loops and collection methods as you
   did above.
#. You *should*, on the other hand, read and understand
   ``FindByColumnAndValue()``, since your code will look similar in some
   ways.

You'll need to call ``FindByValue()`` from somewhere in ``RunProgram()``. We'll
leave it up to you to find where. You might have noticed that when you
try to search all columns using the app, a message is printed, so that
is a good clue to help you find where to place this new method call.
Once you find where to call your new method, you can *Run* the program
again to test your code.

Make Search Methods Case-Insensitive
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

You've completed your first two tasks!

Let's assume you demonstrated the updated application for the Company Team, and
they noticed a feature that could be improved. When searching for jobs with
the skill ``"JavaScript"`` some results were missing (e.g. the Watchtower
Security job on line 31 of the CSV file). The search methods turn out to be
case-sensitive, so they treat ``"JavaScript"`` and ``"Javascript"`` as different
strings.

The Company Team strongly requested that this needs to be fixed, and of course
you told them that you are up to the task.

Here are some questions to ask yourself as you get started:

#. Which methods are called when searching?
#. How is the user's search string compared against the values of fields of the
   job ``Dictionary`` objects?
#. How can you make this comparison in a way that effectively ignores the case
   of the strings?
#. How can you do this *without* altering the capitalization of the items in
   ``AllJobs`` so that the data gets printed out the same way that it appears
   in ``job_data.csv``?

You might find it useful to review the String methods listed in the
chapter on :ref:`string-methods`.

When this task is completed, you're done!

Sanity Check
-------------

Before submitting, make sure that your application:

#. Prints each field of a job when using search functionality, and when
   listing all columns. If there are no search results, a descriptive
   message is displayed.
#. Allows the user to search for a string across all columns.
#. Returns case-insensitive results.

How to Submit
--------------

To turn in your assignment and get credit, follow the
:ref:`submission instructions <submitting-your-work>`.

.. _tech-jobs-console-bonus-missions:

Bonus Missions
--------------

If you want to take your learning a few steps further, here are some
additional problems you can try to solve. We're not providing you much
guidance here, but we have confidence that you can figure these problems
out!

#. **Sorting list results**: When a user asks for a list of employers,
   locations, position types, etc., it would be nice if results were
   sorted alphabetically. Make this happen.
#. **Returning a copy of AllJobs**: Look at ``JobData.FindAll()``.
   Notice that it's returning the ``AllJobs`` property, which is a
   static property of the ``JobData`` class. In general, this is not a
   great thing to do, since the person calling our ``FindAll()`` method
   could then mess with the data that ``AllJobs`` contains. Fix this by
   creating a copy of ``AllJobs``. *Hint:* Look at the methods of the ``List`` class listed in the Microsoft documentation.