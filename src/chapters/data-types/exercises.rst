Exercises: Data Types
=====================

To get started, open up Visual Studio and create a new console program.

.. admonition:: Tip

   If you do not recall how to create a new console program or need a quick refresher to get started, check out the section on :ref:`creating a C# project <create-new-csharp-project>`.

For each part of the exercises, create a new project in your solution. When you are done, push your solution up to a repository on your Github account!

Input/Output
------------

#. Write a new "Hello, World" program to prompt the
   user for their name and greet them by name.

   #. Add a question to ask the user:

      .. sourcecode:: csharp

         Console.WriteLine("What is your name?");

   #. Create a variable to store the user's input:

      .. sourcecode:: csharp

         string name = Console.ReadLine(); 

   #. Use concatenation to print the greeting:

      .. sourcecode:: csharp

         Console.WriteLine("Hello " + name);

   #. Run your program.

Numeric Types
-------------

#. Write a program to calculate the area of a
   rectangle and print the answer to the console. You should prompt the
   user for the dimensions. (What data types should the dimensions be?)

   #. Add a print line to prompt the user for the length of the rectangle.
   #. Define a variable to handle the user's response.
   #. Repeat the previous two steps to ask for and store the rectangle's width.
   #. Use the length and width values to calculate the rectangle's area.
   #. Print a statement using concatenation to communicate to the user what the area of
      their rectangle is.
   #. Run the program to verify your code.

More on Numeric Types
---------------------

#. Write a program that asks a user for the number of
   miles they have driven and the amount of gas they’ve consumed (in
   gallons), and print their miles-per-gallon.

Strings
-------

#. The first sentence of *Alice’s Adventures in Wonderland*
   is below. Store this sentence in a string, and then prompt the user
   for a term to search for within this string. Print whether or not the
   search term was found. Make the search case-insensitive, so that searching
   for "alice", for example, prints ``true``.

      ``Alice was beginning to get very tired of sitting by her sister on the
      bank, and of having nothing to do: once or twice she had peeped into the
      book her sister was reading, but it had no pictures or conversations in
      it, 'and what is the use of a book,' thought Alice 'without pictures or
      conversation?'``

#. Extend the previous exercise. Assume the user enters a word that is
   in the sentence. Print out its index within the string and its length. Next,
   remove the word from the string and print the sentence again to confirm your
   code. Remember that strings are *immutable*, so you will need to reassign
   the old sentence variable or create a new one to store the updated phrase.
