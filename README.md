Opencaching GPX Extension
=========================

Introduction
------------

This repository contains the XML Schema of the newly proposed Opencaching GPX
Extension. This extension will reside in the
`https://github.com/opencaching/gpx-extension-v1` XML namespace (as discussed
[here](https://github.com/opencaching/gpx-extension-v1/issues/6)).

This is a fairly new project, so the schema is currently empty. We are
discussing introducing new elements in separate feature branches (which will
eventually be merged to the stable schema in the `master` branch).


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


Other popular GPX Extensions
----------------------------

Read about them in a separate article
[here](https://github.com/opencaching/gpx-extension-v1/blob/master/all-these-namespaces.md).
