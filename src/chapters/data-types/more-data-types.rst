More Data Types
===============

Strings and Single Characters
------------------------------

Immutability
^^^^^^^^^^^^^

Strings in C# are *immutable*, which means that the characters within a
string cannot be changed.

Single vs. Double Quotation Marks
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

C# syntax requires double quotation marks when declaring strings.

C# has another variable type, ``char``, which is used for a single character.
``char`` uses single quotation marks. The single character can be a letter,
digit, punctuation, or whitespace like tab (``'\t'``).

.. sourcecode:: C#
   :linenos:

   string staticVariable = "dog";
   char charVariable = 'd';

.. _string-methods:

Manipulation
^^^^^^^^^^^^

The table below summarizes some of the most common string methods available in
C#. For these examples, we use the string variable
``string str = "Rutabaga"``.

.. list-table:: String methods in C#
   :header-rows: 1

   * - C# Syntax
     - Description
   * - ``str.Substring(3,1)`` 
     - Returns the character in 3rd position, (``a``).
   * - ``str.Substring(2,3)``
     - Return substring from 2nd to 4th, i.e. substring starting at 
       index 2 and 3 characters long, (``tab``).
   * - ``str.Length()``
     - Returns the length of the string, (``9``).
   * - ``str.IndexOf('a')``
     - Returns the index for the first occurrence of 'a', (``3``).
   * - ``str.Split("delimiter")``
     - Splits the string into sections at each ``delimiter`` and stores the
       sections as elements in an array, (``Rutabaga``).
   * - ``str + str``
     - Concatenate two strings together, (``RutabagaRutabaga``).
   * - ``str.Trim()``
     - Removes any whitespace at the beginning or end of the string, (``Rutabaga``).
   * - ``str.ToUpper(), str.ToLower()``
     - Changes all alphabetic characters in the string to UPPERCASE or
       lowercase, respectively,(``RUTABAGA``, ``rutabaga``).
   
