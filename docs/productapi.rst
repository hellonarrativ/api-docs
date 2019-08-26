Multi-Match Exclusive API
============

Overview
--------

This API takes a product identifier and matches the product to all instances of this product in our merchant network. The output will include matched product information, merchant information, and Narrativ links which are exclusively matched to each merchant. Please note that by using this API, Narrativ's bidding algorithm will be bypassed. This endpoint is typically used for multiple links or multiple buttons per product.


Request
^^^^^^^

::

   GET /api/v1/product_match/clickmate/exclusive_links/


.. list-table::
   :widths: 10 10 80
   :header-rows: 1

   * - Query Param
     - Type
     - Description

   * - publisher_slug
     - string(64)
     - (*Required*) The account identifier provided by your Narrativ account rep.

   * - gtin
     - string(14)
     - **Product descriptor** (*Optional - see below*): the GTIN of the product - used as an identifier to find matches in Narrativ merchant network. Please note, this is sometimes referred to as the UPC of the product.

   * - sku
     - string(255)
     - **Product descriptor** (*Optional - see below*): the SKU of the product - used as an identifier to find matches in Narrativ merchant network
   
   * - article_url
     - string(2048)
     - **Article info** (*Required*): The URL of the article or page the link is published on (must be URL encoded!)

   * - article_name
     - string(100)
     - **Article info** (*Required*): The name or title of the article or page the link is published on


Identifier Parameters
^^^^^^^^^^^^^^^^^^^
**Please Note:** at least one identifier (``gtin``, ``sku``) must be present for this endpoint.


Response
^^^^^^^^

The response data consists of the list ``data``, with each entry
having the following structure:

.. list-table::
   :widths: 10 10 60
   :header-rows: 1

   * - Field Name
     - Type
     - Description

   * - best_effort_cpc
     - float
     - Point in time prediction of the CPC for the merchant publisher pairing in USD

   * - clickmate_link
     - string
     - The monetized Narrativ link which is exclusively matched to each merchant


   * - product_information
     - json
     - Product details
        - brand
            - string
            - The retrieved product's brand

        - gtin
            - string
            - The retrieved product's GTIN

        - image_url
            - string
            - The retrieved product's image URL

        - in_stock
            - boolean
            - If the product is currently in stock or not

        - price
            - string
            - The price of the retrieved product in USD

        - product_name
            - string
            - The retrieved product's name

        - merchant_name
            - string
            - The name of the merchant selling the retrieved product


URL Encoding
------------

All parameters must be URL encoded. See `URL Encoder`_.


Example Requests
----------------

::

    GET /api/v1/product_match/clickmate/exclusive_links/?publisher_slug=myacct&gtin=77777777777&article_name=Top+5+Products&article_url=https%3A%2F%2Fwww.narrativ.com%2Farticles%2Ftop5products

    GET /api/v1/product_match/clickmate/exclusive_links/?publisher_slug=myacct&sku=00000000&&gtin=88888888888888&article_name=Top+5+Products&article_url=https%3A%2F%2Fwww.narrativ.com%2Farticles%2Ftop5products

    GET /api/v1/product_match/clickmate/exclusive_links/?publisher_slug=myacct&sku=00000000&article_name=Top+5+Products&article_url=https%3A%2F%2Fwww.narrativ.com%2Farticles%2Ftop5products


Example Response
----------------

::

    {
        "data": [
            {
                "product_information": {
                    "price": "15.99",
                    "product_name": "Example Product",
                    "in_stock": true,
                    "gtin": "55555555555555",
                    "image_url": "https://merchant.example/path/to/image_url",
                    "brand": "Example Brand",
                    "merchant_name": "Example Retailer"
                },
                "clickmate_link": "https://shop-links.co/link/?url=https%3A%2F%2Fwww.merchant.example%2Fproduct%2F123%0Aexclusive=1&publisher_slug=myacct",
                "best_effort_cpc": 0.50,
            }
        ]
    }


.. _contact us: mailto:hello@narrativ.com
.. _URL Encoder: https://www.urlencoder.org/
