Subproducts (Product Bundles)
*****************************

Subproducts (or Bundled Products or Component Products) is Logitrail's feature that allows you to
bundle multiple existing products into one orderable product.

For example, you may build a product bundle that contains one newspaper and two chocolate bars:

.. code-block:: json

    {
        "merchants_id": "READ_AND_EAT_CHOCOLATE",
        "name": "Product Bundle: Read and Eat Chocolate (Magazine + 2 Chocolate Bars)",
        "subproducts": [
            {
                "merchants_id": "FINANCIAL_TIMES",
                "amount": 1
            },
            {
                "merchants_id": "FAZER_BLUE_CHOCOLATE_BAR",
                "amount": 2
            }
        ]
    }

When a bundled product (the main product) is ordered, Logitrail will internally convert the main
product to defined subproducts. Therefore, 1 x READ_AND_EAT_CHOCOLATE will actually ship as
1 x FINANCIAL_TIMES + 2 x FAZER_BLUE_CHOCOLATE_BAR.

Creating Product Bundles
========================

Product bundles should be created with a Create Product API call with proper ``subproducts`` parameter **before**
orders are placed. See :doc:`create_or_modify` for more information.

Subproducts must be created before a product bundle (main product) is created. Creating a product bundle
with unknown subproduct will raise an error.

Other product bundles cannot be defined as subproducts.

Product Bundle Orders
=====================

Product bundles are handled as normal products when creating an order. In the example case above,
you should place an order of 1 x READ_AND_EAT_CHOCOLATE.

Note that individual subproducts should not be included in the order, except if the subproducts
are also ordered separately. In the example case above, customer could order third chocolate bar,
making the correct order as 1 x READ_AND_EAT_CHOCOLATE + 1 x FAZER_BLUE_CHOCOLATE_BAR.
Logitrail would then ship 1 x FINANCIAL_TIMES + 3 x FAZER_BLUE_CHOCOLATE_BAR.

Inbound Shipments
=================

Product bundles must not be included in inbound shipments.

Product Inventory
=================

Product bundle products are reported as individual products in the Product Inventory API (see :doc:`../product_inventory`),
but only ``available`` quantity is reported. Other values are not available.