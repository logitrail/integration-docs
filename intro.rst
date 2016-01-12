API Introduction
****************

Logitrail API is a REST-style HTTP API, providing the merchant ways to manage most of the
Logitrail operations via their own systems.

API Endpoint
============

There are two parallel and redundant endpoints for API operations:

 * ``https://api-1.logitrail.com/2015-01-01/``
 * ``https://api-2.logitrail.com/2015-01-01/``
 
The date-like part in the URL is the API version. New and backwards incompatible operations
or endpoints will update also the version.

Test Environment
================

Logitrail provides a separate test environment to support the integration work.

Test environment is available at endpoint:

 * ``http://api-1.test.logitrail.com/2015-01-01/``

See :doc:`test_environment` for detailed information.

Authentication
==============

Most of the API requests should be sent with a proper HTTP Basic ``Authentication`` header.

By Merchant ID
--------------

+------------+----------------------------+----------------------+
| Username   | ``M-`` + Merchant ID       | ``M-logitrail.com``  |
+------------+----------------------------+----------------------+
| Password   | Merchant's Shared Secret   | ``YmanmKWi7)2Mcqa``  |
+------------+----------------------------+----------------------+

Merchant authentication is the recommended way for most API calls. The username
is your Merchant ID (most likely your domain) prefixed with ``M-``. The password
is your Merchant's Shared Secret. Both of the details are provided by Logitrail
Customer Service.

By Session ID
-------------

+------------+----------------------------+---------------------------------+
| Username   | ``S-`` + Session ID        | ``S-5812af1fa971adceabffb910``  |
+------------+----------------------------+---------------------------------+
| Password   | Session Password           | ``KMMMi(Iqlsq5&236Cas``         |
+------------+----------------------------+---------------------------------+

You may also create an API session and obtain per-session username and password.
This method is not yet fully supported.

Unauthenticated Requests
------------------------

Some operations and requests are also available without authentication. This allows the
merchant to use these endpoints in their public website. **By default, the authentication is required.**
