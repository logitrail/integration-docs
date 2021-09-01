Returns
*******

Whenever an order is returned back to Logitrail's warehouse, an order return is created to the system.

If the order is restocked, an inbound shipment is created and processed for the return.

There are two types of returns in the system (see `type` field in the return object):

 * `agent_return` is created if the customer has not picked the parcel up and the pickup point returns
   the parcel back. The parcel is unopened. An agent return can be usually sent again.
 * `customer_return` is created if the customer has opened the parcel and returns the original order only
   partially. See `inbound_shipment` for returned items.

List Order Returns
==================

+---------------+--------------------------------------------------------+
| Endpoint      | ``/orders/returns``                                    |
+---------------+--------------------------------------------------------+
| Method        | GET                                                    |
+---------------+--------------------------------------------------------+

Query Parameters
----------------

+----------------------+----------------------------------------------------------------------+
| ``status``           | Filter by status. If omitted, only "active" returns are listed.      |
|                      | (`processed` and `deleted` returns are omitted)                      |
+----------------------+----------------------------------------------------------------------+
| ``created_at_min``   | Filter by return creation date, starting from the given date.        |
+----------------------+----------------------------------------------------------------------+
| ``created_at_max``   | Filter by return creation date, ending to the given date.            |
+----------------------+----------------------------------------------------------------------+
| ``offset``           | Pagination: start listing from nth result (defaults to 0)            |
+----------------------+----------------------------------------------------------------------+
| ``limit``            | Pagination: return max given results (defaults to 250)               |
+----------------------+----------------------------------------------------------------------+

Response
--------

Status: **HTTP 200 OK**

JSON object with following parameters.

+----------------------+----------------------------------------------------------------------+
| ``id``               | Logitrail's ID for the return (24-digit hex)                         |
+----------------------+----------------------------------------------------------------------+
| ``created``          | Timestamp when the return is created to the system.                  |
+----------------------+----------------------------------------------------------------------+
| ``status``           | Return status: `pending`, `resend_pending`, `restocking_pending`,    |
|                      | `processing`, `processed`                                            |
+----------------------+----------------------------------------------------------------------+
| ``type``             | `agent_return` or `customer_return`                                  |
+----------------------+----------------------------------------------------------------------+
| ``order``            | Full order JSON of the original order.                               |
+----------------------+----------------------------------------------------------------------+
| ``inbound_shipment`` | Full inbound shipment JSON of the restocking order.                  |
+----------------------+----------------------------------------------------------------------+

