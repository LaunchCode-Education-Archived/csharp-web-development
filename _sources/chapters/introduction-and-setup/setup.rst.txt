Setup For C#
============

For the entirety of this course, we will be coding in C# with the help of Visual Studio and .NET. 

.. index:: ! integrated development environment, IDE

.. _install-visual-studio:

The Integrated Development Environment 
--------------------------------------

Visual Studio (VS) is an **integrated development environment (IDE)**. 
An IDE is like a text editor on steroids. 
We can write and edit code *and* make use of additional features that enhance our coding experience. 
VS offers code completion hints, debugging, and even it's own compiler. 

We'll be using it throughout this course, so it's time to get familiar with some of the basics.

.. admonition:: Note

   Visual Studio IDE is *not* the same application as the source-code editor called Visual Studio Code (VS Code). 
   If you already have VS Code installed on your machine, you will still need to install and configure VS.


.. _dotnet-intro: 

.. index:: ! .NET, ! Software Development Kit, ! SDK

Development Frameworks
----------------------

.NET
^^^^

**.NET** is a set of tools for developing software in a number of different programming languages, including C#.
The tools together make what is known as a **software development kit**, or **SDK**.

Some of its featuers:

* Open-source and available on several operating systems.
* The SDK provides the runtime environment and the virtual machine for compiling and running C# programs. 
* Contains the **base class libraries** which include the built-in code that takes care of common programming items, such as object types.
* Able to be extended using additional frameworks such as ASP.NET.

You can learn more about .NET `here <https://dotnet.microsoft.com/en-us/learn/dotnet/what-is-dotnet>`_.

ASP.NET Core
^^^^^^^^^^^^

As we progress through this portion of the course, we will start creating web projects.  
.NET will compile C#, but does not contain any libraries for web development.  
ASP.NET Core is an open source collection of libraries specifically for web development and creating dynamic web applications.

We will use ASP.NET Core midway through this course; however, you can to learn more about this framework at `this <https://dotnet.microsoft.com/en-us/learn/aspnet/what-is-aspnet-core>`_ site.

.. _compiling-csharp:

C# and the Frameworks
---------------------

A summary of the relationship between the code you write in C# and tools provided by .NET:

#. We write code in C#.
#. The source code is compiled (like translating) into another intermediate language.
#. The intermediate code is read by a runtime program included in the .NET SDK.
#. The runtime environment translates the intermediate code into machine-readable language.

Fortunately for us, .NET can be installed along with Visual Studio IDE.

Windows Users vs. Mac Users
---------------------------

Windows users will setup their C# development environment with a community version of Visual Studio. Mac users
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
   
   Visual Studio is a framework. 

   #. True
   #. False

.. ans: False, Visual Studio is an IDE.  The .NET and ASP.NET Core are frameworks that we use inside Visual Studio. 

.. admonition:: Question

   .NET contains:
   (Select all that apply)

   #. A C# compiler
   #. A virtual machine
   #. Visual Studio IDE
   #. C# class library

.. ans: a, b, d. C# compiler, virtual machine, C# class library

