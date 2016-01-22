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

+--------------------+-------------------------------------------------------------------------+
| ``merchants_ref``  | Merchant's own reference to the inbound shipment. This can be           |
|                    | for example the purchase order number.                                  |
+--------------------+-------------------------------------------------------------------------+
| ``sender_name``    | Name of the sender of the shipment.                                     |
+--------------------+-------------------------------------------------------------------------+
| ``products``       | A JSON object array of products in the shipment. See                    |
|                    | section "Product Details" below.                                        |
+--------------------+-------------------------------------------------------------------------+
| ``expected_at_wh`` | Date when the shipment is expected to arrive at the Logitrail's         |
|                    | warehouse. Format ``yyyy-mm-dd``.                                       |
+--------------------+-------------------------------------------------------------------------+
| ``status``         | Status of the shipment. See :doc:`statuses`                             |
+--------------------+-------------------------------------------------------------------------+
| ``problems``       | In case there are problems with the shipment (identified by Logitrail), |
|                    | the problem information is provided. See "Problem Details" below.       |
+--------------------+-------------------------------------------------------------------------+

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

Problem Details
---------------

Occassionally the inbound shipment has some problems with it. In this case, the shipment gets
a ``problem`` status and further information about the problems are provided for the merchant.

See :doc:`problems` for further information.

+--------------------+----------------------------------------------------------------------+
| ``id``             | A "problem id" given for the issue.                                  |
+--------------------+----------------------------------------------------------------------+
| ``ts``             | Timestamp of the problem report.                                     |
+--------------------+----------------------------------------------------------------------+
| ``type``           | Problem type code. See :doc:`problems`                               |
+--------------------+----------------------------------------------------------------------+
| ``description``    | Description of the problem, given by Logitrail's staff               |
+--------------------+----------------------------------------------------------------------+
| ``resolved``       | ``true`` or ``false``                                                |
+--------------------+----------------------------------------------------------------------+