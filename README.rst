===============================
Using the Simple Plone Buildout
===============================
 
`Windows users, click this link to get started <#using-windows>`_

Get started by cloning this repository

.. code:: sh

   $ git clone https://github.com/plone/simple-plone-buildout

First, copy the ``buildout.cfg_tmpl`` into the buildout root. The 
``profiles/testing.cfg`` profile is active by default, but you can use any of
the others. See descriptions below.

.. code:: sh

    $ cd simple-plone-buildout
    $ cp profiles/buildout.cfg.tmpl buildout.cfg

Then you need to run::

 $ virtualenv env
 
This will create an env directory with a virtual environment. You should then
install the versions of ``zc.buildout`` and ``setuptools`` you need

.. code:: sh

   $ env/bin/pip install -r requirements.txt
   
In Windows some version of python creates the Script folder instead of bin folder. In that case
   
.. code:: sh

   $ env/Scripts/pip install -r requirements.txt

To create an instance, run

.. code:: sh

   $ env/bin/buildout

In case of Scripts folder

.. code:: sh

 $ env/Scripts/buildout

Do not be alarmed if you see the following

.. code:: python

   SyntaxError: 'return' outside function

**Ignore** ``SyntaxErrors`` that scroll by while you enjoy your coffee. It's just
a Zope Script (Python) thing.

This will download Plone's eggs and products for you, as well as other 
dependencies, create a new Zope 2 installation, and create a new Zope instance
configured with these products.

You can start your Zope instance by running

.. code:: sh

   $ bin/instance fg
 
or, to run in background mode

.. code:: sh

   $ bin/instance start

Enjoy!
------

Navigate your browser to `<http://localhost:8080>`_

The initial ZMI user is **admin** with **admin** as the password.
 

Working with buildout.cfg
-------------------------

You can change any option in ``base.cfg`` and re-run ``env/bin/buildout`` to reflect
the changes. This may delete things inside the ``parts`` directory, but should
keep your ``Data.fs`` and source files intact.

To save time, you can run buildout in non-updating (``-N``)
mode, which will prevent it from downloading things and checking for new
versions online

.. code:: sh

   $ env/bin/buildout -Nv

Extending buildout configs
--------------------------

This buildout makes use of the 'extends' functionality of buildout.  The
buildout.cfg contains only minimal information.  Here are what the rest of the
configs are for.

buildout.cfg.tmpl
  This is a template to be used for the buildout.cfg at the root of the
  site. See the file for more details.

base.cfg
  The base config contains all of the configuration for the basis of the site.
  Typical sections include zope2, instance, zeoserver and plone.  In this
  config we include all the eggs and products that will be used in all of the
  extended configs.

local.cfg
  The local config sets up our local development environment for us.  It
  includes all the debugging packages that are typically used during
  development.  It extends base.cfg and debug.cfg

debug.cfg
  The debug config contains all of our debugging products and packages. One
  package to make note of is PDBDebugMode.  It will open up a pdb prompt
  anytime there is an error.  This will cause the page to hang until you tell
  pdb to (c)ontinue.

  The debug config also contains a way to 'refresh' your product in
  plone.reload.  You can access it like this::

    http://<zope_host>:<zope_port>/@@reload

  And also a way of recording doctests::

    http://<zope_host>:<zope_port>/++resource++recorder/index.html

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
  Zope cluster, tune the number of threads being used, bump up zeo cache
  sizes, set up pound, squid, nginx, etc.  This will be the config used to run
  the site in production mode.

=============
Using Windows
=============

Download and double click install the following installers.

* `Python 2.7.12 x86-64 MSI Installer <https://www.python.org/downloads/release/python-2712>`_

  * When installing, ensure the option for "Add python.exe to Path" is active
  * After installing, make sure ``python.exe`` is in your Path

* `Microsoft Visual C++ Compiler for Python 2.7 <http://aka.ms/vcpython27>`_
* `Git for Windows <https://git-for-windows.github.io>`_
* Open PowerShell and install ``virtualenv``::

    PS C:\Users\foo> pip install virtualenv

You are now ready to follow the instructions at the top of this file, but keep
in mind that your ``virtualenv`` will not have a ``bin`` directory. It will be
called ``Scripts`` so adjust the commands accordingly.
