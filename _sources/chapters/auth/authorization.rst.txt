.. index:: ! [Authorize], ! [AllowAnonymous]

Identity and Authorization
==========================

.. admonition:: Note

   Try and code along as you read more about Identity!
   This page starts off with the code in the `identity-config <https://github.com/LaunchCodeEducation/CodingEventsDemo/tree/identity-config>`__ branch in ``CodingEventsDemo``.
   The final code for this page is in the `authorization <https://github.com/LaunchCodeEducation/CodingEventsDemo/tree/authorization>`__ branch in ``CodingEventsDemo``.

While this chapter is focused on authentication, you may find yourself wanting
to use Identity to limit pages to logged-in users. Authorization allows us to
restrict access to pages by allowing only logged in users to see them. While
this can be a very complex process, ``ASP.NET`` has two simple attributes that
allow us to restrict access to pages to only logged in users.

``[Authorize]`` is an attribute that limits access to content to only logged in users.
``[Authorize]`` can be used for a specific method or a whole controller.

``[AllowAnonymous]`` is an attribute that allows *any* viewer to access content.
This is the default state, so ``[AllowAnonymous]`` is oftentimes used in conjunction with ``[Authorize]``.

In ``CodingEvents``, we may only want to allow logged-in users to add an event.
We can add ``[Authorize]`` at the controller level to prevent any anonymous
users from accessing those pages.

.. sourcecode:: csharp
   :lineno-start: 16

   [Authorize]
   public class EventsController : Controller
   {
      // Controller code here!
   }

Why do this? Because giving all users the ability to add, edit, or delete
events can cause trouble.

However, we do want to give all users the ability to view the events. That is
where ``[AllowAnonymous]`` comes in. We can update the controller so that the
``Index`` view is accessible to everyone like so:

.. sourcecode:: csharp
   :lineno-start: 16

   [Authorize]
    public class EventsController : Controller
    {

        private EventDbContext context;

        public EventsController(EventDbContext dbContext)
        {
            context = dbContext;
        }

        [AllowAnonymous]
        // GET: /<controller>/
        public IActionResult Index()
        {
            List<Event> events = context.Events
                .Include(e => e.Category)
                .ToList();

            return View(events);
        }

        // Other action methods here!
    }

Now every user can see available events, but only logged-in users can add, edit, or delete events!