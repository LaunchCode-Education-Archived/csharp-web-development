.. _testinginheritance:

Testing Inheritance
===================

Not sure you get the whole inheritance idea? Still not sure which fields and methods get inherited and 
which are overridden? Looking to *test* your understanding?

Knowing what we know now about :ref:`unit-testing` and :ref:`inheritance`, we can test that our 
subclasses extend their base classes.

We can add a ``CatTests`` project to our ``Cats`` solution and write some code to ensure that 
``HouseCat`` inherits what we expect it to.

.. sourcecode:: csharp
   :linenos:

   [TestMethod]
   public void InheritsBaseInFirstConstructor()
   {
      HouseCat keyboardCat = new HouseCat("Keyboard Cat", 7);
      Assert.AreEqual(7, keyboardCat.Weight, .001);
   }

Here, we're testing that one of our ``HouseCat`` constructors will call the ``Cat`` constructor
and appropriately assign the ``HouseCat`` object's ``weight`` field. Remember, we don't need
to write unit tests for getters or setters unless they do something extra in addition to getting
or setting the field. The purpose of this test, though, is less to test getting ``keyboardCat.Weight`` 
and more to validate that the subclass constructor has inherited the base class constructor.

It's a good practice to test your subclasses to verify the items that they inherit or override.

Check Your Understanding
------------------------

.. admonition:: Question

   Fill in the blank to test that the no-argument constructor of ``Cat`` is called when the second 
   constructor on ``HouseCat`` is used?

   Second ``HouseCat`` constructor:

   .. sourcecode:: csharp
      :lineno-start: 14

      public HouseCat(string name)
      {
         Name = name;
      }

   .. sourcecode:: csharp
      :linenos:

      [TestMethod]
      public void InheritsDefaultCatInSecondConstructor()
      {
         HouseCat keyboardCat = new HouseCat("Keyboard Cat");
         // <insert assertion method here>
      }

   a. ``Assert.AreEqual(13, keyboardCat.Weight);``

   b. ``Assert.IsNotNull(keyboardCat.Weight);``

   c. ``Assert.AreEqual(13, keyboardCat.Weight, .001);``

   d. ``Assert.IsNotNull(keyboardCat.weight);``

.. ans c, ``Assert.AreEqual(13, keyboardCat.Weight, .001);``

.. admonition:: Question

   What additional assert method can we add to this test to properly verify that ``HouseCat``
   inherits ``Eat()``?

   .. sourcecode:: csharp
      :linenos:

      [TestMethod]
      public void IsNotInitiallyTired()
      {
         HouseCat keyboardCat = new HouseCat("Keyboard Cat");
         Assert.IsFalse(keyboardCat.Hungry);
         Assert.IsFalse(keyboardCat.Tired);
         keyboardCat.Eat();
      }

   a. ``Assert.IsFalse(keyboardCat.Tired);``

   b. ``Assert.IsTrue(keyboardCat.Tired);``

   c. ``Assert.IsTrue(keyboardCat.Hungry);``

   d. ``Assert.IsFalse(keyboardCat.tired);``

.. ans b, ``Assert.IsTrue(keyboardCat.Tired);``

