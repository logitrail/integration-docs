Test Environment
****************

If requested by a merchant or an integrator, Logitrail provides an access to
a separate test environment. The test environment is fully separated from the production
environment and also provides an early access to new features that are not yet
in production.

Most of the Logitrail's services are available in the test environment, but
in limited manner. For example shipments are not processed (unless agreed with
Logitrail Customer Service in special occasions).

Please note that use of the test servers is limited and servers might be occassionally
offline or otherwise unavailable.

Credentials
===========

Authentication credentials (Merchant ID, Merchant Secret, User login's) are different
in the test and production environments. Credentials cannot be transferred between
the environments.

URLs
====

In general, test environment URLs are identical to production URLs but only the hostname is
different and points to the test servers.

**API Test Server**: ``https://api-1.test.logitrail.com/``
**Merchant Portal**: ``https://my.test.logitrail.com``
**Checkout Service**: ``https://checkout.test.logitrail.com``
 
From Test to Production
=======================

The test environment's interfaces differs from the production only a little bit.
When you are ready to start using the production system, you should need to do only
couple of changes in your integration:

 * Change URLs to production endpoints (HTTPS + change in the hostname)
 * Enter your production credentials (Merchant ID, Merchant Secret, user details etc...)
