Narrativ Advertiser Tag
=======================

Functionality
-------------

The Narrativ advertiser tag allows Narrativ to track user behavior on an advertiser's site. Our auction system 
optimizes advertiser acquisition and ROI by analyzing data on page views and purchase behavior. Any other Personal 
Identifying Information (PII) that is captured, such as names, etc. will be hashed and never stored in plain text. The 
tag runs asynchronously in the background so there is no impact to page load times.

Implementation
--------------

We track two types of events for our partners - check outs and page views:

* Place the check out tag on the page that loads after your customer has finished shopping and paid
  for their purchase (your site's equivalent of a "Thank you for your order" page).

* Place the page view tag on every other page that loads during your user's journey, so that we can
  empower you with data on what products they are looking at before they check out.
  Important! Replace "ACCOUNT NAME" with your Narrativ account name in all snippets. Reach out to
  hello@narrativ.com for help with your Narrativ account name as needed.

Adding Information About Your Checkout Page
-------------------------------------------


For checkout events, you have to fill in some information about the checkout before loading our Javascript. This is
done by inserting the relevant data into a variable called window.BAMX_EVENT_DATA. If a field is optional, you can
just leave it out if you choose not to include the data.

*window.BAMX_EVENT_DATA*

.. list-table::
   :widths: 30 10 60
   :header-rows: 1

   * - Field Name
     - Type
     - Description

   * - page_type
     - string
     - Required. Must be "checkout" to tell the tag to fire a checkout event.

   * - user_id
     - string
     - Optional. The ID the user has in your system, if available.

   * - order_id
     - string
     - Required. The unique order_id for the checkout that just completed.

   * - order_value
     - float
     - Required. The total purchase price of the order.

   * - currency
     - string
     - Required. The three digit code for the currency that order_value is in (ex: 'USD'). Uses `ISO 4217`_

   * - products_purchased
     - array
     - Required. An array of Product objects representing the purchased items, as defined below.

*Product*

.. list-table::
   :widths: 30 10 60
   :header-rows: 1

   * - Field Name
     - Type
     - Description

   * - product_id
     - string
     - Required. The unique identifier for this product.

   * - product_name
     - string
     - Required. The name of the product.

   * - product_category
     - string
     - Optional. The `Google category`_ of the product.

   * - product_brand
     - string
     - Optional. The brand of the product.

   * - product_price
     - float
     - Required. The price of the product.

   * - product_quantity
     - integer
     - Required. The number of this product purchased in this order.

Full Example (remember, replace "ACCOUNT NAME" with your Narrativ account name)

What you see below is just an example. You cannot copy and paste it as is. Insert the check out
information from your own page into our data layer using Javascript before loading the Narrativ tag.

::

    <!-- begin NARRATIV jstag -->
    <script type="text/javascript">
        var purchased = window.dataLayer[3]['OrderItems'];
        var productsPurchased = [];
        var orderTotal = 0;
        for (var i = 0; i < purchased.length; i++) {
          productsPurchased.push({
            product_id: purchased[i].ItemID,
            product_name: purchased[i].ItemName,
            product_category: purchased[i].ItemCategory,
            product_brand: purchased[i].ItemBrand,
            product_price: purchased[i].ItemPrice,
            product_quantity: purchased[i].ItemQuantity
          });
          orderTotal += product_price;
        }
        window.BAMX_EVENT_DATA = {
            page_type: 'checkout',
            user_id: {{UserID}},
            is_new_visitor: {{RegisteredCustomer}},
            products_purchased: productsPurchased,
            order_id: {{OrderID}},
            order_value: orderTotal,
            currency: {{CurrencyCode}}
        };
        (function (account) {
            try {
              var b = document.createElement("script");
              b.type = "text/javascript";
              b.src = "//static.narrativ.com/tags/" + account + ".js";
              b.async = true;
              var a = document.getElementsByTagName("script")[0];
              a.parentNode.insertBefore(b, a);
            } catch (e) {}
        }("ACCOUNT NAME"));
    </script>
    <!-- end NARRATIV jstag -->


Adding Information for the Page View Tag
----------------------------------------

The page view tag goes on every page except for pages with PII. Remember to change "ACCOUNT NAME" to your Narrativ 
account name.

What you see below is another example. You cannot copy and paste it as is. Insert the page view
information into our data layer using Javascript before loading the Narrativ tag.

::

  <!-- begin NARRATIV jstag -->
  <script type="text/javascript">
      (function (account) {
          try {
              var b = document.createElement("script");
              b.type = "text/javascript";
              b.src = "//static.narrativ.com/tags/" + account + ".js";
              b.async = true;
              var a = document.getElementsByTagName("script")[0];
              a.parentNode.insertBefore(b, a);
          } catch (e) {}
      }("ACCOUNT NAME"));
  </script>
  <!-- end NARRATIV jstag -->

Google Tag Manager Walkthrough
------------------------------

Below is a walkthrough for implementing the Narrativ pixel using a "Custom HTML" tag in Google Tag Manager.
Start by navigating to your Google Tag Manager Dashboard.


- Select "Tag Configuration" to begin making a new pixel.

.. image:: _static/pixel_implementation_screenshots/1_tap_configuration.png

- Select "Custom HTML" to open a text field to copy and paste the above code. Make sure you replace "ACCOUNT NAME" with your Narrativ account name.

.. image:: _static/pixel_implementation_screenshots/2_choose_custom_html.png

- Enter the code from the "Page View Tag" snippet (See the section before this). Replace the content of "BAMX_EVENT_DATA" with the relevant data from your data layer.

.. image:: _static/pixel_implementation_screenshots/3_enter_tag_html.png

- Select "All Pages" as the correct trigger for this "Page View Tag."

.. image:: _static/pixel_implementation_screenshots/4_select_trigger.png

- Name the Tag "Narrativ Page Impression" and double check that the trigger is set to "All Pages"

.. image:: _static/pixel_implementation_screenshots/5_final_product.png

- For the "Check Out Pixel", create a new tag and open the text field.

.. image:: _static/pixel_implementation_screenshots/checkout_1_open_editor.png

- This example is using a dummy data layer. You will have to customize "var purchased" to point at how you access the order content in your data layer.

.. image:: _static/pixel_implementation_screenshots/checkout_2_confirm_code_product_info.png

- Add box under "Triggering" to add a trigger for this tag.

.. image:: _static/pixel_implementation_screenshots/checkout_3_add_trigger.png

- If you don’t already have a trigger for checkout pages, then it’s easy to create one!

.. image:: _static/pixel_implementation_screenshots/checkout_4_add_confirmation_page_trigger.png

- The below example has a series of triggers based off of common URL types for checkout or confirmation pages. (E.g. narrativ.com/checkout/ will trigger the "Checkout Page" option). Replace "checkout" with whatever word your site uses on checkout pages. Remember, you only need one trigger!

.. image:: _static/pixel_implementation_screenshots/checkout_4.1_add_confirmation_rules.png

- Double check the tag name, make sure you’ve updated the code with the information on your checkout page, and make sure you’ve selected the correct trigger.

.. image:: _static/pixel_implementation_screenshots/checkout_5_double_check.png

- Make sure that the tag(s) are showing up in the "Tag" tab.

.. image:: _static/pixel_implementation_screenshots/submit_1_tag_confirmation.png

- Preview the changes made and fix any errors that pop up in the window.

.. image:: _static/pixel_implementation_screenshots/submit_2_review.png

- Click the "Submit" button to save your changes (this step is not final)

.. image:: _static/pixel_implementation_screenshots/submit_3_submit_changes.png

- Double check that everything you worked on is in this submission. Name the submission something like "Adding Narrativ Pixel" so that it’s easy to find if you need to go back and debug any issues in the future.

.. image:: _static/pixel_implementation_screenshots/submit_4_title_the_changes.png


You did it!!

If you have any issues during this process then reach out to your Narrativ contact or hello@narrativ.com

.. _Google category: https://support.google.com/merchants/answer/6324436?hl=en
.. _ISO 4217: https://www.iso.org/iso-4217-currency-codes.html
