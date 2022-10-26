.. _clone-csharp-project:

Cloning a C# Project
====================

Follow along with the provided walkthroughs to learn how to clone repos into Visual Studio.  
Try it out on your own by cloning the `LaunchCodeEducation/csharp-web-dev-datatypes <https://github.com/LaunchCodeEducation/csharp-web-dev-datatypes>`__
repository page and fork the repository into your own GitHub account by selecting *Fork* from the top right of the page.



Windows Users
-------------

`Clone a Git Repository in Visual Studio <https://learn.microsoft.com/en-us/visualstudio/version-control/git-clone-repository?view=vs-2022>`_

Note the path where you save this repo. 

Mac Users 
---------

`Cloning an Existing Repo <https://learn.microsoft.com/en-us/visualstudio/mac/set-up-git-repository?view=vsmac-2022#clone-an-existing-repository>`_

Be sure to note the Target Folder where this repo is saved.

Exploring the Cloned Repo in Your Terminal
------------------------------------------

Once you have cloned it into Visual Studio, locate the repo using your terminal.

On a Windows machine, it is a path you saved your repo at.  On a Mac, it's in the Target Folder.

Once you find the repo, ``cd`` into it.  
Look for the **Solution** file which uses the ``.sln`` file type.  

.. sourcecode:: 

   students-computer:csharp-web-dev-datatypes student$ ls
   HelloMethods			csharp-web-dev-datatypes.sln
   TempConverter

.. admonition:: Note

   The ``csharp-web-dev-datatype`` solution contains 2 separate projects:  ``HelloMethods`` and ``TempConverter``.
   A single solution can hold multiple projects.

Try to open the solution using the command line prompt: 

* Windows Users: ``start *.sln``
* Mac Users: ``open *.sln``


Return to the terminal.  Locate your ``Program.cs`` file for the ``HelloMethods`` project.  
This will be contained in the project directory of the same name.

.. sourcecode:: 

   students-computer:csharp-web-dev-datatypes student$ ls
   HelloMethods			csharp-web-dev-datatypes.sln
   TempConverter

   students-computer:csharp-web-dev-datatypes student$ cd HelloMethods
   students-computer:csharp-web-dev-datatypes student$ ls
   HelloMethods.csproj	Message.cs		Program.cs

You have now stepped into the project files for ``HelloMethods``.
All of the files here are related to the ``HelloMethods`` project.

As you work with repos in this unit, some solutions may contain a single project and others may contain multiple.

How to Work with a Cloned Repo
------------------------------

We recommend using the terminal to open and work with your repos.  You will be able to interact with git easily this way.

Use the terminal to locate the repo you wish to open.  ``cd`` into the solution.  
You can verify this by looking for a file that has the ``.sln`` type.
Use the command prompt above for your operating system.

Open the solution file tree in Visual Studio.
If you see multiple projects, you can select which one to run two ways:

#. Right-clicking on the name of the project and selecting the **Run** option.
#. Open the project's ``Program.cs`` file then use the run button in the menu bar.

Check Your Understanding
------------------------

.. admonition:: Question

   Which file is the solution?

   .. sourcecode:: 

      students-computer:csharp-web-dev-datatypes student$ ls
      HelloMethods			csharp-web-dev-datatypes.sln
      TempConverter

   #. ``TempConverter``
   #. ``HelloMethods``	
   #. ``csharp-web-dev-datatypes.sln``
   #. ``Program.cs``

.. ans: c, csharp-web-dev-datatypes.sln

.. admonition:: Question

   Where would Willow find the ``Program.cs`` file for the ``TempConverter`` project?
   

   .. sourcecode:: 

      students-computer:csharp-web-dev-datatypes student$ ls
      HelloMethods			csharp-web-dev-datatypes.sln
      TempConverter

   #. Inside the ``TempConverter`` project
   #. Inside the ``HelloMethods`` project
   #. Inside the ``csharp-web-dev-datatypes.sln``
   #. None of the above

.. ans: a, Inside the ``TempConverter`` project