Debugger
========

Watch this video to learn the basics of the debugging tools available in Visual Studio. If you want 
to follow along, Chris is debugging the :ref:`hello-methods` program back in the introduction to data types. 

.. youtube::
   :video_id: sACkw915kmg


A summary of Chris's debugger tips:

- Right click in the text editing window to add a `breakpoint <https://learn.microsoft.com/en-us/visualstudio/debugger/debugger-feature-tour?view=vs-2022#set-a-breakpoint-and-start-the-debugger>`_ to your code.
- Start debug mode with the run button as you might normally run your program.
- Debugger Panes:
   - `Autos <https://learn.microsoft.com/en-us/visualstudio/debugger/autos-and-locals-windows?view=vs-2022>`_ pane shows the values of parameters and variables on the line that the debugger is 
     currently sitting on, as well as the line above.
   - `Locals <https://learn.microsoft.com/en-us/visualstudio/debugger/autos-and-locals-windows?view=vs-2022>`_ pane shows the value of local variables and parameters within the program being debugged.
   - Add variables, parameters, and expressions to the `Watch <https://learn.microsoft.com/en-us/visualstudio/debugger/debugger-feature-tour?view=vs-2022#set-a-watch>`_ pane to monitor their values while debugging.
   - `Call Stack <https://learn.microsoft.com/en-us/visualstudio/debugger/how-to-use-the-call-stack-window?view=vs-2022>`_ pane displays the record of the methods that have been called in the program being debugged.
   - View a list of breakpoints in the *Breakpoints* pane. You may also disable and enable breakpoints from here.
- Debugger `Code Stepping <https://learn.microsoft.com/en-us/visualstudio/debugger/navigating-through-code-with-the-debugger?view=vs-2022&tabs=csharp#code-stepping>`_ Buttons:
   - `Step over <https://learn.microsoft.com/en-us/visualstudio/debugger/debugger-feature-tour?view=vs-2022#step-over-code-to-skip-functions>`_ button moves debugger to the next line to be executed within a method.
   - *Step out* button brings the debugger out of the execution of a method.
   - *Step into* button makes the debugger enter the method at which it is currently paused. Note that 
     you can't step into ``System`` defined methods, only those defined by your program.

- Right click on the breakpoint to set conditional logic for when you want the breakpoint to run.
- Stop debug mode wth the stop button.


.. admonition:: Tip

   Visual Studio for Mac extra tips:

   - Your IDE may not default to *Debug* mode. To select for it, in the top menu, select *View > Debug*.
   - To view the debugging panes, select *View* in the top menu and scroll down to *Debug Pads*. Select 
     the items you wish to view, ie. *Breakpoints*, *Watch*, etc.
   - To add conditions to a breakpoint, right click on the breakpoint and select *Edit Breakpoint*. From 
     menu that opens, use the *Advanced Conditions* section to set your conditions for when you want the 
     breakpoint to be executed.
   - For more information on using the Debugger in Visual Studio for Mac, check out this `guide <https://learn.microsoft.com/en-us/visualstudio/debugger/using-breakpoints?view=vs-2022>`_.


Check Your Understanding
------------------------

.. admonition:: Question

   Breakpoints on ``Console.WriteLine()`` are helpful because stepping into them reveals what is printed in the console.

   a. True
   b. False

.. ans: False, The Visual Studio debugger tool does not allow us to step into ``Console.WriteLine()`` methods or any method defined by ``System``.

.. admonition:: Question

   Define a *breakpoint*.

   a. A point in our code where the debugger will stop running and provide information about the current state.
   b. A point in our code that we anticipate will result in an exception or error.
   c. A point in our code where we include a print statement to see what's going on.
   d. A point in our code where we want to throw the computer out of a window because nothing works.

.. ans; a, A point in our code where the debugger will stop running and provide information about the current state.
