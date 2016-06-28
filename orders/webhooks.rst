Order Webhooks
**************

order.info.change: Order details were changed
=============================================

``order.info.change`` webhook is emitted whenever the details of the order is changed.

Payload
-------

+----------------------------+---------------------------------------------------------------------------------------+
| **``order``**              | **Details about the shipped order:**                                                  |
+----------------------------+---------------------------------------------------------------------------------------+
| ``.id``                    | Logitrail's ID for the order (24-digit hex)                                           |
+----------------------------+---------------------------------------------------------------------------------------+
| ``.merchants_order``       | Merchant's order ID for the order.                                                    |
+----------------------------+---------------------------------------------------------------------------------------+
| ``.status``                | New status for the order.                                                             |
+----------------------------+---------------------------------------------------------------------------------------+
| ``.tracking_code``         | Tracking code for the order, to be passed for the customer. Only in confirmed orders. |
+----------------------------+---------------------------------------------------------------------------------------+
| ``.tracking_url``          | Tracking URL for the order, to be passed for the customer. Only in confirmed orders.  |
+----------------------------+---------------------------------------------------------------------------------------+

Note that it's possible that only the properties above are passed to the webhook, even some other properties
(like customer name etc) were changed.

order.shipped: Order was shipped by Logitrail to the customer
=============================================================

``order.shipped`` webhook is emitted when the order was actually shipped

Payload
-------

+----------------------------+---------------------------------------------------------------------------------------+
| **``order``**              | **Details about the shipped order:**                                                  |
+----------------------------+---------------------------------------------------------------------------------------+
| ``.id``                    | Logitrail's ID for the order (24-digit hex)                                           |
+----------------------------+---------------------------------------------------------------------------------------+
| ``.merchants_order``       | Merchant's order ID for the order.                                                    |
+----------------------------+---------------------------------------------------------------------------------------+
| ``.status``                | New status for the order.                                                             |
+----------------------------+---------------------------------------------------------------------------------------+
| ``.tracking_code``         | Tracking code for the order, to be passed for the customer. Only in confirmed orders. |
+----------------------------+---------------------------------------------------------------------------------------+
| ``.tracking_url``          | Tracking URL for the order, to be passed for the customer. Only in confirmed orders.  |
+----------------------------+---------------------------------------------------------------------------------------+
| **``shipment``**           | **Details about the shipment:**                                                       |
+----------------------------+---------------------------------------------------------------------------------------+
| ``.id``                    | Logitrail's ID for the shipment (24-digit hex)                                        |
+----------------------------+---------------------------------------------------------------------------------------+
| ``.carrier_tracking_code`` | Carrier's tracking code. Note: this should not be sent to customer. Use               |
|                            | ``order.tracking_code`` instead.                                                      |
+----------------------------+---------------------------------------------------------------------------------------+

