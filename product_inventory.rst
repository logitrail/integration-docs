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

 * Purchase price of the products (as given in inbound shipment notification)
 * Best Before Date
 * Lot Number

In case items from the same lot arrives at Logitrail's warehouse at different
times, they are combined together.

Requesting Individual Product Inventory (JSON)
==============================================

+---------------+--------------------------------------------------------+
| Endpoint      | ``/products/inventory``                                |
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

The request parameters might be provided as JSON object in the body (POST request) or
as the HTTP GET parameters in the query string.

**Requesting by Merchant's own product identifiers**

+-------------------------+---------------------------------------------------------------+
| ``merchants_id_list[]`` | List of merchant's product identifiers.                       |
+-------------------------+---------------------------------------------------------------+

In case you provide the parameters as a JSON object, you should provide ``merchants_id_list``
as a JSON array.

.. code-block:: json

    {
        "merchants_id_list": ["VAREKSEN_TURKU", "PUIKULA_JALKIUUNI"]
    }

**Requesting by last movements**

+-------------------------+---------------------------------------------------------------+
| ``after``               | Return only movements after or at the given time. (ISO 8901)  |
+-------------------------+---------------------------------------------------------------+
| ``offset``              | Where to start results? (Defaults = 0)                        |
+-------------------------+---------------------------------------------------------------+
| ``limit``               | How many results to return? (Defaults/max = 500)              |
+-------------------------+---------------------------------------------------------------+

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

+----------------------+----------------------------------------------------------------------+
| ``merchants_id``     | Merchant's Product ID                                                |
+----------------------+----------------------------------------------------------------------+
| ``id``               | Logitrail's Product ID                                               |
+----------------------+----------------------------------------------------------------------+
| ``name``             | Product's Name                                                       |
+----------------------+----------------------------------------------------------------------+
| ``gtin``             | Product's GTIN (EAN)                                                 |
+----------------------+----------------------------------------------------------------------+
| ``inventory``        | Inventory sub-document with quantities.                              |
+----------------------+----------------------------------------------------------------------+
| ``.inbound``         | Inbound quantity                                                     |
+----------------------+----------------------------------------------------------------------+
| ``.in_stock``        | In Stock quantity                                                    |
+----------------------+----------------------------------------------------------------------+
| ``.available``       | Available quantity                                                   |
+----------------------+----------------------------------------------------------------------+
| ``.reserved``        | Reserved quantity                                                    |
+----------------------+----------------------------------------------------------------------+
| ``.on_hold``         | On Hold quantity                                                     |
+----------------------+----------------------------------------------------------------------+
| ``.last_movement``   | Timestamp of the last movement/update in the quantities (ISO 8601)   |
+----------------------+----------------------------------------------------------------------+
| ``.best_before``     | Earliest available best before date, if applicable. See              |
|                      | :ref:`Best Before Dates <best_before_dates>` below.                  |
+----------------------+----------------------------------------------------------------------+
| ``.availability_by`` | Grouped available/reserved quantities.                               |
|                      | Contains currently only only ``best_before_dates``.                  |
+----------------------+----------------------------------------------------------------------+

.. _best_before_dates:

Best Before Dates
=================

Logitrail tracks the best before dates (also known as expiration dates) of the product articles
in the inventory. This information is communicated to the merchant in the inventory document.

``best_before`` field contains information about **the earliest available** best before date.

``availability_by.best_before_dates`` object contains details about availability by a certain
product lot.

Example
=======

.. code-block:: json

    {
        "id": "57fcd113aac87194fedde81d",
        "merchants_id": "PUIKULA_JALKIUUNI",
        "name": "Fazer Puikula - Pehmeämpi jälkiuuni",
        "ean": "6413466124007",
        "inventory": {
            "inbound": 5,
            "in_stock": 8,
            "available": 5,
            "reserved": 3,
            "on_hold": 0,
            "last_movement": "2017-06-26T15:09:04+00:00",
            "best_before": "2017-08-02",
            "availability_by": {
                "best_before_dates": {
                    "2017-08-02": {
                        "available": 2,
                        "reserved": 2
                    },
                    "2017-12-19": {
                        "available": 3,
                        "reserved": 1
                    },
                }
            }
        }
    }

In the above example you can see that Logitrail has three (8) items of the product
in the warehouse. Three (3) of the items are reserved, while five (5) are yet available
for new orders.

The earliest available best before date is 2nd Aug 2017. In the warehouse, there are also
items with best before date 19th Dec 2017.

There are five (5) items inbound, i.e. coming within couple of days. Last
warehouse movement happened 26th Jun 2017 at 15:09:04 UTC (18:09:04 Finnish time).