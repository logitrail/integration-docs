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

Authentication
==============

Most of the API requests should be sent with a proper HTTP Basic authentication header.
The username is the merchant id and the password the merchant's shared secret. These details
are available via Logitrail's customer service.

Unauthenticated Requests
========================

Some operations and requests are also available without authentication. This allows the
merchant to use these endpoints in their public website. **By default, the authentication is required.**
