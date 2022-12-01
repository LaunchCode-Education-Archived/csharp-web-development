.. _inheritance-studio:

Studio: Fun with Quizzes
========================

For this studio, you will design and build a console program that allows
the user to take a quiz. This means you will have to create some
questions and get some input from the user.

First, the questions. We want to be able to handle multiple types of
questions:

#. **Multiple choice**: A question with a fixed set of possible answers. A user can only select one answer
   and only one answer is correct.
#. **Checkbox**: A question with a fixed set of possible answers. A user can select any number of 
   answers and there is one correct combination of choices.
#. **True/False**: A question that has a true/false answer.

Design
------

In order to design your program, consider:

#. What do these types of questions have in common?
#. What makes these question types different?

First, design a base class (called ``Question``) that contains the common features, and
design subclasses for each of the question types. For each question type
be sure to include: 

#. Class name
#. Fields and properties with access modifiers
#. Methods with access modifiers
#. Any inheritance relationship

Should any of the classes be abstract? If so, should any of its
methods be abstract?

Make sure that there is functionality included to display the questions,
to display the possible answers, and to check to see if the answer(s) is
correct.

Then design the ``Quiz`` class. A quiz has a list of questions, and we
should be able to: 

#. Add questions
#. Run or carry out the quiz
#. Grade the quiz

Implementation
--------------

Create a new Visual Studio console project and implement the design that you created.
If you are unsure about your design, get some feedback by talking through it with a classmate 
before you start coding.

Putting it All together
-----------------------

In the ``Main`` method within ``Program``, the project should
create several questions, present them to the user, accept the user’s
responses, and then tell them whether their answers were correct or
incorrect.

Commit Your Work
----------------

Push up your work to a new Github repository. 

Bonus Missions
--------------

#. Add a short answer question type that includes validation behavior to
   only allow the user to enter text with less than 80 characters.
#. Add a couple of more question types to your program:

   #. Linear scale: a question that allows the user to provide a numeric
      response within an integer scale, which may vary from question to
      question. For instance, it could be 1-3 for one linear scale
      question, and 1-5 for another.
   #. Paragraph: Similar to a short answer, allows for responses of up
      to 500 characters.

#. Test your non-abstract classes with a new MSTest project. 

