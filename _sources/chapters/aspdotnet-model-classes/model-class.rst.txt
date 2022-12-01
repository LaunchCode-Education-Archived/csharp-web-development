Create a Model
==============

In this book section, we will continue to make incremental changes to ``CodingEvents``. The next set of 
changes show model creation, how models relate to data, and the practice of model binding. First, we 
replace the dictionary in ``EventsController`` with a list of ``Event`` models. We’ll then update our 
action methods to take advantage of the new model and its properties. Lastly, we refactor the view template 
to reflect the changes in the controller.

Create a Model Class - Video
----------------------------

.. youtube::
   :video_id: fs7m2Qo84d4

.. admonition:: Note

   The starter code for this video is found at the `models1-start branch <https://github.com/LaunchCodeEducation/CodingEventsDemo/tree/models1-start>`__
   of ``CodingEventsDemo``. The final code presented in this 
   video is found on the `create-model branch <https://github.com/LaunchCodeEducation/CodingEventsDemo/tree/create-model>`__.
   As always, code along to the videos on your own ``CodingEvents`` project.

Create a Model Class - Text
---------------------------

.. index:: ! POCO

Like controllers, model classes are conventionally located in a ``Models``
folder. Model classes resemble the kinds of classes we practiced making at 
the start of this course. In other words, models are **plain old C# objects**, or **POCOs**.

To create a model, we’ll transform the information that we once stored in an ``Events`` dictionary into a class.
This new ``Event`` class will include a property for ``Name``, a constructor, and a ``ToString()`` override.

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


We now need to update the ``POST`` handler that creates new events. 

First, replace the ``Events`` dictionary with a list of ``Event`` objects.

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


Back in ``Events/Index.cshtml``, update the HTML to use the ``Event`` object’s fields, rather than strings.

.. sourcecode:: guess
   :lineno-start: 22

   @foreach (var evt in ViewBag.events)
   {
      <tr>
         <td>@evt.Name</td>
      </tr>
   }

.. admonition:: Tip

   Here's a shorthand to create auto-implementing properties. In a class, type the word “prop” followed 
   by hitting the Tab key twice. This swiftly supplies the property’s scaffolding:

   .. sourcecode:: c#

      public object MyProperty { get; set; }


Add a Model Property - Video
----------------------------

.. youtube::
   :video_id: ajHm5DQFaYU

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
         public string Description { get; set; }

         public Event(string name, string description)
         {
            Name = name;
            Description = description;
         }

         public override string ToString()
         {
            return Name;
         }
      }
   }

Now that our data is object-oriented, it’s quick and easy to add a new property affiliated with an event. 
If we decide to add properties, such as ``Date`` or ``Location``, we can follow the pattern established. 
Think about when we stored events as key-value pairs. At that stage, more significant changes were necessary 
to add fields.

In the ``Views`` folder, the ``Events/Add.cshtml`` template still uses a ``desc`` field so we don't need to update
this view. We do, however, need to go into ``Events/Index.cshtml`` to add the table data for an event's description.

``Events/Index.cshtml``:

.. sourcecode:: guess
   :lineno-start: 26

   <td>@evt.Description</td>

Lastly, add a parameter to the ``NewEvent`` action method. This parameter passes the description value into 
the creation of the ``Event`` object.

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

.. ans: True, models are just C# objects


.. admonition:: Question

   Say we do add a ``Date`` property to the ``Event`` class. Which line would we add to ``Events/Index.cshtml`` 
   to also display that value in our table of events?

   #. ``<li>@evt.Date</li>``
   #. ``<td>evt.Date</td>``
   #. ``<td>@event.Date</td>``
   #. ``<td>@evt.date</td>``

.. ans: a, ``<td>@evt.Date</td>``



