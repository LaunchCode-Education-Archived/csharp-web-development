Create a New ASP.NET Project
============================

ASP.NET is a framework in the .NET Core family that is used to build web applications.
While `ASP.NET <https://docs.microsoft.com/en-us/aspnet/core/?view=aspnetcore-3.1>`_ can be used to build a wide variety of web applications, we will be focusing on using it to build MVC web applications.

.. _initialize-aspdotnet-project:

Getting Started
---------------

To create a ASP.NET MVC project, start a new project in Visual Studio.

#. When selecting the type of project, head over to *.NET Core* and select *Web Application (model-view-controller)* for Mac users.
   For Windows users, select *ASP.NET Core*.

   .. figure:: figures/userselectmvc.png
      :alt: User selects Web Application MVC from the .NET Core Application menu

      User selects the appropriate project type

#. Name your project *HelloASPDotNET* and put it in the appropriate directory for all of your classwork. Hit *Create*!
   Windows users may have to take one additional step and select *Web Application (model-view-controller)* after hitting *Create*.

   .. figure:: figures/usernamesproject.png
      :alt: User names new project HelloASPDotNET

   User names their new project

#. Visual Studio creates a fully-functional web application for you.
#. Hit *Run* and take note of the port number your application opens up to.

   .. figure:: figures/portnumber.png
      :alt: Arrow points to URL indicating port number is 5001.

   Taking note of the port number used by the server

.. admonition:: Note

   The home page of your application already contains curated content from Microsoft on how to use ASP.NET Core.
   If you want extra study materials, check out this `tutorial <https://docs.microsoft.com/en-us/aspnet/core/tutorials/first-mvc-app/start-mvc?view=aspnetcore-3.1&tabs=visual-studio>`_ from the home page Microsoft designed!

In the ``controllers`` directory, check out ``HomeController.cs``.
Microsoft provided the code in ``HomeController`` and that is why our application ran immediately after we created it and was full of content.
As we work on our new application, we will be adding a new controller, ``HelloController``.

.. admonition:: Note

   As you code along with the videos, you will be working on your own project.
   However, should you want to review a step or double-check your code, fork LaunchCode's ``HelloASPDotNET`` repository to see what the code looked like at each stage.
   The repository is up on `Github <https://github.com/LaunchCodeEducation/HelloASPDotNET>`_.
   The ``master`` branch contains the code after creation and also shows the starting point for the next chapter.

Check Your Understanding
------------------------

.. admonition:: Question

   True/False: All custom code in an ASP.NET MVC application is located in the ``Main`` method.
 
   a. True

   b. False

.. ans: False, most features are developed outside of the ``Main`` method in an ASP.NET MVC application.








