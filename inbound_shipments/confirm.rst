Confirm Inbound Shipment
************************

+---------------+--------------------------------------------------------+
| Endpoint      | ``/inbound_shipments/{id}/_confirm``                   |
+---------------+--------------------------------------------------------+
| Method        | POST                                                   |
+---------------+--------------------------------------------------------+

This endpoint is used to confirm an initial inbound shipment.

Request Parameters
------------------

The request body may contain a JSON object describing the inbound shipment.
See :doc:`create_or_modify` for specifications.

If the body is empty, no modifications are applied to the shipment.

Response
--------

Status: **HTTP 200 OK**