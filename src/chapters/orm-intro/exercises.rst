.. _orm1-exercises:

Exercises: OMG the ORM!
=======================

For the exercises, we are going to continue building on our ``CodingEvents`` application.
The exercise instructions assume that your code resembles the `orm1 <https://github.com/LaunchCodeEducation/CodingEventsDemo/tree/orm1>`_ branch.
Create a new branch off of your ``orm1`` code to get started on the exercises. 

.. admonition:: Note

   You will be making one model class and adding to ``DbContext``.
   If you are not sure what these classes should look like, refer back to the sections on `persistent models <>`_ and `DbContext <>`_.

The ``EventCategory`` Class
---------------------------

First, create a new class called ``EventCategory`` in the ``Models`` directory.

``EventCategory`` needs to have the following:

#. An ``Id`` property of type ``int``.
#. A ``Name`` property of type ``string``.
#. A constructor.

``EventCategory`` represents data that will be stored in our database.

Adding to ``DbContext``
-----------------------

Once you have created ``EventCategory``, you need to add to ``EventDbContext`` to set up a table in the database for storing categories.

Adding a New Table to the Database
----------------------------------

With the two steps completed above, you now need to add a new migration and update your database.
You should now see a new table in your database!
