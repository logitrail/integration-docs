Webhook Event Types
*******************

Inbound Shipments
=================

See :doc:`/inbound_shipments/webhooks`

Orders
=================

See :doc:`/orders/webhooks`

Product Inventory
=================

+--------------------------------------------------+----------------------------------------------------------------+
| Event Type                                       | Description                                                    |
+==================================================+================================================================+
| ``product.inventory.change``                     | Occurs when an inventory of a product has changed.             |
+--------------------------------------------------+----------------------------------------------------------------+

Product Information
===================

+--------------------------------------------------+----------------------------------------------------------------+
| Event Type                                       | Description                                                    |
+==================================================+================================================================+
| ``product.info.change``                          | Occurs when product information (name, weight, dimensions etc) |
|                                                  | change. The event does not trigger in change of inventories.   |
+--------------------------------------------------+----------------------------------------------------------------+
| ``product.info.missing``                         | Occurs when a product does not have enough information and     |
|                                                  | details should be updated to Logitrail.                        |
+--------------------------------------------------+----------------------------------------------------------------+