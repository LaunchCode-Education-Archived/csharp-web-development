Windows Users: Visual Studio Community Edition
==============================================

TODO: Check Windows installation steps - and screenshots? do they match any of the next steps section?

#. Download the Community version of Visual Studio IDE from `this page <https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2019>`__.

   .. admonition:: Note

      There are options for other software downloads on this page, Visual Studio Code and Visual Studio for Mac.
      Do not select either of these.

      Allow at least an hour for the installation process.

#. Run the installer, and select the following packages from the *Workloads* pane: 

   - ASP.NET and web development 
   - Azure development 
   - Data storage and processing 
   - .NET core cross-platform development

   Your selections will look like these screens:

   .. figure:: figures/vs-packages.png
      :alt: Install packages

      Install packages

   .. figure:: figures/vs-packages-2.png
      :alt: Install packages

      Install packages

#. When the install finishes running, select *Launch* and then close the installer window.

TODO: do we need this step?

#. When prompted, create a Microsoft Developer account and use it to sign in to Visual Studio.

#. The launcher window will prompt you with some choices via a window
   similar to what you see below. Select the displayed options. (If you
   don’t see the box about applying customizations, don’t worry about it,
   just proceed.)

   .. figure:: figures/launch-options.png
      :scale: 40%
      :alt: Launch Options

      Launch Options

.. admonition:: Note

   If you fail to install one or more of the required packages, you can do
   so by closing Visual Studio and running the installer again. Select
   *Modify* in the Visual Studio section of the window, and then
   select the additional package(s) to install.

.. admonition:: Warning

   If you don’t have this most recent version of Visual Studio
   installed, you will need to install it via the instructions above.

   If you have a pre-existing Visual Studio install, you may need to
   install the .NET Core Tools package. To do so, follow the `instructions
   provided by
   Microsoft <https://www.microsoft.com/net/core#windowsvs2017>`__.


Connect to GitHub for Windows Users
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Visit this page to download and install the `GitHub Extension for Visual
Studio <https://visualstudio.github.com/>`__.

GitHub Project Setup
~~~~~~~~~~~~~~~~~~~~
TODO: update this repo name

Visit the
`LaunchCodeEducation/csharp-exercises <https://github.com/LaunchCodeEducation/csharp-exercises>`__
repository page and fork the repository into your own GitHub account by
selecting *Fork* from the top right of the page.

After forking, open Visual Studio. From within Visual Studio, choose the
*Team Explorer* tab near the bottom of the *Solution Explorer* pane. If
you don’t see this tab, you can open it via the application menu: *View
> Team Explorer*. The first time you do this, you will need to click
*Connect…* and then sign in to GitHub.

Select *Clone* from the GitHub section of the *Team Explorer* and select
your ``csharp-exercises`` copy from the modal window. **Be sure to
change the Path field** to the location you would like the project to
live, ideally inside of a folder you’ve been using to store other
projects.


