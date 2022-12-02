Product Feeds
=============

Ingesting Product Feeds
-----------------------

In order for Howl to accurately match publisher recommendation links to a merchant's product, we require a
comprehensive product feed. Depending on your preference, we can either fetch your feed or you can send it to us via
HTTP, FTP or SFTP using the specifications detailed below. Feeds sent via FTP or SFTP should be scheduled for daily
export.

Formatting
----------

We currently support CSV and XML file formats and zip and gzip compressed files. Please ensure all fields adhere to
our `formatting requirements`_. You can view a `sample file`_ here.

Send via FTP
------------
Note: Enable passive and binary modes

.. list-table::
   :widths: 20 70
   :header-rows: 1

   * - Field Name
     - Value

   * - Host
     - ftp.planethowl.com

   * - Static IP
     - 34.235.193.55, 44.205.197.234

   * - Port
     - 21

   * - Username
     - Will be provided to you

   * - Password
     - Will be provided to you

   * - Filename
     - USERNAME-USD-yyyy-mm-dd.csv.zip


Send via SFTP
-------------
Please generate and provide us with a public RSA key to register as an authorized key for your users.

.. list-table::
   :widths: 20 70
   :header-rows: 1

   * - Field Name
     - Value

   * - Host
     - sftp.planethowl.com

   * - Static IP
     - 44.196.54.0, 44.207.179.93

   * - Port
     - 22

   * - Username
     - Will be provided to you

   * - Filename
     - USERNAME-USD-yyyy-mm-dd.csv.zip

If you have any questions about product feed requirements, please feel free to reach out to solutions@planethowl.com
for assistance.

.. _sample file: https://static.bam-x.com/api-docs/samplefeed.csv
.. _formatting requirements: https://docs.google.com/spreadsheets/d/1cwH1GrNLUy5QyPfK5zIVdvM7Z2e38A7p4BUKugYfru8/edit#gid=0
