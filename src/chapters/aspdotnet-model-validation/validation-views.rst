Validation and Views
====================

While our application is properly handing errors, we need to display the error messages so that the users know what information they should be adding.

Displaying Error Messages in our View - Video
---------------------------------------------

.. youtube::
   :video_id: 3twcm6Smpkg

.. admonition:: Note

   If you want to verify what code this video starts with, check out the `handling-errors <https://github.com/LaunchCodeEducation/CodingEventsDemo/tree/handling-errors>`__ branch.
   If you want to verify what code this video ends with, check out the `display-error-messages <https://github.com/LaunchCodeEducation/CodingEventsDemo/tree/display-error-messages>`__ branch.


Displaying Error Messages in our View - Text
--------------------------------------------

Create a separate ``span`` element in the form.
In the ``<span>`` tag, we can add ``asp-validation-for`` to specify which property's validation error messages should be displayed if the conditions are not met.

.. admonition:: Note

   We don't have to add anything else to display error messages, because that validation is already built in!

Now when we run our application and enter a bad event name or forget our description, we get the error message displaying what we should be entering!

.. admonition:: Warning

   In the video, we note that the ``<span>`` element will only be materialized if the validation fails. This isn't true. The ``<span>`` element
	to contain the error message is always created, it just doesn't contain any text if the validation rule it met.

Check Your Understanding
------------------------

.. admonition:: Question

   **True or False** In order to implement validation, all three elements of MVC applications are involved.

.. ans: true!
