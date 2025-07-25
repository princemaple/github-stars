---
project: geo
stars: 657
description: A collection of GIS functions for Elixir
url: https://github.com/felt/geo
---

Geo
===

A collection of GIS functions. Handles conversions to and from well-known text (WKT), well-known binary (WKB), and GeoJSON for the following geometries:

-   Point
-   PointZ
-   PointM
-   PointZM
-   LineString
-   LineStringZ
-   LineStringZM
-   Polygon
-   PolygonZ
-   MultiPoint
-   MultiPointZ
-   MultiLineString
-   MultiLineStringZ
-   MultiLineStringZM
-   MultiPolygon
-   MultiPolygonZ
-   GeometryCollection

_Note_: If you are looking for the Postgrex PostGIS extension, check out geo\_postgis.

_Note_: If you are looking to do geospatial calculations in memory with Geo's structs, check out topo.

defp deps do
  \[
    {:geo, "~> 4.0"}
  \]
end

Examples
--------

Encode and decode WKT and EWKT:

iex(1)\> {:ok, point} \= Geo.WKT.decode("POINT(30 -90)")
%Geo.Point{ coordinates: {30, \-90}, srid: nil}

iex(2)\> Geo.WKT.encode!(point)
"POINT(30 -90)"

iex(3)\> point \= Geo.WKT.decode!("SRID=4326;POINT(30 -90)")
%Geo.Point{coordinates: {30, \-90}, srid: 4326}

Encode and decode WKB and EWKB:

iex(1)\> {:ok, point} \= Geo.WKB.decode("0101000000000000000000F03F000000000000F03F")
%Geo.Point{ coordinates: {1.0, 1.0}, srid: nil }

iex(2)\> Geo.WKB.encode!(point)
"00000000013FF00000000000003FF0000000000000"

iex(3)\> point \= Geo.WKB.decode!("0101000020E61000009EFB613A637B4240CF2C0950D3735EC0")
%Geo.Point{ coordinates: {36.9639657, \-121.8097725}, srid: 4326 }

iex(4)\> Geo.WKB.encode!(point)
"0020000001000010E640427B633A61FB9EC05E73D350092CCF"

Encode and decode GeoJSON:

Geo only encodes and decodes maps shaped as GeoJSON. JSON encoding and decoding must be done before and after.

\# Examples using JSON as the JSON parser

iex(1)\> Geo.JSON.encode(point)
{:ok, %{ "type" \=> "Point", "coordinates" \=> \[100.0, 0.0\] }}

iex(2)\> point \= JSON.decode!("{\\"type\\": \\"Point\\", \\"coordinates\\": \[100.0, 0.0\] }") |> Geo.JSON.decode
{:ok, %Geo.Point{coordinates: {100.0, 0.0}, srid: 4326, properties: %{}}

iex(3)\> Geo.JSON.encode!(point) |> JSON.encode!
"{\\"coordinates\\":\[100.0,0.0\],\\"type\\":\\"Point\\"}"

Copyright and License
---------------------

Copyright (c) 2014 Bryan Joseph

Released under the MIT License, which can be found in the repository in `LICENSE`.
