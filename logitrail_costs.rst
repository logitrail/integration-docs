Logitrail's Costs
*****************

To query the estimated Logitrail's costing structure you may use this endpoint.

+---------------+---------------------------------------------+
| Endpoint      | ``/logitrail_costs``                        |
+---------------+---------------------------------------------+
| Method        | POST                                        |
+---------------+---------------------------------------------+

Request Body (JSON)
-------------------

+------------------+----------------------------------------------------------------------+
| ``order_id``     | ID of the order.                                                     |
+------------------+----------------------------------------------------------------------+
| ``facts``        | Internal "facts" for costing decision.                               |
+------------------+----------------------------------------------------------------------+

Response (JSON)
---------------

+---------------------+----------------------------------------------------------------------+
| ``facts``           | Internal "facts" for costing decision.                               |
+---------------------+----------------------------------------------------------------------+
| ``cost_components`` | List of individual cost components:                                  |
|                     | ``shipping``, ``picking``, ``picking_lines``                         |
+---------------------+----------------------------------------------------------------------+
| ``total_cost``      | Total cost                                                           |
+---------------------+----------------------------------------------------------------------+

Cost components and the total cost are given as a JSON object:

+------------------+----------------------------------------------------------------------+
| ``gross``        | Gross total                                                          |
+------------------+----------------------------------------------------------------------+
| ``currency``     | Currency code (always ``EUR``)                                       |
+------------------+----------------------------------------------------------------------+
| ``tax``          | TAX Percent (VAT)                                                    |
+------------------+----------------------------------------------------------------------+
| ``net``          | Net total                                                            |
+------------------+----------------------------------------------------------------------+

Example
-------

**Request**

``POST https://api-1.logitrail.com/2015-01-01/logitrail_costs``

.. code-block:: json

    {
        "order_id": "56a3cd253e250de22d8b4567"
    }

**Response**

.. code-block:: json

    {
        "cost_components": {
            "shipping": {
                "gross": 5.58,
                "net": 4.5,
                "currency": "EUR",
                "tax": 24
            },
            "picking": {
                "gross": 3.72,
                "net": 3,
                "currency": "EUR",
                "tax": 24
            },
            "picking_lines": {
                "gross": 0.31,
                "net": 0.25,
                "currency": "EUR",
                "tax": 24
            }
        },
        "total_cost": {
            "gross": 9.61,
            "net": 7.75,
            "currency": "EUR",
            "tax": 24
        },
        "facts": {
            "pup.branch": "fi.k-market",
            "customer.country": "FI",
            "order.shipping_type": "prc_pickup",
            "order.tags": [],
            "order.total_eur": 0,
            "order.letter_possible": true,
            "order.total_weight": 0,
            "order.total_volume": 0,
            "customer.postalcode": "20780",
            "customer.address": "Juristinkatu 6",
            "order.item_count": true,
            "order.item_article_count": true,
            "pup.type": "unattended"
        }
    }