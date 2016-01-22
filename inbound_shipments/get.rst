Get Inbound Shipment Details
****************************

Endpoints
=========

By Logitrail's Inbound Shipment ID
----------------------------------

+---------------+--------------------------------------------------------+
| Endpoint      | ``/inbound_shipments/{id}``                            |
+---------------+--------------------------------------------------------+
| Method        | GET                                                    |
+---------------+--------------------------------------------------------+

This endpoint does not accept any parameters, except the ``{id}`` in the
URL.

Response
========

Logitrail responds with a JSON object representing the details of the
requested inbound shipment.

Inbound Shipment Details
------------------------

+--------------------+----------------------------------------------------------------------+
| ``merchants_ref``  | Merchant's own reference to the inbound shipment. This can be        |
|                    | for example the purchase order number.                               |
+--------------------+----------------------------------------------------------------------+
| ``sender_name``    | Name of the sender of the shipment.                                  |
+--------------------+----------------------------------------------------------------------+
| ``products``       | A JSON object array of products in the shipment. See                 |
|                    | section "Product Details" below.                                     |
+--------------------+----------------------------------------------------------------------+
| ``expected_at_wh`` | Date when the shipment is expected to arrive at the Logitrail's      |
|                    | warehouse. Format ``yyyy-mm-dd``.                                    |
+--------------------+----------------------------------------------------------------------+
| ``status``         | Status of the shipment.                                              |
+--------------------+----------------------------------------------------------------------+

Product Details
---------------

Each item in the inbound shipment is represented with following JSON object.

+--------------------+----------------------------------------------------------------------+
| ``product``        | Simple product information.                                          |
+--------------------+----------------------------------------------------------------------+
| ``qty``            | Quantity of items to be expected.                                    |
+--------------------+----------------------------------------------------------------------+
| ``arrivedQty``     | Quantity of already arrived (handled) items.                         |
+--------------------+----------------------------------------------------------------------+
| ``arrivals``       | Detailed information of the arrivals of the items. In case the       |
|                    | items have arrived in multiple batches, each batch is identified.    |
+--------------------+----------------------------------------------------------------------+