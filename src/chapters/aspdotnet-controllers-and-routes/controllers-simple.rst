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

.. admonition:: Note 

   If you ever want to verify what code you started the video with, the starter code for this video is on the ``master`` branch.
   If you ever want to verify what code you end the video with, the solution code for this video is on the ``static-responses`` branch.

Controllers and Static Responses - Intro
----------------------------------------

.. index:: ! Controller

``Controller``
^^^^^^^^^^^^^^

In ASP.NET, we'll organize controller code into the provided ``controller`` directory.
Remember when we mentioned that the framework works by convention over configuration?
In the case of ASP.NET, some tools may depend on us following the convention. 
If you want to change something about the provided structure, be sure to double check the documentation to make sure a tool does not depend on you following it!

To designate a given class as a controller within the ASP.NET framework, we extend the ``Controller`` class.
The `Controller class <https://docs.microsoft.com/en-us/dotnet/api/system.web.mvc.controller?view=aspnet-mvc-5.2>`_ provides us with the necessary members and methods to manage traffic between the three components in our MVC application. 

.. sourcecode:: csharp

   public class HelloController : Controller
   {

      // class code here ...

   }

.. index:: ! endpoint, ! route, ! routing

Controllers Map to Requests
^^^^^^^^^^^^^^^^^^^^^^^^^^^

The first HTTP request we will work with in this chapter is a ``GET`` request.
For every ``GET`` request made to the provided path, the controller method will be called.
How do we provide the path?
ASP.NET MVC has two different ways to map these routes: conventional routing and attribute routing.
For now, we will be using conventional routing and will progress to attribute routing later on in the chapter.

For every controller method that you want to respond to a request, you will want to map the route.
Open up ``Startup.cs`` in the solution.
Towards the bottom of the file, you will notice a block of code that calls some ``UseEndpoints()`` method on an ``app`` object.
This is how ASP.NET maps controller routes in conventional routing.
When we created a new ASP.NET application, without adding any code, we were immediately able to run it.
Looking at this method, shown in the code block below, you may notice that the code is specifying endpoints.
When an HTTP request comes in, routing matches the request with an endpoint.
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
      endpoints.MapControllerRoute(
         name: "hello",
         pattern: "hello/{*index}",
         defaults: new { controller = "Hello", action = "Index" });
   });

Above, on lines 6-8, we added a new endpoint for the ``HelloController``.
We gave the name ``"hello"`` for simplicity, specified that the pattern for the routes starts with ``/hello/``, and that the default for the route is to go to the ``Index()`` method in ``HelloController``.

Now, we can add various methods to our ``HelloController``.
Let's start by adding the following ``Index()`` method:

.. sourcecode:: csharp
   :linenos:

   // GET: /<controller>/
   public IActionResult Index() 
   {
      string html = "<h1>" + "Hello World!" + "<h1>";
      return Content(html, "text/html");
   }

The ``Index()`` method returns an unfamiliar type, ``IActionResult``.
We will be using ``IActionResult`` quite a bit in our applications, so let's take a deeper look.

.. index:: ! IActionResult

``IActionResult``
^^^^^^^^^^^^^^^^^

``IActionResult`` is an interface in the ASP.NET framework.
Classes that implement this interface are representative of what the client will do because of the controller action.
So if our ``Index()`` method is called in ``HelloController``, the returned value dictates what the client will display.

We will often choose throughout this book to return content as a result.
Content can include a view (from model-view-controller), JSON, and simple text, for example. 
In our ``Index()`` method, we want to return a simple string of HTML to be displayed on the webpage.
We use ``Content()`` to specify which string we want to use for our content and we specify the content type with ``"text/html"``.
When using ``Content()``, we need to specify the content type in order the page to render how we want it to!

.. admonition:: Note

   For more info on the different types of results we could specify as return types, check out this `article <https://exceptionnotfound.net/asp-net-core-demystified-action-results/>`_!

After we add the ``Index()`` method and configure the routing properly, we can run our application and navigate to ``localhost:5001/hello``.
The result is a simple web page with one heading that says "Hello World!"

.. figure:: figures/staticresponseresult.png
   :alt: Simple webpage resulting from adding a new method to the controller

   Our end result!

Check Your Understanding
------------------------

.. admonition:: Question

   True/False: The ``Controller`` class does not have to be extended to classify a class as a controller.
 
   a. True
      
   b. False

.. ans: b

.. admonition:: Question

   Which of the following is true about controllers?
 
   a. Controllers handle the data storage of an MVC app.

   b. Controllers manage what the user of an MVC application sees.

   c. Controllers relay the messages between data and views in an MVC application.

   d. Controllers determine what information can be submitted in an online form.

.. ans: c, Controllers relay the messages between data and views in an MVC application.

