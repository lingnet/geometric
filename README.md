# Geometric.js
A JavaScript library for doing geometry. [![Build Status](https://travis-ci.org/HarryStevens/geometric.svg?branch=master)](https://travis-ci.org/HarryStevens/geometric)

[<img src="https://raw.githubusercontent.com/HarryStevens/geometric/master/img/angle-thumb.png" />](https://bl.ocks.org/HarryStevens/5fe49df19892c04dfb9883c217571409)
[<img src="https://raw.githubusercontent.com/HarryStevens/geometric/master/img/length-thumb.png" />](https://bl.ocks.org/HarryStevens/c4eddfb97535e8e01643325cb43175ff)
[<img src="https://raw.githubusercontent.com/HarryStevens/geometric/master/img/centroid-thumb.png" />](https://bl.ocks.org/HarryStevens/37287b23b345f394f8276dc87a9c2bc6)

## Installation

### Web browser
In vanilla, a `geometric` global is exported. You can use the latest version from unpkg.
```html
<script src="https://unpkg.com/geometric@2.0.2/build/geometric.js"></script>
<script src="https://unpkg.com/geometric@2.0.2/build/geometric.min.js"></script>
```
If you'd rather host it yourself, download the latest release from the [`build` directory](https://github.com/HarryStevens/geometric/tree/master/build).

### npm

```bash
npm i geometric -S
```
```js
const geometric = require("geometric");
```

## API

Geometric.js uses the geometric primitives <b>points</b>, <b>lines</b>, and <b>polygons</b>.
* [<b>Points</b>](#points) are represented as arrays of two numbers, such as [0, 0].
* [<b>Lines</b>](#lines) are represented as arrays of two points, such as [[0, 0], [1, 0]]. Because they have endpoints, these are technically [line <em>segments</em>](https://www.mhschool.com/math/mathconnects/wa/assets/docs/394_397_wa_gr3_adllsn_onln.pdf), but Geometric.js refers to them as lines for simplicity's sake.
* [<b>Polygons</b>](#polygons) are represented as arrays of vertices, each of which is a point, such as [[0, 0], [1, 0], [1, 1], [0, 1]]. Polygons can be closed – the first and last vertex are the same – or open.
* There are also functions to [calculate relationships](#relationships) between these primitives.

You will also encounter <b>angles</b>, <b>areas</b>, <b>distances</b>, and <b>lengths</b>.
* [<b>Angles</b>](#angles) are represented as numbers, measured in degrees. Geometric.js also provides functions to convert angles from [degrees to radians](#angleToRadians) or [vice versa](#angleToDegrees).
* <b>Areas</b>, <b>distances</b>, and <b>lengths</b> are represented as numbers, measured in pixels.

<hr />

### <a name="points"></a>Points

<a name="pointRotate" href="#pointRotate">#</a> geometric.<b>pointRotate</b>(<em>point</em>, <em>angle</em>[, <em>origin</em>]) · [Source](https://github.com/HarryStevens/geometric/blob/master/src/points/pointRotate.js "Source"), [Example](https://observablehq.com/@harrystevens/geometric-pointrotate "Example")

Returns the coordinates resulting from rotating a <em>point</em> about an origin by an <em>angle</em> in degrees. If <em>origin</em> is not specified, the origin defaults to [0, 0].

<a name="pointTranslate" href="#pointTranslate">#</a> geometric.<b>pointTranslate</b>(<em>point</em>, <em>angle</em>, <em>distance</em>) · [Source](https://github.com/HarryStevens/geometric/blob/master/src/points/pointTranslate.js "Source"), [Example](https://observablehq.com/@harrystevens/geometric-pointtranslate "Example")

Returns the coordinates resulting from translating a <em>point</em> by an <em>angle</em> in degrees and a <em>distance</em>.

<hr />

### <a name="lines"></a>Lines

<a name="lineAngle" href="#lineAngle">#</a> geometric.<b>lineAngle</b>(<em>line</em>) · [Source](https://github.com/HarryStevens/geometric/blob/master/src/lines/lineAngle.js "Source"), [Example](https://observablehq.com/@harrystevens/geometric-lineangle "Example")

Returns the angle of a <em>line</em>, in degrees, with respect to the horizontal axis.

<a name="lineLength" href="#lineLength">#</a> geometric.<b>lineLength</b>(<em>line</em>) · [Source](https://github.com/HarryStevens/geometric/blob/master/src/lines/lineLength.js "Source"), [Example](https://observablehq.com/@harrystevens/geometric-linelength "Example")

Returns the length of a <em>line</em>.

<a name="lineMidpoint" href="#lineMidpoint">#</a> geometric.<b>lineMidpoint</b>(<em>line</em>) · [Source](https://github.com/HarryStevens/geometric/blob/master/src/lines/lineMidpoint.js "Source"), [Example](https://observablehq.com/@harrystevens/geometric-linemidpoint "Example")

Returns the midpoint of a <em>line</em>.

<hr />

### <a name="polygons"></a>Polygons

<a name="polygonArea" href="#polygonArea">#</a> geometric.<b>polygonArea</b>(<em>polygon</em>) · [Source](https://github.com/HarryStevens/geometric/blob/master/src/polygons/polygonArea.js "Source"), [Example](https://observablehq.com/@harrystevens/geometric-polygonarea "Example")

Returns the area of a <em>polygon</em>.

<a name="polygonBounds" href="#polygonBounds">#</a> geometric.<b>polygonBounds</b>(<em>polygon</em>) · [Source](https://github.com/HarryStevens/geometric/blob/master/src/polygons/polygonBounds.js "Source"), [Example](https://observablehq.com/@harrystevens/geometric-polygonbounds "Example")

Returns the bounds of a <em>polygon</em>, ignoring points with invalid values (null, undefined, NaN, Infinity). The returned bounds are represented as an array of two points, where the first point is the top-left corner and the second point is the bottom-right corner. For example:

```js
const rectangle = [[0, 0], [0, 1], [1, 1], [1, 0]];
const bounds = geometric.polygonBounds(rectangle); // [[0, 0], [1, 1]]
```

Returns null if the <em>polygon</em> has fewer than three points.

<a name="polygonCentroid" href="#polygonCentroid">#</a> geometric.<b>polygonCentroid</b>(<em>polygon</em>) · [Source](https://github.com/HarryStevens/geometric/blob/master/src/polygons/polygonCentroid.js "Source"), [Example](https://observablehq.com/@harrystevens/geometric-polygoncentroid-geometric-polygonmean "Example")

Returns the weighted centroid of a <em>polygon</em>. Not to be [confused](https://github.com/Turfjs/turf/issues/334) with a [mean center](#polygonMean).

<a name="polygonHull" href="#polygonHull">#</a> geometric.<b>polygonHull</b>(<em>points</em>) · [Source](https://github.com/HarryStevens/geometric/blob/master/src/polygons/polygonHull.js "Source"), [Example](https://observablehq.com/@harrystevens/geometric-polygonhull "Example")

Returns the [convex hull](https://en.wikipedia.org/wiki/Convex_hull), represented as a polygon, for an array of <em>points</em>. Returns null if the input array has fewer than three points. Uses [Andrew’s monotone chain algorithm](https://en.wikibooks.org/wiki/Algorithm_Implementation/Geometry/Convex_hull/Monotone_chain#JavaScript).

<a name="polygonLength" href="#polygonLength">#</a> geometric.<b>polygonLength</b>(<em>polygon</em>) · [Source](https://github.com/HarryStevens/geometric/blob/master/src/polygons/polygonLength.js "Source"), [Example](https://observablehq.com/@harrystevens/geometric-polygonlength "Example")

Returns the length of a <em>polygon</em>'s perimeter.

<a name="polygonMean" href="#polygonMean">#</a> geometric.<b>polygonMean</b>(<em>polygon</em>) · [Source](https://github.com/HarryStevens/geometric/blob/master/src/polygons/polygonMean.js "Source"), [Example](https://observablehq.com/@harrystevens/geometric-polygoncentroid-geometric-polygonmean "Example")

Returns the arithmetic mean of the vertices of a polygon. Keeps duplicate vertices, resulting in different values for open and closed polygons. Not to be [confused](https://github.com/Turfjs/turf/issues/334) with a [centroid](#polygonCentroid).

<a name="polygonRegular" href="#polygonRegular">#</a> geometric.<b>polygonRegular</b>([<em>sides</em>[, <em>area</em>[, <em>center</em>]]]) · [Source](https://github.com/HarryStevens/geometric/blob/master/src/polygons/polygonRegular.js "Source"), [Example](https://observablehq.com/@harrystevens/geometric-polygonregular "Example")

Returns the vertices of a regular polygon of the specified number of <em>sides</em>, <em>area</em>, and <em>center</em> coordinates. If <em>sides</em> is not specified, deafults to 3. If <em>area</em> is not specified, defaults to 100. If <em>center</em> is not specified, defaults to [0, 0].

<a name="polygonRotate" href="#polygonRotate">#</a> geometric.<b>polygonRotate</b>(<em>polygon</em>, <em>angle</em>[, <em>origin</em>]) · [Source](https://github.com/HarryStevens/geometric/blob/master/src/polygons/polygonRotate.js "Source"), [Example](https://observablehq.com/@harrystevens/geometric-polygonrotate "Example")

Returns the vertices resulting from rotating a <em>polygon</em> about an origin by an <em>angle</em> in degrees. If <em>origin</em> is not specified, the origin defaults to [0, 0].

<a name="polygonScale" href="#polygonScale">#</a> geometric.<b>polygonScale</b>(<em>polygon</em>, <em>scaleFactor</em>[, <em>origin</em>]) · [Source](https://github.com/HarryStevens/geometric/blob/master/src/polygons/polygonScale.js "Source"), [Example](https://observablehq.com/@harrystevens/geometric-polygonscale "Example")

Returns the vertices resulting from scaling a <em>polygon</em> by a <em>scaleFactor</em> (where 1 is the polygon's current size) from an origin point. If <em>origin</em> is not specified, the origin defaults to the polygon's centroid.

<a name="polygonTranslate" href="#polygonTranslate">#</a> geometric.<b>polygonTranslate</b>(<em>polygon</em>, <em>angle</em>, <em>distance</em>) · [Source](https://github.com/HarryStevens/geometric/blob/master/src/polygons/polygonTranslate.js "Source"), [Example](https://observablehq.com/@harrystevens/geometric-polygontranslate "Example")

Returns the vertices resulting from translating a <em>polygon</em> by an <em>angle</em> in degrees and a <em>distance</em>.

<hr />

### <a name="relationships"></a>Relationships

<a name="lineIntersectsLine" href="#lineIntersectsLine">#</a> geometric.<b>lineIntersectsLine</b>(<em>lineA</em>, <em>lineB</em>) · [Source](https://github.com/HarryStevens/geometric/blob/master/src/relationships/lineIntersectsLine.js "Source"), [Example](https://observablehq.com/@harrystevens/geometric-lineintersectsline "Example")

Returns a boolean representing whether <em>lineA</em> intersects <em>lineB</em>.

<a name="lineIntersectsPolygon" href="#lineIntersectsPolygon">#</a> geometric.<b>lineIntersectsPolygon</b>(<em>line</em>, <em>polygon</em>) · [Source](https://github.com/HarryStevens/geometric/blob/master/src/relationships/lineIntersectsPolygon.js "Source"), [Example](https://observablehq.com/@harrystevens/geometric-lineintersectspolygon "Example")

Returns a boolean representing whether a <em>line</em> intersects a <em>polygon</em>.

<a name="pointInPolygon" href="#pointInPolygon">#</a> geometric.<b>pointInPolygon</b>(<em>point</em>, <em>polygon</em>) · [Source](https://github.com/HarryStevens/geometric/blob/master/src/relationships/pointInPolygon.js "Source"), [Example](https://observablehq.com/@harrystevens/geometric-pointinpolygon "Example")

Returns a boolean representing whether a <em>point</em> is inside of a <em>polygon</em>. Uses [ray casting](https://en.wikipedia.org/wiki/Point_in_polygon#Ray_casting_algorithm).

<a name="pointOnPolygon" href="#pointOnPolygon">#</a> geometric.<b>pointOnPolygon</b>(<em>point</em>, <em>polygon</em>) · [Source](https://github.com/HarryStevens/geometric/blob/master/src/relationships/pointOnPolygon.js "Source"), [Example](https://observablehq.com/@harrystevens/geometric-pointonpolygon "Example")

Returns a boolean representing whether a <em>point</em> is located on one of the edges of a <em>polygon</em>.

<a name="pointOnLine" href="#pointOnLine">#</a> geometric.<b>pointOnLine</b>(<em>point</em>, <em>line</em>) · [Source](https://github.com/HarryStevens/geometric/blob/master/src/relationships/pointOnLine.js#L17 "Source"), [Example](https://observablehq.com/@harrystevens/geometric-pointonline-geometric-pointwithline "Example")

Returns a boolean representing whether a <em>point</em> is collinear with a <em>line</em> and is also located on the line segment. See also [pointWithLine](#pointWithLine).

[<img width="150" src="https://raw.githubusercontent.com/HarryStevens/geometric/master/img/point-on-with-line.png" />](https://observablehq.com/d/c463ce4b7cbcd048)

<a name="pointWithLine" href="#pointWithLine">#</a> geometric.<b>pointWithLine</b>(<em>point</em>, <em>line</em>) · [Source](https://github.com/HarryStevens/geometric/blob/master/src/relationships/pointOnLine.js#L21 "Source"), [Example](https://observablehq.com/@harrystevens/geometric-pointonline-geometric-pointwithline "Example")

Returns a boolean representing whether a <em>point</em> is collinear with a <em>line</em>. See also [pointOnLine](#pointOnLine).

<a name="pointLeftofLine" href="#pointLeftofLine">#</a> geometric.<b>pointLeftofLine</b>(<em>point</em>, <em>line</em>) · [Source](https://github.com/HarryStevens/geometric/blob/master/src/relationships/pointOnLine.js#L9 "Source"), [Example](https://observablehq.com/@harrystevens/geometric-pointleftofline-geometric-pointrightofline-g "Example")

Returns a boolean representing whether a <em>point</em> is to the left of a <em>line</em>.

<a name="pointRightofLine" href="#pointRightofLine">#</a> geometric.<b>pointRightofLine</b>(<em>point</em>, <em>line</em>) · [Source](https://github.com/HarryStevens/geometric/blob/master/src/relationships/pointOnLine.js#L13 "Source"), [Example](https://observablehq.com/@harrystevens/geometric-pointleftofline-geometric-pointrightofline-g "Example")

Returns a boolean representing whether a <em>point</em> is to the right of a <em>line</em>.

<a name="polygonInPolygon" href="#polygonInPolygon">#</a> geometric.<b>polygonInPolygon</b>(<em>polygonA</em>, <em>polygonB</em>) · [Source](https://github.com/HarryStevens/geometric/blob/master/src/relationships/polygonInPolygon.js "Source"), [Example](https://observablehq.com/@harrystevens/geometric-polygoninpolygon "Example")

Returns a boolean representing whether <em>polygonA</em> is contained by <em>polygonB</em>.

<a name="polygonIntersectsPolygon" href="#polygonIntersectsPolygon">#</a> geometric.<b>polygonIntersectsPolygon</b>(<em>polygonA</em>, <em>polygonB</em>) · [Source](https://github.com/HarryStevens/geometric/blob/master/src/relationships/polygonIntersectsPolygon.js "Source"), [Example](https://observablehq.com/@harrystevens/geometric-polygonintersectspolygon "Example")

Returns a boolean representing whether <em>polygonA</em> intersects but is not contained by <em>polygonB</em>.

<hr />

### Angles

<a name="angleReflect" href="#angleReflect">#</a> geometric.<b>angleReflect</b>(<em>incidence</em>, <em>surface</em>) · [Source](https://github.com/HarryStevens/geometric/blob/master/src/angles/angleReflect.js "Source"), [Example](https://observablehq.com/@harrystevens/geometric-anglereflect "Example")

Returns the angle of reflection given a starting angle, also known as the angle of <em>incidence</em>, and the angle of the <em>surface</em> off of which it is reflected.

<a name="angleToDegrees" href="#angleToDegrees">#</a> geometric.<b>angleToDegrees</b>(<em>angle</em>) · [Source](https://github.com/HarryStevens/geometric/blob/master/src/angles/angleToDegrees.js "Source")

Returns the result of a converting an <em>angle</em> in radians to the same angle in degrees.

<a name="angleToRadians" href="#angleToRadians">#</a> geometric.<b>angleToRadians</b>(<em>angle</em>) · [Source](https://github.com/HarryStevens/geometric/blob/master/src/angles/angleToRadians.js "Source")

Returns the result of a converting an <em>angle</em> in degrees to the same angle in radians.