Validation Attributes
=====================

Within the model of a C# web application, we can define validation rules using attributes.
Validation attributes can be applied to model fields. 

.. index::
   single: validation, annotations

.. index:: ! [Required], ! [EmailAddress], ! [Range], ! [StringLength]

Common Attributes
------------------

We'll use only a few of these attributes, but you can find a full list in the `documentation <https://docs.microsoft.com/en-us/aspnet/core/mvc/models/validation?view=aspnetcore-3.1#built-in-attributes>`_.

.. list-table:: Common Validation Annotations
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
     - Specifies the maximum length of a string field.
     - ``[StringLength(100)]``
   * - ``[EmailAddress]``
     - Specifies that a string field should conform to email formatting standards.
     - ``[EmailAddress]``

.. admonition:: Example

   To apply the validation rules of the :ref:`example on the previous page <validation-example>` to the fields of a ``User`` model class, we can use ``@Size`` and ``@NotBlank``.

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

.. TODO: Add video here on what attributes to add 

.. starting branch: adding-viewmodels
.. ending branch: validation-attributes

Applying Validation Attributes - Text
-------------------------------------

To configure validation on the model-side, we begin by adding validation attributes to each field to which we want to apply constraints.

For our ``AddEventViewModel`` class, we add ``[StringLength]`` and ``[Required]`` to the ``Name`` property, and just ``[StringLength]`` to the ``Description`` property.

.. sourcecode:: csharp
   :lineno-start: 8

   [Required(ErrorMessage = "Name is required.")]
   [StringLength(50, MinimumLength = 3, ErrorMessage = "Name must be between 3 and 50 characters")]
   public string Name { get; set; }

   [StringLength(500, ErrorMessage = "Description too long!")]
   public string Description { get; set; }

The ``MaximumLength`` and ``MinimumLength`` parameters for ``[StringLength]`` specify the maximum and minimum number of allowed characters, respectively
Omitting either of these means that no min or max will be applied for the field.
For our ``Description`` field, leaving off ``[Required]`` makes this field optional.

Each of our attributes also receives a ``ErrorMessage`` parameter, which provides a user-friendly message to display to the user if the particular validation rule fails.
We will see how to display these in a view a bit later. 

Next, we add a new property to store a contact email for each event.
This is a ``string`` named ``ContactEmail``.
Validating email addresses by directly applying each of the rules that an email must satisfy is *extremely* difficult. Thankfully, there is an ``@Email`` validation annotation that we can apply to our new field.

After adding this new field to our constructor, our class is done for the moment.

.. sourcecode:: csharp
   :lineno-start: 8

      [Required(ErrorMessage = "Name is required.")]
      [StringLength(50, MinimumLength = 3, ErrorMessage = "Name must be between 3 and 50 characters")]
      public string Name { get; set; }

      [StringLength(500, ErrorMessage = "Description too long!")]
      public string Description { get; set; }

      [EmailAddress(ErrorMessage = "Invalid email. Try again.")]
      public string ContactEmail { get; set; }
   }

Before we can start up our application, we need to add a new column to the ``Events/Index`` template to make ``ContactEmail`` visible. 

.. sourcecode:: html
   :lineno-start: 5

   <form asp-controller="Events" asp-action="NewEvent" method="post">
      <div class="form-group">
         <label asp-for="Name">Name</label>
         <input asp-for="Name" />
      </div>
      <div class="form-group">
         <label asp-for="Description">Description</label>
         <input asp-for="Description" />
      </div>
      <div>
         <label asp-for="ContactEmail">Contact Email</label>
         <input asp-for="ContactEmail" />
      </div>
      <input type="submit" value="Add Event" />
   </form>

Now we can start up our application and test. Submitting an empty form at ``/Events/Add`` still results in an event being created, which may not be what you were expecting. 

.. TODO: Add end result image?
   
Rather than a bug, this is expected behavior.
Recall that validation involves *both* the model and controller, but we have not modified the controller in any way.
Validation attributes simply define the validation rules that *should* be used to check data.
The responsibility of checking the data before saving a new event lies with the controller.

In the next section, we'll modify the controller to properly check for valid data.

Check Your Understanding
------------------------

.. admonition:: Question

   **True or False:** When using ``[StringLength]`` you must provide both minimum and maximum arguments.

.. ans: False, only maximum length is required.

.. admonition:: Question

   **True or False:** Adding validation attributes to a model ensures that bad data is not saved.

.. ans: False, server-side validation requires cooperation from annotations on the model, as well as controller logic
