Mac Users: Visual Studio for Mac
================================

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

GitHub Project Setup
~~~~~~~~~~~~~~~~~~~~
TODO: update repo name

#. Visit the `LaunchCodeEducation/csharp-exercises <https://github.com/LaunchCodeEducation/csharp-exercises>`__
   repository page and fork the repository into your own GitHub account by
   selecting *Fork* from the top right of the page.

#. With Visual Studio open, select *Version Control > Checkout* from the menu bar. 

#. This opens a window to connect to a remote repository. Copy the address for your forked exercises repository 
   and enter it into the *url* section of the form. The rest of the form fields will auto-populate:

   .. figure:: ./figures/vsmac-checkout-github.png
      :alt: Visual Studio for Mac checkout Github repository

      Visual Studio for Mac checkout Github repository

#. Enter the *Target Directory* where you would like to keep your project

   .. admonition:: Tip
   
      Make this a new, empty folder that you will easily find when you want to open the project next.


