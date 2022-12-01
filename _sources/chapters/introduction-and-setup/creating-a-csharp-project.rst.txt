.. _create-new-csharp-project:

Creating a C# Project
=====================

Following the "Hello World" trend, let's create a new Visual Studio project.

1. Create a new folder to hold your C# practice files. Since you will be
   creating lots of small projects as you move through this course, we
   suggest that you also add sub-folders with names corresponding to the
   related chapters and projects. Something like
   ``csharp-practice/chapter-name/project-name``.

2. In Visual Studio, from the project opener window, select the 
   option to create a *New* Visual Studio project.

3. You next need to choose what project template to use. For this first project
   (and those in the next several lessons), select the 
   **.NET Core Console Application** option for C#.

   Mac Users:
      * You can find this by selecting **Web and Console** options in the left menu.  
      * Select the **App** subdirectory
      * Select **Console Application** from the **General** menu option in the center menu pane

   Windows Users:
      * Select **Console App** 
      * If you can't find it easily, you can search "Console App"

4. Select **.NET 6.0** as your Target Framework.

5. Then, give your new project a name. Following :ref:`naming-conventions`, 
   call your project ``HelloWorld``. The solution name will be the same. Choose 
   where you want this project to be saved, ideally somewhere inside the 
   directory you created in Step 1 of this tutorial.   

   Mac Users:
      * Pick the options for "Use git for version control."  and "Create a .gitignore file to ignore inessential files"

6. Visual Studio will now create a **Solution** to hold your console **Project**. 
   The project is your current app.  The project contains all of the files that app needs to build and run.
   The solution is a workspace that combines multiple projects, which are usually related to each other.  
   The solution file type is *.sln*.

   Once created, Visual Studio opens a new project window that displays your ``Program.cs`` file.

7. To see the other files inside this solution, you will need to **View** either the 
   **Solution** (Mac Users) or the **Solution Explorer** (Windows Users).

   You'll see the project file tree containing a file called ``Program.cs`` 
   in a pane called *Solution Explorer*.

8. You are new to C# and we'll go over the syntax present in ``Program.cs``
   in time. For now, can you guess what line 2 accomplishes?

   .. sourcecode:: csharp
      :linenos:

        // See https://aka.ms/new-console-template for more information
        Console.WriteLine("Hello, World!");

   Click on the **Run** button (a triangle button located above the ``Program.cs`` panel) indicated in one of the images above to 
   run the project and see the output.

9. A console window should pop up with the line "Hello World" printed. 
   That's it. You have created and executed your first C# application.

   .. admonition:: Tip
   
      The first time you run a console app in Visual Studio, you may be prompted
      to allow VS to access the terminal. This is ok.

      This may also take longer than a few seconds to run the very first time.

Troubleshooting
^^^^^^^^^^^^^^^

This app is printing to the terminal.  If you are not able to see the output, look inside the project's terminal.

If you would like more instructions on creating and running this project check out the following documentation:

* `Windows Users <https://learn.microsoft.com/en-us/visualstudio/get-started/csharp/visual-studio-ide?view=vs-2022>`_   
* `Mac Users <https://learn.microsoft.com/en-us/visualstudio/mac/ide-tour?view=vsmac-2022>`_


.. index:: ! solution

Hello, Solution!
----------------

You've just created your first C# project. Congrats! In fact, you've also just created your own C# **solution**.
Your ``HelloWorld`` project is nested within a solution called ``HelloWorld``. A solution behaves like a container for
related projects and other Visual Studio settings. 

A C# project contains all the code to run a particular application. Along with the ``Program.cs`` file you ran just a 
moment ago, you may have also noticed a ``Dependencies`` folder. Many applications require extra code like dependencies
or other compiling configurations to execute. 

You can create another project inside of the ``HelloWorld`` solution 
very easily. Right click on the solution name to add a new project, 
another console app as above, and name it ``Hello<YourName>``. 
Change the starter code in ``Program.cs`` to greet you by name.

Now that you have more than one project in your solution, you need to select which one you want to run. Select 
the project name from the menu next to the *Run* button.


Check Your Understanding
------------------------

.. admonition:: Question

   Given the code below, which line is responsible for printing a message?

   .. sourcecode:: csharp
      :linenos:

        // See https://aka.ms/new-console-template for more information
        Console.WriteLine("Hello, World!");

   #. Line 1
   #. Line 2
   #. None of the above

.. ans: b, Line 2

.. admonition:: Question

   Where does to the following code print out?

   .. sourcecode:: csharp
      :linenos:

        // See https://aka.ms/new-console-template for more information
        Console.WriteLine("Hello, World!");

   #. In line 3 of the ``Program.cs`` file
   #. In the browser
   #. In the terminal
   #. None of the above

.. ans: c, in the terminal
