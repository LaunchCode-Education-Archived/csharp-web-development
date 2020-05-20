The Shared Directory
====================

Earlier in the lesson, we touched upon the role of ``_Layout.cshtml``.
When we set ``Layout`` to ``null``, the header and footer and Bootstrap disappear from our site and we are left with static HTML.
``_Layout`` is in the ``Shared`` directory of the ``Views`` directory.
Files inside this ``Shared`` directory are used sitewide and can accessed by the templates we create when we are working with our controllers.

Layout pages
------------

Whenever we create a new project, we get one layout page, ``_Layout.cshtml``, and this file contains links to Bootstrap.
Layout pages in ASP.NET MVC focus on the header and footer of the site. 
The header and footer of our site when we first create it contains links to important info like a privacy statement.
As you work on your application, you may want your header and footer for each page to include your own privacy statement or a contact page.
When you make updates to ``_Layout``, every template in the application using ``_Layout`` reflects the updates you have made.  

.. index:: ! partial view

Partial Views
-------------

If you want to create repeatable elements of your webpage that are contained within the main body of the page, you can use a **partial view**.
Partial views are blocks of HTML elements that we want to use across multiple templates.
When creating a partial view, we add the file to the ``Shared`` directory.
Then we can upon the patial view in the appropriate spot in our template by using ``Render()``.