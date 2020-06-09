ViewModels and Passing Data To and From Views
=============================================

Now that we have an understanding for what a model is, we can focus on how to effectively pass information between the three elements of MVC applications.
With our current MVC application, we can add new events and remove events.
However, our application is also susceptible to run-time errors.
Our view can accept any type of input and if we mistype something in our view, we can run into issues later down the line.

A **ViewModel** is a model class designed specifically to be used in a view.
By utilizing ViewModels in our application, we can make our views strongly-typed and add validation to forms to prevent bad user input.
These benefits of ViewModels will help reduce potential errors in our application.

Refactoring the View and Controller to Use a Model in a View - Video
--------------------------------------------------------------------

.. TODO: Add video covering an intro about how to use a model in a view

.. starting branch: model-binding
.. ending branch: models-in-views

Refactoring the View and Controller to Use a Model in a View - Text
-------------------------------------------------------------------

To start with understanding why we may want to use a viewmodel, let's refactor our code to use a model directly in our view.

First, we want to convert the collection of Events we have been holding into a list.

.. sourcecode:: csharp

   List<Event> events = new List<Event>(EventData.GetAll());

Pass the events object into the view!
Now that we are storing our items in a List, we need to import the model into our view so we can use the new ``events`` collection.
We can add a small statement up on line 1 to do so: ``@model List<CodingEventsDemo.Models.Event>``
After refactoring the view so it uses the the appropriate list.
Update the necessary points of data with ``Model`` syntax and run the application!

This was merely a refactor so the functionality of the app hasn't changed, but we have eliminated the possibility of bugs in our code being discovered at runtime!

Adding a ViewModel - Video
--------------------------

.. TODO: Add video here!

.. starting branch: models-in-views
.. ending branch: adding-viewmodels

Adding a ViewModel - Text
-------------------------

* Add a ViewModels directory at the top level of the project
* Name the new class ``AddEventViewModel``.
* Add name and description properties
* Add new instance of viewmodel to get action method called ``addEventViewModel`` and add it to ``View()``.
* Pass in ViewModel to view, ``Add.cshtml``.
* Add asp-controller and asp-action to form
* Add asp-for to label and input tags
* Refactor post method to use viewmodel. Set values to newEvent object.
* Run!

Check Your Understanding
------------------------

.. admonition:: Question

   ViewModels are views designed to specifically be used in models.

.. ans: False, ViewModels are models!