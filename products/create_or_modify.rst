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
See :doc:`../products` for definitions.

``merchants_id`` is required in the given JSON.

Response
--------

Status: **HTTP 200 OK** or **HTTP 201 Created**

+------------------+----------------------------------------------------------------------+
| ``success``      | ``true``                                                             |
+------------------+----------------------------------------------------------------------+
| ``created``      | ``true`` (when a new product is created)                             |
+------------------+----------------------------------------------------------------------+

Update Product
==============

Updating a product is done similarly as creating a new product. When ``merchants_id`` already
exists in the database, the product is updated, otherwise it's created.
