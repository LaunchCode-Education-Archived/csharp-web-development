Static Resources
================

Previously, we briefly saw that when adding a view, we inherited some CSS from the ``_Layout.cshtml`` file in the ``Shared`` directory.
While every view we add for our action methods in the controllers inherits from this template, we can also add view-specific styles and scripts.

To add styles that only apply to the view we are currently working on, we can use the same ``<link>`` tag we normally do for a static HTML page.
We can also add JS files the same way. 
However, we want to make sure of a couple things first:

#. That we are overriding any styles and scripts from ``_Layout``.
#. That we have put custom CSS or JS in a separate ``Content`` folder.

We can also put any images that we need in the separate ``Content`` folder as well.

Let's say that for each event in ``CodingEvents``, we want to add an image of the meeting location and some customized CSS 