Exercise Solutions: Razor Views
===============================

Line numbers are for reference. They may not match your code exactly.

Expanding our Events Schedule
-----------------------------

.. _view-dictionary:

2. Update the ``Events/Add.cshtml`` template with a new field for a user to submit an event description.

.. sourcecode:: html

   <h1>Add Event</h1>

   <form method="post">
      <label for="name">Name</label>
      <input name="name" type="text" />
      <label for="desc">Description</label>
      <input name="desc" />
      <input type="submit" value="Add Event" />
   </form>

.. _view-kvp:

:ref:`Return to exercises<ex-part-1>`  

3. Back in ``EventsController.cs``, add the description parameter to the ``NewEvent`` action 
   method and within the method, add the new event key/value pair to the ``Events`` dictionary.

.. sourcecode:: csharp

   [HttpPost]
   [Route("Events/Add")]
   public IActionResult NewEvent(string name, string desc)
   {
      Events.Add(name, desc);

      return Redirect("/Events");
   }

.. _view-table:

:ref:`Return to exercises<ex-part-1>`

4. Now to ``Events/Index.cshtml``. Replace the ``ul`` with a ``table`` to display event names and descriptions.

.. sourcecode:: csharp
   :linenos:

      // inside the "else" block 
      <table>
         <tr>
            <th>
               Name
            </th>
            <th>
               Description
            </th>
         </tr>
         @foreach (KeyValuePair<string, string> evt in ViewBag.events)
         {
            <tr>
               <td>@evt.Key</td>
               <td>@evt.Value</td>
            </tr>
         }
      </table>

.. _view-layout:

:ref:`Return to exercises<ex-part-1>`

5. Lastly, modify ``_Layout.cshtml`` to display links for the Coding Events app (only ``Events/Index`` and ``Events/Add`` for now).


.. sourcecode:: html
   :linenos:

      <header>
      <!-- html code -->
         <div class="navbar-collapse collapse d-sm-inline-flex flex-sm-row-reverse">
            <ul class="navbar-nav flex-grow-1">
               <li class="nav-item">
                  <a class="nav-link text-dark" asp-area="" asp-controller="Events" asp-action="Add">Add</a>
               </li>
            </ul>
         </div>
      <!-- more html -->
      </header>

:ref:`Return to exercises<ex-part-1>`