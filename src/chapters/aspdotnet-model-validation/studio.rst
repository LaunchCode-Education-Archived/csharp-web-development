Studio: Spa User Validation
===========================

We’ll build on the :ref:`User Signup <user-signup-studio>` studio from last
class, adding in model validation.

Getting Started
---------------

Open up your ``SpaDay`` application and checkout the `user-signup-pt2 <https://github.com/LaunchCodeEducation/SpaDay/tree/user-signup-pt2>`__ branch. 

Creating a New ViewModel
------------------------

To get started with adding validation to our application, we need to first make a ViewModel.
After adding a folder for storing our ViewModels, create a new ViewModel for working with form submission called ``AddUserViewModel``.
Add properties for the user's username, password, and email.
Also, add a new property called ``VerifyPassword``.

Add Validation Attributes
-------------------------

Navigate to ``AddUserViewModel``. Add `validation
attributes <https://docs.microsoft.com/en-us/dotnet/api/system.componentmodel.dataannotations?view=netcore-3.1>`__
to ensure these conditions are satisfied:

#.  Username, password, and ``VerifyPassword`` are required.
#.  Username is between 5 and 15 characters.
#.  Email is optional.
#.  If provided, the email has the format of a valid email address.
#.  The password is between 6 and 20 characters.

Remember to add error messages to your attributes!

Refactoring ``UserController``
------------------------------

With our new ViewModel set up and ready, we need to refactor our action methods to make use of ``AddUserViewModel``.
First, pass an instance of ``AddUserViewModel`` to ``User/Add.cshtml`` via our ``Add()`` action method.
Next, to refactor the ``SubmitAddUserForm()`` action method, we need to do the following:

#. Take in the instance of ``AddUserViewModel`` as a parameter.
#. Use ``ModelState.IsValid`` to make sure that the conditions outlined using validation attributes have been met.
#. If ``ModelState.IsValid`` is ``true``, we want to double check that the value of ``Password`` is equal to ``VerifyPassword``.
   If it is, we can create an instance of ``User`` and pass it to the ``User/Index.cshtml`` view.
   If the two passwords do not match, we need to reload the form with an error message displayed.

   .. admonition:: Hint

      We can pass an object and the name of a view to the ``View()`` method by using the following syntax:

      .. sourcecode:: csharp

         return View("ViewName", objectName);

Validating That Passwords Match
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Last studio, we added some validation checks to make sure the password fields match.
Now we have two validation sections: one for the attribute-configured
validation (which checks ``ModelState.IsValid``), and one that checks
that the password fields match. Make sure they work in-sync with each
other to properly return to the form if any of the validation conditions
fail.

.. admonition:: Tip

   You can, in fact, validate that passwords match using attributes by
   taking a slightly different approach than we’ve done here. We
   outline how to do so in the Bonus Mission section.

Refactoring the Views
---------------------

The final step in adding ViewModels and validation to our ``SpaDay`` application is to refactor our views!

In ``User/Index.cshtml``:

#. Make the ``User`` model accessible to the view.
#. Replace instances of ``ViewBag`` with the ``@Model`` syntax.

If we do this correctly, when a form with valid data is submitted, we should still see our personalized greeting!

In ``User/Add.cshtml``:

#. Make ``AddUserViewModel`` accessible to the view.
#. Keep the ``@if`` statement up at the top so if the two passwords don't match, we can see the error message.
#. Replace the inner contents of the form with a properly formatted form field for each property in the ViewModel.
   Each of your form fields should look something like this:

   .. sourcecode:: guess
      :linenos:

      <div class="form-group">
         <label asp-for="PropertyName">PropertyName</label>
         <input asp-for="PropertyName" />
         <span asp-validation-for="PropertyName"></span>
      </div>

   Note when it comes to the password fields you may want to add a ``type`` attribute to the ``<input>`` tag for better data security!

Test, Test, Test!
-----------------

You made a lot of changes! Be sure to thoroughly test them to make sure
everything works as expected.

Bonus Mission
-------------

Let’s set up our application so we can validate that the password fields match using attributes.

#. Add a ``[Compare]`` attribute to the ``Password`` property in ``AddUserViewModel`` to check if the value of ``Password`` is equal to the value of ``VerifyPassword``.

   .. admonition:: Note

      ``[Compare]`` can be used to validate that the values of two properties are equal.
      If the two values are not equal, you can add an optional ``ErrorMessage`` parameter with a helpful message (for example, "Passwords do not match.")
      Here is an example of how this might look:

      .. sourcecode:: csharp

         public string PropertyA { get; set; }

         [Compare("PropertyA", ErrorMessage = "The two properties must match!")]
         public string PropertyB { get; set; }

#. Remove the ``@if`` statement from the top of the ``User/Add.cshtml`` form.
#. In the ``SubmitAddUserForm()`` method in ``UserController``, ``ModelState.IsValid`` checks for if the validation conditions have been met.
   Now that we have added the validation attribute to the ``Password`` property, we can simplify our code so that we are not separately checking the password form fields against each other.