Pickup Point Lookup
*******************

Logitrail provides a direct API access to its pickup point directory.

.. warning::

    It's not recommended to do queries to the Pickup Point API when the customer
    is checking out. Use our Checkout Service (see :doc:`checkout`) instead.
    
.. warning::

    In our **Test Environment** only small portion of our pickup points are available.
    Also pickup point identifiers are different in the test and in production
    environments.

Querying Pickup Points by Customer's Address
============================================

+---------------+---------------------------------------------+
| Endpoint      | ``/pickup_points/``                         |
+---------------+---------------------------------------------+
| Method        | GET                                         |
+---------------+---------------------------------------------+

Request Parameters
------------------

This endpoint accepts only **query string** arguments.

+------------------+----------------------------------------------------------------------+
| ``postalcode``   | Postal code                                                          |
+------------------+----------------------------------------------------------------------+
| ``country``      | Country code (defaults to ``FI``)                                    |
+------------------+----------------------------------------------------------------------+

Response
--------

Status: **HTTP 200 OK**

JSON array of Pickup Point details matching the query. Each pickup point is represented
as a JSON object with following properties:

+------------------+----------------------------------------------------------------------+
| ``id``           | Our Pickup Point ID (24-digit hex)                                   |
+------------------+----------------------------------------------------------------------+
| ``name``         | Name of the pickup point                                             |
+------------------+----------------------------------------------------------------------+
| ``address``      | Address of the pickup point                                          |
+------------------+----------------------------------------------------------------------+
| ``postalcode``   | Postal code of the pickup point                                      |
+------------------+----------------------------------------------------------------------+
| ``city``         | City of the pickup point                                             |
+------------------+----------------------------------------------------------------------+
| ``country``      | Country code                                                         |
+------------------+----------------------------------------------------------------------+
| ``coordinates``  | Two-item array of the coordinates of the pickup point:               |
|                  | ``[ lat, lon ]``                                                     |
+------------------+----------------------------------------------------------------------+
| ``branch``       | The branch code of the pickup point operator. Note that this does    |
|                  | not match the carrier and multiple carriers may serve the same       |
|                  | pickup point.                                                        |
+------------------+----------------------------------------------------------------------+
| ``location_info``| Additional information about the pickup point location.              |
+------------------+----------------------------------------------------------------------+
| ``location_info``| Additional information about the pickup point location.              |
+------------------+----------------------------------------------------------------------+