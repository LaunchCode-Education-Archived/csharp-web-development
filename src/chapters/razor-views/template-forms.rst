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

.. youtube::
   :video_id: 30uNDl80lIc

.. admonition:: Note

   The final code presented in this video is found on the `views-setup branch <https://github.com/LaunchCodeEducation/CodingEventsDemo/tree/views-setup>`__ of the ``CodingEventsDemo`` repository.

.. admonition:: Tip

	**Windows Users**: You might need to change some solution settings if you pull down this demo repository and run it on your computer.
	Refer to :ref:`vs-troubleshooting` for help.

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

.. youtube::
   :video_id: rdEsTOYhM_E

.. admonition:: Note

   The starter code presented in this video is found on the `views-setup branch <https://github.com/LaunchCodeEducation/CodingEventsDemo/tree/views-setup>`__ of the ``CodingEventsDemo`` repository.
   The final code presented in this video is found on the `render-form branch <https://github.com/LaunchCodeEducation/CodingEventsDemo/tree/render-form>`__ of the ``CodingEventsDemo`` repository.

Create and Render a Form - Text
-------------------------------

A Razor form can be made simply with a template that includes a ``<form>`` element.
The method for the form should be of type ``post``. 

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

.. admonition:: Note

   If the ``action`` attribute in the ``<form>`` tag leads to the same route as the form is being rendered at, you do not have to include an ``action`` attribute.

Handle Form Submission - Video
------------------------------

Now that you have created and rendered a form in your ``CodingEvents``
project, you need to add a method to the controller to *handle* its submission.
Code along with the video below to add this functionality.

.. youtube::
   :video_id: ElaXOEpFQZQ

As usual, the following summary outlines the ideas from the clip.

.. admonition:: Note

   The starter code presented in this video is found on the `render-form branch <https://github.com/LaunchCodeEducation/CodingEventsDemo/tree/render-form>`__ of the ``CodingEventsDemo`` repository.
   The final code presented in this video is found on the `handle-form-submission branch <https://github.com/LaunchCodeEducation/CodingEventsDemo/tree/handle-form-submission>`__ of the ``CodingEventsDemo`` repository.


Handle Form Submission - Text
-----------------------------

To *process* a form after the user clicks the *Submit* button, you need to add
a method to the controller using the ``[HttpPost]`` annotation:

.. sourcecode:: csharp
   :lineno-start: 31

   [HttpPost]
   [Route("/Events/Add")]
   public IActionResult NewEvent(string name)
   {
      // Method code...

      return Redirect("/Events");
   }

Some points to note:

#. Line 2: For each piece of data that needs to be retrieved from the form,
   declare a parameter of the appropriate type.
#. The method code performs any data manipulation required after the
   information gets submitted.
#. Line 6: We may want to send the user to a different page after they
   successfully submit a form. Instead of re-rendering the form, we want
   to use ``Redirect()`` to *redirect* the user to a different template.

Now that we have a form and can handle the form submission, we want to create a link to the form to add an event in our ``Index`` template.
This way, after reviewing the list of events, users can click on the link to the form and add an event.
To do this, we use anchor tag helpers. If we put in the following line in our template:

.. sourcecode:: html

   <a asp-controller="Events" asp-action="Add">Add Event</a>

Then when we build our application, the generated HTML of the page will look like:

.. sourcecode:: html

   <a href="/Events/Add">Add Event</a>

Users can now click on the link on our page at ``localhost:5001/Events`` and are directed to the form to add an event.
Once they hit the button to submit the form, the data is passed to the ``NewEvent()`` method, the user's event is added to the ``Events`` list, and the application redirects back to ``localhost:5001/Events`` where an updated ``Events`` list is displayed.
