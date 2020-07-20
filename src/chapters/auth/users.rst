Handling User Data
==================

Customizing User Data
^^^^^^^^^^^^^^^^^^^^^

Identity has a default user class called ``IdentityUser``.
`IdentityUser <https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.identity.entityframeworkcore.identityuser?view=aspnetcore-1.1>`__ has a number of properties that are important and relevant to storing user data.
As you scan through your app's requirements, you may find that you need additional information.
This is why we created a custom ``User`` class above.
One property that is not included in ``IdentityUser``, but we do want to include is ``Name``.

Whenever we want to check out hte code we generated during the scaffolding process, we go to *Areas* > *Identity*.
To update our customer ``User`` class, we can locate it in the ``Data`` subdirectory.

After adding a ``Name`` property, the ``User`` class should look like the following code:

.. sourcecode:: csharp
   :lineno-start: 7

   namespace CodingEventsDemo.Areas.Identity.Data
   {
      // Add profile data for application users by adding properties to the User class
      public class User : IdentityUser
      {
         public string Name { get; set; }
      }
   }