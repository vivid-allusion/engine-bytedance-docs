---
title: "GIS spatiotemporal analysis"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/gis-spatiotemporal-analysis"
---

In the digital era, geospatial analysis has become a crucial tool for aiding businesses in market strategy insights. Whether it is accurate advertising or optimizing the efficiency of e\-commerce logistics, it is indispensable to search, analyze, and visually process geospatial data for better business decision\-making.

With the expansion of the OLAP market, such as real\-time analysis reports, geospatial analysis has also been promoted as a new value\-added feature by several major mainstream OLAP products in the industry. OLAP+GIS capabilities not only meet the basic needs of user geospatial data analysis but also satisfy high\-performance query needs in scenarios with large data volumes and high timeliness requirements. As an OLAP engine launched by BytePlus, ByteHouse has also developed high\-performance geospatial analysis GIS capabilities, providing high\-performance geospatial data analysis services for scenarios such as location insights and user segmentation.

<span id="66a12cfc"></span>
### General concept

SRID (Spatial Reference Identifier):


* SRID is a unique identity identifier used to identify a reference system in geospatial data. The reference system defines how geospatial data is measured and represented on Earth.

* The commonly used SRID value 4326, which is the WGS84 geographic coordinate system. This is a widely used global reference system, where latitude and longitude are represented in metric units. Suitable for situations where only a rough location of geospatial data is needed, without the need for accurate measurements and analysis.

* Spatial operations can only be performed between two instances if they share the same SRID.


<span id="cff30151"></span>
### Data type

The GIS Function contains geometric types such as points, lines, polygons, the spatial relationship between geometries, and the surrounding ecology. To comply with the [Open Geospatial Consortium](https://en.wikipedia.org/wiki/Open_Geospatial_Consortium) standards and satisfy user needs, the Bytehouse GIS module includes seven geometric types: Point, LineString, Polygon, MultiPoint, MultiLineString, MultiPolygon, GeometryCollection.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/61cb9e1bb90f4e36829258187f16627e~tplv-goo7wpa0wc-image.image" width="1280px" /></div>



* Point: point data type, which can be declared as Geometry('Point',) or Geometry('Point') (the default SRID is 0).

* LineString: line data type, which can be declared as Geometry('LineString',) or Geometry('LineString') (the default SRID is 0).

* Polygon: polygon data type, which can be declared as Geometry('Polygon',) or Geometry('Polygon') (the default SRID is 0).

* MultiPoint: A multipoint data type that can be declared as Geometry('MultiPoint',) or Geometry('MultiPoint') (default SRID is 0).

* MultiLineString: A multilinestring data type that can be declared as Geometry('MultiLineString',) or Geometry('MultiLineString') (default SRID is 0).

* MultiPolygon: A multipolygon data type that can be declared as Geometry('MultiPolygon',) or Geometry('MultiPolygon') (default SRID is 0).

* GeometryCollection: A geometry collection data type that can be declared as Geometry('GeometryCollection',) or Geometry('GeometryCollection') (default SRID is 0).


<span id="979a2962"></span>
### Table creation and insertion

If you want to create a GIS\-related table, you need to declare the corresponding geometry column during table creation.

Commonly declared data types include:


* Point data type, such as declared `Geometry('Point', 4326)`, where 4326 is the SRID Value, if not specified, Geometry('Point') defaults to 0

* Line data type, such as declared `Geometry('LineString', 4326)`

* Polygon data type, such as Geometry('Polygon', 4326)


If you want to utilize spatial indexes, you need to specify the geometry column as the primary index in the order by.

<span id="f9514590"></span>
#### Point type

```SQL
CREATE TABLE IF NOT EXISTS test_gis_point_type
(
    `p` Geometry('Point', 4326)
)
    ENGINE = CnchMergeTree
ORDER BY p
SETTINGS index_granularity = 8192;

insert into test_gis_point_type values ((0,0)), ('(1,1)'), (ST_GeomFromText('POINT (2 2)'));

select ST_AsText(p) from test_gis_point_type order by p;
```


<span id="0c2a61a7"></span>
#### LineString type

```SQL
CREATE TABLE IF NOT EXISTS test_gis_linestring_type
(
    `p` Geometry('LineString', 4326)
)
    ENGINE = CnchMergeTree
ORDER BY p
SETTINGS index_granularity = 8192;

insert into test_gis_linestring_type values ([(0,0), (0, 0)]), ('[(2,2), (2,2)]'), (ST_GeomFromText('LINESTRING (3 3, 3 3)'));

select ST_AsText(p) from test_gis_linestring_type order by p;
```


<span id="aedca198"></span>
#### Polygon type

```SQL
CREATE TABLE IF NOT EXISTS test_gis_polygon_type
(
    `p` Geometry('Polygon', 4326)
)
    ENGINE = CnchMergeTree
ORDER BY p
SETTINGS index_granularity = 8192;

insert into test_gis_polygon_type values ([[(0,0), (1,0), (1,1), (0,1), (0,0)]]), ('[[(0,0), (2,0), (2,2), (0,2), (0,0)]]'), (ST_GeomFromText('POLYGON ((0 0, 3 0, 3 3, 0 3, 0 0))'));

select ST_AsText(p) from test_gis_polygon_type order by p;
```


<span id="c9e8523f"></span>
#### MultiPoint type

```SQL
CREATE TABLE IF NOT EXISTS test_gis_multipoint_type
(
    `p` Geometry('MultiPoint', 4326)
)
    ENGINE = CnchMergeTree
ORDER BY p
SETTINGS index_granularity = 8192;

insert into test_gis_multipoint_type values ([(0,0), (0,0)]), ('[(2,2), (2,2)]'), (ST_GeomFromText('MULTIPOINT ((3 3), (3 3))'));

select ST_AsText(p) from test_gis_multipoint_type order by p;
```


<span id="4bb15b19"></span>
#### MultiLineString type

```SQL
CREATE TABLE IF NOT EXISTS test_gis_multilinestring_type
(
    `p` Geometry('MultiLineString', 4326)
)
    ENGINE = CnchMergeTree
ORDER BY p
SETTINGS index_granularity = 8192;

insert into test_gis_multilinestring_type values ([[(0,0), (0,0)], [(0,0), (0,0)]]), ('[[(1, 1), (1, 1)], [(1, 1), (1, 1)]]'), (ST_GeomFromText('MULTILINESTRING ((0 0, 1 1), (2 2, 3 3))'));
 
select ST_AsText(p) from test_gis_multilinestring_type order by p;
```


<span id="531fd51e"></span>
#### MultiPolygon type

```SQL
CREATE TABLE IF NOT EXISTS test_gis_multipolygon_type
(
    `p` Geometry('MultiPolygon', 4326)
)
    ENGINE = CnchMergeTree
ORDER BY p
SETTINGS index_granularity = 8192;

insert into test_gis_multipolygon_type values ([[[(0,0), (1,0), (1,1), (0,1), (0,0)]], [[(0,0), (2,0), (2,2), (0,2), (0,0)]]]), ('[[[(0,0), (1,0), (1,1), (0,1), (0,0)]], [[(0,0), (2,0), (2,2), (0,2), (0,0)]]]'), (ST_GeomFromText('MULTIPOLYGON (((1 1, 1 3, 3 3, 3 1, 1 1)), ((4 3, 6 3, 6 1, 4 1, 4 3)))')), (ST_GeomFromText('MULTIPOLYGON (((0 0, 3 0, 3 3, 0 3, 0 0)))'));
 
select ST_AsText(p) from test_gis_multipolygon_type order by p;
```


<span id="79bad598"></span>
#### GeometryCollection type

```SQL
CREATE TABLE IF NOT EXISTS test_gis_geometrycollection_type
(
    `p` Geometry('GeometryCollection', 4326)
)
    ENGINE = CnchMergeTree
ORDER BY p
SETTINGS index_granularity = 8192;

insert into test_gis_geometrycollection_type values (ST_GeomFromText('GEOMETRYCOLLECTION (MULTIPOINT((0 0), (1 1)), POINT(3 4), LINESTRING(2 3, 3 4))')), (ST_GeomFromText('GEOMETRYCOLLECTION (MULTIPOINT((2 2), (3 3)), POINT(5 6), LINESTRING(5 3, 3 4))')), (ST_GeomFromText('GEOMETRYCOLLECTION (MULTIPOINT((-1 -1), (1 1)), POINT(10 10), LINESTRING(20 30, 30 40))'));
 
select ST_AsText(p) from test_gis_geometrycollection_type order by p;
```


<span id="5bc638fc"></span>
### Spatial function

Please refer to Function \- [Geographic functions](https://docs.byteplus.com/docs/bytehouse/docs-geo).
