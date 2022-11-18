Configuring Identity
====================

With Identity in place, we can start to configure the settings of the library to meet our authentication requirements.
The first place to start with configuring Identity to fit the needs of the project is in ``Startup.cs``.

.. admonition:: Note

   Try and code along as you read more about Identity!
   This page starts off with the code in the `identity-scaffolding <https://github.com/LaunchCodeEducation/CodingEventsDemo/tree/identity-scaffolding>`__ branch in ``CodingEventsDemo``.
   The final code for this page is in the `identity-config <https://github.com/LaunchCodeEducation/CodingEventsDemo/tree/identity-config>`__ branch in ``CodingEventsDemo``.
   If you are looking for an additional walkthrough, check out this `article <https://learn.microsoft.com/en-us/aspnet/core/security/authentication/customize-identity-model?source=recommendations&view=aspnetcore-6.0>`__ from Microsoft.

``Startup.cs``
--------------

``ConfigureServices()``
^^^^^^^^^^^^^^^^^^^^^^^

Now that we are getting to configure our user, let's check out the code in ``ConfigureServices()``.
Earlier you may have added the following:

.. sourcecode:: csharp
   :linenos:

   services.AddDefaultIdentity<IdentityUser>
   (options =>
   {
      options.SignIn.RequireConfirmedAccount = true;
      options.Password.RequireDigit = false;
      options.Password.RequiredLength = 10;
      options.Password.RequireNonAlphanumeric = false;
      options.Password.RequireUppercase = true;
      options.Password.RequireLowercase = false;
   }).AddEntityFrameworkStores<JobDbContext>();

This code is dictating the settings for account creation. Right now, for a user to create an account, they have to have the following:

#. They have to click a link to confirm their account.
#. Their password has to be more than 10 characters long.
#. Their password has to include an uppercase letter(s).

The following is not true for a user to create an account.

#. Their password does not have to include a number.
#. Their password does not have to include a special character such as a question mark.
#. Their password does not have to include lowercase letters.

These are just some basic requirements that can be changed to suit the needs of your application.
For a full list of the default settings for users' passwords and how we can change those settings, check out the `documentation <https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.identity.passwordoptions?view=aspnetcore-3.1>`__.

In ``ConfigureServices()``, we can also configure cookie settings, password hashers, user validation requirements, sign in settings and more.

Additional Customizations
-------------------------

As you learn more about what Identity can do, you may find yourself wanting to customize it more and more to suit your needs!
Here are some examples of what you can do with it.

#. Customize user information
#. Customize user roles
#. Customize the UI
#. Add new settings to user passwords
#. Change the default settings around user sign-in

.. admonition:: Note

   If you want to customize user data, it is best to do so when initially scaffolding the app.
   `IdentityUser <https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.identity.entityframeworkcore.identityuser?view=aspnetcore-1.1>`__ has a number of properties that are important and relevant to storing user data.
   However, when you read through the requirements you may notice that you need additional properties, such as the user's first and last name.
   If you want to add custom properties, check out this `article <https://docs.microsoft.com/en-us/aspnet/core/security/authentication/add-user-data?view=aspnetcore-5.0&tabs=visual-studio>`__ from Microsoft.