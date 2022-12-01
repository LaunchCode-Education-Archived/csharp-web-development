Creating a Many-to-Many Relationship
====================================

Let's set up a many-to-many relationship between ``Event`` and ``Tag``.

Join Tables
-----------

To relate data in a many-to-many fashion in a relational database requires a new type of SQL table.

One-to-many relationships are established at the database level by the use of a foreign key column on one side of the relationship. Our ``Events`` table has a foreign key column: ``CategoryId``. 

For each ``Events`` row, the column ``CategoryId`` contains the ``Id`` of a ``Categories`` row. This is the primary key of the row in ``Categories`` that the ``Events`` row is related to. The ``Event``/``EventCategory`` relationship is many-to-one, so *many* event rows may have the same ``CategoryId`` value. 

.. index:: ! join table

Using foreign and primary keys to create many-to-many relationships is a bit trickier. In order to relate rows in ``Events`` to rows in ``Tag``, we need need a third table, known as a **join table**. A join table consists of two columns, each of which is a foreign key column to another table. Each row in a join table represents a relationship between one row in each of the two tables being joined. This technique enables many-to-many relationships.

Consider some example data in our ``Events`` and ``Tags`` tables.

.. list-table:: Sample ``Events`` data
   :header-rows: 1

   * - Id
     - Name
     - CategoryId
   * - 13
     - WWDC
     - 2
   * - 15
     - SpringOne Platform
     - 2
   * - 17
     - Java meetup
     - 3
   
.. list-table:: Sample ``Categories`` data
   :header-rows: 1

   * - Id
     - Name
   * - 2
     - Conference
   * - 3
     - Meetup

.. list-table:: Sample ``Tags`` data
   :header-rows: 1

   * - Id
     - Name
   * - 4
     - ios
   * - 5
     - spring
   * - 6
     - java

A join table for these two tables would be called ``EventTags``, and would have two columns, ``EventId`` and ``TagId``. Each of these columns are foreign key columns into their respective tables. 

If we want to relate the ``ios`` tag to the ``WWDC`` event, we create a new row in ``EventTags``:

.. list-table:: A join table with a single relationship
   :header-rows: 1

   * - EventId
     - TagId
   * - 13
     - 4

We can do this again and again to generate more relationships. Let's revisit the many-to-many diagram from earlier in the chapter. 

.. figure:: figures/many-to-many.png
   :alt: Three Event objects on the left, with various relationships to three Tag objects on the right
   :width: 800px

   A many-to-many relationship between Event and Tag objects

The join table representing these relationships looks like this:

.. list-table:: The full join table representing the relationships in the figure above
   :header-rows: 1

   * - EventId
     - TagId
   * - 13
     - 4
   * - 15
     - 5
   * - 15
     - 6
   * - 17
     - 6

.. index:: ! composite primary key

Notice that join table doesn't have an explicit primary key column. Values in both ``EventId`` and ``TagId`` may be duplicated in each column. Indeed, this is the exact property of a join table that allows many-to-many relationships. A join table makes use of a new type of primary key, called a **composite primary key**. A composite primary key is a combination of columns that is unique and functions as a primary key. So, for example, the primary key of the first row of the example just above is the pair (13, 4). This combination is unique, because the objects with the two IDs can be related to each other in only one way. 

In order to enable many-to-many relationships with EF, we need a class to model a join table.

The ``EventTag`` Model - Video
------------------------------

Let's create a new model class, ``EventTag``, to model a join table for ``Event`` and ``Tag`` classes. 

.. admonition:: Note

   The starter code for this video is found at the `event-detail-view branch <https://github.com/LaunchCodeEducation/CodingEventsDemo/tree/event-detail-view>`_ of ``CodingEventsDemo``. The final code presented in this video is found on the `event-tag-model branch <https://github.com/LaunchCodeEducation/CodingEventsDemo/tree/event-tag-model>`_. As always, code along to the videos on your own ``CodingEvents`` project.

.. youtube::
   :video_id: xZLFVV9SHiM

The ``EventTag`` Model - Text
-----------------------------

.. index:: ! join class

To model a join table for ``Event`` and ``Tag`` classes, we will create a **join class**. Given our discussion of join tables above, we know that it will need ``EventId`` and ``TagId`` properties. To more easily work with the corresponding ``Event`` and ``Tag`` objects in our controllers, we will also include properties of those specific types.

.. sourcecode:: csharp
   :linenos:

   using System;
   namespace CodingEventsDemo.Models
   {
      public class EventTag
      {

         public int EventId { get; set; }
         public Event Event { get; set; }

         public int TagId { get; set; }
         public Tag Tag { get; set; }

         public EventTag()
         {
         }
      }
   }

To make this class persistent, and a new ``DbSet`` entry to ``EventDbContext``:

.. sourcecode:: csharp
   :lineno-start: 11

   public DbSet<EventTag> EventTags { get; set; }

.. index:: composite primary key

Since our join table will make use of a composite primary key, we need to add some additional configuration to ``EventDbContext``.

.. sourcecode:: csharp
   :lineno-start: 18

   protected override void OnModelCreating(ModelBuilder modelBuilder)
   {
      modelBuilder.Entity<EventTag>()
            .HasKey(et => new { et.EventId, et.TagId });
   }

The method ``OnModelCreating`` can be overridden from the base class, ``DbContext``, in order to provide additional configuration for the data store. In this case, we add code that configures ``EntityTag`` to have a composite primary key consisting of the properties/columns ``EventId`` and ``TagId``.

This completes configuration of our join class. Before proceeding, create and apply a database migration. Refer to the :ref:`previous section <create-migration>` for details if needed, being sure to use a unique, descriptive migration name. After running the migration, verify that there is a new join table, ``EventTag``.

Adding a ``Tag`` to an ``Event`` - Video
----------------------------------------

Now that we have established a many-to-many relationship between ``Event`` and ``Tag``, we can write controller and view code to allow users to add tags to events.

.. admonition:: Note

   The starter code for this video is found at the `event-tag-model branch <https://github.com/LaunchCodeEducation/CodingEventsDemo/tree/event-tag-model>`_ of ``CodingEventsDemo``. The final code presented in this video is found on the `add-tag-to-event branch <https://github.com/LaunchCodeEducation/CodingEventsDemo/tree/add-tag-to-event>`_. As always, code along to the videos on your own ``CodingEvents`` project.

.. youtube::
   :video_id: KwAqPy2nDsU

Adding a ``Tag`` to an ``Event`` - Text
---------------------------------------

For a user to be able to add a tag to an event, they will need a view in which to do so. Our approach will be to create a view at the path ``/Tag/AddEvent/X``, where ``X`` is a path parameter containing the ID of the event we want to add a tag to.

This new view will contain a form with a dropdown that will allow the user to select the tag to add to the event with ID ``X``. To model this form data, we need a new ViewModel.

``ViewModels/AddEventTagViewModel``
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. sourcecode:: csharp
   :linenos:

   using System;
   using System.Collections.Generic;
   using System.ComponentModel.DataAnnotations;
   using CodingEventsDemo.Models;
   using Microsoft.AspNetCore.Mvc.Rendering;

   namespace CodingEventsDemo.ViewModels
   {
      public class AddEventTagViewModel
      {
         [Required(ErrorMessage = "Event is required")]
         public int EventId { get; set; }

         [Required(ErrorMessage = "Tag is required")]
         public int TagId { get; set; }

         public Event Event { get; set; }

         public List<SelectListItem> Tags { get; set; }

         public AddEventTagViewModel(Event theEvent, List<Tag> possibleTags)
         {
               Tags = new List<SelectListItem>();

               foreach (var tag in possibleTags)
               {
                  Tags.Add(new SelectListItem
                  {
                     Value = tag.Id.ToString(),
                     Text = tag.Name
                  });
               }

               Event = theEvent;
         }

         public AddEventTagViewModel()
         {            
         }
      }
   }

This class models the data that is need to render and process our form. In order to add a tag to an event, our ``POST`` handler will need to know the IDs of the two objects in question. Therefore, our ViewModel has required ``EventId`` and ``TagId`` properties. It also contains an ``Event`` property, which we will use to display details (such as the event name) in the view.

Finally, the ViewModel has a property ``List<SelectListItem> Tags``. As with previous forms containing a dropdown, this property will be used to populate the ``select`` element containing the all of the tag options. 

The constructor requires an ``Event`` object as well as a ``List<Tag>`` object. The list will contain a collection of all tags pulled from the database when we call the constructor from within our controller.

Now, let's create the view template.

``Views/Tag/AddEvent.cshtml``
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Our template needs a form with two inputs. The more obvious input will be the ``select`` element containing tag options. Since we also need to submit the event ID in our request, we'll add a hidden input that holds the value of ``EventId`` from our ViewModel.

.. sourcecode:: html
   :linenos:

   @model CodingEventsDemo.ViewModels.AddEventTagViewModel

   <h1>Add Tag to Event: @Model.Event.Name</h1>

   <form asp-controller="Tag" asp-action="AddEvent" method="post">
      <input type="hidden" value="@Model.Event.Id" name="EventId" />
      <div class="form-group">
         <label asp-for="TagId">Tag</label>
         <select asp-for="TagId" asp-items="Model.Tags"></select>
         <span asp-validation-for="TagId"></span>
      </div>
      <input type="submit" value="Add Tag" />
   </form>

``GET`` and ``POST`` Handlers
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

We're now ready to add handler methods to ``TagController``.

The ``GET`` method is simple since it just displays the form.

.. sourcecode:: csharp
   :lineno-start: 50

   // responds to URLs like /Tag/AddEvent/5 (where 5 is an event ID)
   public IActionResult AddEvent(int id)
   {
      Event theEvent = context.Events.Find(id);
      List<Tag> possibleTags = context.Tags.ToList();
      AddEventTagViewModel viewModel = new AddEventTagViewModel(theEvent, possibleTags);
      return View(viewModel);
   }

This method creates an ``AddEventTagViewModel`` using the event specified by the ``id`` parameter and the list of all tags from the database. Then it renders the view.

The ``POST`` method is more complicated.

.. sourcecode:: csharp
   :lineno-start: 59

   [HttpPost]
   public IActionResult AddEvent(AddEventTagViewModel viewModel)
   {
      if (ModelState.IsValid)
      {

         int eventId = viewModel.EventId;
         int tagId = viewModel.TagId;

         EventTag eventTag = new EventTag {
            EventId = eventId,
            TagId = tagId
         };
         context.EventTags.Add(eventTag);
         context.SaveChanges();

         return Redirect("/Events/Detail/" + eventId);
      }

      return View(viewModel);
   }

This action method takes in a ``AddEventTagViewModel`` object which will be created via model binding. Assuming validation passes (that is, both ``EventId`` and ``TagId`` are not ``null``) we create a new ``EventTag`` object and save it to the database. Then we redirect to the detail view for the given event.

With this code, we can now add a tag to an event. Start up the application and test it out. In order to verify that everything worked, you'll need to look at the ``EventTag`` table in the database to verify a new row is created upon form submission. 

In the next section, we'll work to display tags in the view.

Displaying Tags in the Detail View - Video
------------------------------------------

Now that we have ``EventTag`` data in the database, let's display the tags for a given event in the view.

.. admonition:: Note

   The starter code for this video is found at the `add-tag-to-event branch <https://github.com/LaunchCodeEducation/CodingEventsDemo/tree/add-tag-to-event>`_ of ``CodingEventsDemo``. The final code presented in this video is found on the `display-tags branch <https://github.com/LaunchCodeEducation/CodingEventsDemo/tree/display-tags>`_. As always, code along to the videos on your own ``CodingEvents`` project

.. youtube::
   :video_id: WqhXqnXqnyk

Displaying Tags in the Detail View - Text
-----------------------------------------

We want an event's tags to be displayed on its detail view, so let's start in ``EventsController``. The ``Detail`` method needs to pass in tag data for the given event. To do this, we must query ``context.EventTags`` and pass the resulting list of ``EventTag`` objects into the ViewModel's constructor.

.. sourcecode:: csharp
   :lineno-start: 92

   List<EventTag> eventTags = context.EventTags
         .Where(et => et.EventId == id)
         .Include(et => et.Tag)
         .ToList();

   EventDetailViewModel viewModel = new EventDetailViewModel(theEvent, eventTags);

Our query of ``context.EventTags`` has a few pieces:

#. **Line 93** - Filters the ``EventTags`` set to include only objects related to the given ``Event``.
#. **Line 94** - Forces eager loading of the ``Tag`` property of those ``EventTag`` objects.
#. **Line 95** - Converts the ``DbSet`` to a list.

.. admonition:: Note

   You might be wondering why we have to query ``context.EventTags``. Indeed, it would be convenient of we could just reference a ``Tags`` property from the ``Event`` class. But notice that there *is no such property* in ``Event``. The many-to-many relationship is defined by the data in ``EventTag``, so we must use this class in order to access related objects.

Now let's move into ``EventDetailsViewModel``. Here, we add data related to an event's tags to pass into the view.

First, add a new string property named ``TagText``.

.. sourcecode:: csharp
   :lineno-start: 14

   public string TagText { get; set; }

Then in the constructor, add a parameter to represent the list of all of ``EventTag`` objects associated with a given ``Event``. Use this parameter to set the value of ``TagText``.

.. sourcecode:: csharp
   :lineno-start: 16

   public EventDetailViewModel(Event theEvent, List<EventTag> eventTags)
   {
      EventId = theEvent.Id;
      Name = theEvent.Name;
      Description = theEvent.Description;
      ContactEmail = theEvent.ContactEmail;
      CategoryName = theEvent.Category.Name;

      TagText = "";
      for (var i = 0; i < eventTags.Count; i++)
      {
            TagText += ("#" + eventTags[i].Tag.Name);
            if (i < eventTags.Count - 1)
            {
               TagText += ", ";
            }
      }
   }

We build up the contents of ``TagText`` by looping over ``eventTags`` and appending tag names, separated by commas. For example, if an event has tags with names ``"java"``, ``"csharp"``, and ``"object-oriented"``, then the ``TagList`` will be ``"#java, #csharp, #object-oriented"``. 

Displaying this data in the view is straightforward. In ``Views/Events/Detail.cshtml``, add an additional row to the table.

.. sourcecode:: html
   :lineno-start: 18
   
   <tr>
      <th>Tags</th>
      <td>@Model.TagText</td>
   </tr>

Now, any tags associated with the given event will display nicely.

To make it easy for users to add a tag to an event, add the following link below the table.

.. sourcecode:: html
   :lineno-start: 25

   <a asp-controller="Tag" asp-action="AddEvent" asp-route-id="@Model.EventId">Add Tag</a>

This creates a URL of the form ``/Tag/AddEvent/X``, where ``X`` is the ID of the given event.

Preventing Errors When Adding a Tag - Video
-------------------------------------------

With the current state of our code, attempting to add a tag to an event that already has that tag results in an error. This is because the ``EventId``/``TagId`` combination is the primary key for our join table, and primary keys must be unique. 

Let's address this scenario.

.. admonition:: Note

   The starter code for this video is found at the `display-tags branch <https://github.com/LaunchCodeEducation/CodingEventsDemo/tree/display-tags>`_ of ``CodingEventsDemo``. The final code presented in this video is found on the `tag-errors branch <https://github.com/LaunchCodeEducation/CodingEventsDemo/tree/tag-errors>`_. As always, code along to the videos on your own ``CodingEvents`` project

.. youtube::
   :video_id: CWX3juBW4zk

Preventing Errors When Adding a Tag - Text
------------------------------------------

There are multiple ways to address this issue. The approach we take is to allow the user to submit a form with a potentially duplicate ``EventId``/``TagId`` combination and add a check in the ``POST`` handler.

Within ``Controller/TagController.cs`` update the ``AddEvent`` (``POST`` handler) code to look like this:

.. sourcecode:: csharp
   :lineno-start: 59

   [HttpPost]
   public IActionResult AddEvent(AddEventTagViewModel viewModel)
   {
      if (ModelState.IsValid)
      {

            int eventId = viewModel.EventId;
            int tagId = viewModel.TagId;

            List<EventTag> existingItems = context.EventTags
               .Where(et => et.EventId == eventId)
               .Where(et => et.TagId == tagId)
               .ToList();

            if (existingItems.Count == 0)
            {
               EventTag eventTag = new EventTag {
                  EventId = eventId,
                  TagId = tagId
               };
               context.EventTags.Add(eventTag);
               context.SaveChanges();
            }

            return Redirect("/Events/Detail/" + eventId);
      }

      return View(viewModel);
   }

Lines 68-71 query for existing ``EventTag`` objects that have the some ``EventId``/``TagId`` pair. In other words, ``existingItems`` will be empty unless that given event already has the given tag. Before creating and saving a new ``EventTag`` object, we check the size of ``existingItems``, skipping this step if the event already has the tag.

Display Items With a Given Tag - Video
--------------------------------------

In addition to seeing which tags are on an event, we would also like to see all events with a specific tag.

.. admonition:: Note

   The starter code for this video is found at the `tag-errors branch <https://github.com/LaunchCodeEducation/CodingEventsDemo/tree/tag-errors>`_ of ``CodingEventsDemo``. The final code presented in this video is found on the `display-tag-items branch <https://github.com/LaunchCodeEducation/CodingEventsDemo/tree/display-tag-items>`_. As always, code along to the videos on your own ``CodingEvents`` project

.. youtube::
   :video_id: Ajs-tg9nunA

Display Items With a Given Tag - Text
-------------------------------------

We start by creating a ``Detail`` action in ``Controllers/TagController.cs``. This action method should retrieve all ``EventTag`` objects with a given ``TagId``.

.. sourcecode:: csharp
   :lineno-start: 89

   public IActionResult Detail(int id)
   {
      List<EventTag> eventTags = context.EventTags
            .Where(et => et.TagId == id)
            .Include(et => et.Event)
            .Include(et => et.Tag)
            .ToList();

      return View(eventTags);
   }

Here's a breakdown of this query:

#. **Line 92** - Filters the collection of all ``EventTag`` objects down to just those with the given ``TagId``.
#. **Line 93** - Eager loads the ``Event`` child object.
#. **Line 94** - Eager loads the ``Tag`` child object.
#. **Line 95** - Converts the ``DbSet`` to a list.

This controller is accessible at the route ``/Tag/Detail/X`` where ``X`` is the ID of a specific tag.

The view is similar to other listings that we have created.

.. sourcecode:: html
   :linenos:

   @model List<CodingEventsDemo.Models.EventTag>

   @if (Model.Count == 0)
   {
      <h1>No elements with the given tag</h1>
   }
   else
   {
      <h1>Events Tagged: @Model[0].Tag.Name</h1>

      <ul>
         @foreach (var evtTag in Model)
         {
            <li>@evtTag.Event.Name</li>
         }
      </ul>

   }

Finally, we add links to the name of each tag in our tag index.

``Views/Tag/Index.cshtml``:

.. sourcecode:: html
   :lineno-start: 18

   <tr>
         <td>@tag.Id</td>
         <td><a asp-controller="Tag" asp-action="Detail" asp-route-id="@tag.Id">@tag.Name</a></td>
   </tr>

Start the app up and test user behavior. Viewing the main tag listing should allow you to click on each tag name and view the events that have that tag.

Check Your Understanding
------------------------

.. admonition:: Question

   The use of join tables enables (select all that apply):

   #. A database where you never need to run a ``JOIN`` query.
   #. Many-to-many relationships between tables.
   #. Many-to-many relationships between classes without creating a join class.
   #. Rainbows and butterflies to be stored in your database.

.. ans: B only.

.. admonition:: Question

   **True/False:** A join table does not have a primary key.

.. ans: False. It has a composite key

.. admonition:: Question

   Which ``EventDbContext`` property allows you to access ``Tag`` objects that are related to an ``Event`` object?

   #. ``DbSet<Event> Events``
   #. ``DbSet<Tag> Tags``
   #. ``DbSet<EventTag> EventTags``
   #. All of the above

.. ans: C. The join object must be used to determine m2m relationships