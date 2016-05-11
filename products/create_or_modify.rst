Create or Modify Products
*************************

Logitrail adds products to the product database automatically when a new inbound shipment or
outgoing order is sent. You can optionally add and/or update products to the database with a separate API request.

Create Product
==============

+---------------+--------------------------------------------------------+
| Endpoint      | ``/products/``                                         |
+---------------+--------------------------------------------------------+
| Method        | POST                                                   |
+---------------+--------------------------------------------------------+

This endpoint is used to create a new product.

Request Parameters
------------------

The request body should contain a JSON object describing the product.
See :doc:´/products` for definitions.

Response
--------

Status: **HTTP 200 OK** or **HTTP 201 Created**

+------------------+----------------------------------------------------------------------+
| ``success``      | ``true``                                                             |
+------------------+----------------------------------------------------------------------+
| ``created``      | ``true`` (when a new product is created)                             |
+------------------+----------------------------------------------------------------------+

