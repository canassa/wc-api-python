WooCommerce API - Python Client
===============================

A Python wrapper for the WooCommerce REST API. Easily interact with the WooCommerce REST API using this library.

.. image:: https://secure.travis-ci.org/woothemes/wc-api-python.svg
    :target: http://travis-ci.org/woothemes/wc-api-python

.. image:: https://img.shields.io/pypi/v/woocommerce.svg
    :target: https://pypi.python.org/pypi/WooCommerce


Installation
------------

.. code-block:: bash

    pip install woocommerce

Getting started
---------------

Generate API credentials (Consumer Key & Consumer Secret) following this instructions http://docs.woothemes.com/document/woocommerce-rest-api/.

Check out the WooCommerce API endpoints and data that can be manipulated in http://woothemes.github.io/woocommerce-rest-api-docs/.

Setup
-----

.. code-block:: python

    from woocommerce import API

    wcapi = API(
        url="http://example.com",
        consumer_key="ck_XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX",
        consumer_secret="cs_XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX"
    )


Options
~~~~~~~

+--------------------+------------+----------+-------------------------------------------------------------------------------------------------------+
|       Option       |    Type    | Required |                                              Description                                              |
+====================+============+==========+=======================================================================================================+
| ``url``            | ``string`` | yes      | Your Store URL, example: http://woo.dev/                                                              |
+--------------------+------------+----------+-------------------------------------------------------------------------------------------------------+
| ``consumerKey``    | ``string`` | yes      | Your API consumer key                                                                                 |
+--------------------+------------+----------+-------------------------------------------------------------------------------------------------------+
| ``consumerSecret`` | ``string`` | yes      | Your API consumer secret                                                                              |
+--------------------+------------+----------+-------------------------------------------------------------------------------------------------------+
| ``version``        | ``string`` | no       | API version, default is ``v3``                                                                        |
+--------------------+------------+----------+-------------------------------------------------------------------------------------------------------+
| ``verify_ssl``     | ``bool``   | no       | Verify SSL when connect, use this option as ``false`` when need to test with self-signed certificates |
+--------------------+------------+----------+-------------------------------------------------------------------------------------------------------+

Methods
-------

+--------------+----------------+------------------------------------------------------------------+
|    Params    |      Type      |                           Description                            |
+==============+================+==================================================================+
| ``endpoint`` | ``string``     | WooCommerce API endpoint, example: ``customers`` or ``order/12`` |
+--------------+----------------+------------------------------------------------------------------+
| ``data``     | ``dictionary`` | Data that will be converted to JSON                              |
+--------------+----------------+------------------------------------------------------------------+

GET
~~~

- ``.get(endpoint)``

POST
~~~~

- ``.post(endpoint, data)``

PUT
~~~

- ``.put(endpoint, data)``

DELETE
~~~~~~

- ``.delete(endpoint)``

Response
--------

All methods will return `Response <http://docs.python-requests.org/en/latest/api/#requests.Response>`_ object.

Example of returned data:

.. code-block:: bash

    >>> r = wcapi.get("products")
    >>> r.status_code
    200
    >>> r.headers['content-type']
    'application/json; charset=UTF-8'
    >>> r.encoding
    'UTF-8'
    >>> r.text
    u'{"products":[{"title":"Flying Ninja","id":70,...' // Json text
    >>> r.json()
    {u'products': [{u'sold_individually': False,... // Dictionary data


Changelog
---------

1.0.3 - 2015/08/07
~~~~~~~~~~~~~~~~~~

- Forced utf-8 encoding on ``API.__request()`` to avoid ``UnicodeDecodeError``

1.0.2 - 2015/08/05
~~~~~~~~~~~~~~~~~~

- Fixed handler for query strings

1.0.1 - 2015/07/13
~~~~~~~~~~~~~~~~~~

- Fixed support for Python 2.6

1.0.1 - 2015/07/12
~~~~~~~~~~~~~~~~~~

- Initial version
