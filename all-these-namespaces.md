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
in the new XML namespace. Effectively, it has created an entirely new file
format instead of extending the existing one. Does anyone know why they have
decided to use this strategy? Discuss [here][weird-namespaces].

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
 * [TerraCaching](http://terracaching.com/) is using Topografix 1.1 format
   ([source](https://github.com/opencaching/gpx-extension/issues/2)).


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
version of its schema in the new XML namespace. Discuss
[here][weird-namespaces].


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


GSAK Extensions
---------------

[GSAK](http://www.gsak.net/) is a desktop Geocaching application. They have
defined some extensions of their own, some of which got adopted by the rest of
the geocaching community.


### Versions

 * **GSAK 1.1**, identified by `http://www.gsak.net/xmlv1/1` XML namespace, see
   XSD [here][gsak-1.1-xsd].

 * **GSAK 1.2**, identified by `http://www.gsak.net/xmlv1/2` XML namespace, see
   XSD [here][gsak-1.2-xsd].

 * **GSAK 1.3**, identified by `http://www.gsak.net/xmlv1/3` XML namespace, see
   XSD [here][gsak-1.3-xsd].

 * **GSAK 1.4**, identified by `http://www.gsak.net/xmlv1/4` XML namespace, see
   XSD [here][gsak-1.4-xsd].

 * **GSAK 1.5**, identified by `http://www.gsak.net/xmlv1/5` XML namespace, see
   XSD [here][gsak-1.5-xsd].

 * **GSAK 1.6**, identified by `http://www.gsak.net/xmlv1/6` XML namespace, see
   XSD [here][gsak-1.6-xsd].


### Backward-compatibility issues

Same issues as with Topografix and Groundspeak. Their changes seem to be
backward-compatible (can someone confirm this?), but still, they choose to
switch XML namespace on every release, which seems to be effectively ruining
this backward-compatibility.

Currently, GSAK seems to be generating the most problems of all schema
providers, because Topografix and Groundspeak seem to have learned something
from their mistakes (they stopped releasing new namespaces, or at least it
seems that they have).

Discuss [here][weird-namespaces].


### Usage

 * Opencaching sites have adopted the usage of the `<Parent>` element, as a
   way to attach alternate waypoints to Geocaches. This information is included
   in the **GSAK 1.5** format.

 * Not sure if Geocaching.com uses it too?

 * [c:geo](http://www.cgeo.org/) seems to support a much larger set of the
   extra GSAK attributes than just the `<Parent>` element. See
   [here](https://github.com/cgeo/cgeo/blob/da0d45046baeb45ee3d436f8f55a66dc9530b89a/main/src/cgeo/geocaching/files/GPXParser.java#L761)
   (note that a commit hash is embedded in this permalink; this means that the
   recent versions of c:geo may support even more GSAK extensions).

   - Can someone explain what these extra elements do? Why does c:geo support
     them? Perhaps it would be useful to make use of them in other geocaching
     sites? Perhaps Geocaching.com does include these elements in their GPX
     files?


c:geo Extensions
----------------

### Versions

Only one version so far:

 * **c:geo 1.0**, identified by `http://www.cgeo.org/wptext/1/0` XML namespace,
   see XSD [here][cgeo-1.0-xsd].


### Backward-compatibility issues

As far as we know, only one version has been released, so we don't know if
c:geo will follow [the weird strategy][weird-namespaces] that others did.
However, the `/1/0` suffix in the namespace identifier suggests they might...


### Usage

As far as we know, c:geo uses these attributes internally only. The XSD does
not document the meaning of them, but the `<visited>` element looks quite
promising. Might be useful to support this information in other contexts.


Conclusion
----------

When generating GPX files:

 * **It seems that you should always generate your Geocaching GPX files using
   the combination of *Topografix 1.0* + *Groundspeak 1.0.1*.** It's simply the
   best option, supported by all the apps.

 * Geocaching.com allows users to export *Topografix 1.0* + *Groundspeak 1.0*,
   but none of the Opencaching sites do, and the users don't complain. This
   probably means that *Groundspeak 1.0* namespace is used very rarely, and
   Geocaching.com supports this option just for a handful of users. (Can
   someone confirm this?)

 * It's hard to definitely say which GSAK namespace you should use, if you want
   to attach information about additional waypoints. Opencaching sites use the
   **GSAK 1.5** namespace. C:geo
   [looks for](https://github.com/cgeo/cgeo/blob/da0d45046baeb45ee3d436f8f55a66dc9530b89a/main/src/cgeo/geocaching/files/GPXParser.java#L759)
   GSAK elements in a
   [hardcoded subset](https://github.com/cgeo/cgeo/blob/da0d45046baeb45ee3d436f8f55a66dc9530b89a/main/src/cgeo/geocaching/files/GPXParser.java#L86)
   of GSAK namespaces (they need to extend this subset every time GSAK break
   backward-compatibility by released a new XML namespace).


When parsing GPX files:

 * **You need to support at least the *Topografix 1.0* + *Groundspeak 1.0.1*
   combination.** All sites, and all newer apps can export to this format, so
   your users shouldn't have problems with providing it.

 * You may sometimes encounter *Topografix 1.1* format, but this is probably
   due to some conversion by an external app. These files usually won't contain
   any Groundspeak namespace (except, possibly, the TerraCaching ones, but this
   is not confirmed).

 * You may still encounter *Groundspeak 1.0* format. This is due to the
   fact, that geocaching.com still allows their users to export this format.
   Some users have this format set in their geocaching.com preferences, and
   these users will have their GPX files exported in this format. In other
   words, it seems to be a good idea to be able to import it.

 * GSAK namespaces seem to be generating the most work for everyone. They have
   already released 6 XML namespaces! And it seems that **if you want to
   support GSAK, then you need to parse all of those** (like
   [c:geo does](https://github.com/cgeo/cgeo/blob/da0d45046baeb45ee3d436f8f55a66dc9530b89a/main/src/cgeo/geocaching/files/GPXParser.java#L759)),
   and also, you will be required to update your application once in a while,
   because GSAK authors seem to be happy with changing their format in a
   backward-incompatible way, on a regular basis (probably they believe it's
   backward-compatible, but it isn't, not really).

   You might also try supporting all namespaces with a common
   `http://www.gsak.net/xmlv1/` prefix, and hope that GSAK will keep all of
   them backward compatible. But this hope might be ungrounded, it's impossible
   to guess what versioning-strategy GSAK authors use.


[topografix-1.0-xsd]: http://www.topografix.com/GPX/1/0/gpx.xsd
[topografix-1.1-xsd]: http://www.topografix.com/GPX/1/1/gpx.xsd
[groundspeak-1.0-xsd]: http://static.groundspeak.com/cache/1/0/cache.xsd
[groundspeak-1.0.1-xsd]: http://static.groundspeak.com/cache/1/0/1/cache.xsd
[groundspeak-1.1-xsd]: http://static.groundspeak.com/cache/1/1/cache.xsd
[oc-gpx-extension]: https://github.com/opencaching/gpx-extension
[weird-namespaces]: https://github.com/opencaching/gpx-extension/issues/4
[gsak-1.1-xsd]: http://www.gsak.net/xmlv1/1/gsak.xsd
[gsak-1.2-xsd]: http://www.gsak.net/xmlv1/2/gsak.xsd
[gsak-1.3-xsd]: http://www.gsak.net/xmlv1/3/gsak.xsd
[gsak-1.4-xsd]: http://www.gsak.net/xmlv1/4/gsak.xsd
[gsak-1.5-xsd]: http://www.gsak.net/xmlv1/5/gsak.xsd
[gsak-1.6-xsd]: http://www.gsak.net/xmlv1/6/gsak.xsd
[cgeo-1.0-xsd]: https://raw.githubusercontent.com/cgeo/cgeo/master/main/project/xsd/cgeo.xsd
