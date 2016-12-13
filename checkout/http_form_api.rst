HTTP Form API for Logitrail Checkout
************************************

URL: ``https://checkout.logitrail.com/go``
Method: POST

New Order Fields
================

+-----------------------+---------------------------------------------------------------------------+
| ``merchant`` *        | Merchant ID                                                               |
+-----------------------+---------------------------------------------------------------------------+
| ``request`` *         | Static value: ``new_order``                                               |
+-----------------------+---------------------------------------------------------------------------+
| ``order_id`` *        | Merchant's own ID for the order.                                          |
+-----------------------+---------------------------------------------------------------------------+
| ``customer_fn`` *     | Customer's first name.                                                    |
+-----------------------+---------------------------------------------------------------------------+
| ``customer_ln`` *     | Customer's last name.                                                     |
+-----------------------+---------------------------------------------------------------------------+
| ``customer_addr`` *   | Customer's address.                                                       |
+-----------------------+---------------------------------------------------------------------------+
| ``customer_pc`` *     | Customer's postal code.                                                   |
+-----------------------+---------------------------------------------------------------------------+
| ``customer_city`` *   | Customer's postal city.                                                   |
+-----------------------+---------------------------------------------------------------------------+
| ``customer_country``  | Customer's country code in ISO 3166 two-letter format. Defaults to ``FI`` |
+-----------------------+---------------------------------------------------------------------------+
| ``customer_email``    | Customer's email address.                                                 |
+-----------------------+---------------------------------------------------------------------------+
| ``customer_phone``    | Customer's phone number in international format.                          |
+-----------------------+---------------------------------------------------------------------------+
| ``weight``            | Total weight of the order in grams (g). Optional if individual product    |
|                       | weights or details are given.                                             |
+-----------------------+---------------------------------------------------------------------------+
| ``volume``            | Total volume of the order in square meters (m3). Optional.                |
+-----------------------+---------------------------------------------------------------------------+
| ``layout``            | A custom layout to be used in the checkout. A layout consists of custom   |
|                       | theme files, like custom CSS.                                             |
+-----------------------+---------------------------------------------------------------------------+
| ``language``          | Language to be used in the checkout process. Defaults to ``fi``           |
+-----------------------+---------------------------------------------------------------------------+
| ``products_N_XXXX``   | Product details for the order are given in separate repeating fields.     |
|                       | N = index of the product (starting from 0),                               |
|                       | XXXX = the product field name. See the actual fields below.               |
+-----------------------+---------------------------------------------------------------------------+
| ``shipping_fee_mode`` | | Customize the display and handling of shipping fees.                    |
|                       | | ``hide`` = do not show shipping fees at all                             |
|                       | | ``exclude_vat`` = show shipping fees excluding VAT                      |
|                       | | (empty) = show shipping fees including VAT, default                     |
+-----------------------+---------------------------------------------------------------------------+
| ``tag``               | Add the given tag to the order. Synonym to ``tag_0`` field.               |
+-----------------------+---------------------------------------------------------------------------+
| ``tags_N``            | Add the given tags to the order. N = index of the tag, starting from 0.   |
+-----------------------+---------------------------------------------------------------------------+
| ``pricelist``         | Force checkout to use the given shipping fee price list.                  |
+-----------------------+---------------------------------------------------------------------------+
| ``mac``               | MAC Hash of the request. See MAC calculation below.                       |
+-----------------------+---------------------------------------------------------------------------+

Passing Product Details
-----------------------

Product details are given in repeating fields named after ``products_N_XXXX`` where N is index
of the product (starting from 0) and XXXX is the product field name. Product field names are as follows:

+-----------------------+---------------------------------------------------------------------------+
| ``id``                | Merchant's Product ID.                                                    |
+-----------------------+---------------------------------------------------------------------------+
| ``name``              | Merchant's Product Name.                                                  |
+-----------------------+---------------------------------------------------------------------------+
| ``amount``            | Quantity how many items are ordered.                                      |
+-----------------------+---------------------------------------------------------------------------+
| ``weight``            | Weight of one item of the product in grams.                               |
+-----------------------+---------------------------------------------------------------------------+
| ``gtin``              | Product's EAN/GTIN                                                        |
+-----------------------+---------------------------------------------------------------------------+
| ``dimensions``        | Dimensions of one item of the product in millimeters. Use string format   |
|                       | ``<width> x <height> x <depth>``, for example ``60 x 30 x 30``.           |
+-----------------------+---------------------------------------------------------------------------+
| ``price``             | Price of one item of the product, including taxes.                        |
+-----------------------+---------------------------------------------------------------------------+
| ``tax``               | Tax percentage of the product.                                            |
+-----------------------+---------------------------------------------------------------------------+

Only fields ``_id`` and ``_amount`` are required if the product is known to Logitrail before. It's recommended
to pass all information anyway.

MAC Calculation
---------------

The ``mac`` field of the request should include a base64-encoded SHA512 hash of all field values, joined
together with a pipe (|) and suffixed with the merchant's secret key. Fields are sorted in alphapetical order
by the field name (as in HTTP form). In case a field is missing completely in the request, it's not included
in the calculation. If the field is included but is empty, it's calculated into the MAC.

See our PHP Integration Examples for an example script of how to calculate the MAC.