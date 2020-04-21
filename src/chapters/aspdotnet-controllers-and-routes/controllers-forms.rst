Controllers with Forms
======================

Sending Form Data - Video
-------------------------

.. TODO: Add "Hello ASP.NET Part 4" vid

.. admonition:: Note

   In your forked version of LaunchCode's `HelloASPDotNET <https://github.com/LaunchCodeEducation/HelloASPDotNET>`_, the starter code for this video is on the ``query-parameters`` branch.
   The solution code for this video is on the ``forms`` branch.

Sending Form Data - Text
-------------------------

What if we want to send over some form data?
To send data via a simple form in ASP.NET, we'll set things up like this:

We have an action method that generates a form at index and responds to a ``GET`` request. 

.. sourcecode:: csharp
   :linenos:

   public IActionResult Index()
   {
      string html = "<form method='post' action='Hello/Display'>" +
         "<input type='text' name='name' />" +
         "<input type='submit' value='Greet Me!' />" +
         "</form>";

      return Content(html, "text/html");
   }

With conventional routing, we know that the ``Index()`` method currently responds to ``localhost:5001/Hello``.
On form submission, we want to send the data down another path, ``/Hello/Display``.
We need an action method for that to repond to the ``POST`` request upon form submission.

.. sourcecode:: csharp
   :linenos:

   public IActionResult Display(string name = "World")
   {
      return Content("<h1>Hello " + name + "!</h1>", "text/html");
   }

Now, you have a method that can handle the form submission.
When the form submits, the input entered in the text box will be passed to the URL.
This is why the ``Display()`` method above accepts a ``name`` argument.

With the ``Index()`` method rewritten and a new ``Display()`` method, we can run our app and see what happens!

.. figure:: figures/filledoutform.png
   :alt: Webpage with filled out form 

   New form filled out with the name "Tillie"

Once we hit *Greet Me*, the value of ``name``, ``"Tillie"``, is submitted to the ``Display()`` method.

.. figure:: figures/displayformresult.png
   :alt: Webpage displaying the form result

   A whole new page on our site!

With our form working, we can add some attribute routing to streamline the process and send our form data down a different route.
For the ``Index()`` method, we want the method to respond to a ``GET`` request at ``localhost:5001/helloworld``.

.. sourcecode:: csharp
   :linenos:

   [HttpGet]
   [Route("/helloworld")]
   public IActionResult Index()
   {
      string html = "<form method='post' action='helloworld/display'>" +
         "<input type='text' name='name' />" +
         "<input type='submit' value='Greet Me!' />" +
         "</form>";

      return Content(html, "text/html");
   }

Now we also want to add attributes to the ``Display()`` method.
``Display()`` needs to respond to a ``POST`` request so we will add an ``[HttpPost]`` attribute.
We changed the value of ``action`` in our HTML form in the ``Index()`` method to ``'helloworld/display'``.
In order for our form data to properly be sent over to the ``Display()`` method, we need to map the method to the route specified in ``action``.
We will do so with a ``[Route("path")]`` attribute.

.. sourcecode:: csharp
   :linenos:

   [HttpPost]
   [Route("/helloworld/display")]
   public IActionResult Display(string name = "World")
   {
      return Content("<h1>Hello " + name + "!</h1>", "text/html");
   }

Now when we run our app, we can navigate to ``localhost:5001/helloworld`` and see our form.
Once we fill out the form and hit *Greet Me!*, the app redirects to ``localhost:5001/helloworld/display`` and greets the user!

Check Your Understanding
------------------------

.. admonition:: Question

   Which type of request is the ``Index()`` method going to respond to?
 
   a. ``GET`` request
      
   b. ``POST`` request

   c. ``PUT`` request

   d. ``DELETE`` request

.. ans: a

.. admonition:: Question

   Which type of request is the ``Display()`` method going to respond to?
 
   a. ``GET`` request
      
   b. ``POST`` request

   c. ``PUT`` request

   d. ``DELETE`` request

.. ans: b
