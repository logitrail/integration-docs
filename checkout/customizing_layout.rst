Customizing Checkout Layout
***************************

Merchants have possibility to use custom CSS rules in Logitrail's system
to further customize the customer's checkout experience to match the merchant's
own theme and layout.

The merchant creates a new layout in Logitrail's merchant portal. Each layout
is identified with a key (any string value). Layout with the key ``default``
is used by default.

When forwarding the customer to the checkout process, the merchant can pass
a field ``layout`` to Logitrail in the HTTP Form to apply the custom layout.

Logitrail Checkout UI is based on Twitter's Bootstrap CSS framework. Custom CSS
definitions are applied last, so they will override Bootstrap's and Logitrail's
styles by default.

Note that Logitrail CSS is served over HTTPS, so references to plain HTTP (non-HTTPS)
resources in custom CSS definitions may not work correctly in all browsers.