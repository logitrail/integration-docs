Inbound Shipment Webhooks
*************************

inbound_shipment.info.change: Inbound shipment details were changed
===================================================================

``inbound_shipment.info.change`` webhook is emitted whenever the details of the inbound shipment is changed.

Payload
-------

+----------------------------+---------------------------------------------------------------------------------------+
| **``inbound_shipment``**   | **Details about the inbound shipment:**                                               |
+----------------------------+---------------------------------------------------------------------------------------+
| ``.id``                    | Logitrail's ID for the order (24-digit hex)                                           |
+----------------------------+---------------------------------------------------------------------------------------+

inbound_shipment.arrived_at_warehouse: The inbound shipment arrives at Logitrail's warehouse
============================================================================================

``inbound_shipment.arrived_at_warehouse`` webhook is emitted at time the inbound shipment arrives at the Logitrail's
warehouse. Note that this **does not** mean that the inbound shipment is already handled and included products
can be further shipped to customers.

Also note that the inbound shipment is not checked and verified to be complete.

Payload
-------

+----------------------------+---------------------------------------------------------------------------------------+
| **``inbound_shipment``**   | **Details about the inbound shipment:**                                               |
+----------------------------+---------------------------------------------------------------------------------------+
| ``.id``                    | Logitrail's ID for the order (24-digit hex)                                           |
+----------------------------+---------------------------------------------------------------------------------------+

inbound_shipment.processed: The inbound shipment was processed
==============================================================

``inbound_shipment.arrived_at_warehouse`` webhook is emitted at time the inbound shipment is completely processed and
arrived products are shippable.

Payload
-------

+----------------------------+---------------------------------------------------------------------------------------+
| **``inbound_shipment``**   | **Details about the inbound shipment:**                                               |
+----------------------------+---------------------------------------------------------------------------------------+
| ``.id``                    | Logitrail's ID for the order (24-digit hex)                                           |
+----------------------------+---------------------------------------------------------------------------------------+