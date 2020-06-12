Studio: If It Ain't Broke, Add a Breakpoint!
============================================

On your machine, open up your copy of ``csharp-web-dev-lsn7interfaces-studio`` in Visual Studio.
The purpose of this studio is to talk about your current debugging strategies and how to make the most of the debugger tools discussed in this chapter.

Before we start practicing with debugging tools, go over with the group one error you encountered when working on your own version of last lesson's studio.
This could be the result of a typo or a logical error. 

#. What was the error?
#. How did you solve this error? What have been the strategies and tools you have been using so far to debug your code?
#. Could one of the debugging tools help you when addressing this error?
   For example, if you encountered an error where data was not being written onto a disc object, could you track the properties of the object with a debugging tool?

Now, checkout the `debugging branch <https://github.com/LaunchCodeEducation/csharp-web-dev-lsn7interfaces-studio/tree/debugging>`__ of
the studio repo. Review the code and use the debugging tools in Visual Studio to practice assessing the program.

To get started, try the following:

#. Add ``cd.Name`` to the *Watch* pane to track the value of that property. Does it change?
#. Add a few breakpoints inside of ``Program.cs`` and make note of where you expect the program to break its execution. 
#. Add a breakpoint inside of some of the methods in ``BaseDisc.cs``. Anticipate what you expect to see as the last line in the 
	*Call Stack* pane when the debugger stops.

After you look through the code and try out these tasks, take it one step further by answering these questions.

#. When would you use the *Call Stack* pane? If you run the app and it is already functioning, what shows up there? 
#. Would a conditional breakpoint make sense to use in the context of this app? Try changing one of the breakpoints you have already added to a conditional breakpoint and run your app! 

Once you have gone through the code, open up a piece of code you have been struggling with.
In what ways could making use of debugging tools help you figure out what is going on with the code?
