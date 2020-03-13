Exercises: Unit Testing
=======================

Work on these exercises in your local copy of the `csharp-web-dev-lsn5unittesting <https://github.com/LaunchCodeEducation/csharp-web-dev-lsn5unittesting>`_ repo.
You were directed to fork and clone this repo earlier in the chapter. If you have not done so, do so now!
Before starting work on the exercises, check out the ``exercises-start`` branch.

.. admonition:: Tip

   Earlier in the chapter, we instantiated an object of the ``Car`` class called ``test_car``.
   Be sure to take note of the values of the ``make``, ``model``, ``gasTankSize``, and ``milesPerGallon`` fields!
   Having a note you can quickly reference of how big the gas tank is will you help you decide on values to use in your tests!

``TestGasTankAfterDriving()``
-----------------------------

Add a test for the third TODO, "GasTankLevel is accurate after driving within tank range".

#. Your test must use the ``Car`` method ``Drive()`` 

   .. sourcecode:: csharp

      test_car.Drive(50);

#. With a value of ``50`` miles passed into ``Drive()``, we expect 
   ``test_car`` to have a ``GasTankLevel`` of ``9``.

   .. sourcecode:: csharp

      Assert.AreEqual(9, test_car.GasTankLevel, .001);

``TestGasTankAfterExceedingTankRange()``
----------------------------------------

Add a test for the fourth TODO, "GasTankLevel is accurate after attempting to drive past tank range".

#. You're on your own for this one. You'll need to simulate the ``Car``
   travelling farther than it's ``gasTankLevel`` allows.

``TestGasOverfillException()``
------------------------------

The test for our last TODO is a little different. We are going to 
perform an action on our car object, and we are expecting the object 
to throw an error. In this case, we are going to attempt to add gas 
to our car that exceeds the gas tank size.

#. First, we'll add our ``[TestMethod]`` annotation to tell MSTest
   this is a test. 

   .. sourcecode:: csharp

      //TODO: can't have more gas than tank size, expect an exception
      [TestMethod]
      public void TestGasOverfillException() {

      }

#. Now we need to tell MSTest the test passes if an exception is thrown. We will use a new attribute ``[ExpectedException]``.

   .. sourcecode:: csharp

      //TODO: can't have more gas than tank size, expect an exception
      [TestMethod]
      [ExpectedException(typeof(ArgumentOutOfRangeException))]
      public void TestGasOverfillException() {

      }
   

#. Update the ``Car`` class to include an ``AddGas()`` method.

   .. sourcecode:: csharp

      public void AddGas(double gas) {
        GasTankLevel += gas;
      }

#. Back in ``CarTests``, implement the new ``AddGas()`` method and a 
   ``Assert.Fail()`` scenario.

   .. sourcecode:: csharp

      test_car.AddGas(5);
      Assert.Fail("Shouldn't get here, car cannot have more gas in tank than the size of the tank");

#. Run the test. It should fail! In the output log, we can see our 
   ``Assert.Fail()`` statement about not being able to add more gas printed out.

#. We need to refactor ``Car`` to throw an exception when too much
   gas is added to the tank. Find the ``AddGas()`` method and
   modify it by adding the following code in the appropriate place.

   .. sourcecode:: csharp

      if (GasTankLevel > GasTankSize)
      {
         throw new ArgumentOutOfRangeException("Can't exceed tank size");
      }

#. Now, run the test - it should pass!

   












