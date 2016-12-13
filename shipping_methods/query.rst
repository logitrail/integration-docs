Querying Shipping Methods and Delivery Fees
*******************************************

Logitrail provides a couple of different shipping methods that can be selected when creating an order.

The supported types of shipping methods are ``pickup``, ``home`` and ``letter``. Home and Letter deliveries
are sent to the customer by the given address. Pickup delivery requires that a pickup location is selected for
the order.

Requesting Possible Shipping Methods
====================================

Logitrail API provides two endpoints to request the possible shipping methods.

  * ``GET /shipping_options`` is a generic endpoint to request shipping options, pickup points and delivery fees
  * ``GET /order/{id}/shipping_options`` returns shipping options for the given order.

Query Available Shipping Methods
================================

**Note!** If you want to query available shipping options for an order, see :doc:`orders/shipping_options`.

+---------------+--------------------------------------------------------+
| Endpoint      | ``/shipping_options``                                  |
+---------------+--------------------------------------------------------+
| Method        | GET                                                    |
+---------------+--------------------------------------------------------+

Query Parameters
----------------

+------------------+----------------------------------------------------------------------+
| ``postalcode``   | Customer's postal code.                                              |
+------------------+----------------------------------------------------------------------+
| ``country``      | Customer's country (defaults to ``FI``)                              |
+------------------+----------------------------------------------------------------------+
| ``weight``       | Total weight of the shipment (in grams)                              |
+------------------+----------------------------------------------------------------------+

Response
--------

Status: **HTTP 200 OK**

JSON Object:

+------------------+----------------------------------------------------------------------+
| ``order_id``     | Logitrail's ID for the order (24-digit hex)                          |
+------------------+----------------------------------------------------------------------+
| ``options``      | JSON Object of the possible shipping methods.                        |
+------------------+----------------------------------------------------------------------+

**Options**

The different shipping methods are given as a properties of ``options``. Each method is presented
in the following format.

+--------------------+------------------------------------------------------------------------+
| ``available``      | ``true`` or ``false``                                                  |
+--------------------+------------------------------------------------------------------------+
| ``reason``         | Reason code if the method is not available.                            |
+--------------------+------------------------------------------------------------------------+
| ``price``          | Delivery fee (for the customer) of the given method. Note: ``pickup``  |
|                    | method does not have this property.                                    |
+--------------------+------------------------------------------------------------------------+
| ``pickup_points``  | List of (nearest and preferred) pickup points available for ``pickup`` |
|                    | delivery. Each pickup point is presented as a JSON object as described |
|                    | in :doc:`pickup_points/lookup`. An extra property ``price`` is given.  |
+--------------------+------------------------------------------------------------------------+

**Price**

The price information is given in JSON format.

+------------------+----------------------------------------------------------------------+
| ``gross``        | Gross total for the delivery fee, payable by the customer.           |
+------------------+----------------------------------------------------------------------+
| ``currency``     | Currency code.                                                       |
+------------------+----------------------------------------------------------------------+
| ``tax``          | TAX Percent (VAT)                                                    |
+------------------+----------------------------------------------------------------------+

Note: Logitrail does not charge customers directly. Instead it's up to the merchant to define the pricing model
and pass the information to the payment gateway / invoicing.

Pricing rules can be defined in the merchant portal. Read more about :doc:`rules`.

Example
-------

Request: ``GET https://api-1.logitrail.com/2015-01-01/shipping_options?postalcode=20780&country=FI``

.. code-block:: json

    {
       "facts":{
          "pup.branch":null,
          "customer.country":"FI",
          "order.shipping_type":null,
          "order.tags":[

          ],
          "order.total_eur":0,
          "order.letter_possible":false,
          "order.total_weight":0,
          "order.total_volume":0,
          "customer.postalcode":"20780",
          "customer.address":null,
          "order.item_count":0,
          "order.item_article_count":0
       },
       "options":{
          "letter":{
             "available":false,
             "reason":"item_does_not_allow"
          },
          "home":{
             "available":false,
             "reason":"merchant_disabled"
          },
          "pickup":{
             "available":true,
             "pickup_points":{
                "5692616b01250d3a458b4567":{
                   "id":"5692616b01250d3a458b4567",
                   "name":"Posti, K-supermarket Katariina",
                   "address":"Hovirinnantie 5",
                   "postalcode":"20780",
                   "city":"Kaarina",
                   "country":"FI",
                   "coordinates":[
                      60.4068057,
                      22.3631381
                   ],
                   "branch":"fi.k-supermarket",
                   "location_info":"K-supermarket Katariina ma-la 7.00 - 21.00, su 10.00 - 19.00",
                   "carrier_info":{
                      "fi_posti":{
                         "id":"207803200",
                         "label_name":"c\/o Posti, K-supermarket Katariina",
                         "type":"Posti"
                      }
                   },
                   "price":{
                      "gross":9.77,
                      "currency":"EUR",
                      "tax":24
                   }
                },
                "571c9fcc3e250d43528b4568":{
                   "id":"571c9fcc3e250d43528b4568",
                   "name":"R-kioski Kaarina",
                   "address":"Puntarikatu 1",
                   "postalcode":"20780",
                   "city":"Kaarina",
                   "country":"FI",
                   "coordinates":[
                      60.4074658,
                      22.3663125
                   ],
                   "branch":"fi.r-kioski",
                   "location_info":"ark. 08:00-21:30, la 08:00-21:30, su 09:00-21:30",
                   "carrier_info":{
                      "fi_schenker":{
                         "id":"6682"
                      }
                   },
                   "price":{
                      "gross":9.77,
                      "currency":"EUR",
                      "tax":24
                   }
                },
                "5692616b01250d3a458b4568":{
                   "id":"5692616b01250d3a458b4568",
                   "name":"Pakettiautomaatti, K-market Kaarina Center",
                   "address":"Oskarinaukio 5",
                   "postalcode":"20785",
                   "city":"Kaarina",
                   "country":"FI",
                   "coordinates":[
                      60.4078816,
                      22.3685542
                   ],
                   "branch":"fi.k-market",
                   "location_info":"Pullonpalautuksen vieress\u00e4 ma-pe 7.00 - 22.00, la 8.00 - 22.00, su 10.00 - 22.00",
                   "carrier_info":{
                      "fi_posti":{
                         "id":"207853201",
                         "label_name":"c\/o Automaatti, K-market Kaarina Center",
                         "type":"SmartPOST"
                      }
                   },
                   "price":{
                      "gross":9.77,
                      "currency":"EUR",
                      "tax":24
                   }
                },
                "56cc505f3e250d170c8b4584":{
                   "id":"56cc505f3e250d170c8b4584",
                   "name":"Siwa Kuskinkuja \/ Kaarina",
                   "address":"Kuskinkuja 1",
                   "postalcode":"20780",
                   "city":"Kaarina",
                   "country":"FI",
                   "coordinates":[
                      60.4077908,
                      22.3733018
                   ],
                   "branch":"fi.siwa",
                   "location_info":null,
                   "carrier_info":{
                      "fi_matkahuolto":{
                         "id":"5214",
                         "office":"TURKU",
                         "type":"TRS"
                      }
                   },
                   "price":{
                      "gross":9.77,
                      "currency":"EUR",
                      "tax":24
                   }
                },
                "56e2be8f3e250d241a8b456a":{
                   "id":"56e2be8f3e250d241a8b456a",
                   "name":"Tokmanni Piispanristi\/tokmanni Oy",
                   "address":"J\u00e4nnekatu 4",
                   "postalcode":"20760",
                   "city":"Kaarina",
                   "country":"FI",
                   "coordinates":[
                      60.4147772,
                      22.3287886
                   ],
                   "branch":"fi.matkahuolto",
                   "location_info":null,
                   "carrier_info":{
                      "fi_matkahuolto":{
                         "id":"8076",
                         "office":"TURKU",
                         "type":"MHN"
                      }
                   },
                   "price":{
                      "gross":9.77,
                      "currency":"EUR",
                      "tax":24
                   }
                },
                "5692616b01250d3a458b4569":{
                   "id":"5692616b01250d3a458b4569",
                   "name":"Pakettiautomaatti, Prisma Piispanristi Turku",
                   "address":"Kairiskulmantie 3",
                   "postalcode":"20765",
                   "city":"Piispanristi",
                   "country":"FI",
                   "coordinates":[
                      60.4153141,
                      22.3266782
                   ],
                   "branch":"fi.prisma",
                   "location_info":"Sis\u00e4\u00e4ntuloaulassa ma-la 8.00 - 21.00, su 10.00 - 21.00",
                   "carrier_info":{
                      "fi_posti":{
                         "id":"207653201",
                         "label_name":"c\/o Automaatti, Prisma Piispanristi Turku",
                         "type":"SmartPOST"
                      }
                   },
                   "price":{
                      "gross":9.77,
                      "currency":"EUR",
                      "tax":24
                   }
                },
                "5692616b01250d3a458b456a":{
                   "id":"5692616b01250d3a458b456a",
                   "name":"Posti, Siwa Lauste",
                   "address":"Pormestarinkatu 5",
                   "postalcode":"20750",
                   "city":"Turku",
                   "country":"FI",
                   "coordinates":[
                      60.4322632,
                      22.3449483
                   ],
                   "branch":"fi.siwa",
                   "location_info":"Siwa Lauste ma-pe 7.00 - 23.00, la 8.00 - 23.00, su 9.00 - 23.00",
                   "carrier_info":{
                      "fi_posti":{
                         "id":"207503200",
                         "label_name":"c\/o Posti, Siwa Lauste",
                         "type":"Posti"
                      }
                   },
                   "price":{
                      "gross":9.77,
                      "currency":"EUR",
                      "tax":24
                   }
                },
                "56c2f9e03e250df95a8b4594":{
                   "id":"56c2f9e03e250df95a8b4594",
                   "name":"Siwa Lauste",
                   "address":"Pormestarinkatu 5",
                   "postalcode":"20750",
                   "city":"Turku",
                   "country":"FI",
                   "coordinates":[
                      60.4325444,
                      22.3451216
                   ],
                   "branch":"fi.siwa",
                   "location_info":null,
                   "carrier_info":{
                      "fi_matkahuolto":{
                         "id":"5240",
                         "office":"TURKU",
                         "type":"TRS"
                      }
                   },
                   "price":{
                      "gross":9.77,
                      "currency":"EUR",
                      "tax":24
                   }
                },
                "5692616b01250d3a458b456b":{
                   "id":"5692616b01250d3a458b456b",
                   "name":"Pakettiautomaatti, K-citymarket Skanssi",
                   "address":"It\u00e4kaari 20",
                   "postalcode":"20735",
                   "city":"Turku",
                   "country":"FI",
                   "coordinates":[
                      60.4280545,
                      22.3227706
                   ],
                   "branch":"fi.k-citymarket",
                   "location_info":"Kassoja vastap\u00e4\u00e4t\u00e4 ma-pe 8.00 - 21.00, la 8.00 - 18.00, su 12.00 - 18.00",
                   "carrier_info":{
                      "fi_posti":{
                         "id":"207353201",
                         "label_name":"c\/o Automaatti, K-citymarket Skanssi",
                         "type":"SmartPOST"
                      }
                   },
                   "price":{
                      "gross":9.77,
                      "currency":"EUR",
                      "tax":24
                   }
                },
                "56cc505f3e250d170c8b4585":{
                   "id":"56cc505f3e250d170c8b4585",
                   "name":"R-Kioski Turku Skanssi",
                   "address":"Skanssinkatu 10",
                   "postalcode":"20730",
                   "city":"Turku",
                   "country":"FI",
                   "coordinates":[
                      60.4297193,
                      22.3193539
                   ],
                   "branch":"fi.r-kioski",
                   "location_info":null,
                   "carrier_info":{
                      "fi_matkahuolto":{
                         "id":"4512",
                         "office":"TURKU",
                         "type":"MHN"
                      }
                   },
                   "price":{
                      "gross":9.77,
                      "currency":"EUR",
                      "tax":24
                   }
                }
             }
          }
       }
    }