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

(*) = Required field.

Product Details
---------------

Each product in the order should be provided in an array of objects in
``products`` or ``products_all`` properties.

+--------------------+----------------------------------------------------------------------+
| ``name``           | Name of the product                                                  |
+--------------------+----------------------------------------------------------------------+
| ``merchants_id``   | Merchant's ID of the product.                                        |
+--------------------+----------------------------------------------------------------------+
| ``gtin``           | EAN (GTIN) barcode of the product.                                   |
+--------------------+----------------------------------------------------------------------+
| ``qty``            | Quantity of the product items expected to arrive in the shipment.    |
+--------------------+----------------------------------------------------------------------+
| ``fulfillment_by`` | Possible values are ``merchant`` and ``logitrail`` (default).        |
+--------------------+----------------------------------------------------------------------+
| ``best_before``    | Best before date restriction for the products that should be sent to |
|                    | the customer. See :doc:`best_before_dates`.                          |
+--------------------+----------------------------------------------------------------------+

Note that existing properties are used to update the product database. You may skip ``name`` and ``gtin``
properties if you are sure that a product with ``merchants_id`` already exists in the database. See
:doc:`products` for details.

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