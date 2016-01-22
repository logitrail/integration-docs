Request Examples
****************

This page includes a sample flow of API requests related to an inbound shipment.

Submit Inbound Shipment
=======================

A merchant places a purchase order to their supplier (*New Organics Oy*). At the same
time, the merchant sends an inbound shipment notification to Logitrail. The merchant
has ordered two different products, 6 items of each. At this point, the merchant
does not know when the shipment is expected to arrive at Logitrail.

Logitrail responds with Logitrail's shipment identifier. This value should be
saved by the merchant for possible updates.

``POST https://api-1.logitrail.com/2015-01-01/inbound_shipments/_create``

.. code-block:: json

    {
      "merchants_ref": "46057",
      "sender_name": "New Organics Oy",
      "products": [
        {
          "merchants_id": "13248",
          "name": "Puhdas+ Caps Saccharomyces boulardii, 60 kaps",
          "gtin": "6430050001025",
          "qty": 6
        },
        {
          "merchants_id": "18504",
          "name": "Puhdas+ Caps Kollageeni & Biotiini kampanjapakkaus",
          "gtin": "6430050001766",
          "qty": 6
        },
      ]
    }

``201 Created``

.. code-block:: json

    {
      "success": true,
      "shipment_id": "56987b391fb35ebd798b4573"
    }

Modify Inbound Shipment
=======================

The supplier confirms the order to the merchant. At this point, the merchant updates
the inbound shipment with the expected arrival date (*18th Jan 2016*).

``POST https://api-1.logitrail.com/2015-01-01/inbound_shipments/56987b391fb35ebd798b4573``

.. code-block:: json

    {
      "expected_at_wh": "2016-01-18"
    }

``200 OK``

.. code-block:: json

    {
      "success": true,
      "shipment_id": "56987b391fb35ebd798b4573"
    }

Webhook of Arrived Items
========================

When the items arrive at Logitrail's warehouse, Logitrail sends a webhook notification
to merchant's system.

.. note::

    Information about webhooks are added later.

Get Inbound Shipment Information
================================

``GET https://api-1.logitrail.com/2015-01-01/inbound_shipments/56987b391fb35ebd798b4573``

.. code-block:: json

    {
      "id": "56987b391fb35ebd798b4573",
      "merchants_ref": "46057",
      "sender_name": "New Organics Oy",
      "status": "initial",
      "products": [
        {
          "product": {
            "id": "5499362b1fb35e73548b45aa",
            "merchants_id": "13248",
            "name": "Puhdas+ Caps Saccharomyces boulardii, 60 kaps",
            "gtin": "6430050001025"
          },
          "qty": 6,
          "arrivedQty": 6,
          "arrivals": [
            {
              "ts": "2016-01-18T08:17:55+00:00",
              "change": 6
            }
          ]
        },
        {
          "product": {
            "id": "54cf7ddb1fb35e594a8b457e",
            "merchants_id": "18504",
            "name": "Puhdas+ Caps Kollageeni & Biotiini kampanjapakkaus",
            "gtin": "6430050001766"
          },
          "qty": 6,
          "arrivedQty": 6,
          "arrivals": [
            {
              "ts": "2016-01-18T08:17:55+00:00",
              "change": 6
            }
          ]
        },
        {
          "product": {
            "id": "55e4cfc81fb35e3c118b458b",
            "merchants_id": "20277",
            "name": "Puhdas+ Hair Capsules 2-pack",
            "gtin": ""
          },
          "qty": 10,
          "arrivedQty": 10,
          "arrivals": [
            {
              "ts": "2016-01-18T08:17:55+00:00",
              "change": 10
            }
          ]
        },
        {
          "product": {
            "id": "560987bd1fb35ef66e8b4573",
            "merchants_id": "20669",
            "name": "Puhdas+ Kasviper\u00e4inen D3-vitamiini, 50 mikrog, 60 kaps",
            "gtin": "6430050002350"
          },
          "qty": 6,
          "arrivedQty": 6,
          "arrivals": [
            {
              "ts": "2016-01-18T08:17:55+00:00",
              "change": 6
            }
          ]
        },
        {
          "product": {
            "id": "566fa2d31fb35eb33e8b4570",
            "merchants_id": "21249",
            "name": "Puhdas+ Garcinia Cambogia 120+30 kaps kampanjapakkaus",
            "gtin": "6430050003098"
          },
          "qty": 6,
          "arrivedQty": 6,
          "arrivals": [
            {
              "ts": "2016-01-18T08:17:55+00:00",
              "change": 6
            }
          ]
        }
      ]
    }