Create a Model
==============

In the next several pages, we will be making updates to ``CodingEvents`` to demonstrate model creation,
how models relate to data, and the practice of model binding. The first of these steps is to move data 
handling out of our controller classes and into a model class. As we discussed on the previous page, the 
controller class is not responsible for holding data.

In ``CodingEvents``, we'll remove the list data from ``EventsController`` and create a proper 
C# class to deal with event items. We'll then update our action methods to take
advantage of the new model and its properties, rather than the strings stored in the list.
Lastly, because the controller is updating, the template variables it relies upon will also need to
change to reflect the model properties.

Create a Model Class - Video
----------------------------

.. TODO: Add create model class video

.. topics covered: Create Event class - including name property only
.. Refactor post handler to create Event object + add to list of events
.. Refactor events/index template to reference Event field for name

YOUTUBE VIDEO HERE

.. admonition:: Note

   The starter code for this video is found at the `models1-start branch <https://github.com/LaunchCodeEducation/CodingEventsDemo/tree/models1-start>`__
   of ``CodingEventsDemo``. The final code presented in this 
   video is found on the `create-model branch <https://github.com/LaunchCodeEducation/CodingEventsDemo/tree/create-model>`__.
   As always, code along to the videos on your own ``CodingEvents`` project.

Create a Model Class - Text
---------------------------

.. index:: ! POCO

Like controllers, model classes are conventionally located in a ``Models``
folder. Structurally, model classes most closely resemble the kinds of classes we practiced
making at the start of this course in console apps, before introducing ASP.NET. In other words,
models are **plain old C# objects**, or **POCOs**.

To create a model to shape event data, we'll transform the information that we once stored in the ``Events``
dictionary in ``EventsController`` into a class. This new ``Event`` class will include a property for ``Name``, 
a constructor, and a ``ToString()`` override.

In ``Models/Event.cs``:

.. sourcecode:: c#
   :linenos: 

   namespace CodingEventsDemo.Models
   {
      public class Event
      {
         public string Name { get; set; }

         public Event(string name)
         {
            Name = name;
         }

         public override string ToString()
         {
            return Name;
         }
      }
   }


Now that we're working to move the data handling out from the controller classes and into a class of its own, 
we'll need to update the ``POST`` handler that creates new events. 

First, remove replace the ``Events`` dictionary with a list of ``Event`` objects.

.. sourcecode:: c#
   :lineno-start: 15

   static private List<Event> Events = new List<Event>();

Update the ``Add()`` method inside of 
``NewEvent()`` to add a new ``Event`` instance to the list:

.. sourcecode:: c#
   :lineno-start: 30

   [HttpPost]
   [Route("Events/Add")]
   public IActionResult NewEvent(string name)
   {
      Events.Add(new Event(name));

      return Redirect("/Events");
   }


Back in the ``Events/Index.cshtml`` view template, update the HTML to use the ``Event`` object's fields, rather 
than simply strings.

.. sourcecode:: guess
   :lineno-start: 22

   @foreach (var evt in ViewBag.events)
   {
      <tr>
         <td>@evt.Name</td>
      </tr>
   }

.. admonition:: Tip

   For a shorthand to create auto-implementing properties in a class, you can type the word "prop" followed by 
   hitting the *Tab* key twice to swiftly supply the property's scaffolding:

   .. sourcecode:: c#

      public object MyProperty { get; set; }

.. TODO: check this on windows ^^


Add a Model Property - Video
----------------------------

.. TODO: Add adding model property video

.. topics covered: add description property to event model, update index view and post handler 
.. to display the property and use it to create the object

YOUTUBE VIDEO HERE

.. admonition:: Note

   The starter code for this video is found at the `create-model branch <https://github.com/LaunchCodeEducation/CodingEventsDemo/tree/create-model>`__
   of ``CodingEventsDemo``. The final code presented in this 
   video is found on the `add-property branch <https://github.com/LaunchCodeEducation/CodingEventsDemo/tree/add-property>`__.

Add a Model Property - Text
---------------------------

To round out the ``Event`` class, we'll add a ``Description`` property to showcase what our events are all about.

Updates to ``Models/Event.cs``:

.. sourcecode:: c#
   :linenos:

   namespace CodingEventsDemo.Models
   {
      public class Event
      {
         public string Name { get; set; }

         public Event(string name)
         {
            Name = name;
         }

         public override string ToString()
         {
            return Name;
         }
      }
   }

Now that our data is object-oriented, it's quick and easy to add a new property affiliated with an event. If after 
this, we decide to add properties, such as ``Date`` or ``Location``, we can simply follow the pattern established. 
Before, with events stored as key-value pairs in a dictionary, we would have had more changes to make in order 
to add other information fields to the shape of the data.

In the ``Views`` folder, the ``Events/Add.cshtml`` template still uses a ``desc`` field so we don't need to update
this view. We do, however, need to do into ``Events/Index.cshtml`` to add the table data for an event's description.

``Events/Index.cshtml``:

.. sourcecode:: guess
   :lineno-start: 26

   <td>@evt.Description</td>

Lastly, add a parameter to the 
``NewEvent`` action method to handle the form submission and pass the description
value into the creation of the ``Event`` object.

``EventController``:

.. sourcecode:: c#
   :lineno-start: 30

   [HttpPost]
   [Route("Events/Add")]
   public IActionResult NewEvent(string name, string desc)
   {
      Events.Add(new Event(name, desc));

      return Redirect("/Events");
   }


Check Your Understanding
-------------------------

.. admonition:: Question

   True/False: Model code is framework independent.

   #. True
   #. False

.. ans: true, models are just C# objects


.. admonition:: Question

   If we do add a ``Date`` property to the ``Event`` class, which line would we add to ``Events/Index.cshtml``
   to also display that value in our table of events?

   #. ``<li>@evt.Date</li>``
   #. ``<td>evt.Date</td>``
   #. ``<td>@event.Date</td>``
   #. ``<td>@evt.date</td>``

.. ans: c, ``<td>@event.Date</td>``



