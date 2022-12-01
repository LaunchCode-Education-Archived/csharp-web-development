.. _equals-shortcut:

Visual Studio Generator Shortcut
================================

Instead of cutting, pasting, and refactoring old code to ensure that you create a well-structured ``GetHashCode()`` method whenever you define your own ``Equals()`` method, you can use Visual Studio’s code generation tool!
Just right-click in your class file on the class name and follow these prompts.

Let’s use a Course class to demonstrate:

.. sourcecode:: csharp
   :linenos:

   public class Course
   {
      public string Topic { get; set; }
      public Teacher Instructor { get; set; }
      public List<Student> EnrolledStudents { get; set; }
   }

#. In Visual Studio, right-click on the class name and select *Quick Fix* for Mac users or *Quick Actions and Refactorings* for Windows users from the menu.
   You can also skip this step by placing your cursor on the line with the class name and clicking on the screwdriver icon to the left.

   .. figure:: figures/select-quick-fix.png
      :alt: Screenshot showing the Quick Fix option at the top of the menu when one right-clicks on the class name.

#. Select the *Generate Equals() and GetHashCode()* option from the resulting menu:

   .. figure:: figures/generate-equals.png
      :alt: Screenshot showing the Generate Equals() and GetHashCode() option in the pop up.

#. A new menu will appear where you can make selections about which class members you want to use for the ``Equals()`` and ``GetHashCode()`` methods.
   In the case of equality between two ``Course`` objects, we want to establish that two ``Course`` objects are equal if the ``Topic`` members and ``Instructor`` members are equal.
   Once you select the necessary members, click *Ok*!

   .. figure:: figures/make-selections.png
      :alt: Screenshot showing the topic and instructor members selected in a pop-up.

#. Once you click *Ok*, Visual Studio generates the ``Equals()`` and ``GetHashCode()`` methods, resulting in the following class.

   .. sourcecode:: csharp
      :linenos:

      public class Course
      {
         public string Topic { get; set; }
         public Teacher Instructor { get; set; }
         public List<Student> EnrolledStudents { get; set; }

         public override bool Equals(object obj)
         {
            return obj is Course course &&
               Topic == course.Topic &&
               EqualityComparer<Teacher>.Default.Equals(Instructor, course.Instructor);
         }

         public override int GetHashCode()
         {
            return HashCode.Combine(Topic, Instructor);
         }
      }

In order to gain an understanding at what Visual Studio just did for us, review the section on the :ref:`Equals() method <equals-method>` and take note of the following lines of code in the code block above.
While the behavior of the code is the same as the various implementations of the ``Equals()`` methods on the previous page, Visual Studio's method does not necessarily look similar to the ones we wrote before.

#. On line 9, we see some new syntax. With ``is``, the compiler confirms that it is possible to cast ``obj`` to a variable ``course`` of type ``Course``. If it is, the value of ``course`` is set to ``obj``. All in one line!
#. On line 10, the value of ``course.Topic`` and ``Topic`` is compared for equality.
#. On line 11, the value of ``course.Instructor`` and ``Instructor`` is compared for equality.

If *all* of the equality checks on lines 9, 10, and 11 come out to be true, then the generated ``Equals()`` method will return true.

Try It!
-------

Try using the Visual Studio shortcut to generate a different method in the ``Course`` class!