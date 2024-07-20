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

Error Responses
===============

See :doc:`/errors` for generic documentation regarding error responses.

``code`` values
---------------

+---------------------------------------+-----------+-----------------------------------------------------------------------------------------------+
| Code                                  | HTTP Code | Reason + how to fix                                                                           |
+---------------------------------------+-----------+-----------------------------------------------------------------------------------------------+
| ``order_already_cancelled``           | 400       | The order is already in cancelled status.                                                     |
+---------------------------------------+-----------+-----------------------------------------------------------------------------------------------+
| ``order_already_processing``          | 400       | The order is already in processing status and cannot be cancelled. Contact Logitrail for      |
|                                       |           | manually intercept the parcel and cancel the shipment, if possible.                           |
+---------------------------------------+-----------+-----------------------------------------------------------------------------------------------+
| ``order_already_processed``           | 400       | The order is already in processed status (i.e. sent out from the warehouse) and cannot be     |
|                                       |           | cancelled.                                                                                    |
+---------------------------------------+-----------+-----------------------------------------------------------------------------------------------+