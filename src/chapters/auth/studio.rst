Studio: TechJobs Authentication
===============================

For this studio, you'll be tasked with adding simple user authentication to your 
``TechJobs`` application. The steps to do this will match what you have already done 
in ``CodingEvents``. You should refer back to the tutorial starting 
:ref:`here <user-auth-walkthrough>`.

#. :ref:`auth_studio_scaffolding`
#. :ref:`auth_studio_config`
#. :ref:`auth_studio_user`

The Starter Code
----------------

#. Fork and clone the starter code for 
   `TechJobsAuthentication <https://github.com/LaunchCodeEducation/TechJobsAuthentication>`__.

#. You will need to do some work to ensure that the schema, user, and database password 
   match your own local MySQL setup.

   #. Open ``appsettings.json`` and find the following statement:

      ::

         "ConnectionStrings": {
            "DefaultConnection": "server=localhost;userid=techjobs_auth;password=ILoveTechJobs;database=techjobs_auth;"
         }

   #. You likely do not already have a schema named ``techjobs_auth`` or 
      this combination of username and password so you must create them.

      .. admonition:: Tip
      
         To create a new schema in your current connection, refer 
         back to the instructions in the `SQL Part 1 Exercises <https://education.launchcode.org/SQL/chapters/mysql-part-1/exercises.html>`_.

         To create a new user with permissions, refresh your memory
         in :ref:`setup-orm-database`.

   #. Before getting started with setting up Identity, run a new migration to make sure that all of the database info is correct.

.. admonition:: Note
   
      We've greatly reduced the functionality of the app so you can focus
      on the work to set up authentication. Running the application now 
      gives you a familiar-looking navbar with one menu option, *Add Jobs*.
      You can add jobs right away and an astute observer of the starter code and
      schema tables will notice that the fields on ``Job`` are only strings, not
      complex objects.

.. _auth_studio_scaffolding:

Scaffolding
-----------

#. In the project you have cloned, scaffold Identity onto the codebase.

   #. Use the same files as the chapter content and ``JobDbContext``.

#. Update ``IdentityHostingStartup.cs``, ``Startup.cs``, and ``JobDbContext`` as necessary.
#. Add the ``LoginPartial`` partial view to the navbar.
#. Run a new migration and test the application.

.. _auth_studio_config:

Configuration
-------------

#. Use the appropriate methods to set the following validation conditions on the password:

   #. The password must be at a minimum of 8 characters.
   #. The password does NOT need to contain an uppercase letter.

#. Complete any additional necessary configuration steps in ``Startup.cs``.

.. _auth_studio_user:

Authorization
-------------

#. Add the necessary attributes so only logged-in users can add jobs, but all visitors to the application can see the listing of jobs.

That's it, that's all. You're done. Go forth and test the auth flow by visiting the home page, registering for a new account, and logging into and out of an existing account. 
Then add this to any other ASP.NET project you're working on!
      
