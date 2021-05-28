.. index:: ! scaffolding

.. _user-auth-walkthrough:

Getting Started with Identity
=============================

As a developer, you may find yourself wanting to add Identity in one of the two following situations:

#. You are creating a new project and you know that you need Identity in the project.
#. You are working with an existing project and need to add Identity to continue your work.

For this chapter, we are going to focus on the second situation and how we might add Identity to ``CodingEvents``.
The process of adding Identity to an existing code base is called **scaffolding**.

.. admonition:: Note

   Try and code along as you read more about Identity!
   This page starts off with the code in the `display-tag-items <https://github.com/LaunchCodeEducation/CodingEventsDemo/tree/display-tag-items>`__ branch in ``CodingEventsDemo``.
   The final code for this page is in the `identity-scaffolding <https://github.com/LaunchCodeEducation/CodingEventsDemo/tree/identity-scaffolding>`__ branch in ``CodingEventsDemo``.

.. TODO: Check package version compatibility. Asp Net Core 5.0 was causing some issues

.. Students need to check with SDK is being used by global.json and which sdks they have available. Starter code is set up to use 3.1 so they may have to generate new global.json and roll package versions to 3.1 to work with CLI tools and ensure scaffolding is successful.

Before You Start
----------------

Before getting started, you need to make note of the version of .NET Core SDK your project is using.
Inside the project directory, run the following command:

.. sourcecode:: guess

   dotnet --info

When you run this command, the output may look something like the following:

.. sourcecode:: guess
   :linenos:

   .NET Core SDK (reflecting any global.json):
   Version:   3.1.101
   Commit:    b377529961

   Runtime Environment:
   OS Name:     Mac OS X
   OS Version:  10.15
   OS Platform: Darwin
   RID:         osx.10.15-x64
   Base Path:   /usr/local/share/dotnet/sdk/3.1.101/

   Host (useful for support):
   Version: 5.0.5
   Commit:  2f740adc14

   .NET SDKs installed:
   3.1.101 [/usr/local/share/dotnet/sdk]
   5.0.202 [/usr/local/share/dotnet/sdk]

   .NET runtimes installed:
   Microsoft.AspNetCore.App 3.1.1 [/usr/local/share/dotnet/shared/Microsoft.AspNetCore.App]
   Microsoft.AspNetCore.App 5.0.5 [/usr/local/share/dotnet/shared/Microsoft.AspNetCore.App]
   Microsoft.NETCore.App 2.1.15 [/usr/local/share/dotnet/shared/Microsoft.NETCore.App]
   Microsoft.NETCore.App 2.1.23 [/usr/local/share/dotnet/shared/Microsoft.NETCore.App]
   Microsoft.NETCore.App 3.1.1 [/usr/local/share/dotnet/shared/Microsoft.NETCore.App]
   Microsoft.NETCore.App 5.0.5 [/usr/local/share/dotnet/shared/Microsoft.NETCore.App]

   To install additional .NET runtimes or SDKs:
   https://aka.ms/dotnet-download

If the .NET Core SDK listed on line 2 does not match the SDK specified in your ``csproj`` file, you need to open up your ``global.json`` and edit it so that the SDK used by the project matches.

You need to install five NuGet packages before getting started with this process:

#. ``Microsoft.AspNetCore.Identity``
#. ``Microsoft.AspNetCore.Identity.UI``
#. ``Microsoft.AspNetCore.Identity.EntityFrameworkCore``
#. ``Microsoft.EntityFrameworkCore.SqlServer``
#. ``Microsoft.VisualStudio.Web.CodeGeneration.Design``

When installing these packages, make sure that the versions are the same as the .NET Core version your project is using. You can confirm this is the case by reviewing the code in your ``csproj`` file.

With these packages installed, you are ready to go!

Scaffolding Identity in an Exisiting Project
--------------------------------------------

In both Visual Studio for Mac and Visual Studio for Windows, you have the option to add new scaffolded items through the UI and through the terminal.

Adding Identity Through the UI
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

#. Right click on the project folder at the top of the solution.
#. Select *Add* > *New Scaffolded Item*.
#. From the menu, select *Identity*.

This approach is the simpler of the two approaches. However, for some Mac users, you may not find Identity as an option when you use this approach.
If that is the case, use the terminal method.

Adding Identity through the Command Line
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

All of these commmands should be run in the project directory *inside* of the solution.

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

   ::

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

#. Configuration of Identity is dependent on you and your project requirements. In the case of ``CodingEvents``, you would want to continue to use ``EventDbContext``.
   This is how your final generation command would look:

   .. sourcecode:: guess

         dotnet aspnet-codegenerator identity --dbContext EventDbContext --files "Account.Register;Account.Login;Account.Logout;Account.RegisterConfirmation"

   .. admonition:: Note

      In the above command, we used the option for ``files``.
      Identity is a Razor Class Library so it comes with Razor pages preconfigured for registration, login, etc.
      This option means that we want the scaffolder to generate these files and add them to the solution, making it easier for us to customize these files in the future.
      The option for ``defaultUI`` means that we have no need to have these files in the solution and so we won't have the ability to customize them. 

#. Once we run this series of commands, we will have successfully scaffolded Identity code onto our existing project.

.. admonition:: Note

   If you do not see any new scaffolding, try using the command ``dotnet restore``. This will restore our NuGet packages manually as opposed to them automatically restoring. 

``DbContext``
^^^^^^^^^^^^^

If you tried to run the application right now, you would encounter some build errors.
While we specified in our scaffolding commands that we wanted to use ``EventDbContext``, we need to open up two files to make sure that Identity is properly using ``EventDbContext``: ``Startup.cs`` and ``IdentityHostingStartup.cs``.

``IdentityHostingStartup.cs`` can be found in the ``Areas/Identity`` directory. 
You should update this file to make sure that it uses MySQL and the ``"DefaultConnection"`` string:

.. sourcecode:: csharp
   :lineno-start: 14

   public class IdentityHostingStartup : IHostingStartup
    {
        public void Configure(IWebHostBuilder builder)
        {
            builder.ConfigureServices((context, services) => {
                services.AddDbContext<EventDbContext>(options =>
                    options.UseMySql(
                        context.Configuration.GetConnectionString("DefaultConnection")));

                services.AddDefaultIdentity<IdentityUser>(options => options.SignIn.RequireConfirmedAccount = true)
                    .AddEntityFrameworkStores<EventDbContext>();
            });
        }
    }

Now go to ``Startup.cs`` and comment out the following lines in ``ConfigureServices()``:

.. sourcecode:: csharp
   :lineno-start: 29

   services.AddDbContext<EventDbContext>(options =>
      options.UseMySql(Configuration.GetConnectionString("DefaultConnection")));

Add one line to ``ConfigureServices()`` in ``Startup.cs`` for the use of the Razor pages in Identity:

.. sourcecode:: csharp

   services.AddRazorPages();

Add an additional line to ``app.UseEndpoints()`` inside of ``Configure()`` in ``Startup.cs``:

.. sourcecode:: csharp
   :lineno-start: 62
   :emphasize-lines: 6

   app.UseEndpoints(endpoints =>
   {
      endpoints.MapControllerRoute(
         name: "default",
         pattern: "{controller=Home}/{action=Index}/{id?}");
      endpoints.MapRazorPages();
   });

``endpoints.MapRazorPages()`` specifies to the app that the Identity pages should follow the routing laid out in ``_LoginPartial.cshtml``.

These initial steps were to make sure that the application is still using ``EventDbContext`` for its connection to the database now that we have added Identity.
However, if you take a look inside the ``Areas/Identity/Data`` directory, you will find a file also called ``EventDbContext``. Delete that generated file and continue to use the one we initially created for ``CodingEvents``.
Now we just need to dive into our copy of ``EventDbContext`` and do the following:

#. ``EventDbContext`` should now extend ``IdentityDbContext<IdentityUser>``.
#. We need to add an additional line to ``OnModelCreating()``:

   .. sourcecode:: csharp

      base.OnModelCreating(modelBuilder);

With these changes made, ``EventDbContext`` will look like the following:      

.. sourcecode:: csharp
   :lineno-start: 13

   public class EventDbContext : IdentityDbContext<IdentityUser>
   {
        public DbSet<Event> Events { get; set; }
        public DbSet<EventCategory> Categories { get; set; }
        public DbSet<Tag> Tags { get; set; }
        public DbSet<EventTag> EventTags { get; set; }

        public EventDbContext(DbContextOptions<EventDbContext> options)
            : base(options)
        {
        }

        protected override void OnModelCreating(ModelBuilder modelBuilder)
        {
            modelBuilder.Entity<EventTag>().HasKey(et => new { et.EventId, et.TagId });

            base.OnModelCreating(modelBuilder);
        }
   }

You may note that we didn't add any ``DbSet`` for ``IdentityUser`` like we did for other models in the application.
This is not an oversight! With ``EventDbContext`` properly set up, we can run a migration and the database will add the appropriate tables for our authentication data.

Views
^^^^^

In your solution, you will find a new view inside the ``Views/Shared`` directory called ``_LoginPartial.cshtml``.
This partial view contains the logic for the links to actions that the users need, such as registration forms, login forms, sign out actions, and so on.
If you peek inside the file, you will find these links live inside a conditional.

.. sourcecode:: csharp
   :linenos:

   @using Microsoft.AspNetCore.Identity
   @using CodingEventsDemo.Areas.Identity.Data

   @inject SignInManager<IdentityUser> SignInManager
   @inject UserManager<IdentityUser> UserManager

   <ul class="navbar-nav">
   @if (SignInManager.IsSignedIn(IdentityUser))
   {
      <li class="nav-item">
         <a id="manage" class="nav-link text-dark" asp-area="Identity" asp-page="/Account/Manage/Index" title="Manage">Hello @UserManager.GetUserName(IdentityUser)!</a>
      </li>
      <li class="nav-item">
         <form id="logoutForm" class="form-inline" asp-area="Identity" asp-page="/Account/Logout" asp-route-returnUrl="@Url.Action("Index", "Home", new { area = "" })">
            <button id="logout" type="submit" class="nav-link btn btn-link text-dark">Logout</button>
         </form>
      </li>
   }
   else
   {
      <li class="nav-item">
         <a class="nav-link text-dark" id="register" asp-area="Identity" asp-page="Account/Register">Register</a>
      </li>
      <li class="nav-item">
         <a class="nav-link text-dark" id="login" asp-area="Identity" asp-page="/Account/Login">Login</a>
      </li>
   }
   </ul>

`UserManager <https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.identity.usermanager-1?view=aspnetcore-3.1>`__ deals with the user information in the database. We can use the properties and methods to perform operations on user objects such as adding a new user or fetching user information.
On line 11 in the code above, ``UserManager`` is used to fetch the signed-in user's username so we greet them by name!
`SignInManager <https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.identity.signinmanager-1?view=aspnetcore-3.1>`__ deals with users signing in. 
On line 8, ``SignInManager`` is used to check if the user is signed in. If the user is signed in, then the links that will be displayed are to manage the account or log out of the account.
If the user is not signed in, then the links are to either log in or register for an account on the site.

This partial view can be placed anywhere you need it, but we recommend starting with placing it in ``_Layout.cshtml`` so that a signed-in user can easily access the necessary links from any page.
To add it to the navbar, use the following syntax:

.. sourcecode:: guess

   <partial name="_LoginPartial" />

Final Steps
^^^^^^^^^^^

No matter which approach you took for the initial steps in scaffolding, you need to run a new migration and update your database.
Once you update the database, your database will contain a number of tables related to Identity such as ``AspNetUsers`` and ``AspNetRoles``.

To test that you are on the right track, run the application. Click on the link to register and create a new account.
Query the ``AspNetUsers`` table in the database to make sure that the newly added account is there.

Now that we have successfully added Identity to our project, we are ready to start coding!

