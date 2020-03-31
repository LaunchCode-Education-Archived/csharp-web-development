Controllers with Parameters
===========================

Now that you know the basics of a controller method, we can start to add some more variables into the mix.
Some controller methods can take in parameters in the form of query strings or sections of the URL path.
Passing this URL data to the controller is one step closer to more flexible web applications. 

On the previous page, we learned a route is the mechanism by which a request path gets assigned to a
controller within our application.
In this section, we’ll further explore routes and how data is transferred from a webpage with a given route to a specific controller.

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

.. admonition:: Note

   In your forked copy of LaunchCode's `HelloASPDotNET <https://github.com/LaunchCodeEducation/HelloASPDotNET>`_, the starter code for this video is on the ``static-responses`` branch. 
   The solution code for this video is on the ``query-parameters`` branch.

Parameters
----------

We can pass different parameters in controller method.
Let's add a method called ``Welcome()`` to ``HelloController.cs``. 

.. sourcecode:: csharp
   :linenos:

   // GET: /<controller>/welcome
   public IActionResult Welcome(string name = "World")
   {
      return Content(string.Format("<h1>Welcome to my app, {0}!</h1>", name), "text/html");
   }

The ``Welcome()`` method has one argument, ``name``.
You may have noticed on the function signature on line 2 that we give the argument, ``name``, a value of ``"World"``.
We do this to make ``name`` an **optional parameter**.
Optional parameters are designated with a default value (in our case, ``"World"``) and method calls do not have to include a value for that parameter.
When working with query strings, it is wise to make the key an optional parameter in case no value is provided for it.
If a query string is not provided and we navigate to just ``localhost:5001/hello/welcome``, then our webpage will display "Welcome to my app, World!".

.. figure:: figures/queryparamdefault.png
   :alt: Webpage displaying "Welcome to my app, World!"

   Our webpage when we don't provide a query string.

If we do provide a query string and navigate to ``localhost:5001/hello/welcome?name=Ringo``, then our webpage will display "Welcome to my app, Ringo!".

.. figure:: figures/queryparamused.png
   :alt: Webpage displaying "Welcome to my app, Ringo!"

   Our webpage when we do provide a query string.

Check Your Understanding
------------------------

.. admonition:: Question

   Your application is served at ``myfavoriteplanets.net``. What is the path 
   that this controller maps to?

   .. sourcecode:: csharp
      :linenos:

      public IActionResult VenusSurface(string Terrestrial)
      {
         if (Terrestrial == true)
         {
            return "Venus is rocky."        
         }
         else
         {
            return "Venus is gaseous."
         }
      }
 
   a. ``myfavoriteplanets.net/venus?terrestrial=true``
      
   b. ``net.myfavoriteplanets/venus?terrestrial=true``

   c. ``myfavoriteplanets/venus?terrestrial=true``

   d. ``myfavoriteplanets/venus/terrestrial``

.. ans: a, myfavoriteplanets.net/venus?terrestrial=true


