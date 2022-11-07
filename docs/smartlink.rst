Dynamic API
===========

Create a new Narrativ Dynamic Link (SmartLink)
----------------------------------------------

Request
^^^^^^^

::

    POST /api/v1/smart_links/

.. NOTE: Adding required for article name and url

.. list-table::
   :widths: 30 10 60
   :header-rows: 1

   * - Field Name
     - Type
     - Description

   * - url
     - string
     - The URL of the product page for this SmartLink.

   * - article_name
     - string
     - (*Required*) The name of the article that this SmartLink will be featured on.

   * - article_url
     - string
     - (*Required*) The URL of the article that this SmartLink will be featured on.

   * - article_publication_date
     - timestamp
     - The date/time when the article is expected to be published.

   * - exclusive_match_requested
     - boolean
     - (*Optional*) If true, lock this SmartLink to the original merchant. Default false.

   * - pub_id
     - integer
     - Publisher ID. Required if you have multiple publisher accounts.

Response
^^^^^^^^

.. list-table::
   :widths: 30 10 60
   :header-rows: 1

   * - Field Name
     - Type
     - Description

   * - auction_id
     - string
     - A long unique identifier for the SmartLink that was created.

   * - smart_link_id
     - integer
     - A unique identifier for the SmartLink that was created.

   * - smart_link_url
     - string
     - The URL of the SmartLink, which should be substituted for the original link in your article. This is the monetized Narrativ link.

Example
^^^^^^^

::

    curl -i -H 'Authorization: NRTV-API-KEY Sy8xLzE2MTE3MDIxNzY3NDM0OTc0MDcv' \
        -H 'Content-Type: application/json' \
        -d '{"url": "https://www.google.com/",
             "article_name": "Top Ten Search Engines",
             "article_url": "http://www.my-blog.example",
             "article_publication_date": "2017-08-02T17:00:00Z",
             "exclusive_match_requested": true,
             "pub_id": 1}' \
        https://api.narrativ.com/api/v1/smart_links/

::

    HTTP/1.1 201 CREATED
    Content-Type: application/json

    {
      "info": {
        "error": false,
        "status": 201,
      },
      "data": [
        {
          "smart_link_id": 2554,
          "auction_id": "1611792246540568252",
          "uid_created": 2,
          "datetime_created": "2017-07-26T19:48:25Z",
          "pub_id": 1,
          "url": "https://www.google.com/",
          "exclusive_match_requested": true,
          "smart_link_url": "https://shop-links.co/1611792246540568252",
          "howl_link_url": "https://howl.me/chPWcXAXAOa",
          "encoded_auction_id": "chPWcXAXAOa"
          "article": {
            "article_id": 2536,
            "uid": 2,
            "pub_id": 1,
            "url": "http://www.my-blog.example",
            "publication_date": "2017-08-02T17:00:00Z",
            "datetime_created": "2017-07-26T19:48:25Z",
            "datetime_updated": "2017-07-26T19:48:25Z",
            "name": "Top Ten Search Engines"
          }
        }
      ]
    }
