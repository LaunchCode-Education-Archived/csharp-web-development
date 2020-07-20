.. index:: ! scaffolding

Getting Started with Identity
=============================

As a developer, you may find yourself wanting to add Identity in one of the two following situations:

#. You are creating a new project and you know that you need Identity in the project.
#. You are working with an existing project and need to add Identity to continue your work.

For this chapter, we are going to focus on the second situation and how we might add Identity to ``CodingEvents``.
The process of adding Identity to an existing code base is called **scaffolding**.

Scaffolding Identity in an Exisiting Project
--------------------------------------------

In both Visual Studio for Mac and Visual Studio for Windows machines, you have the option to add new scaffolded items through the UI and through the terminal.

Adding Identity through the UI
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

#. Right click on the project folder at the top of the solution.
#. Select *Add* > *New Scaffolded Item*.
#. From the menu, select *Identity*.

This approach is the simpler of the two approaches. However, when you may not find Identity as an option when you use this approach.
If that is the case, use the terminal method.

Adding Identity through the Command Line
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

#. Use the following command to make sure you have the necessary code generator tools installed.

   .. sourcecode:: guess

      dotnet tool install -g dotnet-aspnet-codegenerator

   If the tool is installed, you are ready to proceed.
#. Use the following command to add the full package necessary to generate the actual Identity code.

   .. sourcecode:: guess

      dotnet add package Microsoft.VisualStudio.Web.CodeGeneration.Design

#. Now you are ready to add Identity to your project! You can configure Identity in any number of ways to fit the project requirements. To see all of the options use this command:

   .. sourcecode:: guess

      dotnet aspnet-codegenerator identity -h

   When you use this command, you will see a menu of options in your terminal and can configure from there.

   .. sourcecode:: bash

      Usage: aspnet-codegenerator [arguments] [options]

      Arguments:
         generator  Name of the generator. Check available generators below.

      Options:
         -p|--project             Path to .csproj file in the project.
         -n|--nuget-package-dir   
         -c|--configuration       Configuration for the project (Possible values: Debug/ Release)
         -tfm|--target-framework  Target Framework to use. (Short folder name of the tfm. eg. net46)
         -b|--build-base-path     
         --no-build               

      Selected Code Generator: identity

      Generator Options:
         --dbContext|-dc       : Name of the DbContext to use, or generate (if it does not exist).
         --files|-fi           : List of semicolon separated files to scaffold. Use the --listFiles option to see the available options.
         --listFiles|-lf       : Lists the files that can be scaffolded by using the '--files' option.
         --userClass|-u        : Name of the User class to generate.
         --useSqLite|-sqlite   : Flag to specify if DbContext should use SQLite instead of SQL Server.
         --force|-f            : Use this option to overwrite existing files.
         --useDefaultUI|-udui  : Use this option to setup identity and to use Default UI.
         --layout|-l           : Specify a custom layout file to use.
         --generateLayout|-gl  : Use this option to generate a new _Layout.cshtml
         --bootstrapVersion|-b : Specify the bootstrap version. Valid values: '3', '4'. Default is 4.

#. Configuration of Identity is dependent on you and your project requirements. In the case of ``CodingEvents``, you would want to continue to use ``EventDbContext`` and you may want to use a custom user named ``User``.
   This is how your final generation command would look:

   .. sourcecode:: guess

      dotnet aspnet-codegenerator identity --useDefaultUI --dbContext EventDbContext --userClass User

   .. admonition:: Note

      In the above command, we used the option for ``useDefaultUI``. Identity is a Razor Class Library so it comes with Razor pages preconfigured for registration, login, etc.
      This option means that we want to use the default pages.

#. Once we run this series of commands, we will have successfully scaffolded Identity code onto our existing project.

Final Steps
^^^^^^^^^^^

No matter which approach you take for scaffolding, you need to run a new migration and update your database.
Once you update the database, your database will contain a number of tables related to Identity such as ``AspNetUsers`` and ``AspNetRoles``.

Configuring Your Custom Settings
--------------------------------

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
   :linenos: 7

   namespace CodingEventsDemo.Areas.Identity.Data
   {
      // Add profile data for application users by adding properties to the User class
      public class User : IdentityUser
      {
         public string Name { get; set; }
      }
   }

