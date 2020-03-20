Interfaces In The Wild
======================

The first situations where you’ll want to use interfaces involve applying pre-defined interfaces 
and classes that are part of C#. In fact, you have already encountered implementations of several these 
``System`` provided interfaces. 

.. _icomparer:

IComparer<T>
------------

**Purpose**: A class implements this interface to compare two objects of a given class. This is 
a *parameterized* interface, which means that when using it, you need to specify the class that 
it will be comparing. For example, ``IComparer<Job>`` would compare ``Job`` objects.

**Important Methods and Properties**: ``Compare(T, T)``

`IComparer.Compare
Documentation <https://msdn.microsoft.com/en-us/library/system.collections.icomparer.compare(v=vs.110).aspx>`__

This interface can be used to determine, given two objects of the given
type, which one is *greater* than the other. It is also used by
collections such as
`List <https://msdn.microsoft.com/en-us/library/6sh2ey19(v=vs.110).aspx>`__
to sort its contents with the
`Sort <https://msdn.microsoft.com/en-us/library/234b841s(v=vs.110).aspx>`__
method.

Using ``IComparer<T>`` is a two step process. You must first create a class that implements the interface. 
Then, provide a custom implementation of the ``Compare`` method:

**Example**

.. sourcecode:: c#

   public class JobComparer : IComparer<Job>
   {
      public int Compare(Job x, Job y)
      {
         // ^^ This Compare method is an implementation of IComparer.Compare
         // Here, we write our own logic for comparing two job objects.
         // For example, if we want to compare Job objects by name values, we'd write:
         return string.Compare(x.Name, y.Name);
         // ^^ Note, this Compare method is the built-in string method
         // if we want to compare Jobs based on multiple fields, we can do so by expanding the custom logic
         // in this ``IComparer.Compare`` implementation
      }
   }


``Compare(T, T)`` returns an integer which determines which of the two objects comes before (in other 
words, "is less than") the other. If the returned value is less than zero, then the first parameter 
comes before the second. If the integer is zero, then they are considered the same. If the integer is 
greater than zero, then the second parameter comes before the first. 

You can think of the result of calling ``Compare(x, y)`` as being the value of subtracting, like 
``x - y``. If ``x`` is smaller than ``y``, this value is negative. If ``x`` is larger than ``y``, 
this value is positive.

IEnumerable<T>
--------------

**Purpose**: Enable iteration over a collection of objects using
``foreach``.

**Important Methods and Properties**: ``MoveNext()``, ``Current``

`IEnumerable<T>
Documentation <https://msdn.microsoft.com/en-us/library/9eekhta0(v=vs.110).aspx>`__

This interface is implemented by the ``List<T>`` class, which we’ve been
using throughout this course.

**Example**

.. sourcecode:: c#

   IEnumerable<string> collection = new List<string>();

   // add items to the collection

   foreach (string item in collection) 
   {
      // do something with the item
   }

Indeed, if you so desire, you may replace other instances of ``List`` with this interface as long as those
interfaces don't require specifically ``List`` methods.

IList<T>
--------

**Purpose**: Enable access to objects in a collection by index.

**Important Methods and Properties**: ``Add(T)``, ``Contains(T)``,
``Remove(T)``, ``Count``

`IList<T>
Documentation <https://msdn.microsoft.com/en-us/library/5y536ey6(v=vs.110).aspx>`__

This interface is also implemented by the ``List<T>`` class, which we’ve
been using throughout this course. In fact, ``IList<T>`` extends
``IEnumerable<T>``. An interface may extend another interface, in the
same way that classes may extend each other.

**Example**

.. sourcecode:: c#

   IList<string> collection = new List<string>();

   // Add items to the collection

   string firstItem = collection[0];

IDictionary<TKey, TValue>
-------------------------

**Purpose**: Represent a collection of key/value pairs.

**Important Methods and Properties**: ``Add(TKey, TValue)``,
``Contains(T)``, ``Remove(T)``, ``Count``, ``Keys``, ``Values``

`IDictionary<TKey, TValue>
Documentation <https://msdn.microsoft.com/en-us/library/s4ys34ea(v=vs.110).aspx>`__

This interface is implemented by the ``Dictionary<TKey, TValue>`` class,
which we’ve been using throughout this course.

**Example**

.. sourcecode:: c#

   IDictionary<string, string> collection = new Dictionary<string, string>();

   // Add items to the collection

   // Get item with key "hello"
   string hello = collection["hello"];

Check Your Understanding
------------------------

.. admonition:: Question

   True or False
   
   An interface can extend another interface.

.. ans: True
