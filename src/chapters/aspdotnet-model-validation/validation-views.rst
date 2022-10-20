Validation and Views
====================

While our application is properly handing errors, 
we need to display the error messages so that the users know what 
information they should be adding.  
Client-side validation like this can prevent faulty data submissions.

Since the filming of this video, ASP.NET requires a different method
for changing the color of error messages.  
Instructions for working with ``field-validation-valid`` have been updated below.

Displaying Error Messages in our View - Video
---------------------------------------------

.. youtube::
   :video_id: 3twcm6Smpkg

.. admonition:: Note

   If you want to verify what code this video starts with, check out the `handling-errors <https://github.com/LaunchCodeEducation/CodingEventsDemo/tree/handling-errors>`__ branch.
   If you want to verify what code this video ends with, check out the `display-error-messages <https://github.com/LaunchCodeEducation/CodingEventsDemo/tree/display-error-messages>`__ branch.


Displaying Error Messages in our View - Text
--------------------------------------------

Create a separate span element in the form. 
In the ``<span>`` tag, we can add asp-validation-for to specify which property’s 
validation error messages should be displayed if the conditions are not met.

.. admonition:: Note

   We don’t have to add anything else to display error messages, 
   because that validation is already built in!

Now when we run our application and enter a bad event name or forget our description, 
we get the error message displaying what we should be entering!

.. admonition:: Warning

   In the video, we note that the <span> element will only be materialized if the validation fails. This isn’t true. The <span> element
   to contain the error message is always created, it just doesn’t contain any text if the validation rule it met.


Changing the Color of Error Messages
------------------------------------

Adding to the project's ``site.css`` will not change the color of your error messages.
We need to add more code to the project.

One way to do this is by using **unobtrusive validation** methods, such as using a third-party library.

The `jQuery Unobtrusive Validation <https://github.com/aspnet/jquery-validation-unobtrusive>`_ library.
contains scripts that will perform validation tasks, such as updating the color of error messages.
To utilize this library, we need to point to it in our ``_Layout.cshtml`` page and then 
add more attributes to our Views.

``_Layout.cshtml`` Updates
^^^^^^^^^^^^^^^^^^^^^^^^^^^

To utilize the library, we need to add the following references to it within the 
``<main>`` area.

.. sourcecode:: html

   <main>
      @RenderBody()
      <script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.6.0/jquery.js"></script>
      <script src="https://cdnjs.cloudflare.com/ajax/libs/jquery-validate/1.19.3/jquery.validate.js"></script>
      <script src="https://cdnjs.cloudflare.com/ajax/libs/jquery-validation-unobtrusive/3.2.12/jquery.validate.unobtrusive.js"></script>
   </main>


In the ``Add`` View, you will need to add more ``class`` attributes for the library to target.

.. sourcecode:: html
   :lineno-start: 8

    <div asp-controller="Events" asp-action="Add" class="form-group">
        <label asp-for="Name"></label>
        <input asp-for="Name" class="form-control"/>
        <span asp-validation-for="Name" class="text-danger"></span>
    </div>

Note in line 10 the addition of ``class="form-control"`` and in line 11 ``class="text-danger"``.
These attributes will be noted by the jQuery Unobtrusive Validation library and print our red
if the client does not meet the requirements.

You can read morea about client-side validation 
and the jQuery Unobtrusive Validation library `here <https://learn.microsoft.com/en-us/aspnet/core/mvc/models/validation?view=aspnetcore-6.0#client-side-validation>`_.
That is were we found the syntax for this portion of the project.

Check Your Understanding
------------------------

.. admonition:: Question

   **True or False** In order to implement validation, all three elements of MVC applications are involved.

.. ans: true!
