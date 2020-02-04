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
Unlike it's predecessor, just called .NET, .NET Core is open-source and available for development on several 
operating systems. The SDK provides the runtime environment, as well as the virtual machine for compiling 
and running C# programs. 

.. _compiling-csharp:

A step-by-step walk-through of the process:

#. We write code in C#, 
#. The source code is compiled (like translating) into another intermediate language,
#. The intermediate code is read by a runtime program included in the .NET SDK
#. The runtime environement translates the intermediate code into machine-readable language

Fortunately for us, .NET Core can be installed along with Visual Studio IDE.

TODO: Check Windows installation steps - and screenshots? do they match the next steps section?

First Steps: Windows Users
--------------------------

#. Download the Community version of Visual Studio IDE from `this page <https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2019>`__.

   .. admonition:: Note

      There are options for other software downloads on this page, Visual Studio Code and Visual Studio for Mac.
      Do not select either of these.

First Steps: Mac Users
----------------------

#. Check that you are using supported MacOS version `here <https://docs.microsoft.com/en-us/dotnet/core/install/dependencies?pivots=os-macos&tabs=netcore31#supported-operating-systems>`__.

#. Download `Visual Studio for Mac <https://visualstudio.microsoft.com/vs/mac/net/>`__. You may be prompted for your 
   computer's password to complete the download and begin installation.

Next Steps: All Users
---------------------

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





.. #. In the second window, select *Create project from template*. This gives us
..    some of the C# project scaffolding to save us some time with project infrastructure. 

..    .. figure:: figures/projectTemplate.png
..       :alt: Select project template

..       Select project template

.. #. On the next window, enter ``HelloWorld`` for the name of the project.
..    Click on the "3-dot" button to select a location to save the project. Here you can
..    choose the C# projects folder you created in step one. Leave the base package as
..    ``com.company``. 

..    .. figure:: figures/newProjectName.png
..       :alt: New project window for IntelliJ

..       Create the ``HelloWorld`` project in your C# projects folder.

.. #. Click *Finish* to create the project. Below is the view of your new project:

..    .. figure:: figures/newProjectView.png
..       :alt: New project view

..       Initial IntelliJ project view

..    The section on the left is the project's file tree. 

..    Clicking the triangle next to the project name, ``HelloWorld``, displays the ``src`` file, 
..    followed by the base package we created, and finally our ``Main.C#`` file. 
   
..    ``Main.C#`` is also opened on the right in this initial project view. 
   
..    In line 1, ``package com.company``, establishes a *package*, which C# uses to help
..    organize and encapsulate our code. 

.. #. We'll dive into the use of a ``main`` function and ``Main`` class later. At this point,
..    let's just get right to printing our greeting. Where the project template tells you to write your
..    code on line 6, add the following:

..    .. sourcecode:: C#

..       System.out.println("Hello, world!");

..    Ok sure, we haven't gone over this exact syntax yet. But you can take a guess at what this line will do.

.. #. To run your program in IntelliJ, you have several options.

..    .. figure:: figures/runProgram.png
..       :alt: Run code options

..       IntelliJ run code options

..    You can click on either of the green arrows indicated above, or 
..    choose *Run* from your top menu bar.

.. #. Once run, IntelliJ will generate a third panel in your view, with your program's output:

..    .. figure:: figures/output.png
..       :alt: Run code output

..       IntelliJ output

.. This is just the start of your relationship with IntelliJ. Not that we know the fundamentals,
.. let's return to C# basics so we can start writing more code.

Check Your Understanding
------------------------

.. admonition:: Question

   Given the code below, which line is responsible for printing a message?

   .. sourcecode:: C#
      :linenos:

      public class HelloWorld {

         public static void main(String[] args) {
            System.out.println("Hello, World");
         }

      }

   #. line 1
   #. line 3
   #. line 4

.. admonition:: Question

   In the sourcecode above, which line is responsible for defining the class?

   #. line 1
   #. line 3
   #. line 4

   .. index:: ! .NET SDK

.. C# Development Kit
.. ------------------

.. Installing C# means downloading a package of software called the **C# Development Kit**. The development kit contains software the tools needed 
.. to develop and run C# code. These tools 
.. together, give us the means to write, compile, and run C#
.. on our machines.

.. Install the SDK
.. ---------------

.. Open a terminal window on your machine and enter the following command:

.. .. sourcecode:: bash

..    C# -version

.. If the response returns a version 13 or higher, you can move on to the section below,
.. :ref:`terminal-C#`.

.. If you do not have a version of C# at 13 or higher or the command does not work, you can download 
.. it `here <https://www.oracle.com/technetwork/C#/C#se/downloads/jdk13-downloads-5672538.html>`__.
.. The relevant install link for your operating system is on the bottom of the page:

.. .. figure:: figures/installC#.png
..    :alt: Install C#

..    Install C#

.. To install, you must first select *Accept License Agreement*, then select any of 
.. the file type options for your operating system. 

.. .. tip::

..    - Mac users, we recommend the ``.dmg`` option
..    - Windows users, we recommend the ``.exe`` option

.. Once you have completed the 
.. installation steps, move onto the next section.

.. .. admonition:: Note

..    When installing C# on Windows, the installer will tell you where it wants to install C#.
..    The default is in the C: Drive under ``Program Files``. Make note of the destination as we will be using it later.

.. .. _terminal-C#:

.. C# in the Terminal
.. --------------------

.. Mac Users
.. ^^^^^^^^^

.. Let's write a simple "Hello, World" program and watch the JDK in action. 

.. In the future, we'll be doing most of our C# coding with the IntelliJ IDE. 
.. IntelliJ contains many features to help us write C# properly and easily, 
.. including its own compiler. For now though, we'll use a simpler text editor 
.. so we can demonstrate what we get with the JDK.

.. In the text editor of your choice, create and save a file called 
.. ``HelloWorld.C#`` and include the code below:

.. .. sourcecode:: C#
..    :linenos:

..    public class HelloWorld {

..       public static void main(String[] args) {

..          System.out.println("Hello, World");
..       }

..    }

.. We'll discuss the syntax of this program soon, but you can likely trust your gut
.. that this program has an expected output of "Hello, World". To test this hypothesis,
.. open a terminal window and navigate to the parent directory of your new file. Run:

.. .. sourcecode:: bash

..    C# HelloWorld.C#

.. You should see your greeting printed! 

.. Recall from the walk-through :ref:`above <compiling-C#>`, C# needs to be be compiled before executing. C# version 11 introduced 
.. the capability to compile single-file C# programs without explicitly running a command to compile. If our 
.. ``Hello, World`` program were more complex and contained another file, we would need to first run 
.. ``C#c HelloWorld.C#``, to compile, followed by ``C# HelloWorld.C#``.

.. Windows Users
.. ^^^^^^^^^^^^^

.. Let's write a simple "Hello, World" program and watch the JDK in action. 

.. In the future, we'll be doing most of our C# coding with the IntelliJ IDE. 
.. IntelliJ contains many features to help us write C# properly and easily, 
.. including its own compiler. For now though, we'll use a simpler text editor 
.. so we can demonstrate what we get with the JDK.

.. In the text editor of your choice, create and save a file called 
.. ``HelloWorld.C#`` and include the code below:

.. .. sourcecode:: C#
..    :linenos:

..    public class HelloWorld {

..       public static void main(String[] args) {

..          System.out.println("Hello, World");
..       }

..    }

.. We'll discuss the syntax of this program soon, but you can likely trust your gut
.. that this program has an expected output of "Hello, World". 

.. To test this hypothesis, open a terminal window and navigate to the parent directory of your new file.
.. In a separate window, navigate to the ``bin`` folder in the C# Development Kit to get the file path (the image below shows you how to get there from the C: Drive). Copy the file path.

.. .. figure:: figures/windowsC#filepath.png
..    :alt: Image showing that the JDK can be found inside the Program Files directory in the C: Drive.

.. Run the following command, replacing the ``{filepath}`` with the file path to your JDK that you just copied:

.. .. sourcecode:: bash

..    set path=%path%;{filepath}

.. This command sets a path in our system for ``C#`` so that we can compile and run C# programs.

.. .. sourcecode:: bash

..    C# HelloWorld.C#

.. You should see your greeting printed! 

.. Recall from the walk-through :ref:`above <compiling-C#>`, C# needs to be be compiled before executing. C# version 11 introduced 
.. the capability to compile single-file C# programs without explicitly running a command to compile. If our 
.. ``Hello, World`` program were more complex and contained another file, we would need to first run 
.. ``C#c HelloWorld.C#``, to compile, followed by ``C# HelloWorld.C#``.

.. .. admonition:: Note

..    These steps change the path in just that directory.
..    While this is sufficient to get us through the rest of the course, you may want change the system path for your whole system.
..    Check out these `instructions <https://www.C#.com/en/download/help/path.xml>`_ to change the path globally.

.. .. index:: ! integrated development environment, IDE
