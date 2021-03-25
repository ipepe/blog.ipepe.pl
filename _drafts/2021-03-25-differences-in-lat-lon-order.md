

lon lat lon lat
Geospatial software has a fundamental inconsistency: which order we put longitude and latitude in. Below, a table of each format and technology's decision, and below that, some explanations.

lon, lat	lat, lon
formats	formats
GeoJSON ref
KML ref
Shapefile ref
WKT ref
WKB ref
geobuf ref
GeoRSS ref
Encoded Polylines (Google) ref
javascript apis	javascript apis
OpenLayers ref
d3 ref
ArcGIS API for JavaScript ref
Mapbox GL JS ref
Leaflet ref
Google Maps API ref
mobile apis	mobile apis
Tangram ES[1]
Google Maps iOS/Android
Apple MapKit
service specifications	service specifications
WFS 1.0.0 [1]
WMS 1.1.1 [1]
WFS 1.1.0 & 2.0.0 [1]
WMS 1.3.0 [1]
misc	misc
OSRM[1]
Redis[1]
A frustrating inconsistency in geospatial (mapping) software is coordinate order. Coordinates are often represented as arrays, like [-87.73, 41.83], instead of objects, like { lng: -87.73, lat: 41.83 }. This leaves it up to the developer to determine whether -87.73 is the longitude or latitude. One choice places a point on Chicago, and the other a location deep in Antarctica.

There's some consensus growing around longitude, latitude order for geospatial formats, but still chaos for libraries and software. It's up to the developer to be aware of this issue and read the requisite documentation, and flip coordinates if necessary to translate between different systems.

FAQ
Which is right?
Neither. This is an opinion with no right answer. Geographical tradition favors lat, lon. Math and software prefer lon, lat.
What about GPX or OSM XML?
Formats that represent lat and lon with separate XML attributes don't enforce any coordinate order, because XML attributes are not ordered.
What about GML?
GML doesn't make any statement about coordinate order: it allows the datum to dictate the order, so some data may be longitude, latitude and other data the reverse.
Why is the cartographic tradition to put latitude first?
There are many theories. The most convincing is that since we were able to judge latitude much earlier than we could judge longitude, we put it first.
What about ISO 6709 - did the ISO standardize on lat, lon?
The ISO standard specifically only applies to form inputs, not storage mechanisms, software or formats.
Do you have a preference?
Yes I do: longitude, latitude.
Why do you always write "lon" instead of "long"?
long is a number type in the C and C++ languages, and likely others. So if you were to write float long; to define a floating-point longitude value, it'll result in a syntax error. So I always use lon, which is not a keyword or built-in type in any language I've encountered.

Sources:
 * <https://macwright.com/lonlat/>