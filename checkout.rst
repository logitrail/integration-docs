Checkout Integration
********************

.. toctree::
   :maxdepth: 2

   checkout/http_form_api
   checkout/customizing_layout

Overview
========

The easiest method to pass customer's order details to Logitrail is to use Logitrail
Checkout integration in the end of customer's checkout process in the e-commerce store.

The checkout integration requires three different components on the e-commerce site:

 * A simple server-side bridge script (libraries and example scripts are provided by Logitrail)
 * Client-side JavaScript snippet installed on the site headers
 
Server-side Bridge Script
=========================

The server-side bridge script is required to pass the checkout details securely to Logitrail.

The bridge script should be made aware of a couple of details:

 * Customer's contact details
 * Products and quantities in the cart
 * Merchant's ID and merchant's shared secret
 
The bridge script should output a hidden HTML form of the details and a calculated
``mac`` field to sign the request. The HTML form should be automatically submitted behalf
of the user.

See :doc:`checkout/http_form_api` for further information about the form and its fields.

Client-side JavaScript
======================

The e-commerce store should include our client-side JavaScript library in the ``<head>`` section of the site.

.. code-block:: html

    <script src="https://connect.logitrail.com/logitrail.js"></script>
    
When it's time to pass the order details to Logitrail and allow the customer to make his/her delivery method
and pickup point selections, you should further do a couple more JavaScript calls with our library.

.. code-block:: html

     <script>
     Logitrail.checkout({
        containerId: 'logitrailHolder',          // DOM ID of the element where Logitrail's checkout is embedded
        bridgeUrl: '/server-side-bridge-script', // URL of the server side bridge script
        success: function(success) {
            
        },
        error: function(error) {

        }
    });
    </script>

``Logitrail.checkout()`` function loads the Logitrail's embedded checkout screen into the DOM element
defined in ``containerId`` parameter. In practice, the browser does a HTTP GET request to the ``bridgeUrl``
which in turn forwards the browser to Logitrail's checkout service.

When the customer completes the delivery selections, the given ``success`` callback function is called.
At that time, your e-commerce platform should do at least two things:

 * Save the Logitrail's order ID to your system (given in ``success.order_id``)
 * Add amount given in ``success.delivery_fee`` to the customer's payable amount
 * ... forward customer to pay the order

Success callback properties
---------------------------

Logitrail JS API provides a couple of properties back to the success callback. The first and only
argument is a JS object with following properties.

+--------------------+-------------------------------------------------------------+
| ``order_id``       | The Logitrail's Order ID                                    |
+--------------------+-------------------------------------------------------------+
| ``delivery_fee``   | The delivery fee of the selected payment method and pickup  |
|                    | point, as defined in the merchant's profile in Logitrail.   |
|                    | Note that it's not mandatory to set delivery fee prices     |
|                    | in Logitrail and the merchant may override this.            |
+--------------------+-------------------------------------------------------------+
| ``delivery_info``  | An object describing the selected delivery method, see      |
|                    | "Delivery Info" below.                                      |
+--------------------+-------------------------------------------------------------+

Delivery Info
-------------

The Checkout JS API provides also further delivery selection details in ``success.delivery_info``
property.

+--------------------+-------------------------------------------------------------+
| ``type``           | The delivery type: ``pickup``, ``home`` or ``letter``       |
+--------------------+-------------------------------------------------------------+
| ``pickup_point``   | Optional object describing the selected pickup point.       |
+--------------------+-------------------------------------------------------------+
| ``.title``         | Pickup point's name                                         |
+--------------------+-------------------------------------------------------------+
| ``.address``       | Pickup point's address (in one line)                        |
+--------------------+-------------------------------------------------------------+
| ``.info``          | Pickup point info, like business hours or location.         |
+--------------------+-------------------------------------------------------------+
| ``.carrier``       | Carrier that serves the selected pickup point.              |
|                    | Possible values: ``fi_posti``, ``fi_matkahuolto`` or        |
|                    | ``fi_schenker``                                             |
+--------------------+-------------------------------------------------------------+
| ``.carrier_id``    | Carrier's own ID for the pickup point.                      |
+--------------------+-------------------------------------------------------------+

.. warning::

    It's not guaranteed that Logitrail uses the mentioned carrier for the order
    or shipment. Due this, it's not recommended to show the carrier information
    to the customer.
 
Confirming the Order
====================

Note that an order submitted via our checkout integration is created as ``passive``. After you have
received customer's payment, you should separately **confirm** the order.

Order can be confirmed via two ways:

 * HTTP Redirect to Logitrail Checkout service
 * API Call (see :doc:`orders/confirm`)

Examples
========

Working examples are available in GitHub `PHP Integration Examples repository
<https://github.com/logitrail/php-integration-examples>`_.