Exercise Solutions: Unit Testing
================================

Line numbers are for reference. They may not match your code exactly.

.. _unit_testing_solution-1: 

``TestGasTankAfterDriving()``
-----------------------------

Add a test for the third TODO, "GasTankLevel is accurate after driving within tank range".

.. sourcecode:: csharp
   :linenos:
   
      [TestMethod]
      public void TestGasTankAfterDriving()
      {
         test_car.Drive(50);
         Assert.AreEqual(9, test_car.GasTankLevel, .001);
      }

:ref:`Back to the exercises <unit_testing-exercises1>`

.. _unit_testing_solution-2: 

``TestGasTankAfterExceedingTankRange()``
----------------------------------------

Add a test for the fourth TODO, "GasTankLevel is accurate after attempting to drive past tank range".

#. You're on your own for this one. You'll need to simulate the ``Car``
   travelling farther than it's ``gasTankLevel`` allows.

.. sourcecode:: csharp
   :linenos:
   
      [TestMethod]
      public void TestGasTankAfterExceedingTankRange()
      {
         test_car.Drive(501);
         Assert.AreEqual(test_car.GasTankLevel, 0, .001);
      }

:ref:`Back to the exercises <unit_testing-exercises2>`

.. _unit_testing_solution-3: 

``TestGasOverfillException()``
------------------------------
The test for our last TODO is a little different. We are going to 
perform an action on our car object, and we are expecting the object 
to throw an error. In this case, we are going to attempt to add gas 
to our car that exceeds the gas tank size.


2. Now we need to tell MSTest the test passes if an exception is thrown. We will use a new attribute ``[ExpectedException]``.

.. sourcecode:: csharp
   :linenos:
   
      //TODO: can't have more gas than tank size, expect an exception
      [TestMethod]
      [ExpectedException(typeof(ArgumentOutOfRangeException))]
      public void TestGasOverfillException() 
      {
      
      }

:ref:`Back to the exercises <unit_testing-exercises3>`   

4. Back in ``CarTests``, implement the new ``AddGas()`` method and a 
   ``Assert.Fail()`` scenario.

.. sourcecode:: csharp
   :linenos:
   
      //TODO: can't have more gas than tank size, expect an exception
      [TestMethod]
      [ExpectedException(typeof(ArgumentOutOfRangeException))]
      public void TestGasOverfillException()
      {
         test_car.AddGas(5);
         Assert.Fail("Shouldn't get here, car cannot have more gas in tank than the size of the tank");
      }

:ref:`Back to the exercises <unit_testing-exercises3>`

6. We need to refactor ``Car`` to throw an exception when too much
   gas is added to the tank. Find the ``AddGas()`` method and
   modify it by adding the following code in the appropriate place.

.. sourcecode:: csharp
   :linenos:
   
      public void AddGas(double gas)
      {
         GasTankLevel += gas;
         if (GasTankLevel > GasTankSize)
         {
            throw new ArgumentOutOfRangeException("Can't exceed tank size");
         }
      }

:ref:`Back to the exercises <unit_testing-exercises3>`
