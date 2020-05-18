Studio: If It Ain't Broke, Add a Breakpoint!
============================================

On your machine, open up your copy of ``HelloASPDotNET`` in Visual Studio.
The purpose of this studio is to talk about your current debugging strategies and how to make the most of the debugger tools discussed in this chapter.

.. admonition:: Note

   If your version of ``HelloASPDotNET`` is currently broken, no worries!
   You can fork the `demo code <https://github.com/LaunchCodeEducation/HelloASPDotNETDemo>`_ and open it up in Visual Studio.

Before we start practicing with debugging tools, go over with the group one error you encountered when working on your own version of ``HelloASPDotNET``.
This could be an error where you mistyped the route in the ``[Route("path")]`` attribute or didn't configure the HTML form properly. 

#. What was the error?
#. How did you solve this error? What have been the strategies and tools you have been using so far to debug your code?
#. Could one of the debugging tools help you when addressing this error?
   For example, if you encountered an error when submitting the form, using a debugging tool to track the value of the ``name`` variable might have helped you diagnose the issue.

Review the code from ``HelloASPDotNET`` and use the debugging tools in Visual Studio to address potentional problems.
To get started, try the following:

#. Add ``name`` to the *Watch* pane to track the value of that variable.
#. Navigate to different routes in the application. Does what is going on in the *Watch* pane align with your expectations? Why or why not?
#. Add a breakpoint to the line where you use ``name`` in ``Content()``. 
#. Run your app in debugger mode and navigate to the appropriate route for using a query string. What is the last line in the *Call Stack* pane when the debugger stops?
#. Try running your app and navigating the route to see your form. Enter a value and hit *Greet Me!*. What is the last line in the *Call Stack* pane when you do this?

After you look through the code and try out these tasks, take it one step further by answering these questions.

#. When would you use the *Call Stack* pane? If you run the app and it is already functioning, what shows up there? If you navigate to a route that is not configured in our application, does what is in the *Call Stack* pane change? How so?
#. What additional breakpoints should you add? Where should you add these breakpoints? Go ahead and add more breakpoints!
#. Would a conditional breakpoint make sense to use in the context of this app? Try changing one of the breakpoints you have already added to a conditional breakpoint and run your app! 

Once you have gone through the code, open up a piece of code you have been struggling with.
In what ways could making use of debugging tools help you figure out what is going on with the code?
