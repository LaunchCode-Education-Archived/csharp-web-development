Working with Data Stores
========================

With our data store and persistent class configured, we are ready to realize the full power of ORM.

Data Stores in the Controller - Video
-------------------------------------

Since our data store, ``EventDbContext``, extends ``DbContext``, we have access to all of the methods defined by ``DbContext``. There are quite a few such methods (see `the documentation <https://docs.microsoft.com/en-us/dotnet/api/microsoft.entityframeworkcore.dbcontext?view=efcore-3.1#methods>`_ for details), but the most frequently used are ``Add``, ``Remove``, ``Update``, and ``Find``. 

.. todo: add data store / controller video

Data Stores in the Controller - Text
-------------------------------------

Adding the Data Store
^^^^^^^^^^^^^^^^^^^^^

To access data from the database in a controller, we'll need an instance of ``EventDbContext``. Adding the following code to the top of ``EventsController`` will make one available as an instance variable of the controller.

.. sourcecode:: csharp
   :lineno-start: 17

   private EventDbContext context;

   public EventsController(EventDbContext dbContext)
   {
      context = dbContext;
   }

We can reference ``context`` anywhere within our controller in order to query the database.

.. index:: dependency injection

.. admonition:: Note

   It may not be obvious how this code works, since we never explicitly call the constructor for ``EventsController``. When we run our application, ASP.NET will call this constructor for us, and will pass in an instance of ``EventDbContext``. This is an example of the concept of **dependency injection**, a topic which is fairly complex and beyond the scope of this course.

Using Data Store Methods
^^^^^^^^^^^^^^^^^^^^^^^^

Check Your Understanding
------------------------