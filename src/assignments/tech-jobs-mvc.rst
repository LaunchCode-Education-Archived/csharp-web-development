.. _tech-jobs-mvc:

Assignment #3: Tech Jobs (MVC Edition)
=======================================

Introduction
------------

Your first two tasks as an apprentice went well! You, Blake, and Sally built
the TechJobs console prototype and then refactored the code to move it to an
object-oriented format.

After demonstrating the prototype for the Company Team at LaunchCode, it
received the green light to be fully built out as a web application.

.. index:: ! minimum viable product

The first step in this process will be to quickly develop a `minimum viable
product <https://en.wikipedia.org/wiki/Minimum_viable_product>`__, or MVP. The
goal is to get a functioning web app up and running with as little work as
possible. That way, additional feedback and testing can be done early in the
development process. After that, additional behind-the-scenes work will be
carried out to fully develop the model and data side of the application.

For this next step in the project, you’ll be working with Carly.

.. figure:: figures/LC-Carly.png
   :scale: 55%
   :alt: Carly's LaunchCode avatar.

Carly was once a LaunchCode apprentice as well, so she knows just what
it’s like to be in your shoes. She’s done some initial work on the
project and left you some ``TODO`` tasks that she knows you can handle.

Learning Objectives
-------------------

In this project, you’ll show that you can:

#. Read and understand code written by others.
#. Work within the controller and view portions of a ASP.NET MVC application.
#. Use Razor syntax to display data within a view.
#. Create new action methods to process form submission.

TechJobs (MVC Edition)
----------------------

You’ll start with some code that Carly has provided. The idea behind your
current assignment is to quickly deliver a functioning ASP.NET MVC application,
so you’ll focus on the controllers and views.

In order to do this, you’ll be reusing the ``JobData`` class and
``job_data.csv`` file from the console app. You will eventually have to go back
and rewrite the data portion of the application to make a true, database-backed
model. However, using the existing ``JobData`` class to provide some basic data
functionality lets you focus on the views and controllers for now.

Your Assignment
---------------

The list below provides a general overview of your assigned tasks. Specific
details for each part appear in the following sections, so be sure to read them
carefully as you solve each problem.

#. Review Carly’s code in the ``JobData`` file as well as in the existing
   controllers and views.
#. Carly needs your help completing the code to display only certain jobs. She has the code to display all of the values that users can select to filter the jobs.
#. Carly started working on the search feature, but only got as far as
   writing the code to display the search form. She’s handed the project to you
   to finish the rest. First, you'll create a controller method to retrieve search results.
#. Finally, you'll display search results in the view. 

Getting Started
----------------

Set up a local copy of the project:

#. In Canvas, **Graded Assignment #3: TechJobs (MVC Edition)** contains a GitHub Classroom assignment invitation link and then set up the project in IntelliJ. Refer back to the GitHub Classroom instructions from :ref:`assignment0` for details. 
#. Launch the application to make sure it starts up properly. Then shut it down.
#. Run the autograding tests. The tests for this assignment are set up the same way as for :ref:`assignment 2 <assignment-2-autograding>`. There are four tasks for this assignment, but the first doesn't require any coding on your part. Therefore, there are 3 tests files (for tasks 2-4). As with assignment 2, we recommend that you only run the tests for the task you are currently working on.


1) Review the Code
-------------------

.. admonition:: Tip

   One essential programming skill that you will develop is the ability to read
   and understand someone else's code. This assignment begins with you
   practicing exactly that. Make sure you carefully examine the provided code
   BEFORE you start changing things.

   Trying to "fix" a code sample before understanding how it works leads to
   confusion, frustration, and a broken program. DO NOT SKIP the code review!

Carly created a ASP.NET MVC application and filled in some features. She
refactored ``JobData`` to generate a List of ``Job`` objects based on
your TechJobs-OO work, and she added controllers and views for a "Home",
"List", and "Search" page. ``JobData`` now also builds Lists for the
``Employer``, ``Location``, ``PositionType``, and ``CoreCompetency`` objects.

The Data and Model
^^^^^^^^^^^^^^^^^^

The "model" is contained in the ``JobData`` class, which is in the ``Data``
folder. We put "model" in quotes, since this class isn’t a model in the
typical, MVC/object-oriented sense (maybe a better name for this assignment
would be *TechJobs VC*).

The ``JobData`` class serves the same purpose as before---it reads data from
the ``job_data.csv`` file and stores it in a format we can use. In this case,
that format is a ``List`` of ``Job`` objects, which is stored in the ``Models`` folder. Note that Carly changed the
path to the ``job_data.csv`` file to store it in the ``Data`` folder too.

You’ll use some of the static methods provided by ``JobData`` in your
controller code. Since you’re already familiar with these, we’ll leave it to
you to review their functionality as you go.

The Controllers
^^^^^^^^^^^^^^^

Expand the ``Controllers`` folder, and you’ll see that you have three
controllers already in place. Let’s look at these one at a time.

The ``HomeController``
~~~~~~~~~~~~~~~~~~~~~~~

This class has only one action method, ``Index()``, which displays the home page
for the app. The controller renders the ``Index.cshtml`` template (in
``Views/Home``) and provides a fairly simple view.

.. figure:: figures/techJobsMvcHome.png
   :alt: TechJobs MVC home screen.

The ``ListController``
~~~~~~~~~~~~~~~~~~~~~~~

This controller provides functionality for users to see either a table showing
all the options for the different ``Job`` fields (``Employer``, ``Location``,
``CoreCompetency``, and ``PositionType``) or a list of details for a selected
set of jobs.

If you look at the corresponding page at ``/list``, you’ll see an "All" column
in the table. However, this option doesn’t work yet, and you will fully
implement the constructor as you work on this project.

At the top of ``ListController`` is a constructor that populates
``ColumnChoices`` and ``TableChoices`` with values. These Dictionaries play the
same role as in the console app, which is to provide a centralized collection
of the different *List* and *Search* options presented throughout the user
interface.

``ListController`` also has ``Index()`` and ``Jobs()`` action
methods. The first method
renders a view that displays a table of clickable links for the different job
categories. The second method needs to render a different view that displays
information for the jobs that relate to a selected category. Both of the
action methods can obtain data by implementing the ``JobData`` class methods.

``Jobs()`` will work similarly to the search functionality, in
that we are "searching" for a particular value within a particular field and
then displaying jobs that match. However, this is slightly different from the
other way of searching in that the user will arrive at this handler method as a
result of clicking on a link within the ``Index.cshtml`` view, rather than via
submitting a form.

The ``SearchController``
~~~~~~~~~~~~~~~~~~~~~~~~~

Currently, the search controller contains only a single method, ``Index``.
It simply renders the form defined in the ``Index.cshtml`` template.

Later in this assignment, you will receive instructions for adding a second
handler to deal with user input and display the search results.

The Views
^^^^^^^^^

Let’s turn our attention to the views.

Bootstrap Classes
^^^^^^^^^^^^^^^^^

The application uses a few Bootstrap classes to style the view content and job tables. You won’t have to explicitly add any Bootstrap classes to your views in this assignment, but it’s a great way to make your sites look good with minimal work.

The List Views
~~~~~~~~~~~~~~~

Turn your attention to ``List/Index.cshtml``. This page displays a table of links
broken down into several categories. Data from ``ColumnChoices`` is used to
fill in the header row, and information stored in ``TableChoices`` generates
the link text.

The most interesting part of this template is how we generate the links:

.. sourcecode:: html
   :lineno-start: 17

   @foreach (var category in ViewBag.tableChoices)
   {
      <td>
         <ul>
         @foreach (var item in category.Value)
         {
            <li>
                  <a asp-controller="List" asp-action="Jobs" asp-route-column="@category.Key" asp-route-value="@item">@item</a>
            </li>
         }
          </ul>
      </td>
   }

#. ``TableChoices`` is a Dictionary from ``ListController``, and it contains the names of
   the ``Job`` fields as keys (``Employer``, etc.). The value for each key is
   a List of ``Employer``, ``Location``, ``CoreCompetency``, or
   ``PositionType`` objects.
#. In line 17, ``category`` represents one key/value pair from
   ``TableChoices``, and in line 21, ``item`` represents one entry from the
   stored ``List``.
#. We’ve seen some of the syntax to generate a link within a Razor
   template, but we don't have as much experience with ``asp-route-column`` and ``asp-route-value``.This syntax causes Razor
   to dynamically generate query parameters for our URL.

In line 24, we set these parameters by using ``asp-route-column=`` and ``asp-route-value=``. The
values of these parameters are determined dynamically based on
``@category.key`` and ``@item``. Since these values come from
``TableChoices``, the *keys* will be ``employer``, ``location``, etc. The
*values* will be the individual elements from the related ``List``. When the
user clicks on these links, they will be routed to the
``Jobs()`` action method in ``ListController``, which looks for
these parameters.

By the end of your work on this project, clicking on one of the links display a list of jobs that relate to the
choice, via the ``Jobs()`` action method.

For now, click one of the *Location* links. This sends a request as we
outlined above, but doing so only leads to an error.

Once you have completed the project, the page you will see at ``/list/values?column=location&value=...`` is generated by
the ``Jobs.cshtml`` template. It has a similar structure as ``Index.cshtml``,
but the table consists of only one column.

.. admonition:: Note

   Select "Kansas City" from the list of locations, and then check the address
   bar of your browser:

   .. sourcecode:: bash

      /list/jobs?column=location&value=Kansas%20City

   Razor inserts ``%20`` for us, to represent a space, but this may
   actually be hidden in your browser’s address bar.

The Search View
~~~~~~~~~~~~~~~~

Finally, click on *Search* from the home page, or the navigation bar, and open
up ``Search/Index.cshtml`` in Visual Studio. You’ll see a search form (in both the browser
and template file) that gives the user the option of searching by a given
``Job`` field, or across all fields. This is an exact visual analog of our
console application.

This template will be used to display search results, in addition to rendering
the form. This will give the nice user experience of easily searching multiple
times in a row.

Wrap Up the Code Review
^^^^^^^^^^^^^^^^^^^^^^^^

Once you understand the controllers and views that are already in place, you’re
ready to begin your work.

In Visual Studio, select *View > Tasks* to pop open a small pane at
the bottom of the window. This list is populated by any code comments that
start with ``TODO``. You’ll see your tasks listed, and clicking on any one will
open the relevant file.

.. admonition:: Note

   You may not see a ``TODO #4``. This is because TODO comments in views do not always show up in the Task List.
   If it is not there, check out the ``Search/Index.cshtml`` view to locate it!

2) Complete ``ListController``
------------------------------

Complete the ``Jobs()`` action method in ``ListController``. Right now, it returns a view, but we need to send some details about jobs to that view.

#. The view relies on ``ViewBag.jobs``, so to start create a list in the action method called ``jobs``.
#. If the user selects "View All", you should use ``JobData.FindAll()`` to populate ``jobs`` with all the jobs and update ``ViewBag.title``. If the user selects something specific, you should use ``JobData.FindJobsByColumnAndValue()`` to populate ``jobs`` with jobs that only match that criteria and update ``ViewBag.title`` to include the criteria the user chose.
#. Make sure to set ``ViewBag.jobs`` equal to ``jobs`` and run the program to see how it is working now!

If everything looks good to you, run the tests in ``TestTaskTwo`` in ``AutogradingTests`` to make sure you are on the right track before proceeding to task three.

3) Complete ``SearchController``
-------------------------------------

Add a ``Results()`` action method to ``SearchController``:

#. The ``Results()`` method should take in two parameters. Both parameters must be strings and the first one should be called "searchType" and the second one should be called "searchTerm".
#. First, you need to create a local variable called "jobs" that is of type ``List<Job>``.
#. If the user enters "all" in the search box, or if they leave the box empty,
   call the ``FindAll()`` method from ``JobData``. Otherwise, send the search
   information to ``FindByColumnAndValue``. In either case, store
   the results in a ``jobs`` List.
#. Pass ``jobs`` into the ``Index.cshtml`` view.
#. Pass ``ListController.ColumnChoices`` into the view, as the existing
   ``Index()`` action method does.

Run the tests in ``TestTaskThree`` to see how you did!

4) Display Search Results
-------------------------

.. admonition:: Note

   Before starting this task, un-comment out the tests in ``TestTaskFour``. You can do so by removing the ``/*`` on line 18 and the ``*/`` on line 44.

Once you have your ``Results()`` action method passing information to the
view, you need to display the data.

#. In ``Index.cshtml``, create a loop to display each job passed in from the
   controller.
#. Put the job results into a set of tables, similar to what you did for the
   ``List/Jobs.cshtml`` view.

Run the tests in ``TestTaskFour`` to make sure that you have passed everything properly to the view!

Sanity Check
-------------

At this point, all autograding tests should be passing. To be sure, run all the tests at once and if any are failing, evaluate the error message and go back and fix your code.

How to Submit
--------------

To turn in your assignment and get credit, follow the
:ref:`submission instructions <submitting-your-work>`.

Bonus Missions
--------------

Here are some additional challenges, for those willing to take them on:

#. When we select a given field to search within and then submit, our choice is
   forgotten and returns to "All" by default. Modify the view template to keep
   the previous search field selected when displaying the results.
#. In the tables displaying the full job data, find a way to manipulate the
   font, style, capitalization, etc. to further distinguish the labels from the
   data (e.g. **Employer:** *LaunchCode*). (*Hint:* We capitalize the title
   string in multiple templates, so have a look around).
#. In the tables of the job results, make each value (except ``name``)
   hyperlinked to a new listing of all jobs with that same value. For example,
   if we have a list of jobs with the ``JavaScript`` skill, clicking on a
   location value like ``Saint Louis`` will generate a new list with all the
   jobs available in that city.