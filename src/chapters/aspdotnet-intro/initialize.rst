Create a New ASP.NET Project
============================

ASP.NET is a framework in the .NET Core family that is used to build web applications.
While `ASP.NET <https://learn.microsoft.com/en-us/aspnet/core/?view=aspnetcore-6.0>`_ can be used to build a wide variety of web applications, 
we will be focusing on using it to build MVC web applications.

.. _initialize-aspdotnet-project:

Getting Started
---------------

To create a new ASP.NET MVC project, start a new project in Visual Studio.

Windows Users
^^^^^^^^^^^^^

#. Use the **Get started** Menu to **Create a new project**.
#. When selecting the type of project, select **ASP.NET Core Web App (Model-View-Controller)**.  
   
   There are 2 ways to find this easily:
      A. Use the search bar.
      B. Select "Web" from the dropdown menu.  

   Once you have your project type, click *Next*.
#. Name your project ``HelloASPDotNET`` and put it in the appropriate directory for all of your classwork. 
   Hit Next. 
#. Select the Framework.  We are going to use *.NET Core 6.0*. 
   You do not need to adjust any other options at this point.  Select Create!
#. Visual Studio creates a fully-functional web application for you.

Troubleshooting
   This `tutorial for Windows <https://learn.microsoft.com/en-us/aspnet/core/tutorials/first-mvc-app/start-mvc?view=aspnetcore-6.0&tabs=visual-studio>`_ 
   can help you if you are stuck.

Mac Users
^^^^^^^^^

#. Open Visual Studio for Mac and select a **New**
#. The type of project is a **Web Application (Model-View-Controller)**.  
   In the left-side menu, select **App** from under the **Web and Console** list.
   Continue on to the next screen.
#.  Target Framework will be ``.NET 6.0``.  You don't need to adjust any other settings at this time.
#. Name your project ``HelloASPDotNET`` and put it in the appropriate directory for all of your classwork. 
   Hit Next. 
#. Visual Studio creates a fully-functional web application for you.

Troubleshooting
   Microsoft created a tutorial for creating an MVC in Visual Studio, but for the Mac version they recommend the following `guide <https://learn.microsoft.com/en-us/aspnet/core/tutorials/first-mvc-app/start-mvc?view=aspnetcore-5.0&tabs=visual-studio-mac>`_.

.. admonition:: Note 
   
   The guide is working with ``.NET 5.0`` which is no longer supported.  Make you that you are using ``.NET 6.0``.

All Users
^^^^^^^^^

#. Now launch the application!

   a. **Mac Users**: Click *Run*.  It is a button that looks like a triangle pointing to the right.
   b. **Windows Users**: Try clicking *IIS Express* first. If this results in
      an ``HTTP Error 500.0``, use the dropdown arrow next to *IIS Express*.
      Select ``HelloAspDotNet`` (or whatever you named your project) and try
      launching the application again.
      
#. Eventually, your browser will open and display your application. 
   Take note of the port number in the address bar.

Troubleshooting
   Refer to the guides mentioned above

.. admonition:: Note

   The home page of your application already contains a link to a tutorial from Microsoft on how to use ASP.NET MVC.
   If you want extra study materials, check out 
   that `tutorial <https://learn.microsoft.com/en-us/aspnet/core/tutorials/first-mvc-app/start-mvc?view=aspnetcore-6.0&tabs=visual-studio>`_ from the home page Microsoft designed!

Explore the Code
----------------

In the ``Controllers`` directory, check out ``HomeController.cs``.
Microsoft provided the code in ``HomeController`` and that is why our application ran immediately after we created it and was full of content.
As we work on our new application, we will be adding a new controller, ``HelloController``.

.. admonition:: Note

   As you code along with the videos, you will be working on your own project.
   However, should you want to review a step or double-check your code, fork LaunchCode's ``HelloASPDotNETDemo`` repository to see what the code looked like at each stage.
   The repository is up on `Github <https://github.com/LaunchCodeEducation/HelloASPDotNETDemo>`_.
   The ``main`` branch contains the code after creation and also shows the starting point for the next chapter.

Check Your Understanding
------------------------

.. admonition:: Question

   True/False: You should take note of the port number the server is using to run your application.
 
   a. True
   b. False

.. ans: True! It may not run at 5001








