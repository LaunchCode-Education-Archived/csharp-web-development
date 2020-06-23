.. _orm1-exercises:

Exercises: OMG the ORM!
=======================

For the exercises, we are going to continue building on our ``CodingEvents`` application.
The exercise instructions assume that your code resembles the `orm1 <https://github.com/LaunchCodeEducation/CodingEventsDemo/tree/orm1>`_ branch.
Create a new branch off of your ``orm1`` code to get started on the exercises. 

.. admonition:: Note

   You will be making one entity class, one repository, and one controller.
   If you are not sure what these classes and interface should look like, refer back to the sections on `persistent models <>`_ and `controllers and repositories <>`_.

The ``EventCategory`` Class
---------------------------

First, create a new class called ``EventCategory`` in the ``<odels`` directory.

``EventCategory`` needs to have the following:

#. An ``Id`` property of type ``int``.
#. A ``Name`` property of type ``string``.
#. A constructor.

``EventCategory`` represents data that will be stored in our database.

The ``EventCategoryRepository`` Interface
-----------------------------------------

Once you have created ``EventCategory``, you need to create the ``EventCategoryRepository`` in the ``Data`` folder.
``EventCategoryRepository`` will extend ``EventCategory``.

The ``EventCategoryController`` Class
-------------------------------------

Create ``EventCategoryController`` in the ``Controllers`` directory.
To get our action methods working, we also need a variable of type ``EventCategoryRepository``.

We will be creating 3 action methods in our controller:

#. ``DisplayAllEvents``
#. ``RenderCreateEventCategoryForm``
#. ``ProcessCreateEventCategoryForm``

``DisplayAllEvents``
^^^^^^^^^^^^^^^^^^^^

``DisplayAllEvents`` needs to do the following:

#. Use ``[HttpGet]`` and return ``"eventCategories/index"``.
#. Add a property for the ``title`` that uses ``"All Categories"``.
#. Add a property for the ``categories`` that uses all of the values in your ``EventCategoryRepository`` variable.

``RenderCreateEventCategoryForm``
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

``RenderCreateEventCategoryForm`` needs to do the following:

#. Use ``[HttpGet]`` and return ``"eventCategories/create"``.
#. Add a property for the ``title`` and assign it ``"Create Category"``.
#. Add a property for a new instance of ``EventCategory``.

``ProcessCreateEventCategoryForm``
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

``ProcessCreateEventCategoryForm`` needs to do the following:

#. Use ``[HttpPost]``.
#. Use error validation and ``ModelState.IsValid`` appropriately. If you want to review how to use ``ModelState.IsValid``, check out the section on :ref:`error validation <validating-models>`.
#. Add a property for the ``title`` and assign it ``"Create Category"``.
#. Add a property for a new instance of ``EventCategory``.
#. Either return ``"eventCategories/create"`` or ``Redirect()``.

Razor Templates
---------------

To finish the exercises, we need to make two new templates.

#. ``EventCategories/Index.cshtml``, which will contain a table of the event categories.
#. ``EventCategories/Create.cshtml``, which will contain a form for adding new event categories.

The Final Application
---------------------

Once you are done, launch your app and head to ``localhost:5001/eventCategories``!
If you added categories already, you will see any categories already stored in the database.
In this case, we added "Meetup" as a category the first time we ran our app to test it.

.. TODO: Add figure showing categories table with only Meetup in it

If you click on "Create Category", you should be directed to ``localhost:5001/eventCategories/create``.
We decided to add "Networking" as a category and filled out the form.

.. TODO: Add figure showing the category form filled out with the word Networking

Once you hit submit, you are redirected back to ``localhost:5001/eventCategories``, and your table now contains the newest event category!

.. TODO: Add figure showing categories table with Meetup and Networking in it.
