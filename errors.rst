Error Handling
**************

Logitrail returns an error response in case your request cannot be fulfilled. Standard
HTTP error status codes are used to give a hint of the high level reason. Further details
are provided in response body JSON parameter ``code`` and other parameters.

HTTP Error codes
================

 * 400 Bad Request. The request is malformed or contains invalid information.
 * 403 Forbidden. You are not allowed to access the requested resource or operation.
 * 404 Not Found. The URL is invalid, or the underlying resource (like order) is not found.
 * 405 Method Not Allowed. The requested HTTP Method is not allowed on this resource.
 * 409 Conflict. The request cannot be fulfilled due conflicting state or data.
 * 500 Internal Server Error. Internal failure in Logitrail's system. If the problem persists, please contact us.
 * 503 Service Unavailable. Internal failure in Logitrail's system. If the problem persists, please contact us.

Generic error response ``code`` values
======================================

The following errors may occur in any operation and/or endpoint.

+---------------------------------------+-----------+-----------------------------------------------------------------------------------------------+
| Code                                  | HTTP Code | Reason + how to fix                                                                           |
+---------------------------------------+-----------+-----------------------------------------------------------------------------------------------+
| ``unknown``                           | any       | Unknown or unclassified error. This will most likely happen in case of server error.          |
|                                       |           | Response parameter ``message`` may include further details.                                   |
+---------------------------------------+-----------+-----------------------------------------------------------------------------------------------+
| ``access_denied``                     | 403       | You are not allowed to access the requested resource or operation.                            |
+---------------------------------------+-----------+-----------------------------------------------------------------------------------------------+
| ``method_not_allowed``                | 405       | The requested HTTP Method is not allowed on this resource. Check the documentation for        |
|                                       |           | supported method(s).                                                                          |
+---------------------------------------+-----------+-----------------------------------------------------------------------------------------------+
