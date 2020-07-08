A Tale of Two Cats 
==================

Let’s revisit our ``Cat`` and ``HouseCat`` friends.
Check out this `repository <https://github.com/LaunchCodeEducation/csharp-web-dev-lsn6inheritance>`_ for the code for the lesson.
In Visual Studio, open the solution and examine the two classes inside the ``Cats`` project.

Inheriting Fields and Properties 
--------------------------------

Notice that ``Cat`` has a property called ``Family``, representing
the biological family of all cats. 

.. sourcecode:: csharp
   :lineno-start: 10

   public string Family { get; } = "Felidae";

The ``family`` field is not directly accessible by ``HouseCat`` and can only be accessed by the ``get`` accessor of the ``Family`` property.
However, there is no ``set`` accessor for ``Family``, so the value of the ``family`` field may only be changed within ``Cat``. 
It makes sense that a subclass should not be able to change the biological family of a cat, since this property should rarely, if ever, change.

Methods of the base class ``Cat`` may be called on instances of the
subclass ``HouseCat`` as if they were defined as part of the
``HouseCat``.

Try it out. In your project, open up ``Program.cs``. Within the ``Main`` method,
create an instance of ``HouseCat`` and call some of the methods it inherits from ``Cat``.

.. sourcecode:: csharp
   :linenos:

   HouseCat garfield = new HouseCat("Garfield", 12.0);
   garfield.Eat();
   Console.WriteLine(garfield.Tired);   // prints true

The ``Eat`` method was defined in ``Cat``, but may be called on all
``HouseCat`` instances as well. We say: “``HouseCat`` inherits the
method ``Eat()`` from ``Cat``.” We know we have successfully called ``Eat()`` on 
``garfield`` because the printed statement indicates the cat is now tired. 

``base``
--------

We mention above that a subclass inherits all *non-constructor*
methods from its base class. Indeed, when extending a class, we will not
be able to create new instances of our subclass ``HouseCat`` using any
constructors provided by ``Cat``. 

The base class ``Cat`` has a constructor that takes a single parameter
of type ``double``.

.. sourcecode:: csharp
   :lineno-start: 12

   public Cat(double weight)
   {
      Weight = weight;
   }

But because ``HouseCat`` does not have such a constructor, the following code 
does not compile:

.. sourcecode:: csharp

   HouseCat mittens = new HouseCat(8.4);

.. index:: ! base

``Cat`` constructors are not inherited by ``HouseCat``. If we want
to use a ``Cat`` constructor in this subclass, we must explicitly
provide it. 

To do so, look at the constructor included in ``HouseCat``:

.. sourcecode:: csharp
   :lineno-start: 11

   public HouseCat(string name, double weight) : base(weight)
   {
      Name = name;
   }

Here, we use the ``:`` syntax again with the ``base`` keyword on the constructor signature. 
This combination allows the constructor to extend the base class constructor that takes a ``weight`` parameter.
In this case, the subclass constructor also sets the value of the ``name`` field.
The call to the base class constructor must be on the subclass's constructor signature.

.. index:: ! no-arg constructor

If a base class constructor takes no arguments, then the 
**no-argument constructor** is implicitly called for you in the subclass. A no-argument,
or **no-arg constructor**, is just as the name implies, a constructor that takes no arguments. 

For example, we can add an additional constructor in ``Cat``:

.. sourcecode:: csharp
   :lineno-start: 17

   public Cat()
   {
      Weight = 13.0;
   }

Then in ``HouseCat``, we can simply define another constructor as this:

.. sourcecode:: csharp
   :lineno-start: 16

   public HouseCat(string name)
   {
      Name = name;
   }

Even though we don’t explicitly specify that we want to call a
constructor from ``Cat``, the no-argument constructor will be called. Now, we can 
initialize a new ``HouseCat`` with only a name field and the ``Cat`` no-argument
constructor will still be applied. Back in ``Program.cs``, you can confirm that the base
class constructor has been called:

.. sourcecode:: csharp
   :linenos:

   HouseCat spike = new HouseCat("Spike");
   Console.WriteLine(spike.Weight);   // prints 13

As a consequence of this constructor syntax, we can easily expose any
constructor from the base class by providing a subclass constructor that has the same signature, no method body, and calls the base class constructor with ``: base``.

.. sourcecode:: csharp
   :linenos:

   public HouseCat(double weight) : base(weight)
   {
      // This is all there is to this constructor!
   }

.. admonition:: Warning

   This constructor is a bad one, and is included merely to introduce
   syntax and usage. We would not want to have a constructor for
   ``HouseCat`` that didn’t initialize an essential field such as ``name``.

.. _method-overriding:

.. index:: override, method overriding, ! virtual

``override``
------------

Sometimes when extending a class, we’ll want to modify behavior provided
by the base class. This can be done by replacing the implementation of
an inherited method by a completely new method implementation. For a
given method, we can do this via **method overriding**.

In our example, the ``Noise`` method of ``HouseCat`` overrides the
method of the same name in ``Cat``. When we override it, we should use ``override`` 
in the signature of the method in the subclass and ``virtual`` in the signature of the base class.

Here are the methods in question.

In ``Cat``:

.. sourcecode:: csharp
   :lineno-start: 38

   public virtual string Noise()
   {
      return "Meow!";
   }

In ``HouseCat``:

.. sourcecode:: csharp
   :lineno-start: 26

   public override string Noise()
   {
      return "Hello, my name is " + Name + "!";
   }

If we have a ``HouseCat`` object and call its ``Noise()`` method, we will be 
using the method defined in ``HouseCat``.

.. sourcecode:: csharp
   :linenos:

   Cat plainCat = new Cat(8.6);
   HouseCat cheshireCat = new HouseCat("Cheshire Cat", 26.0);

   Console.WriteLine(plainCat.Noise()); // prints "Meow!"
   Console.WriteLine(cheshireCat.Noise()); // prints "Hello, my name is Cheshire Cat!"

.. admonition:: Warning

   When overriding a method from a base class, the method name, access level, type and number of parameters, and return type *must
   be exactly the same*.

   In this example, the parts of our method that we have to match are:

   .. sourcecode:: csharp

      public string Noise();

When overriding a method, we may call the method from the base class
that we are overriding by using ``base``. Modify your ``HouseCat.Noise()``
method as follows:

.. sourcecode:: csharp
   :lineno-start: 38

   public override string Noise()
   {
      if (IsSatisfied())
      {
         return "Hello, my name is " + Name + "!";
      } 
      else
      {
         return base.Noise(); // prints "Meow!"
      }
   }

This calls the overridden method in the base class via
``base.Noise()``, carrying out the original behavior if the given
conditional branch is reached.

.. index:: ! Object class

``Object`` Class
----------------

In a previous lesson, we introduced the :ref:`special methods <special-methods>`: ``Equals`` and
``ToString``. All classes contain default implementations of these methods that 
can be overridden.

In fact, these default methods are part of a class called ``Object``.
All classes we create in C# have access to the methods and members of the ``Object`` class, because it is the base class in all .NET class hierarchies.
In the case of ``Cat`` and ``HouseCat``, ``Cat`` implicitly extends ``Object``.
Since ``Cat`` is a subclass of the ``Object`` class and ``HouseCat`` is a subclass of the ``Cat`` class, ``HouseCat`` and ``Cat`` can both access different methods and members of the ``Object`` class.
So the default implementations of ``Equals`` and ``ToString`` (along with a few `other
methods <https://docs.microsoft.com/en-us/dotnet/api/system.object?view=netframework-4.8#methods>`__)
are made available to us via inheritance.

Note that we should use the ``override`` keyword when we provide new
implementations of these methods as well.

Check Your Understanding
------------------------

.. admonition:: Question

   For this question, refer to the code block below.

   .. sourcecode:: csharp
      :linenos:

      public class Message
      {
         public bool Friendly { get; } = true;
         public string Language { get; }
         public string Text { get; }

         public Message(string language, string text) {
            Language = language;
            Text = text;
         }
      }

   A class called ``Greeting`` extends ``Message``. ``Greeting`` and 
   ``Message`` are both defined within a package called ``Speech``. 
   Select all of the fields, properties, and methods that are inherited by 
   ``Greeting``.

   a. ``Friendly``
   b. ``Language`` 
   c. ``Text``
   d. ``Message``
   e. ``friendly``
   f. ``language``
   g. ``text``
   

.. ans: ``Friendly``, ``Text``, and ``Language``.


.. admonition:: Question

   For this question, refer to the code block below.

   .. sourcecode:: csharp
      :linenos:

      public class Message
      {
         public bool Friendly { get; } = true;
         public string Language { get; }
         public string Text { get; }

         public Message(string language, string text) {
            Language = language;
            Text = text;
         }
      }

   A class called ``Greeting`` extends ``Message``. What would a constructor for 
   ``Greeting`` need to be to call the ``Message`` constructor?

   a. .. sourcecode:: csharp

         public Greeting(string language, string text, bool friendly)
         {
            super(language, text);
            Friendly = friendly;
         }
      
   b. .. sourcecode:: csharp

         public Greeting(string language, string text) : base(language, text)
         {
         }

   c. .. sourcecode:: csharp

         public Greeting() : base(language, text)
         {
         }

   d. .. sourcecode:: csharp

         public Greeting(string language, string text) {
            Language = language;
            Text = text;
         }

.. ans: b
