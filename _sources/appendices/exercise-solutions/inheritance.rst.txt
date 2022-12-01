Exercise Solutions: Inheritance
===============================

Line numbers are for reference. They may not match your code exactly.

Class Design
------------

.. _inheritance-solution-1:

.. figure:: figures/InheritanceExDiagram.png
   :scale: 50%
   :alt: Quick design plan of 1 parent class and 2 child classes

This is *one* example of how 1 base class (``Computer``) and 2 derived classes (``Laptop`` & ``Smartphone``) can use inheritance.

1. Using the diagram above, set up the base class: ``Computer``.

* Testing the ``Computer`` class.

.. sourcecode:: csharp
   :linenos:
   
      public class Computer
      {
         public double Ram { get; set; }
         public double Storage { get; set; }
         public readonly bool hasKeyboard;
         
         public Computer(double ram, double storage, bool hasKeyboard)
         {
            Ram = ram;
            Storage = storage;
            this.hasKeyboard = hasKeyboard;
         }
         
         public double IncreaseRam(double extraRam)
         {
            return Ram += extraRam;
         }
         
         public double IncreaseStorage(double extraStorage)
         {
         return Storage += extraStorage;
         }
      }


*  Use inheritance to create the ``Laptop`` derived class. 

.. sourcecode:: csharp
   :linenos:
   
      public class Laptop : Computer
      {
         public double Weight { get; set; }
         
         public Laptop(double ram, double storage, bool hasKeyboard, double weight) : base(ram, storage, hasKeyboard)
         {
         Weight = weight;
         }
         
         public bool IsClunky()
         {
            if (Weight > 5.0)
            {
               return true;
            }
               else
            {
               return false;
            }
         }
      }

:ref:`Back to the exercises <inheritance-exercises>`

Class Implementation
--------------------

.. _inheritance-solution-2:

1. Add a new MSTest project to your solution.

.. sourcecode:: csharp
   :linenos:
   
      // one Computer class tests in the Computer Class
      [TestMethod]
      public void TestIncreasingRam()
      {
         Computer testingComputer = new Computer(2, 3, true);
         Assert.AreEqual(2, testingComputer.Ram);
         testingComputer.IncreaseRam(3);
         Assert.AreEqual(5, testingComputer.Ram);
      }

2. Try to add three MSTest tests to each class.  Consider testing each method or field.

*  Testing the ``Smartphone`` class

.. sourcecode:: csharp
   :linenos:
      
      //Smartphone Class
      [TestMethod]
      public void TestTakingSelfies()
      {
         SmartPhone testingSmartphone = new SmartPhone(2, 3, true, 800);
         testingSmartphone.TakeSelfie();
         Assert.AreEqual(801, testingSmartphone.NumberOfSelfies);
      }

:ref:`Back to the exercises <inheritance-exercises>`

Abstract class design
---------------------

.. _inheritance-solution-3:

1. Create the ``AbstractEntity`` Class.  

.. sourcecode:: csharp
   :linenos:
   
      // AbstractEntity Class
      public class AbstractEntity
      {
         public int Id { get; set; }
         private static int nextId = 1;

         public AbstractEntity()
         {
            Id = nextId;
            nextId++;
         }
      }

2. Update the ``Computer`` class.  Remember ``Computer`` extends ``AbstractEntity``.
  
.. sourcecode:: csharp
   
   public class Computer : AbstractEntity


Testing ``AbstractEntity`` using MSTest:

3. Testing the ``Computer`` Class 

.. sourcecode:: csharp
   :linenos:
   
      //Computer Class
      [TestMethod]
      public void TestInheritsId()
      {
         Computer testingComputer = new Computer(2, 3, true);
         Assert.AreEqual(1, testingComputer.Id);

         Computer testingComputer2 = new Computer(4, 6, true);
         Assert.AreEqual(2, testingComputer2.Id);
      }

4. Testing the ``Smartphone`` class

.. sourcecode:: csharp
   :linenos:
   
      //Smartphone class
      [TestMethod]
      public void TestInheritingBaseConstructor()
      {
         SmartPhone testingSmartphone = new SmartPhone(2, 3, true, 800);
         Assert.IsNotNull(testingSmartphone.Id);
         //...
      }   

:ref:`Back to the exercises <inheritance-exercises>`