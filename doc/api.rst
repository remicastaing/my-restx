.. _api:

API
===

.. currentmodule:: my_restx

Core
----

.. autoclass:: Api
    :members:
    :inherited-members:

.. autoclass:: Namespace
    :members:


.. autoclass:: Resource
    :members:
    :inherited-members:


Models
------

.. autoclass:: my_restx.Model
    :members:

All fields accept a ``required`` boolean and a ``description`` string in ``kwargs``.

.. automodule:: my_restx.fields
    :members:


Serialization
-------------
.. currentmodule:: my_restx

.. autofunction:: marshal

.. autofunction:: marshal_with

.. autofunction:: marshal_with_field

.. autoclass:: my_restx.mask.Mask
    :members:

.. autofunction:: my_restx.mask.apply


Request parsing
---------------

.. automodule:: my_restx.reqparse
    :members:

Inputs
~~~~~~

.. automodule:: my_restx.inputs
    :members:


Errors
------

.. automodule:: my_restx.errors
    :members:

.. autoexception:: my_restx.fields.MarshallingError

.. autoexception:: my_restx.mask.MaskError

.. autoexception:: my_restx.mask.ParseError


Schemas
-------

.. automodule:: my_restx.schemas
    :members:


Internals
---------

These are internal classes or helpers.
Most of the time you shouldn't have to deal directly with them.

.. autoclass:: my_restx.api.SwaggerView

.. autoclass:: my_restx.swagger.Swagger

.. autoclass:: my_restx.postman.PostmanCollectionV1

.. automodule:: my_restx.utils
    :members:
