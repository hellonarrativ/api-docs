Publisher Report
================

The Publisher Reports consist of the Clicks, Orders and Returns reports.

These reports contain detailed information about clicks, purchases, returns, attribution, and
earnings.

The reports can be published to an FTP/SFTP location or cloud storage bucket (S3/GCS) accessible by the partner.

The reports are published on configurable interval which defaults to 24 hours.

Each interval publishes data for the last 7 days.

The naming convention for each of the reports is:

* Prefix: ``/<key>/YYYY/MM/`` (defaults to slug)

* Clicks: ``narrativ_log_files_clicks_YYYYMMDD.csv``. The date in the filename indicates the clicks in the report took place on that date

* Orders: ``narrativ_log_files_orders_YYYYMMDD.csv``. The date in the filename indicates the orders/checkouts in the report took place on that date

* Returns: ``narrativ_log_files_returns_YYYYMMDD.csv``. The date in the filename indicates the returns in the report were processed on that date

The partner's report reader should be compatible with Python's ``csv.DictWriter``

Contact your account manager to get started.

Schema and File Format
----------------------

Clicks
^^^^^^
The Click File contains information about Clicks and Impressions for that day, separated by
each event occurrence. For example, each click or impression will be a new row.

This table can be used to identify:

* Information about Clicks (ex. Number of clicks a given day)

* Information about Impressions (ex. Number of impressions on a given day)

* Earnings from CPC campaigns and clients


*What to expect in the Clicks report*

Let's break it down with an example:

* Link 987 received 2 clicks on day 1 and 4 clicks on day 2

The Clicks reports would look like:

* On Day 1 two rows for link_id 987 with associated click information including earnings (if any)

* On Day 2 four rows for link_id 987 with associated click information including earnings (if any)

======================  ===========
Column                  Description
======================  ===========
click_id                Unique identifier for each click event
click_timestamp         Date Time of click in GMT
cookie_id               The cookie ID
article_url             For clicks: this is the URL which has the link that was clicked on; For impressions: the page URL that was viewed
is_clean_article_url    Bool: true if article url was passed to Howl during link creation; False if no url was passed to Howl and we read url from the page
referrer                Referrer from web browser
user_agent              User agent from web browser
is_click                Boolean flag to indicate click vs impressions Is_click will equal 1 when the record is a click, and 0 when the record is an impression
click_product_url       Product URL of the link that was clicked on
earnings                Earning for publisher. Please note this includes all payment models
click_product_category  Category of the product that was clicked on
click_is_brand_page     Boolean: true is the link that was clicked on linked to a brand page
click_u1_param          U1 parameter of the click
click_product_brand     Brand of the product that was clicked on
click_product_price     Price of the product that was clicked on
click_product_name      Name of the product that was clicked on
article_name            For clicks: this is the name of the article which has the link that was clicked on; For impressions: the Name of article that was viewed
link_id                 Unique identifier for each Howl link, sometimes referred to as auction ID.
network                 This identifies the payment model associated with the record - the values can be CPC, CPA, CPM, EPP
merchant                Merchant name of link
publication             Publisher name
link_type               Indicates if the link was created through a manual or programmatic process
channel                 Digital channel of the event i.e. desktop
device_type             Device event occurred on
country_code            ISO 3166-2 Country code
link_source             Detailed information on how link was created.
======================  ===========

Orders
^^^^^^
The Orders File contains information about orders (checkouts) for that day. Each product
purchased has its own row in this file, thus there may be multiple records associated with one checkout in the file.

This table can be used to identify -

* Information about Orders (ex. Number of orders a given day)

* Earnings from EPP campaigns and clients


*What to expect in the Orders report*

Let's break it down with an example:

* Checkout 123 is attributed to a publication, and included :

- product A1 with a quantity of 4, earnings 40, revenue 400, and

- product B1 with a quantity of 1, earning 15 and revenue 150

and

* Checkout 321 is attributed to a publication, and included :

- product A1 with a quantity of 1, earnings 10, revenue 100, and

The Orders reports would look like:

* One row for checkout ID 123 and product ID A1 with number_products_purchased 4, earnings 40, revenue 400.

* One row for checkout ID 123 and product ID B1 with number_products_purchased 1, earnings 15, revenue 150.

* One row for the checkout ID 321  and product ID A1 with number_products_purchased 1, earnings 10, revenue 100.


===========================  ===========
Column                       Description
===========================  ===========
order_product_id             Unique identifier for each record in the orders file, which is a combination of the order_id and the
product_id                   Unique identifier of the order product
order_id                     Unique identifier of the order generated by Howl
checkout_timestamp           Date time of the checkout in GMT
cookie_id                    The cookie ID
article_url                  URL of the page that has the link clicked attributed to this checkout
link_id                      Unique identifier for each Howl link, sometimes referred to as auction ID. This refers to the link attributed to this checkout. Please note this can be used to join the orders file.
referrer                     Referrer from web browser
user_agent                   User agent from web browser
network_type                 Type of network from where the checkout data is obtained - ‘Howl - No returns’ or ‘Rakuten - Returns Apply’
click_product_url            Product URL of the link that was clicked on, attributed to this checkout
click_product_category       Category of the product that was clicked on
click_is_brand_page          Boolean: true is the attributed link that was clicked on linked to a brand page
days_since_attributed_click  Number of days since the click event attributed to this checkout
purchased_product_id         Product ID of the product purchased. This is the Merchant’s product ID
purchased_product_name       Name of the product purchased
purchased_product_brand      Brand of the product purchased
purchased_product_price      Price of the product purchased
click_u1_param               U1 parameter of the click attributed to this checkout
checkout_id                  Identifier of the checkout from the Merchant
earnings                     This contains EPP and Linkshare earnings. Please note for orders with multiple products, the earnings column for each row is the earnings for the total order, not that individual product within the order.
revenue                      Revenue driven by the order
number_products_purchased    Quantity of products purchased
click_product_brand          Brand of the product that was clicked on attributed to this checkout
click_product_price          Price of the product that was clicked on attributed to this checkout
click_product_name           Name of the product that was clicked on attributed to this checkout
article_name                 name of the article which has the link that was clicked on attributed to this checkout
network                      This identifies the payment model associated with the record - the values can be CPC, CPA, CPM, EPP. This can be used to pivot the earnings and identify how much the EPP earnings are, and how much the CPA earnings are
merchant                     Merchant name
publication                  Publisher Name
channel                      Digital channel of the event i.e. desktop
device_type                  Device event occurred on
country_code                 ISO 3166-2 Country code
click_id                     Unique identifier for each click event attributed to this checkout
click_timestamp              Date time in GMT of the click attributed to this checkout
===========================  ===========


Returns
^^^^^^^
The Returns File contains information about returns processed on that day from orders (checkouts) attributed
to the publisher at specific merchant partners in the past. This report captures the
returns processed on a particular day, regardless of when the original checkout occurred. The returns can be partial
or full, and can be broken over multiple days.

The report contains unique rows for each product returned in the order as they are processed, even if multiple products from the same checkout are returned and processed separately.
Each row will include information about the number of items returned(quantity), the amount of earnings borne from the items returned, and the revenue associated with the returned items.
Since the data in these reports pertains to returns, the earnings, revenue and quantity values are negative.

To gain a comprehensive view of returns, we recommend aggregating the values for each unique combination of
checkout_id, merchant and product_id (denoted by the order_product_id column) across all return files.

Since this report is designed to be used to complement the data in the orders reports, the column 'order_product_id'
can be used to join to the orders report, or one can choose to join to the orders report by using a combination/compound key of the merchant + checkout_id + product_id.

This table can be used to identify -

* Quantity of products returned

* Earnings and revenue from the returned products


*What to expect in the Returns Report*

Let's break it down with an example:

Checkout 123 is attributed to a publication, and originally included :

* product A1 with a quantity of 4, earnings 40, revenue 400, and

* product B1 with a quantity of 1, earning 15 and revenue 150

The customer returns:

* 2 quantity of product A1 on day 1, and

* 1 quantity of product A1 and 1 quantity of product B1 on day 2.

The Returns reports would look like:

* One row in the report for day 1 for checkout ID 123 and product ID A1 with quantity -2, earnings -20, revenue -200.

* One row in the report for day 2 for the checkout ID 123  and product ID A1 with quantity -1, earnings -10, revenue -100 and one row for the checkout ID 123 and product ID B1 with quantity -1, earnings -15, revenue -150.


When combining the returns information with the orders information, make sure to group the returns information
by order_product_id or checkout_id-merchant-product_id first. Then, join it with the orders data,
to avoid missing data regarding partial returns that may be processed over multiple days.

===========================  ===========
Column                       Description
===========================  ===========
order_product_id             Foreign key to join to Orders Report, unique to checkout_id,merchant and purchased_product_id combination
checkout_timestamp           Timestamp of checkout
purchased_product_id         Unique identifier for product returned
checkout_id                  Identifier of the checkout returned from the Merchant
merchant                     Merchant name
publication                  Publisher Name
return_revenue               Revenue associated with product items returned
return_earnings              Earnings associated with product items returned
return_quantity              Quantity of product items returned
return_datetime              Datetime of return's/partial return's processing
return_id                    Unique identifier for the return/partial returns for this checkout on this day
===========================  ===========

Example Data Queries
--------------------

Calculate earnings by payment model
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
To calculate the CPC earnings, use the Clicks file, and sum up the earnings column. This file
contains only the CPC earnings as only CPC pays on click.

To calculate CPA earnings, use the Orders file, and apply a filter for Network = CPA. After that
dedupe to only consider unique order_id and sum up the filtered earnings column.  This is
because for orders with multiple products, the earnings column for each row is the earnings for
the total order, not that individual product within the order. (Note these earnings are subject to
return and will not be finalized for 90 days)

To calculate EPP earnings, use the Orders file, and apply a filter for Network = EPP. After that
dedupe to only consider unique order_id and sum up the filtered earnings column.  This is
because for orders with multiple products, the earnings column for each row is the earnings for
the total order, not that individual product within the order.
Calculate total earnings

To calculate the total earnings, you would need to sum up the earnings columns of both the
Clicks and Orders files. This would allow you to get the CPC earnings (from the earnings
column in clicks file) * 0.01 and EPP + CPA earnings (from the earnings column in orders file)
Calculate clicks and impressions
To calculate clicks based on merchants, you would use the clicks file. The field is_click can be
used to identify whether the record corresponds to a click (is_click=1) or an impression (is_click
= 0)

SELECT merchant, COUNT(*) FROM clicks_file WHERE is_click = 1 group by 1

To get count of click/impressions/earnings based on posts or articles, the data can be split
based `article_url`, however we recommend using a clean version of the URL (probably without
query and fragment portions).

Similarly, clicked_product_name can be used to pivot data on a product basis.

Calculate earnings per product
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
The earnings per product in an order can be calculated using the formula below -
earnings_per_product = total_order_earnings * (purchased_product_price *
number_products_purchased / total_order_revenue)
These can then be summed up based on the product ID, if needed.
Since certain merchants honor returns, including the earnings returned due to returns is pertinent.
