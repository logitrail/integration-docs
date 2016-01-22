Inbound Shipment Problems
*************************

Occassionally the inbound shipment has some problems with it. In this case, the shipment gets
a ``problem`` status and further information about the problems are provided for the merchant.

Problem Types
=============

+--------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------+
| Type Code                                        | Description                                                                                                           |
+==================================================+=======================================================================================================================+
| ``product.missing``                              | A product was missing from the arrived shipment. See :doc:`get` to request the shipment contents and arrived amounts. |
+--------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------+
| ``product.not_ok``                               | An arrived product is not in acceptable state. See the problem description for further details.                       |
+--------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------+
| ``product.extra``                                | The shipment contained products that were not reported.                                                               |
+--------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------+
| ``damaged``                                      | The whole shipment was damaged in transit and cannot be handled.                                                      |
+--------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------+

Resolving Problems
==================

An inbound shipment problem should be resolved by the merchant and the shipment updated accordingly. For example, if a missing product is not expected to arrive
at all, the product should be removed from the shipment. Removal can be done over API (by updating the quantities) or over Merchant's Portal.

After Logitrail identifies that the problem is resolved, the shipment processing continues normally.