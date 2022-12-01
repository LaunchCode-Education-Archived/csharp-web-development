NuGet
=====

.. index:: ! NuGet

**NuGet** is a package management tool for .NET software. 
NuGet allows you to use external code sources without including the codebase itself. You can make 
use of compiled libraries that other developers have already built. You can choose to use a 
specific version of a package hosted by NuGet, and update that version as need be. 

As with MSBuild, we will only scratch the surface of the utility of a .NET package manager. That 
said, it is still a good idea to get `familiar with these tools <https://learn.microsoft.com/en-us/nuget/what-is-nuget>`_. As your programs grow larger, 
MSBuild and NuGet will help to maintain a robust codebase.

NuGet packages are readily available within the IDE itself. Perhaps you have noticed the 
*Dependencies* directory that is created in our projects? 

To browse available NuGet packages:

#. Right-click on that directory
#. Select “Manage NuGet Packages” from the dropdown menu
#. The resulting window will show you a catalog of software packages you may add to your project

Managing NuGet Packages
^^^^^^^^^^^^^^^^^^^^^^^

The following documentation can help you become more familiar with downloading and managing NuGet packages.

**Windows Users:** `Follow this guide <https://learn.microsoft.com/en-us/nuget/consume-packages/install-use-packages-visual-studio>`_.

**Mac Users:** `Use this guide <https://learn.microsoft.com/en-us/visualstudio/mac/nuget-walkthrough?toc=%2Fnuget%2Ftoc.json&view=vsmac-2022>`_




Check Your Understanding
------------------------

.. admonition:: Question

   Select which item best describes the job of NuGet.

   a. NuGet compiles your C# programs to be deployed in different conditions.
   b. NuGet is a marshmallow-like confection found in many candy bars.
   c. NuGet is a package manager for .NET programs.
   d. NuGet allows you to download dependency library source code into your solution.

.. ans: c, NuGet is a package manager for .NET programs.

.. admonition:: Question

   NuGet and MSBuild share responsibilities and only one is needed to deploy a C# app.

   a. True
   b. False

.. ans: False, While NuGet gives you access to the dependencies you need for your application, 
   MSBuild can configure how those dependencies are used in different executable environments.
