====
UNIX
====

Requirements
============

- Python 2.7
- Git
- A compiler, usually GCC

For a full list of requirements please consult the `documentation about requirements <https://docs.plone.org/manage/installing/requirements.html>`_.

Installing Plone
================

Get started by cloning this repository:

.. code-block:: shell

   git clone https://github.com/plone/simple-plone-buildout

Copy the ``buildout.cfg_tmpl`` into the buildout root.

The ``profiles/testing.cfg`` profile is active by default, but you can use any of the :doc:`others <working_with_buildout>`.

.. code-block:: shell

   cd simple-plone-buildout
   cp profiles/buildout.cfg.tmpl buildout.cfg

Then you need to run

.. code-block:: shell

   virtualenv env

This will create an **env** directory with a virtual environment.

You should then install the versions of ``zc.buildout`` and ``setuptools`` you need run:

.. code-block:: shell

   env/bin/pip install -r requirements.txt

Create an instance:

.. code-block:: shell

   env/bin/buildout


**Do not** be alarmed if you see the following:

.. code-block:: python

   SyntaxError: 'return' outside function

**Ignore** ``SyntaxErrors`` that scroll by while you enjoy your coffee.

This will download Plone's eggs and modules for you, as well as other dependencies and create a new Plone instance.

You can start your Plone instance by running:

.. code-block:: shell

   bin/instance fg

Or, to run in background mode

.. code-block:: shell

   bin/instance start


Navigate your browser to `<http://localhost:8080>`_.

The initial user is **admin** with **admin** as the password.
