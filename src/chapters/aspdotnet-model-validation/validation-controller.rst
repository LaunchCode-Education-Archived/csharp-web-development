.. _validating-models:

Validating Models in a Controller
=================================

Validation involves both model and controller components of an MVC application.
After we have defined validation rules using attributes on the model, we must also update the controller to ensure that the rules are 
checked and appropriate action is taken when validation fails.

Validation Flow
---------------

Before diving into the details of the code, let's consider the logical flow of control for validating data in a request.
Let's check out our ``POST`` action method for processing the *Add Event* form. Remember that this method uses model binding to create new ``Event`` 
objects from form submissions.

.. sourcecode:: csharp
   :lineno-start: 32

   [HttpPost]
   public IActionResult Add(AddEventViewModel addEventViewModel)
   {
      Event newEvent = new Event
      {
         Name = addEventViewModel.Name,
         Description = addEventViewModel.Description,
         ContactEmail = addEventViewModel.ContactEmail
      };

      EventData.Add(newEvent);

      return Redirect("/Events");
   }

The flow of this request can be described as follows:

#. Server receives ``POST`` request
#. Server creates ``newEvent`` object using request parameters
#. ``Add()`` is called with ``newEvent``
#. ``newEvent`` is saved
#. A redirect response is returned, redirecting the user to ``/Events``

The request creates an ``Event`` object using data from the incoming request.
Regardless of what the data looks like, the new object is saved to the data layer.
The user could submit an empty form, with no name or description filled in, and our code would be happy to create an ``Event`` and save it.
Similarly, a user could submit the full text of the massive novel "War and Peace" as the description.
This isn't great. 

.. admonition:: Note

   Technically, submitting a request containing "War and Peace" would fail with most applications.
   This is because web servers typically set a limit on the maximum size of a ``POST`` request.
   However, our application code is willing to take requests of any size, at this point.

Now that we have created ``AddEventViewModel`` and added validation attributes, we want to refactor our controller to use the ViewModel and handle errors in form submission.
Instead of using model binding to create a new ``Event`` object, we will use model binding to create a new ``AddEventViewModel`` object called ``addEventViewModel``.
Our modest validation rules for a new ``AddEventViewModel`` object are as follows:

- The ``Name`` property must contain between 3 and 50 characters, 
- The ``Description`` property may contain no more than 500 characters, and 
- The ``ContactEmail`` property must satisfy email formatting rules.

With these rules in place, conceptually, the flow of our controller code should look more like the following:

#. Server receives ``POST`` request
#. Server creates ``addEventViewModel`` object using request parameters
#. ``Add()`` (``POST`` request type) is called with ``addEventViewModel``
#. **Controller checks for validation errors in the ViewModel object. If errors are found, return the user to the form. Otherwise, proceed.**
#. ``addEventViewModel`` is used to create a new ``Event`` object called ``newEvent``, which is saved to the data store.
#. A redirect response is returned, redirecting the user to ``/Events``

Let's look at how we can practically do this within ASP.NET Core MVC.

Handling Validation Errors - Video
----------------------------------

.. youtube::
   :video_id: n1KMXzDzvuU

.. admonition:: Note

   If you want to verify what code this video starts with, check out the `validation-attributes <https://github.com/LaunchCodeEducation/CodingEventsDemo/tree/validation-attributes>`__ branch.
   If you want to verify what code this video ends with, check out the `handling-errors <https://github.com/LaunchCodeEducation/CodingEventsDemo/tree/handling-errors>`__ branch.

   Actually, the first 4 minutes of the video above cover some of the code changes to get the project to the starting state of the ``validation-attributes`` branch.


Handling Validation Errors - Text
---------------------------------

When using model binding, we can use tools to validate new model objects before they are saved to a data layer or database. 

Using ``ModelState.IsValid``
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Within ``EventController``, the ``Add()`` action method uses model binding to receive an ``AddEventViewModel`` object when the form is posted. 
That ViewModel instance is created using form data.
This object is NOT validated automatically, even if validation attributes are present on its fields.

Recall that *both* the model and controller play a role in validation.
The model's responsibility is simply to define validation rules.
The controller must check that those rules are satisfied.

``ModelState.IsValid`` will check if the constraints on the model properties are met.
If these constraints are met, ``ModelState.IsValid`` equates to true and we want to create and add an ``Event`` object to our list of events.
If these constraints are not met and the ViewModel object is *not* valid, we want to redirect the user back to the *Add Event* form.  

Once we are done refactoring the ``Add()`` action method to use ``ModelState.IsValid``, our action method will look like the code below. 

.. sourcecode:: csharp
   :lineno-start: 32

   [HttpPost]
   public IActionResult Add(AddEventViewModel addEventViewModel)
   {
      if (ModelState.IsValid)
      {
         Event newEvent = new Event
         {
            Name = addEventViewModel.Name,
            Description = addEventViewModel.Description,
            ContactEmail = addEventViewModel.ContactEmail
         };

         EventData.Add(newEvent);

         return Redirect("/Events");
      }

      return View(addEventViewModel);
   }

Now we have refactored our action method to handle any errors in form submission.
However, if you submit a value that doesn't meet our conditions, you won't see any error messages indicating what was wrong with your submission.
Let's tackle that next!

Check Your Understanding
------------------------

.. admonition:: Question

   Which of the following statements about ``ModelState.IsValid`` are true?

   #. ``ModelState.IsValid`` can only be used in conjunction with model binding.
   #. Using ``ModelState.IsValid`` means that a method will never be called with invalid data.
   #. ASP.NET can infer validation requirements based on the name of a field. 

.. ans: a, ModelState.IsValid can only be used in conjunction with model binding.
