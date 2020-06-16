.. _validating-models:

Validating Models in a Controller
=================================

Validation involves both model and controller components of an MVC application.
After we have defined validation rules using attributes on the model, we must also update the controller to ensure that the rules are checked and appropriate action is taken when validation fails.

Validation Flow
---------------

Before diving into the details of the code, let's consider the logical flow of control for validating data in a request.
Recall our ``POST`` action method from the previous chapter, which used model binding to create new ``Event`` objects from form submissions.

.. sourcecode:: csharp

   [HttpPost]
   [Route("Events/Add")]
   public IActionResult NewEvent(Event newEvent) {
      EventData.add(newEvent);
      return Redirect("/Events");
   }

The flow of this request can be described as follows:

#. Server receives ``POST`` request
#. Server creates ``newEvent`` object using request parameters
#. ``NewEvent()`` is called with ``newEvent``
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

Some modest validation rules for a new ``Event`` object might be:

- The ``name`` field must contain between 3 and 20 characters, and 
- The ``description`` field may be empty, but may contain no more than 500 characters.

With these rules in place, conceptually, the flow of our controller code should look more like the following:

#. Server receives ``POST`` request
#. Server creates ``newEvent`` object using request parameters
#. ``NewEvent()`` is called with ``newEvent``
#. **Controller checks for validation errors in the model object. If errors are found, return the user to the form. Otherwise, proceed.**
#. ``newEvent`` is saved
#. A redirect response is returned, redirecting the user to ``/Events``

Let's look at how we can practically do this within ASP.NET Core MVC.

Handling Validation Errors - Video
----------------------------------

.. TODO: Add video here

.. admonition:: Note

   If you want to verify what code this video starts with, check out the `validation-attributes <https://github.com/LaunchCodeEducation/CodingEventsDemo/tree/validation-attributes>`__ branch.
   If you want to verify what code this video ends with, check out the `handling-errors <https://github.com/LaunchCodeEducation/CodingEventsDemo/tree/handling-errors>`__ branch.

Handling Validation Errors - Text
----------------------------------

When using model binding, we can use tools to validate new model objects before they are saved to a data layer or database. 

Using ``ModelState.IsValid``
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Within ``EventController``, the ``NewEvent()`` action method uses model binding to receive an ``Event`` object that is created using form data.
This object is NOT validated automatically, even if validation attributes are present on its fields.

Recall that *both* the model and controller play a role in validation.
The model's responsibility is simply to define validation rules.
The controller must check that those rules are satisfied.

``ModelState.IsValid`` will check in the constraints on the model properties are met.
If these constraints are met, ``ModelState.IsValid`` equates to true and we want to add the valid ``Event`` object to our list of events.
If these constraints are not met and the object is *not* valid, we want to redirect to the form.  

Check Your Understanding
------------------------

.. admonition:: Question

   Which of the following statements about ``ModelState.IsValid`` are true?

   #. ``ModelState.IsValid`` can only be used in conjunction with model binding.
   #. Using ``ModelState.IsValid`` means that a method will never be called with invalid data.
   #. ASP.NET can infer validation requirements based on the name of a field. 

.. ans: b, @Valid can only be used in conjunction with model binding.
