Exercises: Control Flow and Collections
=======================================

If you haven't done so already, fork and clone 
`csharp-web-dev-lsn2controlflowandcollections <https://github.com/LaunchCodeEducation/csharp-web-dev-lsn2controlflowandcollections>`__.
Work on these exercises in this solution and create a new class for each item. 
You may call these classes whatever you
like, but remember to use the proper
:ref:`C# naming conventions <naming-conventions>`.

Array Practice
--------------

#. Create and initialize an array with the following values in a single line:

   :: 
   
      1, 1, 2, 3, 5, 8

#. Loop through the array and print out each value. 
#. Modify the loop to only print the odd numbers from the array.

String Practice
---------------

#. For this exercise, create a string for the value: 

   ::
   
      I would not, could not, in a box. I would not, could not with a fox. 
      I will not eat them in a house. I will not eat them with a mouse.
       
#. Use the ``Split`` method to divide the string at
   each space and store the individual words in an array. If you need to review
   the method syntax, look back at the :ref:`string methods <string-methods>`
   table.
#. Print the array of words to verify that your code works. The syntax is:

   .. sourcecode:: c#

      Console.WriteLine(string.Join(",", arrayName));

#. Repeat steps 2 and 3, but change the delimiter to split the string into
   separate sentences.

List Practice
-------------

#. Write a static method to find the sum of all the even numbers in a
   List. 
#. Within ``Main``, create a list with at least 10 integers and call
   your method on the list.
#. Write a static method to print out each word in a list that has exactly 5
   letters.
#. Modify your code to prompt the user to enter the word length for the search.

Dictionary Practice
-------------------

Make a program similar to ``GradebookDictionary`` that does the following:

#. It takes in student names and ID numbers (as integers) instead of names and
   grades.
#. The keys should be the IDs and the values should be the names.
#. Modify the roster printing code accordingly.


Bonus Mission
-------------

#. Update your solution from the *List Practice* section to use the 
   string from the *String Practice* section. Search "C# convert string to
   list" online to see how to split a string into the more flexible
   ``List`` collection.
