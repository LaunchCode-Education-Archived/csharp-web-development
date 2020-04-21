.. index:: ! route

Simple Controllers
==================

The first of the MVC elements we'll work on implementing are the controllers. Recall that controllers 
are like the traffic cops of our application. They handle the requests made from users interacting with the 
application's view and update model data accordingly. Conversely, changes to model data are sent to the view 
via controller methods. When the client issues an HTTP request via URL, we want to make sure that the URL leads to the correct controller so we get an appropriate response.
A **route** is the mechanism by which a request path gets assigned to a controller within our application.

.. figure:: figures/mvcOverviewDetail.png
      :scale: 50%
      :alt: MVC Flow Diagram showing controllers in the middle passing data between the view and the model

      MVC Flow

.. admonition:: Note

   Do HTTP requests and responses feel unfamiliar?
   If you're feeling rusty on these topics, it's a good idea to brush up now, as routing requires a foundational understanding of HTTP data transfer.

   Here's our `introduction to HTTP <https://education.launchcode.org/intro-to-professional-web-dev/chapters/http/index.html>`__ 
   for reviewing the concepts.

Controllers and Static Responses - Video
----------------------------------------

.. TODO: Add video titled "Hello ASP.NET Part 2"

.. admonition:: Note 

   If you ever want to verify what code you started the video with, the `starter code <https://github.com/LaunchCodeEducation/HelloASPDotNET>`_ for this video is on the ``master`` branch.
   If you ever want to verify what code you end the video with, the `solution code <https://github.com/LaunchCodeEducation/HelloASPDotNET/tree/static-responses>`_ for this video is on the ``static-responses`` branch.

Controllers and Static Responses - Intro
----------------------------------------

.. index:: ! Controller

``Controller``
^^^^^^^^^^^^^^

In ASP.NET, we'll organize controller code into the provided ``Controllers`` directory.
Some tools may depend on us following the convention of the MVC design pattern, so it is important to put our controller code in this directory. 
If you want to change something about the provided structure, be sure to double check the documentation to make sure a tool does not depend on you following it!

To designate a given class as a controller within the ASP.NET framework, we extend the ``Controller`` class.
The `Controller class <https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.mvc.controller?view=aspnetcore-3.1>`_ provides us with the necessary members and methods to manage traffic between the three components in our MVC application. 

.. sourcecode:: csharp

   public class HelloController : Controller
   {

      // class code here ...

   }

.. index:: ! endpoint, ! route, ! routing, ! conventional routing, ! attribute routing

Controllers Map to Requests
^^^^^^^^^^^^^^^^^^^^^^^^^^^

Controllers need to handle HTTP requests coming in and that routes are a key component of that process
ASP.NET MVC has two different ways to map these routes: conventional routing and attribute routing.
**Conventional routing** establishes the routes as endpoints in one of the application's configuration files.
**Attribute routing** establishes the routes using code called attributes that are placed in the controller file.

When we created a new ASP.NET application, without adding any code, we were immediately able to run it.
Microsoft created a ``HomeController`` that maps to the route ``localhost:5001``. 
This is because the MVC application we start out with has the routing for ``HomeController`` set up using conventional routing.
For every controller method that you want to respond to a request, you will want to map the route using either conventional routing, attribute routing, or both.

Open up ``Startup.cs`` in the solution.
Towards the bottom of the file, you will notice a block of code that calls the ``UseEndpoints()`` method on an ``app`` object.
This is how ASP.NET maps controller routes in conventional routing.
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

The ``default`` route is to the ``HomeController``, which came with our application courtesy of Microsoft.
When we navigate to our application's address, we see the result of the ``Index()`` method in the ``HomeController`` which is a view.
We will learn more about how views work in a later chapter.

When adding a new controller, such as ``HelloController``, we need to make sure that routing is properly configured whether we use conventional routing or attribute routing.
Let's start by adding the following ``Index()`` method:

.. sourcecode:: csharp
   :linenos:

   // GET: /<controller>/
   public IActionResult Index() 
   {
      string html = "<h1>" + "Hello World!" + "<h1>";
      return Content(html, "text/html");
   }

The comment above our new method tells us that the ``Index()`` method above will respond to ``GET`` requests at ``localhost:5001/Hello``.
Let's run the app and navigate to ``localhost:5001/Hello``!

.. admonition:: Warning

   Conventional routing makes use of the controller's name.
   If you capitalize the controller name, but don't capitalize the name in the route, then you will get an error.
   In the case of our ``HelloController``, if you go to ``localhost:5001/hello``, the page will not work!
   You have to make sure that ``Hello`` is capitalized in the route.

.. index:: ! attribute

We might also want to make use of attribute routing in our new ``HelloController``.
To do so, we can add attributes to our ``Index()`` method.
**Attributes** lie somewhere between code and comments.
While an attribute cannot change the code inside the method or class, an attribute does supply critical information to the compiler.
Attribute routing is powerful because it does not require us to add any mapping info to ``Startup.cs``.

As we did above, we want to ``Index()`` to respond to a ``GET`` request at a specified route.
The route we want to go to is ``localhost:5001/hello/attribute``. 
We can use an ``[HttpGet]`` attribute to specify that the method will respond to a ``GET`` request.
We also want to use a ``[Route("path")]`` attribute and a ``[RoutePrefix("path")]`` attribute.
``[Route("path")]`` is used above the method to establish the route that maps to that method and ``[RoutePrefix("path")]`` goes above the class name to establish a common start to all of the routes for the methods in the controller.

Let's see how we can add attributes to ``HelloController``!

.. sourcecode:: csharp
   :linenos:

   [RoutePrefix("/hello")]
   class HelloController : Controller
   {
      [HttpGet]
      [Route("/attribute")]
      public IActionResult Index() 
      {
         string html = "<h1>" + "Hello World!" + "<h1>";
         return Content(html, "text/html");
      }
   }

"/[controller]" to match conventional route.

Now when we run our application, we can head over to ``localhost:5001/hello/attribute`` to see the result.
If we head over to the route that was mapped through conventional routing, ``localhost:5001/Hello``, we will find a broken page.

After we add the ``Index()`` method and configure the routing properly, we can run our application and navigate to ``localhost:5001/hello/attribute``.
The result is a simple web page with one heading that says "Hello World!"

.. figure:: figures/staticresponseresult.png
   :alt: Simple webpage resulting from adding a new method to the controller

   Our end result!

.. admonition:: Note

   Throughout this chapter, we will add map our routes with both approaches.
   While, you may prefer one or the other, many applications contain a combination of both conventional and attribute routing.
   We encourage you to try out both approaches to make sure that you can recognize and understand both approaches to routing.

The ``Index()`` method above returns an unfamiliar type, ``IActionResult``.
We will be using ``IActionResult`` quite a bit in our applications, so let's take a deeper look.

.. index:: ! IActionResult

``IActionResult``
^^^^^^^^^^^^^^^^^

``IActionResult`` is an interface in the ASP.NET framework and often times the return type of controller methods.
When we specify the return type as ``IActionResult``, the returned value dictates what the client will display.
We can use ``IActionResult`` to get the client to display JSON, a view, or even plain text.
We will only scratch the surface of what ``IActionResult`` can do so for now, let's focus on ``Content``.

In our ``Index()`` method, we want to return a simple string of HTML to be displayed on the webpage.
We use ``Content()`` to specify which string we want to use for our content and we specify the content type with ``"text/html"``.
When using ``Content()``, we need to specify the content type in order the page to render how we want it to!

.. admonition:: Note

   For more info on the different types of results we could specify as return types, check out this `article <https://exceptionnotfound.net/asp-net-core-demystified-action-results/>`_!

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

