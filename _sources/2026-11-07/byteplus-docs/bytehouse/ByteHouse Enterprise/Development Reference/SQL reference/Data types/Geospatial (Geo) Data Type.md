---
title: "Geospatial (Geo) Data Type"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/geospatial-geo-data-type"
---

<span id="ca49ee08"></span>
## Point
`Point` is represented by its X and Y coordinates, stored as Tuple(Float64, Float64).
**For example**
Search:
```SQL
CREATE TABLE geo_point (p Point) ENGINE = Memory();
INSERT INTO geo_point VALUES((10, 10));
SELECT p, toTypeName(p) FROM geo_point;
```

As a result:
```Plain
┌─p───┬─toTypeName(p)─┐
│ (10,10)│ Point          │ 
└─────┴─────────┘
```

<span id="2de3d792"></span>
## Ring
`Ring` is a simple polygon without holes, represented as an array of points: Array(Point).
**Example**
Search:
```SQL
CREATE TABLE geo_ring (r Ring) ENGINE = Memory();
INSERT INTO geo_ring VALUES([(0, 0), (10, 0), (10, 10), (0, 10)]);
SELECT r, toTypeName(r) FROM geo_ring;
```

Outcome:
```Plain
┌─r─────────────────────────────┬─toTypeName(r)─┐
│ [(0,0),(10,0),(10,10),(0,10)] │ Ring          │
└───────────────────────────────┴───────────────┘
```

<span id="f89cbcd8"></span>
## Polygon
`Polygon` is a polygon with holes, stored as: Array(Ring). The first element of the external array is the exterior of the polygon, and all subsequent elements are holes.
**Example**
This is a polygon with one hole:
```SQL
CREATE TABLE geo_polygon (pg Polygon) ENGINE = Memory();
INSERT INTO geo_polygon VALUES([[(20, 20), (50, 20), (50, 50), (20, 50)], [(30, 30), (50, 50), (50, 30)]]);
SELECT pg, toTypeName(pg) FROM geo_polygon;
```

Result:
```Plain
┌─pg────────────────────────────────────────────────────────────┬─toTypeName(pg)─┐
│ [[(20,20),(50,20),(50,50),(20,50)],[(30,30),(50,50),(50,30)]] │ Polygon        │
└───────────────────────────────────────────────────────────────┴────────────────┘
```

<span id="36731430"></span>
## MultiPolygon
`MultiPolygon` consists of multiple polygons, stored in the form of an array of polygons: Array(Polygon).
**Example**
This polygon is composed of two independent polygons—The first polygon does not have a hole, and the second polygon has one hole:
```SQL
CREATE TABLE geo_multipolygon (mpg MultiPolygon) ENGINE = Memory();
INSERT INTO geo_multipolygon VALUES([[[(0, 0), (10, 0), (10, 10), (0, 10)]], [[(20, 20), (50, 20), (50, 50), (20, 50)],[(30, 30), (50, 50), (50, 30)]]]);
SELECT mpg, toTypeName(mpg) FROM geo_multipolygon;
```

As a result:
```Plain
┌─mpg─────────────────────────────────────────────────────────────────────────────────────────────┬─toTypeName(mpg)─┐
│ [[[(0,0),(10,0),(10,10),(0,10)]],[[(20,20),(50,20),(50,50),(20,50)],[(30,30),(50,50),(50,30)]]] │ MultiPolygon    │
└─────────────────────────────────────────────────────────────────────────────────────────────────┴─────────────────┘
```
