.. How do you make a new template for your app?

Creating a Template
====================

Using templates is a useful way to reduce the effort required to create and
maintain a web-based project. Before you can dive into using templates,
however, you need to take care of a little groundwork first.

Razor
-----

.. index:: ! Razor

**Razor** is a templating syntax included in the application framework for our MVC project. 
It allows us to write C# code directly into an HTML tree. 

More information on Razor can be found 
`here <https://docs.microsoft.com/en-us/aspnet/core/mvc/views/razor?view=aspnetcore-3.1>`__.

For the most part, Razor templates look and operate just like
regular HTML code. Any C# logic we add to a template is preceded with 
the ampersand symbol, ``@``. You can open any template in a browser and view it just
like a static HTML file. 

In this chapter, you will construct some small practice projects to help you
learn how to implement Razor templates. 

Start a Practice Project
-------------------------

Open up your ``HelloASPDotNET`` project in Visual Studio and code along with the
following video.

.. admonition:: Warning

   The videos in this chapter walk you through building small web-based
   projects. Do NOT skip this practice, because the end of chapter exercises
   pick up where the tutorials end.

.. TODO: Add static view video. 
   .. topics covered: Demonstrate how templates are already being returned in homecontroller, 
   creating simple form template, updating controller to return view template

.. YOUTUBE VIDEO HERE

.. TODO: add branches

.. admonition:: Note

   The starter code for this video is found at: <starter-branch>. The final code persented in this 
   video is found at <end-branch>.

The sections below outline the main ideas presented in the video. However, the
text is NOT a substitute for completing the work described in the clip.

.. index:: ! View() method

Controllers Return View Templates
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Out of the box, your MVC project contains several Razor templates within the ``Views`` directory.
The sub-directory ``Home``, found inside of ``Views``, contains the Razor templates returned from the 
``HomeController`` action methods. Just as an action method's name will map to a route with the same 
name, an action method's name can also correspond to a Razor template's name. The ``Index()`` method 
inside of ``HomeController`` returns the ``Index.cshtml`` template found inside of ``Views/Home``.
In order to return that template, the action method calls a **View() method**.

Add a Template
^^^^^^^^^^^^^^^

To create a template, we update ``HelloController.Index()`` to return a Razor template instead of a 
string of HTML. In ``Views``, create a new subdirectory called ``Hello``. 

.. TODO: check which file type to select from menu.

Within ``Hello`` create a new file called ``Form.cshtml``. Add the from HTML to the template.
Update the ``HelloController`` method ``Form()`` to return ``View()``. 


Check Your Understanding
------------------------

.. admonition:: Question

   How is C# code indicated in Razor templates?

   #. A C# compiler
   #. It is preceded by an octothorpe symbol, ``#``
   #. It is preceded by an ampersand symbol, ``@``
   #. It is enclosed in curly brackets, ``{}``

.. ans: c, It is preceded by an ampersand symbol, ``@``

.. admonition:: Question

   What is the file type for Razor templates?

   #. razor
   #. rzr
   #. html
   #. cshtml

.. ans: d, cshtml



.. TODO: the ASP rough equivalent here is the layout file. I think this makes sense to introduce this idea 
.. once the more basics above have been established and perhaps once bootstrap is introduced. Commenting out this 
.. section for now in case we want to adapt it to fit later

.. Razor Template
.. -------------------

.. As described in the video, you can save yourself some time by creating your own
.. boilerplate code for a Razor template. This will save you from having to
.. make the edits described above every time you add a new base html file.

.. #. Right-click on the ``templates`` folder (or any other directory), and select
..    *New --> Edit File Templates*.
.. #. In the window that pops up, click the "+" icon to add a new file.

..    .. figure:: ./figures/createNewTemplate.png
..       :alt: Icon to click to create a new Razor template.
..       :scale: 80%

.. #. Name your template, set the extension as ``html``, then edit the starter
..    code. This will be the boilerplate HTML that appears anytime you select your
..    custom template. For Razor, the code should at least close the ``meta``
..    tag and include the ``xmlns`` attribute.

..    .. figure:: ./figures/RazorTemplateCode.png
..       :alt: Editor pane for setting Razor template code.

..    If you find yourself routinely using other code in your Razor files, you
..    can return to this window and edit the HTML as needed. Don't forget to save
..    your changes.
.. #. To use your custom Razor template, right-click on the ``templates``
..    folder and select *New --> TemplateName*.

..    .. figure:: ./figures/selectRazorTemplate.png
..       :alt: Menu options for selecting a custom Razor template.
