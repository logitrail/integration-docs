Handling Best Before Dates
**************************

Logitrail tracks the best before date (expiration date) of each product in the warehouse, where applicable.
Products are sent out to customers in first-expiring-first-out basis.

The merchant may want to sell certain, near-expiring products in discounted price. As a result, the merchant
should communicate the required best before date back to Logitrail. Logitrail is then able to send the proper
discounted product to the customers, as well as not to send near-expiring dates to customers paying non-discounted price.

Best Before Dates in Warehouse
==============================

Logitrail provides information about existing best before dates and their availability in product inventory
document, see :doc:`/product_inventory` for details.

It's up to e-commerce store implementation how to handle the information internally.

Orders
======

When an order is placed, the merchant may pass ``best_before`` date field when creating or modifying the order.
Ssee :doc:`/orders/create_or_modify` for details.

If no explicit ``best_before`` date is defined, Logitrail will always reserve the first-expiring product items
for the order. If products with the explicitly defined date is not available, Logitrail reserves items with later best before date,
but never earlier.

Example
=======

Let's assume that there are four items of a certain product, with two different best before dates.

+-------------+----------------------+-----------------------------+
| **Item #**  | **Expiration Date**  | **Reserved For**            | 
+-------------+----------------------+-----------------------------+
| 1           | 2017-06-27           | Available                   |
+-------------+----------------------+-----------------------------+
| 2           | 2017-06-27           | Available                   |
+-------------+----------------------+-----------------------------+
| 3           | 2017-09-01           | Available                   |
+-------------+----------------------+-----------------------------+
| 4           | 2017-09-01           | Available                   |
+-------------+----------------------+-----------------------------+

A new order (A) is placed **without ``best_before``** field. The first-expiring product is reserved for the order.

+-------------+----------------------+-----------------------------+
| **Item #**  | **Expiration Date**  | **Reserved For**            | 
+-------------+----------------------+-----------------------------+
| 1           | 2017-06-27           | Order (A)                   |
+-------------+----------------------+-----------------------------+
| 2           | 2017-06-27           | Available                   |
+-------------+----------------------+-----------------------------+
| 3           | 2017-09-01           | Available                   |
+-------------+----------------------+-----------------------------+
| 4           | 2017-09-01           | Available                   |
+-------------+----------------------+-----------------------------+

A new order (B) is placed **with ``best_before`` = 2017-08-30**. Due there are no items explicitly expiring on 30th Aug 2017,
the next expiring product is reserved for the order.

+-------------+----------------------+-----------------------------+
| **Item #**  | **Expiration Date**  | **Reserved For**            | 
+-------------+----------------------+-----------------------------+
| 1           | 2017-06-27           | Order (A)                   |
+-------------+----------------------+-----------------------------+
| 2           | 2017-06-27           | Available                   |
+-------------+----------------------+-----------------------------+
| 3           | 2017-09-01           | Order (B)                   |
+-------------+----------------------+-----------------------------+
| 4           | 2017-09-01           | Available                   |
+-------------+----------------------+-----------------------------+

A new order (C) is placed **without ``best_before``** field. As again, first-expiring product is reserved for the order.

+-------------+----------------------+-----------------------------+
| **Item #**  | **Expiration Date**  | **Reserved For**            | 
+-------------+----------------------+-----------------------------+
| 1           | 2017-06-27           | Order (A)                   |
+-------------+----------------------+-----------------------------+
| 2           | 2017-06-27           | Order (C)                   |
+-------------+----------------------+-----------------------------+
| 3           | 2017-09-01           | Order (B)                   |
+-------------+----------------------+-----------------------------+
| 4           | 2017-09-01           | Available                   |
+-------------+----------------------+-----------------------------+