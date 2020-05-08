If It Ain't Broke, Add a Breakpoint!
====================================

On your machine, open up your copy of ``HelloASPDotNET`` in Visual Studio.
The purpose of this studio is to talk about your current debugging strategies and how to make the most of the debugger tools discussed in this chapter.

.. admonition:: Note

   If your version of ``HelloASPDotNET`` is currently broken, no worries!
   You can fork the `demo code <https://github.com/LaunchCodeEducation/HelloASPDotNETDemo>`_ and open it up in Visual Studio.

Before we start practicing with debugging tools, go over with the group one error you encountered when working on your own version of ``HelloASPDotNET``.
This could be an error where you mistyped the route in the ``[Route(path)]`` attribute or didn't configure the HTML form properly. 

#. What was the error?
#. How did you solve this error? What have been the strategies and tools you have been using so far to debug your code?
#. Could one of the debugging tools help you when addressing this error?

Review the code from ``HelloASPDotNETDemo`` and use the debugging tools in Visual Studio to address potentional problems.
Start out by trying to add ``name`` to the *Watch* pane to track the value of that variable.

Questions to review as you look through the code:

#. When would you use the *Call Stack* pane? If you run the app and it is already functioning, what shows up there? 
#. What breakpoints should you add? Where should you add these breakpoints? For example, if you want to add a breakpoint to check the value of ``name``, what line in your code should you add it to?
#. Would a conditional breakpoint make sense to use in the context of this app?

Once you have gone through the code, open up a piece of code you have been struggling with.
In what ways could making use of debugging tools help you figure out what is going on with the code?
