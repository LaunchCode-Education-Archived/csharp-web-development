Models in MVC
==============

In the previous chapter, you learned about Razor, which displays data and an
interface for a user. Before that, you learned about :ref:`controllers`. Remember that controllers
determine what data to send to the the views. This data needs to come from some source 
and take some shape. Cue the models.

What is a Model?
-----------------

.. index:: model, ! business logic

A **model** represents the logic for accessing and storing the data used in an application. 
Properly constructed, models do not depend on any controllers or views. Models should be classes that 
are easy to reuse without modification.

Models are not the data itself, but rather the logic that moulds the data for a particular
purpose. They dictate how we want to handle the data in an application-specific way. The data used in 
an application is often sourced from a database or an external data service. Data is typically 
application-agnostic. It is the work of the models we write to shape raw data into useful 
application information. This shaping of data to for the needs of a program is part of what is referred 
to as the **business logic**.

Consider a physical address book (a model). The pages contain blank lines for names and addresses. 
Anyone (a controller) can pick up the book, retrieve the information, and write to the contact. 
The address book model does not depend on who picks it up and enters their contacts. The book just 
provides organization and storage logic. On the flip side, the same person can input the same contact 
data into a different book. So a model transforms raw information  into something useful for a particular 
application.

MVC: Putting it Together
------------------------

.. figure:: figures/mvcOverviewDetail.png
   :scale: 50%
   :alt: Diagram of the MVC flow showing summaries of responsibilities for the three components.

   Each MVC node carries its own responsibilities.

Model
~~~~~
Shapes data to fit the needs of an application.

View
~~~~
Displays data to the user. Via events, the user interacts with the view and updates the program 
data. The view communicates with the controller but not the model.

Controller
~~~~~~~~~~
Directs the flow of information between the view and the
model. It does not store the data or determine how to display it for the
user. It passes information retrieved from the view to update the model. 
And it passes information retrieved from the model to update the view.

.. admonition:: Tip

   Need further review? Check out `MVC for Noobs <https://code.tutsplus.com/tutorials/mvc-for-noobs--net-10488>`__.

Model vs. Controller
--------------------

At this point, it might be tough to decide what code belongs in the model and what belongs in the 
controller. Here are some general guidelines. Any code that transfers data or responds to user 
actions belongs in the controller. Code that retrieves data from a database or organizes that 
data belongs with the model.

So far, ``CodingEvents`` handles all data inside of controller classes. However, most 
data manipulation should occur in model classes. So we need to make a distinction between these 
actions. For any manipulations that must occur regardless of a user's actions, that code belongs 
in the model. For changes that vary depending on a user’s input, that code belongs in the controller.

Model code defines the logic for processes that the user never needs to see.
These include:

#. The mechanics for storing data.
#. The mechanics for retrieving data.
#. The mechanics for organizing data.
#. Updating or manipulating the data independent of any controller or view
   actions.

Controller code handles *requests* made by the user. These include:

#. "Please retrieve this information from the model.",
#. "Please store this according to the rules of the model.",
#. "Please delete this item.",
#. "Please change this item.",
#. "Please display this.",
#. "Please modify this data in a novel way".

Remember, the controllers are the traffic cops. These classes direct information from one place to 
another. Like a model, a controller does not permanently store data. Instead, it either sends the 
information to the model for shaping or to the view for display.

Check Your Understanding
------------------------

.. admonition:: Question

   If we use baking as an analogy for an MVC project, which of the
   following items best represents a model?

   a. The bread ingredients: flour, water, yeast, salt
   b. Mixing and shaping the ingredients together
   c. Baking the loaves into the final product
   d. Eating the bread

.. Answer: b, Mixing and shaping the ingredients together

.. admonition:: Question

   If we use a library as an analogy for an MVC project, which of the
   following items best represents a model?

   a. The books on the shelves
   b. The Dewey Decimal storage system
   c. The librarians
   d. The book readers

.. Answer: b, The Dewey Decimal storage system

