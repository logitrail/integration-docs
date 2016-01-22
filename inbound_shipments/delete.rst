Delete Inbound Shipment
***********************

+---------------+--------------------------------------------------------+
| Endpoint      | ``/inbound_shipments/{id}``                            |
+---------------+--------------------------------------------------------+
| Method        | DELETE                                                 |
+---------------+--------------------------------------------------------+
| Endpoint 2    | ``/inbound_shipments/{id}/_delete``                    |
+---------------+--------------------------------------------------------+
| Method 2      | POST                                                   |
+---------------+--------------------------------------------------------+

This endpoint is used to update an existing inbound shipment. Note that two different endpoints
are provided: with POST method and with DELETE method.

Inbound shipment can be deleted before the shipment has arrived the Logitrail's warehouse. In case
the shipment is already arrived, the shipment cannot be deleted anymore.

Request Parameters
==================

URL placeholder ``{id}`` should be replaced with the Logitrail's ID of the inbound shipment.

The request body should be empty.

Response
========

Inbound Shipment Deleted Successfully
-------------------------------------

Status: **HTTP 200 OK**

JSON object with following parameters.

+------------------+----------------------------------------------------------------------+
| ``success``      | ``true``                                                             |
+------------------+----------------------------------------------------------------------+