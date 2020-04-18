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

We have a controller method that generates a form at index and responds to a ``GET`` request. 

.. sourcecode:: csharp
   :linenos:

   public IActionResult Index()
   {
      string html = "<form method='post' action='hello/display'>" +
         "<input type='text' name='name' />" +
         "<input type='submit' value='Greet Me!' />" +
         "</form>";

      return Content(html, "text/html");
   }

Remember, we set our endpoint to default to the ``Index()`` method.
On form submission, the data is sent to another path, ``/hello/display``.
We need a controller method for that to repond to the ``POST`` request.

.. sourcecode:: csharp
   :linenos:

   public IActionResult Display(string name = "World")
   {
      return Content(string.Format("<h1>Hello {0}</h1>", name), "text/html");
   }

Now, you have a method that can handle the form submission.
When the form submits, the input entered in the text box will be passed to the URL via a query string.
This is why the controller method above accepts a ``name`` argument.

With the ``Index()`` method rewritten and a new ``Display()`` method, we can run our app and see what happens!

.. figure:: figures/filledoutform.png
   :alt: Webpage with filled out form 

   New form filled out with the name "Tillie"

Once we hit *Greet Me*, the value of ``name``, ``"Tillie"``, is submitted to the ``Display()`` method.

.. figure:: figures/displayformresult.png
   :alt: Webpage displaying the form result

   A whole new page on our site!

Let's add more attributes!

``[HttpGet]`` for the ``Index()`` method and ``[HttpPost]`` for the ``Display`` method.
The ``action`` of the form specifies the route that the controller maps to after the button is hit.

If we want to change the route from the conventional routing, we need to modify the value of ``action`` to make sure that the page that is properly redirected.

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
