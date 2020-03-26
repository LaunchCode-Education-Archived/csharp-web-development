Controllers with Forms
======================

Sending Form Data - Video
-------------------------

.. TODO: Add "Hello ASP.NET Part 4" vid

Sending Form Data - Text
-------------------------

What if we want to send over some form data? To send data via a simple form in Spring 
Boot, we'll set things up like this:

We have a controller method that generates a form at index. 

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

Remember, we set our endpoint to default to the ``Index()`` method. On form submission, the 
data is sent to another path, ``/welcome``. We need a controller method for that.

.. sourcecode:: csharp

   public IActionResult Display(string name = "World")
   {
      return Content(string.Format("<h1>Hello {0}</h1>", name), "text/html");
   }

Now, you have a method that can handle the form submission. When the form submits, the 
input entered in the text box will be passed to the URL via a query string. This is why 
the controller method above accepts a ``Name`` argument.

Check Your Understanding
------------------------

.. admonition:: Question

   From the list below, which annotations are applied above a controller class.
 
   a. ``@Controller``
      
   b. ``@GetMapping``

   c. ``@PostMapping``

   d. ``@RequestMapping``

   e. ``@ResponseBody``

   f. ``@RequestParam``

   g. ``@PathVariable``

.. ans: a, d, + e, controller, requestmapping, and responsebody

.. admonition:: Question

   From the list below, which annotations are applied above a controller method.
 
   a. ``@Controller``
      
   b. ``@GetMapping``

   c. ``@PostMapping``

   d. ``@RequestMapping``

   e. ``@ResponseBody``

   f. ``@RequestParam``

   g. ``@PathVariable``

.. ans: b, c, d, + e, getmapping, postmapping, requestmapping, and responsebody
