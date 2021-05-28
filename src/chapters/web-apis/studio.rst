.. index:: ! headless API

Studio: Consuming the CodingEvents API With Postman
===================================================

The UI of a browser is designed to make simple ``GET`` requests for URLs entered into its address bar. This design works great for browsing sites, but 
falls short when working with APIs. Anything beyond a ``GET`` request is difficult to send via a browser address bar alone. Think about what is needed to 
create a new ``CodingEvent``. This type of request contains a body. Our MVC application included a view to allow us to test inputs. Our API, however, is 
**headless**. It does not contain the client-side form. In order to test how it handles requests then, we need a way to interact with the API server without 
the browser. In this studio, we work with Postman to explore how APIs can be consumed.

Setup
-----

Install Postman
^^^^^^^^^^^^^^^

If you haven't done so already, :ref:`install Postman <postman-installation>`.

Fork and Clone the API Source Code
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

With Postman installed, we're ready to fork and clone the `CodingEvents API <https://github.com/LaunchCodeEducation/coding-events-api/tree/1-sqlite>`__. 
Although it is implemented differently from CodingEvents MVC, you will find that most of the features from the MVC application have been supported through 
endpoints in the API.

.. admonition:: Note

   Our focus in this course is on operations and as such we will not be going into the development of the API. However, feel free to explore the source 
   code if you are curious about the similarities and differences between the .NET MVC and API implementations.

Let's begin by forking and cloning the repo onto our machine. In your Powershell or terminal window, move into a directory where you plan to save your local
copy of the API codebase.

.. sourcecode:: bash

   > git clone https://github.com/<GitUsername>/coding-events-api

For this studio, we want to have the ``1-sqlite`` branch checked out. This branch has an API with a single (``CodingEvent``) 
resource and a built-in SQLite database. 

.. admonition:: Note

   Including a SQLite database in this project means you don't need to have your MySQL server running to test the API. We won't get into what this looks like
   and instead just concentrate on testing the API endpoints.

Let's change into the repo and switch to this branch:

.. sourcecode:: bash

   # cd is an alias (like a nick-name) for the Set-Location cmdlet in PowerShell
   > cd coding-events-api

   # check out the 1-sqlite branch
   > git checkout 1-sqlite

You can leave this PowerShell window open, we will return to it in a later step:

.. figure:: figures/powershell-in-repo-dir.png
   :alt: A PowerShell window in coding-events-api repo directory on 1-sqlite branch

   A PowerShell window after cloning the ``coding-events-api`` repo

Start the API Server
^^^^^^^^^^^^^^^^^^^^

We'll start the API server from the terminal using the ``dotnet run`` command. Navigate to the ``CodingEventsAPI`` project folder *within* your 
``coding-events-api`` solution. This is the folder that contains ``Controllers/`` and so on, and is NOT the main project folder.

.. sourcecode:: bash

   # change to the CodingEventsAPI project directory
   > cd CodingEventsAPI

   # run the project
   > dotnet run

   info: Microsoft.Hosting.Lifetime[0]
      Now listening on: https://localhost:5001
   info: Microsoft.Hosting.Lifetime[0]
         Now listening on: http://localhost:5000
   info: Microsoft.Hosting.Lifetime[0]
         Application started. Press Ctrl+C to shut down.
   info: Microsoft.Hosting.Lifetime[0]
         Hosting environment: Development
   info: Microsoft.Hosting.Lifetime[0]
         Content root path: C:\Users\<username>\coding-events-api\CodingEventsAPI

If you see something like this output above, then your API is running! You'll note, we're not using Visual Studio here to run the application but feel free to 
open the solution in VS and explore the source code. 

Swagger Documentation
^^^^^^^^^^^^^^^^^^^^^

With the application running, go to the first location listed as: "Now listening on:". Enter ``https://localhost:5001`` into your browser. You'll see a page
that looks nothing like any view we created in our CodingEvents MVC applications. This view is indeed not an equivalent. What you see running in the browser is not
at all a client-side application, but rather, some documentation resources for the API itself. 

You'll see a list of those endpoints we asked you to describe for this lesson's exercises:

Two endpoints at the ``CodingEvents`` entry-point path, ``/api/events``, to interact with the collection as a whole:

- **list CodingEvents**: ``GET /api/events -> CodingEvent[]``
- **create a CodingEvent**: ``POST /api/events (NewCodingEvent) -> 201, CodingEvent``

And two that require a sub-path variable, ``/events/{codingEventId}``, to interact with a single entity:

- **delete a CodingEvent**: ``DELETE /api/events/{codingEventId} -> 201, CodingEvent``
- **find single CodingEvent**: ``GET /api/events/{codingEventId} -> CodingEvent``

And below this list are two *Schemas*, or shapes, of resources the API handles. 

**Swagger** is a popular tool API developers use to include fast documentation for their API codebase. The page we're looking at is generated by this tool and gives
us a nice summary of the endpoints made available by the CodingEvents API we currently have running. But remember, we'll test the API in Postman.


Making Requests to the Coding Events API
----------------------------------------

List the Coding Events
^^^^^^^^^^^^^^^^^^^^^^

To create our first request using Postman, select the *New* button in the top left corner of the Postman window:

.. figure:: figures/new-button.png
   :alt: Close up of the Postman New item button

   Select the *New* button to create a new request

Creating a New Request
~~~~~~~~~~~~~~~~~~~~~~

With the new item dialog open, select the *Create New* tab (on the left) then select *Request*. 

.. figure:: figures/new-item-dialog.png
   :alt: Close up of the top of the Postman New item dialog

   Create a new request item in Postman

This will open the new request dialog:

.. figure:: figures/new-request-dialog.png
   :alt: Top of the Postman New Request dialog

   The new request dialog includes fields for a request name, description, and collection

Postman requests require a name and a collection. A collection is just a container to hold related requests. They make it easy to import and export 
collections of requests for portability across teams. For our first request, enter "list coding events" in the *Request name* form field. At the 
bottom of the new request dialog, you will see that the collections are empty. Select the orange *Create Collection* button, then enter the 
name ``coding events API``. The new request dialog button will change to say *Save to coding events API*:

.. figure:: figures/new-request-dialog-complete.png
   :alt: Full view of the Postman New Request dialog

   Once the collection is selected, save the new request

After saving, a new request tab will be created where you can customize its behavior:

.. figure:: figures/empty-request-tab.png
   :alt: Postman new request tab view after creation

   A new request has been created in Postman 

Configuring the Request
~~~~~~~~~~~~~~~~~~~~~~~

Postman exposes an exhaustive set of tools for configuring every aspect of a request. Fortunately, this request is relatively simple.

We want to request the state of the CodingEvents collection, in shorthand:

``GET /api/events -> CodingEvent[]``

In Postman, we can make this request by configuring the following settings:

- the URL of the endpoint: ``http://localhost:5000/api/events``
- the HTTP method of the endpoint: ``GET``
- the request header: (``Accept: application/json``)

.. admonition:: Note

   Though we view the Swagger docs from port 5001, we request the resources on port 5000.

To the left of the URL bar is a dropdown selector for HTTP methods. It will default to ``GET``. In the following requests, you will need to select the 
appropriate method from this list. 

.. figure:: figures/http-method-selector.png
   :alt: Opening the Postman HTTP method dropdown menu

   The dropdown menu contains all of the HTTP request types available to send

Next to the request method type, enter the request URL where the API request should be sent: ``http://localhost:5000/api/events``.

Underneath the URL bar are tabs for other aspects of the request. Select the ``Headers`` tab to configure our header. The ``Accept`` header lets the API 
know that we accept responses that are formatted as JSON. 

.. admonition:: Note

   In our context, the API only responds with JSON. However, some APIs offer multiple 
   `MIME types <https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/MIME_types>`_ for their responses. It is a best practice to set this 
   header explicitly to the content type the consuming application expects.

You can set multiple headers in this section. As you begin to type the name and value of headers, Postman will autocomplete them for you. After 
configuration, your request should look like this:

.. figure:: figures/list-coding-events-request.png
   :alt: Postman view of Accept header configured in request

   The request Accept header is given a value of "application/json"

To issue the request, you can select the blue *Send* button on the right of the window, or use the *ctrl + enter* keyboard shortcut. 

Viewing the Response
~~~~~~~~~~~~~~~~~~~~

Below the request configuration, you will see the response section has been populated. From here, you see the response body along with the status code 
(on the right) and a tab for headers:

.. figure:: figures/list-coding-events-response.png
   :alt: Postman response window displays an empty array returned from requesting all CodingEvents 

   The initial CodingEvents collection state is empty


Since this is our first time running the application, the database is empty. We expectedly received an empty JSON list ``[]`` which corresponds to the 
empty representation of the Coding Events collection.

If you select the *Headers* tab in the response pane, you see the API satisfied our ``Accept`` request header and provided the response in ``application/json`` format.

.. figure:: figures/response-headers.png
   :alt: Postman close up view of response headers tab opened

   The response is returned as ``application/json``

.. admonition:: Note

   If you get a connection refused error, it means you likely forgot to start the API server or mistyped the URL. Check both of these before attempting 
   the request again.

   .. figure:: figures/connection-refused.png
      :alt: Error message displayed in Postman from a refused connection 

      If sending the request results in a connection error, check your setup and request settings

Create a ``CodingEvent``
^^^^^^^^^^^^^^^^^^^^^^^^

For our next request, we will create a ``CodingEvent``. Repeat the steps you performed in the previous request:

#. Click on the orange *New* button in the top left corner of the Postman window to create a new request named: ``create coding event``
#. Add it to the existing ``coding events API`` collection

This request will change the state of the Coding Events collection by adding a new entity to it. Recall that the shorthand for this request is:

``POST /api/events (NewCodingEvent) -> 201, CodingEvent``

We will need to set the following request settings:

#. The URL of the endpoint: ``http://localhost:5000/api/events``
#. The HTTP method of the endpoint: ``POST``
#. The request header: (``Content-Type`` ``application/json``)
#. The request body: a JSON ``NewCodingEvent`` object

As a best practice, we explicitly define the ``Content-Type`` header. This header indicates that our request contains ``application/json`` data so that 
the API knows how to parse the incoming request body. 

Configure the Request Body
~~~~~~~~~~~~~~~~~~~~~~~~~~

In addition to the configurations you are now familiar with setting, we will need to define the request body. For this task, select the *Body* tab that 
is next to *Headers*. 

The body of the request must be in a raw JSON format. In the *Body* tab, open the the dropdown to select your data format. Select *raw* from the menu. Once 
this format is selected, enter the following JSON body:

.. sourcecode:: bash
   :linenos:

   {
      "Title": "Halloween Hackathon!",
      "Description": "A gathering of nerdy ghouls to work on GitHub Hacktoberfest contributions",
      "Date": "2020-10-31"
   }

Before sending the request, check that your configuration matches the following image:

.. figure:: figures/create-coding-event-request.png
   :alt: Postman request display of new CodingEvent item in Body tab 

   You can write JSON directly into the request Body tab 

Hit send and we'll take a look at the result.

Analyzing the Response
~~~~~~~~~~~~~~~~~~~~~~

You can see in the response that the API reflected back the representation of the new ``CodingEvent`` entity. Notice that a unique ``id`` has been 
assigned to it by the API. Looking at the status code (``201``) and headers of the response, we can see the API conformed to the REST convention. Open the *Headers*
tab in the response panel. The URL value of the ``Location`` header is: ``http://localhost:5000/api/events/1``. This location can be can now be used to 
view the individual ``CodingEvent`` entity that was created by our request.

Sending a Bad Request
~~~~~~~~~~~~~~~~~~~~~

To test the rejection of bad requests, let's send one that violates the ``NewCodingEvent`` validation constraints. Send another request with the 
following JSON body:

.. sourcecode:: bash

   {
      "Title": "too short",
      "Description": "A gathering of nerdy ghouls to work on GitHub Hacktoberfest contributions",
      "Date": "2020-10-31"
   }

You can see from the response that the API rejected the request. The response returns a bad request status of ``400`` which indicates a client-side error. 
The response body includes information about what needs to be corrected to issue a successful request:

.. figure:: figures/create-coding-event-bad-request.png
   :alt: Postman response returned from CodingEvent creation request containing an invalid request body

   The response body error message tells us we need to modify our ``CodingEvent`` title

Get a Single Coding Event
^^^^^^^^^^^^^^^^^^^^^^^^^

For this step, we will make a request for the state of a single entity. You can use the URL from the ``Location`` header of the previous request to 
complete this task. Remember to follow the steps you performed before, keeping in mind the shorthand for this request:

``GET /api/events/{codingEventId} -> CodingEvent``

#. Create a new request named: ``get a single coding event``
#. Add it to the existing ``coding events API`` collection
#. Configure the URL of the endpoint: ``http://localhost:5000/api/events/1``
#. Configure the HTTP method of the endpoint: ``GET``
#. Configure the request header: (``Accept: application/json``)

You should get back the following JSON response body:

.. sourcecode:: bash
   :linenos:

   {
      "id": 1,
      "title": "Halloween Hackathon!",
      "description": "A gathering of nerdy ghouls to work on GitHub Hacktoberfest contributions",
      "date": "2020-10-31T00:00:00"
   }

Requesting a Non-Existent Entity
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Our REST API allows us to interact with the state of its resources. If we make a request for a resource that doesn't exist in this state, we expect a 
``404`` (not found) response. 

Try issuing the request again with a non-existent ``codingEventId`` of ``100``. You should get back the following response:

.. figure:: figures/404-response.png
   :alt: Postman 404 response for a non-existent resource

   We got a 404 response when requesting a resource that cannot be found on the server

Delete a Coding Event
^^^^^^^^^^^^^^^^^^^^^

In this final step, we will issue a ``DELETE`` request. Before we make the request, let's re-issue the request to list the collection of CodingEvents. Now 
that we have added an entity, we expect the state of the CodingEvents resource collection to have changed. Switch back to the ``list coding events`` request 
tab and re-issue the request. You should get a response of the collection's list representation containing the single entity we have created.

.. sourcecode:: bash
   :linenos:

   [
     {
        "id": 1,
        "title": "Halloween Hackathon!",
        "description": "A gathering of nerdy ghouls to work on GitHub Hacktoberfest contributions",
        "date": "2020-10-31T00:00:00"
     }	
   ]

To delete this entity, and therefore change the state of our resources, we will need to issue the following shorthand request:

``DELETE /api/events/{codingEventId} -> 204``

Once again, go through the methodical process of setting up the request:

#. Create a new request named: ``delete a coding event``
#. Add it to the existing ``coding events API`` collection
#. Configure the URL of the endpoint: ``http://localhost:5000/api/events/1``
#. Configure the HTTP method of the endpoint: ``DELETE``

Notice that for this request, we do not need to set any request headers. A ``DELETE`` request should send back an empty (``no-content``) response body 
with its ``204`` status code. 

.. figure:: figures/delete-coding-event-response.png
   :alt: Postman delete a CodingEvent response

   Deleting a ``CodingEvent`` returns no body in the response

As a final confirmation, check the state of the CodingEvents collection and notice that it has returned to its initial state. The representation of this 
state is shown in the empty list ``[]`` response body.

Bonus Missions
--------------

If you complete this studio early and want some additional practice, consider the following bonus missions:

- Explore the API source code using your IDE debugger to step through the request and response process
- Try consuming the API from the command-line using the Bash `curl <https://linuxhint.com/curl_bash_examples/>`_ program or the PowerShell 
  `Invoke-RestMethod <https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/invoke-restmethod?view=powershell-7>`_ cmdlet.

