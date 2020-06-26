.. _orm1-exercises:

Exercises: OMG the ORM!
=======================

For the exercises, we are going to continue building on our ``CodingEvents`` application.
The exercise instructions assume that your code resembles the `orm1 <https://github.com/LaunchCodeEducation/CodingEventsDemo/tree/orm1>`_ branch.
Create a new branch off of your ``orm1`` code to get started on the exercises. 

.. admonition:: Note

   You will be making one model class and adding to ``DbContext``.
   If you are not sure what these classes should look like, refer back to the sections on persistent models and ``DbContext``.

The ``EventCategory`` Class
---------------------------

First, create a new class called ``EventCategory`` in the ``Models`` directory.

``EventCategory`` needs to have the following:

#. An ``Id`` property of type ``int``.
#. A ``Name`` property of type ``string``.
#. A constructor.

``EventCategory`` represents data that will be stored in our database.

Adding to ``DbContext``
-----------------------

Once you have created ``EventCategory``, you need to add to ``EventDbContext`` to set up a table in the database for storing categories.

Adding a New Table to the Database
----------------------------------

With the two steps completed above, you now need to add a new migration and update your database.
You should now see a new table in your database!

The ``EventCategoryController`` Class
-------------------------------------

Create ``EventCategoryController`` in the ``Controllers`` directory.
To get our action methods working, we also need a variable of type ``EventDbContext``.

For now, we are just going to set up our ``Index()`` action method so that it displays all of the categories in our table.

``Index()``
^^^^^^^^^^^

``Index()`` needs to do the following:

#. Use ``[HttpGet]`` and return ``"eventCategories/index"``.
#. Add a property for the ``categories`` that uses all of the values in your ``EventDbContext`` variable.

Adding a View
-------------

Create an ``EventCategory`` directory inside of our ``Views`` directory.
Add a new view called ``Index.cshtml``.

``Index.cshtml`` needs to have the following:

#. An ``h1`` with an appropriate heading for the page.
#. A table that will display all of the category names of the event categories stored in our database.

Test Your Application
---------------------

If you navigate to ``localhost:5001/eventcategory``, you will see an empty table on the page.
That is what you should see!
We haven't added the ability to add a new category to our table yet. 
We will do so in the :ref:`studio <orm1-studio>` this week.