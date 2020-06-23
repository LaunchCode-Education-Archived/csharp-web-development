.. _user-signup-studio:

Studio: Spa User Signup
=======================

For this studio you will add functionality to allow users to sign up for your ``SpaDay`` app. 

The starter code has been modified from where you left off last class. Grab the refactored code 
on the `user-signup-starter branch <https://github.com/LaunchCodeEducation/SpaDay/tree/user-signup-starter>`__. 

You'll notice in this branch that the name has been removed from the service selection form. Once we
implement user-signup functionality, we can use a given user's name to identify the spa client. We've also 
moved data into a ``Client`` model and out of the ``SpaController`` class.

In this studio, we'll ask you to write another model, ``User``. ``User`` and ``Client`` may at first 
appear redundant, but in the future as you develop your spa application, you may find a scenario where 
a user is logging in who is not also ``Client``.

Getting Ready
-------------

Within ``SpaDay``, create the following files. 

#. Create a ``UserController`` in ``Controllers``.
#. Create a new folder, ``User``, within ``Views``. 
#. Create ``Index.cshtml`` and ``Add.cshtml`` templates within ``Views/User/``. 
#. Create a ``User`` class within ``Models``.

Creating the Model
------------------

Your ``User`` class should have a few properties: ``Username``, ``Email``, and ``Password``. 

Rendering the Add User Form
---------------------------

#. In the ``UserController``, create an action method ``Add()`` to
   render the form. This action method should correspond to the path
   ``/user/add``, and for now, it can just return the ``Add.cshtml`` view.

   .. admonition:: Tip

      Don't forget to add ``/user/add`` to your path when you test your new features. 

#. Within the ``Add.cshtml`` template, create a form that accepts inputs for
   each of the ``User`` class properties. Include an additional password input field to verify 
   the password input. The form should be set up to ``POST`` to ``/user``. 

#. Be sure to set ``type="password"`` for the password and verify inputs,
   to ensure the passwords are not visible when being typed into the form.
   You can also set ``type="email"`` on the email input, which will enable
   some basic client-side validation. We'll tackle validation in more detail 
   in the next lesson. 

Processing Form Submission
--------------------------

#. Within the ``UserController``, create an action method with this signature:

   .. sourcecode:: csharp

      public IActionResult SubmitAddUserForm(User newUser, string verify) {
         // add form submission handling code here
      }

   This will use model binding to create a new user object, ``newUser``, and
   pass it into your action method. 

   .. admonition :: Note
   
      You don’t need to store the ``User`` object anywhere for this studio.
      We’re focusing on form handling and validation in this exercise. If you
      want to keep track of users using the method we employed in the models
      lesson video, check out the Bonus Missions below.

#. Check that the ``verify`` parameter matches the
   password within the ``newUser`` object.
   
   a. If it does, store the user's name in a ``ViewBag`` property and render the ``User/Index.cshtml`` view by returning ``View("Index")``.
   b. If the passwords don’t match, render the form again.

Refining Form Submission
------------------------

#. Once registered, we want the user to access the form selecting their spa services and see a personalized welcome message!

   a. In ``User/Index.cshtml``, add an ``h1`` element with a welcome message. Use the ``ViewBag`` property containing the user's name to personalize the message!
   b. Also in ``User/Index.cshtml``, add an ``a`` element to take the user back to the path, ``/spa``, where the ``Spa/Index.cshtml`` template will be rendered.

#. If the form is re-rendered when a password is not verified, we should let the user know that their form
   was not properly submitted. Add an ``error`` property to ``ViewBag`` letting the user know 
   that their passwords should match. This property will need to correspond to an element in the template that will only render the error text when the passwords do not match.

#. If we send a user back to re-populate the form, it would be nice to not clear their previous 
   submission. We won't need to save the password entries in this fashion.
   
   a. In the form submission action method, add the ``username`` and ``email`` fields of the submitted user as 
      ``ViewBag`` properties. 
   
   b. Back in the form, add a value attribute to these form fields and make them equal to the
      ``ViewBag`` properties. 

Bonus Missions
--------------

#. Add a ``Date`` property in ``User``, and initialize it to the time the
   user joined (i.e. when the ``User`` object was created).
#. At the bottom of ``User/Index.cshtml``, add a ``div``.
   Inside that element, add account details such as the user's email and the date they joined.
