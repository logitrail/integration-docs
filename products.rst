Product Information
*******************

.. toctree::
   :maxdepth: 2

   products/create_or_modify
   
Products Overview
=================

Logitrail keeps track of basic profile information of each merchant's products.
The product profiles can be updated during the lifecycle of the product.

A product is identified primarily by the merchant's product identifier
that should be unchanged within the lifecycle of the product.
Logitrail assigns also an internal product identifier for each product.

Barcode, weight and dimensions are not applicable for a product that consists of subproducts (product components).

JSON Product Document
=====================

When requesting or updating product details, the following JSON object structure
should be used.

+-------------------------+---------------------------------------------------------------+
| ``merchants_id``        | Merchant's own product id - should be unique. (required)      |
+-------------------------+---------------------------------------------------------------+
| ``name``                | Name of the product (as visible to the customers)             |
+-------------------------+---------------------------------------------------------------+
| ``gtin``                | Barcode (GTIN/EAN)                                            |
+-------------------------+---------------------------------------------------------------+
| ``weight``              | Weight of the product in grams.                               |
+-------------------------+---------------------------------------------------------------+
| ``dimensions``          | Dimensions of the product in millimeters.                     |
|                         | Property is an array of three elements, i.e. ``[30,40,50]``   |
+-------------------------+---------------------------------------------------------------+
| ``subproducts``         | In case the main product consists of multiple products,       |
|                         | the subproduct details are given in this subdocument          |
|                         | as an array.                                                  |
+-------------------------+---------------------------------------------------------------+
| ``fulfillment_by``      | The party who is responsible for fulfilling the orders.       |
|                         | Possible values are ``merchant`` and ``logitrail`` (default). |
+-------------------------+---------------------------------------------------------------+

Subproducts
-----------

+-------------------------+---------------------------------------------------------------------------+
| ``merchants_id``        | Merchant's own product id.                                                |
+-------------------------+---------------------------------------------------------------------------+
| ``amount``              | How many items of the sub-product should be included?                     |
+-------------------------+---------------------------------------------------------------------------+
| (other fields)          | (other fields can be optionally included as in the main product document) |
+-------------------------+---------------------------------------------------------------------------+

Examples
--------

Let's assume you have a product bundle that includes one book and two magazines. The full
product document describing the bundle might look like following.

.. code-block:: json

    {
        "merchants_id": "MAG_BOOK_MAG",
        "name": "Product Bundle: Vareksen Turku and Two Magazines",
        "subproducts": [
            {
                "merchants_id": "VAREKSEN_TURKU",
                "amount": 1
            },
            {
                "merchants_id": "SUOMEN_KUVALEHTI",
                "amount": 2
            }
        ]
    }
