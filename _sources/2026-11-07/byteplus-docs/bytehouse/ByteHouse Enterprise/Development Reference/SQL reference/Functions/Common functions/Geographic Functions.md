---
title: "Geographic Functions"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/geographic-functions"
---

<span id="大圆形距离"></span>
## Great Circle Distance
Use [great-circle distance formula](https://en.wikipedia.org/wiki/Great-circle_distance) to calculate the distance between two points on the Earth's surface.
greatCircleDistance(lon1Deg, lat1Deg, lon2Deg, lat2Deg)
Input Parameters

* `lon1Deg` — Longitude of the first point, unit: degrees, range: `[-180°, 180°]`.
* `lat1Deg` — Latitude of the first point, unit: degrees, range: `[-90°, 90°]`.
* `lon2Deg` — Longitude of the second point, unit: degrees, range: `[-180°, 180°]`.
* `lat2Deg` — Latitude of the second point, unit: degrees, range: `[-90°, 90°]`.

Positive values correspond to north latitude and east longitude, negative values correspond to south latitude and west longitude.
Return Value
The distance between two points on the earth's surface, in meters.
An exception is thrown when the input parameter values exceed the specified range.
Example
SELECT greatCircleDistance(55.755831, 37.617673, -55.755831, -37.617673)
```plaintext
┌─greatCircleDistance(55.755831, 37.617673, -55.755831, -37.617673)─┐
│                                                14132374.194975413 │
└───────────────────────────────────────────────────────────────────┘
```

<span id="pointinellipses"></span>
## pointInEllipses
Checks whether the specified point is contained within at least one specified ellipse. The coordinates in the following are the positions of geometric shapes in the Cartesian coordinate system.
pointInEllipses(x, y, x₀, y₀, a₀, b₀,...,xₙ, yₙ, aₙ, bₙ)
Input Parameters

* `x, y` — Coordinates of a point on a plane.
* `xᵢ, yᵢ` — Coordinates of the center of the i-th ellipse.
* `aᵢ, bᵢ` — Axes of the i-th ellipse in x, y coordinates.

The number of input parameters must be `2+4⋅n`, where `n` represents the number of ellipses.
Return value
If a point is contained within at least one ellipse, return `1`; otherwise, return `0`.
Example
SELECT pointInEllipses(55.755831, 37.617673, 55.755831, 37.617673, 1.0, 2.0)
```plaintext
┌─pointInEllipses(55.755831, 37.617673, 55.755831, 37.617673, 1., 2.)─┐
│                                                                   1 │
└─────────────────────────────────────────────────────────────────────┘
```

<span id="pointinpolygon"></span>
## pointInPolygon
Check if a specified point is contained within a specified polygon.
pointInPolygon((x, y), [(a, b), (c, d) ...], ...)
Input Param

* `(x, y)` — coordinates of a point on the plane. Type of tuple containing two numbers for coordinates.
* `[(a, b), (c, d) ...]` — vertices of the polygon. Type of array. Each vertex is represented by a coordinate pair `(a, b)`. Vertices can be specified in either clockwise or counterclockwise order. The number of vertices should be three or more. Can only be constants meanwhile.
* The function also supports hollowed-out polygons (cut-out parts). If necessary, other parameters of the function can be used to define the polygons that need to be cut out. (The function does not support non-simply-connected polygons.)

Return value
If the coordinate point is inside the polygon range, it returns `1`. Otherwise, it returns `0`. If the coordinate is on the boundary of the polygon, the function may return `1`, or it may return `0`.
Example
SELECT pointInPolygon((3, 5), [(6, 0), (8, 4), (5, 8), (0, 2)]) AS res
```plaintext
┌─res─┐
│   1 │
└─────┘
```

<span id="geohashencode"></span>
## geohashEncode
Encode latitude and longitude into a geohash-string, please refer to [http://geohash.org/](http://geohash.org/), [https://en.wikipedia.org/wiki/Geohash](https://en.wikipedia.org/wiki/Geohash).
geohashEncode(longitude, latitude, [precision])
Enter a value

* longitude - The longitude part of the coordinates to be encoded. Its value should be within the range of `[-180°, 180°]`
* latitude - The latitude part of the coordinates to be encoded. Its value should be within the range of `[-90°, 90°]`
* precision - Optional, the length of the generated geohash-string, default is `12`. Value range is `[1,12]`. Any value smaller than `1` or bigger than `12` will default to `12`.

Return value

* String of coordinate encoding (using modified version of base32 encoding).

Example
SELECT geohashEncode(-5.60302734375, 42.593994140625, 0) AS res
```plaintext
┌─res──────────┐
│ ezs42d000000 │
└──────────────┘
```

<span id="geohashdecode"></span>
## geohashDecode
Decodes any geohash-encoded string into longitude and latitude.
Enter a value

* encoded string - geohash encoded string.

Return value

* (longitude, latitude) - 2-tuple of `Float64` values for longitude and latitude.

Example
SELECT geohashDecode('ezs42') AS res
```plaintext
┌─res─────────────────────────────┐
│ (-5.60302734375,42.60498046875) │
└─────────────────────────────────┘
```

<span id="geotoh3"></span>
## geoToH3
Calculate the H3 index at a specified [Screen resolution](https://uber.github.io/h3/#/documentation/overview/introduction) `(lon, lat)`.
geoToH3(lon, lat, resolution)
Enter a value

* `lon` — Longitude. Float64 Type.
* `lat` — Latitude. Float64 Type.
* `Resolution` — index's screen resolution. Scope: `[0, 15]`. UInt8 type.

Return value

* H3 index value of the hexagon in H3.
* Returns 0 when an exception occurs.

UInt64 type.
Example
SELECT geoToH3(37.79506683, 55.71290588, 15) as h3Index
```plaintext
┌────────────h3Index─┐
│ 644325524701193974 │
└────────────────────┘
```

<span id="geohashesinbox"></span>
## geohashesInBox
Calculate the minimum geohash array that contains the specified latitude and longitude range at a given precision.
Enter a value

* longitude_min - Min longitude. Its value should be within `[-180°, 180°]`
* latitude_min - Min latitude. Its value should be within `[-90°, 90°]`
* longitude_max - Max longitude. Its value should be within `[-180°, 180°]`
* latitude_max - Max latitude. Its value should be within `[-90°, 90°]`
* precision - geohash accuracy. Its value should be a number of type `UInt8` within `[1, Dec]`.

Please note, all coordinate parameters must be either of type `Float32` or `Float64`.
Return value

* Contains an array of geohash strings with specified precision within the specified range. Note, you should not rely on the order of geohashes in the returned array.
* [] - An empty array will be returned when the input min longitude and latitude are Bigger than the max longitude and latitude.

Please note, if the generated array length exceeds 10000, then the function will throw an abnormality.
Example
SELECT geohashesInBox(24.48, 40.56, 24.785, 40.81, 4) AS thasos
```sql
┌─thasos──────────────────────────────────────┐
│ ['sx1q','sx1r','sx32','sx1w','sx1x','sx38'] │
└─────────────────────────────────────────────┘
```
