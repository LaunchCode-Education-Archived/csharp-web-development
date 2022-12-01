.. _model-exercises:

Exercises: Edit Model Classes
=============================

Add functionality to edit event objects in your ``CodingEvents`` application. 
These exercises assume that you have added all of the code from this section of the book and your 
application resembles the `model-binding branch <https://github.com/LaunchCodeEducation/CodingEventsDemo/tree/model-binding>`__.

The edit form will resemble the form used to create an event.

.. admonition:: Tip 

   As you work through these steps, test your code along the way! 
   With each change you apply to your code, ask yourself what you expect to see when the application
   is run. You may not find that all of the steps result in observable changes, though.
   Use Visual Studio’s debugging tools and read your error messages if you run into issues after applying any of
   the changes.

#. Create the two action methods listed below in ``EventsController``. We’ll add code
   to these in a moment, so just put the outline in place for
   now.

   #. Create an action method to display an edit form with this signature:

      .. sourcecode:: csharp
         :linenos:

         public IActionResult Edit(int eventId) {
            // controller code will go here
         }

   #. Create an action method to process the form with this signature:

      .. sourcecode:: csharp
         :linenos:

         [HttpPost]
         public IActionResult SubmitEditEventForm(int eventId, string name, string description) {
            // controller code will go here
         }

#. Add the necessary annotations to the ``SubmitEditEventForm()`` method for it to live at the path ``/Events/Edit``.

   :ref:`Check your solution<model-ex-2>`

#. You’ll need to configure the route for ``Edit()`` to include the path variable ``eventId``, 
   so that paths like ``/Events/Edit/3`` will work.

   :ref:`Check your solution<model-ex-3>`

#. Create an ``Edit.cshtml`` view in ``Views/Events``.

#. Copy the code from ``Add.cshtml`` into ``Edit.cshtml``. 

   #. You'll want to update the text of the submit button and the heading to reflect the edit functionality.

   :ref:`Check your solution<model-ex-5>`

#. Back in ``EventsController``, round out the ``Edit()`` method.

   #. Use an ``EventData`` method to find the event object with the given ``eventId``.
   
   #. Put the event object in ``ViewBag``.

   #. Return the appropriate view.

   :ref:`Check your solution<model-ex-6>`

#. Within the form fields in ``Edit.cshtml``, 

   #. Get the name and description from the event that was passed in via ``ViewBag`` and
      set them as the values of the form fields.
   
   #. Add ``action="/events/edit"`` to the ``form`` tag.

      :ref:`Check your solution<model-ex-7>`

#. Add another input to hold the id of the event being edited. This
   should be hidden from the user:

   .. sourcecode:: html

      <input type="hidden" value="@ViewBag.eventToEdit.Id" name="eventId" />

   .. admonition:: Note

      You may not have named your ``ViewBag`` property ``eventToEdit``.
      Make sure you are using the name you gave your property!

   :ref:`Check your solution<model-ex-8>`

#. Back in the ``Edit()`` action method, add a title to ``ViewBag`` that reads ``“Edit Event
   NAME (id=ID)”`` where ``"NAME"`` and ``"ID"`` are replaced by the values for the
   given event. 

   :ref:`Check your solution<model-ex-9>`

#. In ``SubmitEditEventForm()``, 

   #. Query ``EventData`` for the event being edited with the given id parameter. 
   
   #. Update the name and description of the event.

   #. Redirect the user to ``/Events`` (the event listing page).

   :ref:`Check your solution<model-ex-10>`

#. To access event editing, the user will need an edit option in the list of event data.

   #. In ``Index.cshtml``, add a link to edit the 
      event as a column in the event table:

      .. sourcecode:: html

         <td><a asp-controller="Events" asp-action="Edit" asp-route-id="@evt.Id">Edit Event</a></td>

      ``asp-route-id`` is a new tag helper for us.
      Our routes normally go ``/<controller>/<action>``.
      ``asp-route-id`` passes an ``{id?}`` parameter at the end of our route.
      When the site is built, we can inspect it and see that for the first item in the table this line of HTML will look like:

      .. sourcecode:: html

         <td><a href="/Events/Edit/1">Edit Event</a></td>



   :ref:`Check your solution<model-ex-11>`

