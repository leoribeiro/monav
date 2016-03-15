# Introduction #

The GPSGrid plugin stores the routing edges in grid cells. A 3-stage table lookup is used as an index, similar to a multilevel page table.

# Details #

## Coordinate Transformation ##

The node coordinates are converted with a Mercator projection. This allows distance comparison with Euclidean metric in a local environment.

## Grid ##

The transformed coordinate system is divided into a grid of 32768x32768 cells. Each edge is inserted into every grid cell it clips. Within each cell edges are concatenated into paths to store them efficiently. Furthermore each cell is compressed.

## Index ##

The index resembles a multilevel page table with 3 levels. Each level contains tables with 32x32 entries. In the top and middle layer each entry refers to a table in the lower level. The bottom layer stores the index of the grid cell in question.

![http://monav.googlecode.com/svn/wiki/images/GPSGridIndex.png](http://monav.googlecode.com/svn/wiki/images/GPSGridIndex.png)