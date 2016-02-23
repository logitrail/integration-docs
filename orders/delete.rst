Delete Order
************

+---------------+---------------------------------------------+
| Endpoint      | ``/orders/{id}``                            |
+---------------+---------------------------------------------+
| Method        | DELETE                                      |
+---------------+---------------------------------------------+
| Endpoint 2    | ``/orders/{id}/_delete``                    |
+---------------+---------------------------------------------+
| Method 2      | POST                                        |
+---------------+---------------------------------------------+

This endpoint is used to delete an order. Note that two different endpoints
are provided: with POST method and with DELETE method.

An order can be deleted any time before the order is picked up and shipped by Logitrail.

Request Parameters
==================

URL placeholder ``{id}`` should be replaced with the Logitrail's ID of the order.

The request body should be empty.

Response
========

Order Deleted Successfully
--------------------------

Status: **HTTP 200 OK**

JSON object with following parameters.

+------------------+----------------------------------------------------------------------+
| ``success``      | ``true``                                                             |
+------------------+----------------------------------------------------------------------+