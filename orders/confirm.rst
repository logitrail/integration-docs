Confirm Order
*************

A created order must be confirmed with a separate call to Logitrail. This call
can be done asynchronously after you have received the payment for the order or
otherwise previewed the order.

+---------------+--------------------------------------------------------+
| Endpoint      | ``/orders/{id}/_confirm``                              |
+---------------+--------------------------------------------------------+
| Method        | POST                                                   |
+---------------+--------------------------------------------------------+

Request Parameters
------------------

URL placeholder ``{id}`` should be replaced with the Logitrail's ID of the order.

The request body may contain a JSON object describing order details that should
be updated. See section "Order JSON Object" in :doc:`create_or_modify`.

Response
--------

Status: **HTTP 200 OK**

JSON object with following parameters.

+-------------------+----------------------------------------------------------------------+
| ``success``       | ``true``                                                             |
+-------------------+----------------------------------------------------------------------+
| ``order_id``      | Logitrail's ID for the order (24-digit hex)                          |
+-------------------+----------------------------------------------------------------------+
| ``tracking_code`` | Tracking code for the order, to be passed for the customer.          |
+-------------------+----------------------------------------------------------------------+
| ``tracking_url``  | Tracking URL for the order, to be passed for the customer.           |
+-------------------+----------------------------------------------------------------------+