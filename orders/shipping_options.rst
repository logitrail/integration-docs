Available Shipping Methods
**************************

Merchant can request available shipping methods and delivery fees for a defined order. A typical use case
is to request available shipping options for orders created in the merchant's ERP (back office).

The endpoint takes the order contents, customer details and all available information into account when
presenting the possible shipping methods.

+---------------+--------------------------------------------------------+
| Endpoint      | ``/orders/{id}/shipping_options``                      |
+---------------+--------------------------------------------------------+
| Method        | GET                                                    |
+---------------+--------------------------------------------------------+

See :doc:`/shipping_methods/query` for response format.

Modifying the Shipping Method
=============================

When you have found a proper shipping method for the order, you may change the method via :doc:`Modify Order <create_or_modify>` API Call.

Home or Letter Delivery
-----------------------

To set order's delivery method to Home or Letter delivery, pass ``{"destination": "home"}`` or ``{"destination": "letter"}`` to :doc:`Modify Order <create_or_modify>` endpoint.

Pickup Point Delivery
---------------------

To set order's delivery method to a selected Pickup Point, pass ``{"destination": "<pickup_point_id>"}`` to :doc:`Modify Order <create_or_modify>` endpoint. To find out the ID
of the pickup point, you can use any of the endpoints ``/orders/{id}/shipping_options``, ``/shipping_options`` or :doc:`/pickup_points/lookup`.

