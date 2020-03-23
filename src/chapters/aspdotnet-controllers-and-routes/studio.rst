Studio: Skills Tracker
======================

Wouldn't it be nice to have a small tracker to show us what skills we have built and where we are at in learning them?
Let's build something that would let us do just that!

As always, read through the whole studio before starting.

At the end of the studio, your final project should be able to take input from a user via a form and post the information 
in a way that is easy to read.

Create the MVC Project
----------------------

In Visual Studio, create a new ASP.NET project using the *Web Application (Model-View-Controller)* option. Name your 
new project ``SkillsTracker``. Once created, run the project and go to ``localhost:5001`` to ensure that there are no 
underlying build errors to fix before coding. Now you are ready to start tracking skills.

Creating Controllers
--------------------

In your project, add a class called ``SkillsController`` inside of the ``Controllers`` folder.
Inside ``SkillsController``, you will add several methods to accomplish the following:

#. At ``localhost:5001``, add text that states the three possible programming languages someone could be working on.
   You need to have an ``h1`` with the title "Skills Tracker", an ``h2``, and an ``ol`` containing three programming languages 
   of your choosing.
#. At ``localhost:5001/form``, add a form that lets the user enter their name and choose their favorite, second favorite, and 
   third favorite programming languages on your list. Use ``select`` elements for each of the rankings. Just as we did in 
   the exercises, we will use a ``GET`` request.
#. Also at ``localhost:5001/form``, use ``[HttpPost]`` and request parameters to update the HTML with an ``h1`` stating the 
   user's name and an ``ol`` showing the three programming languages in the order they chose.

End Result
----------

At the end of the studio, when you navigate to ``localhost:5001``, you should see the following:

.. figure:: figures/studio-home-page.png
   :alt: Image showing functioning home page.

   Skill Tracker app home page.

When you navigate to ``localhost:5001/form``, you should see a blank form that looks something like: 

.. figure:: figures/blank-studio-form.png
   :alt: Image showing the blank form.

   Skill Tracker app blank skill form.

If you fill out the form, your page may render like so:

.. figure:: figures/completed-studio-form.png
   :alt: Image showing the web page with information from the completed form.

   Skill Tracker app result of skill form submission.

Bonus Missions
--------------

#. Reformat your ``form`` page to use a table instead of an ordered list.
#. Add a new path to the site to display the information from the completed form.