Exercise Solutions: Classes and Objects
=======================================

.. _classes_part1_solution-1: 

1. Open up the file, ``Student.cs``, and update the starter code to make use of auto-implemented properties.

.. sourcecode:: csharp
   :linenos:
   
      public class Student
      {
         private static int nextStudentId = 1;
         public string Name { get; set; }
         public int StudentId { get; set; }
         public int NumberOfCredits { get; set; } = 0;
         public double Gpa { get; set; } = 0.0;
         
         public Student(string name, int studentId, int numberOfCredits, double gpa)
         {
            Name = name;
            StudentId = studentId;
            NumberOfCredits = numberOfCredits;
            Gpa = gpa;
         }
         
         public Student(string name, int studentId): this(name, studentId, 0, 0) { }
         
         public Student(string name): this(name, nextStudentId)
         {
            nextStudentId++;
         }
      }

:ref:`Back to the exercises <classes_part1-exercises1>`

.. _classes_part1_solution-2: 

2. In ``Program.cs``, instantiate the ``Student`` class using yourself as the student. For the
   ``NumberOfCredits`` give yourself ``1`` for this class and a GPA of ``4.0``
   because you are a C# superstar!

.. sourcecode:: csharp
   :linenos:
      
      public static void Main(string[] args)
      {
      // TODO: Instantiate your objects and test your exercise solutions with print statements here.
      Student kimberly = new Student("Kimberly", 1, 1, 4.0);
      Console.WriteLine("The Student class works! " + kimberly.Name + " is a student!");
      }

:ref:`Back to the exercises <classes_part1-exercises2>`

.. _classes_part1_solution-3: 

3. In the ``SchoolPractice`` project, create a class ``Course`` with at least three
   fields. Before diving into Visual Studio, try using pen and paper to work through
   what these might be. At least one of your fields should be a ``List``
   or ``Dictionary``, and you should use your ``Student`` class.

.. sourcecode:: csharp
   :linenos:
      
      // Create a new file Course.cs
      
      using System;
      using System.Collections.Generic;
      
      namespace SchoolPractice
      {
         public class Course
         {
            private string topic;
            private Teacher instructor;
            private List<Student> enrolledStudents;
         }
      }

:ref:`Back to the exercises <classes_part1-exercises3>`
