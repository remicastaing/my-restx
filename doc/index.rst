.. my-restx documentation master file, created by
   sphinx-quickstart on Wed Aug 13 17:07:14 2014.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Welcome to my-restx's documentation!
=======================================

my-restx is an extension for Flask that adds support for quickly building REST APIs.
my-restx encourages best practices with minimal setup.
If you are familiar with Flask, my-restx should be easy to pick up.
It provides a coherent collection of decorators and tools to describe your API
and expose its documentation properly (using Swagger).

my-restx is a community driven fork of `Flask-RESTPlus
<https://github.com/noirbizarre/flask-restplus>`_


Why did we fork?
================

The community has decided to fork the project due to lack of response from the
original author @noirbizarre. We have been discussing this eventuality for
`a long time <https://github.com/noirbizarre/flask-restplus/issues/593>`_.

Things evolved a bit since that discussion and a few of us have been granted
maintainers access to the github project, but only the original author has
access rights on the PyPi project. As such, we been unable to make any actual
releases. To prevent this project from dying out, we have forked it to continue
development and to support our users.


Compatibility
=============

my-restx requires Python 2.7+ or 3.4+.


Installation
============

You can install my-restx with pip:

.. code-block:: console

    $ pip install my-restx

or with easy_install:

.. code-block:: console

    $ easy_install my-restx


Documentation
=============

This part of the documentation will show you how to get started in using
my-restx with Flask.

.. toctree::
    :maxdepth: 2

    installation
    quickstart
    marshalling
    parsing
    errors
    mask
    swagger
    logging
    postman
    scaling
    example
    configuration


API Reference
-------------

If you are looking for information on a specific function, class or
method, this part of the documentation is for you.

.. toctree::
   :maxdepth: 2

   api

Additional Notes
----------------

.. toctree::
   :maxdepth: 2

   contributing


Indices and tables
==================

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`
