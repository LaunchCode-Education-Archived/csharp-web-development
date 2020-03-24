Unit Testing and Interfaces
===========================

After all that we have learned about interfaces, perhaps you are wondering, *how do I write my unit tests with interfaces?*

The best practices to testing interfaces are very similar to those of :ref:`testing inheritance <testinginheritance>`. You want to focus on testing the contract 
that the interface is supposed to be upholding as opposed to the interface itself.

.. admonition:: Example

   We have an ``IFeedable`` interface and a ``HouseCat`` class.

   .. sourcecode:: c#
      :linenos: 

      public interface IFeedable
      {
         string Eat()
         {
            return "the feedable is eating";
         }
      }

      public class HouseCat : IFeedable
      {
         public string Name { get; set; }
         public HouseCat(string name)
         {
            Name = name;
         }
      }

   Based on the class above and the interface it implements, we should expect that a call to ``.Eat()`` on an instance of 
   a ``HouseCat`` will return the default implementation.

   .. sourcecode:: c#
      :linenos: 

      [TestClass]
      public class CatTests
      {
         [TestMethod]
         public void TestHouseCatImplementsEatMethod()
         {
            IFeedable test_cat = new HouseCat("test");
            Assert.AreEqual("the feedable is eating", test_cat.Eat()); 
            // This test passes. Don't believe us? Try it yourself!
         }
      }

   In this situation, we test the contract that the interface is supposed to be upholding, but not the interface itself.
   While there are strategies to test interface code itself using *mock objects*, we won't approach those tactics in this course. 

Check Your Understanding
------------------------

.. admonition:: Question

   True or False: A class ``PetDog`` also implements ``IFeedable`` and contains its own ``Eat()`` method. Should we test that method's results?

   #. No, the interface contract will not be tested in this scenario.
   #. Yes, testing the class's custom methods is always a worthy endeavor.
   
.. ans: b, testing the class's custom methods is always a worthy endeavor.
