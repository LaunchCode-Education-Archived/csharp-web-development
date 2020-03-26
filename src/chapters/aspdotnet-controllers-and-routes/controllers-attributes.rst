Attribute Routing
=================

Attribute Routing - Video
--------------------------

.. TODO: Add vid

Attribute Routing - Text
------------------------

Once you have written several controller methods within a class, you may notice some similar behavior across handlers.
You may also want to expand upon the behavior that different methods can make use of.
So far, we have been relying on conventional routing for mapping our requests and our endpoints.
As we continue learning, we will also make use of attribute routing.
**Attribute routing** makes use of **attributes** to establish routes, different types of requests that the method responds to, and so on.

Here is how we might modify ``HelloController`` to make the most of attribute routes.

.. admonition:: Note

   ASP.NET has many different attributes that we can use in our controllers. For a more in-depth catalog of different attributes, check out the `documentation <https://docs.microsoft.com/en-us/aspnet/web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2>`_.

Check Your Understanding
------------------------

.. admonition:: Question

   True/False: No one controller method can handle several request types.
 
   a. True
      
   b. False

.. ans: b, A controller method annotated with ``@RequestMapping`` can handle multiple request types.

.. admonition:: Question

   We want the method ``hello`` to take another parameter, ``@RequestParam String friend``, that will 
   add a friend's name to the returned greeting. The use should also be able to enter this name via 
   a text field. What needs to be added to the form?
 
   a. Another ``input`` tag with a ``friend`` attribute.

   b. Another ``input`` tag with a ``name`` attribute.

   c. Another ``form`` tag with a ``method`` attribute.

   d. Another ``submit`` tag with a ``friend`` value.

.. ans:  b, Another ``input`` tag with a ``name`` attribute.


