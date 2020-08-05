.. _tech-jobs-persistent:

Assignment #4: Tech Jobs (Persistent Edition)
=============================================

Your Task
---------

You will once again work with the ``TechJobs`` application. This time around you'll add ORM
functionality by using Entity Framework. You will be responsible for completing the code to allow users
to create new job data.

Your final application will have the same list and search capabilities as your :ref:`Tech Jobs (MVC Edition) <tech-jobs-mvc>` but
you'll need to do the work to connect the project to a database for storing user-submitted job data.

Each of the three sections of this assignment will also ask you to demonstrate your SQL skills under an item labelled **SQL TASK**.

Checkout and Review the Starter Code
------------------------------------

Fork and clone the starter code from the `repository <https://github.com/LaunchCodeEducation/TechJobsPersistent>`__.

You will be able to run your application without any build errors. However, you'll likely see a host of errors relating to the
Entity Framework annotations and classes when you attempt to add any data or load different pages.
Some of these have already been added but the connection to the database has not been set up yet.
That will be one of your tasks. You'll need to complete :ref:`Part1 <tech-jobs-persistent-pt1>` before you can
thoroughly check out the project running in the browser.

That said, it's a good idea to scan the classes and templates even before you're able to run the application. 
Take a gander at the ``Job`` class. It will look somewhat similar to the model in
:ref:`Tech Jobs (MVC Edition) <tech-jobs-mvc>`, with a few key differences.

You're no longer using a csv file to load job data, instead, we'll be creating new ``Job`` objects via a
user form. The job data will be stored in a MySQL database that you'll setup in :ref:`Part 1 <tech-jobs-persistent-pt1>` of this assignment.

As you explore
the starter code, you'll notice that the ``JobField`` class is missing. You will focus on just two aspects of a job listing: the employer and the skills required.
Your task for :ref:`Part 2 <tech-jobs-persistent-pt2>` is to add code to let a user create an employer object.

The ``Job`` class will also look different from how you have last seen it.
In :ref:`Part 3 <tech-jobs-persistent-pt3>`, you will use the many-to-many relationship between skills and jobs to make it easier for users to add skills to new jobs.
In your ASP.NET project, you'll see an empty file in the solution called ``queries.sql``. After completing the
C# updates for parts 1, 2, and 3, we ask you to test your application updates with SQL statements.

Since you are entering your own data, the queries we ask you to write will return unique result sets. For example, if you haven't entered
any data yet, there may be an empty result set. However, as the architect of the database, you have the knowledge to write the
appropriate queries nonetheless.

.. _tech-jobs-persistent-pt1:

Part 1: Connect a Database to an ASP.NET App
--------------------------------------------

#. Start MySQL Workbench and create a new schema named ``techjobs``.

   .. admonition:: Tip

      Remember to double click on the schema name in the file tree to make it the default schema.

#. In the administration tab, create a new user, ``techjobs`` with the same settings as described in
   the lesson tutorial.

#. Make sure that ``TechJobsPersistent`` has all of the necessary dependencies.

#. Read through the code that is currently in ``JobDbContext`` to get an idea for what the database will look like.

#. Update ``appsettings.json`` with the right info. This will include the name of the database, as well as the username and password
   for a user you have created.

#. Check that ``ConfigureServices`` in ``Startup.cs`` includes the configuration for the database.

   .. admonition:: Tip

      You can double check your setup against what you've already done for
      :ref:`your CodingEvents repo <setup-orm-database>`. You can copy these property assignments from your ``CodingEvents`` repo, only needing to change the database address and username/password values.

#. Run a new migration and update the database.

Test It with SQL
^^^^^^^^^^^^^^^^

#. In your MySQL workbench, open a new query tab to check your database connection.

#. **SQL TASK:** At this point, you will have tables for ``Jobs``, ``Employers``, ``Skills``, and ``JobSkills``. In ``queries.sql`` under "Part 1", list the columns and their data types
   in the ``Jobs`` table.

Your running application still has limited functionality. You won't yet be able to add a job with the *Add Job* form. You also
won't yet be able to view the list of jobs or search for jobs - but this is mostly because you have no job data. Move on to
Part 2 below to start adding these functionalities.

.. _tech-jobs-persistent-pt2:

Part 2: Adding Employers
------------------------

You will need to have completed the :ref:`setup steps <tech-jobs-persistent-pt1>` before starting this
section.

ViewModels
^^^^^^^^^^ 

#. Create a new ViewModel called ``AddEmployerViewModel`` that has 2 properties: ``Name`` and ``Location``.

   .. admonition:: Note

      For the purposes of this application, an employer can only have one location.

#. Add validation to both properties in the ViewModel so that both properties are required.

Controllers
^^^^^^^^^^^

``EmployerController`` contains four relatively empty action methods. Take the following steps to handle traffic between the views and the model:

#. Set up a private ``DbContext`` variable so you can perform CRUD operations on the database. Pass it into a ``EmployerController`` constructor.
#. Complete ``Index()`` so that it passes all of the ``Employer`` objects in the database to the view. 
#. Create an instance of ``AddEmployerViewModel`` inside of the ``Add()`` method and pass the instance into the ``View()`` return method.
#. Add the appropriate code to ``ProcessAddEmployerForm()`` so that it will process form submissions and make sure that only valid ``Employer`` objects are being saved to the database.
#. ``About()`` currently returns a view with vital information about each employer such as their name and location. Make sure that the method is actually passing an ``Employer`` object to the view for display.

Views
^^^^^

The starter code comes with 3 views in the ``Employer`` subdirectory.
Read through the code in each view.
You may have to add models or make sure naming is consistent between the controller and the view.

Adding a Job
^^^^^^^^^^^^

One important feature of your application is a form to add a new job.
Two action methods in ``HomeController``, ``AddJob()`` and ``ProcessAddJobForm()``, will work together to return the view that contains the form and handle form submission.
In the ``Home`` subdirectory in ``Views``, you will find an ``AddJob.cshtml`` file which contains the beginning of the form.
Right now, there is only one field to the form and that is for the job's name.
As you work on the application, you will add more fields to this form to add employer and skill info.

#. Create a new ViewModel called ``AddJobViewModel``. You will need properties for the job's name, the selected employer's ID, and a list of all employers as ``SelectListItem``.

   .. admonition:: Note

      This is different from the given ViewModel, ``JobDetailViewModel``.
      ``JobDetailViewModel`` has properties for the selected employer's info and the selected skill's info.
      ``AddJobViewModel`` has properties for all of the employers and skills in the database.
      We need both ViewModels for the application.
      If you want to see more of ``JobDetailViewModel`` in action, check out ``ListController`` and ``SearchController``.

#. In ``AddJob()`` pass an instance of ``AddJobViewModel`` to the view.
#. In ``AddJob.cshtml``, add a new ``<div class="form-group">`` element to the form.
   Add the appropriate ``<label>`` and ``<input>`` tags to the new ``<div>`` element to create the form field to add employer information to the job.
   This field should be a dropdown menu with all of the employers in the database.
   In addition, add a link to the ``<div>`` element to add new employers.
   This way, if a user doesn't see the employer they are looking for, they can easily click on the link and add a new employer to the database.
#. In ``ProcessAddJobForm()``, you need to take in an instance of ``AddJobViewModel`` and make sure that any validation conditions you want to add are met before creating a new ``Job`` object and saving it to the database.

Test It with SQL
^^^^^^^^^^^^^^^^

Before you move on, test your application now to make sure it runs as expected.
You should be able to create Employer objects and view them.

#. Open *MySQL Workbench* and make sure you have an ``Employers`` table and that it is empty.

#. Start up your application – don’t forget to have your SQL server running – and go to the *Add Jobs*
   view.

#. You won't be able to add a job yet, but you'll see a link to *Add Employers* in the form. Click on it and proceed
   to check the functionality of the form that follows.

#. Be sure to test your validation requirements and error handling.

#. **SQL TASK:** In ``queries.sql`` under "Part 2", write a query to list the names of the employers in St. Louis City.

.. admonition:: Tip

   If everything seems to work – that is, you are
   able to submit the form without any errors – but you don’t see your
   employers in the list after submission, here’s what you should check:

   #. Is there any data in the ``Employers`` table? Check by going to MySQL Workbench
      and looking for the employer data within your schema.

   #. If there’s data in the database, check that you are correctly
      querying for the list of all objects in the controller
      Are you calling for the proper list with ``DbContext``?

   #. Ensure you’re passing the list into the view.

   When everything works, move on to Part 3 below.

.. _tech-jobs-persistent-pt3:

Part 3: Working with a Many-To-Many Relationship
------------------------------------------------

Using a many-to-many relationship, we can use the ``JobSkill`` object to store a ``Job`` object's skills. 
Just as a job requires many skills, any skill can be associated with several jobs.
With this in mind, the form to add a job needs to contain all of the skills available as checkboxes so users can add the necessary skills when they create a job.

Review Existing Code
^^^^^^^^^^^^^^^^^^^^

Before diving into this section, make sure that you have read through all models, ViewModels, views, and ``SkillController`` to see how the exisiting features and functions to add skills and add a skill to a job work.

Updaing ``AddJobViewModel``
^^^^^^^^^^^^^^^^^^^^^^^^^^^

In order to add additional functionality to the form for adding a job, we need to add properties to ``AddJobViewModel``.

#. Add a property for a list of each ``Skill`` object in the database.
#. Previously, in an ``AddJobViewModel`` constructor, you probably set up a ``SelectListItem`` list of ``Employer`` information.
   Pass another parameter of a list of ``Skill`` objects. Set the ``List<Skill>`` property equal to the parameter you have just passed in.

Updating ``HomeController``
^^^^^^^^^^^^^^^^^^^^^^^^^^^

You next need to update ``HomeController`` so that skills data is being shared with the form and that the user's skill selections are properly handled.

#. In the ``AddJob()`` method, update the ``AddJobViewModel`` object so that you pass all of the ``Skill`` objects in the database to the constructor.
#. In the ``ProcessAddJobForm()`` method, pass in a new parameter: an array of strings called ``selectedSkills``.
   When we allow the user to select multiple checkboxes, the user's selections are stored in a string array.
   The way we connect the checkboxes together is by giving the ``name`` attribute on the ``<input>`` tag the name of the array.
   In this case, each ``<input>`` tag on the form for the skills checkboxes should have ``"selectedSkills"`` as the name.

   a. After you add a new parameter, you want to set up a loop to go through each item in ``selectedSkills``. This loop should go right after you create a new ``Job`` object and before you add that ``Job`` object to the database.
   b. Inside the loop, you will create a new ``JobSkill`` object with the newly-created ``Job`` object. You will also need to parse each item in ``selectedSkills`` as an integer to use for ``SkillId``.
   c. Add each new ``JobSkill`` object to the ``DbContext`` object, but do not add an additional call to ``SaveChanges()`` inside the loop! One call at the end of the method is enough to get the updated info to the database.

Updating ``Home/AddJob.cshtml``
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Now that we have the controller and ViewModel set up, we need to update the form to add a job.

#. Add a new ``<div class="form-group">`` element to the form for collecting skills.
#. Loop through each object in the list of ``Skill`` objects.
#. Give each checkbox a label and add the checkbox input itself.
   Here is an example of how that ``<input>`` tag might look:

   .. sourcecode:: guess

      <input type="checkbox" name="selectedSkills" value="@skill.Id" />

#. Add a link to the form to add skills to the database so if a user doesn't see the skills they need, they can add skills themselves!

Test It with SQL
^^^^^^^^^^^^^^^^

Run your application and make sure you can create a new job with an employer and several skills. You should now also have restored
full list and search capabilities.

#. **SQL TASK:** In ``queries.sql`` under "Part 3", write a query to return a list of the names
   and descriptions of all skills that are attached to jobs in alphabetical order.
   If a skill does not have a job listed, it should not be
   included in the results of this query.

   .. admonition:: Tip

      You will need to make use of "is not null".

When you are able to add new employers and skills and use those objects to create a new job, you’re done! Congrats!


How to Submit
-------------

To turn in your assignment and get credit, follow the :ref:`submission instructions <how-to-submit-work>`.

