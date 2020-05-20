Razor Forms
===========

Already we have seen that templates allow us to build generic forms.
Using templates, you can reuse the structure by rendering the same form, but with different labels and data.
Thus, a single form can serve different purposes, saving you extra effort.

Whenever possible, reuse existing templates!

Start a New Project
-------------------

You will build a new project so you can practice with templates and forms.
If you have not done so, commit and push any unsaved work from your ``HelloASPDotNET`` project.

Your new project will keep track of some coding events, such as meetups and conferences.
To get started, follow the :ref:`steps <initialize-aspdotnet-project>` you took to create ``HelloASPDotNET``, but call the project ``CodingEvents``.

CodingEvents Setup - Video
--------------------------

.. TODO: Add video

.. admonition:: Note

   The final code presented in this video is found on the `views-setup branch <https://github.com/LaunchCodeEducation/CodingEventsDemo/tree/views-setup>`__ of the ``CodingEventsDemo`` repository.

CodingEvents Setup - Text
-------------------------

#. In the ``Controllers`` directory, create a new controller named ``EventsController``.
#. In the new controller, create an action method for ``GET`` requests. 
#. Within the action method, create an empty list and add a few event names to it.
#. Add the list to ``ViewBag``. Then return the corresponding view.
#. Within the ``Views`` directory, create a new directory named ``Events``. Within this directory, create a new view named ``Index.cshtml``.
#. Within the new template, loop over the list and display the name of each event.

Create and Render a Form - Video
--------------------------------

.. TODO: Add video

.. admonition:: Note

   The starter code presented in this video is found on the `views-setup branch <https://github.com/LaunchCodeEducation/CodingEventsDemo/tree/views-setup>`__ of the ``CodingEventsDemo`` repository.
   The final code presented in this video is found on the `render-form branch <https://github.com/LaunchCodeEducation/CodingEventsDemo/tree/render-form>`__ of the ``CodingEventsDemo`` repository.

Create and Render a Form - Text
-------------------------------

A Razor form can be made simply with a template that includes a ``<form>`` element.
The method for the form should be of type ``post``. 
If you need the form to post at a different route, you could also add an ``action`` attribute to the ``<form>`` tag.

.. sourcecode:: html
   :linenos:

   <!-- Other HTML -->

   <form method="post">
      <input type="text" name="inputName">
      <input type="submit" value="submitButtonText">
   </form>

   <!-- Other HTML -->

You can include as many inputs as you need in the form, and these can be of
different types (e.g. text, email, checkbox, etc.). However, each different
piece of data you want to collect needs to have a unique ``name`` attribute.

To *render* the form in the view, add a method to the controller with an ``[HttpGet]`` annotation:

.. sourcecode:: csharp
   :lineno-start: 26

   [HttpGet]
   public IActionResult Add()
   {
      // Any additional method code here

      return View();
   }

Add a Form Handler Method - Video
---------------------------------

Now that you have created and rendered a form in your ``CodingEvents``
project, you need to add a method to the controller to *handle* its submission.
Code along with the video below to add this functionality.

.. TODO: Add video

As usual, the following summary outlines the ideas from the clip.

Add a Form Handler Method - Text
--------------------------------

To *process* a form after the user clicks the *Submit* button, you need to add
a method to the controller using the ``[HttpPost]`` annotation:

.. sourcecode:: csharp
   :lineno-start: 31

   [HttpPost]
   [Route("/events")]
   public IActionResult AddEvent(string name)
   {
      // Method code...

      return View();
   }

Some points to note:

#. Line 2: For each piece of data that needs to be retrieved from the form,
   declare a parameter of the appropriate type.
#. The method code performs any data manipulation required after the
   information gets submitted.
#. Line 6: We may want to send the user to a different page after they
   successfully submit a form. Instead of re-rendering the form, we want
   to use ``Redirect()`` to *redirect* the user to a different template.

