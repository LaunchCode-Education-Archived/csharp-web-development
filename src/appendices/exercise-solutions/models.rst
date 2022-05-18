.. _model-ex-2:

Exercises Solutions: Edit Model Classes
=======================================

Line numbers are for reference. They may not match your code exactly.

.. _model-ex-3:

2. Add the necessary annotations to the ``SubmitEditEventForm()`` method for it to live at the path ``/Events/Edit``.  See **Line 2**.

   .. sourcecode:: csharp
      :linenos:

         [HttpPost]
         [Route("Events/Edit")]
         public IActionResult SubmitEditEventForm(int eventId, string name, string description)
         {
            // controller code will go here
         }
   
   :ref:`Back to exercises<model-exercises>`

.. _model-ex-5:


3. You’ll need to configure the route for ``Edit()`` to include the path variable ``eventId``, so that paths like ``/Events/Edit/3`` will work.  See **Line 2**.

   .. sourcecode:: csharp
      :linenos:

         [HttpPost]
         [Route("Events/Edit/{eventId}")]
         public IActionResult Edit(int eventId)
         {
            // controller code will go here
         }


   :ref:`Back to exercises<model-exercises>`

.. _model-ex-6:

5. Copy the code from ``Add.cshtml`` into ``Edit.cshtml``. 
   
   a. You’ll want to update the text of the submit button and the heading to reflect the edit functionality.

   .. sourcecode:: html
      :linenos:

         <h1>Edit Event</h1>

         <form method="post">
            <div class="form-group">
               <label for="name">Name</label>
               <input name="name" type="text" />
            </div>
            <div class="form-group">
               <label for="description">Description</label>
               <input name="description" />
            </div>
            <input type="submit" value="Edit Event" />
         </form>


   :ref:`Back to exercises<model-exercises>`

.. _model-ex-7:

6. Back in ``EventsController``, round out the ``Edit()`` method.

   .. sourcecode:: csharp
      :linenos:

         [HttpGet]
         [Route("Events/Edit/{eventId}")]
         public IActionResult Edit(int eventId)
         {
            Event editingEvent = EventData.GetById(eventId);
            ViewBag.eventToEdit = editingEvent;
            return View();
         }

   :ref:`Back to exercises<model-exercises>`

.. _model-ex-8:

7. Within the form fields in ``Edit.cshtml``,

   a. Get the name and description from the event that was passed in via ``ViewBag`` and set them as the values of the form fields.
   b. Add ``action="/events/edit"`` to the form tag.

   .. sourcecode:: html
      :linenos:

         <h1>@ViewBag.title</h1>

         <form method="post" action="/events/edit">
            <div class="form-group">
               <label for="name">Name</label>
               <input name="name" type="text" value="@ViewBag.eventToEdit.Name"/>
            </div>
            <div class="form-group">
               <label for="description">Description</label>
               <input name="description" type="text" value="@ViewBag.eventToEdit.Description" />
            </div>
            <input type="submit" value="Edit Event" />

         </form>


   :ref:`Back to exercises<model-exercises>`

.. _model-ex-9:

8. Add another input to hold the id of the event being edited. This should be hidden from the user:

   .. sourcecode:: html
      :lineno-start: 10      
         
            <!-- description div code here -->
            </div>
            <input type="hidden" value="@ViewBag.eventToEdit.Id" name="eventId">
            <input type="submit" value="Edit Event" />
         </form>


   :ref:`Back to exercises<model-exercises>`

.. _model-ex-10:

9. Back in the ``Edit()`` action method, add a title to ``ViewBag`` that reads ``“Edit Event NAME (id=ID)”`` where ``"NAME"`` and ``"ID"`` are replaced by the values for the given event.

   .. sourcecode:: csharp
      :linenos:

         [HttpGet]
         [Route("Events/Edit/{eventId}")]
         public IActionResult Edit(int eventId)
         {
            Event editingEvent = EventData.GetById(eventId);
            ViewBag.eventToEdit = editingEvent;
            ViewBag.title = "Edit Event " + editingEvent.Name + "(id = " + editingEvent.Id + ")";
            return View();
         }


   :ref:`Back to exercises<model-exercises>`

.. _model-ex-11:

10. In ``SubmitEditEventForm()``,
   
a. Query ``EventData`` for the event being edited with the given id parameter.
b. Update the name and description of the event.
c. Redirect the user to ``/Events`` (the event listing page).

   .. sourcecode:: csharp
      :linenos:
      
         [HttpPost]
         [Route("Events/Edit")]
         public IActionResult SubmitEditEventForm(int eventId, string name, string description)
         {
            Event editingEvent = EventData.GetById(eventId);
            editingEvent.Name = name;
            editingEvent.Description = description;
            return Redirect("/Events");
         }

:ref:`Back to exercises<model-exercises>`



11. In ``Index.cshtml``, add a link to edit the event as a column in the event table.  See **Line 38**.

   .. sourcecode:: html
      :lineno-start: 32

         @foreach (var evt in ViewBag.events)
            {
               <tr>
                  <td>@evt.Id</td>
                  <td>@evt.Name</td>
                  <td>@evt.Description</td>
                  <td><a asp-controller="Events" asp-action="Edit" asp-route-id="@evt.Id">Edit Event</a></td>
               </tr>
            }
         </table>

:ref:`Back to exercises<model-exercises>`

   
