Order Statuses
**************

+--------------------------+----------------------------------------------------------+
| Status Code              | Description                                              |
+==========================+==========================================================+
| ``passive``              | Any new order is created to passive status. A passive    |
|                          | order must be confirmed to make Logitrail pickup and     |
|                          | send the order to the recipient.                         |
+--------------------------+----------------------------------------------------------+
| ``confirmed``            | The order is confirmed.                                  |
+--------------------------+----------------------------------------------------------+
| ``waiting_products``     | The order is waiting for products to arrive.             |
+--------------------------+----------------------------------------------------------+
| ``processed``            | The order is shipped to the recipient.                   |
+--------------------------+----------------------------------------------------------+
| ``cancelled``            | The order is cancelled (deleted) after confirmation.     |
+--------------------------+----------------------------------------------------------+
| ``deleted``              | The order is deleted before confirmation.                |
+--------------------------+----------------------------------------------------------+
