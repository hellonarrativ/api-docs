ClickMate
=========

.. _clickmate_overview:

Overview
--------

ClickMate provides a wrapper that you can use on any link to convert
it, on the fly, to a SmartLink. This means that the link will go through our
matching process and clicks will work through our real time
auction system to re-route to the most beneficial advertiser.



Build a ClickMate Link
----------------------

If you wanted to monetize a link to `https://dermstore.com.example/shop/product1234`
you would put that link in your HTML, or use our Chrome Extension to turn it into a SmartLink.
ClickMate gives you another option. You would wrap the link in the form:

::

   https://howl.me/link/?url=https%3A%2F%2Fdermstore.com.example%2Fshop%2Fproduct1234&publisher_slug=myacct&article_name=my-story


On click, our system will create a SmartLink in your account if
`dermstore.com.example` is one of the domains we handle for you. The link is matched and an auction takes place 
on the link in order to redirect to the appropriate destination. If there is no auction,
the link will just be redirected to the original URL.

The ideal usage for this is to set up a programmatic integration--either wrap all commerce links
on your site or all of the ones you want Narrativ to monetize. Our system will make sure that
your readers get to the appropriate destination while finding you all the best monetization opportunities.
If the wrapping happens server side by your CMS, this will even work in no-javascript or ad-blocked
environments like AMP.

The legacy url domain of shop-links.co is still supported.

::

   https://shop-links.co/link/?url=https%3A%2F%2Fdermstore.com.example%2Fshop%2Fproduct1234&publisher_slug=myacct&article_name=my-story&article_url=https%3A%2F%2Fwww.mywebpage.com


Query Params
--------------------------

.. list-table::
   :widths: 35 10 55
   :header-rows: 1

   * - URL Path Parameter
     - Type
     - Description

   * - url
     - string(2048)
     - *Required* The URL of the target link (must be URL encoded!). Without this, users will see an error page

   * - article_url
     - string(2048)
     - *Required* The canonical URL of the article your link is coming from (must be URL encoded!).

   * - article_name
     - string(100)
     - *Required* The readable name or title of the article your link is coming from (not a numeric identifier).

   * - publisher_slug
     - string(64)
     - *Required* The slug provided by your Narrativ account rep. Without this we will not know what account to monetize clicks for.

   * - exclusive
     - Integer
     - *Optional* Set this to 1 if you want to ensure that this particular link only goes to the original retailer.

   * - u1
     - string(2048)
     - *Optional* Arbitrary tracking parameter that you may apply to links for your own tracking (will be passed to our stats).


URL Encoding
------------

All parameters must be URL encoded. See `URL Encoder`_.


Example Code
------------

In Javascript:

.. code-block:: javascript

   var url = 'https://merchant.example/product1234';
   var slug = 'myacct';
   var articleName = document.title;
   var articleUrl = window.location.href;
   var clickmateUrl = 'https://howl.me/link?url=' + encodeURIComponent(url) +
      '&publisher_slug=' + slug +
      '&article_name=' + encodeURIComponent(articleName) +
      '&article_url=' + encodeURIComponent(articleUrl);


.. _contact us: mailto:hello@narrativ.com
.. _URL Encoder: https://www.urlencoder.org/
