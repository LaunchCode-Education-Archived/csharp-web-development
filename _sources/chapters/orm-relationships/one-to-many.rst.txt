Creating a One-to-Many Relationship
===================================

The first relationship we implement will be between the ``Event`` and ``EventCategory`` classes. We will allow multiple events to be in the same category, but each event will only have one category. Thus, this will be a one-to-many relationship. In this case, we will set up both sides of the relationship, so a many-to-one relationship will result as well.

Setting Up the Relationship - Video
-----------------------------------

We are now ready to create a relationship between ``Event`` and ``EventCategory``.

.. admonition:: Note

   The starter code for this video is found at the `event-category branch <https://github.com/LaunchCodeEducation/CodingEventsDemo/tree/event-category>`_ of ``CodingEventsDemo``. The final code presented in this video is found on the `one-to-many branch <https://github.com/LaunchCodeEducation/CodingEventsDemo/tree/one-to-many>`_. As always, code along to the videos on your own ``CodingEvents`` project.

.. youtube::
   :video_id: 9V_7j6ARM00

Setting Up the Relationship - Text
----------------------------------

We want to relate ``Event`` objects to ``EventCategory`` objects, and vice versa. Currently, similar functionality is enabled via the ``EventType`` field of ``Event``. However, ``EventType`` is an enum, which means that new values can not be added without changing the code and re-compiling. Using the persistent ``EventCategory`` class to organize events will be a much more flexible and user-friendly approach. 

Replacing ``EventType`` With ``EventCategory``
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

In the ``Event`` class, replace the ``Type`` property with a new property of type ``EventCategory``. In order for EntityFrameworkCore to be able to persist relationships between ``Event`` objects and ``EventCategory`` objects, we must also have a property that stores the ``Id`` of the given ``EventCategory``.

.. sourcecode:: csharp
   :lineno-start: 14

   public EventCategory Category { get; set; }

   public int CategoryId { get; set; }

The ``CategoryId`` property functions as a `foreign key <https://education.launchcode.org/SQL/chapters/mysql-part-2/relationships.html#adding-a-foreign-key>`_. EF will create a ``CategoryId`` column in the ``Event`` table. The value of this column for a given row will determine which row in the ``Category`` table is related to the given event. Our code is now set up so that each ``Event`` will knows about its ``EventCategory`` object, and that relationship persists.

.. admonition:: Note

   It is *very* important that the ID field corresponding to the ``Category`` property be named ``CategoryId``. This naming convention lets EF know that it should set ``Category`` to be the object with ``Id`` value the same as ``CategoryId``. 

Now, let's remove all references to ``EventType`` in the project.

Open ``AddEventViewModel``, which is in the ``ViewModels`` directory. Recall that this ViewModel represents the data that is needed to display and process the form used to create new ``Event`` instances. Replace its ``Type`` and ``EventType`` properties with similar properties that use ``EventCategory``.

.. sourcecode:: csharp
   :lineno-start: 22

   [Required(ErrorMessage = "Category is required")]
   public int CategoryID { get; set; }

   public List<SelectListItem> Categories { get; set; }

The constructor for this class populates the ``EventTypes`` collection, which we have just removed. This collection stored a collection of ``SelectListItem`` objects, one for each possible value of ``Type``. The corresponding code to work with categories should populate ``Categories`` with each possible value of ``Category``. In other words, ``Categories`` should have one ``SelectListItem`` for each item in the ``EventCategory`` table. 

We'll rely on the controller to provide our constructor with a list of all ``EventCategory`` objects, so we can update the constructor to look like this:

.. sourcecode:: csharp
   :lineno-start: 28

   public AddEventViewModel(List<EventCategory> categories)
   {
      Categories = new List<SelectListItem>();

      foreach (var category in categories)
      {
            Categories.Add(new SelectListItem
            {
               Value = category.Id.ToString(),
               Text = category.Name
            });
      }
   }

The ``Value`` of each ``SelectListItem`` will be the ``Id`` of the given category. The ``Id`` of a category is unique (in fact, it functions as a primary key) while the ``Name`` may not be. Therefore, we must use ``Id`` for the ``value`` attribute.

Since we no longer have a no-arg constructor, we must add one to allow model binding.

.. sourcecode:: csharp
   :lineno-start: 42

   public AddEventViewModel()
   {
   }

There is another reference to ``EventType``, and it is in ``Views/Events/Add.cshtml``. Within that file, update the ``select`` input and its label to reference our new ``Category`` and ``Categories`` properties.

.. sourcecode:: html
   :lineno-start: 21

   <label asp-for="CategoryId">Category</label>
   <select asp-for="CategoryId" asp-items="Model.Categories"></select>

Finally, we have a reference to ``EventType`` in the ``EventsController.Add`` method that handles POST requests. This method creates a new ``Event`` object using data from the ``AddEventViewModel`` parameter.

.. sourcecode:: csharp
   :lineno-start: 46

   Event newEvent = new Event
   {
      Name = addEventViewModel.Name,
      Description = addEventViewModel.Description,
      ContactEmail = addEventViewModel.ContactEmail,
      Type = addEventViewModel.Type
   };

When this method runs, ``addEventViewModel`` contains form data. The data that specifies which ``EventCategory`` and ``Event`` should be assigned to is ``CatgoryId`` and NOT and actually ``EventCategory`` object. Therefore, we must first retrieve the category object, and then pass it into the ``Event`` constructor.

The code above can be refactored as follows:

.. sourcecode:: csharp
   :lineno-start: 46

   EventCategory category = context.Categories.Find(addEventViewModel.CategoryId);
   Event newEvent = new Event
   {
      Name = addEventViewModel.Name,
      Description = addEventViewModel.Description,
      ContactEmail = addEventViewModel.ContactEmail,
      Category = category
   };

Our app is now free of all references to ``EventType``, so we may delete this unused class. 

Defining the Inverse Relationship
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

For categories to be aware of the events that they relate to, we must add an ``Event`` collection property to ``EventCategory``.

In ``EventCategory``:

.. sourcecode:: csharp
   :lineno-start: 12

   public List<Event> Events { get; set; }

.. admonition:: Note

   The new property on ``Event`` is a single ``EventCategory`` reference, while the new property on ``EventCategory`` is a *collection* of ``Event`` objects. This is due to the one-to-many nature of the relationship. Each ``Event`` can have only one ``EventCategory``, but an ``EventCategory`` may be related to multiple ``Event`` objects.

Refactoring the Controller and View - Video
-------------------------------------------

.. admonition:: Note

   The starter code for this video is found at the `one-to-many branch <https://github.com/LaunchCodeEducation/CodingEventsDemo/tree/one-to-many>`_ of ``CodingEventsDemo``. The final code presented in this video is found on the `refactoring-controller branch <https://github.com/LaunchCodeEducation/CodingEventsDemo/tree/refactoring-controller>`_. As always, code along to the videos on your own ``CodingEvents`` project.

.. youtube::
   :video_id: xj2EZl37Ooo

Refactoring the Controller and View - Text
------------------------------------------

Our ``EventsController`` requires a few updates now that ``Event`` objects reference ``EventCategory`` objects.

The ``Index`` method passes the collection of all ``Event`` objects into the view for display:

.. sourcecode:: csharp
   :lineno-start: 28

   List<Event> events = context.Events.ToList();

.. index:: ! lazy loading, ! eager loading

When we reference ``context.Events``, all ``Event`` objects will be queried from the database. By default, EF uses **lazy loading** to retrieve objects. Lazy loading results in *only* the data in the ``Event`` table being returned in the result set. Any data stored in other tables, such as data belonging to a referenced object, will NOT be loaded. In our case, this means that ``Event`` objects in ``context.Events`` will NOT have their ``Category`` properties set by EF. As-is, our code would display an empty category column in the main view.

.. admonition:: Note

   While lazy loading is not what we want now, it can be a useful strategy in a lot of cases. Suppose your application wants to display a list of all users, where each ``User`` has a ``UserDetails`` property that stores info like profile image, email, etc. 

   If all we need is a list of users, loading all of the additional data in ``UserProfile`` is unnecessary and will slow down the application. Lazy loading minimizes the data returned to optimize performance and reduce queries. 

The solution is to use **eager loading**. Eager loading is a technique that allows us to specify that data from other tables/objects be loaded when the querying a specific table/object. In our case, we want our ``Event`` objects to be returned with their corresponding ``EventCategory`` objects. We can tell EF to load the categories eagerly with the following code:

.. index:: lambda expression

.. sourcecode:: csharp
   :lineno-start: 28

   List<Event> events = context.Events.Include(e => e.Category).ToList();

The ``Include`` method takes a lambda expression which specifies the property of each ``Event`` object that should be included in the query results. The effect of this additional method is that a ``JOIN`` query is performed between the ``Event`` and ``EventCategory`` tables, with ``Event.CategoryId`` being joined on ``EventCategory.Id``.

Our next update is more straightforward. Recall that we modified the main controller in ``AddEventViewModel`` to take a list of all ``EventCategory`` objects. This constructor is called in the ``Add`` method of our controller. Let's update it to pass in a list of all ``EventCategory`` objects, as queried from the database.

.. sourcecode:: csharp
   :lineno-start: 35

   AddEventViewModel addEventViewModel = new AddEventViewModel(context.Categories.ToList());

Database Migration and Testing - Video
--------------------------------------

We are done updating our code for now, but before we can test we must update the database. Recall that we changed the structure of the model by relating ``Event`` and ``EventCategory`` classes, and by removing ``EventType``. Any model change requires a database update.

.. admonition:: Note

   The starter code for this video is found at the `refactoring-contoller branch <https://github.com/LaunchCodeEducation/CodingEventsDemo/tree/refactoring-contoller>`_ of ``CodingEventsDemo``. The final code presented in this video is found on the `migration-testing branch <https://github.com/LaunchCodeEducation/CodingEventsDemo/tree/migration-testing>`_. As always, code along to the videos on your own ``CodingEvents`` project.

.. youtube::
   :video_id: Ihjgp8oG3Wg

.. _create-migration:

Database Migration and Testing - Text
--------------------------------------

Open a terminal and navigate to the ``CodingEvents`` project directory within the solution. Then run ``dotnet ef migrations add RelateEventsAndCategories`` to create a new migration.

To apply the migration, run ``dotnet ef database update``.

If you look at the database, you'll see that the ``Event`` table no longer has a ``Type`` column. In addition, it now has a ``CategoryId`` column that is a foreign key to ``EventCategory.Id``.

Now, start up the app and test!

Check Your Understanding
------------------------

.. admonition:: Question

   You are working on an ASP.NET application tracking elected officials. Your model class, ``Senator`` has a many-to-one relationship with another model class, ``State``. To properly configure this relationship in the EF context, what must be present?

   #. In ``Senator``, a ``State`` property and a ``StateId`` property
   #. In ``Senator``, only a ``State`` property
   #. In ``State``, a ``Senator`` property and a ``SenatorId`` property
   #. In ``State``, only a ``Senator`` property

.. ans: a. In ``Senator``, a ``State`` property and a ``StateId`` property

.. admonition:: Question

   What is the default technique for loading child objects of persistent objects? 

   #. Eager loading
   #. Lazy loading
   #. Explicit loading
   #. There is no default, the technique must always be explicitly specified

.. ans: b. Lazy loading