Inbound Shipment Statuses
*************************

+--------------------------+----------------------------------------------------------+
| Status Code              | Description                                              |
+==========================+==========================================================+
| ``initial``              | Initial info about inbound shipment. The shipment can    |
|                          | be still cancelled or deleted.                           |
+--------------------------+----------------------------------------------------------+
| ``confirmed``            | The inbound shipment is confirmed.                       |
+--------------------------+----------------------------------------------------------+
| ``en_route``             | The inbound shipment is on its way to Logitrail.         |
+--------------------------+----------------------------------------------------------+
| ``arrived_at_warehouse`` | The shipment has arrived at the Logitrail's warehouse    |
|                          | but is not yet processed. The shipment cannot be deleted |
|                          | but it's possible to cancel the shipment (return it).    |
+--------------------------+----------------------------------------------------------+
| ``processing``           | The inbound shipment is currently being processed, i.e.  |
|                          | items are partially unloaded to the Logitrail warehouse. |
+--------------------------+----------------------------------------------------------+
| ``problem``              | The inbound shipment has one or more problems that need  |
|                          | further information from the merchant.                   |
+--------------------------+----------------------------------------------------------+
| ``processed``            | The inbound shipment is fully processed. The shipment    |
|                          | cannot be deleted, cancelled or modified.                |
+--------------------------+----------------------------------------------------------+
| ``cancelled``            | The inbound shipment is cancelled after confirmation.    |
+--------------------------+----------------------------------------------------------+
| ``deleted``              | The inbound shipment is deleted.                         |
+--------------------------+----------------------------------------------------------+

Partial Shipments
=================

Note that the status tag resembles the overall status of the shipment. While the shipment
may initially have two products, six items of each, only one product may have arrived.
In this case the shipment falls to ``problem`` status until a) the missing items have
arrived; or b) the missing items are removed from the shipment by the merchant.