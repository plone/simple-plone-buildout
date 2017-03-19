========
Buildout
========

Working with buildout.cfg
=========================

You can change any option in ``base.cfg`` and re-run ``env/bin/buildout`` to reflect
the changes. This may delete things inside the ``parts`` directory, but should
keep your ``Data.fs`` and source files intact.

To save time, you can run buildout in non-updating (``-N``)
mode, which will prevent it from downloading things and checking for new
versions online

.. code-block:: shell

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
