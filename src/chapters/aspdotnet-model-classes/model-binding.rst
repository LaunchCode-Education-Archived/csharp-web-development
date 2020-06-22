Model-Binding
=============

.. index:: ! model binding

We now introduce a useful technique to auto-create model instances, 
called **model binding**. Model binding takes place when a whole 
model object is created by the ASP.NET framework on form submission. This saves us the effort, 
and the code, needed to pass in each form field to a controller. 

Model binding reduces the amount of code we need to 
write to create an object and helps with validation (which we’ll explore further in the next
section). With a few modifications to our project, ASP.NET creates an ``Event`` object for us when 
the *New Event* form is posted.

How to Use Model-Binding - Video
--------------------------------

.. youtube::
   :video_id: vvfPmxLeinU

.. admonition:: Note

   The starter code for this video is found at the `delete-events branch <https://github.com/LaunchCodeEducation/CodingEventsDemo/tree/delete-events>`__
   of ``CodingEventsDemo``. The final code presented in this 
   video is found on the `model-binding branch <https://github.com/LaunchCodeEducation/CodingEventsDemo/tree/model-binding>`__.
   As always, code along to the videos on your own ``CodingEvents`` project.

How to Use Model-Binding - Text
-------------------------------

When submitting new event information, rather than passing in each field used to 
instantiate a model, we can instead pass in ``Event newEvent`` as a parameter 
of the controller method. 

Revised ``NewEvent`` method in ``EventsController``:

.. sourcecode:: c#
   :lineno-start: 29

   [HttpPost]
   [Route("Events/Add")]
   public IActionResult NewEvent(Event newEvent)
   {
      EventData.Add(newEvent);

      return Redirect("/Events");
   }

This is the essence of model binding. The model instance is created
on form submission. With only two fields needed to create an event, the value of this data binding may not be
particularly apparent right now. You can imagine, though, with a larger form and class, that the practice of 
model binding is pretty potent.

For binding to take place, we must use the model field names as the form field names. So back in 
the create form HTML, we update the form fields to match the event fields. 

``Views/Events/Add.cshtml``:

.. sourcecode:: html
   :lineno-start: 4

   <div class="form-group">
      <label>
         Name
         <input type="text" name="name" class="form-control">
      </label>
      <label>
         Description
         <input type="text" name="description" class="form-control">
      </label>
    </div>  

If a form field name does NOT match up with a model field, then binding will fail for that piece of data. 
It is critically important to ensure these names match up. 

.. index:: ! [FromForm]

.. admonition:: Tip

   The basics of model binding require that model property names match form field names. If they don't, 
   you still have the option to bind the model with attributes. We could have left the description
   field in the *Add Event* form with ``name="desc"``. Then back in the ``Event`` class, we could modify the 
   description property as such:

   .. sourcecode:: c#
      :lineno-start: 10

      [FromForm(Name="desc")]	
      public string Description { get; set; }


The changes above only scratch the surface of what can be done with model binding.
We address more aspects and advantages of this technique in the coming pages If you'd 
like to read more on the topic now, take a look at the `documentation <https://docs.microsoft.com/en-us/aspnet/core/mvc/models/model-binding?view=aspnetcore-3.1>`__.



Check Your Understanding
------------------------

.. admonition:: Question

   Complete this sentence: Model binding ...
   *Check all that apply*

   #. requires the use of attributes.
   #. helps with form validation.
   #. reduces controller code.
   #. makes your code more rigid and vulnerable to errors.

.. ans: b + c, helps with form validation, reduces controller code.

.. admonition:: Question

   In ``CodingEvents``, we add an additional property, ``NumberOfAttendees``, to the ``Event`` class. What other change must we make to ensure the user of our 
   application can determine this value? (Assume we are using model binding to process form submission.) 

   #. Pass in a ``numberOfAttendees`` parameter to the form submission handler.
   #. Add another input element to the create event form with a ``name="numberOfAttendees"`` attribute.
   #. Add a ``getAttendees`` method to ``EventData``.
   #. All of the above. 

.. ans: b, Add another input element to the create event form with a ``name="numberOfAttendees"`` attribute.
