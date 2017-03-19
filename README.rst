===============================
Using the Simple Plone Buildout
===============================
 
This is a method for installing Plone on all platforms that run Python, including Windows.

For the complete list of Plone installation methods, see https://plone.org/download

.. contents:: 

Requirements
============

`For Windows, click this link to install the software required by Plone <#installing-required-software-for-windows>`_

For all other platforms, you will require:

- Python 2.7
- Git
- a compiler, usually GCC

Installation Steps
==================

1. Clone the repository
-----------------------

Get started by cloning this repository:

.. code:: sh

   $ git clone https://github.com/plone/simple-plone-buildout

On Windows:
  
.. code:: bat

  C:\Users\foo> git clone https://github.com/plone/simple-plone-buildout

2. Select a configuration
-------------------------

Copy the ``buildout.cfg_tmpl`` into the buildout root. The 
``profiles/testing.cfg`` profile is active by default, but you can use any of
the others (see the `possible buildout configurations below <#extending-buildout-configs>`_):

.. code:: sh

    $ cd simple-plone-buildout
    $ cp profiles/buildout.cfg.tmpl buildout.cfg

On Windows:

.. code:: bat

  C:\Users\foo> cd simple-plone-buildout
  C:\Users\foo\simple-plone-buildout> copy profiles\buildout.cfg.tmpl buildout.cfg

3. Create a Python virtual environment
--------------------------------------

Create a Python virtual environment ("sandbox") in a directory named `env`, to avoid affecting your system Python::

 $ virtualenv env
 
On Windows:

.. code:: bat

  C:\Users\foo\simple-plone-buildout> virtualenv env

4. Install buildout and setuptools
----------------------------------

Install the versions of ``zc.buildout`` and ``setuptools`` you will need:

.. code:: sh

   $ env/bin/pip install -r requirements.txt

On Windows, the executable for `pip.exe` is in the ``Scripts`` directory, instead of ``bin``:

.. code:: bat

  C:\Users\foo\simple-plone-buildout> env\Scripts\pip install -r requirements.txt

5. Run buildout
---------------

To create an instance, run

.. code:: sh

   $ env/bin/buildout

On Windows:

.. code:: bat

  C:\Users\foo\simple-plone-buildout> env\Scripts\buildout

Do not be alarmed if you see the following

.. code:: python

   SyntaxError: 'return' outside function

**Ignore** ``SyntaxErrors`` that scroll by while you enjoy your coffee. 

This will download Plone's eggs and modules for you, as well as other 
dependencies and create a new Plone instance.

6. Start Plone
--------------

You can start your Plone instance by running

.. code:: sh

   $ bin/instance fg
 
On Windows:

.. code:: bat

    C:\Users\foo\simple-plone-buildout> bin\instance fg

or, to run in background mode

.. code:: sh

   $ bin/instance start

On Windows:

.. code:: bat

    C:\Users\foo\simple-plone-buildout> bin\instance start

7. Enjoy!
---------

Navigate your browser to `<http://localhost:8080>`_

The initial user is **admin** with **admin** as the password.
 

Working with buildout.cfg
=========================

You can change any option in ``base.cfg`` and re-run ``env/bin/buildout`` to reflect
the changes. This may delete things inside the ``parts`` directory, but should
keep your ``Data.fs`` and source files intact.

To save time, you can run buildout in non-updating (``-N``)
mode, which will prevent it from downloading things and checking for new
versions online

.. code:: sh

   $ env/bin/buildout -Nv

Extending buildout configs
==========================

This buildout makes use of the 'extends' functionality of buildout.  The
buildout.cfg contains only minimal information.  Here are what the rest of the
configs are for.

buildout.cfg.tmpl
  This is a template to be used for the buildout.cfg at the root of the
  site. See the file for more details.

base.cfg
  The base config contains all of the configuration for the basis of the site.
  Typical sections include zope2, instance, zeoserver and plone.  In this
  config we include all the eggs and modules that will be used in all of the
  extended configs.

local.cfg
  The local config sets up our local development environment for us.  It
  includes all the debugging packages that are typically used during
  development.  It extends base.cfg and debug.cfg

debug.cfg
  The debug config contains all of our debugging modules and packages. One
  package to make note of is PDBDebugMode.  It will open up a pdb prompt
  anytime there is an error.  This will cause the page to hang until you tell
  pdb to (c)ontinue.

  The debug config also contains a way to 'refresh' your product in
  plone.reload.  You can access it like this::

    http://localhost:8080/@@reload

  And also a way of recording doctests::

    http://localhost:8080/++resource++recorder/index.html

  Take a look at the config to see what other tools are available.

release.cfg
  The release config is the base config for doing releases.  It contains the
  specific versions of eggs that are needed to make the site run properly.  It
  also contains some configuration that is common for each release stage.

versions.cfg
  This contains the pinned versions of packages for use when release to 
  production.

testing.cfg
  The dev config merely sets up the proper port and ip-address for the dev
  site to run on. This profile also does not use a `zeoserver` part to simplify
  operation on windows and those wanting to just try Plone.

prod.cfg
  The prod config is similar to the dev and maint configs in that it sets up
  the proper ip-address and port numbers.  But it can also be used to set up a
  cluster, tune the number of threads being used, bump up zeo cache
  sizes, set up pound, squid, nginx, etc.  This will be the config used to run
  the site in production mode.

========================================
Installing Required Software for Windows
========================================

Download and run the following installers.

* `Python 2.7.13 x86-64 MSI Installer <https://www.python.org/downloads/release/python-2713>`_

  * You may choose either "Install for all users" or "Install just for me" (both work). On the installer's "Customize Python 2.7.13 (64-bit)" page, scroll down and click on the option to "Add python.exe to Path".
  * After installing, make sure ``python.exe`` is in your PATH. To test if it is in your PATH, type "python" and hit Return; if you see a message ``'python' is not recognized as an internal or external command, operable program or batch file`` then it is not in your PATH and you may have to restart Windows, or you can add it to your PATH manually with the command ``PATH=$PATH;c:\Python27``.

.. figure:: https://raw.githubusercontent.com/plone/simple-plone-buildout/master/docs/customize-python-setup-add-to-path.jpg
  :width: 50 %
  :align: center

  Be sure to add python.exe to Path

* `Microsoft Visual C++ Compiler for Python 2.7 <http://aka.ms/vcpython27>`_

* `Git for Windows <https://git-for-windows.github.io>`_

  * When installing Git for Windows, use the default choices on all the installer questions. You may have to restart Windows for git.exe to appear in your PATH. To add it to your PATH manually, use the command ``PATH=$PATH;c:\Program Files\Git\bin``

* Open PowerShell and install ``virtualenv``. You may have to use the command ``PATH=$PATH;c:\python27\scripts`` for pip.exe to appear in your PATH::

    C:\Users\foo> pip install virtualenv


You are now ready to follow the instructions at the top of this file, but keep
in mind that your ``virtualenv`` will not have a ``bin`` directory. It will be
called ``Scripts`` so adjust the commands accordingly.
