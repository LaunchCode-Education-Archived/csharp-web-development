Interfaces In The Wild
======================

The first situations where you’ll want to use interfaces involve applying pre-defined interfaces 
and classes that are part of C#. Here are a few examples.

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
