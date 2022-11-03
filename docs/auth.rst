API Authentication
==================

Creating an API key
-------------------

To use the Howl API, you will need to create an API key for your user account.
Navigate to the `Developer Options`_ page and follow the directions there.


Using your API key
------------------

Unless otherwise indicated, Howl API requests must include a valid
API key. Send your API key in the HTTP ``Authorization`` header, prefixed
with the scheme ``NRTV-API-KEY``.
For example::

    curl -i -H 'Authorization: NRTV-API-KEY Sy8xLzE2MTE3MDIxNzY3NDM0OTc0MDcv' \
        https://api.narrativ.com/api/v1/tokeninfo/

::

    HTTP/1.1 200 OK

    {
      "info": {
        "error": false,
        "status": 200
      },
      "data": [
        {
          "token_id": 1001,
          "uid": 2,
          "description": "My API Key",
          "datetime_created": "2017-07-25T20:58:38Z",
          "datetime_updated": "2017-07-25T20:58:38Z",
          "datetime_active": "2017-07-25T20:58:38Z",
          "datetime_expires": null,
          "datetime_last_used": null,
          "is_enabled_by_user": true
        }
      ]
    }

If a valid API key is not sent, the server will return an HTTP 401 error::

    curl -i -H 'Authorization: NRTV-API-KEY TestInvalidAPIKey' \
        https://api.narrativ.com/api/v1/tokeninfo/

::

    HTTP/1.1 401 UNAUTHORIZED

    {
      "info": {
        "error": true,
        "status": 401
      },
      "data": [],
      "error": {
        "code": 4302,
        "message": "Invalid API token",
        "data": null
      }
    }


Keeping your account secure
---------------------------

Remember to keep your API key secret, since anyone who has it can use it to
access your Howl account. If you ever lose your API key, you can visit the
`Developer Options`_ page to disable it and create a new one.

.. _Developer Options: https://dashboard.narrativ.com/#/account/developer
