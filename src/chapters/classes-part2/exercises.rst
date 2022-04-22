.. _classes-part-2-exercises:

Exercises: Objects and Classes, Part 2
======================================

Work on these exercises in your
`csharp-web-dev-classespart1and2 <https://github.com/LaunchCodeEducation/csharp-web-dev-classespart1and2/tree/classes2-exercises-start>`__.
project. Be sure to checkout the ``classes2-exercises-start`` branch.
You will update your ``Student.cs`` file by implementing the ``AddGrade`` and
``GetGradeLevel`` methods that were sketched out in the
:ref:`Instance Methods <instance-methods>` section.

The ``GetGradeLevel`` Method
----------------------------

This method returns the student's level based on the number of credits they
have earned: Freshman (0-29 credits), Sophomore (30-59 credits), Junior (60-89
credits), or Senior (90+ credits).

:ref:`Check your solutions <classes-2-solution-1>`

The ``AddGrade`` Method
-----------------------

This method accepts two parameters---a number of course credits and a
numerical grade (0.0-4.0). With this data, you need to update the student’s
GPA.


GPA Information
^^^^^^^^^^^^^^^

GPA is computed via the formula:

   gpa = (total quality score) / (total number of credits)

#. The *quality score* for a class is found by multiplying the letter grade
   score (0.0-4.0) by the number of credits.
#. The *total quality score* is the sum of the quality scores for all classes.

For example, if a student received an "A" (worth 4 points) in a 3-credit course
and a "B" (worth 3 points) in a 4-credit course, their total quality score
would be: 4.0 * 3 + 3.0 * 4 = 24. Their GPA would then be 24 / 7 = 3.43.

Determine the New GPA
^^^^^^^^^^^^^^^^^^^^^

To update the student's GPA:

#. Calculate their *current* total quality score by using the formula
   ``gpa * numberOfCredits``.
#. Use the new course grade and course credits to update their total quality
   score.
#. Update the student's total ``numberOfCredits``.
#. Compute their new GPA.

:ref:`Check your solutions <classes-2-solution-2>`

``ToString`` and ``Equals``
---------------------------

#. Add custom ``Equals()`` and ``ToString()`` methods to the ``Student``
   class.
#. Add custom ``Equals()`` and ``ToString()`` methods to the ``Course``
   class which you started in the exercises for the :ref:`previous chapter <classes_part1-exercises1>`.

:ref:`Check your solutions <classes-2-solution-3>`