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

Controllers and Static Responses - Video
----------------------------------------

.. TODO: Add video titled "Hello ASP.NET Part 2"

Controllers and Static Responses - Intro
----------------------------------------

.. index:: ! Controller

``Controller``
^^^^^^^^^^^^^^

In the ASPP.NET context, we'll organize controller code into a controller directory. Remember when we 
mentioned that the framework works by convention over configuration? This is what we mean. It's not required 
for a controller to be in a controller package, but it's generally a good idea.

To designate a given class as a controller within the ASP.NET framework, we extend the ``Controller`` class.
The `Controller class <https://docs.microsoft.com/en-us/dotnet/api/system.web.mvc.controller?view=aspnet-mvc-5.2>`_ provides us with the necessary members and methods to send and receive HTTP requests in our controller. 

.. sourcecode:: csharp

   public class HelloController : Controller
   {

      // class code here ...

   }

Controllers Map to Requests
^^^^^^^^^^^^^^^^^^^^^^^^^^^

The first request we will work with is a GET request. When mapping the route for the GET request we want to designate the path that the method needs to be called for.
ASP.NET MVC has two different ways to map routes: default routing and attribute routing. For now, we will be using default routing and will progress to attribute routing later on.

.. sourcecode:: csharp
   :linenos:

   public class HelloController : Controller
   {
      // GET: "/hello/"
      public String Index() {
         // method code here ...
      }
   }

For every controller method that you want to respond to a request, you will want to use map the route.
Not surprisingly, though, mapping routes only handles ``GET`` requests. If you want to write a controller 
method that takes care of a ``POST`` request, you'll want to use . Of course, there are 
other annotations for the other request methods, but these are the two we will use in this class.

.. sourcecode:: java

   @Controller
   public class HelloSpringController {

      // responds to post requests at "/goodbye"
      @PostMapping("goodbye")
      public String goodbye() {
         // method code here ...
      }

   }

If we want to write a controller method that will be used for both ``GET`` and ``POST`` at the same path, we
can label the method with ``@RequestMapping``. ``@RequestMapping`` can handle more than one method as such:

.. _request-method-example:

.. sourcecode:: java

   @Controller
   public class HelloSpringController {

      // responds to get and post requests at "/hellogoodbye"
      @RequestMapping(value="hellogoodbye", method = {RequestMethod.GET, RequestMethod.POST})
      public String hellogoodbye() {
         // method code here ...
      }

   }

The default method of ``@RequestMapping`` is ``GET``. Another added capability of ``@RequestMapping`` is that 
it can be applied to a whole class, not just a single method. When applied to a whole class, ``@RequestMapping``
essentially designates a base path that all methods in the class start with. 

.. index:: ! @ResponseBody

``@ResponseBody``
^^^^^^^^^^^^^^^^^

``@ResponseBody`` is yet another annotation used in the Spring controller context to return plain text
from a controller method. This annotation we will only need to use for a short while, before we start
to work with templates. Spring Boot's default action when responding to a controller method is to return 
a template. Since we aren't doing that yet however, we need to tell the framework to return plain text by 
adding the ``@ResponseBody`` annotation.

Let's put it all together:

.. sourcecode:: java

   @Controller
   public class HelloSpringController {

      // responds to get requests at "/hello" 
      @GetMapping("hello")
      @ResponseBody
      public String hello() {
         return "Hello, Spring!";
      }

   }


Check Your Understanding
------------------------

.. admonition:: Question

   True/False: The ``@Controller`` annotation goes above a method to classify
   it as a controller method.
 
   a. True
      
   b. False

.. ans: b, False the annotation goes atop the class 

.. admonition:: Question

   Which of the following is true about controllers?
 
   a. Controllers handle the data storage of an MVC app.

   b. Controllers manage what the user of an MVC application sees.

   c. Controllers relay the messages between data and views in an MVC application.

   d. Controllers determine what information can be submitted in an online form.

.. ans: c, Controllers relay the messages between data and views in an MVC application.

