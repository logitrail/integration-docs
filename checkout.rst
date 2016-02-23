Checkout Integration
********************

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

Client-side JavaScript
======================

The checkout page should include our client-side JavaScript library in the ``<head>`` section of the page.

.. code-block:: html

    <script src="https://rawgit.com/logitrail/javascript-library/master/src/logitrail.js"></script>
    
.. warning::

    The library URL above points to the development version of the library in
    Logitrail's GitHub repository, served via `RawGit <https://rawgit.com/>`_.
    Changes are possible and the library might be occassionally in unstable state.

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