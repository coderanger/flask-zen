Flask-Zen
=========

.. module:: flaskext.zen

Flask-Zen is an extension to `Flask`_ that allows you to use `PyZen`_ via
`Flask-Script`_ commands. Both a simple test runner command and the standard
PyZen auto-runner are provided. You can install the requirements from PyPI
with `easy_install` or `pip` or download them by hand.

Installation
------------

Install the extension with one of the following commands::

    $ easy_install Flask-Zen

or alternatively if you have `pip` installed::

    $ pip install Flask-Zen

.. _Flask: http://flask.pocoo.org/
.. _PyZen: http://pypi.python.org/pypi/PyZen/
.. _Flask-Script: http://pypi.python.org/pypi/Flask-Script

Configuration
-------------
PyZen exposes two Flask-Script commands: ``Test`` and ``ZenTest``. To
configure both::

    from flask.ext.script import Manager
    from flask.ext.zen import Test, ZenTest

    manager = Manager(app)

    manager.add_command('test', Test())
    manager.add_command('zen', ZenTest())

    if __name__ == '__main__':
        manager.run()


Any of the command-line options below can be overridden using a keyword
argument to the ``Test`` or ``ZenTest`` constructor::

    manager.add_command('zen', ZenTest(nocolor=True, ui='none'))


Usage
-----
The ``Test`` command will run a single test run and exit. The ``ZenTest``
command will run the normal PyZen continuous tester.

``-s``, ``--start-dir`` : *default: location of manage.py*
    Base directory for test discovery.

``-p``, ``--pattern`` : *default: \*/tests/\*.py;\*/tests.py*
    Semicolon separated file globs to use for loading tests.

``-v``, ``--verbosity`` : *default: 1*
    Test runner verbosity.

``--nocolor`` : *flag, default: False*
    Disable colored output.

``-u``, ``--ui`` : *only for ZenTest, default: autodetect*
    Force the use of a specific UI module. Available options are ``win32``,
    ``osx``, ``linux``, and ``none``.
