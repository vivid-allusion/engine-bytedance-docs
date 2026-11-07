---
title: "Instructions"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/gis-instructions"
---

This article will introduce the basic concepts, SQL statements, and specific usage methods involved in using GIS spatiotemporal analysis functions.

<span id="442319eb"></span>
## Required conditions

Please refer to [Start service](https://docs.byteplus.com/docs/bytehouse/start-gis-service) to confirm the GIS service is enabled first.

<span id="53d9b239"></span>
## Basic concept


* SRID (Spatial Reference Identifier):

   * SRID is a unique identifier used to identify reference systems in geospatial data. Reference systems define how geospatial data is measured and represented on Earth.

   * **The commonly used SRID value is 4326, which is the WGS84 geographic coordinate system.** This is a widely used global reference system, with latitude and longitude expressed in units of measure. Suitable for situations where only rough geospatial data is generally required, without the need for precise measurement and analysis.

   * You can operate on two instances only if they have the same SRID.


<span id="48b2f72a"></span>
### Data types and functions

<span id="7250c099"></span>
#### Data type


* Point: A point data type that can be declared as`Geometry('Point',)`, or`Geometry('Point')`(Default`SRID`Is 0).

* LineString:Line data type, which can be declared as`Geometry('LineString',)`, or`Geometry('LineString')`(Default`SRID`Is 0).

* PolygonThe face data type can be declared as`Geometry('Polygon',)`, or`Geometry('Polygon')`(Default`SRID为`0).


<span id="d3934c17"></span>
#### Function

ByteHouse provides commonly used GIS functions, please refer to the "SQL Reference \- Functions" section below.

<span id="ef76d4d9"></span>
### Table building syntax

If you want to create a GIS\-related table, you need to declare the corresponding geometry column when creating the table.

Common declaration data types include:


* Point data types, such as those declared as`Geometry('Point', 4326)`;

* Line data types, such as those declared as`Geometry('LineString', 4326)`, in which 4326 for SRID Value.Geometry ('Point') defaults to 0 if not filled in.

* Face data type,such as Geometry ('Polygon', 4326)


If you want to use spatial indexes, you need to specify the geometry column as the primary key index in order by.

```SQL
CREATE TABLE IF NOT EXISTS gis_table ON CLUSTER XXX
(
    `id` UInt64,
    `point` Geometry('Point', 4326)
)
    ENGINE = HaMergeTree
ORDER BY point
SETTINGS index_granularity = 8192;
```


<span id="3281466e"></span>
### Visual build table

You can also use this feature in visual table building.


1. Log in to the ByteHouse console and enter **data management** Interface.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/af25da49d8fe4c2c8c9e2f14540275b4~tplv-goo7wpa0wc-image.image) </span>

2. Drop down in the upper left corner and select the successfully created cluster information.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/884310918e4a459185e288510efd8477~tplv-goo7wpa0wc-image.image) </span>

3. Click the ➕ button on the left and select **Create new table**, you can create a new data table by visually creating a table.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4ee8315ec4f94bc094be68e98429f6b9~tplv-goo7wpa0wc-image.image) </span>

4. Fill in the form information according to the needs, and the field type can be selected as `Geometry`.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5d1c2136c84f4cddb0844326a1ccb5ff~tplv-goo7wpa0wc-image.image) </span>

5. Select the `Geometry`type in `Order by key` to speed up queries.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/50c26d2286414e21aebf0d79fb943aff~tplv-goo7wpa0wc-image.image) </span>

6. A created GIS data table is shown below.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f64034086bbf40fb8494863fb4151531~tplv-goo7wpa0wc-image.image) </span>


<span id="fefee339"></span>
## SQL reference

<span id="b45a8eb2"></span>
### Data type

<span id="68e949d4"></span>
#### Point

The way to declare a point type is:`Geometry('Point')`or`Geometry('Point', SRID)`, in which `SRID` Is a `UInt16` The integer of represents the coordinate system corresponding to the geometric column.

Geometry ('Point') belongs to `DataTypeGeometry` Type,`DataTypeGeometry`One is stored internally`DataTypeTuple`Type is used to represent`Point`Data, one`Point`The bottom layer is stored as a`Tuple`, that is (Float64, Float64).

When inserting data, we can insert the two columns of data in other tables into the Point geometry column in the form of (x, y) by inserting into select, or we can insert into the point in the form of string Tuple.

```SQL
CREATE TABLE IF NOT EXISTS test_gis_tmp
(
    `id`  UInt64,
    `lon` Float64,
    `lat` Float64
)
    ENGINE = MergeTree
ORDER BY id
SETTINGS index_granularity = 8192;

insert into test_gis_tmp values (1, 1, 1), (2, 2, 2), (3, 3.1, 3.1); 

CREATE TABLE IF NOT EXISTS test_gis_point
(
    `id` UInt64,
    `p` Geometry('Point', 4326)
)
    ENGINE = MergeTree
ORDER BY id
SETTINGS index_granularity = 8192;

insert into test_gis_point select id, (lon, lat) from test_gis_tmp;
insert into test_gis_point values (4, '(4, 4)'), (5, '(5.5, 5.5)');

select * from test_gis_point order by id;
```


Expected result:

```SQL
1        (1,1)
2        (2,2)
3        (3.1,3.1)
4        (4,4)
5        (5.5,5.5)
```


<span id="97d614b6"></span>
#### LineString

`LineString` Type and `Point`Type usage is similar, the difference is that`LineString`Stored in is the coordinate array.

```SQL
-- LineString
CREATE TABLE IF NOT EXISTS test_gis_linestring_type
(
    `p` Geometry('LineString', 4326)
)
    ENGINE = MergeTree
ORDER BY p
SETTINGS index_granularity = 8192;

insert into test_gis_linestring_type values ([(0,0), (0, 0)]), ('[(2,2), (2,2)]'), (ST_GeomFromText('LINESTRING (3 3, 3 3)'));

select ST_AsText(p) from test_gis_linestring_type order by p;

DROP TABLE IF EXISTS test_gis_linestring_type;
```


<span id="d29d9690"></span>
#### Polygon

Similar to before,`Polygon`Stored in multiple coordinate arrays.

```SQL
CREATE TABLE IF NOT EXISTS test_gis_polygon_type
(
    `p` Geometry('Polygon', 4326)
)
    ENGINE = MergeTree
ORDER BY p
SETTINGS index_granularity = 8192;

insert into test_gis_polygon_type values ([[(0,0), (1,0), (1,1), (0,1), (0,0)]]), ('[[(0,0), (2,0), (2,2), (0,2), (0,0)]]'), (ST_GeomFromText('POLYGON ((0 0, 3 0, 3 3, 0 3, 0 0))'));
```


<span id="8c36fc3f"></span>
### Function

<span id="0e27b47f"></span>
#### ST_GeomFromText/ST_AsText

The ST_GeomFromText (WKT_Geometry) or ST_GeomFromText (WKT_Geometry, SRID) functions are used to convert the geometric text representation string defined by the OGC standard to the geometric data described above.


* Where WKT_Geometry represents a string, for example for Point data can be'POINT (0 0) 'or'POINT (3.1 3.1) ' etc.

* For example, ST_GeomFromText ('POINT (0 0) ') will return a ColumnGeometry column with a ColumnTuple column embedded inside the ColumnGeometry column to store Point data, ST_GeomFromText return value can be directly inserted into the corresponding geometry column in the table.


ST_AsText (GeometryType) Contrary to ST_GeomFromText, it converts geometric data in ck to the string representation of WKT.

```SQL
CREATE TABLE IF NOT EXISTS test_gis_point
(
    `id` UInt64,
    `p` Geometry('Point', 4326)
)
    ENGINE = MergeTree
ORDER BY id
SETTINGS index_granularity = 8192;

insert into test_gis_point values(1, ST_GeomFromText('POINT (0 0)'));
insert into test_gis_point values(2, ST_GeomFromText('POINT (1 1)'));
insert into test_gis_point values(3, ST_GeomFromText('POINT (2 2)'));
insert into test_gis_point values(4, ST_GeomFromText('POINT (3.1 3.1)'));
insert into test_gis_point values(5, ST_GeomFromText('POINT (4 4)', 4326));
insert into test_gis_point values(6, ST_GeomFromText('POINT (5.1 5.1)', 4326));

select ST_AsText(p) from test_gis_point order by id;
```


Expected result:

```SQL
POINT (0 0)
*POINT (1 1)
*POINT (2 2)
*POINT (3.1 3.1)
*POINT (4 4)
*POINT (5.1 5.1)
```


<span id="e21676fc"></span>
#### ST_Distance

ST_Distance (p1, p2) function is used to calculate the distance between two geometries in a Cartesian space and returns a Float64 type.Where p1 and p2 can be constant or non\-constant types.

```SQL
CREATE TABLE IF NOT EXISTS test_gis_point
(
    `id` UInt64,
    `p` Geometry('Point', 4326)
)
    ENGINE = MergeTree
ORDER BY id
SETTINGS index_granularity = 8192;

insert into test_gis_point values(1, ST_GeomFromText('POINT (0 0)'));
insert into test_gis_point values(2, ST_GeomFromText('POINT (1 1)'));
insert into test_gis_point values(3, ST_GeomFromText('POINT (2 2)'));
insert into test_gis_point values(4, ST_GeomFromText('POINT (3 3)'));
insert into test_gis_point values(5, ST_GeomFromText('POINT (4 4)'));

select ST_Distance(p, ST_GeomFromText('POINT (1 1)')) from test_gis_point order by id;

select '--';

select ST_Distance(ST_GeomFromText('POINT (1 1)'), p) from test_gis_point order by id;
```


Expected result:

```SQL
1.4142135623730951
0
1.4142135623730951
2.8284271247461903
4.242640687119285
--
1.4142135623730951
0
1.4142135623730951
2.8284271247461903
4.242640687119285
```


<span id="11b46917"></span>
#### ST_Within

ST_Within (p1, p2) represents whether the geometry p1 is contained by p2, and the return value is a Boolean type, which represents whether it is contained. Currently, the function supports Point/LineString/Polygon types.

As shown in the figure below, each represents the contained relationship between different geometric types.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/52813ed2a71447c0a720e7ff7fbf7365~tplv-goo7wpa0wc-image.image" width="208px" /></div>


```SQL
CREATE TABLE IF NOT EXISTS test_gis_point
(
    `id` UInt64,
    `p` Geometry('Point', 4326)
)
    ENGINE = MergeTree
ORDER BY id
SETTINGS index_granularity = 8192;

insert into test_gis_point values(1, ST_GeomFromText('POINT (1 1)'));
insert into test_gis_point values(2, ST_GeomFromText('POINT (2 2)'));
insert into test_gis_point values(3, ST_GeomFromText('POINT (3 3)'));
insert into test_gis_point values(4, ST_GeomFromText('POINT (4 4)'));
insert into test_gis_point values(5, ST_GeomFromText('POINT (5 5)'));

optimize table test_gis_point final;

select id from test_gis_point where ST_Within(p, ST_GeomFromText('POLYGON ((0 0, 1 0, 1 1, 0 1, 0 0))'));

select '--';

select id from test_gis_point where ST_Within(p, ST_GeomFromText('POLYGON ((0 0, 3 0, 3 3, 0 3, 0 0))'));

select '--';

select id from test_gis_point where ST_Within(p, ST_GeomFromText('POLYGON ((0 0, 5 0, 5 5, 0 5, 0 0))'));
```


Expected result:

```SQL
1
--
1
2
3
--
1
2
3
4
5
```


<span id="053d266f"></span>
#### ST_MultiAddressFilter

The ST_MultiAddressFilter function is used to filter point. Given a central point and multiple radii, it filters out geometric data that lies within the corresponding multiple circles. Here, WKT_Geometry represents a rectangular range in WKT format, which is used to perform primary key filtering with the R\-tree index. Distance denotes the radius of the circles, and (longitude, latitude) represents the coordinates of different circle centers.

The ST_MultiAddressFilter function returns a Boolean value.

The parameters supported by `ST_MultiAddressFilter` are as follows:

```SQL
ST_MultiAddressFilter(point, WKT_Geometry, distance, longitude, latitude)
```


Example:

```SQL
CREATE TABLE test_gis_point
(
    `id` UInt64,
    `p` Geometry('Point', 4326)
)
ENGINE = MergeTree
ORDER BY id
SETTINGS index_granularity = 8192;

insert into test_gis_point values(1, ST_GeomFromText('POINT (1 1)'));
insert into test_gis_point values(2, ST_GeomFromText('POINT (2 1)'));
insert into test_gis_point values(3, ST_GeomFromText('POINT (3 1)'));
insert into test_gis_point values(4, ST_GeomFromText('POINT (4 1)'));
insert into test_gis_point values(5, ST_GeomFromText('POINT (5 1)'));
insert into test_gis_point values(6, ST_GeomFromText('POINT (6 1)'));
insert into test_gis_point values(7, ST_GeomFromText('POINT (7 1)'));
insert into test_gis_point values(8, ST_GeomFromText('POINT (8 1)'));
insert into test_gis_point values(9, ST_GeomFromText('POINT (9 1)'));
insert into test_gis_point values(10, ST_GeomFromText('POINT (10 1)'));

optimize table test_gis_point final;

SELECT p from test_gis_point WHERE ST_MultiAddressFilter(p, ST_GeomFromText('POLYGON ((0 0, 20 0, 20 20, 0 20, 0 0))'), 1., 5., 1.);

select '--';

SELECT p from test_gis_point WHERE ST_MultiAddressFilter(p, ST_GeomFromText('POLYGON ((0 0, 20 0, 20 20, 0 20, 0 0))'), 120000., 5., 1.);


```


Expected result:

```SQL
(5,1)
--
(4,1)
(5,1)
(6,1)
```


<span id="b1fc6e5c"></span>
#### ST_X/ST_Y

ST_X/ST_Y functions are mainly for the Point type, that is, return the x coordinate value and y coordinate value of the Point.

```SQL
CREATE TABLE IF NOT EXISTS test_gis_point
( 
    `id` UInt64,
    `p` Geometry('Point', 4326)
)
    ENGINE = MergeTree
ORDER BY id
SETTINGS index_granularity = 8192;

insert into test_gis_point values(1, ST_GeomFromText('POINT (1 2)'));
insert into test_gis_point values(2, ST_GeomFromText('POINT (2 3)'));
insert into test_gis_point values(3, ST_GeomFromText('POINT (3 4)'));
insert into test_gis_point values(4, ST_GeomFromText('POINT (4 5)'));
insert into test_gis_point values(5, ST_GeomFromText('POINT (5 6)'));

optimize table test_gis_point final;

select ST_X(p), ST_Y(p) from test_gis_point;


```


Expected:

```SQL
1        2
2        3
3        4
4        5
5        6
```


<span id="4d95ae4f"></span>
### R\-tree index

For GIS spatial queries, it is recommended to set the GIS fields to INDEX indexes. When we sort by geometric columns (i.e. order by point), ByteHouse will build an R\-tree index for the table to speed up spatial queries.

R\-tree indices are mark\-level, that is, the smallest bouding box of all geometric data in each mark will constitute an entry in the R\-tree leaf node.

When we configure the R\-tree index for the spatial geometry function, the query will first be filtered by the R\-tree index through the incoming geometry parameters, and then the filtered data will be handed over to the spatial function for actual execution.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/313fe2c0ef054c9dafdd3578feceb24d~tplv-goo7wpa0wc-image.image" width="500px" /></div>


For example, in the following example, the table follows a geometric column`p`Sorting, so the R\-tree index is built on this column, and we also configure the R\-tree index for ST_Within. So when we do `select id from test_gis_point where ST_Within(p, ST_GeomFromText('POLYGON ((0 0, 2 0, 2 2, 0 2, 0 0))'))`When querying, during the primary key index filtering process, ST_Within will extract the p column and `ST_GeomFromText('POLYGON ((0 0, 2 0, 2 2, 0 2, 0 0))')`Constants, first filter whether the data in the p column is related to the R\-tree index`'POLYGON ((0 0, 2 0, 2 2, 0 2, 0 0))'`Intersect, and the filtered data will be handed over to `ST_Within` Do real calculations.

```SQL
CREATE TABLE IF NOT EXISTS test_gis_point
(
    `id` UInt64,
    `p` Geometry('Point', 4326)
)
    ENGINE = MergeTree
ORDER BY p
SETTINGS index_granularity = 1;

insert into test_gis_point values(1, ST_GeomFromText('POINT (1 1)'));
insert into test_gis_point values(2, ST_GeomFromText('POINT (2 2)'));
insert into test_gis_point values(3, ST_GeomFromText('POINT (3 3)'));
insert into test_gis_point values(4, ST_GeomFromText('POINT (4 4)'));
insert into test_gis_point values(5, ST_GeomFromText('POINT (5 5)'));

optimize table test_gis_point final;

select id from test_gis_point where ST_Within(p, ST_GeomFromText('POLYGON ((0 0, 2 0, 2 2, 0 2, 0 0))'));

select '--';

select id from test_gis_point where ST_Within(p, ST_GeomFromText('POLYGON ((0 0, 5 0, 5 5, 0 5, 0 0))'));

```


Expected result:

```SQL
1
2
--
1
2
3
4
5
```
