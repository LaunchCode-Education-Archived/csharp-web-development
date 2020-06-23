.. index:: ! ViewModel

ViewModels and Passing Data To and From Views
=============================================

Now that we have an understanding for what a model is, we can focus on how to effectively pass information between the three elements of MVC applications.
With our current MVC application, we can add new events and remove events.
However, our application is also susceptible to run-time errors.
Our view can accept any type of input and if we mistype something in our view, we can run into issues later down the line.

A **ViewModel** is a model class designed specifically to be used in a view.
By utilizing ViewModels in our application, we can make our views strongly-typed and add validation to forms to prevent bad user input.
Also, if we have information we want to collect as part of a form, but not save as part of a model, we can store that data as a property of a ViewModel.
An example of this would be if we have a form for users to create an account on our site.
The form includes two fields: one for the password and one for confirming the new user's password.
While we only want to save the password and may only have a ``Password`` property in our model, we can add a ``ConfirmPassword`` property to the ViewModel so we can check that the two match before saving the user's info.
These benefits of ViewModels will help reduce potential errors in our application.

Refactoring the View and Controller to Use a Model in a View - Video
--------------------------------------------------------------------

.. youtube::
   :video_id: _lUUT1oDE-U

.. admonition:: Note

   If you want to verify what code this video starts with, check out the `model-binding <https://github.com/LaunchCodeEducation/CodingEventsDemo/tree/model-binding>`__ branch.
   If you want to verify what code this video ends with, check out the `models-in-views <https://github.com/LaunchCodeEducation/CodingEventsDemo/tree/models-in-views>`__ branch.

Refactoring the View and Controller to Use a Model in a View - Text
-------------------------------------------------------------------

To start with understanding why we may want to use a ViewModel, let's refactor our code to use a model directly in our view.

First, in ``EventsController``, we want to convert the collection of Events we have been holding into a list.

.. sourcecode:: csharp
   :lineno-start: 19

   List<Event> events = new List<Event>(EventData.GetAll());

Now that we are storing our items in a ``List``, we need to import the model into our ``Events/Index.cshtml`` view so we can use the new ``events`` collection.
We can add a small statement up on line 1 to do so: 

.. sourcecode:: csharp

   @model List<CodingEventsDemo.Models.Event>

Or, as we write in the video:

.. sourcecode:: csharp
   :linenos:

   @using CodingEventsDemo.Models

   @model List<Event>

Wherever we used our ``ViewBag`` property, we can now use ``Model`` syntax.
Once the view has been updated, run the application!

This was merely a refactor so the functionality of the app hasn't changed, but we have eliminated some of the possibility of bugs in our code being discovered at runtime!
Using a model in a view like this makes our view *strongly-typed*.
Before if we misspelled a property of ``Event`` or ``ViewBag``, those errors would have been caught at run-time and possibly interfered with users' experience. 
With a strongly-typed view, the same errors would be caught at compile-time before users see the application.
Strongly-typed views also support intellisense, so as we work with properties of a model, we can make sure we have the correct property name.

Adding a ViewModel - Video
--------------------------

.. youtube::
   :video_id: XAPP0VTiwk8

.. admonition:: Note

   If you want to verify what code this video starts with, check out the `models-in-views <https://github.com/LaunchCodeEducation/CodingEventsDemo/tree/models-in-views>`__ branch.
   If you want to verify what code this video ends with, check out the `adding-viewmodels <https://github.com/LaunchCodeEducation/CodingEventsDemo/tree/adding-viewmodels>`__ branch.

Adding a ViewModel - Text
-------------------------

Now that we have refactored our ``Events/Index.cshtml`` view and ``EventsController`` to use a model, let's investigate how to create a ViewModel.
We can do so by following these steps:

#. Add a ``ViewModels`` directory at the top level of the project.
#. Add a new class to the ``ViewModels`` directory and name it ``AddEventViewModel``.
#. Add ``Name`` and ``Description`` properties to the new class.

   .. admonition:: Note

      For now, your ViewModel does not need a constructor!

#. In the ``Add()`` action method responsible for retrieving the form to add events, in ``EventsController``, create a new instance of ``AddEventViewModel`` called ``addEventViewModel`` and add it to the ``View()``.
#. Import the ViewModel to the ``Add.cshtml`` view with the ``@model`` syntax.
#. Add ``asp-controller = Events`` and ``asp-action = NewEvent`` to the ``<form>`` tag to designate which method the form data should be sent to.
#. Add ``asp-for`` to ``<label>`` and ``<input>`` tags. This allows us to specify which form field corresponds to which property in our ViewModel.
#. Refactor the ``NewEvent()`` action method to be named ``Add()``. Have it also now use the ViewModel as its parameter. Set values of a new ``Event`` object using the values of the properties stored in the instance of the ``AddEventViewModel``.
#. Add the new ``Event`` object to ``EventData`` and make sure that the method still returns a ``Redirect`` to ``/Events``.
#. Run your application.

Following these steps, we effectively refactored our application to use a ViewModel.
While the functionality of the application remains the same, we are now in a position to easily add validation to our application.

Check Your Understanding
------------------------

.. admonition:: Question

   **True or False** ViewModels are views designed to specifically be used in models.

.. ans: False, ViewModels are models designed to be used in views!