Exercise Solutions: Controllers and Routes
==========================================

Line numbers are for reference. They may not match your code exactly.

Part 1: ``GET`` Request
-----------------------

.. _modify-controller:

Modify your ``HelloController`` class to display a form on a ``GET`` request 
that asks the user for both their name and the language they would like to be greeted in.

.. sourcecode:: csharp
   :linenos:

      //GET: /<controller>/
      public IActionResult Index()
      {
         string html = "<form method='post'>" +
            "<input type='text' name='name' />" +
            "<select name='language'>" +
            "<option value='english' selected>English</option>" +
            "<option value='french'>French</option></select>" +
            // ... add any other languages here ... 
            "<input type='submit' value='Greet Me!'/>" +
            "</form>";

         return Content(html, "text/html");
      }

:ref:`Return to exercises<controller-routes-exercises-1>`

Part 2: ``POST`` Request
------------------------

.. _modify-POST:

2. Include a new ``public static`` method, ``CreateMessage``, in the ``HelloController`` that takes a name as well as a language string. 
   Based on the language string, you’ll display the proper greeting.

.. sourcecode:: csharp
   :linenos:

      public static string CreateMessage(string name, string language)
      {
         string helloTranslation = "";
         switch (language)
         {
            case "french":
               helloTranslation = "Bonjour ";
               break;
            case "english":
               helloTranslation = "Hello ";
               break;
            // ... add any other languages here ...
         }
         return helloTranslation + name;
      }


:ref:`Return to exercises<controller-routes-exercises-2>`