Validation Attributes
=====================

Within the ViewModel or model of a C# web application, we can define validation rules using attributes.
Validation attributes can be applied to model fields. 

.. index::
   single: validation, annotations

.. index:: ! [Required], ! [EmailAddress], ! [Range], ! [StringLength]

Common Attributes
------------------

We'll use only a few of these attributes, but you can find a full list in the `documentation <https://docs.microsoft.com/en-us/aspnet/core/mvc/models/validation?view=aspnetcore-3.1#built-in-attributes>`_.

.. list-table:: Common Validation Attributes
   :header-rows: 1

   * - Annotation
     - Description
     - Syntax
   * - ``[Required]``
     - Specifies that a field cannot be null
     - ``[Required]``
   * - ``[Range]``
     - Specifies the range of potential values of a numeric field.
     - ``[Range(0,100)]``
   * - ``[StringLength]``
     - Specifies the maximum length of a string field. Has additional optional parameters to specify the minimum length of a string field.
     - ``[StringLength(100)]``
   * - ``[EmailAddress]``
     - Specifies that a string field should conform to email formatting standards.
     - ``[EmailAddress]``


.. admonition:: Example

   To apply the validation rules of the :ref:`example on the previous page <validation-example>` to the fields of an ``AddUserViewModel`` class, we can use ``[StringLength]`` and ``[Required]``.

   .. sourcecode:: csharp
      :linenos:

      [Required]
      [StringLength(12, MinimumLength = 3)]
      public string Username { get; set; }

      [Reguired]
      [StringLength(20, MinimumLength=6)]
      public string Password { get; set; }

Defining Validation Messages
----------------------------

.. _validation-messages:

.. index::
   single: validation, message

Each of these attributes takes an optional ``ErrorMessage`` parameter that allows you to define a user-friendly description to be used when validation fails.

.. admonition:: Example

   .. sourcecode:: csharp
      :linenos:

      [Required(ErrorMessage = "Username is required")]
      [StringLength(12, MinimumLength = 3, ErrorMessage = "Username must be between 3 and 12 characters long")]
      public string Username { get; set; }

      [Required(ErrorMessage = "Password is required")]
      [StringLength(20, MinimumLength = 6, ErrorMessage = "Sorry, but the given password is too short. Passwords must be at least 6 characters long.")]
      public string Password { get; set; }

We will see how to ensure these error messages are properly displayed in the next section, :ref:`validating-models`.

Applying Validation Attributes - Video
--------------------------------------

.. youtube::
   :video_id: CIdCQ-7fHDY

.. admonition:: Note

   If you want to verify what code this video starts with, check out the `adding-viewmodels <https://github.com/LaunchCodeEducation/CodingEventsDemo/tree/adding-viewmodels>`__ branch.
   If you want to verify what code this video ends with, check out the `validation-attributes <https://github.com/LaunchCodeEducation/CodingEventsDemo/tree/validation-attributes>`__ branch.

Applying Validation Attributes - Text
-------------------------------------

To configure validation on the model-side, we begin by adding validation attributes to each field to which we want to apply constraints.

For our ``AddEventViewModel`` class, we add ``[StringLength]`` and ``[Required]`` to the ``Name`` and ``Description`` properties. 

.. sourcecode:: csharp
   :lineno-start: 8

   [Required(ErrorMessage = "Name is required.")]
   [StringLength(50, MinimumLength = 3, ErrorMessage = "Name must be between 3 and 50 characters.")]
   public string Name { get; set; }

   [Required(ErrorMessage = "Please enter a description for your event.")]
   [StringLength(500, ErrorMessage = "Description is too long!")]
   public string Description { get; set; }

The required ``MaximumLength`` and optional ``MinimumLength`` parameters for ``[StringLength]`` specify the maximum and minimum number of allowed characters, respectively.
Omitting the minimum length requirement means that no min or max will be applied for the field.
Not adding a ``[Required]`` attribute onto a property would make the field optional to the form submission.

Each of our attributes also receives an ``ErrorMessage`` parameter. This parameter provides a user-friendly message to display to the user if the particular validation rule fails.
We will see how to display these in a view a bit later. 

Next, we add a new property to store a contact email for each event.
This is a ``string`` named ``ContactEmail``.
Validating email addresses by directly applying each of the rules that an email must satisfy is *extremely* difficult.
Thankfully, there is an ``[EmailAddress]`` validation attribute that we can apply to our new field.

.. sourcecode:: csharp
   :lineno-start: 16

   [EmailAddress]
   public string ContactEmail { get; set; }

Before we can start up our application, we need to add a new input to our form in ``Events/Add.cshtml`` to take in the contact email for 
an event organizer. While we don't demonstrate these items in the video above, we cover them on the next page before tackling validation in the controller.

.. sourcecode:: html
   :lineno-start: 14

   <div class="form-group">
      <label asp-for="ContactEmail">Contact Email</label>
      <input asp-for="ContactEmail" />
   </div>

We also need to add a new column to the ``Events/Index.cshtml`` template to make ``ContactEmail`` visible. 

.. sourcecode:: html
   :lineno-start: 20

   <table class="table">
		<tr>
			<th>
				Id
			</th>
			<th>
				Name
			</th>
			<th>
				Description
			</th>
			<th>
				Contact Email
			</th>
		</tr>
		@foreach (var evt in Model)
		{
			<tr>
				<td>@evt.Id</td>
				<td>@evt.Name</td>
				<td>@evt.Description</td>
				<td>@evt.ContactEmail</td>
			</tr>
		}
    </table>

Now we can start up our application and test.
Submitting an empty form at ``/Events/Add`` still results in an event being created, which may not be what you were expecting. 
   
Rather than a bug, this is expected behavior.
Validation involves *both* the model and controller, but we have not modified the controller in any way.
Validation attributes simply define the validation rules that *should* be used to check data.
The responsibility of checking the data before saving a new event lies with the controller.

In the next section, we'll modify the controller to properly check for valid data.

Check Your Understanding
------------------------

.. admonition:: Question

   **True or False:** When using ``[StringLength]`` you must provide both minimum and maximum length arguments.

.. ans: False, only maximum length is required.

.. admonition:: Question

   **True or False:** Adding validation attributes to a model ensures that bad data is not saved.

.. ans: False, server-side validation requires cooperation from attributes on the model, as well as controller logic
