Common Exception Objects
========================

Below is a summary of some of the more commonly used exception types in C#. As we mention before, all exceptions 
extend the ``System.Exception`` class. 

.. admonition:: Note

   It is also possible to write your own exception type that inherits from ``System.Exception``. You 
   may find that your particular cause of error elicits a custom exception type. We won't cover how to write 
   custom exception objects in this book, but you can read about how to define your own exception 
   `here <https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/exceptions/creating-and-throwing-exceptions#defining-exception-classes>`__.

The examples in this table are excerpted from 
`this page <https://docs.microsoft.com/en-us/dotnet/api/system.exception?view=netframework-4.8#choosing-standard-exceptions>`__,
where you can find several other commonly used exception types.

.. list-table:: Common Exception Types in C#
   :header-rows: 1

   * - Type
     - Description
     - Example
   * - ``ArgumentOutOfRangeException``
     - Thrown by methods that verify that arguments are in a given range.
     - ``String s = "string";`` 

       ``s.Substring(s.Length+1);``
   * - ``ArgumentNullException``
     - Thrown by methods that do not allow an argument to be null.
     - ``String s = null;`` 
     
       ``"Calculate".IndexOf(s);``
   * - ``IndexOutOfRangeException``
     - Thrown when an array is indexed improperly.
     - Indexing an array outside its valid range: ``arr[arr.Length+1]``
   * - ``InvalidOperationException``
     - Thrown by methods when in an invalid state.	
     - Calling an ``Enumerable`` method on an empty collection: ``Enumerator.MoveNext()``
   * - ``NullReferenceException``
     - Thrown when a ``null`` object is referenced.	
     - ``object o = null;``

       ``o.ToString();``
   

As with catching, be specific with which types of exceptions you throw. Never throw an instance of the base ``Exception`` class. 
If a built-in exception type works well based on it's documented intended use, then use it! If there 
isn't a built-in exception that matches your needs, then you can use a custom exception type.

Check Your Understanding
------------------------

.. admonition:: Question

   When should you write your own exception class?

   #. The error the your code encounters is very specific and targeted.
   #. You know your code will produce an error, but you're not sure which exception is the best fit.
   #. Writing custom exception classes is done by .NET developers only.
   #. Never, don't do it.

.. ans: a, The error the your code encounters is very specific and targeted.

.. admonition:: Question

   Suppose you have created an empty array of ``Temperature`` objects :

   .. sourcecode:: c#

      Temperature[] temps = new Temperature[] { };

   What, if any, exception would expect to encounter when the following line executes:

   .. sourcecode:: c#

      double firstTemp = temps[0].Fahrenheit;

   #. No exception will be thrown --- ``temps[0].Fahrenheit`` will return ``null``.
   #. ``NullReferenceException`` --- the object at ``temps[0]`` is null.
   #. ``InvalidOperationException``--- cannot access the object's property.
   #. ``IndexOutOfRangeException`` --- the array is empty.

.. ans: d, ``IndexOutOfRangeException`` --- the array is empty.

