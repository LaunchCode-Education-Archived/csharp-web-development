.. index:: ! [Authorize], ! [AllowAnonymous]

Identity and Authorization
==========================

.. TODO: Add branch info

While this chapter is focused on authentication, you may find yourself wanting to use Identity to limit pages to logged-in users.
Authorization allows us to restrict access to pages to only logged in users.
While this can be a very complex process, ASP.NET has two simple attributes that will allow us to restrict access to pages to only logged in users.

``[Authorize]`` is an attribute that limits access to content to only logged in users.
``[Authorize]`` can be used for a specific method or a whole controller.

``[AllowAnonymous]`` is an attribute that allows any viewer to access content.
This is the default state, so ``[AllowAnonymous]`` is oftentimes used in conjunction with ``[Authorize]``.

In ``CodingEvents``, we may only want logged-in users to be able to add an event.
We can add ``[Authorize]`` at the controller level to prevent any anonymous users to then be able to access those pages.
