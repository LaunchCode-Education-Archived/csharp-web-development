Exercises: Controllers and Routing
==================================

.. TODO: check on starter repo name from book content. holding spot name for now: HelloASPDotNET

While reading the chapter, you created a basic Hello, World application using ASP.NET
called ``HelloASPDotNET``. Open that project up in Visual Studio, and get ready to add some 
features.

Modify your ``HelloController`` class to display a form on a ``GET``
request that asks the user for both their name and the language they
would like to be greeted in. It should look something like this:

.. figure:: figures/form.png
   :alt: Greeting Form

   Greeting Form

The resulting form submission should return and display the message,
“Bonjour Chris”.

.. admonition:: Note

   The language is presented in a dropdown, more formally known as a ``select`` element. 
   For more information about the ``select`` element and how it works, read the 
   `MDN documentation <https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select>`__.

When the user submits the form (via a ``POST`` request), they should be
greeted in the selected language. Your new feature should: 

#. Include at least 5 languages, with English being the default. If you don’t speak 5 
   languages yourself, ask your friend 
   `the Internet <http://pocketcultures.com/2008/10/30/say-hello-in-20-languages/>`__.
#. Include a new ``public static`` method, ``CreateMessage``, in the ``HelloController`` 
   that takes a name as well as a language string. Based on the language string, you’ll 
   display the proper greeting.

Bonus Mission
-------------

#. Add some more HTML and inline styles to your returned greeting
   response string so that the displayed message looks a bit nicer.