.. _orm1-studio:

Studio: OMG More ORM!
=====================

Today's studio depends on completion of the :ref:`exercises <orm1-exercises>`.
If you have not completed the exercises, go back and complete them before continuing with the studio.
If you want to check out one possible solution to the exercises before you get started, look at the `studio16-starter <https://github.com/LaunchCodeEducation/CodingEventsDemo/tree/studio16-starter>`__ branch in ``CodingEventsDemo``.

Adding a ViewModel
------------------

With the new table set up in our database and our application displaying event categories, we need to add a ViewModel so we can add validation for new event categories.
Create a new ViewModel called ``AddEventCategoryViewModel``.
Add one property to your ViewModel for the name of the event category.
Add validation attributes to the property so that it is required and that it has to be between 3 and 20 characters long.

Updating ``EventCategoryController``
------------------------------------

We will be creating 2 new action methods in our controller:

#. ``Create()``
#. ``ProcessCreateEventCategoryForm()``

``Create()``
^^^^^^^^^^^^

``Create()`` needs to do the following:

#. Responds to ``GET`` requests at ``EventCategory/Create`` and returns a view called ``Create.cshtml``.
#. Pass a new instance of ``AddEventCategoryViewModel`` to ``View()``.

``ProcessCreateEventCategoryForm()``
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

``ProcessCreateEventCategoryForm()`` needs to do the following:

#. Responds to ``POST`` requests at the route of your choosing.
#. Use error validation and ``ModelState.IsValid`` appropriately. If you want to review how to use ``ModelState.IsValid``, check out the section on :ref:`error validation <validating-models>`.
#. Create a new instance of ``EventCategory`` and add it to the database if the form input meets the validation conditions.
#. Either reload the form or add a new event category to the database and direct the user back to the ``EventCategory/Index.cshtml`` template.

Razor Templates
---------------

To finish the studio, we need to make a new template, ``EventCategory/Create.cshtml``, which will contain a form for adding new event categories.

We also need to add links to the pages for all of the events, all of the event categories, and the form to add a new event category to the navbar.
To do so, open up ``_Layout.cshtml`` and scroll down to approximately line 24 where you find the code for the link to add an event:

.. sourcecode:: guess
   :lineno-start: 24

   <li class="nav-item">
      <a class="nav-link text-dark" asp-area="" asp-controller="Events" asp-action="Add">Add</a>
   </li>

Using this code as a template, add links to the ``Events/Index.cshtml``, ``EventCategory/Create.cshtml``, and ``EventCategory/Index.cshtml`` views.

The Final Application
---------------------

Once you are done, launch your app and head to the ``/EventCategory`` route!
If you added categories already, you will see any categories already stored in the database.

If you click on "Create Category", you should be directed to the ``/EventCategory/Create`` route.
Once you hit submit, you are redirected back to ``/EventCategory``, and your table now contains the newest event category!
