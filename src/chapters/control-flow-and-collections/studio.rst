.. _counting-characters-studio:

Studio: Counting Characters
===========================

In this studio, you will write a program to count the number of times each
character occurs in a string and then print the results to the console.

Getting Started
---------------

Create your own project from scratch. Review :ref:`create-new-csharp-project`
if you need to.

Some Items to Ponder Before Coding
----------------------------------

#. There are multiple ways to approach this task, but one way involves the
   following steps:

   a. Loop through the string one character at a time,
   b. Store and/or update the count for a given character using an appropriate
      data structure.
   c. Loop through the data structure to print the results (one character and its
      count per line).

#. Which type of data structure (``List``, ``array``, or ``Dictionary``)
   should you use to store character counts? Any of these options would work, 
   but using one of these data structures will optimize your code's efficiency.
#. You’ll need to *initialize* the counts for the characters in some fashion.
   It’s probably better to do this as you go through the string instead of
   doing so before you loop through it. (*WHY?*)
#. If you need to review how to create a new class, revisit the 
   :ref:`Hello Methods <hello-methods>` program.
#. Don’t forget to check out the *Bonus Missions* below.

.. admonition:: Tip

   Remember, you can turn a ``string`` object into an array of characters
   using:

   .. sourcecode:: c#

      char[] charactersInString = myString.ToCharArray();


Sample Input
------------

Feel free to prompt the user for a string. However, for the sake of simplicity,
you might want to start by hard-coding some text and storing it in a variable.
For your convenience, here is some `lorem ipsum <https://loremipsum.io/>`__ text:

   Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nunc accumsan sem ut 
   ligula scelerisque sollicitudin. Ut at sagittis augue. Praesent quis rhoncus justo. 
   Aliquam erat volutpat. Donec sit amet suscipit metus, non lobortis massa. Vestibulum 
   augue ex, dapibus ac suscipit vel, volutpat eget massa. Donec nec velit non ligula 
   efficitur luctus.


Sample Output
-------------

For the example string above, your output should look something like:

::

   L: 1
   o: 15
   r: 9
   e: 26
   m: 11
    : 50
   i: 27
   p: 7
   s: 29
   u: 28
   d: 4
   l: 17
   t: 29
   a: 22
   ,: 4
   c: 17
   n: 14
   g: 7
   .: 8
   N: 1
   q: 3
   U: 1
   P: 1
   h: 1
   j: 1
   A: 1
   v: 4
   D: 2
   b: 3
   V: 1
   x: 1
   f: 2

Bonus Missions
---------------

Try these modifications on your code:

#. Prompt the user to enter the string in the command line.
#. Make the character counts case-insensitive.
#. Exclude non-alphabetic characters.

Super Bonus
^^^^^^^^^^^^

Read the string in from a file.

.. admonition:: Note

   This is a hard one. We won’t talk about reading from files in C# in this
   course, so be ready for a tough challenge if you accept this mission.



