Controllers with Parameters
===========================

Now that you know the basics of action methods and controllers, we can start to add some more variables into the mix.
Some action methods can take in parameters in the form of query strings or sections of the URL path.
Passing this URL data to the controller is one step closer to more flexible web applications. 

On the previous page, we learned that a route is the mechanism by which a request path gets assigned to a controller within our application.
In this section, we’ll further explore routes and how data is transferred from a webpage with a given route to a specific controller.

.. index:: ! query string

Query Strings are URL Data
--------------------------

A brief refresher: **query strings** are additional bits of information tacked onto the ends of urls.
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

We can pass different parameters into an action method.
Let's add a method called ``Welcome()`` to ``HelloController.cs``. 

.. sourcecode:: csharp
   :linenos:

   // GET: /<controller>/Welcome
   public IActionResult Welcome(string name = "World")
   {
      return Content(string.Format("<h1>Welcome to my app, {0}!</h1>", name), "text/html");
   }

The ``Welcome()`` method has one argument, ``name``.
You may have noticed on the function signature on line 2 that we give the argument, ``name``, a value of ``"World"``.
We do this to make ``name`` an **optional parameter**.
Optional parameters are designated with a default value (in our case, ``"World"``) and method calls do not have to include a value for that parameter.
When working with query strings, it is wise to make the key an optional parameter in case no value is provided for it.
If a query string is not provided and we navigate to just ``localhost:5001/Hello/Welcome``, then our webpage will display "Welcome to my app, World!".

.. figure:: figures/queryparamdefault.png
   :alt: Webpage displaying "Welcome to my app, World!"

   Our webpage when we don't provide a query string.

If we do provide a query string and navigate to ``localhost:5001/Hello/Welcome?name=Ringo``, then our webpage will display "Welcome to my app, Ringo!".

.. figure:: figures/queryparamused.png
   :alt: Webpage displaying "Welcome to my app, Ringo!"

   Our webpage when we do provide a query string.

If we want to use a query string with attribute routing, we need to add a ``[HttpGet]`` attribute to specify that our method responds to a ``GET`` request.
We also want to specify the path with the ``[Route]`` attribute.

.. sourcecode:: csharp
   :linenos:

   [HttpGet]
   [Route("/helloworld/welcome/{name?}")]
   public IActionResult Welcome(string name = "World")
   {
      return Content("<h1>Welcome to my app, " + name + "!</h1>", "text/html");
   }

Now when we run our app and navigate to ``localhost:5001/helloworld/welcome?name=Ringo``, we get the same webpage as when we used conventional routing.
For the path of our route, we specified that the path end with ``{name?}``. Surrounding ``name`` with curly braces in the route path means that the URL uses the value of the ``name`` variable.
Adding the ``?`` specifies that ``name`` is an optional parameter so if we don't give it a value via query string, the web page will still display "Welcome to my app, World!". 

Path Variables
^^^^^^^^^^^^^^

Earlier in the chapter, we briefly mentioned that some controller methods could take in parameters in the form of a section of a URL path.
These types of parameters are called **path variables**.

With attribute routing added to the ``Welcome()`` method, ``Welcome()`` also responds to the path, ``localhost:5001/helloworld/welcome/Tillie``, and produces a webpage that displays ``"Welcome to my app, Tillie!"``.
When we enclosed ``name`` in curly braces, specifying that the value of ``name`` should be used, we also made it a path variable!
Now the action method, ``Welcome()``, responds to ``localhost:5001/helloworld/welcome``, ``localhost:5001/helloworld/welcome?name=Tillie``, and ``localhost:5001/helloworld/welcome/Tille``!

.. admonition:: Note

   Before moving on, make sure to add info about the different routes the method maps to in comments in your code!

Check Your Understanding
------------------------

.. admonition:: Question

   Your application is served at ``myfavoriteplanets.net``. What is the path 
   that this controller maps to?

   .. sourcecode:: csharp
      :linenos:

      [HttpGet]
      [Route("/venus/{terrestrial?}")]
      public IActionResult VenusSurface(string terrestrial)
      {
         if (terrestrial == true)
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


