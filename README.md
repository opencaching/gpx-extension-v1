Opencaching GPX Extension
=========================

Introduction
------------

This repository contains the [XML Schema](https://github.com/opencaching/gpx-extension-v1/blob/master/schema.xsd)
of the Opencaching GPX Extension. This extension allows to add Opencaching-specific
information to GPX files. It resides in the `https://github.com/opencaching/gpx-extension-v1`
XML namespace (as discussed [here](https://github.com/opencaching/gpx-extension-v1/issues/6)).


Versioning Strategy
-------------------

* We use [Semantic Versioning](http://semver.org/) in our schema releases. This
  means that, as long as the version stays at `1.x.x`, we have not introduced
  any breaking changes.

* We are also NOT planning to ever change the XML namespace itself. Hopefully,
  it will forever stay the same:

  ```
  https://github.com/opencaching/gpx-extension-v1
  ```

* We *are* however planning to update the schema periodically, by introducing
  new elements, in a way we consider backward-compatible. In particular, this
  means that we will keep modifying the existing schema, without changing its
  XML namespace.

  Note, that this stands in contrast with the strategy adopted by many other
  Geocaching schema providers. We believe that our way is better. You can read
  more about this (and discuss it with us)
  [here](https://github.com/opencaching/gpx-extension-v1/blob/master/all-these-namespaces.md).


Implementations
---------------

The Opencaching GPX Extension is implemented in [OKAPI](https://opencaching.pl/okapi)
and in native [Opencaching.de](https://www.opencaching.de) GPX download. An
Implementation for other Opencaching sites is
[on the way](https://github.com/opencaching/opencaching-pl/pull/1240).


Other popular GPX Extensions
----------------------------

Read about them in a separate article
[here](https://github.com/opencaching/gpx-extension-v1/blob/master/all-these-namespaces.md).
