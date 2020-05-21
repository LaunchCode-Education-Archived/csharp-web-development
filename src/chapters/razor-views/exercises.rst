Exercises: Razor Views
======================

In this chapter, we started working on an application for tracking various
coding events around town.

Getting Started
---------------

Open up your ``CodingEvents`` project in Visual Studio. Create and checkout a new branch to 
complete these exercises. 

The code you start with should roughly resemble 
`this branch <https://github.com/LaunchCodeEducation/CodingEventsDemo>`__.
If you have been coding along with the video lessons, you're probably in good shape.

As always, give the branch a useful name, like ``view-exercises``.

Now, let's add descriptions to our events.

Expanding our Events Schedule
-----------------------------

#. In the video lessons, we learned how to use templates to display the elements in a
   static list called ``Events``. Let's convert our ``Events`` list to a ``Dictionary``.
   The structure of a dictionary enables us to add descriptions to our events. You'll 
	need to think about what data types the event name and description will be.

   .. admonition:: Tip

      If you need to refresh your memory on dictionaries, refer to :ref:`this page <dictionary>`. 
       
#. Update the ``Events/Add.cshtml`` template with a new field for a user to submit an event 
   description.

   .. admonition:: Tip

      You'll want to also add some ``label`` tags to your form to let the user know what 
      data they are entering.

#. Back in ``EventsController.cs``, add the description parameter to the ``NewEvent`` action method
   and within the method, add the new event key/value pair to the ``Events`` dictionary.

   .. admonition:: Tip

      Whatever value you provided in the ``name`` attribute of your new description field 
      is the name of the parameter.

#. Now to ``Events/Index.cshtml``. Replace the ``ul`` with a ``table`` to display event names 
   and descriptions.

#. Lastly, modify ``_Layout.cshtml`` to display links for the Coding Events app (only ``Events/Index`` and ``Events/Add`` for now).

