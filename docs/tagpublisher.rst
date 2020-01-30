Narrativ Publisher Tag
======================

Functionality
-------------

The Narrativ publisher tag is a lightweight JavaScript tag that serves two main purposes. First, it will track user behavior
such as page views, Narrativ link impressions and clicks. Second, it will find all eligible commerce links on the page and run
the auctions, allowing the destination of the links to be updated ahead of time.

**Please Note:** The tag identifies each link in our system by the product url and page url. If your website uses dynamic values (such as user or session id) in either the product or page urls please inform your Narrativ rep to ensure correct functionality

Core Implementation
-------------------

Getting the publisher tag to run successfully is a simple process. Copy and paste the following Javascript snippet
in the HEAD section of all your site's pages.

* Make sure to replace "ACCOUNT NAME" with your Narrativ account name.
* Need to know your Narrativ account name? Log into dashboard.narrativ.com and go to `setup`_ to see the snippet
  customized with your account info, or reach out to your account manager for support as needed.
* See if it's working: There is a checker on your "setup" page where you can insert your site URL to verify if
  the Narrativ Publisher tag is correctly installed.

::

    <script type="text/javascript">
        (function(window, document, account) {
            window.skimlinks_exclude = ["shop-links.co", "shop-edits.co"];
            var b = document.createElement("script");
            b.type = "text/javascript";
            b.src = "https://static.narrativ.com/tags/" + account + ".js";
            b.async = true;
            var a = document.getElementsByTagName("script")[0];
            a.parentNode.insertBefore(b,a);
        })(window, document, "ACCOUNT NAME");
    </script>


.. _setup: https://dashboard.narrativ.com/#/publisher/account/setup

Link Rewriting
--------------

This is a feature of our JavaScript tag that must best be enabled in your account settings. Once enabled, the tag will automatically scan your article and convert any regular links to SmartLinks.

Toggle Feature
^^^^^^^^^^^^^^^

* To enable or disable link rewriting globally for your publisher account, contact us at `hello@narrativ.com`_

* Once this feature is enabled on your publisher account, you can toggle it on or off across your entire site
  by updating the Narrativ window object
  ::

    window.NRTV_EVENT_DATA.linkmate = true;

* Once this feature is enabled on your publisher account, you can toggle it on and off on a
  specific article by updating the Narrativ window object
  ::

    window.NRTV_EVENT_DATA.donotlink = true;

* To make all links on the page exclusive (meaning each link is locked to a merchant), you can use the ``exclusiveLinks`` flag on the Narrativ window object.
  ::

    window.NRTV_EVENT_DATA.exclusiveLinks = true;

* To disable link rewrite on a specific link, add ``#donotlink`` to the end of the URL::

    http://amazon.com.example/BF93JSD34/ref=ods?#donotlink

* To indicate an exclusive link, update your link in one of the following two ways:

    * Add a ``rel="noauction"`` attribute to your link::

        <a href="http://amazon.com.example/BF93JSD34/ref=ods?" rel="noauction">
            Example Product
        </a>

    * Add ``#locklink`` to the end of the URL::

        http://amazon.com.example/BF93JSD34/ref=ods?#locklink

Dynamic Display
---------------------------------------------

As discussed above, one main benefit of the Narrativ JsTag is to find commerce links on your site and run the auctions on page load. For publishers whose commerce buttons or article content mention the merchant's name and product price (“$5 at Nordstrom”), this feature will enable you to update those values dynamically.

After an auction completes, the Narrativ tag will write the output of the auction to the `data-bamx-auction` attribute. In that attribute, you can find product price, retailer name, image_url, etc. to update the article information for a link. A full list of the auction response can be found on our :doc:`Auction <auction>` page.

Updating Your Buttons
^^^^^^^^^^^^^^^^^^^^^

Below is an example JS snippet that will create a `MutationObserver`_, on all relevant links on your article, which trigger after our auction runs. Please note, the code below assumes ``monetized-links`` is a pre-existing identifier. If there is no identifier you may use ``document.querySelectorAll("a[data-bamx-auction]")`` instead.


.. code-block:: javascript
  :linenos:
  :emphasize-lines: 11

  const anchorNodes = [...document.querySelectorAll('a.monetized-links')];
  const config = {attributes: true};

  for (let i = 0; i < anchorNodes.length; i++) {
    let anchor = anchorNodes[i];

    const logFunction = (mutationList, observer) => {
      for (let j = 0; j < mutationList.length; j++) {
        const mutation = mutationList[j];

        if (mutation.type === 'attributes' && mutation.attributeName === 'data-bamx-auction') {
          console.log('Narrativ Auction has finished. Update display values now');
          console.log(anchor.getAttribute('data-bamx-auction'));
          // Your custom update function here.
        }
      }
    };

    const observer = new MutationObserver(logFunction);
    observer.observe(anchor, config);
  }

.. _MutationObserver: https://developer.mozilla.org/en-US/docs/Web/API/MutationObserver

.. _hello@narrativ.com: mailto:hello@narrativ.com
