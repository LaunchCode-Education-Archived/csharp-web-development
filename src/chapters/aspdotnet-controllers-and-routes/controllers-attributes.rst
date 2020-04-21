Streamling Your Code with Attribute Routing
===========================================

Attribute Routing - Video
--------------------------

.. TODO: Add vid

.. admonition:: Note

   In your forked version of LaunchCode's `HelloASPDotNET <https://github.com/LaunchCodeEducation/HelloASPDotNET>`_, the starter code for this video is on the ``forms`` branch.
   The solution code for this video is on the ``attribute-routing`` branch.

.. index:: ! attribute routing, ! attributes

Attribute Routing - Text
------------------------

Once you have written several action methods within a class, you may notice some similar behavior.
You may also want to expand upon the behavior that different action methods can make use of.
So far, we have been adding multiple different ``[Route("path")]`` attributes to each method to get every method to respond to a path that starts with ``localhost:5001/helloworld``.
The ``Welcome()`` method and ``Display()`` method also serve similar purposes and feel a bit repetitive.
Time to DRY our code!

Class-Level Attributes
^^^^^^^^^^^^^^^^^^^^^^

In addition to adding attributes above action methods, we can also add attributes for routing above the class.
When we do so, we are designating class-wide behavior.
In ``HelloController``, we want every action method to respond to requests at paths that start with ``localhost:5001/helloworld``.
We can use ``[Route("path")]`` once above the class to designate that every path for each action method needs to start with ``/helloworld``.

.. sourcecode:: csharp 
   :linenos:

   [Route("/helloworld")]
    public class HelloController : Controller
    {
        // action methods here
    }

Now that we have added that ``[Route("/helloworld")]`` above the class, we can start to modify the attributes we placed above the ``Index()`` method.

.. sourcecode:: csharp
   :linenos:

   [HttpGet]
   public IActionResult Index()
   {
      string html = "<form method='post' action='helloworld/display'>" +
            "<input type='text' name='name' />" +
            "<input type='submit' value='Greet Me!' />" +
            "</form>";

      return Content(html, "text/html");
   }

Since we want to map ``Index()`` to the path ``localhost:5001/helloworld``, we removed the ``[Route("/helloworld")]`` attribute above the method.
If we hadn't, we would have inadvertently mapped the ``Index()`` method to the path, ``localhost:5001/helloworld/helloworld``.
We want to leave the ``[HttpGet]`` attribute above the ``Index()`` method so we can still specify that ``Index()`` responds to ``GET`` requests.

Now that just leaves us the ``Welcome()`` and ``Display()`` methods!

One Method, Two Request Types
-----------------------------

Despite ``Welcome()`` and ``Display()`` responding to different request types, the two methods return very similar strings of HTML.
With attributes, we can DRY our code and create one method that can respond to two different request types at two different routes.
Before we begin, we should note that we can add route info directly to ``[HttpGet]`` and ``[HttpPost]``.

.. sourcecode:: csharp
   :linenos:

   [HttpPost("display")]
   public IActionResult Display(string name = "World")
   {
      return Content("<h1>Hello " + name + "!</h1>", "text/html");
   }

On line 1, we modified the ``[HttpPost]`` attribute to include the end of our path.
Now ``Display()`` still responds to ``POST`` requests at ``localhost:5001/helloworld/display``.
However, this is just the beginning of us DRYing our code.

We want to comment out the ``Welcome()`` method and add another attribute to ``Display()`` so that we have one method responding to two different types of HTTP requests at two different paths.
We can add an ``[HttpGet]`` attribute to ``Display()`` to do so.

.. sourcecode:: csharp
   :linenos:

   [HttpGet("welcome/{name?}")]
   [HttpPost("display")]
   public IActionResult Display(string name = "World")
   {
      return Content("<h1>Hello " + name + "!</h1>", "text/html");
   }

We added an ``[HttpGet]`` attribute on line 1 with a different path.
Now ``Display()`` can respond to ``GET`` requests at ``localhost:5001/helloworld/welcome``, ``localhost:5001/helloworld/welcome?name=Tillie``, and ``localhost:5001/helloworld/welcome/Tille``.
``Display()`` can also still respond to the ``POST`` request at ``localhost:5001/helloworld/display`` upon submission of the form.

Now when we run our code, our app will still have the same functionalities, but now we have a more refined and organized code base!

Check Your Understanding
------------------------

.. admonition:: Question

   True/False: Attributes go below the class definition, but above the method signature.
 
   a. True
      
   b. False

.. ans: b, attributes go above both the class definition and the method signature

