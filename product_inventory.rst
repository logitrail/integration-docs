Product Inventory
*****************

When the merchant outsources the full warehouse management to Logitrail,
the product inventory and stock status management becomes extremely
important integration point.

Logitrail acts as a master datasource and is responsible for maintaining
the actual product quantities in different phases of the product lifecycle
in the warehouse. Logitrail provides multiple integration methods to make use
of the quantities.

Inventory Quantities
====================

There are multiple types of inventory quantities that Logitrail provides for
the merchant.

 * **Inbound** is a quantity of items expected to arrive at Logitrail in
   the near future. This value gets updated when
   :doc:`an inbound shipment <inbound_shipments>` notification is sent.
 * **In Stock** is a quantity of items that are currently in Logitrail's warehouse.
 * **Available** is a quantity of items that are currently available for new orders.
 * **Reserved** is a quantity of items that are currently in stock
   but reserved for existing orders.
 * **On Hold** is a quantity of items that are currently in Logitrail's
   warehouse but not available for orders or shipments.

All quantities, expect *Inbound*, is provided individually for each product lot,
as well as aggregated as a total for the product (all lots together).
   
Product Lots
============

Whenever a new identifiable product lot arrives at Logitrail's warehouse,
a new lot is created for the product. A lot is identified with following
details of the product:

 * Best Before Date
 * Lot Number

In case items from the same lot arrives at Logitrail's warehouse at different
times, they are combined together.

Requesting Individual Product Inventory (JSON)
==============================================

+---------------+--------------------------------------------------------+
| Endpoint      | ``/product/inventory``                                 |
+---------------+--------------------------------------------------------+
| Method        | POST or GET                                            |
+---------------+--------------------------------------------------------+

Request Parameters
------------------

+------------------+----------------------------------------------------------------------+
| ``merchants_id`` | Merchant's Product ID                                                |
+------------------+----------------------------------------------------------------------+
| ``id``           | Logitrail's Product ID                                               |
+------------------+----------------------------------------------------------------------+

The request parameters might be provided as JSON object in the body (POST request) or
as the HTTP GET parameters in the query string.

Response
--------

Status: **HTTP 200 OK**

The response contains a :ref:`Product Inventory JSON object <product_inventory_json_object>`
of the single found product.

Requesting Inventory of Multiple Products (JSON)
================================================

+---------------+--------------------------------------------------------+
| Endpoint      | ``/products/inventory``                                |
+---------------+--------------------------------------------------------+
| Method        | POST or GET                                            |
+---------------+--------------------------------------------------------+

Request Parameters
------------------

+-------------------------+---------------------------------------------------------------+
| ``merchants_id_list[]`` | List of merchant's product identifiers.                       |
+-------------------------+---------------------------------------------------------------+
| ``offset``              | Where to start results? (Defaults = 0)                        |
+-------------------------+---------------------------------------------------------------+
| ``limit``               | How many results to return? (Defaults/max = 500)              |
+-------------------------+---------------------------------------------------------------+
| ``after``               | Return only movements after or at the given time. (ISO 8901)  |
+-------------------------+---------------------------------------------------------------+

The request parameters might be provided as JSON object in the body (POST request) or
as the HTTP GET parameters in the query string.

In case you provide the parameters as a JSON object, you should provide ``merchants_id_list``
as a JSON array.

.. code-block:: json

    {
        "merchants_id_list": ["VAREKSEN_TURKU", "PUIKULA_JALKIUUNI"]
    }

Response
--------

Status: **HTTP 200 OK**

The response contains always a JSON object containing information about
the result set. Each found product is given as defined in
:ref:`Product Inventory JSON object <product_inventory_json_object>`.

.. code-block:: json

    {
        "total_count": <total count of results>,
        "offset": <offset of this request>,
        "count": <products in this result set>,
        "products": [ array of product inventory objects ]
    }

.. _product_inventory_json_object:

Product Inventory JSON Object
=============================

When product inventory information is requested, Logitrail provides the info as a JSON
object described below (a single product).

+-------------------+----------------------------------------------------------------------+
| ``merchants_id``  | Merchant's Product ID                                                |
+-------------------+----------------------------------------------------------------------+
| ``logitrail_id``  | Logitrail's Product ID                                               |
+-------------------+----------------------------------------------------------------------+
| ``name``          | Product's Name                                                       |
+-------------------+----------------------------------------------------------------------+
| ``ean``           | Product's EAN                                                        |
+-------------------+----------------------------------------------------------------------+
| ``inventory``     | Inventory sub-document with quantities.                              |
+-------------------+----------------------------------------------------------------------+
| ``.inbound``      | Inbound quantity                                                     |
+-------------------+----------------------------------------------------------------------+
| ``.in_stock``     | In Stock quantity                                                    |
+-------------------+----------------------------------------------------------------------+
| ``.available``    | Available quantity                                                   |
+-------------------+----------------------------------------------------------------------+
| ``.reserved``     | Reserved quantity                                                    |
+-------------------+----------------------------------------------------------------------+
| ``.on_hold``      | On Hold quantity                                                     |
+-------------------+----------------------------------------------------------------------+
| ``.last_movement``| Timestamp of the last movement/update in the quantities (ISO 8601)   |
+-------------------+----------------------------------------------------------------------+
| ``lots``          | If there are product lots for the product, lot information is given  |
|                   | in this property as sub-document hash. Keys are Logitrail's internal |
|                   | identifications for the lot.                                         |
+-------------------+----------------------------------------------------------------------+
| ``.lot_number``   | Lot Number (as given in the product items)                           |
+-------------------+----------------------------------------------------------------------+
| ``.best_before``  | Best Before Date (in format yyyy-mm-dd)                              |
+-------------------+----------------------------------------------------------------------+
| ``.inventory``    | Inventory quantities in the same format as in the parent document.   |
+-------------------+----------------------------------------------------------------------+

Example
-------

.. code-block:: json

    {
        "logitrail_id": "57fcd113aac87194fedde81d",
        "merchants_id": "PUIKULA_JALKIUUNI",
        "name": "Fazer Puikula - Pehmeämpi jälkiuuni",
        "ean": "6413466124007",
        "inventory": {
            "inbound": 5,
            "in_stock": 3,
            "available": 0,
            "reserved": 3,
            "on_hold": 0,
            "last_movement": "2015-12-17T15:09:04+00:00",
        },
        "lots": {
            "57fcd113aac87194faade89c": {
                "best_before": "2015-12-19",
                "inventory": {
                    "inbound": 5,
                    "in_stock": 3,
                    "available": 0,
                    "reserved": 3,
                    "on_hold": 0,
                    "last_movement": "2015-12-17T15:09:04+00:00",
                }
            }
        }
    }

In the above example you can see that Logitrail has three (3) items of the product
in the warehouse. All items are already reserved and no products are available.
There are five (5) items inbound, i.e. coming within couple of days.