Create or Modify Inbound Shipment
*********************************

The merchant should send an inbound shipment notification to Logitrail in advance before the
actual shipment arrives at the warehouse. The inbound shipment should be created prior one
day of the expected arrival date.

Inbound Shipment JSON Object
============================

While **creating** an inbound shipment or **modifying** an existing shipment, the following
JSON object structure is used.

+--------------------+----------------------------------------------------------------------+
| ``merchants_ref``  | Merchant's own reference to the inbound shipment. This can be        |
|                    | for example the purchase order number.                               |
+--------------------+----------------------------------------------------------------------+
| ``sender_name``    | Name of the sender of the shipment.                                  |
+--------------------+----------------------------------------------------------------------+
| ``products`` or    | A JSON object array of products expected in the shipment. See        |
| ``products_all``   | section "Product Details" below. When using ``products_all`` the     |
|                    | shipment contents will be updated to match the product list.         |
+--------------------+----------------------------------------------------------------------+
| ``expected_at_wh`` | Date when the shipment is expected to arrive at the Logitrail's      |
|                    | warehouse. Use format yyyy-mm-dd.                                    |
+--------------------+----------------------------------------------------------------------+

Product Details
---------------

Each product in the inbound shipment should be provided in an array of objects in
``products`` or ``products_all`` properties.

+------------------+----------------------------------------------------------------------+
| ``name``         | Name of the product                                                  |
+------------------+----------------------------------------------------------------------+
| ``merchants_id`` | Merchant's ID of the product.                                        |
+------------------+----------------------------------------------------------------------+
| ``gtin``         | EAN (GTIN) barcode of the product.                                   |
+------------------+----------------------------------------------------------------------+
| ``qty``          | Quantity of the product items expected to arrive in the shipment.    |
+------------------+----------------------------------------------------------------------+

Note that existing properties are used to update the product database. You may skip ``name`` and ``ean``
properties if you are sure that a product with ``merchants_id`` already exists in the database. See
:doc:`products` for details.

Create Inbound Shipment
=======================

+---------------+--------------------------------------------------------+
| Endpoint      | ``/inbound_shipments/_create``                         |
+---------------+--------------------------------------------------------+
| Method        | POST                                                   |
+---------------+--------------------------------------------------------+

This endpoint is used to create a new inbound shipment.

Request Parameters
------------------

The request body should contain a JSON object describing the inbound shipment.
See section "Inbound Shipment JSON Object" above.

Response
--------

Status: **HTTP 201 Created**

JSON object with following parameters.

+------------------+----------------------------------------------------------------------+
| ``success``      | ``true``                                                             |
+------------------+----------------------------------------------------------------------+
| ``shipment_id``  | Logitrail's ID for the shipment (24-digit hex)                       |
+------------------+----------------------------------------------------------------------+

Update Inbound Shipment
=======================

+---------------+--------------------------------------------------------+
| Endpoint      | ``/inbound_shipments/{id}``                            |
+---------------+--------------------------------------------------------+
| Method        | POST                                                   |
+---------------+--------------------------------------------------------+

This endpoint is used to update an existing inbound shipment.

Request Parameters
------------------

URL placeholder ``{id}`` should be replaced with the Logitrail's ID of the inbound shipment.

The request body should contain a JSON object describing the inbound shipment.
See section "Inbound Shipment JSON Object" above.

Response
--------

Status: **HTTP 200 OK**

JSON object with following parameters.

+------------------+----------------------------------------------------------------------+
| ``success``      | ``true``                                                             |
+------------------+----------------------------------------------------------------------+
| ``shipment_id``  | Logitrail's ID for the shipment (24-digit hex)                       |
+------------------+----------------------------------------------------------------------+