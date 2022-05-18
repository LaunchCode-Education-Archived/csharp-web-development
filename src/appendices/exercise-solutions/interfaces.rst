Exercise Solutions: Interfaces and Polymorphism
===============================================

Line numbers are for reference. They may not match your code exactly.

Sorting Flavors by Cones by Cost
--------------------------------

.. _interfaces-cones:

1. Create the new class ``ConeComparer``.

2. Implement the ``IComparer`` interface and evaluate Cone objects by cost

.. sourcecode:: csharp
   :linenos:

      public class ConeComparer : IComparer<Cone>
      {
         public ConeComparer()
         {
         }

         public int Compare(Cone x, Cone y)
         {
            double diff = x.Cost - y.Cost;
            if(diff == 0)
            {
               return 0;
            }
            else if (diff < 0)
            {
               return -1;
            }
            else
            {
               return 1;
            }
         }
      }

:ref:`Back to exercises<cones>`


3. In the ``Main()`` method, sort the ``availableCones`` list, then print the elements to the screen to verify the results.

.. _interfaces-sort:

.. sourcecode:: csharp
   :linenos:

      ConeComparer compareCones = new ConeComparer();
      availableCones.Sort(compareCones);
      foreach (Cone c in availableCones)
      {
         Console.WriteLine(c);
      }
            
:ref:`Back to exercises<cones>`

