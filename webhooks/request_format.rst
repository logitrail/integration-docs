Webhook Request Format
**********************

Logitrail calls a defined webhook URL with an ordinary HTTP POST request.

The request body contains details about the occurred event in JSON format. In case the webhook
URL is configured to accept multiple events at a same time (that is preferred way), array of
maximum 100 events are aggregated to the same request.

+------------------+------------------------------------------------------------------------------+
| ``event_id``     | Logitrail's internal ID for the event. The same event may raise calls        |
|                  | to more than one webhook, while the ``event_id`` stays same.                 |
+------------------+------------------------------------------------------------------------------+
| ``event_type``   | A string identifying the type of the event.                                  |
+------------------+------------------------------------------------------------------------------+
| ``webhook_id``   | The webhook called.                                                          |
+------------------+------------------------------------------------------------------------------+
| ``ts``           | Original timestamp of the event.                                             |
+------------------+------------------------------------------------------------------------------+
| ``retry_count``  | If the previous call to the webhook URL for the same event did not succeed,  |
|                  | further calls will increase the ``retry_count``.                             |
+------------------+------------------------------------------------------------------------------+
| ``payload``      | The payload is an arbitrary JSON object, providing further information       |
|                  | about the event. The payload format and data differs between different event |
|                  | types.                                                                       |
+------------------+------------------------------------------------------------------------------+

Example
=======

.. code-block:: json

    {
      "event_id": "2016-01-18T08:17:55_5499362b1fb35e73548b45af",
      "webhook_id": "logitrail.com_5499362b1fb35e73118b45ad",
      "event_type": "product.info.updated",
      "ts": "2016-01-18T08:17:55+00:00",
      "retry_count": 0,
      "payload": {
        "product": {
          "id": "5499362b1fb35e73548b45aa",
          "merchants_id": "13248",
          "name": "Puhdas+ Caps Saccharomyces boulardii, 60 kaps",
          "gtin": "6430050001025"
        }
      }
    }
