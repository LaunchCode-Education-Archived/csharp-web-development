Create a New ASP.NET Project
============================

ASP.NET is a framework in the .NET Core family that is used to build web applications.
While `ASP.NET <https://docs.microsoft.com/en-us/aspnet/core/?view=aspnetcore-3.1>`_ can be used to build a wide variety of web applications, we will be focusing on using it to build MVC web applications.

.. _initialize-aspdotnet-project:

Getting Started
---------------

To create a ASP.NET MVC project, start a new project in Visual Studio.

**Windows Users:**

#. When selecting the type of project, choose *ASP.NET Core Web Application* for C#.

   .. figure:: figures/vs-windows-create-asp-app.png
      :alt: User selects ASP.NET Core Web Application for C# from the project type menu.

      User selects the appropriate project type.

#. Name your project *HelloASPDotNET* and put it in the appropriate directory for all of your classwork. Hit *Create*!
   
   .. figure:: figures/vs-windows-name-asp-app.png
      :alt: User names new project HelloASPDotNET

      User names their new project.

#. After naming, select *Web Application (Model-View-Controller)* from the project template options and unselect
   *Configure for HTTPS* under the *Advanced* header on the right.
   
   .. figure:: figures/vs-windows-select-mvc-asp-app.png
      :alt: User selects MVC template type from selection menu

      User selects the MVC template type.

**Mac Users:**

#. When selecting the type of project, head over to *.NET Core* and select *Web Application (model-view-controller)* for Mac users.
   For Windows users, select *ASP.NET Core*.

   .. figure:: figures/userselectmvc.png
      :alt: User selects Web Application MVC from the .NET Core Application menu

      User selects the appropriate project type.

   .. admonition:: Warning

      A page may appear asking if you want to add authentication to the app. If you do get this page, make sure to select *No Authentication* before proceeding forward.
   
#. Name your project *HelloASPDotNET* and put it in the appropriate directory for all of your classwork. Hit *Create*!
   Windows users may have to take one additional step and select *Web Application (model-view-controller)* after hitting *Create*.

   .. figure:: figures/usernamesproject.png
      :alt: User names new project HelloASPDotNET

      User names their new project.

**All Users:**

#. Visual Studio creates a fully-functional web application for you.
#. Hit *Run* (Mac) / *IIS Express* (Windows) and take note of the port number your application opens up to.

   .. figure:: figures/portnumber.png
      :alt: Arrow points to URL indicating port number is 5001.

   Taking note of the port number used by the server

.. admonition:: Note

   The home page of your application already contains a link to a tutorial from Microsoft on how to use ASP.NET MVC.
   If you want extra study materials, check out that `tutorial <https://docs.microsoft.com/en-us/aspnet/core/tutorials/first-mvc-app/start-mvc?view=aspnetcore-3.1&tabs=visual-studio>`_ from the home page Microsoft designed!

In the ``Controllers`` directory, check out ``HomeController.cs``.
Microsoft provided the code in ``HomeController`` and that is why our application ran immediately after we created it and was full of content.
As we work on our new application, we will be adding a new controller, ``HelloController``.

.. admonition:: Note

   As you code along with the videos, you will be working on your own project.
   However, should you want to review a step or double-check your code, fork LaunchCode's ``HelloASPDotNETDemo`` repository to see what the code looked like at each stage.
   The repository is up on `Github <https://github.com/LaunchCodeEducation/HelloASPDotNETDemo>`_.
   The ``master`` branch contains the code after creation and also shows the starting point for the next chapter.

Check Your Understanding
------------------------

.. admonition:: Question

   True/False: You should take note of the port number the server is using to run your application.
 
   a. True

   b. False

.. ans: True! It may not run at 5001








