.. include:: links.rst

.. _Comprehensive Theming:

##################################
Comprehensive Theming for Open edX
##################################

This section describes how to create and use a theme for your Open edX
installation.

.. contents::
 :local:
 :depth: 1

**********
Background
**********

When the Open edX codebase was first made open source, there was no theming
system: the code was designed only for edx.org, and there was no way to
change the look and feel of the website to resemble anything else (without
forking the codebase). Over time, people in the Open edX community started
building their own piecemeal theming systems, to solve their own specific
problems. Two of these the theming systems managed to get merged into the
Open edX codebase: "Stanford theming" and "microsites". Neither of these
systems were designed to provide a robust, consistent, and comprehensive
theming system; they made specific parts of the system themable in specific
ways, and were built and extended as necessary to meet the needs of the teams
that built them.

The Open Source team at edX is developing a new theming system, called
"comprehensive theming", to provide a robust, consistent, and comprehensive
theming system for Open edX. This theming system will encompass all the features
provided by both "Stanford theming" and "microsites", and will be the only
supported theming system for Open edX. This documentation is only for
"comprehensive theming", and "Stanford theming" and "microsites" are
intentionally not documented. When comprehensive theming has all of the
features provided by Stanford theming, Stanford theming will be officially
deprecated and removed from the codebase, and Open edX installations that are
using Stanford theming will need to migrate their theme to use comprehensive
theming if they want to update their installation. Similarly, when
comprehensive theming has all of the features provided by microsites,
microsites will be officially deprecated and removed from the codebase,
and Open edX installations that are using microsites will need to migrate
their theme to use comprehensive theming if they want to update
their installation.

***********
Definitions
***********

* A **theme** is a collection of templates and assets that override the
  look and feel of an Open edX installation. It consists of a directory
  containing those templates and assets in a specific hierarchy.
* A **core template** is a template that exists in one of the Open edX
  codebases. For example, the HTML files in the ``lms/templates`` directory
  of the ``edx-platform`` repository are core templates.
* A **core asset** is an image, CSS file, or JavaScript file that exists
  in one of the Open edX codebases. For example, the image files in the
  ``lms/static/images`` directory of the ``edx-platform`` repository are
  core assets.
* A **themed template** is a template that exists in a theme. Typically,
  themed templates are organized and named in a way that parallels a core
  template, so that the themed template will override the core template.
  For example, a themed template named
  ``my-theme-directory/lms/templates/header.html`` will override a core
  template named ``lms/templates/header.html`` in the ``edx-platform``
  repository.
* A **themed asset** is an image, CSS file, or JavaScript file that exists
  in a theme. Typically, themed assets are organized and named in a way that
  parallels a core asset, so that the themed asset will override the core
  template. For example, a themed asset named
  ``my-theme-directory/lms/static/images/logo.png`` will override a core
  asset named ``lms/static/images/logo.png`` in the ``edx-platform`` repository.

****************
Creating a Theme
****************

To make a theme, start by creating a directory with a reasonable name for
your theme. It's a good idea to put a README file into this directory with
a description of what your theme is for, and to put the entire directory under
version control. In this example, we'll call the theme ``my-theme``:

.. code::

    my-theme
    └── README.rst

Next, create a subdirectory for the Open edX subsystem that you want your theme
to apply to. One theme can apply to multiple subsystems: LMS, Studio,
certificates, emails, etc. For the moment, only the LMS subsystem is
supported, so we'll make a ``lms`` directory.

.. code::

    my-theme
    ├── README.rst
    └── lms

Let's override an asset in the LMS. To do that, make a ``static``
directory in the ``lms`` directory, and add an asset with the same name and
directory path as the asset you want to override. For example, to override
the logo in the LMS, the name and path is ``images/logo.png``.

.. code::

    my-theme
    ├── README.rst
    └── lms
        └── static
            └── images
                └── logo.png

Let's also override a template in the LMS. To do that, make a ``templates``
directory in the ``lms`` directory, and add a template with the same name
and directory path as the template you want to override. At the moment, only
Mako templates are supported. For example, to override the header of the LMS,
the name and path is simply ``header.html``.

.. code::

    my-theme
    ├── README.rst
    └── lms
        ├── static
        |   └── images
        |       └── logo.png
        └── templates
            └── header.html
