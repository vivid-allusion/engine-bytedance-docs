---
title: "Geographic functions"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/docs-geo"
---

<span id="b1e3c2c5"></span>
## Geometric construction functions

<span id="b76b892c"></span>
### ST_AsWKB

Returns the WKB representation of the geometry.

**Syntax**

```SQL
ST_AsWKB(geometryA)
```


**Parameters**

`geometryA` — Geometry Type

**Return Value**

Binary string in WKB format

**Example**

```SQL
SELECT
    ST_AsWKB(ST_GeomFromText('POINT(0 1)')) AS g1,
    ST_AsWKB(ST_GeomFromText('LINESTRING(1 1,0 0, -1 1)')) AS g2,
    ST_AsWKB(ST_GeomFromText('POLYGON((1 1,0 0, -1 1, 1 1))')) AS g3 
```


```SQL
g1─┬─g2──┬─g3────┐
│ �?  │ �?�?��? │ �?�?��?�?�? │
└────┴─────┴───────┘
```


<span id="3daa6102"></span>
### ST_AsText

Returns the WKT representation of the geometry.

**Syntax**

```SQL
ST_AsText(geometryA)
```


**Parameter**

`geometryA` — Geometry type

**Return Value**

Binary string in WKT format

**Example**

```SQL
SELECT
    ST_AsText(ST_GeomFromText('POINT(0 1)')),
    ST_AsText(ST_GeomFromText('LINESTRING(1 1,0 0, -1 1)')),
    ST_AsText(ST_GeomFromText('POLYGON((1 1,0 0, -1 1, 1 1))'))
```


```SQL
g1──────────┬─g2──────────────────────────┬─g3──────────────────────────────┐
│ POINT (0 1) │ LINESTRING (1 1, 0 0, -1 1) │ POLYGON ((1 1, 0 0, -1 1, 1 1)) │
└─────────────┴─────────────────────────────┴─────────────────────────────────┘
```


<span id="c7f2066b"></span>
### ST_GeometryFromText

Constructs a geometry type object using WKT.

**Syntax**

```SQL
ST_GeometryFromText(WKT)
```


**Param**

`WKT`— WKT String

**Return Value**

Geometry Type

**Example**

```SQL
SELECT
    ST_GeomFromText('POINT(0 1)') g1,
    ST_GeomFromText('LINESTRING(1 1,0 0, -1 1)') g2,
    ST_GeomFromText('POLYGON((1 1,0 0, -1 1, 1 1))') g3
```


```SQL
g1────┬─g2───────────────────┬─g3───────────────────────────┐
│ (0,1) │ [(1,1),(0,0),(-1,1)] │ [[(1,1),(0,0),(-1,1),(1,1)]] │
└───────┴──────────────────────┴──────────────────────────────┘
```


<span id="48b91fb3"></span>
### ST_GeomFromBinary

Construct a geometry type object from WKB.

**Syntax**

```SQL
ST_GeomFromBinary(WKB)
```


**Param**

`WKB`— WKB String

**Return Value**

Geometry Type

**Example**

```SQL
SELECT
    ST_AsText(ST_GeomFromWKB(ST_AsWKB(ST_GeomFromText('POINT(0 1)')))) AS g1,
    ST_AsText(ST_GeomFromWKB(ST_AsWKB(ST_GeomFromText('LINESTRING(1 1,0 0, -1 1)')))) AS g2,
    ST_AsText(ST_GeomFromWKB(ST_AsWKB(ST_GeomFromText('POLYGON((1 1,0 0, -1 1, 1 1))')))) AS g3
```


```SQL
g1──────────┬─g2──────────────────────────┬─g3──────────────────────────────┐
│ POINT (0 1) │ LINESTRING (1 1, 0 0, -1 1) │ POLYGON ((1 1, 0 0, -1 1, 1 1)) │
└─────────────┴─────────────────────────────┴─────────────────────────────────┘
```


<span id="661fec5a"></span>
## Spatial Relationship Functions

<span id="0e2809ae"></span>
### ST_Contains

If the geometry `geometryA` completely contains `geometryB` (all points of `geometryB` are in `geometryA` and at least one point is internally in `geometryA`), then return `true`, otherwise return `false`

**Syntax**

```SQL
ST_Contains(geometryA, geometryB)
```


**Param**

`geometryA, geometryB`— Geometry Type

**Return value**

Boolean Value

**Example**

```SQL
SELECT
    ST_Contains(ST_GeomFromText('POLYGON((0 0, 0 10, 10 10, 10 0, 0 0))'), ST_GeomFromText('POINT(5 5)')) AS contains1,
    ST_Contains(ST_GeomFromText('POLYGON((0 0, 0 10, 10 10, 10 0, 0 0))'), ST_GeomFromText('POINT(0 0)')) AS contains2,
    ST_Contains(ST_GeomFromText('POLYGON((0 0, 0 10, 10 10, 10 0, 0 0))'), ST_GeomFromText('POINT(-1 0)')) AS contains3
```


```SQL
┌─contains1─┬─contains2─┬─contains3─┐
│         1 │         0 │         0 │
└───────────┴───────────┴───────────┘
```


<span id="e13b7def"></span>
### ST_ContainsProperly

If the geometric figure `geometryA` strictly contains `geometryB`, that is, all points of `geometryB` are inside `geometryA` (excluding the boundary), then return `true`; otherwise, return `false`.

**Grammar**

```SQL
ST_ContainsProperly(geometryA, geometryB)
```


**Param**

`GeometryA, GeometryB`— Geometric Types

**Return value**

Boolean Value

**Example**

```SQL
SELECT
    ST_ContainsProperly(ST_GeomFromText('POLYGON((0 0, 0 10, 10 10, 10 0, 0 0))'), ST_GeomFromText('GEOMETRYCOLLECTION (POINT(5 5),LINESTRING(1 1,2 2))')) AS containsproperly1,
    ST_ContainsProperly(ST_GeomFromText('POLYGON((0 0, 0 10, 10 10, 10 0, 0 0))'), ST_GeomFromText('GEOMETRYCOLLECTION (POINT(10 10), LINESTRING(0 0, 0 10))')) AS containsproperly2,
    ST_ContainsProperly(ST_GeomFromText('POLYGON((0 0, 0 10, 10 10, 10 0, 0 0))'), ST_GeomFromText('GEOMETRYCOLLECTION (POINT(-1 0),LINESTRING(11 5,12 5))')) AS containsproperly3
```


```SQL
containsproperly1─┬─containsproperly2─┬─containsproperly3─┐
│                 1 │                 0 │                 0 │
└───────────────────┴───────────────────┴───────────────────┘
```


<span id="d5aa40d2"></span>
### ST_Crosses

If the two input geometry objects partially intersect but do not contain each other, then the function returns true.

**Grammar**

```SQL
ST_Crosses(geometryA, geometryB)
```


**Param**

geometryA, geometryB — Geometric types

**Return value**

Boolean Value

**Example**

```SQL
SELECT
    ST_Crosses(ST_GeomFromText('LINESTRING(0 10, 0 -10)'), ST_GeomFromText('LINESTRING(0 0, 1 1)')) AS crosses1,
    ST_Crosses(ST_GeomFromText('LINESTRING(0 10, 0 -10)'), ST_GeomFromText('LINESTRING(-4 0, 1 1)')) AS crosses2,
    ST_Crosses(ST_GeomFromText('POLYGON((0 0, 0 10, 10 10, 10 0, 0 0))'), ST_GeomFromText('GEOMETRYCOLLECTION (POINT(5 5),LINESTRING(1 1,2 2))')) AS crosses3
```


```SQL
─crosses1─┬─crosses2─┬─crosses3─┐
│        0 │        1 │        0 │
└──────────┴──────────┴──────────┘
```


<span id="319b61f6"></span>
### ST_Disjoint

If the geometry objects`geometryA`and `geometryB` do not intersect at all (completely disjoint), then return `true`; otherwise return `false`.

**Syntax**

```SQL
ST_Disjoint(geometryA, geometryB)
```


**Parameter**

`geometryA, geometryB` — Geometry Type

**Return Value**

Boolean Value

**Example**

```SQL
SELECT
    ST_Disjoint(ST_GeomFromText('POINT(5 5)'), ST_GeomFromText('POLYGON((0 0, 0 10, 10 10, 10 0, 0 0))')) AS disjoint1,
    ST_Disjoint(ST_GeomFromText('POINT(0 0)'), ST_GeomFromText('POLYGON((0 0, 0 10, 10 10, 10 0, 0 0))')) AS disjoint2,
    ST_Disjoint(ST_GeomFromText('POINT(-1 0)'), ST_GeomFromText('POLYGON((0 0, 0 10, 10 10, 10 0, 0 0))')) AS disjoint3
```


```SQL
disjoint1─┬─disjoint2─┬─disjoint3─┐
│         0 │         0 │         1 │
└───────────┴───────────┴───────────┘
```


<span id="a87df6a3"></span>
### ST_Equals

If the geometrical objects `geometryA` and `geometryB` are exactly the same in shape and location, then return `true`; otherwise return `false`.

**Syntax**

```SQL
ST_Equals(geometryA, geometryB)
```


**Param**

`geometryA, geometryB`— Geometry Type

**Return Value**

Boolean

**Example**

```SQL
SELECT
    ST_Equals(ST_GeomFromText('LINESTRING(0 0, 1 1)'), ST_GeomFromText('LINESTRING(1 1, 0 0)')) AS quals1,
    ST_Equals(ST_GeomFromText('POLYGON((0 0, 0 10, 10 10, 10 0, 0 0))'), ST_GeomFromText('GEOMETRYCOLLECTION (POLYGON((0 0, 10 0, 10 10, 0 10, 0 0)),LINESTRING(0 2, 0 5))')) AS quals2,
    ST_Equals(ST_GeomFromText('POLYGON((0 0, 0 10, 10 10, 10 0, 0 0))'), ST_GeomFromText('GEOMETRYCOLLECTION (POLYGON((0 0, 10 0, 10 10, 0 10, 0 0)),MULTIPOINT(0 2, 0 5))')) AS quals3
```


```SQL
quals1─┬─quals2─┬─quals3─┐
│      1 │      1 │      1 │
└────────┴────────┴────────┘
```


<span id="b93a6b62"></span>
### ST_Intersects

If the geometric objects `geometryA` and `geometryB` intersect at any part (including boundaries and internal), then return `true`; otherwise, return `false`.

**Syntax**

```SQL
ST_Intersects(geometryA, geometryB)
```


**Param**

`geometryA, geometryB`— Geometry Type

**Return Value**

Boolean Value

**Example**

```SQL
SELECT
    ST_Intersects(ST_GeomFromText('POINT(5 5)'), ST_GeomFromText('POLYGON((0 0, 0 10, 10 10, 10 0, 0 0))')) AS intersects1,
    ST_Intersects(ST_GeomFromText('POINT(0 0)'), ST_GeomFromText('POLYGON((0 0, 0 10, 10 10, 10 0, 0 0))')) AS intersects2,
    ST_Intersects(ST_GeomFromText('POINT(-1 0)'), ST_GeomFromText('POLYGON((0 0, 0 10, 10 10, 10 0, 0 0))')) AS intersects3
```


```SQL
intersects1─┬─intersects2─┬─intersects3─┐
│           1 │           1 │           0 │
└─────────────┴─────────────┴─────────────┘
```


<span id="139206e2"></span>
### ST_Overlaps

If the geometric objects `geometryA` and `geometryB` partially overlap (i.e., they intersect and the result is neither `geometryA` nor `geometryB`), then return `true`; otherwise, return `false`.

**Syntax**

```SQL
ST_Overlaps(geometryA, geometryB)
```


**Parameter**

`geometryA, geometryB`— Geometry Type

**Return Value**

Boolean Value

**Example**

```SQL
SELECT
    ST_Overlaps(ST_GeomFromText('POLYGON((0 0, 0 2, 2 2, 2 0, 0 0))'), ST_GeomFromText('POLYGON((1 1, 1 3, 3 3, 3 1, 1 1))')) AS overlaps1,
    ST_Overlaps(ST_GeomFromText('POLYGON((0 0, 0 10, 10 10, 10 0, 0 0))'), ST_GeomFromText('GEOMETRYCOLLECTION (POINT(5 5),LINESTRING(1 1,2 2))')) AS overlaps2
```


```SQL
┌─overlaps1─┬─overlaps2─┐
│         1 │         0 │
└───────────┴───────────┘
```


<span id="322b74a2"></span>
### ST_Relate

A function used to describe the spatial relationship between two geometric objects. It returns `true` if the relationship between the two geometric objects matches the specified pattern; otherwise, it returns `false`.

**Syntax**

```SQL
ST_Relate(geometryA, geometryB)
ST_Relate(geometryA, geometryB, pattern_matrix)
```


**Param**

`geometryA, geometryB`: geometry type

pattern_matrix: a string for specifying the relational mode

**Return value**

Boolean Value

**Example**

```SQL
SELECT
    ST_Relate(ST_GeomFromText('POINT(0 0)'), ST_GeomFromText('LINESTRING(0 0, 1 1)')) AS relate1,
    ST_Relate(ST_GeomFromText('POINT(0 0)'), ST_GeomFromText('LINESTRING(0 0, 1 1)'), 'F0FFFF*02') AS relate2,
    ST_Relate(ST_GeomFromText('POINT(0 0)'), ST_GeomFromText('LINESTRING(0 0, 1 1)'), 'F0FFF0*02') AS relate3
```


```SQL
┌─relate1───┬─relate2─┬─relate3─┐
│ F0FFFF102 │       1 │       0 │
└───────────┴─────────┴─────────┘
```


<span id="0e90dc5f"></span>
### ST_Touches

If the boundaries of the geometric objects `geometryA` and `geometryB` touch but their interiors do not intersect, then return `true`; otherwise, return `false`.

**Syntax**

```SQL
ST_Touches(geometryA, geometryB)
```


**Parameters**

`geometryA, geometryB` — Geometric types

**Return Value**

Boolean Value

**Example**

```SQL
SELECT
    ST_Touches(ST_GeomFromText('LINESTRING(0 10, 0 -10)'), ST_GeomFromText('LINESTRING(0 0, 1 1)')) AS touches1,
    ST_Touches(ST_GeomFromText('POLYGON((0 0, 0 10, 10 10, 10 0, 0 0))'), ST_GeomFromText('GEOMETRYCOLLECTION (POINT(5 5),LINESTRING(1 1,2 2))')) AS touches2
```


```SQL
─touches1─┬─touches2─┐
│        1 │        0 │
└──────────┴──────────┘
```


<span id="92d54c01"></span>
### ST_Within

If geometric object `geometryA` is completely within geometric object `geometryB` (including boundaries), return `true`; otherwise, return `false`. Full

Key Points:

**Grammar**

```SQL
ST_Within(geometryA, geometryB)
```


**Parameters**

`geometryA, geometryB`— Geometry Types

**Return Value**

Boolean Value

**Examples**

```SQL
SELECT
    ST_Within(ST_GeomFromText('POINT(0 0)'), ST_GeomFromText('POLYGON((0 0, 0 10, 10 10, 10 0, 0 0))')) AS within1,
    ST_Within(ST_GeomFromText('POINT(521513 5377804)', 32631), ST_GeomFromText('POLYGON((521526 5377783, 521481 5377811, 521494 5377832, 521539 5377804, 521526 5377783))', 32631)) AS within2
```


```SQL
┌─within1─┬─within2─┐
│       0 │       1 │
└─────────┴─────────┘
```


<span id="74f6865d"></span>
### ST_DWithin

A function used to determine whether the distance between two geometric objects is within a given threshold. If the shortest distance between two geometric objects is less than or equal to a given distance threshold, return `true`; otherwise, return `false`

**Syntax**

```SQL
ST_DWithin(geometryA, geometryB, distance)
```


**Parameters**

`geometryA, geometryB`— Geometry types

`distance`— Represents the distance threshold

**Return value**

Boolean

**Examples**

```SQL
SELECT
    ST_DWithin(ST_GeomFromText('POINT(1 1)'), ST_GeomFromText('POINT(2 2)'), 2.) AS dwithin1,
    ST_DWithin(ST_GeomFromText('POINT(1 1)'), ST_GeomFromText('POINT(5 5)'), 2.) AS dwithin2
```


```SQL
dwithin1─┬─dwithin2─┐
│        1 │        0 │
└──────────┴──────────┘
```


<span id="b99d802f"></span>
### ST_Covers

If the geometric object `geometryA` completely covers `geometryB` (i.e., `geometryB` is entirely inside `geometryA` and the boundary of `geometryA` can coincide with the boundary of `geometryB`), then return `true`; otherwise, return `false`

**Syntax**

```SQL
ST_Covers(geometryA, geometryB)
```


**Parameters**

`geometryA, geometryB`— Geometry types

**Return values**

Boolean value

**Example**

```SQL
SELECT
    ST_Covers(ST_GeomFromText('POLYGON((0 0, 0 10, 10 10, 10 0, 0 0))'), ST_GeomFromText('LINESTRING(1 10, 9 10, 9 8)')) AS covers1,
    ST_Covers(ST_GeomFromText('POLYGON((0 0, 0 10, 10 10, 10 0, 0 0))'), ST_GeomFromText('POINT(-1 0)')) AS covers2
```


```SQL
┌─covers1─┬─covers2─┐
│       1 │       0 │
└─────────┴─────────┘
```


<span id="1f17381a"></span>
### ST_CoveredBy

If the geometric object `geometryA` is completely covered by the geometric object `geometryB` (i.e., `geometryA` is entirely inside `geometryB` and the boundary of `geometryB` can coincide with the boundary of `geometryA`), then return `true`; otherwise, return `false`.

**Syntax**

```SQL
ST_CoveredBy(geometryA, geometryB)
```


**Parameters**

`geometryA, geometryB` — Geometry types

**Return Value**

Boolean Value

**Example**

```SQL
SELECT
    ST_CoveredBy(ST_GeomFromText('LINESTRING(1 10, 9 10, 9 8)'), ST_GeomFromText('POLYGON((0 0, 0 10, 10 10, 10 0, 0 0))')) AS coveredby1,
    ST_CoveredBy(ST_GeomFromText('POINT(-1 0)'), ST_GeomFromText('POLYGON((0 0, 0 10, 10 10, 10 0, 0 0))')) AS coveredby2
```


```SQL
┌─coveredby1─┬─coveredby2─┐
│          1 │          0 │
└────────────┴────────────┘
```


<span id="794b0c4a"></span>
## Geometry operation function

<span id="3abd6cf1"></span>
### ST_Boundary

Function for obtaining the boundary of geometric objects.

**Syntax**

```SQL
ST_Boundary(geometryA)
```


**Parameters**

`geometryA` — Geometry type

**Return Value**

Returns a geometry object that represents the boundaries of the input geometry object.

**Example**

```SQL
SELECT
    ST_AsText(ST_Boundary(ST_GeomFromText('POINT(0 1)'))) AS boundary01,
    ST_AsText(ST_Boundary(ST_GeomFromText('MULTIPOINT(0 0, 1 1)'))) AS boundary02,
    ST_AsText(ST_Boundary(ST_GeomFromText('LINESTRING(1 1,0 0, -1 1)'))) AS boundary03
```


```SQL
─boundary01───────────────┬─boundary02───────────────┬─boundary03─────────────────┐
│ GEOMETRYCOLLECTION EMPTY │ GEOMETRYCOLLECTION EMPTY │ MULTIPOINT ((1 1), (-1 1)) │
└──────────────────────────┴──────────────────────────┴────────────────────────────┘
```


<span id="b53ceabc"></span>
### ST_Buffer

Function for creating a buffer zone around a geometry object.

**Syntax**

```SQL
ST_Buffer(geometryA, distance)
```


**Parameters**

`geometryA` — Geometry type.

`distance` — Buffer distance, can be positive or negative. Positive indicates expansion outward, negative indicates contraction inward.

**Return Value**

Returns a new geometry object representing the buffer of the input geometry object

**Example**

```SQL
SELECT ST_AsText(ST_Buffer(ST_GeomFromText('POINT(100 90)'), 50.)) AS buffer
```


```SQL
buffer─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┐
│ POLYGON ((150 90, 149.0392640201615 80.24548389919359, 146.19397662556435 70.86582838174552, 141.57348061512727 62.22148834901989, 135.35533905932738 54.64466094067263, 127.77851165098011 48.42651938487274, 119.1341716182545 43.80602337443566, 109.75451610080641 40.960735979838475, 100 40, 90.24548389919359 40.960735979838475, 80.86582838174552 43.80602337443566, 72.2214883490199 48.42651938487273, 64.64466094067262 54.64466094067262, 58.426519384872734 62.22148834901989, 53.80602337443566 70.8658283817455, 50.960735979838475 80.24548389919357, 50 90, 50.960735979838475 99.75451610080641, 53.80602337443566 109.13417161825448, 58.42651938487273 117.7785116509801, 64.64466094067262 125.35533905932738, 72.22148834901989 131.57348061512727, 80.86582838174549 136.19397662556432, 90.24548389919357 139.0392640201615, 99.99999999999999 140, 109.75451610080641 139.0392640201615, 119.1341716182545 136.19397662556435, 127.7785116509801 131.57348061512727, 135.35533905932738 125.35533905932738, 141.57348061512727 117.77851165098011, 146.19397662556432 109.13417161825453, 149.0392640201615 99.75451610080644, 150 90)) │
└────────────────────────────────────────────────────────────────────────────────────────────
```


<span id="ecd9f993"></span>
### ST_Difference

A function used to calculate the difference between two geometry objects.

**Syntax**

```SQL
ST_Difference(geometryA, geometryB)
```


**Parameters**

`geometryA, geometryB` — Geometry type

**Return Value**

Returns a new geometry object representing the parts of `geometryA` that do not overlap with `geometryB`

**Example**

```SQL
SELECT ST_AsText(ST_Difference(ST_GeomFromText('LINESTRING(50 100, 50 200)'), ST_GeomFromText('LINESTRING(50 50, 50 150)'))) AS difference
```


```SQL
┌─difference──────────────────┐
│ LINESTRING (50 150, 50 200) │
└─────────────────────────────┘
```


<span id="74c95db3"></span>
### ST_Envelope

Function to get the minimum bounding rectangle of a geometric object, which is the smallest rectangle that can completely contain the input geometric object.

**Syntax**

```SQL
ST_Envelope(geometryA)
```


**Parameters**

`geometryA`— Geometric type

**Return Value**

Returns a polygon geometry object representing the minimum bounding rectangle of the input geometric object.

**Example**

```SQL
SELECT
    ST_AsText(ST_Envelope(ST_GeomFromText('POINT(521513 5377804)'))) AS envelope_1,
    ST_AsText(ST_Envelope(ST_GeomFromText('LINESTRING(0 2, -1 1,0 0, 0.5 0, 1 0, 2 1, 1 2, 0.5 2, 0 2)'))) AS envelope_2,
    ST_AsText(ST_Envelope(ST_GeomFromText('POLYGON((0 0, 10 0, 10 10, 0 10, 0 0),(2 2, 2 4, 4 4, 4 2, 2 2))'))) AS envelope_3
```


```SQL
┌─envelope_1─────────────┬─envelope_2─────────────────────────────┬─envelope_3──────────────────────────────┐
│ POINT (521513 5377804) │ POLYGON ((-1 0, 2 0, 2 2, -1 2, -1 0)) │ POLYGON ((0 0, 10 0, 10 10, 0 10, 0 0)) │
└────────────────────────┴────────────────────────────────────────┴─────────────────────────────────────────┘
```


<span id="dec4f5a6"></span>
### ST_ExteriorRing

A function for obtaining the outer boundary ring (outer ring) of a polygon geometry object.

**Syntax**

```SQL
ST_ExteriorRing(polygon_geometry)
```


**Parameters**

`Polygon Geometry`— Geometry type

**Return Value**

Returns a linestring geometry object representing the outer boundary ring of a polygon.

**Example**

```SQL
SELECT ST_AsText(ST_ExteriorRing(ST_GeomFromText('POLYGON((52 18,66 23,73 9,48 6,52 18),(59 18,67 18,67 13,59 13,59 18))'))) AS exteriorring
```


```SQL
┌─exteriorring─────────────────────────────────┐
│ LINESTRING (52 18, 66 23, 73 9, 48 6, 52 18) │
└──────────────────────────────────────────────┘
```


<span id="d27abfee"></span>
### ST_Intersection

A function to calculate the intersecting part of two geometry objects.

**Syntax**

```SQL
ST_Intersection(geometryA, geometryB)
```


**Parameter**

`geometryA, geometryB`— Geometry types

**Return Value**

Returns a geometric object representing the intersection of `geometryA` and `geometryB`

**Example**

```SQL
SELECT ST_AsText(ST_Intersection(ST_GeomFromText('LINESTRING(0 10, 0 -10)'), ST_GeomFromText('LINESTRING(0 0, 1 1)'))) AS intersection
```


```SQL
┌─intersection─┐
│ POINT (0 0)  │
└──────────────┘
```


<span id="8d70c784"></span>
### ST_Union

A function to merge two or more geometric objects.

**Syntax**

```SQL
ST_Union(geometryA, geometryB)
```


**Parameter**

`geometryA, geometryB`— Geometry types

**Return value**

Returns a new geometry object merged from the input geometry objects

**Example**

```SQL
SELECT ST_AsText(ST_Union(ST_GeomFromText('POINT(1 2)'), ST_GeomFromText('POINT(1 2)'))) AS union_1
```


```SQL
─union_1─────┐
│ POINT (1 2) │
└─────────────
```


<span id="69b972a1"></span>
### ST_Collect

Used to combine multiple geometry objects into a collection.

**Syntax**

```SQL
ST_Collect(geometryA, geometryB,...)
```


**Param**

Usually returns a `GEOMETRYCOLLECTION` type geometry object

**Return value**

Boolean value

**Example**

```SQL
SELECT ST_AsText(ST_Collect(ST_GeomFromText('POINT(-1 -1)', 4326), ST_GeomFromText('LINESTRING ( 0 0, 0 2 )', 4326), ST_GeomFromText('POLYGON((0 0, 0 10, 0 51, 50 20, 30 20, 7 32, 0 0), (1 1, 1 3, 18 18, 1 1))', 4326))) AS collect
```


```SQL
┌─collect─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┐
│ GEOMETRYCOLLECTION (POINT (-1 -1), LINESTRING (0 0, 0 2), POLYGON ((0 0, 0 10, 0 51, 50 20, 30 20, 7 32, 0 0), (1 1, 1 3, 18 18, 1 1))) │
└─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┘
```


<span id="e2190b18"></span>
### ST_Normalize

Function for normalizing geometric objects

**Syntax**

```SQL
ST_Normalize(geometryA)
```


**Param**

`geometryA`— Geometric Type

**Return value**

Boolean

**Example**

```SQL
SELECT ST_AsText(ST_Normalize(ST_GeomFromText('POLYGON((0 10,0 0,10 0,10 10,0 10),(4 2,2 2,2 4,4 4,4 2),(6 8,8 8,8 6,6 6,6 8))'))) AS normalize
```


```SQL
┌─normalize─────────────────────────────────────────────────────────────────────────────────────┐
│ POLYGON ((0 0, 0 10, 10 10, 10 0, 0 0), (6 6, 8 6, 8 8, 6 8, 6 6), (2 2, 4 2, 4 4, 2 4, 2 2)) │
└───────────────────────────────────────────────────────────────────────────────────────────────┘
```


<span id="51fe1220"></span>
### ST_RemoveRepeatedPoints

A function to remove duplicate vertices from the boundaries of linestrings or polygons.

**Syntax**

```SQL
ST_RemoveRepeatedPoints(geometryA)
```


**Parameters**

`geometryA` — Geometry Type

**Return value**

Returns a new geometry object in which duplicate vertices from the input geometry object have been removed.

**Example**

```SQL
SELECT
    ST_AsText(ST_RemoveRepeatedPoints(ST_GeomFromText('LINESTRING(0 0, 1 1, 1 1, 2 2)'))) AS remove1,
    ST_AsText(ST_RemoveRepeatedPoints(ST_GeomFromText('MULTILINESTRING((0 0, 1 1, 1 1, 2 2, 2 2, 2 2, 2 2, 3 3, 3 3),(5 5, 5 5, 5 5, 4 4, 2 2))'))) AS remove2,
    ST_AsText(ST_RemoveRepeatedPoints(ST_GeomFromText('POLYGON((0 0, 10 0, 10 10, 10 10, 0 10, 0 10, 0 10, 0 0, 0 0, 0 0),(5 5, 5 5, 5 8, 8 8, 8 8, 8 8, 8 5,8 5, 5 5, 5 5, 5 5, 5 5, 5 5))'))) AS remove3
```


```SQL
remove1────────────────────┬─remove2─────────────────────────────────────────────────┬─remove3────────────────────────────────────────────────────────────┐
│ LINESTRING (0 0, 1 1, 2 2) │ MULTILINESTRING ((0 0, 1 1, 2 2, 3 3), (5 5, 4 4, 2 2)) │ POLYGON ((0 0, 10 0, 10 10, 0 10, 0 0), (5 5, 5 8, 8 8, 8 5, 5 5)) │
└────────────────────────────┴─────────────────────────────────────────────────────────┴────────────────────────────────────────────────────────────────────┘
```


<span id="2d064ead"></span>
### ST_Simplify

A function for simplifying geometry objects.

**Syntax**

```SQL
ST_Simplify(geometryA, tolerance)
```


**Param**

`geometryA`— geometry type

`tolerance`: a simplified tolerance used to control the degree of simplification. The higher the value, the higher the degree of simplification.

**Return value**

Returns a simplified geometry object

**Example**

```SQL
SELECT
    ST_AsText(ST_Simplify(ST_GeomFromText('LINESTRING(0 0, 0 10, 0 51, 50 20, 30 20, 7 32)'), 2.)) AS simplify1,
    ST_AsText(ST_Simplify(ST_GeomFromText('POLYGON((0 0, 0 10, 0 51, 50 20, 30 20, 7 32, 0 0), (1 1, 1 3, 18 18, 1 1))'), 20.)) AS simplify2
```


```SQL
─simplify1──────────────────────────────────┬─simplify2───────────────────────────────┐
│ LINESTRING (0 0, 0 51, 50 20, 30 20, 7 32) │ POLYGON ((0 0, 0 51, 50 20, 7 32, 0 0)) │
└────────────────────────────────────────────┴─────────────────────────────────────────┘
```


<span id="4bbd4f43"></span>
### ST_Translate

Function used to translate geometry objects.

**Syntax**

```SQL
ST_Translate(geometryA, x_delta, y_delta)
```


**Param**

`geometryA, geometryB`— Geometry Type

`x_delta`: Translation distance in the X axis direction

`y_delta`: Translation distance in the Y axis direction

**Return value**

Returns a newly translated geometry object

**Example**

```SQL
SELECT
    ST_AsText(ST_Translate(ST_GeomFromText('POINT (0 0)'), 1., -1.)) AS trans1,
    ST_AsText(ST_Translate(ST_GeomFromText('LINESTRING (0 0, 0 1, 1 2)'), 2., -2.)) AS trans2,
    ST_AsText(ST_Translate(ST_GeomFromText('POLYGON ((0 0, 1 0, 1 1, 0 1, 0 0))'), 1., -1.)) AS trans3
```


```SQL
─trans1───────┬─trans2───────────────────────┬─trans3─────────────────────────────────┐
│ POINT (1 -1) │ LINESTRING (2 -2, 2 -1, 3 0) │ POLYGON ((1 -1, 2 -1, 2 0, 1 0, 1 -1)) │
└──────────────┴──────────────────────────────┴────────────────────────────────────────┘
```


<span id="832c79a0"></span>
### ST_Dump

Function for decomposing complex geometry objects (such as `MULTIPOINT`, `MULTILINESTRING`, `MULTIPOLYGON`) into single geometry objects.

**Syntax**

```SQL
ST_Dump(geometryA)
```


**Param**

`geometryA`— Geometry Type

**Return value**

Returns a result set that contains rows, each containing a single geometry object and URL Path

**Example**

```SQL
SELECT
    ST_AsText(col2.1) AS geom,
    col2.2 AS path
FROM
(
    SELECT arrayJoin(col) AS col2
    FROM
    (
        SELECT ST_Dump(ST_GeomFromText('GEOMETRYCOLLECTION (POINT (1 1), LINESTRING (0 0, 1 1), POLYGON ((0 0, 1 1, 1 0, 0 0)), MULTIPOLYGON (((0 0, 1 1, 1 0, 0 0)), ((2 2, 3 3, 3 2, 2 2))), GEOMETRYCOLLECTION (POINT (3 3)))')) AS col
    )
) AS dump
```


```SQL
─geom───────────────────────────┬─path──┐
│ POINT (1 1)                    │ [1]   │
│ LINESTRING (0 0, 1 1)          │ [2]   │
│ POLYGON ((0 0, 1 1, 1 0, 0 0)) │ [3]   │
│ POLYGON ((0 0, 1 1, 1 0, 0 0)) │ [4,1] │
│ POLYGON ((2 2, 3 3, 3 2, 2 2)) │ [4,2] │
│ POINT (3 3)                    │ [5,1] │
└────────────────────────────────┴───────┘
```


<span id="7a6fe5e0"></span>
### ST_Transform

Function used to transform geometry objects from one spatial reference system to another.

**Syntax**

```SQL
ST_Transform(geometryA, target_srid)
ST_Transform(geometryA, from_srid_text, to_srid_text)
```


**Param**

`geometryA`— Geometry Type

`target_srid`: Identifier of the target spatial reference system (SRID)

`from_srid_text,to_srid_text`: String representation of spatial reference system identifiers

**Return value**

Return the geometry object converted to the specified spatial reference system

**Example**

```SQL
SELECT ST_AsText(p),
    ST_SRID(p)
from (
        SELECT ST_Transform(
                ST_GeomFromText('POINT(52.3676 4.9041)', 4326),
                3857
            ) as p
    );
```


```SQL
─ST_AsText(p)────────────────────────────────┬─ST_SRID(p)─┐
│ POINT (5829534.566065834 546589.7188300652) │       3857 │
└─────────────────────────────────────────────┴────────────┘
```


```SQL
SELECT ST_AsText(p),
    ST_SRID(p)
from (
        SELECT ST_Transform(
                ST_GeomFromText('POINT(52.3676 4.9041)'),
                'EPSG:4326',
                'EPSG:3857'
            ) as p
    );
```


```SQL
─ST_AsText(p)────────────────────────────────┬─ST_SRID(p)─┐
│ POINT (5829534.566065834 546589.7188300652) │       3857 │
└─────────────────────────────────────────────┴────────────┘
```


<span id="c240bf11"></span>
## Geometry access function

<span id="2bdcbefa"></span>
### ST_Centroid

Function for calculating the centroid (geometric center) of a geometry object.

**Syntax**

```SQL
ST_CoveredBy(geometryA)
```


**Parameter**

`geometryA`— Geometry type

**Return value**

Returns a point geometry that represents the centroid of the input geometry object

**Example**

```SQL
SELECT
    ST_AsText(ST_Centroid(ST_GeomFromText('POLYGON((0 0, 0 10, 10 10, 10 0, 0 0),(2 2, 2 4, 4 4, 4 2, 2 2))'))) AS centroid1,
    ST_AsText(ST_Centroid(ST_GeomFromText('LINESTRING(0 2, 0 0, 1 0, 1 2)'))) AS centroid2,
    ST_AsText(ST_Centroid(ST_GeomFromText('MULTIPOINT(0 2, 0 0, 1 0, 1 2)'))) AS centroid3
```


```SQL
┌─centroid1───────────────────────────────────┬─centroid2───────┬─centroid3─────┐
│ POINT (5.083333333333333 5.083333333333333) │ POINT (0.5 0.8) │ POINT (0.5 1) │
└─────────────────────────────────────────────┴─────────────────┴───────────────┘
```


<span id="cacd4278"></span>
### ST_ConvexHull

Function for calculating the convex hull of a geometry object, where the convex hull is the smallest convex polygon that contains the given geometry object.

**Syntax**

```SQL
ST_ConvexHull(geometryA)
```


**Param**

`geometryA`— Geometry type

**Return value**

Return a geometry object that represents the convex hull of the input geometry object.

**Example**

```SQL
SELECT
    ST_AsText(ST_ConvexHull(ST_GeomFromText('MULTIPOINT(0 0, 1 1, 2 0)'))) AS convexhull1,
    ST_AsText(ST_ConvexHull(ST_GeomFromText('POLYGON((0 0, 0 2, 2 2, 2 0, 0 0))'))) AS convexhull
```


```SQL
┌─convexhull1────────────────────┬─convexhull──────────────────────────┐
│ POLYGON ((0 0, 1 1, 2 0, 0 0)) │ POLYGON ((0 0, 0 2, 2 2, 2 0, 0 0)) │
└────────────────────────────────┴─────────────────────────────────────┘
```


<span id="a4e79483"></span>
### ST_PointOnSurface

Function to obtain a point on the surface of a geometry object.

**Syntax**

```SQL
ST_PointOnSurface(geometryA)
```


**Param**

`geometryA`— Geometry Type

**Return value**

Return a geometry object that represents a point on the surface of the input geometry object.

**Example**

```SQL
SELECT ST_AsText(ST_PointOnSurface(ST_GeomFromText('POLYGON((0 0, 0 5, 5 5, 5 0, 0 0))'))) AS p
```


```SQL
┌─p───────────────┐
│ POINT (2.5 2.5) │
└─────────────────┘
```


<span id="02c7def4"></span>
### ST_Dimension

Function for obtaining the dimension of geometric objects.

The dimension of a point is 0.

The dimension of a line is 1.

The dimension of a surface (polygon) is 2.

**Syntax**

```SQL
ST_Dimension(geometryA)
```


**Param**

`geometryA`— Geometry Type

**Return value**

Return an integer representing the dimension of the input geometric object.

**Example**

```SQL
SELECT
    ST_Dimension(ST_GeomFromText('POINT(521513 5377804)')) AS dimension1,
    ST_Dimension(ST_GeomFromText('LINESTRING(0 2, -1 1,0 0, 0.5 0, 1 0, 2 1, 1 2, 0.5 2, 0 2)')) AS dimension2,
    ST_Dimension(ST_GeomFromText('POLYGON((0 0, 10 0, 10 10, 0 10, 0 0),(2 2, 2 4, 4 4, 4 2, 2 2))')) AS dimension3
```


```SQL
┌─dimension1─┬─dimension2─┬─dimension3─┐
│          0 │          1 │          2 │
└────────────┴────────────┴────────────┘
```


<span id="b5d8c00f"></span>
### ST_Distance

Function that calculates the shortest distance between two geometric objects.

**Syntax**

```SQL
ST_Distance(geometryA, geometryB)
```


**Parameters**

`geometryA, geometryB` — Geometric types

**Return Value**

Returns a numeric value representing the shortest distance between two geometric objects.

**Example**

```SQL
SELECT
    ST_Distance(ST_GeomFromText('POINT(1 2)'), ST_GeomFromText('POINT(1 2)')) AS distance_1,
    ST_Distance(ST_GeomFromText('POINT(5 0)'), ST_GeomFromText('POINT(10 12)')) AS distance_2
```


```SQL
┌─distance_1─┬─distance_2─┐
│          0 │         13 │
└────────────┴────────────┘
```


<span id="f31c95bb"></span>
### ST_GeometryType

A function to get the type of geometric objects.

**Syntax**

```SQL
ST_GeometryType(geometryA)
```


**Parameters**

`geometryA` — Geometry type

**Return Value**

Returns a string that represents the type of geometric object.

**Example**

```SQL
SELECT
    ST_GeometryType(ST_GeomFromText('POINT(521513 5377804)')) AS geom_type_1,
    ST_GeometryType(ST_GeomFromText('LINESTRING(0 2, -1 1,0 0, 0.5 0, 1 0, 2 1, 1 2, 0.5 2, 0 2)')) AS geom_type_2,
    ST_GeometryType(ST_GeomFromText('POLYGON((0 0, 10 0, 10 10, 0 10, 0 0),(2 2, 2 4, 4 4, 4 2, 2 2))')) AS geom_type_3
```


```SQL
┌─geom_type_1─┬─geom_type_2─┬─geom_type_3─┐
│ Point       │ LineString  │ Polygon     │
└─────────────┴─────────────┴─────────────┘
```


<span id="4d42273d"></span>
### ST_IsClosed

A function to determine if a geometric object is closed.

For a line string (`LINESTRING`), if the start and end points are the same, it is considered closed.

For polygons (`POLYGON`), their boundaries must form a continuous and closed loop.

**Syntax**

```SQL
ST_IsClosed(geometryA)
```


**Parameters**

`geometryA` — Geometry type

**Return value**

If the geometry object is closed, then return `true`; otherwise, return `false`.

**Examples**

```SQL
SELECT
    ST_IsRing(geom),
    ST_IsClosed(geom),
    ST_IsSimple(geom)
FROM
(
    SELECT ST_GeomFromText('LINESTRING(0 0, 0 1, 1 0, 1 1, 0 0)') AS geom
) AS foo
```


```SQL
─ST_IsRing(geom)─┬─ST_IsClosed(geom)─┬─ST_IsSimple(geom)─┐
│               0 │                 1 │                 0 │
└─────────────────┴───────────────────┴───────────────────┘
```


<span id="b4807762"></span>
### ST_IsSimple

Function for determining if a geometry object is simple.

For linestrings (`LINESTRING`), simplicity means that it does not intersect itself (except possibly at the starting and ending points).

For a polygon (`POLYGON`), simplicity means that its boundaries do not intersect with each other and there are no holes inside.

**Syntax**

```SQL
ST_IsSimple(geometryA)
```


**Parameters**

`geometryA` — Geometry type

**Return value**

If the geometry object is simple, return `true`; otherwise, return `false`

**Example**

```SQL
SELECT
    ST_IsRing(geom),
    ST_IsClosed(geom),
    ST_IsSimple(geom)
FROM
(
    SELECT ST_GeomFromText('LINESTRING(0 0, 0 1, 1 0, 1 1, 0 0)') AS geom
) AS foo
```


```SQL
─ST_IsRing(geom)─┬─ST_IsClosed(geom)─┬─ST_IsSimple(geom)─┐
│               0 │                 1 │                 0 │
└─────────────────┴───────────────────┴───────────────────┘
```


<span id="c025d8da"></span>
### ST_IsRing

This function determines if a linestring forms a ring. The criteria for a ring not only require the start and end points to coincide but also to not have self\-intersections.

**Syntax**

```SQL
ST_IsRing(geometryA)
```


**Parameter**

`geometryA`— Geometry type

**Return value**

If the input linestring geometry forms a loop (i.e., the start point and the endpoint are the same and it does not self\-intersect), return `true`; otherwise, return `false`.

**Example**

```SQL
SELECT
    ST_IsRing(geom),
    ST_IsClosed(geom),
    ST_IsSimple(geom)
FROM
(
    SELECT ST_GeomFromText('LINESTRING(0 0, 0 1, 1 0, 1 1, 0 0)') AS geom
) AS foo
```


```SQL
─ST_IsRing(geom)─┬─ST_IsClosed(geom)─┬─ST_IsSimple(geom)─┐
│               0 │                 1 │                 0 │
└─────────────────┴───────────────────┴───────────────────┘
```


<span id="d36fcfa1"></span>
### ST_IsValid

This function is used to determine whether a geometry object is valid based on a series of spatial rules and constraints, such as polygons must not self\-intersect and the vertex order of linestrings must be logical.

**Syntax**

```SQL
ST_IsValid(geometryA)
```


**Parameter**

`geometryA`— Geometry type

**Return Value**

If the geometry object is valid in space, return `true`; otherwise, return `false`.

**Example**

```SQL
SELECT
    'valid_1',
    ST_IsValid(ST_GeomFromText('LINESTRING(0 0, 1 1)')) AS good_line,
    ST_IsValid(ST_GeomFromText('POLYGON((0 0, 1 1, 1 2, 1 1, 0 0))')) AS bad_poly
```


```SQL
─'valid_1'─┬─good_line─┬─bad_poly─┐
│ valid_1   │         1 │        0 │
└───────────┴───────────┴──────────┘
```


<span id="0b49cb9e"></span>
### ST_Length

Function for calculating the length of a linestring or the perimeter of a polygon.

For linestrings, directly calculate the length of the linestring.

For polygons, calculate the length of its perimeter.

**Syntax**

```SQL
ST_Length(geometryA)
```


**Parameters**

`geometryA` — Geometry type

**Return Value**

Returns a numerical value representing the length of the input geometry object

**Example**

```SQL
SELECT ST_Length(ST_Transform(ST_GeomFromText('LINESTRING(-72.1260 42.45, -72.1240 42.45666, -72.123 42.1546)', 4326), 3857)) len;
```


```SQL
┌───────────────len─┐
│ 46495.61309808517 │
└───────────────────┘
```


<span id="bd48c2ab"></span>
### ST_Area

Function for calculating the area of a polygon geometry object. The calculated area is based on the spatial reference system and coordinate units of the polygon

**Syntax**

```SQL
ST_Area(geometryA)
```


**Parameters**

`geometryA` — Geometry Type

**Return Value**

Returns a numerical value representing the area of the input polygon geometry object

**Example**

```SQL
SELECT ST_Area(geom) AS sqft
FROM
(
    SELECT ST_GeomFromText('POLYGON((743238 2967416,743238 2967450, 743265 2967450,743265.625 2967416,743238 2967416))', 2249) AS geom
) AS subquery
```


```SQL
┌────sqft─┐
│ 928.625 │
└─────────┘
```


<span id="2c174ff7"></span>
### ST_NumPoints

Function for obtaining the number of vertices in linestrings or polygons.

For linestrings, it returns the number of points contained.

For polygons, it returns the number of points on the boundary.

**Syntax**

```SQL
ST_NumPoints(geometryA)
```


**Parameters**

`geometryA`— Geometry Type

**Return Value**

Returns an integer representing the number of vertices in the input geometry object.

**Example**

```SQL
SELECT
    ST_NumPoints(ST_GeomFromText('POINT(521513 5377804)')) AS numpoints_1,
    ST_NumPoints(ST_GeomFromText('LINESTRING(0 2, -1 1,0 0, 0.5 0, 1 0, 2 1, 1 2, 0.5 2, 0 2)')) AS numpoints_2
```


```SQL
┌─numpoints_1─┬─numpoints_2─┐
│           1 │           9 │
└─────────────┴─────────────┘
```


<span id="e528955e"></span>
### ST_SetSRID

A function for setting the Spatial Reference Identifier (SRID) for geometry objects.

**Syntax**

```SQL
ST_SetSRID(geometryA, srid)
```


**Parameters**

`geometryA`— Geometry type

`srid`— The specified spatial reference identifier, an integer

**Return Value**

Returns a new geometry object with the specified SRID

**Example**

```SQL
SELECT ST_SRID(ST_SetSRID(ST_GeomFromText('POINT(521513 5377804)'), 3986)) AS set_srid
```


```SQL
─set_srid─┐
│     3986 │
└──────────┘
```


<span id="cc45b87a"></span>
### ST_SRID

Function for obtaining the Spatial Reference Identifier (SRID) of a geometric object.

**Syntax**

```SQL
ST_SRID(geometryA)
```


**Parameters**

`geometryA` — Geometric type

**Return Value**

Returns an integer representing the SRID of the input geometry object.

**Example**

```SQL
SELECT ST_SRID(ST_GeomFromText('POINT(521513 5377804)', 4326)) AS srid
```


```SQL
─srid─┐
│ 4326 │
└──────
```


<span id="a902ef1c"></span>
### ST_X

Function for obtaining the X coordinate value of a point geometry object.

**Grammar**

```SQL
ST_X(geometryA)
```


**Param**

`geometryA`— Geometry Type

**Return value**

Returns a numerical value representing the X coordinate of the point geometry object

**Example**

```SQL
SELECT
    ST_X(ST_GeomFromText('POINT(521513 5377804)')) AS x,
    ST_Y(ST_GeomFromText('POINT(521513 5377804)')) AS y
```


```SQL
┌──────x─┬───────y─┐
│ 521513 │ 5377804 │
└────────┴─────────┘
```


<span id="3e8de743"></span>
### ST_Y

Function used to obtain the Y coordinate value of a point geometry object.

**Grammar**

```SQL
ST_Y(geometryA)
```


**Param**

`geometryA`— Geometry Type

**Return value**

Returns a numerical value representing the Y\-coordinate of the point geometry object

**Example**

```SQL
SELECT
    ST_X(ST_GeomFromText('POINT(521513 5377804)')) AS x,
    ST_Y(ST_GeomFromText('POINT(521513 5377804)')) AS y
```


```SQL
┌──────x─┬───────y─┐
│ 521513 │ 5377804 │
└────────┴─────────┘
```


<span id="1458c516"></span>
### ST_XMIN

Function for obtaining the minimum coordinate value of a geometry object in the X\-axis direction.

**Syntax**

```SQL
ST_XMIN(geometryA)
```


**Param**

`geometryA`— Geometry Type

**Return value**

Returns a numerical value representing the minimum coordinate of a geometric object on the X\-axis

**Example**

```SQL
SELECT
    ST_XMIN(p),
    ST_XMAX(p),
    ST_YMIN(p),
    ST_YMAX(p)
FROM
(
    SELECT ST_GeomFromText('POLYGON((-5 -8, 10 0, 10 15, 0 15, -5 -8),(-6 2, 2 40, 4 40, 4 2, -6 2))') AS p
) AS t
```


```SQL
┌─ST_XMIN(p)─┬─ST_XMAX(p)─┬─ST_YMIN(p)─┬─ST_YMAX(p)─┐
│         -5 │         10 │         -8 │         15 │
└────────────┴────────────┴────────────┴────────────
```


<span id="a784057b"></span>
### ST_XMAX

Function to obtain the maximum coordinate value of a geometric object on the X\-axis.

**Syntax**

```SQL
ST_XMAX(geometryA)
```


**Param**

`geometryA`— Geometry Type

**Return value**

Returns a numerical value representing the maximum coordinate of a geometric object on the X\-axis

**Example**

```SQL
SELECT
    ST_XMIN(p),
    ST_XMAX(p),
    ST_YMIN(p),
    ST_YMAX(p)
FROM
(
    SELECT ST_GeomFromText('POLYGON((-5 -8, 10 0, 10 15, 0 15, -5 -8),(-6 2, 2 40, 4 40, 4 2, -6 2))') AS p
) AS t
```


```SQL
┌─ST_XMIN(p)─┬─ST_XMAX(p)─┬─ST_YMIN(p)─┬─ST_YMAX(p)─┐
│         -5 │         10 │         -8 │         15 │
└────────────┴────────────┴────────────┴────────────
```


<span id="29d32883"></span>
### ST_YMIN

Function to obtain the minimum Y\-axis coordinate value of a geometric object.

**Syntax**

```SQL
ST_YMIN(geometryA)
```


**Parameters**

`geometryA` — Geometry Type

**Return Value**

Returns a numerical value representing the minimum Y\-axis coordinate of a geometric object.

**Example**

```SQL
SELECT
    ST_XMIN(p),
    ST_XMAX(p),
    ST_YMIN(p),
    ST_YMAX(p)
FROM
(
    SELECT ST_GeomFromText('POLYGON((-5 -8, 10 0, 10 15, 0 15, -5 -8),(-6 2, 2 40, 4 40, 4 2, -6 2))') AS p
) AS t
```


```SQL
┌─ST_XMIN(p)─┬─ST_XMAX(p)─┬─ST_YMIN(p)─┬─ST_YMAX(p)─┐
│         -5 │         10 │         -8 │         15 │
└────────────┴────────────┴────────────┴────────────
```


<span id="a0567e59"></span>
### ST_YMAX

Function to obtain the maximum Y\-axis coordinate value of a geometric object.

**Syntax**

```SQL
ST_YMAX(geometryA)
```


**Param**

`geometryA`— Geometry Type

**Return value**

Returns a numerical value representing the maximum coordinates of the geometry object on the Y axis

**Example**

```SQL
SELECT
    ST_XMIN(p),
    ST_XMAX(p),
    ST_YMIN(p),
    ST_YMAX(p)
FROM
(
    SELECT ST_GeomFromText('POLYGON((-5 -8, 10 0, 10 15, 0 15, -5 -8),(-6 2, 2 40, 4 40, 4 2, -6 2))') AS p
) AS t
```


```SQL
┌─ST_XMIN(p)─┬─ST_XMAX(p)─┬─ST_YMIN(p)─┬─ST_YMAX(p)─┐
│         -5 │         10 │         -8 │         15 │
└────────────┴────────────┴────────────┴────────────
```
