.. _mvc:

Design Patterns, MVC, and Spring, Oh My!
========================================

.. index:: ! design pattern, ! Model-View-Controller, ! MVC, ! model, ! view, ! controller

So far, we have been designing our applications by diagrammming classes, drawing connections, and abstracting via interfaces.
This practice benefits us because we can start seeing issues *before* we start coding.
Many software developers start their applications with this process.
Before we start diagramming our ``Cat`` class and our ``HouseCat`` class, we decide on the template for our design that we want to use.
These design templates that are abstract solutions to common software architecture problems are called **design patterns**.
Design patterns provide a set of conventions that we follow to build an application.

**Model-View-Controller** (MVC) is a design pattern where the programming logic behind the application is broken down into 3 components: models, views, and controllers.
A **model** handles the data and business logic of the application. A **view** handles the user interface elements.
A **controller** passes information from the models to the views. Controllers are the traffic cops of the application, capable of passing data back and forth to the browser in MVC web applications. This process will be covered in depth later on in this chapter.

.. figure:: figures/mvcOverview.png
   :alt: Figure showing that controllers handle traffic between models and views, but models do not interact with views.

Because MVC breaks down all of the programming logic of an application into three digestable components, we can use this particular design pattern to make extensible applications.
We also use MVC because it separates the components of the programs that the user interacts with from the underlying business logic.

.. index:: ! ASP.NET, ! ASP.NET MVC

ASP.NET
-------

**ASP.NET** is an extension of .NET core and is used to build web applications.
**ASP.NET MVC** is the framework that allows us to build web applications in a way that uses the MVC design pattern.
Visual Studio has an embedded server so it is easy for us to run our applications and get started.
The server picks a random port number to host the application at, which is why it is important to take note of the port number that your application runs at.

.. admonition:: Note

   Whenever we navigate to ``localhost:portnumber``, make sure that you are navigating to the appropriate port number for your server.
   Your port number may be different from the examples in the book.

How we Teach ASP.NET
--------------------

The following section is the first of many videos we will be using to demonstrate coding an ASP.NET application.
The video below introduces the role of controllers.
In subsequent videos, we ask you to code along for maximum absorption of the topics introduced.
A summary of the content introduced will follow each video.

Intro to ASP.NET - Video
------------------------

.. TODO: Add video called "Hello ASP.NET Intro"