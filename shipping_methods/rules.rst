Shipping Fee Rules
******************

Merchants can build versatile shipping fee rules to Logitrail to define the shipping fees payable
by customers. Shipping fees are visible to the customer during the Checkout process.

The pricing rule system contains three important building blocks:

 * Price list(s)
 * Base price and pricing rules
 * Price modification rules

Price Lists
===========

A price list is the main entity in the pricing rule system. Each merchant should have at least
one price list. Each price list defines the basic details for shipping fee pricing: currency,
VAT percent and VAT handling (included or excluded). Finally, a price list defines also the
fallback price that is effective if no matching pricing rules are found.

Price lists have also a **key** and **effective from date**. A key is a simple string to be used
to explicitly select the price list during the Checkout process
(see :doc:`/checkout/http_form_api` and ``pricelist`` field).
A key is not required to be unique but it's recommended.

Pricing Rules
=============

A price list contains one or more pricing rules. A rule holds one or more criteria that must all be
matched to apply the given rule and apply the defined price.

The price can be defined as including or excluding VAT, as well as a dynamically based on the costs
charged by Logitrail for any given order.

The first rule of a price list that matches will be applied, therefore the order of price rules
within the price list matters.

Price Modification Rules
========================

A price list may contain one or more price modification rules. Price modification rules work
similarly to pricing rules but they are all evaluated and matching rules modify the base price.

.. tip::

    You could create a price modification rule -2€ when an order tag "vip_customer" is defined.
    When you pass a tag ``vip_customer`` in Checkout, the customer receives 2€ discount, no matter
    which shipping method he/she selects.
