Object-Relational Mapping
=========================

.. index:: ! Object-Relational Mapping, ! ORM, ! Data Layer, ! object-relational mapper

.. admonition::  Warning

   Look for notes regarding any changes between the videos, Visual Studio, and Entity Framework Core.
   We will provide notes in the text for working with the ``CodingEventsDemo`` repos as well as 
   projects you created yourself. 

We are now ready to connect our MVC application to a relational database and add persistent data storage to our apps. To do so, we need to use *object-relational mapping*.

**Object-Relational Mapping** or **ORM** is a technique for converting data between C# objects and relational databases.
ORM converts data between two incompatible type systems (C# and MySQL), such that each model class becomes a table in our database and each instance a row of the table.

.. admonition:: Example

   Let's say we have a C# class called ``ContactInfo``. ``ContactInfo`` has three properties: an integer ``Id``, a string ``Name``, and a string ``Email``.
   Now we want to store this information in a MySQL database.
   We can use ORM so that the database of our application has a table to contain all objects instantiated from the ``ContactInfo`` class.
   The table called ``contactinfo`` has three columns: an integer ``Id``, a varchar ``Name``, and a varchar ``Email``.

   Now, let's instantiate a C# object:

   .. sourcecode:: csharp

      public ContactInfo frank = new ContactInfo(3,"Frank","frank@email.com"); 

   Having set up our application, we can add Frank's info to our ``contactinfo`` table.
   While we will write the code to add Frank's info to our database in C#, the frameworks and APIs that make ORM happen will run the following MySQL query for us.

   .. sourcecode:: mysql

      INSERT INTO contactinfo (Id,Name,Email)
      VALUES (3,"Frank","frank@email.com");
   
   Now Frank's info is stored in our MySQL database in the ``contactinfo`` table!

To make ORM work in our C# applications, we need an **object-relational mapper** to convert between C# and MySQL.
When we create a new model class and configure it to be stored in a database, a mapper creates a MySQL query to make the corresponding table. In our example above, the query to create the ``contactinfo`` table from the ``ContactInfo`` class would be:

.. sourcecode:: mysql
   :linenos:

   CREATE TABLE contactinfo (
      INT Id,
      VARCHAR(255) Name,
      VARCHAR(255) Email
   );

One of the most widely used object-relational mappers available for C# and ASP.NET Core is **Entity Framework Core**. This framework makes use of **data layers**. When we learned about models, we learned that :ref:`data layers <data-layer-dev>` add abstraction between models and the data we want to store. With Entity FrameworkCore, data layers take the form of classes that extend ``DbContext``. Models are NOT persistent data stores and relational databases do NOT shape the C# objects we will be using. We want to make sure that the two remain separate.

.. admonition:: Note

   We'll often shorten Entity Framework Core to EF. The "Core" in the name indicates that we're talking about the version of EF that is compatible with ASP.NET Core.

.. index:: ! EntityFrameworkCore 

ORM in ASP.NET
--------------

To enable ORM in our apps, we need to connect our EF mapper to a MySQL database. Let's do this with ``CodingEvents``!

.. _setup-orm-database:

Setting up a Persistent Database - Video
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The following video explains how we can add a MySQL database to our ``CodingEvents`` application and configure our app to connect to the database. 

.. admonition:: Note

   If you want to verify what code this video starts with, check out the `enums <https://github.com/LaunchCodeEducation/CodingEventsDemo/tree/enums>`_ branch. If you want to verify what code this video ends with, check out the `db-setup <https://github.com/LaunchCodeEducation/CodingEventsDemo/tree/db-setup>`_ branch.

.. youtube:: 
   :video_id: RJ0NRG1FjIA

Setting up a Persistent Database - Text
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

To get started with using a relational database with our MVC applications, we need to first go to MySQL Workbench.

In MySQL Workbench, do the following:

#. Create a new schema, ``coding_events``.   
   
#. Add a new user, ``coding_events``, with a new password. Give the user all privileges to modify your new schema. 

Now, attach MySQL to your project in ``appsettings.json`` by adding the following property.

.. sourcecode:: javascript

  "ConnectionStrings": {
    "DefaultConnection": "server=localhost;userid=coding_events;password=PASSWORD;database=coding_events;"
  }

The ``DefaultConnection`` property contains key/value pairs for each piece of information needed for our app to connect to the database created above. Be sure to replace ``PASSWORD`` with the password that you used when creating the ``coding_events`` user above.

We now need to add a couple of NuGet packages to support our database connection. This process differs slightly for Windows and MacOS users. 

Install MySQL Dependency
~~~~~~~~~~~~~~~~~~~~~~~~

**Working with the NuGet Package Manager**

Open the NuGet Package Manager in Visual Studio:

- **Windows** - *Tools > NuGet Package Manager > Manage NuGet Packages for Solution*
- **Mac** - *Project > Manage NuGet Dependencies*

Search for for all of the packages listed below. Select the package and install.

When installing these packages, make sure that the versions are the same as the .NET Core version your project is using. 
You can confirm this is the case by reviewing the code in your csproj file.

We will need to install the following NuGet packages:

* ``Pomelo.EntityFrameworkCore.MySql``  
   This dependency provides code that is able to connect to a MySQL database 
   from within an ASP.NET Core application using EF. Note that this package 
   itself depends on the following EF packages:

* ``Microsoft.EntityFrameworkCore.Relational``  
   This is a mapping framework that automates access and storage of data in your project's database.

* ``Microsoft.EntityFrameworkCore.Design``  
   This helps manage data migrations and the design-time logic.
   **Note:** This was not installed in the video above.  
   If you do not install it, Entity Framework Core will print an error message asking you to install it.


.. admonition:: Tip 

   You can view installed packages and their dependencies by navigating to 
   *Dependencies > NuGet* in the Solution Explorer (or the Solution pane on Mac) 
   and expanding a given package. 

Verify EF Core Tools are Present
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

EF 6.0.X is typically installed with Visual Studio 2022.

You can test that it has been installed by running the following in your terminal.

#. ``cd`` your way down into the project folders.  
   Verify your location by running the ``ls`` command.  You should see all the folders within your project.

   .. sourcecode:: bash

      student-computer:CodingEventsDemo student$ ls
      CodingEventsDemo.csproj		ViewModels
      Controllers			Views
      Data				appsettings.Development.json
      Models				appsettings.json
      Program.cs			bin
      Properties			obj
      Startup.cs			wwwroot

#. When you are this level run the following command:

   .. sourcecode:: bash

      dotnet ef 

   You should see the following output:

   .. sourcecode:: bash

      student-computer:CodingEventsDemo student$ dotnet ef

                     _/\__       
               ---==/    \\      
         ___  ___   |.    \|\    
        | __|| __|  |  )   \\\   
        | _| | _|   \_/ |  //|\\ 
        |___||_|       /   \\\/\\

        Entity Framework Core .NET Command-line Tools 6.0.X
        
.. admonition:: Note

   We recommend installing either version 6.0.11 or higher


Troubleshooting EF Core Tools
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

If you are not able to see the Entity Framework Core logo, 
then try the following steps to troubleshoot the issue.

#. Open a terminal window using your terminal app outside of Visual Studio.

#. Open a terminal and run:

   .. sourcecode:: bash

      $ dotnet tool install -g dotnet-ef

   This command installs a set of command-line tools for working with EF *globally*, 
   which means it will be available for any ASP.NET project we use in the future. 
   We will use the tools provided by this package to update our database schema after adding or changing model classes. 

#. Once you have taken these steps, you are ready to set up the appropriate models and controllers for the application. We'll do that in the next section.
#. To test that this install worked, run ``dotnet ef``. The output should be a message displaying basic EF tool commands and options.

.. admonition:: Note for Mac users only
   
   For these tools to be accessible from the command line, they must be within your user path.
   We create or update your `bash profile <https://friendly-101.readthedocs.io/en/latest/bashprofile.html>`_.  
   Your bash profile is a text file that you can add any paths needed.  
   You may add to this as you continue on your programming journey.

   1. Open your ``~/.bash_profile`` with this command: 

      .. sourcecode:: bash

         open ~/.bash_profile 
      
      `Recall <https://education.launchcode.org/intro-to-professional-web-dev/chapters/terminal/basic-commands.html>`_ 
      that ``~`` is shorthand for your home directory, which is the directory you are in when you open a new terminal window.
   
   2. Add the following line to the very bottom of your profile:
   
      .. sourcecode:: bash

            export PATH="$PATH:$HOME/.dotnet/tools/"

   3. Save and close the file. Then close your terminal window and open a new one, so that the changes can take effect.

   4. To test that this install worked, run ``dotnet ef``. The output should be a message displaying basic EF tool commands and options.


Once you have taken these steps, you are ready to set up the appropriate models and controllers for the application. We’ll do that in the next section.

.. index:: ! environment variables

Ensuring Connection Success and Security
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Before we can get into the ins and outs of using ORM, we need to make sure that our application has a corresponding database and that our application is ready to connect to MySQL. We can start to do this by creating new schemas and setting user privileges in MySQL Workbench. We also *must* make sure that the MVC application has the correct dependencies, username, and password to access the schema.

If we do not do these steps, then our application will not be able to use a persistent data source.

Setting the value of the ``DefaultConnection`` property using the values of the username and password is NOT a best practice. We regularly commit our code to Github, meaning anyone who reads the code in our repository can see the username and password. While you can do it for the applications in this class, you do not want to do it in the future.

.. admonition:: Note

   To avoid this in the future, you can configure your ``DefaultConnection`` string to reference **environment variables**. You then hide the appropriate info by setting the environment variable's value equal to the password, for example.

See Microsoft `documentation <https://learn.microsoft.com/en-us/aspnet/core/fundamentals/configuration/?view=aspnetcore-6.0#environment-variables>`_ to learn how to keep the username and password to your database safe and secure.

Check Your Understanding
------------------------

.. admonition:: Question

   **True/False:** Writing usernames and passwords in plain text in a file is a GREAT idea!

.. ans: False

.. admonition:: Question

   **True/False:** An ORM converts data between C# objects and relational databases.

.. ans: True

.. admonition:: Question

   **True/False:** We need Entity Framework Core AND a MySQL provider to successfully use ORM in this project.

.. ans: True
