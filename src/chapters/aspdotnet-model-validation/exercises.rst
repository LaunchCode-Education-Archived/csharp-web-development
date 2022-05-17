.. _model-validation-exercises:

Exercises: ViewModels and Model Validation
==========================================

Let’s practice adding more properties to our event objects and 
validating them. Create a new branch from the `display-error-messages branch <https://github.com/LaunchCodeEducation/CodingEventsDemo/tree/display-error-messages>`__. 

Below, we describe some new properties for you to add to the ``Event`` class. 
For each property, consider the following factors:

#. What will you call your property?
#. What type of input should be added to capture the field's information from the user?
#. Refer to the chapter content to find appropriate attributes to fit the necessary constraints. 
#. What should the error message convey to the user?
#. What, if anything, will you need to update on the controller to account for the new property?

Event information to add:

#. Add a property to collect information about where the event will take place. This property should not be 
   null or blank. 

   :ref:`Check your solutions<mv-ex-1>`

#. Add a property to collect information about the number of attendees for the event. Valid values for this 
   property should be any number between zero and 100,000.

#. Add columns for the location and number of attendees to the ``Events/Index.cshtml`` view.

   :ref:`Check your solutions<mv-ex-3>`

Bonus Mission
-------------

Add a property to collect information about whether an attendee must register for the event or not.
For the purposes of validation practice, make this property only able to be marked as true. 

.. admonition:: Hint

   In order to do this, you need to add an additional property called ``IsTrue`` to ``AddEventViewModel`` with the following code:

   .. sourcecode:: csharp

      public bool IsTrue { get { return true; } }

   With ``IsTrue`` in ``AddEventViewModel``, you can use a ``[Compare]`` attribute to compare the value of the ``IsTrue`` property which is always ``true`` and the value of the property you add for registration requirements.
   The `documentation <https://docs.microsoft.com/en-us/dotnet/api/system.componentmodel.dataannotations.compareattribute?view=netcore-3.1>`__ has more information on how the ``[Compare]`` attribute.

