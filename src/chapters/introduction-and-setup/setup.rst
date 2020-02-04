Setup For C#
============

For the entirety of this course, we will be coding in C# with the help of Visual Studio IDE and .NET Core. 

.. index:: ! integrated development environment, IDE

.. _install-visual-studio:

Visual Studio
-------------

Visual Studio is an **integrated development environment (IDE)**. An IDE is like a text
editor on steroids. It not only allows you to write and edit code, but also contains many 
features that enhance the coding experience. Visual Studio offers
code completion hints, debugging, and even it's own compiler. We'll be using it throughout
this course, so it's time to get familiar with some of the basics.

.. admonition:: Note

   Visual Studio IDE is not the same application as the text editor Visual Studio Code. 
   If you already have VS Code installed on your machine, you will still need to 
   install and configure Visual Studio IDE. In this book, we will periodically refer to Visual Studio IDE
   as Visual Studio.


.. index:: ! .NET Core, ! Software Development Kit, ! SDK

.NET Core
---------

**.NET Core** is a set of tools for developing software in a number of different programming languages, including C#.
The tools together make what is known as a **software development kit**, or **SDK**.
Unlike it's predecessor, just called .NET or .NET Framework, .NET Core is open-source and available for development on several 
operating systems. The SDK provides the runtime environment, as well as the virtual machine for compiling 
and running C# programs. 
.NET Core also notably contains the class library. This is the built-in code that takes care of common programming items
like date object formatting, for example. 

.. _compiling-csharp:

A step-by-step walk-through of the process:

#. We write code in C#.
#. The source code is compiled (like translating) into another intermediate language.
#. The intermediate code is read by a runtime program included in the .NET SDK.
#. The runtime environment translates the intermediate code into machine-readable language.

Fortunately for us, .NET Core can be installed along with Visual Studio IDE.

Windows Users vs. Mac Users
---------------------------

Windows users will setup their C# development environment with a community version of Visual Studio IDE. Mac users
need to download and install a related, yet different, tool called Visual Studio for Mac. 

An important note for this class: The content of this book is designed to inform both Windows and Mac users on the 
basics of web programming in C#. There are sometimes significant, and other times more minor, discrepancies between 
how to use the IDE tools provided in Visual Studio on Windows machines and Visual Studio for Mac. We will do our 
best to provide either instructions that are application neutral, or instructions that are tailored to the development
experiences on both operating systems. There may be times when your C# project view will not look exactly like that in
the book because you are on a different operating system and are therefore using a different Visual Studio application.
The actions you take or buttons to click may be slightly different from what you see in the book.

Windows Users: Visual Studio Community Edition
----------------------------------------------

TODO: Check Windows installation steps - and screenshots? do they match any of the next steps section?

#. Download the Community version of Visual Studio IDE from `this page <https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2019>`__.

   .. admonition:: Note

      There are options for other software downloads on this page, Visual Studio Code and Visual Studio for Mac.
      Do not select either of these.

Mac Users: Visual Studio for Mac
--------------------------------

#. Check that you are using supported MacOS version `here <https://docs.microsoft.com/en-us/dotnet/core/install/dependencies?pivots=os-macos&tabs=netcore31#supported-operating-systems>`__.

#. Download `Visual Studio for Mac <https://visualstudio.microsoft.com/vs/mac/net/>`__. You may be prompted for your 
   computer's password to complete the download and begin installation.

#. The first choice you will need to make in the setup process are the development platforms you want to include in 
   the install with Visual Studio. Select **.NET Core** only.

   .. figure:: ./figures/vsmac-dotnetcore-install.png
      :alt: Visual Studio .NET Core package.

      Select .NET Core package to install.

#. Once installed, the IDE will open on it's own. If it does not, you may need to open it manually. You will next 
   see a window asking you to login to your Microsoft account. You do not need to sign-in in order to use the 
   IDE for this class and can select *I'll do this later* to continue setup.

   .. figure:: ./figures/vsmac-microsoft-account.png
      :alt: Visual Studio Microsoft sign-in page.

      Visual Studio Microsoft sign-in page.
      
#. Next you will be asked to choose which shortcut system to use. You may not have a preference yet and can always
   change this later. If you are familiar with the text editor Visual Studio Code, this may be a good starting option
   for you.

   .. figure:: ./figures/vsmac-shortcut-selection.png
      :alt: Visual Studio keyboard shortcut selection.

      Visual Studio keyboard shortcut selection.

#. Finally, you have made it to the project selection window. This will be the item you will see when you open 
   Visual Studio . You do not need to create or open a new project just yet.

   .. figure:: ./figures/vsmac-project-opener.png
      :alt: Visual Studio opening project selection pane.

      Visual Studio opening project selection pane.


You've installed Visual Studio IDE, and you're ready to start exploring its many features.


Check Your Understanding
------------------------

.. admonition:: Question

   True/False: .NET Core is the MacOS version of .NET Framework

   #. True
   #. False

.. ans: False, while .NET Core can operate in MacOS, it is not specific to that operating system

.. admonition:: Question

   .NET Core contains:

   #. A C# compiler
   #. A virtual machine
   #. Visual Studio IDE
   #. C# class library

.. ans: a, b, d. C# compiler, virtual machine, C# class library

