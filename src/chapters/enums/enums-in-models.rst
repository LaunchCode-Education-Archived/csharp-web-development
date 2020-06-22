Enums in Model Classes
======================

One application of enum types is to represent categories of objects. We will take this approach in our ``CodingEvents`` application to categorize events based on their type, such as *conference* or *meetup*.

Enum Types in Models - Video
----------------------------

.. youtube::
   :video_id: Lmt_P3XYYvk

.. admonition:: Note

   If you ever want to verify what code the video starts with, check out the `display-error-messages <https://github.com/LaunchCodeEducation/CodingEventsDemo/tree/display-error-messages>`__ branch in ``CodingEventsDemo``.
   If you ever want to verify what code the video ends with, check out the `enums <https://github.com/LaunchCodeEducation/CodingEventsDemo/tree/enums>`__ branch in ``CodingEventsDemo``.

Enum Types in Models - Text
---------------------------

Create an Enum Class
^^^^^^^^^^^^^^^^^^^^

In your ``Models`` directory within ``CodingEvents``, create a new class called ``EventType``. 
Replace the ``class`` keyword with ``enum`` and delete the default constructor.

Each value is demarcated with a comma.

``EventType``:

.. sourcecode:: csharp
   :lineno-start: 4

   public enum EventType
   {
      Conference,
      Meetup,
      Workshop,
      Social
   }

Add an Enum Property to a Model Class
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Other objects can have enum type properties. To add an ``EventType`` property to our model ``Event``,
we create a ``Type`` property in ``Event`` amongst the other properties declared:

.. sourcecode:: csharp
   :lineno-start: 12

   // other Event property declarations

   public EventType Type { get; set; }

   // Event methods

Once we have added an ``EventType`` property to our model, we need to add an ``EventType`` property to our ViewModel.

Add an Enum Property to a ViewModel
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The first thing we need to do is add an ``EventType`` property to ``AddEventViewModel``.

.. sourcecode:: csharp
   :lineno-start: 20

   // other AddEventViewModel property declarations

   public EventType Type { get; set; }

Now that we have a property to hold the event type that the user selects, we need to create a list of all of the possible event types.
We will use this list to populate the ``select`` element in a later step.

.. sourcecode:: csharp
   :lineno-start: 24

   public List<SelectListItem> EventTypes { get; set; } = new List<SelectListItem>
   {
      new SelectListItem(EventType.Conference.ToString(), ((int)EventType.Conference).ToString()),
      new SelectListItem(EventType.Meetup.ToString(), ((int)EventType.Meetup).ToString()),
      new SelectListItem(EventType.Social.ToString(), ((int)EventType.Social).ToString()),
      new SelectListItem(EventType.Workshop.ToString(), ((int)EventType.Workshop).ToString())
   };

Because the ``EventType`` options are not changing, we can populate this property with a default value.
We add each of the constants to the ``EventTypes`` list. ``SelectListItem`` is an ASP.NET-provided class that represents each ``<option>`` 
element in a ``<select>`` element. The ``SelectListItem`` constructor requires a ``Text`` and ``Value`` property assignment.
The ``Text`` property sets the displayed text in the ``<option>`` tag. This is created by getting each ``EventType`` and casting it to a ``string`` type.
The ``Value`` property sets the ``value`` attribute on the ``<option>`` tag. This is created by getting each ``EventType``, casting it to 
its implicit ``int`` value, and then casting that to a ``string`` type.

This list only exists in ``AddEventViewModel`` because we need it only for the purposes of displaying all of the options.
We do not need a list of the different event types in our ``Event`` model.
We just need the type of one event. 
This is another great reason to use a ViewModel! 

Pass Enum Values Through the Controller
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

In ``EventsController``, the ``Add()`` action method that responds to ``POST`` requests uses model binding to create an ``AddEventViewModel`` object. 
So like any other field on the model, the controller does not necessarily need to know about the addition of ``AddEventViewModel.Type`` in order 
to create an ``AddEventViewModel`` instance from a form. However, we need to make sure that we are properly setting the ``Type`` property of 
our ``Event`` object using the value from the ``Type`` property of our ``AddEventViewModel`` object.

In ``EventsController``:

.. sourcecode:: csharp
   :lineno-start: 37

   Event newEvent = new Event
   {
      Name = addEventViewModel.Name,
      Description = addEventViewModel.Description,
      ContactEmail = addEventViewModel.ContactEmail,
      Type = addEventViewModel.Type
   };

Use Enum Value in a ``select`` Element
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The list of constants returned from ``EventType`` lends itself well to a ``select``-type form 
input. We'll update our form so that a user will have the option to choose one of the provided 
event types from a dropdown menu.

In ``Events/Add.cshtml``:

.. sourcecode:: guess
   :lineno-start: 20

   <div class="form-group">
      <label asp-for="Type">Event Type</label>
      <select asp-for="Type" asp-items="Model.EventTypes"></select>
   </div>

As with the other form inputs on the page, the ``asp-for`` attribute determines the ``name``
and ``id`` attributes for the ``select`` tag.
We also use ``asp-items`` to access all of the items stored in the list of our different enum values.

View the Event Type in the Events Table
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Once an event is created, to display its ``Type`` property in the table of all events, we'll modify 
``Events/Index.cshtml`` to include another column:

.. sourcecode:: html
   :lineno-start: 20

   <table class="table">
      <tr>
         <th>
            Id
         </th>
         <th>
            Name
         </th>
         <th>
            Description
         </th>
         <th>
            Contact Email
         </th>
         <th>
            Event Type
         </th>
      </tr>
      @foreach (var evt in Model)
      {
         <tr>
            <td>@evt.Id</td>
            <td>@evt.Name</td>
            <td>@evt.Description</td>
            <td>@evt.ContactEmail</td>
            <td>@evt.Type</td>
         </tr>
      }
   </table>
