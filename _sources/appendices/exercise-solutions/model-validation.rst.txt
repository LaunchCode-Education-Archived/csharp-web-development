.. _mv-ex-1:

Exercises Solutions:  ViewModels and Model Validation 
=====================================================

Event information to add:

1. Add a property to collect information about where the event will take place.  

.. sourcecode:: csharp

   // In the Events class

   public string Location { get; set; }

      //  In the Event constructor
      public Event( ... string location)
         {

               Location = location;

         }

This property should not be null or blank.

.. sourcecode:: csharp

   // In the AddEventViewModel class

   [Required(ErrorMessage = "Location information is required.")]
   public string Location { get; set; }


:ref:`Return to exercises<model-validation-exercises>`

.. _mv-ex-3:

3. Add columns for the location and number of attendees to the ``Events/Index.cshtml`` view.
Line numbers for reference only.


.. sourcecode:: html
   :linenos:

      <!-- inside your table -->
         <th>
            Location
         </th>
         <th>
            Number of Attendees
         </th>
         @foreach (var evt in Model)
         {
            <tr>
                  <td>@evt.Id</td>
                  <td>@evt.Name</td>
                  <td>@evt.Description</td>
                  <td>@evt.ContactEmail</td>
                  <td>@evt.Location</td>
                  <td>@evt.NumberOfAttendees</td>
            </tr>
         }
      </table>


:ref:`Return to exercises<model-validation-exercises>`


   
