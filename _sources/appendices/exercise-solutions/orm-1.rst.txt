.. _orm1-ex-1:

Exercise Solutions: OMG the ORM!
================================

Line numbers are for reference. They may not match your code exactly.

The ``EventCategory`` Class
---------------------------

``EventCategory`` needs to have the following:
   #. An ``Id`` property of type ``int``.
   #. A ``Name`` property of type ``string``.
   #. A no arg constructor.
   #. A constructor that sets the value of ``Name``.

``EventCategory`` represents data that will be stored in our database.

.. sourcecode:: csharp
   :linenos:

      public class EventCategory
      {
         public string Name { get; set; }

         public int Id { get; set; }

         public EventCategory(string name)
         {
            Name = name;
         }

         public EventCategory()
         {
         }
      }


:ref:`Return to exercises<orm1-exercises>`

.. _orm1-ex-2:

Adding to ``DbContext``
-----------------------

Once you have created ``EventCategory``, you need to add to ``EventDbContext`` to set up a table in the database for storing categories

.. sourcecode:: csharp

   public DbSet<EventCategory> Categories { get; set; }

:ref:`Return to exercises<orm1-exercises>`

.. _orm1-ex-3:

The ``EventCategoryController`` Class
-------------------------------------

Create ``EventCategoryController`` in the ``Controllers`` directory. To get our action methods working, we also need a variable of type ``EventDbContext``.

``Index()`` needs to do the following:
   #. Responds to ``GET`` requests at ``EventCategory/Index`` and returns a view called ``Index.cshtml``.
   #. Pass the ``DbContext`` category values as a list into the view template as a model
   

.. sourcecode:: csharp
   :linenos:

      public class EventCategoryController : Controller
      {
         private EventDbContext context;

         public EventCategoryController(EventDbContext dbContext)
         {
            context = dbContext;
         }

         // GET: /<controller>/
         [HttpGet]
         public IActionResult Index()
         {
            ViewBag.title = "All Categories";
            List<EventCategory> categories = context.Categories.ToList();
            return View(categories);
         }
      }

:ref:`Return to exercises<orm1-exercises>`

.. _orm1-ex-4:

Adding a View
-------------

``Index.cshtml`` needs to have the following:
   #. Use the list passed in from the action method in the controller as a model to populate the view.
   #. An ``h1`` with an appropriate heading for the page.
   #. A table that will display all of the category names of the event categories stored in our database.

   .. sourcecode:: html
      :linenos:

         @model List<CodingEventsDemo.Models.EventCategory>

         <h1>All Event Categories</h1>

         <table>
            <tr>
            <th>Category Name</th>
            </tr>
            @foreach(EventCategory category in Model)
            {
               <tr>
                     <td>@category.Name</td>
               </tr>
            }
         </table>

:ref:`Return to exercises<orm1-exercises>`
