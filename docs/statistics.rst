Statistics
==========

Fetches statistics for a given publisher over a specified date range.


Get statistics grouped by articles and merchant per day
-------------------------------------------------------

Request
^^^^^^^

::

   GET /api/v1/publishers/<pub_id>/stats_by_article_merchant_daily/

.. list-table::
   :widths: 35 10 55
   :header-rows: 1

   * - URL Path Parameter
     - Type
     - Description

   * - pub_id
     - integer
     - Your publisher ID.

.. list-table::
   :widths: 10 10 80
   :header-rows: 1

   * - Query Param
     - Type
     - Description

   * - date_from
     - string
     - **Required**: The starting date to collect statistics, as an ISO 8601 compliant string. Ex:
       '2018-01-01', '2015-03-11'

   * - date_to
     - string
     - **Required**: The end date to collect statistics, as an ISO 8601 compliant string. Must be greater than ``date_from``.

   * - limit
     - integer
     - Optional: The upper limit on the number of rows returned by this query. The current default and maximum is ``10000``.

   * - order_by
     - string
     - Optional: Order the returned rows by the specified column. Current default is ``clicks``. Acceptable values are:

        - ``article_id``
        - ``advertiser_attributed_sales``
        - ``pub_earnings``
        - ``merch_id``
        - ``impressions``
        - ``advertiser_attributed_revenue``
        - ``event_date``
        - ``clicks``

   * - out_of_network
     - boolean
     - Optional: If set to true, return data for other networks in addition to the Narrativ network. Default value is false.

Response
^^^^^^^^

The response data consists of the list ``stats``, with each entry
having the following structure:

.. list-table::
   :widths: 30 10 60
   :header-rows: 1

   * - Field Name
     - Type
     - Description

   * - advertiser_name
     - string
     - The full name of the advertiser. Will default to ``null`` if the advertiser is outside the Narrativ merchant network.

   * - article_name
     - string
     - The full name of the article.

   * - advertiser_attributed_sales
     - integer
     - The total number of sales attributed to the advertiser.

   * - pub_earnings
     - string
     - The amount of money earned by the publisher in USD. (Ex: '12345.67')

   * - article_id
     - integer
     - The ID of the particular article.

   * - article_url
     - string
     - The URL of the particular article.

   * - merch_id
     - integer
     - The ID of the merchant.

   * - impressions
     - integer
     - The total number of page impressions.

   * - advertiser_attributed_revenue
     - string
     - The total amount of revenue attributed to the advertiser in USD. (Ex: '100.00')

   * - pub_id
     - integer
     - The ID of the publisher.

   * - event_date
     - string
     - The date associated with this entry.

   * - clicks
     - integer
     - The total number of clicks.


Examples
^^^^^^^^


Get statistics grouped by articles and merchants per day between 2018-03-11 and 2018-03-12::


    GET /api/v1/publishers/1/stats_by_article_merchant_daily/

    {
        "date": {
            "date_from": "2018-03-11 00:00:00",
            "date_to": "2018-03-12 00:00:00"
        },
        "pub_id": 1,
        "stats": [
            {
                "advertiser_name": "Merchant Name A",
                "article_name": "Some article name",
                "advertiser_attributed_sales": 60,
                "pub_earnings": "10.25",
                "article_id": 1,
                "article_url": "https://www.merchant-name-a.com/article?=1",
                "merch_id": 10,
                "impressions": 200,
                "advertiser_attributed_revenue": "150.00",
                "pub_id": 1000,
                "event_date": "2018-03-11",
                "clicks": 500
            },
            {
                "advertiser_name": "Merchant Name A",
                "article_name": "Another article name",
                "advertiser_attributed_sales": 600,
                "pub_earnings": "99.75",
                "article_id": 1,
                "article_url": "https://www.merchant-name-a.com/article?=2",
                "merch_id": 10,
                "impressions": 700,
                "advertiser_attributed_revenue": "350.00",
                "pub_id": 1000,
                "event_date": "2018-03-12",
                "clicks": 200
            }
        ]
    }
