Registrations and Logins
========================

In order for users to successfully navigate through the application, Identity will handle a number of functions related to both authentication and authorization.
For the purposes of this book, we will focus on just two: registering for a new account and logging in.

.. admonition:: Note

   Razor Class Libraries do not have separate controllers like in the traditional MVC design pattern.
   The logic that we might be inclined to put in a controller for each of the actions that we look at is actually contained within a Razor page.
   Our goal is to locate the correct page and understand what is going on.

   The pages we are looking at end with the file extension ``.cshtml.cs``.
   Some Mac users may have to click on a small arrow on to expand the ``.cshtml`` pages to find the ``cshtml.cs`` files.  

Registration
------------

Open up ``Register.cshtml.cs`` in ``Areas/Identity/Pages/Account`` and inspect it.
Here are some things to note:

#. The return type of the action to register a new user is ``Task<IActionResult>``.
   We have encountered ``IActionResult`` before.
   ``Task<IActionResult>`` is an asynchronous return type.
   The action of adding a new user to a database is asynchronous so our function must return an asynchronous action.
#. We can still use ``ModelState.IsValid`` to make sure that the user's input matches our validation requirements.
#. ``UserManager`` comes back into play here for the addition of the new user to the database.
   The method used for that action is called ``CreateAsync()``. The new user's password is hashed as part of this method, so there aren't any additional method calls here.
#. If the new user row in the database is successfully created, then we want to direct the user to a page to start working.
   If not, the user registration form is reloaded, just as when the validation requirements are not met.

Login
-----

Open up ``Login.cshtml.cs`` in ``Areas/Identity/Pages/Account``.
Here are some things to note:

#. ``Task<IActionResult>`` is back meaning the action of signing in is asynchronous.
#. If the form input is valid, then we want to try and sign in the user.
#. ``SignInManager`` has a method called ``PasswordSignInAsync()`` which takes in parameters like the inputted email and password and compares those values to the values stored in the database.
#. If the action of signing in is successful, the user is directed on to a new page.
   If the action is not successful, then the user is redirected back to the login form with an error message explaining that they could not log in.

Logout
------

There are two main things to note about ``Logout.cshtml.cs`` in ``Areas/Identity/Pages/Account``:

#. ``Task<IActionResult>`` is the return type.
#. ``SignInManager`` has a method called ``SignOutAsync()`` which ends the session. Once that action is completed, the user is redirected to an unrestricted page.

These are the three main actions we want to focus on when it comes to authentication with user accounts.
We could additional elements to these three actions such as 2FA or two factor authentication on log in as the authentication requirements of our project grow.
