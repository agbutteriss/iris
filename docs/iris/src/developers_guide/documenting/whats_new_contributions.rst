=================================
Contributing a "What's New" entry
=================================

Iris has an aggregator for building a draft "What's New" document for each release from a number of separate entries stored in ``docs/iris/src/whatsnew/contributions_<release number>``, where each entry is the description of a single change to Iris which improved Iris in some way for the user. As such, a single Iris pull request may contain multiple changes that are worth highlighting as contributions in the "What's New" document. Likewise, it may occassionally be the case that an update doesn't require a "What's New" entry (for example, fixing a bug that was itself introduced since the most recent release), but as a general rule, each pull request should include at least one "What's New" entry. 

In other words, "What's New" entries should be written by the authors of the relevant code themselves, and then submitted as part of the pull request making the change. This means that the person who has written the "What's New" entry is the person most familiar with the code, and it avoids the release developer having to personally review each change in detail when it comes to making the release.
This document walks through the process for writing a "What's New" entry, and then describes how the draft "What's New" page is created.

Writing a "What's New" Entry
============================

In the ideal case, an Iris "What's New" entry is written as a single concise bullet point (though there may sometimes be exceptions), aimed at the Iris user as an audience.
Like all Iris documentation, it is written in `reStructuredText <http://docutils.sourceforge.net/rst.html>`_, and ultimately compiled using `Sphinx <http://www.sphinx-doc.org/en/stable/index.html>`_.
As an example, if there was a bug where :func:`iris.plot.scatter` was plotting upside down (somehow), and your code fixed it, the "What's New" entry could look something like this::

* Using :func:`iris.plot.scatter` will no longer result in an upside down chart.

Note that this entry begins with an '\*'; in general *all* "What's New" entries should. The `:func:` is a decorator provided by Sphinx, in this case for internal linking to the documentation for a specific function. For more information on using reStructuredText, see the :doc:`quickstart guide <rest_guide>`.
It is also worth noting that the final "What's New" page is edited by the release developer, and so the "What's New" entry does not have to be perfect or complete in every respect.

Once written, the "What's New" entry has to be saved in ``docs/iris/src/whatsnew/contributions_<release number>``, as described above, using the naming convention below.

Filename Conventions
====================

The filename for each item should be of the form ``<category>_<date>_<summary>.txt``, where:

* The category must be one of the following:

    *newfeature*
      Features that are new or changed to add functionality.
    *bugfix*
      A bugfix.
    *incompatiblechange*
      A change that causes an incompatibility with prior versions of Iris.
    *deprecate*
      Deprecations of functionality.
    *docchange*
      Changes to documentation.

* The date must be of the form YYYY-Mon-DD, e.g.:

  * 2012-Jan-30
  * 2014-May-03
  * 2015-Feb-19

* The summary can be any remaining filename characters, and simply provides a short identifying description of the change. e.g:

  * whats-new-aggregator
  * using_mo_pack
  * correction-to-bilinear-regrid
  * GRIB2_pdt11

The following are all examples of valid filenames:

 * bugfix_2015-Aug-18_partial_pp_constraints.txt
 * deprecate_2015-Nov-01_unit-module.txt
 * incompatiblechange_2015-Oct-12_GRIB_optional_Python3_unavailable.txt
 * newfeature_2015-Jul-03_pearsonr_rewrite.txt

.. note::
    A test in the standard test suite ensures that all the contents of the
    latest contributions directory conform to this naming scheme.

Compiling a Draft
=================

Compiling a draft from the supplied contributions should be done when preparing
a release. Running ``docs/iris/src/whatsnew/aggregate_directory.py`` with the
release number as the argument will create a draft what's new with the name
``<release>.rst`` file for the specified release, by aggregating the individual
contributions from the relevant folder.
Omitting the release number will build the latest version for which a
contributions folder is present.
This command fails if a file with the relevant name already exists.

The resulting draft document is only a starting point, which the release
developer will then edit to produce the final 'What's new in Iris x.x'
documentation.

