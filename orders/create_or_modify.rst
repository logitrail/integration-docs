Create or Modify Order
**********************

An order is merchant's intention that Logitrail should ship certain products to
a recipient (customer).

The easiest way to submit orders to Logitrail is via :doc:`../checkout` but orders
can be submitted also via API calls.

Order JSON Object
=================

While **creating** an order or **modifying** an existing order, the following
JSON object structure is used.

+----------------------+----------------------------------------------------------------------+
| ``merchants_order``  | If a string, merchant's order ID. Can be also JSON hash of ID + time:|
|                      | ``{"id":<merchant's id>, "time": <original order time>}``            | 
+----------------------+----------------------------------------------------------------------+
| ``customer``         | Customer (recipient) details. See section "Customer Details" below.  |
+----------------------+----------------------------------------------------------------------+
| ``products`` or      | Product details in the order. See section "Product Details" below.   |
| ``products_all``     |                                                                      |
+----------------------+----------------------------------------------------------------------+
| ``destination``      | Destination, where the order should be actually shipped. See         |
|                      | "Destinations" below.                                                |
+----------------------+----------------------------------------------------------------------+
| ``not_before``       | Earliest date when the shipment should arrive at the customer.       |
+----------------------+----------------------------------------------------------------------+
| ``not_after``        | Latest date when the shipment should arrive at the customer.         |
+----------------------+----------------------------------------------------------------------+
| ``tags``             | Array of tags to set to the order.                                   |
| ``tags_all``         |                                                                      |
+----------------------+----------------------------------------------------------------------+
| ``language``         | Language of the order (``fi``, ``en`` or ``sv``)                     |
+----------------------+----------------------------------------------------------------------+
| ``pricelist``        | Apply the specified pricelist for the order.                         |
|                      | See :doc:`/shipping_methods/rules`                                   |
+----------------------+----------------------------------------------------------------------+
| ``currency``         | Currency code (default `EUR`)                                        |
+----------------------+----------------------------------------------------------------------+

Customer Details
----------------

Customer details are used in multiple phases of the order fulfillment process:

 * Logitrail sends the delivery notification for the customer via e-mail and SMS
 * Customer's name and details are printed on the package slip
 * Arrival notification is sent via e-mail, SMS and/or as a letter
 * Customer's preferred pickup points are saved and suggested in later checkouts

+----------------------+----------------------------------------------------------------------+
| ``lastName`` (*)     | Customer's last (family) name.                                       |
+----------------------+----------------------------------------------------------------------+
| ``firstName`` (*)    | Customer's first name                                                |
+----------------------+----------------------------------------------------------------------+
| ``organizationName`` | Organization name (for business customers)                           |
+----------------------+----------------------------------------------------------------------+
| ``address`` (*)      | Address line (street address)                                        |
+----------------------+----------------------------------------------------------------------+
| ``postalCode`` (*)   | Postal code                                                          |
+----------------------+----------------------------------------------------------------------+
| ``city`` (*)         | City                                                                 |
+----------------------+----------------------------------------------------------------------+
| ``countryCode``      | 2-letter country code of the address. Defaults to ``FI`` (Finland)   |
+----------------------+----------------------------------------------------------------------+
| ``email``            | Customer's email address.                                            |
+----------------------+----------------------------------------------------------------------+
| ``phoneNumber``      | Customer's phone number in international format.                     |
+----------------------+----------------------------------------------------------------------+
| ``eori``             | Customer's EORI Number.                                              |
+----------------------+----------------------------------------------------------------------+
| ``vat_id``           | Customer's VAT ID                                                    |
+----------------------+----------------------------------------------------------------------+

(*) = Required field.

Product Details
---------------

Each product in the order should be provided in an array of objects in
``products`` or ``products_all`` properties.

+---------------------------+----------------------------------------------------------------------+
| ``qty``                   | Quantity of the product items ordered. (required)                    |
+---------------------------+----------------------------------------------------------------------+
| ``merchants_id``          | Merchant's ID of the product. (required)                             |
+---------------------------+----------------------------------------------------------------------+
| ``unit_price``            | Unit price of the order item. Note: Price is not updated to          |
|                           | the product profile, it must be given in each order item separately. |
+---------------------------+----------------------------------------------------------------------+
| ``tax_percent``           | Tax percentage. Note: not updated to the product profile.            |
+---------------------------+----------------------------------------------------------------------+
| ``name``                  | Name of the product.  (required if not existing product)             |
+---------------------------+----------------------------------------------------------------------+
| ``gtin``                  | EAN (GTIN) barcode of the product.                                   |
+---------------------------+----------------------------------------------------------------------+
| ``fulfillment_by``        | Possible values are ``merchant`` and ``logitrail`` (default).        |
+---------------------------+----------------------------------------------------------------------+
| ``best_before``           | Best before date restriction for the products that should be sent to |
|                           | the customer. See :doc:`best_before_dates`.                          |
+---------------------------+----------------------------------------------------------------------+
| ``weight``                | Weight of the product (in grams)                                     |
+---------------------------+----------------------------------------------------------------------+
| ``dimensions``            | Dimensions of the product (in millimeters), given as a string        |
|                           | ``"W x H x D"`` or an array ``[w, h, d]``                            |
+---------------------------+----------------------------------------------------------------------+
| ``taric_code``            | 10-digit TARIC Code of the product. See                              |
|                           | https://en.wikipedia.org/wiki/TARIC_code                             |
+---------------------------+----------------------------------------------------------------------+
| ``manufacturing_country`` | Manufacturing Country of the product. See                            |
|                           | https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2                     |
+---------------------------+----------------------------------------------------------------------+
| ``additional_info``       | Free text information about the line item.                           |
+---------------------------+----------------------------------------------------------------------+

Note that given properties are used to update the product database. You may skip ``name`` and ``gtin``
properties if you are sure that a product with ``merchants_id`` already exists in the database. See
:doc:`products` for details.

`currency`, `unit_price` and `tax_percent` are persisted only each order item and NOT updated
to the product database.

Destinations   
------------

The destination of the order should be described in ``destination`` parameter.

+--------------------+---------------------------------------------------------------------------+
| <24-digit-hex>     | The pickup point ID where the customer picks the shipment up.             |
|                    | See :doc:`/pickup_points` for details.                                    |
+--------------------+---------------------------------------------------------------------------+
| ``letter``         | The shipment should be sent to the customer's address as a letter.        |
+--------------------+---------------------------------------------------------------------------+
| ``home``           | The shipment should be sent to the customer's address as a parcel/courier |
|                    | delivery.                                                                 |
+--------------------+---------------------------------------------------------------------------+

Create Order
============

+---------------+--------------------------------------------------------+
| Endpoint      | ``/orders/_create``                                    |
+---------------+--------------------------------------------------------+
| Method        | POST                                                   |
+---------------+--------------------------------------------------------+

This endpoint is used to create a new order. A new order is always created
to ``passive`` status and should be confirmed with a separate call.

Request Parameters
------------------

The request body should contain a JSON object describing the order.
See section "Order JSON Object" above.

Response
--------

Status: **HTTP 201 Created**

JSON object with following parameters.

+------------------+----------------------------------------------------------------------+
| ``success``      | ``true``                                                             |
+------------------+----------------------------------------------------------------------+
| ``order_id``     | Logitrail's ID for the order (24-digit hex)                          |
+------------------+----------------------------------------------------------------------+

Update Order
============

+---------------+--------------------------------------------------------+
| Endpoint      | ``/orders/{id}``                                       |
+---------------+--------------------------------------------------------+
| Method        | POST                                                   |
+---------------+--------------------------------------------------------+

This endpoint is used to update an existing order details.

Request Parameters
------------------

URL placeholder ``{id}`` should be replaced with the Logitrail's ID of the order.

The request body should contain a JSON object describing the order.
See section "Order JSON Object" above.

Response
--------

Status: **HTTP 200 OK**

JSON object with following parameters.

+------------------+----------------------------------------------------------------------+
| ``success``      | ``true``                                                             |
+------------------+----------------------------------------------------------------------+
| ``order_id``     | Logitrail's ID for the order (24-digit hex)                          |
+------------------+----------------------------------------------------------------------+

Confirm Order
============

A created order **must** be confirmed with a separate API call. See :doc:`confirm`.

Error Responses
===============

See :doc:`/errors` for generic documentation regarding error responses.

``code`` values
---------------

+---------------------------------------+-----------+-----------------------------------------------------------------------------------------------+
| Code                                  | HTTP Code | Reason + how to fix                                                                           |
+---------------------------------------+-----------+-----------------------------------------------------------------------------------------------+
| ``order_not_passive``                 |           | The order is requested to be confirmed (``status`` in modification/creation request)          |
|                                       |           | but the order is already confirmed or in another status but ``passive``.                      |
+---------------------------------------+-----------+-----------------------------------------------------------------------------------------------+
| ``product.merchants_id.required``     | 400       | ``products`` or ``products_all` item does not include ``merchants_id`` or it is empty.        |
|                                       |           | Every product must have merchants_id (SKU).                                                   |
+---------------------------------------+-----------+-----------------------------------------------------------------------------------------------+
| ``item_source_id_missing``            | 400       | At least one product item contains ``source_id`` field, but there is also an item without it. |
|                                       |           | If you use ``source_id`` in product item lines, add it to every item.                         |
+---------------------------------------+-----------+-----------------------------------------------------------------------------------------------+
| ``item_source_id_missing``            | 400       | At least one product item contains ``source_id`` field, but there is also an item without it. |
|                                       |           | If you use ``source_id`` in product item lines, add it to every item.                         |
+---------------------------------------+-----------+-----------------------------------------------------------------------------------------------+