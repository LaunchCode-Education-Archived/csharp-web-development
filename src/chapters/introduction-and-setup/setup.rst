Setup For C#
============

For the entirety of this course, we will be coding in C# with the help of Visual Studio IDE and .NET Core. 

.. index:: ! integrated development environment, IDE

.. _install-visual-studio:

Visual Studio
-------------

Visual Studio is an **integrated development environment (IDE)**. An IDE is like a text
editor on steroids. We can write and edit code *and* make use of additional features that 
enhance our coding experience. Visual Studio offers
code completion hints, debugging, and even it's own compiler. We'll be using it throughout
this course, so it's time to get familiar with some of the basics.

.. admonition:: Note

   Visual Studio IDE is not the same application as the text editor called Visual Studio Code. 
   If you already have VS Code installed on your machine, you will still need to 
   install and configure Visual Studio IDE. In this book, we will periodically refer to Visual Studio IDE
   as Visual Studio.


.. _dotnet-intro: 

.. index:: ! .NET Core, ! Software Development Kit, ! SDK

.NET Core
---------

**.NET Core** is a set of tools for developing software in a number of different programming languages, including C#.
The tools together make what is known as a **software development kit**, or **SDK**.
Unlike it's predecessor, just called .NET or .NET Framework, .NET Core is open-source and available on several 
operating systems. The SDK provides the runtime environment and the virtual machine for compiling 
and running C# programs. 
.NET Core also notably contains the class library. This is the built-in code that takes care of common programming items,
such as object types.

.. _compiling-csharp:

A summary of the relationship between the code you write in C# and tools provided by .NET Core:

#. We write code in C#.
#. The source code is compiled (like translating) into another intermediate language.
#. The intermediate code is read by a runtime program included in the .NET SDK.
#. The runtime environment translates the intermediate code into machine-readable language.

Fortunately for us, .NET Core can be installed along with Visual Studio IDE.

Windows Users vs. Mac Users
---------------------------

Windows users will setup their C# development environment with a community version of Visual Studio IDE. Mac users
need to download and install a different version of Visual Studio called Visual Studio for Mac. While the names of 
these two programs are very similar, the user-experiences are quite different.

An important note for this class: The content of this book is designed to inform both Windows and Mac users on the 
basics of web programming in C#. There are sometimes significant, and other times more minor, discrepancies between 
how to use the IDE tools provided in Visual Studio on Windows machines and Visual Studio for Mac. We will do our 
best to provide either instructions that are application neutral, or instructions that are tailored to the development
experiences on both operating systems. There may be times when your C# project view will not look exactly like that in
the book because you are on a different operating system and are therefore using a different Visual Studio application.
The actions you take or buttons to click may be slightly different from what you see in the book.


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

