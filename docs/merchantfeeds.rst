Merchant Feeds
================

.. _merchantfeeds_overview:

Overview
--------

Narrativ provides the ability for our publisher partners to download merchant feeds in a standardized format for
monetization.  This enables product data to be integrated into your CMS, allowing for more control over monetization
decisions and integration of multi-button formats.

Feed Schema
-----------

**Please note**: all fields are nullable due to incomplete and/or inapplicable data. The feeds will
only include products that are in-stock at time of file generation.

.. list-table::
   :widths: 40 20 40
   :header-rows: 1

   * - Field Name
     - Type
     - Description

   * - brand
     - String
     - Name of product brand

   * - colors
     - List<string>
     - List of colors for the product (if applicable)

   * - currency
     - String
     - Currency code of price

   * - description
     - String
     - Description of the product

   * - google_product_category
     - List<string>
     - List of Google Product categories for this product

   * - gtin
     - String
     - Global trade item number; a unique product identifier

   * - image_url
     - String
     - URL of product image

   * - item_group_id
     - String
     - ID for a group of Item IDs

   * - item_id
     - String
     - Individual Item ID

   * - manufacturer
     - String
     -

   * - model
     - String
     -

   * - mpn
     - String
     -

   * - name
     - String
     - Product name

   * - price
     - Float
     - Regular price of product

   * - sale_price
     - Float
     - Sale price of product

   * - sizes
     - List<string>
     - List of sizes for the product (if applicable)

   * - sku
     - String
     - Stock keeping unit; a unique product identifier to specific retailer

   * - store_page_url
     - String
     - Product page URL

Formatting
----------

Please make note of below formatting standards when ingesting the product feeds:
*  All headers are wrapped in double quotes
*  All string type fields are wrapped in double quotes
*  All empty fields are denoted by empty double quotes


Feed Delivery
-------------

Narrativ supports two methods of feed delivery:

**Amazon S3:**
Feeds will be delivered in a shared S3 bucket configured to have a sub-folder for each merchant.

If the publisher has their own AWS account, we will configure a shared S3 bucket that can be owned by either party.
Access will be managed using IAM roles.

If the publisher does not have their own AWS account, we will configure a shared S3 bucket accessed by secret key &
access key. Credentials will be shared in a 1pass vault for security purposes.

**SFTP:**
Feeds will be delivered to publisher’s SFTP location.

Configuring the URLs
____________________

Product URLs contained in feed must be wrapped in our click wrapper (`Clickmate`_) before publishing to the site.
This ensures the link is properly monetized with Narrativ tracking appended on click.

Publisher JS Tag
________________

It is recommended to add our `Publisher JS Tag`_ for this integration method. The JSTag allows for real-time
optimization utilizing dynamic links and dynamic button displays as detailed in the linked documentation page.
Additionally, the JS Tag unlocks higher rates by enabling impressions tracking and post-impression attribution.

Getting Started
_______________

Please contact your account manager or support@narrativ.com and we will reach out with next steps.

.. _Clickmate: https://docs.narrativ.com/en/stable/clickmate.html

.. _Publisher JS Tag: https://docs.narrativ.com/en/stable/tagpublisher.html
