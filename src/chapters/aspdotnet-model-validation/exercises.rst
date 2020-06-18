Exercises: ViewModels and Model Validation
==========================================

Let’s practice adding more properties to our event objects and 
validating them. Create a new branch from the `display-error-messages branch <https://github.com/LaunchCodeEducation/CodingEventsDemo/tree/display-error-messages>`__. 

Below, we describe some new properties for you to add to the ``Event`` class. 
For each property, consider the following factors:

#. What will you call your property?
#. What type of input should be added to capture the field's information from the user?
#. Refer to the chapter content to find an appropriate attributes to fit the necessary constraints. 
#. What should the error message convey to the user?
#. What, if anything, will you need to update on the controller to account for the new property?

Event information to add:

#. Add a property to collect information about where the event will take place. This property should not be 
   null or blank. 

#. Add a property to collect information about whether an attendee must register for the event or not. For 
   the purposes of validation practice, make this property only able to be marked as true. 

#. Add a property to collect information about the number of attendees for the event. Valid values for this 
   property should be any number over zero.

#. Browse the validation attributes to find one to use on another new property of your choosing.


