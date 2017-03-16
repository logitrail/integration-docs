Embed Shipping Fees Widget to Your Site
***************************************

Logitrail provides a simple iframe shipping fee widget that can
be embedded to the e-commerce store.

The base URL for the widget is ``https://checkout.logitrail.com/shipping_fees?``

Certain query string parameters can be added to the URL to modify the widget:

+-------------------+---------------------------------------------------------------------------+
| ``merchant`` *    | Merchant's ID                                                             |
+-------------------+---------------------------------------------------------------------------+
| ``_locale``       | Language of the widget ``fi``, ``en`` or ``sv``                           |
+-------------------+---------------------------------------------------------------------------+
| ``weight``        | The (estimated) weight of the shipment, if known. Given in kilograms (kg) |
+-------------------+---------------------------------------------------------------------------+
| ``postalcode``    | Postal code of the customer, if known.                                    |
+-------------------+---------------------------------------------------------------------------+
| ``country``       | Country of the customer, if known.                                        |
+-------------------+---------------------------------------------------------------------------+

Only ``merchant`` parameter is mandatory.