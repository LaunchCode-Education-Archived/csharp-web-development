Controllers with Parameters
===========================

Now that you know the basics of a controller method, we can start to add some more variables into the mix. Some 
controller methods can take in parameters in the form of query strings or sections of the URL path. Passing
this URL data to the controller is one step closer to more flexible web applications. 

On the previous page, we learned a route is the mechanism by which a request path gets assigned to a
controller within our application. In this section, we’ll further explore routes and how data is transferred from a webpage with a given route to a specific controller.

.. index:: ! query string

Query Strings are URL Data
--------------------------

A brief refresher: query strings are additional bits of information tacked onto the ends of urls.
They contain data in key-value pairs.

::

   www.galaxyglossary.net?aKey=aValue&anotherKey=anotherValue&thirdKey=thirdValue

Controllers and Query Parameters - Video
-----------------------------------------

.. TODO: Add a video for "Hello ASP.NET Part 3"

Parameters
----------

We can pass different parameters in controller method. Let's add a method called ``Welcome()`` to ``HelloController.cs``. 

.. sourcecode:: csharp
   :linenos:

   public IActionResult Welcome(string Name = "World")
   {
      return Content(string.Format("<h1>Welcome to my app, {0}!</h1>", Name), "text/html");
   }

The ``Welcome()`` method has one argument, ``Name``. We can give ``Name`` a default value so that if it is not assigne3d any other value, our method iwll still function.
This makes ``Name`` an **optional parameter**. If we navigate to ``localhost::5001/hello/welcome``, we will just see "Welcome to my app, World!".
If a value besides ``"World"`` is provided to ``Name``, such as by navigating to ``localhost::5001/hello/welcome?name=Ringo``, then the page displays "Welcome to my app, Ringo!". 

Check Your Understanding
------------------------

.. admonition:: Question

   Your application is served at ``myfavoriteplanets.net``. What is the path 
   that this controller maps to?

   .. sourcecode:: csharp
      :linenos:

      public IActionResult VenusSurface(string Terrestrial) {
      if (Terrestrial == true) {
         return "Venus is rocky."        
      } else {
         return "Venus is gaseous."
      }
 
   a. ``myfavoriteplanets.net/venus?terrestrial=true``
      
   b. ``net.myfavoriteplanets/venus?terrestrial=true``

   c. ``myfavoriteplanets/venus?terrestrial=true``

   c. ``myfavoriteplanets/venus/terrestrial``

.. ans: a, myfavoriteplanets.net/venus?terrestrial=true


