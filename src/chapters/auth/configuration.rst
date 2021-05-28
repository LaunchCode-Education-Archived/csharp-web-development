Configuring Identity
====================

With Identity in place, we can start to configure the settings of the library to meet our authentication requirements.
The first place to start with configuring Identity to fit the needs of the project is in ``Startup.cs``.

.. admonition:: Note

   Try and code along as you read more about Identity!
   This page starts off with the code in the `identity-scaffolding <https://github.com/LaunchCodeEducation/CodingEventsDemo/tree/identity-scaffolding>`__ branch in ``CodingEventsDemo``.
   The final code for this page is in the `identity-config <https://github.com/LaunchCodeEducation/CodingEventsDemo/tree/identity-config>`__ branch in ``CodingEventsDemo``.


``Startup.cs``
--------------

``ConfigureServices()``
^^^^^^^^^^^^^^^^^^^^^^^

The first place that we may want to customize our settings is at the bottom of ``ConfigureServices()``.
When you were testing out your application, you may have accidentally entered an invalid password. 
The validation conditions for a user's password is an example of one of the settings that can be configured here by using a method called ``services.Configure<IdentityOptions>()``.
If we wanted to make the minimum number of characters for our password 10 as opposed to 6, we would do the following.

.. sourcecode:: csharp
   :linenos:

   services.Configure<IdentityOptions>( options =>
      options.Password.RequiredLength = 10
   );

For a full list of the default settings for users' passwords and how we can change those settings, check out the `documentation <https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.identity.passwordoptions?view=aspnetcore-3.1>`__.

In ``ConfigureServices()``, we can also configure cookie settings, password hashers, user validation requirements, sign in settings and more.

``Configure()``
^^^^^^^^^^^^^^^

Below ``ConfigureServices()``, you will find ``Configure()``. Inside ``Configure()``, we must make sure we have the following:

.. sourcecode:: csharp
   :linenos:

   app.UseRouting();

   app.UseAuthentication();
   app.UseAuthorization();

While we did properly scaffold Identity onto our code base, we need to add the calls to ``UseAuthentication()`` and ``UseAuthorization()``.
Our application uses middleware to relay requests between our application and our database.
By adding the calls to ``UseAuthentication()`` and ``UseAuthorization()``, we are specifying that we now need authentication middleware to handle these requests.
Authentication is not just about ensuring users are signed in. It is about protecting data at every point it passes through to make the application work.

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
   Identity has a default user class called ``IdentityUser``.
   `IdentityUser <https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.identity.entityframeworkcore.identityuser?view=aspnetcore-1.1>`__ has a number of properties that are important and relevant to storing user data.
   However, when you read through the requirements you may notice that you need additional properties, such as the user's first and last name.
   If you want to add custom properties, check out this `article <https://docs.microsoft.com/en-us/aspnet/core/security/authentication/add-user-data?view=aspnetcore-5.0&tabs=visual-studio>`__ from Microsoft.