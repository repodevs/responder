Deploying Responder
===================

You can deploy Responder anywhere you can deploy a basic Python application.

Docker Deployment
-----------------

Assuming existing ``api.py`` and ``Pipfile.lock`` containing ``responder``.

``Dockerfile``::

    from kennethreitz/pipenv

    COPY . /app
    CMD python3 api.py

That's it!

Heroku Deployment
-----------------

The basics::

    $ mkdir my-api
    $ cd my-api
    $ git init
    $ heroku create
    ...

Install Responder::

    $ pipenv install responder --pre
    ...

Write out an ``api.py``::

    import responder

    api = responder.API()

    @api.route("/")
    async def hello(req, resp):
        resp.text = "hello, world!"

    if __name__ == "__main__":
        api.run()

Write out a ``Procfile``::

    web: python api.py

That's it! Next, we commit and push to Heroku::

    $ git add -A
    $ git commit -m 'initial commit'
    $ git push heroku master
