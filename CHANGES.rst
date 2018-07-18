Changelog
=========

5.1.x unreleased
----------------

- Make it easier to get at the instance environment variables.
  Remove TZ from preset environment vars.
  Better to leave it with the system tz than to preset to something likely wrong.
  [smcmahon]

- New users have been having a hard time figuring out how to update this buildout.
  Add sections for instance eggs, versions and sources to the buildout.cfg template.
  Make it possible to easily update the Plone version.
  [smcmahon]

5.1.0 (2018-03-24)
------------------

- updated to use Plone 5.1.0
  [tkimnguyen]

5.0.8 (2017-11-05)
------------------

- updated to use Plone 5.0.8
  [tkimnguyen]

- workaround for change in zc.buildout 2.9.5 that forces HTTPS
  [tkimnguyen]

- documentation fixes
  [svx, tkimnguyen]

5.0.7 (2017-03-18)
------------------

- Add explanation about UI and simple buildout
  [tkimnguyen] 

- Add missing parts from 4d55a97
  [svx]

- Improve Docs
  [svx]
