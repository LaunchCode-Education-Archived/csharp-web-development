Exercise Solutions: Classes Part 2
==================================

Line numbers are for reference. They may not match your code exactly.

``GetGradeLevel`` Method
------------------------

.. _classes-2-solution-1:

This method returns the student’s level based on the number of credits they have earned.

.. sourcecode:: csharp
   :linenos:

      public string GetGradeLevel(int credits)
      {
         if (credits <= 29)
         {
            return "freshman";
         }
         else if (credits <= 59)
         {
            return "sophomore";
         }
         else if (credits <= 89)
         {
            return "junior";
         }
         else
         {
            return "senior";
         }
      }

:ref:`Back to the Exercises <classes-part-2-exercises>`

``AddGrade`` Method
-------------------

.. _classes-2-solution-2:

This method accepts two parameters—a number of course credits and a numerical grade (0.0-4.0).

.. sourcecode:: csharp
   :linenos:

      public void AddGrade(int courseCredits, double grade)
      {
         // Update the appropriate properties: NumberOfCredits, Gpa
         double totalQualityScore = Gpa * NumberOfCredits;
         totalQualityScore += courseCredits * grade;
         NumberOfCredits += courseCredits;
         Gpa = totalQualityScore / NumberOfCredits;
      }

:ref:`Back to the Exercises <classes-part-2-exercises>`

``ToString`` & ``Equals``
-------------------------

.. _classes-2-solution-3:


Add custom Equals() and ToString() methods to the Student class.

.. sourcecode:: csharp
   :linenos:

      public override string ToString()
      {
         return Name + " (Credits: " + NumberOfCredits + ", GPA: " + Gpa + ")";
      }

      public override bool Equals(object obj)
      {
         if (obj == this)
         {
            return true;
         }

         if (obj == null)
         {
            return false;
         }

         if (obj.GetType() != GetType())
         {
            return false;
         }

         Student studentObj = obj as Student;
         return StudentId == studentObj.StudentId;
      }
   

:ref:`Back to the Exercises <classes-part-2-exercises>`
