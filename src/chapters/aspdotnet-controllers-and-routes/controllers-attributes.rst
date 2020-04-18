Attribute Routing
=================

Attribute Routing - Video
--------------------------

.. TODO: Add vid

.. admonition:: Note

   In your forked version of LaunchCode's `HelloASPDotNET <https://github.com/LaunchCodeEducation/HelloASPDotNET>`_, the starter code for this video is on the ``forms`` branch.
   The solution code for this video is on the ``attribute-routing`` branch.

.. index:: ! attribute routing, ! attributes

Attribute Routing - Text
------------------------

Once you have written several controller methods within a class, you may notice some similar behavior across handlers.
You may also want to expand upon the behavior that different methods can make use of.
So far, we have been relying on conventional routing for mapping our requests and our endpoints.
As we continue learning, we will also make use of attribute routing.
**Attribute routing** uses **attributes** to establish routes, different types of requests that the method responds to, and so on.
Attributes lie somewhere between code and comments. While an attribute cannot change the code inside the method or class, an attribute does supply critical information to the compiler.
Attribute routing is powerful because it does not require us to add any mapping info to ``Startup.cs``.
We can provide all of the information the compiler needs about mapping routes in attributes in our controller files.

Here is how we might modify an existing method in ``HelloController`` to make use attribute routing.

.. sourcecode:: csharp 
   :linenos:

   [HttpGet]
   public IActionResult Welcome(string name = "World")
   {
      return Content(string.Format("<h1>Welcome to my app, {0}!</h1>", name), "text/html");
   }

The ``[HttpGet]`` attribute on line 1 specifies that the method responds to a ``GET`` request.
Attributes have to go directly above the method signature or the class. 
Other attributes you may find yourself using include ``[HttpPost]`` to specify methods that respondd to ``POST`` requests and ``[Route("path")]`` to map the route that the method responds to.

.. admonition:: Note

   ASP.NET has many different attributes that we can use in our controllers.
   For a more in-depth catalog of different attributes, check out the `documentation <https://docs.microsoft.com/en-us/aspnet/web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2>`_.

.. index:: ! path variable

Class-level Attributes
----------------------

``[RoutePrefix()]``

Check Your Understanding
------------------------

.. admonition:: Question

   True/False: Attributes go below the method signature.
 
   a. True
      
   b. False

.. ans: b, attributes go above the method signature

.. admonition:: Question

   We want the method ``WelcomeByName`` to take another parameter, ``string friend``, that will 
   add a friend's name to the returned greeting. What is an appropriate path to use in our ``Route`` attribute? 
 
   a. ``/hello/{name}?{friend}``

   b. ``/hello/{name}/{friend}``

   c. ``/hello/{name}+{friend}``

   d. ``/hello/name/friend``

.. ans:  b, ``/hello/{name}/{friend}``


