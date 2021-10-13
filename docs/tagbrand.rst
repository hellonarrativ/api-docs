Narrativ Brand Tag
==================

What is it?
-----------

The Narrativ Brand Tag is a lightweight javascript tag that enables partners to maximize their performance
and unlock valuable article and product level insights in a customized dashboard.
Only clients with Narrativ’s Brand Tag can optimize their campaigns by ROAS and see more comprehensive
metrics like revenue and RPC.

**Please note:** data collection by the brand tag does not contain personally identifiable information (PII)
and is in compliance with GDPR and CCPA.


How it Works
------------

The Narrativ Brand Tag is responsible for handling two types of events: page impressions and checkouts.

Page Impressions
^^^^^^^^^^^^^^^^

Page impression events enable Narrativ to ensure attribution for our partners.
These events should be fired on every page that doesn’t contain PII.

Checkouts
^^^^^^^^^

Checkout events allow Narrativ to accurately capture revenue and conversions in real time.
The data gathered by checkout events also powers an experience publishers rely on to track
top sellers and give better product recommendations on their articles.

Checkout events should be fired on your site’s **Order Confirmation Page**, or the page that loads
immediately **after** they’ve *successfully* purchased their items.

**Please note:** Similar to Page Impression, Checkouts are in compliance with GDPR and CCPA
and does not capture personally identifiable information (PII). Additionally, since the tag
runs asynchronously in the background, there is no impact to the page load time.


Implementation
--------------

Page Impression Events
^^^^^^^^^^^^^^^^^^^^^^
Getting the Narrativ Brand Tag to fire page impression events is a simple process.
Copy and paste the following Javascript snippet in the HEAD section of all your
site’s pages *that don’t contain PII*.

* Make sure to replace ``ACCOUNT NAME`` with your Narrativ account name.

* Need your Narrativ account name? Reach out to your growth manager or solutions@narrativ.com for assistance.

::

  <script type="text/javascript">
      (function(account) {
          try {
              var b = document.createElement("script");
              b.type = "text/javascript";
              b.src = "https://static.narrativ.com/tags/" + account + ".js";
              b.async = true;
              var a = document.getElementsByTagName("script")[0];
              a.parentNode.insertBefore(b, a);
          } catch (e) {}
      }("ACCOUNT NAME"));
  </script>

Checkout Events
^^^^^^^^^^^^^^^

In order to successfully fire checkout events with the Narrativ Brand Tag, the following code snippet
must be populated with information about the checkout, along with a few details about each of
the products purchased. This snippet should be placed on your site’s **Order Confirmation Page**,
or the page displayed to customers immediately after they’ve *successfully* purchased their items.


Make the Checkout Event Code Work for You
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Follow the sample code below, making these changes:

.. list-table::
   :widths: 8 60 14 18
   :header-rows: 1

   * - Statement
     - Requirement
     - Data Type
     - Notes

   * - ``var purchased = <dataLayerProducts>;``
     - Replace ``<dataLayerProducts>`` with the list of purchased products in your data layer.
       Each item in this array represents attributes of a single purchased product (explained in the following items).
     - Object
     -

   * - ``product_id: purchased[i].<ItemID>,``
     - Replace ``<ItemID>`` with the variable name your data layer uses to define item ID, or the unique identifier
       for the purchased product. This can likely be found in the ``dataLayerProducts`` array described above.
     - String
     -

   * - ``product_name: purchased[i].<ItemName>,``
     - Replace ``<ItemName>`` with the variable name your data layer uses to define item name, or the name
       for the purchased product. This can likely be found in the ``dataLayerProducts`` array described above.
     - String
     -

   * - ``product_price: purchased[i].<ItemPrice>,``
     - Replace ``<ItemPrice>`` with the variable name your data layer uses to define item price, or the *per-unit price*
       of the purchased product. This can likely be found in the ``dataLayerProducts`` array described above.
     - String
     - Both cart level and product level coupon codes should be captured in this variable (e.g. if a coupon code
       variable in the data layer is not null, apply X% discount to product_price)

   * - ``product_quantity: purchased[i].<ItemQuantity>,``
     - Replace ``<ItemQuantity>`` with the variable name your data layer uses to define item quantity, or the quantity
       of the purchased product. This can likely be found in the ``dataLayerProducts`` array described above.
     - Integer
     -

   * - ``product_brand: purchased[i].<ItemBrand>,``
     - Replace ``<ItemBrand>`` with the variable name your data layer uses to define item brand, or the brand
       of the purchased product. This can likely be found in the ``dataLayerProducts`` array described above.
     - String
     - If Item Brand is not available, replace ``<ItemBrand>`` with ``null``

   * - ``product_size: purchased[i].<ItemSize>,``
     - Replace ``<ItemSize>`` with the variable name your data layer uses to define item size, or the size
       of the purchased product. This can likely be found in the ``dataLayerProducts`` array described above.
     - String
     - If Item Size is not available, replace ``<ItemSize>`` with ``null``

   * - ``product_color: purchased[i].<ItemColor>,``
     - Replace ``<ItemColor>`` with the variable name your data layer uses to define item color, or the color
       of the purchased product. This can likely be found in the ``dataLayerProducts`` array described above.
     - String
     - If Item Color is not available, replace ``<ItemColor>`` with ``null``

   * - ``orderTotal += (purchased[i].<ItemPrice> *``
       ``purchased[i].<ItemQuantity>);``
     - Replace ``<ItemPrice>`` and ``<ItemQuantity>`` with the same respective values used above.
     - String
     -

   * - ``is_new_customer: <isNewCustomer>,``
     - Replace ``<isNewCustomer>`` with a boolean (true/false) indicating if Order is First Order
     - Boolean
     - If field is not available, replace ``<isNewCustomer>`` with ``null``.

   * - ``order_id: <OrderID>,``
     - Replace ``<OrderID>`` with the order ID, a unique identifier for the order.
     - String
     -

   * - ``currency: <CurrencyCode>,``
     - Replace ``<CurrencyCode>`` with the three digit currency code that order was placed in (ex: ‘USD’).
       Uses `ISO 4217`_
     - String
     -

**Note:** Remember to also replace ``ACCOUNT NAME`` with your Narrativ account name.

::

    <script type="text/javascript">
        var purchased = <dataLayerProducts>;
        var productsPurchased = [];
        var orderTotal = 0;
        for (var i = 0; i < purchased.length; i++) {
          productsPurchased.push({
            product_id: purchased[i].<ItemID>,
            product_name: purchased[i].<ItemName>,
            product_brand: purchased[i].<ItemBrand>,
            product_size: purchased[i].<ItemSize>,
            product_color: purchased[i].<ItemColor>,
            product_price: purchased[i].<ItemPrice>,
            product_quantity: purchased[i].<ItemQuantity>,
          });
          orderTotal += (purchased[i].<ItemPrice> * purchased[i].<ItemQuantity>);
        }

        window.BAMX_EVENT_DATA = {
            page_type: 'checkout',
            is_new_customer: <isNewCustomer>,
            products_purchased: productsPurchased,
            order_id: <OrderID>,
            order_value: orderTotal,
            currency: <CurrencyCode>,
        };

        (function(account) {
            try {
              var b = document.createElement("script");
              b.type = "text/javascript";
              b.src = "https://static.narrativ.com/tags/" + account + ".js";
              b.async = true;
              var a = document.getElementsByTagName("script")[0];
              a.parentNode.insertBefore(b, a);
            } catch (e) {}
        }("ACCOUNT NAME"));
    </script>

Shopify Checkout Code
---------------------

Please use the script tag below in place of the previous checkout code if you prefer to implement through an
existing Shopify integration:

::

    <script type="text/javascript">
        if(Shopify.Checkout.step == ‘thank_you’){
            var productsPurchased = [
                {% for line_item in checkout.line_items %}
                {% if line_item.price > 0 %}
                {
                    “product_id” : “{{ line_item.product_id }}”,
                    “product_name” : “{{ line_item.product_title | capitalize }} {% if
                    line_item.product.metafields.c_f.tagline %}
                    {{ line_item.product_metafields.c_f.tagline }}{% endif %}”,
	                "product_brand":"{{ line_item.product.vendor }}",
	                "product_size":"{{ line_item.variant.option1 }}",
	                "product_price" : "{{ line_item.price | money_without_currency }}",
	                "product_quantity" : "{{ line_item.quantity }}", },
                {% endif %}
            {% endfor %} ];
        };

        window.BAMX_EVENT_DATA = {
            "page_type": “checkout”,
            "order_id": Shopify.checkout.order_id.toString() || "{{order_number}}",
            "products_purchased": productsPurchased,
            "order_value": Shopify.checkout.subtotal_price || "{{subtotal_price | money_without_currency }}",
            "currency": Shopify.checkout.currency || "{{currency.iso_code}}",
        };

        (function(account) {
            try {
              var b = document.createElement("script");
              b.type = "text/javascript";
              b.src = "https://static.narrativ.com/tags/" + account + ".js";
              b.async = true;
              var a = document.getElementsByTagName("script")[0];
              a.parentNode.insertBefore(b, a);
            } catch (e) {}
        }("ACCOUNT NAME"));
    </script>

**Note:** Remember to also replace ``ACCOUNT NAME`` with your Narrativ account name.

Google Tag Manager Implementation
---------------------------------

Implementing the Narrativ Brand Tag with Google Tag Manager is a simple process. Follow the instructions below
to implement the tag using a "Custom HTML" tag in GTM.

Page Impression Events
^^^^^^^^^^^^^^^^^^^^^^

Start by navigating to your Google Tag Manager Dashboard.

- Select the "Tags" menu item from the menu on the left-hand side of the page.
- Once on the "Tags" page, select the "New" button to create a new tag.
- Select the "Tag Configuration" box to begin making a new tag.

.. image:: _static/pixel_implementation_screenshots/1_tap_configuration.png

- Select the "Custom HTML" option to open an empty text field.

.. image:: _static/pixel_implementation_screenshots/2_choose_custom_html.png

- Copy and paste the code outlined in the above section entitled “Page Impression Events: Implementation”.
  Make sure you replace ``ACCOUNT NAME`` with your Narrativ account name.

.. image:: _static/pixel_implementation_screenshots/3_enter_tag_html.png

- Select "All Pages" as the correct trigger for these events.

.. image:: _static/pixel_implementation_screenshots/4_select_trigger.png

- Name the tag "Narrativ Page Impression Events" and double check that the trigger is set to "All Pages".

.. image:: _static/pixel_implementation_screenshots/5_final_product.png

Checkout Events
^^^^^^^^^^^^^^^

- For checkout events, create a new tag and open the empty text field again.

.. image:: _static/pixel_implementation_screenshots/checkout_1_open_editor.png

- Follow the instructions outlined in the “Checkout Events: Implementation” Section above to successfully fire checkout events.

**Note:** ``var purchased`` should be set to the data layer variable corresponding to products purchased at checkout.
This can be defined independent of GTM variables (see previous screenshot), or it can be found in the
Variables section of your Tag Manager dashboard
GTM variables referenced in the checkout tag should be wrapped in doubly curly brackets.

Here is an example of the fully implemented checkout code:

.. image:: _static/pixel_implementation_screenshots/checkout_2_confirm_code_product_info.png

- Select the box under "Triggering" to add a trigger for this tag.

.. image:: _static/pixel_implementation_screenshots/checkout_3_add_trigger.png

- If you don’t already have a trigger for checkout pages, then it’s easy to create one!

.. image:: _static/pixel_implementation_screenshots/checkout_4_add_confirmation_page_trigger.png

- The below example has a series of triggers based off of common URL types for checkout or confirmation pages. (E.g. narrativ.com/checkout/ will trigger the "Checkout Page" option). Replace "checkout" with whatever word your site uses on checkout pages. Remember, you only need one trigger!

.. image:: _static/pixel_implementation_screenshots/checkout_4.1_add_confirmation_rules.png

- Double check the tag name, make sure you’ve updated the code with the information on your checkout page, and make sure you’ve selected the correct trigger.

.. image:: _static/pixel_implementation_screenshots/checkout_5_double_check.png

Publishing Tags
^^^^^^^^^^^^^^^

- Make sure that the tag(s) are showing up in the "Tag" tab.

.. image:: _static/pixel_implementation_screenshots/submit_1_tag_confirmation.png

- Preview the changes made and fix any errors that pop up in the window.

.. image:: _static/pixel_implementation_screenshots/submit_2_review.png

- Click the "Submit" button to save your changes (this step is not final)

.. image:: _static/pixel_implementation_screenshots/submit_3_submit_changes.png

- Double check that everything you modified is in this submission. Name the submission something like "Adding Narrativ Brand Tag" so that it’s easy to find if you need to go back and debug any issues in the future.

.. image:: _static/pixel_implementation_screenshots/submit_4_title_the_changes.png

If you have any issues during this process then reach out to your Narrativ growth manager or email us at solutions@narrativ.com.

Testing the Brand Tag
---------------------

Page Impressions
^^^^^^^^^^^^^^^^

To test the page impression code, filter “bam” in Developer Tools and check for these three events on refresh:

.. image:: _static/pixel_implementation_screenshots/test_page_impression.png

Checkouts
^^^^^^^^^

Place a test order to QA the checkout tag. Similar to the page impression test, be sure to have “bam” filtered in
Developer Tools *before* you place the order. On the confirmation page, you should see an additional checkout
event firing:

.. image:: _static/pixel_implementation_screenshots/test_checkouts.png

When you navigate into the “Request Payload” within the checkout event, you should see information about the order
and products purchased:

.. image:: _static/pixel_implementation_screenshots/test_checkouts_payload.png

**Please note:** We recommend placing an additional test order with a coupon code to ensure order value and product
price variables accurately capture any discounts.

If you have any issues during the implementation or testing process, please reach out to your Narrativ growth manager
or email us at solutions@narrativ.com.

.. _Google category: https://support.google.com/merchants/answer/6324436?hl=en
.. _ISO 4217: https://www.iso.org/iso-4217-currency-codes.html
