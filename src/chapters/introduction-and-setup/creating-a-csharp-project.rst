.. _create-new-csharp-project:

Creating a C# Project
=====================

Following the "Hello World" trend, let's create a new Visual Studio project.

#. Create a new folder to hold your C# practice files. Since you will be
   creating lots of small projects as you move through this course, we
   suggest that you also add sub-folders with names corresponding to the
   related chapters and projects. Something like
   ``csharp-practice/chapter-name/project-name``.

#. In Visual Studio, from the project opener window, select the 
   *New* option to create a new Visual Studio project.

#. You next need to choose what project template to use. For this first project,
   select *.NET Core / App / Console Application*.

   .. figure:: figures/vsmac-console-app-template.png
      :alt: Visual Studio console application template selection.

      Visual Studio console application template selection.

#. Then, give your new project a name. Following :ref:`naming-conventions`, 
   call your project ``HelloWorld``. The solution name will be the same. Choose 
   where you want this project to be saved, ideally somewhere inside the 
   directory you created in Step 1 of this tutorial. Pick the option to use 
   Git for version control.
   
   .. figure:: figures/vsmac-name-project.png
      :alt: Name a new Visual Studio Project.

      Name a new Visual Studio project.

#. Once created, Visual Studio opens a new project window. You'll see the project
   file tree on the left and a file called ``Program.cs``.

   .. figure:: figures/vsmac-new-project.png
      :alt: A new Visual Studio Project.

      A new Visual Studio project.

#. You are new to C# the language and we'll go over the syntax present in ``Program.cs``
   in time. For now, can you guess what line 9 accomplishes?

   .. sourcecode:: csharp
      :linenos:

      using System;

      namespace HelloWorld
      {
         class Program
         {
            static void Main(string[] args)
            {
               Console.WriteLine("Hello World!");
            }
         }
      }

   Click on the triangle button to run the project and see the output.

   .. admonition:: Tip
   
      The first time you run a console app in Visual Studio, you may be prompted
      to allow VS to access the terminal. This is ok.

#. A console window should pop up with the line "Hello World"" printed. 
   That's it. You have created your first C# application.

Check Your Understanding
------------------------

.. admonition:: Question

   Given the code below, which line is responsible for printing a message?

   .. sourcecode:: csharp
      :linenos:

      class HelloWorld 
      {
         static void Main(string[] args)
         {
            Console.WriteLine("Hello C# Students");
         }
      }

   #. Line 1
   #. Line 3
   #. Line 5
   #. None of the above

.. ans: c, Line 5

.. admonition:: Question

   In the sourcecode, which line is responsible for defining the class?

   .. sourcecode:: csharp
      :linenos:

      class HelloWorld 
      {
         static void Main(string[] args)
         {
            Console.WriteLine("Hello C# Students");
         }
      }

   #. line 1
   #. line 3
   #. line 5
   #. None of the above

.. ans: a, Line 1
