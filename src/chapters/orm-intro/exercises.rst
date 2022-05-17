.. _orm1-exercises:

Exercises: OMG the ORM!
=======================

For the exercises, we are going to continue building on our ``CodingEvents`` application.
The exercise instructions assume that your code resembles the `persistent-controller <https://github.com/LaunchCodeEducation/CodingEventsDemo/tree/persistent-controller>`_ branch.
Create a new branch in your own ``CodingEvents`` repo to get started on the exercises. 

.. admonition:: Note

   You will be making one model class and adding to ``DbContext``.
   If you are not sure what these classes should look like, refer back to the :ref:`section <intro-to-data-stores>` on data stores and ``DbContext``.

The ``EventCategory`` Class
---------------------------

First, create a new class called ``EventCategory`` in the ``Models`` directory.

``EventCategory`` needs to have the following:

#. An ``Id`` property of type ``int``.
#. A ``Name`` property of type ``string``.
#. A no arg constructor.
#. A constructor that sets the value of ``Name``.

``EventCategory`` represents data that will be stored in our database.

:ref:`Check your solutions<orm1-ex-1>`

Adding to ``DbContext``
-----------------------

Once you have created ``EventCategory``, you need to add to ``EventDbContext`` to set up a table in the database for storing categories.

:ref:`Check your solutions<orm1-ex-2>`

Adding a New Table to the Database
----------------------------------

With the two steps completed above, you now need to add a new migration and update your database.
You should see a new table in your database!

The ``EventCategoryController`` Class
-------------------------------------

Create ``EventCategoryController`` in the ``Controllers`` directory.
To get our action methods working, we also need a variable of type ``EventDbContext``.

For now, we are just going to set up our ``Index()`` action method so that it displays all of the categories in our table.

``Index()``
^^^^^^^^^^^

``Index()`` needs to do the following:

#. Responds to ``GET`` requests at ``EventCategory/Index`` and returns a view called ``Index.cshtml``.
#. Pass the ``DbContext`` category values as a list into the view template as a model.

:ref:`Check your solutions<orm1-ex-3>`

Adding a View
-------------

Create an ``EventCategory`` directory inside of our ``Views`` directory.
Add a new view called ``Index.cshtml``.

``Index.cshtml`` needs to have the following:

#. Use the list passed in from the action method in the controller as a model to populate the view.
#. An ``h1`` with an appropriate heading for the page.
#. A table that will display all of the category names of the event categories stored in our database.

:ref:`Check your solutions<orm1-ex-4>`

Test Your Application
---------------------

If you navigate to the ``/eventcategory`` route, you will see an empty table on the page.
That is what you should see!
We haven't added the ability to add a new category to our table yet. 
We will do so in the :ref:`studio <orm1-studio>` this week.