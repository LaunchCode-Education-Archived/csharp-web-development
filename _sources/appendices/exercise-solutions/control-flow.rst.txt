Exercise Solutions: Control Flow & Collections
==============================================

Line numbers are for reference. They may not match your code exactly.

Array Practice
--------------

.. _control-flow-solution-1: 

2. Loop through the array and print out each value.

.. sourcecode:: csharp
   :linenos:

      foreach(int num in numberArray)
      {
         Console.WriteLine(num);
      }

.. admonition:: Note

   Remember: this is not the only way to loop through an array.

:ref:`Back to the exercises <control-flow-collections-exercises>`


String Practice
---------------

.. _control-flow-solution-2: 

1. For this exercise, create a string for the value.
2. Use the Split method to divide the string at each space and store the individual words in an array.
3. Print the array of words to verify that your code works.

.. sourcecode:: csharp
   :linenos:

      string sentence = "I would not, could not, in a box. I would not, could not with a fox. I will not eat them in a house. I will not eat them with a mouse.";
      string[] words = sentence.Split(" ");
      Console.WriteLine(string.Join("/", words));

:ref:`Back to the exercises <control-flow-collections-exercises>`

List Practice
-------------

.. _control-flow-solution-3: 


1. Write a static method to find the sum of all the even numbers in a List. 

.. sourcecode:: csharp
   :linenos:

      static int sumEven(List<int> arr)
      {
         int total = 0;
         foreach (int integer in arr)
         {
            if (integer % 2 == 0)
            {
               total += integer;
            }
         }
         return total;
      }


3. Write a static method to print out each word in a list that has exactly 5 letters.

.. sourcecode:: csharp
   :linenos:

      static void printFiveLetterWords(List<string> wordlist)
      {
         foreach (string word in wordlist)
         {
            if (word.Length == 5)
            {
               Console.WriteLine(word);
            }
         }
      }

4. Modify your code to prompt the user to enter the word length for the search.

.. sourcecode:: csharp
   :linenos:

      Console.WriteLine("Enter a word length: ");
      string numInput = Console.ReadLine();
      int numChars = int.Parse(numInput);

      // Call the method to print out list words of the chosen length:
      printXLetterWords(wordList, numChars);


      static void printXLetterWords(List<string> wordlist, int length)
      {
         foreach (string word in wordlist)
         {
            if (word.Length == length)
            {
               Console.WriteLine(word);
            }
         }
      }

:ref:`Back to the exercises <control-flow-collections-exercises>`

Dictionary Practice
-------------------

.. _control-flow-solution-4: 

1. It takes in student names and ID numbers (as integers) instead of names and grades.

.. sourcecode:: csharp
   :linenos:

      Console.WriteLine("Enter your students' names and ID numbers (or ENTER to finish):");

      Console.WriteLine("Student Name: ");
      newStudent = Console.ReadLine();

      if (newStudent!= "")
      {
         Console.WriteLine("ID: ");
         int newID = int.Parse(Console.ReadLine());
         students.Add(newID, newStudent);
      }


2. The keys should be the IDs and the values should be the names

.. sourcecode:: csharp
   :linenos:

      Console.WriteLine("\nClass roster:");

      foreach (KeyValuePair<int, string> student in students)
      {
         Console.WriteLine(student.Value + "'s ID: " + student.Key);
      }

      Console.WriteLine("Number of students in roster: " + students.Count);


.. admonition:: Note

   Review the Array and List Gradebooks to see how they used loops 

:ref:`Back to the exercises <control-flow-collections-exercises>`