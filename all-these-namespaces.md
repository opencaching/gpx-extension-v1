GPX XML namespaces related to Geocaching
========================================

About this document
-------------------

This document serves as a summary of what we know about all XML namespaces used
in GPX files used in context of Geocaching and/or Opencaching. Currently, it
resides within the [Opencaching's GPX extension repository][oc-gpx-extension],
but the purpose of this document is more general (unrelated to Opencaching).

We're attempting to write this down, because - as far as we know - no one did
yet. We have tried to google this information, but didn't find much. Perhaps
you, the reader, will help us out here? If you can add some insight into this
document, feel free to start an issue, and/or submit a pull request.


Topografix GPX
--------------

This namespace defines the root of the GPX file.


### Versions

[Topografix](http://topografix.com/) has released two XML namespaces:

 * **Topografix 1.0**, identified by `http://www.topografix.com/GPX/1/0` XML
   namespace, see XSD [here][topografix-1.0-xsd].

 * **Topografix 1.1**, identified by `http://www.topografix.com/GPX/1/1` XML
   namespace, see XSD [here][topografix-1.1-xsd].


### Backward-compatibility issues

I don't know why Topografix decided to release the new version of its schema
in the new XML namespace. Effectivelly, it has created an entirely new file
format instead of extending the existing one. It just seems extremelly weird
to me.

Perhaps this weirdness led big companies, such us Google, to resign from their
support of the GPX format in their applications?


### Usage

Topografix itself is very loosly related to Geocaching. They [have
released](https://www.expertgps.com/geocaching.asp) their app, but as far as
we know, it's not very popular. As far as we know, they have designed the
original GPX file completely independently, then Groundspeak decided to make
use of it, and it was a hit.

**As far as we know, all Geocaching sites export their GPX files in Topografix
1.0 format.** However, many external sites and applications make use of the
*Topografix 1.1* namespace, for example:

 * [GPS Visualizer](http://www.gpsvisualizer.com) exports GPX files in the
   Topografix 1.1 format.

 * [GSAK](http://gsak.net) allows to export GPX files in both 1.0 and 1.1
   formats. 


Groundspeak extensions
----------------------

These are the extensions defined by Groundspeak in order to include information
about geocaches inside the *Topografix 1.0* GPX file.


### Versions

 * **Groundspeak 1.0**, identified by `http://www.groundspeak.com/cache/1/0`
   XML namespace, see XSD [here][groundspeak-1.0-xsd].

 * **Groundspeak 1.0.1**, identified by `http://www.groundspeak.com/cache/1/0/1`
   XML namespace, see XSD [here][groundspeak-1.0.1-xsd].

   List of changes ([source](https://github.com/opencaching/gpx-extension/issues/1)):

   - Added the `inc` attribute to the `<attribute>` element.

 * **Groundspeak 1.1**, identified by `http://www.groundspeak.com/cache/1/1`
   XML namespace, see XSD [here][groundspeak-1.1-xsd].

   List of changes ([source](https://github.com/opencaching/gpx-extension/issues/1)):

   - `guid` attributes were added to the elements that represent caches, logs,
     users and travelbugs.
   - `lastUpdated` and `exported` dates were added to the `<cache>` element.
   - Changed types of lots of elements from *xs:string* to either *xs:long*,
     *xs:decimal*, *xs:double* or *xs:date*.
   - Introduced a new enumeration type *logType* for the type log elements
     (instead of type *xs:string*).
   - Bugfix: changed *maxOccurs* of the `<attributes>`, `<logs>` and
     `<travelbugs>` elements from `unbounded` to `1`.


### Backward-compatibility issues

Same as with Topografix, not sure why Groundspeak decided to release the new
version of its schema in the new XML namespace. Some unanswered questions
which might help with understanding this:

 * What are the differences between these versions?

 * If only new elements were added, why didn't Groundspeak simply add them as
   optional elements to the existing XML namespace? This wouldn't break any
   application, while changing the XML namespace would.


### Usage

As far as we know:

 * **By default, all Geocaching sites export their GPX files in *Groundspeak
   1.0.1* format.**

 * Opencaching sites don't allow any other Groundspeak extensions format than
   the *Groundspeak 1.0.1*.

 * Geocaching.com allows their users to download GPX files with *Groundspeak
   1.0* extensions. Probably for backward-compatibility with some very old apps
   (can someone confirm this?).

 * **Even geocaching.com doesn't allow their users to download GPX files with
   their new *Groundspeak 1.1* extensions.** It seems that the introduction of
   this new format was a failure (see backward-compatibility issues above). And
   again, can someone confirm this?


Summary
-------

When generating GPX files:

 * **It seems that you should always generate your Geocaching GPX files using
   the combination of *Topografix 1.0* + *Groundspeak 1.0.1*.** It's simply the
   best option, supported by all the apps.

 * Geocaching.com allows users to export *Topografix 1.0* + *Groundspeak 1.0*,
   but none of the Opencaching sites do, and the users don't complain. This
   probably means that *Groundspeak 1.0* namespace is used very rarely, and
   Geocaching.com supports this option just for a handful of users. (Can
   someone confirm this?)

When parsing GPX files:

 * **You only need to support *Topografix 1.0* + *Groundspeak 1.0.1*
   combination.** All sites, and all newer apps can export to this format, so
   your users shouldn't have problems with providing it.

 * You may sometimes encounter *Topografix 1.1* format, but this is probably
   due to some conversion by an external app. These files usually won't contain
   any Groundspeak namespace.

 * You may sometimes encounter *Groundspeak 1.0* format (not the 1.0.1 one!).
   This is due to the fact, that geocaching.com still allows their users to
   export this format. Also, presumably, some old apps still export to this
   format.


[topografix-1.0-xsd]: http://www.topografix.com/GPX/1/0/gpx.xsd
[topografix-1.1-xsd]: http://www.topografix.com/GPX/1/1/gpx.xsd
[groundspeak-1.0-xsd]: http://static.groundspeak.com/cache/1/0/cache.xsd
[groundspeak-1.0.1-xsd]: http://static.groundspeak.com/cache/1/0/1/cache.xsd
[groundspeak-1.1-xsd]: http://static.groundspeak.com/cache/1/1/cache.xsd
[oc-gpx-extension]: https://github.com/opencaching/gpx-extension
