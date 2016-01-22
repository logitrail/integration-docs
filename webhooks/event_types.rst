Webhook Event Types
*******************

Inbound Shipments
=================

+--------------------------------------------------+----------------------------------------------------------------+
| Event Type                                       | Description                                                    |
+==================================================+================================================================+
| ``inbound_shipment.arrived_at_warehouse``        | Occurs when an inbound shipment has arrived at the warehouse.  |
|                                                  | This may not yet mean that the shipment is actually processed  |
|                                                  | and the items are processed and shippable.                     |
+--------------------------------------------------+----------------------------------------------------------------+
| ``inbound_shipment.processed``                   | Occurs when an inbound shipment is processed and items shipped |
|                                                  | are available for outbound shipments.                          |
+--------------------------------------------------+----------------------------------------------------------------+

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