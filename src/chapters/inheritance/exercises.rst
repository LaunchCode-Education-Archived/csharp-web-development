Exercises: Inheritance
======================

Work on these exercises in a new Visual Studio .Net Core console app. 
Name your project within the solution ``technology``.

#. **Class design:** Create three classes inside your solution: ``Computer``, ``Laptop`` and ``SmartPhone``.
   Before you start coding anything inside these classes, diagram how the three classes are going to be related 
   to each other. Remember to add properties and methods to your diagram.

   #. For a parent class: add 3 properties, 2 methods, and a constructor.
   #. For a child class: add *at least* 1 additional property and 1 additional method.

#. **Class implementation:** Implement your design and test it in a ``Program.cs`` class.
   
   #. Add a new MSTest project to your solution
   #. Try to add three MSTests tests per class.

#. **Abstract class design:** Consider the group of classes that you designed. Suppose you have a web program 
   that uses these classes and you need to assign a unique ID to every object created from them. 
   Each class should have an ``Id`` field, and no two objects created from any of the classes may have the 
   same value for ``Id``. Create an abstract class, ``AbstractEntity``, that contains the behavior for 
   assigning and accessing such a unique ID for each class that extends it. Add this class to your ``technology``
   project above, and add ``AbstractEntity`` to the class hierarchy in the correct place.

