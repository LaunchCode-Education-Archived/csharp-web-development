Object-Relational Mapping
=========================

.. index:: ! Object-Relational Mapping, ! ORM, ! Data Layer, ! object-relational mapper

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

One of the most widely used object-relational mappers available for C# and ASP.NET Core is **EntityFrameworkCore**. This framework makes use of **data layers**. When we learned about models, we learned that :ref:`data layers <data-layer-dev>` add abstraction between models and the data we want to store. With EntityFrameworkCore, data layers take the form of classes that extend ``DbContext``. Models are NOT persistent data stores and relational databases do NOT shape the C# objects we will be using. We want to make sure that the two remain separate.

.. admonition:: Note

   We'll often shorten EntityFrameworkCore to EntityFramework or just EF. The "Core" in the name indicates that we're talking about the version of EF that is compatible with ASP.NET Core.

.. index:: ! EntityFrameworkCore 

ORM in ASP.NET
--------------

To enable ORM in our apps, we need to connect our mapper, EntityFrameworkCore, to a MySQL database. Let's do this with ``CodingEvents``!

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

Open the NuGet Package Manager in Visual Studio:

- **Windows** - *Tools > NuGet Package Manager > Manage NuGet Packages for Solution*
- **Mac** - *Project > Manage NuGet Dependencies*

Search for ``Pomelo.EntityFrameworkCore.MySql``. Select the package and install. This dependency provides code that is able to connect to a MySQL database from within an ASP.NET Core application using EF. Note that this package itself depends on the main EntityFrameworkCore package, ``Microsoft.EntityFrameworkCore.Relational``, so it is also installed.

.. tip:: 

   You can view installed packages and their dependencies by navigating to *Dependencies > NuGet* in the Solution Explorer (or the Solution pane on Mac) and expanding a given package. 

Install EF Core Tools
~~~~~~~~~~~~~~~~~~~~~

In this section, "terminal" refers to the Terminal app in MacOS and Powershell in Windows (use *Tools > Command Line > Developer Powershell* to open).

Open a terminal and run:

.. sourcecode:: bash

   $ dotnet tool install -g dotnet-ef

This command installs a set of command-line tools for working with EntityFrameworkCore *globally*, which means it will be available for any ASP.NET project we use in the future. We will use the tools provided by this package to update our database schema after adding or changing model classes. 

.. admonition:: Note

   This note applies to *Mac users only*.

   For these tools to be accessible from the command line, they must be within your user path. Open ``~/.bash_profile`` with this command: 
	
	.. sourcecode:: bash

		code ~/.bash_profile 
		
	Add the following line to the very bottom (recall that ``~`` is shorthand for your home directory, which is the directory you are in when you open a new terminal window).

   .. sourcecode:: bash

      export PATH="$PATH:$HOME/.dotnet/tools/"

   This will append the location of the EF tools to your user path. Save and close the file. Then close your terminal window and open a new one, so that the changes can take effect.

To test that this install worked, run ``dotnet ef``. The output should be a message displaying basic EF tool commands and options.

Once you have taken these steps, you are ready to set up the appropriate models and controllers for the application. We'll do that in the next section.

.. index:: ! environment variables

Ensuring Connection Success and Security
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Before we can get into the ins and outs of using ORM, we need to make sure that our application has a corresponding database and that our application is ready to connect to MySQL. We can start to do this by creating new schemas and setting user privileges in MySQL Workbench. We also *must* make sure that the MVC application has the correct dependencies, username, and password to access the schema.

If we do not do these steps, then our application will not be able to use a persistent data source.

Setting the value of the ``DefaultConnection`` property using the values of the username and password is NOT a best practice. We regularly commit our code to Github, meaning anyone who reads the code in our repository can see the username and password. While you can do it for the applications in this class, you do not want to do it in the future.

.. admonition:: Note

   To avoid this in the future, you can configure your ``DefaultConnection`` string to reference **environment variables**. You then hide the appropriate info by setting the environment variable's value equal to the password, for example.

See Microsoft `documentation <https://docs.microsoft.com/en-us/aspnet/core/fundamentals/configuration/?view=aspnetcore-3.1#environment-variables>`_ to learn how to keep the username and password to your database safe and secure.

Check Your Understanding
------------------------

.. admonition:: Question

   **True/False:** Writing usernames and passwords in plain text in a file is a GREAT idea!

.. ans: False

.. admonition:: Question

   **True/False:** An ORM converts data between C# objects and relational databases.

.. ans: True

.. admonition:: Question

   **True/False:** We need EntityFrameworkCore AND a MySQL provider to successfully use ORM.

.. ans: True
