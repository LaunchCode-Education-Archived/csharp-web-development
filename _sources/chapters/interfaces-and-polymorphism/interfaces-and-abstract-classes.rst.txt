Interfaces and Abstract Classes
===============================

We mentioned previously that interfaces share some characteristics with
abstract classes. Recall that an abstract class is one declared with the
``abstract`` keyword. You may not create an object from an abstract
class and, like an interface, an abstract class is allowed to contain
methods that only have signatures (that is, methods that don’t have
implementation code).

The main differences between interfaces and abstract classes are:

#. You *implement* an interface, while you *extend* an abstract class. The net effect of this is 
   that a class may implement interfaces while also extending a class. Note that while you can 
   implement *more than one* interface, you can only extend *one* class.
#. Abstract classes may contain non-constant fields, while interfaces can only contain constant 
   fields.
#. Abstract classes should be used to collect and specify behavior by *related* classes, while an 
   interface should be used to specify related behaviors that may be common across *unrelated* 
   classes.

   .. admonition:: Example

      Think about our ``IFeedable`` interface. If we want to 
      add a ``Dog`` class to our application, we might implement the ``IFeedable`` interface for our 
      ``Dog`` class. This makes sense as dogs are creatures that we feed. However, as dogs and cats are so 
      different, it is unlikely that they would share many characteristics through a ``Pet`` class.

Check Your Understanding
------------------------

.. admonition:: Question

   Check all statements that are TRUE about the differences between interfaces and abstract classes.

   a. You extend an abstract class, but implement an interface.
   b. You can implement many interfaces and many classes.
   c. Interfaces cannot contain non-constant fields, but abstract classes can.
   d. Methods that use instance properties can be in both interfaces and abstract classes.

.. ans: a,c. You extend an abstract class, but implement an interface. and Interfaces cannot contain non-constant fields, but abstract classes can.
