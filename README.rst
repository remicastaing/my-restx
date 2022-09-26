===========
Flask RESTX
===========

.. image:: https://github.com/remicastaing/my-restx/workflows/Tests/badge.svg?branch=master&event=push
    :target: https://github.com/remicastaing/my-restx/actions?query=workflow%3ATests
    :alt: Tests status
.. image:: https://codecov.io/gh/remicastaing/my-restx/branch/master/graph/badge.svg
    :target: https://codecov.io/gh/remicastaing/my-restx
    :alt: Code coverage
.. image:: https://readthedocs.org/projects/my-restx/badge/?version=latest
    :target: https://my-restx.readthedocs.io/en/latest/
    :alt: Documentation status
.. image:: https://img.shields.io/pypi/l/my-restx.svg
    :target: https://pypi.org/project/my-restx
    :alt: License
.. image:: https://img.shields.io/pypi/pyversions/my-restx.svg
    :target: https://pypi.org/project/my-restx
    :alt: Supported Python versions
.. image:: https://badges.gitter.im/Join%20Chat.svg
    :target: https://gitter.im/remicastaing?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge
    :alt: Join the chat at https://gitter.im/remicastaing
.. image:: https://img.shields.io/badge/code%20style-black-000000.svg
    :target: https://github.com/psf/black
    :alt: Code style: black


my-restx is a community driven fork of `Flask-RESTPlus <https://github.com/noirbizarre/flask-restplus>`_.


my-restx is an extension for `Flask`_ that adds support for quickly building REST APIs.
my-restx encourages best practices with minimal setup.
If you are familiar with Flask, my-restx should be easy to pick up.
It provides a coherent collection of decorators and tools to describe your API
and expose its documentation properly using `Swagger`_.


Compatibility
=============

my-restx requires Python 2.7 or 3.4+.

On Flask Compatibility
======================

Flask and Werkzeug moved to versions 2.0 in March 2020. This caused a breaking change in my-restx.

.. list-table:: RESTX and Flask / Werkzeug Compatibility
    :widths: 25 25 25
    :header-rows: 1


    * - my-restx version
      - Flask version
      - Note
    * - <= 0.3.0
      - < 2.0.0
      - unpinned in my-restx. Pin your projects!
    * - == 0.4.0
      - < 2.0.0
      - pinned in my-restx.
    * - >= 0.5.0
      - All (For Now)
      - unpinned, import statements wrapped for compatibility
    * - trunk branch in Github
      - All (and updated more often)
      - unpinned, will address issues faster than releases.

Installation
============

You can install my-restx with pip:

.. code-block:: console

    $ pip install my-restx

or with easy_install:

.. code-block:: console

    $ easy_install my-restx


Quick start
===========

With my-restx, you only import the api instance to route and document your endpoints.

.. code-block:: python

    from flask import Flask
    from flask_restx import Api, Resource, fields

    app = Flask(__name__)
    api = Api(app, version='1.0', title='TodoMVC API',
        description='A simple TodoMVC API',
    )

    ns = api.namespace('todos', description='TODO operations')

    todo = api.model('Todo', {
        'id': fields.Integer(readonly=True, description='The task unique identifier'),
        'task': fields.String(required=True, description='The task details')
    })


    class TodoDAO(object):
        def __init__(self):
            self.counter = 0
            self.todos = []

        def get(self, id):
            for todo in self.todos:
                if todo['id'] == id:
                    return todo
            api.abort(404, "Todo {} doesn't exist".format(id))

        def create(self, data):
            todo = data
            todo['id'] = self.counter = self.counter + 1
            self.todos.append(todo)
            return todo

        def update(self, id, data):
            todo = self.get(id)
            todo.update(data)
            return todo

        def delete(self, id):
            todo = self.get(id)
            self.todos.remove(todo)


    DAO = TodoDAO()
    DAO.create({'task': 'Build an API'})
    DAO.create({'task': '?????'})
    DAO.create({'task': 'profit!'})


    @ns.route('/')
    class TodoList(Resource):
        '''Shows a list of all todos, and lets you POST to add new tasks'''
        @ns.doc('list_todos')
        @ns.marshal_list_with(todo)
        def get(self):
            '''List all tasks'''
            return DAO.todos

        @ns.doc('create_todo')
        @ns.expect(todo)
        @ns.marshal_with(todo, code=201)
        def post(self):
            '''Create a new task'''
            return DAO.create(api.payload), 201


    @ns.route('/<int:id>')
    @ns.response(404, 'Todo not found')
    @ns.param('id', 'The task identifier')
    class Todo(Resource):
        '''Show a single todo item and lets you delete them'''
        @ns.doc('get_todo')
        @ns.marshal_with(todo)
        def get(self, id):
            '''Fetch a given resource'''
            return DAO.get(id)

        @ns.doc('delete_todo')
        @ns.response(204, 'Todo deleted')
        def delete(self, id):
            '''Delete a task given its identifier'''
            DAO.delete(id)
            return '', 204

        @ns.expect(todo)
        @ns.marshal_with(todo)
        def put(self, id):
            '''Update a task given its identifier'''
            return DAO.update(id, api.payload)


    if __name__ == '__main__':
        app.run(debug=True)


Contributors
============

my-restx is brought to you by @remicastaing. Since early 2019 @SteadBytes,
@a-luna, @j5awry, @ziirish volunteered to help @remicastaing keep the project up
and running.
Of course everyone is welcome to contribute and we will be happy to review your
PR's or answer to your issues.


Documentation
=============

The documentation is hosted `on Read the Docs <http://my-restx.readthedocs.io/en/latest/>`_


.. _Flask: https://flask.palletsprojects.com/
.. _Swagger: https://swagger.io/


Contribution
============
Want to contribute! That's awesome! Check out `CONTRIBUTING.rst! <https://github.com/remicastaing/my-restx/blob/master/CONTRIBUTING.rst>`_
