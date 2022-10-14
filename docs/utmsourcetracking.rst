UTM Source Tracking
===================

.. _utmsourcetracking_overview:

Overview
--------

Narrativ leverages ``utm_source`` to better segment traffic from syndicated channels, such as Apple News, AMP, or
Social. This is configured as a simple url parameter appended to Narrativ links. Please note, this will not affect the
link’s monetization in any way.

Building a Narrativ Attributed Link
-----------------------------------

There are two ways to append tracking to links so that clicks and revenue connected to these links can be reported:

    1. Create a Narrativ Deeplink that directs to the product link with Narrativ tracking appended - a “Shop link”
    2. Add a click wrapper around a product link so that upon click Narrativ tracking is added - a “Clickmate link”

In both methods, we support ``utm_source`` tracking so that we can report performance by syndicated platform
(e.g, Apple News)

How to add utm_source to Narrativ Deeplinks (Shop Links)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

These are links that have been created using the Narrativ Chrome Extension, which follows the format:

::

   https://howl.me/1611792246540568252


You may also see the legacy domain shop-links. Tracking parameters can be added to either format in the same way.

::

   https://shop-links.co/1611792246540568252

To add ``utm_source`` simply append it to the end like this:

::

   https://howl.me/1611792246540568252?utm_source=applenews


Often publishers and creators use u1’s as an additional tracking parameter. Narrativ ``utm_source`` works well with
links that utilize u1’s.

A normal link with u1 would look like:

::

   https://howl.me/1611792246540568252?u1=myu1param


To add ``utm_source`` simply append it to the end like this:

::

   https://howl.me/1611792246540568252?u1=myu1param&utm_source=applenews


How to add utm_source to Click wrapper links (Clickmate Links)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

These are links that have been wrapped in Narrativ click wrapper, which follows the format:

::

   https://howl.me/link/?url=https%3A%2F%2Fdermstore.com.example%2Fshop%2Fproduct1234&publisher_slug=myacct&exclusive=1&article_name=my-story&article_url=http%3A%2F%2Fwww.myarticle.com


To add ``utm_source`` simply append it to the end like this:

::

   https://howl.me/link/?url=https%3A%2F%2Fdermstore.com.example%2Fshop%2Fproduct1234&publisher_slug=myacct&exclusive=1&article_name=my-story&article_url=http%3A%2F%2Fwww.myarticle.com&utm_source=applenews


Often publishers and creators use u1’s as an additional tracking parameter. Narrativ ``utm_source`` works well with
links that utilize u1’s.

A normal link with u1 would look like:

::

   https://howl.me/link/?url=https%3A%2F%2Fdermstore.com.example%2Fshop%2Fproduct1234&publisher_slug=myacct&exclusive=1&article_name=my-story&article_url=http%3A%2F%2Fwww.myarticle.com&u1=myu1param


To add ``utm_source`` simply append it to the end like this:

::

   https://howl.me/link/?url=https%3A%2F%2Fdermstore.com.example%2Fshop%2Fproduct1234&publisher_slug=myacct&exclusive=1&article_name=my-story&article_url=http%3A%2F%2Fwww.myarticle.com&u1=myu1param&utm_source=applenews