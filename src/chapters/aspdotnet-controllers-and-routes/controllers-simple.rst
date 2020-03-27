Simple Controllers
==================

The first of the MVC elements we'll work on implementing are the controllers. Recall that controllers 
are like the traffic cops of our application. They handle the requests made from users interacting with the 
application's view and update model data accordingly. Conversely, changes to model data are sent to the view 
via controller methods.

.. figure:: figures/mvcOverviewDetail.png
      :scale: 50%
      :alt: MVC Flow Diagram showing controllers in the middle passing data between the view and the model

      MVC Flow

.. admonition:: Note

   Do HTTP requests and responses feel unfamiliar? Do you remember what a **query string**
   is? If you're feeling rusty on these topics, it's a good idea to brush up now, as routing 
   requires a foundational understanding of HTTP data transfer.

   Here's our `introduction to HTTP <https://education.launchcode.org/intro-to-professional-web-dev/chapters/http/index.html>`__ 
   for reviewing the concepts.

Controllers and Static Responses - Video
----------------------------------------

.. TODO: Add video titled "Hello ASP.NET Part 2"

The starter code is on ``master``
The solution code is on ``static-responses``

Controllers and Static Responses - Intro
----------------------------------------

.. index:: ! Controller

``Controller``
^^^^^^^^^^^^^^

In ASP.NET, we'll organize controller code into a controller directory.
Remember when we mentioned that the framework works by convention over configuration?
This is what we mean. It's not required for a controller to be in a controller package, but it's generally a good idea.

To designate a given class as a controller within the ASP.NET framework, we extend the ``Controller`` class.
The `Controller class <https://docs.microsoft.com/en-us/dotnet/api/system.web.mvc.controller?view=aspnet-mvc-5.2>`_ provides us with the necessary members and methods to send and receive HTTP requests in our controller. 

.. sourcecode:: csharp

   public class HelloController : Controller
   {

      // class code here ...

   }

.. index:: ! endpoint, ! route, ! routing

Controllers Map to Requests
^^^^^^^^^^^^^^^^^^^^^^^^^^^

The first request we will work with is a GET request. When mapping the route for the GET request we want to designate the path that the method needs to be called for.
ASP.NET MVC has two different ways to map routes: conventional routing and attribute routing. For now, we will be using conventional routing and will progress to attribute routing later on.

.. sourcecode:: csharp
   :linenos:

   public class HelloController : Controller
   {
      // GET: "/hello/"
      public String Index() {
         // method code here ...
      }
   }

For every controller method that you want to respond to a request, you will want to map the route.
Check out ``Startup.cs`` in the solution. Towards the bottom of the file, you will notice a block of code that calls some ``UseEndpoints()`` method on an ``app`` object.
This is how ASP.NET maps controller routes. When we created a new ASP.NET application, without adding any code, we were immediately able to run it.
Looking at this method, shown in the code block below, you may notice that the code is specifying endpoints. When an HTTP request comes in to our application, routing matches the request with an endpoint.
**Endpoints** designate the controller action that executes when the appropriate HTTP request comes into the application.

.. sourcecode:: csharp
   :linenos:

   app.UseEndpoints(endpoints =>
   {      
      endpoints.MapControllerRoute(
         name: "default",
         pattern: "{controller=Home}/{action=Index}/{id?}");
   });

The default route is to the ``HomeController``, which came with our application courtesy of Microsoft. When we navifate to our application's address, we see the home page with more information about ASP.NET.
When adding a new controller, such as ``HelloController``, we need to add an endpoint for the controller and its methods.

.. sourcecode:: csharp
   :linenos:

   app.UseEndpoints(endpoints =>
   {      
      endpoints.MapControllerRoute(
         name: "default",
         pattern: "{controller=Home}/{action=Index}/{id?}");
      endpoints.MapControllerRoute(name: "hello",
         pattern: "hello/{*index}",
         defaults: new { controller = "Hello", action = "Index" });
   });

Above, on lines 6-8, we added a new endpoint for the ``HelloController``. We gave the name ``"hello"`` for simplicity and specified a pattern.

Now, we can add various methods to our ``HelloController``. Let's start by adding an ``Index()`` method.

.. sourcecode:: csharp
   :linenos:

   public IActionResult Index() 
   {
      string html = "<h1>" + "Hello World!" + "<h1>";
      return Content(html, "text/html");
   }

The ``Index()`` method returns an unfamiliar type, ``IActionResult``, and uses a method ``Content()``.
We will be using ``IActionResult`` quite a bit in our applications, but won't see as much of ``Content()`` after we learn about views and templates.

.. index:: ! IActionResult

``IActionResult``
^^^^^^^^^^^^^^^^^

Check Your Understanding
------------------------

.. admonition:: Question

   True/False: The ``Controller`` class does not have to be extended to classify a class as a controller.
 
   a. True
      
   b. False

.. ans: a

.. admonition:: Question

   Which of the following is true about controllers?
 
   a. Controllers handle the data storage of an MVC app.

   b. Controllers manage what the user of an MVC application sees.

   c. Controllers relay the messages between data and views in an MVC application.

   d. Controllers determine what information can be submitted in an online form.

.. ans: c, Controllers relay the messages between data and views in an MVC application.

