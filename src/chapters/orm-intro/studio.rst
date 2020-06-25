Studio: 
=======

Today's studio depends on completion of the :ref:`exercises <orm1-exercises>`.
If you have not completed the exercises, go back and complete them before continuing with the studio.

The ``EventCategoryController`` Class
-------------------------------------

Create ``EventCategoryController`` in the ``Controllers`` directory.
To get our action methods working, we also need a variable of type ``EventCategoryRepository``.

We will be creating 3 action methods in our controller:

#. ``Index()``
#. ``Create()``
#. ``ProcessCreateEventCategoryForm()``

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