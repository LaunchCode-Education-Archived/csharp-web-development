.. _accessing-data:

Accessing Data
==============

Now that we have connected our C# application to a MySQL database, we need to set up our C# code to interact with the new schema. In the previous chapters, we learned about performing basic operations on a database and its tables, such as creating, reading, updating, and deleting rows. One of the reasons we use ORM is so that now we can write C# code in our application to manage our relational database.

.. index:: data store

.. _intro-to-data-stores:

Data Stores - Video
-------------------

While classes determine the structure of a table in our relational database, a **data store** does the work of inserting, updating, and retrieving data from the database. 

.. admonition:: Note

   If you want to verify what code this video starts with, check out the `db-setup <https://github.com/LaunchCodeEducation/CodingEventsDemo/tree/db-setup>`_ branch. If you want to verify what code this video ends with, check out the `persistent-data-store <https://github.com/LaunchCodeEducation/CodingEventsDemo/tree/persistent-data-store>`_ branch.

.. youtube::
   :video_id: NV_Tw9sQeEQ

Data Stores - Text
------------------

.. index::
   single: data store; in-memory
   single: data store; persistent

In our work so far, we have been using an in-application data store,. This is the class ``EventData``. The ``EventData`` class is an 
**in-memory data store**. I keeps track of new events using a C# data structure, which gets deleted from memory every time the app shuts 
down. With EF, we can create a **persistent data store**. A persistent data store retains data even when an app shuts down.

Creating a ``DbContext``
^^^^^^^^^^^^^^^^^^^^^^^^

To create a persistent data store for our ``Event`` class, we can extend the class ``DbContext``, which is provided by EF. Here's what that looks like.

.. sourcecode:: csharp
   :linenos:

   using CodingEventsDemo.Models;
   using Microsoft.EntityFrameworkCore;

   namespace CodingEventsDemo.Data
   {
      public class EventDbContext : DbContext
      {
         public DbSet<Event> Events { get; set; }

         public EventDbContext(DbContextOptions<EventDbContext> options)
               : base(options)
         {
         }
      }
   }

This new class is placed in the ``Data`` directory and namespace. By convention, we name it ``EventDbContext`` since it is going to be used to work with ``Event`` objects and data. We extend ``DbContext``, which will provide most of the base functionality that we need. More on this in the next section. 

This extension *must* provide a property of type ``DbSet<Event>``. The ``DbSet`` class provides methods for querying sets of objects of the given type (in this case, ``Event``). In the next section, we will explore how to use these methods.

The only additional code that we need to add is a constructor that calls the constructor from the base class. 

This basic data store template can be used for any class that you want to persist in a database. Each such class will need its own data store. 

Registering a Data Store
^^^^^^^^^^^^^^^^^^^^^^^^

In order to make ASP.NET aware of this data store, we need to register ``EventDbContext`` in the ``Startup`` class. ``Startup`` is automatically executed every time our app starts up, and is a place where application configuration can be customized.

Open up ``Startup.cs`` and find the ``ConfigureServices`` method. By default, it looks like this.

.. sourcecode:: csharp
   :lineno-start: 26

   public void ConfigureServices(IServiceCollection services)
   {
      services.AddControllersWithViews();
   }

A persistent data store is considered a service in ASP.NET, and we can register this service by add the following code to ``ConfigureServices``.

.. sourcecode:: csharp
   :lineno-start: 29

   services.AddDbContext<EventDbContext>(options =>
         options.UseMySql(Configuration.GetConnectionString("DefaultConnection")));

Don't worry too much about the intricate details of what this code is doing. Simply note the following points:

- We are calling the ``AddDbContext<EventDbContext>`` method of the ``services`` object. Referencing ``EventDbContext`` here ensures that we are registering the data store that we just created.
- ``Configuration.GetConnectionString("DefaultConnection")`` will retrieve the database connection string from ``appsettings.json`` that we configured in the previous section. This ensures that the data store interacts with the specific database configured there. Note that it is possible for an application to have connections to multiple databases.
- The method ``options.UseMySql`` is called. This ensures that ``EventDbContext`` is a data store that interacts with a MySQL database.

.. index:: ! persistent class, primary key

Configuring a Primary Key
^^^^^^^^^^^^^^^^^^^^^^^^^

As you learned previously, every relational table should have a primary key. When working with ORM, this means that every **persistent class** needs a primary key property. A persistent class is a class that we want to store (or persist) in a database.

Our ``Event`` class currently has an ID field.

.. sourcecode:: csharp
   :lineno-start: 16

   public int Id { get; }
   static private int nextId = 1;

	public Event()
   {
      Id = nextId;
      nextId++;
   }

   public Event(string name, string description, string contactEmail) : this()
   {
      Name = name;
      Description = description;
      ContactEmail = contactEmail;
   }


When introducing this property previously, we intentionally named it ``Id`` in anticipation of using EF and a data store to persist ``Event`` objects. EF will *automatically* consider any property named ``Id`` to be the primary key for that class. Therefore, we already have the necessary property! 

However, there are two changes we need to make:

#. Primary key properties must have both a getter and setter.
#. The value of a primary key property is set by the database when an object is first stored. Therefore, we shouldn't be setting this value in the constructor. So we can remove the code in the constructors that explicitly sets the value of ``Id``, along with the ``nextId`` field.

So the code sample above can be simplified to the following.

.. sourcecode:: csharp
   :lineno-start: 16

   public int Id { get; set; }

	public Event()
   {
   }

   public Event(string name, string description, string contactEmail)
   {
      Name = name;
      Description = description;
      ContactEmail = contactEmail;
   }

.. index:: ! migration

.. index::
   single: database; migration

Migrations - Video
------------------

If you want to verify what code this video starts with, check out the `persistent-data-store <https://github.com/LaunchCodeEducation/CodingEventsDemo/tree/persistent-data-store>`_ branch. If you want to verify what code this video ends with, check out the `migrations <https://github.com/LaunchCodeEducation/CodingEventsDemo/tree/migrations>`_ branch.

.. youtube::
   :video_id: q6PfagaiHqE

Migrations - Text
-----------------

Our application is now completely configured to store ``Event`` objects in our MySQL database. However, if you look at the ``coding_events`` database, you'll notice that it has no table in which to store such data. To create such a table, we need to create and run a **database migration**. A database migration (or migration, for short) is an update to a database made in order to reflect changes in an application's model. Every time we change our application's model by adding or removing a new persistent class, or by modifying a persistent class, we will need to create and run a migration. 

The EntityFrameworkCore Tools package we installed in the last section provides tools for working with migrations. To get started, open a terminal (the Terminal app on MacOS or Powershell on Windows). Navigate to the ``CodingEventsDemo`` project folder *within* your ``CodingEventsDemo`` solution. This is the folder that contains ``Controllers/``, ``Views/``, and so on, and is NOT the main project folder.

Then run the following command to create a migration:

.. sourcecode:: bash

   $ dotnet ef migrations add InitialMigration

This instructs the EF tools to create a migration named ``InitialMigration``. In doing so, EF scans our project looking for persistent classes (i.e. classes with data stores that have been registered in ``Startup``) and compares them to the current state of the MySQL database. If any classes have been added, removed, or changed, it will generate code to update the database to be in sync with the application's model. This code is stored in the ``Migrations/`` folder of your project.

In order to run a migration, we issue the command:

.. sourcecode:: bash

   $ dotnet ef database update

This command will apply the changes to the database. To verify the changes, open MySQL Workbench and notice that there is now an ``Events`` table with columns corresponding to the properties of our class. 

.. admonition:: Note

   EntityFrameworkCore uses the ``_EFMigrationsHistory`` table in the database to keep track of which migrations have already been run. When we run ``dotnet ef migrations update``, EF will reference this table and run *all* migrations that have not yet been applied, in the correct order.

The next section will look at how we can store and retrieve ``Event`` objects from within our controller.

Check Your Understanding
------------------------

.. admonition:: Question

   **True/False:** Every persistent class will automatically have a MySQL table created to use to store its data.

.. ans: False - we have to use a migration to create the table

.. admonition:: Question

   A data store should extend which of the following classes in the ``Microsoft.EntityFrameworkCore`` package?

   #. ``DataStore``
   #. ``DbContext``
   #. ``MySqlStore``
   #. None of the above

.. ans: B
