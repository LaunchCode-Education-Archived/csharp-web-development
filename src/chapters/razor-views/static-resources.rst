Static Resources
================

Previously, we briefly saw that when adding a view, we inherited some CSS from the ``_Layout.cshtml`` file in the ``Shared`` directory.
While every view we add for our action methods in the controllers inherits from this template, we can also add additional static resources, such as images, scripts, and styles.

Adding Custom Styles
--------------------

In large applications, we may find more CSS files than just ``site.css``.
To add styles that only apply to the view we are currently working on, we can use the same ``<link>`` tag we normally do for a static HTML page.

Two things to keep in mind before we start adding our own CSS:

#. We need to take into account any CSS in ``site.css``. This file contains the site-wide CSS and is included in ``_Layout``.
   If we want to modify something for the whole site CSS-wise, this is a good place to start.
#. We need to organize and store our CSS files in the appropriate location, just as we need to do with other files in ASP.NET Core MVC.
   In our application, we have a ``wwwroot`` directory. Inside that directory, we can add CSS files to the ``css`` subdirectory.
   The ``wwwroot`` directory is the default location for static files so when the application is served, ASP.NET Core MVC can easily locate these files.

.. admonition:: Example

   Let's say we add a custom CSS file to our application called ``custom.css`` and store this file in the ``css`` subdirectory in ``wwwroot``.
   If we want to link to this file to use it for a view, we would use the following line of HTML.

   .. sourcecode:: html

      <link rel="stylesheet" type="text/css" href="~/css/custom.css">

   Because we added our file to the ``css`` subdirectory inside the ``wwwwroot`` directory, our link is simply ``"~/css/custom.css"``.

Add Custom Scripts
------------------

We can also add custom JavaScript files the same way we add our CSS files. 
Inside the ``wwwroot`` directory, we can add JavaScript files to the ``js`` subdirectory.

When adding custom scripts, we want to keep the same things in mind as when we adding custom CSS files.
Our application includes site-wide JavaScript in ``site.js``. If we want to override site-wide scripts, that is where we should start.
If we want to add an additional script, we can add it in the ``js`` subdirectory inside ``wwwroot``.

.. admonition:: Example

   We added an additional JavaScript script called ``custom.js`` and stored this file in the ``js`` subdirectory inside the ``wwwroot`` directory.
   To add this file to a view, we can use the following HTML.

   .. sourcecode:: html

      <script src="~/js/custom.js"></script>

Adding Images to the Site
-------------------------

We can also add images that we want to use to the ``wwwroot`` directory.
To start, we need to create a new subdirectory called ``images``.
If we add an image called ``testimage.png`` to ``images``, we can reference it in our view with the ``<img>`` tag:

.. sourcecode:: html

   <img src="~/images/testimage.png">

Check Your Understanding
------------------------

.. admonition:: Question

   If we add an image called ``fluffy.jpg`` to the ``images`` directory inside of ``wwwroot``, what is the path we could use for the ``src`` attribute in the ``<img>`` tag?

   a. ``"/Views/images/fluffy.jpg"``
   b. ``"~/images/fluffy.jpg"``
   c. ``"~/img/fluffy.jpg"``
   d. ``"wwwroot/fluffy.jpg"``

.. ans: b 