# Introduction #

The QTileRenderer renders tiles based on vector data as they are needed. Data from Openstreetmap is converted by the preprocessor to a format that is space efficient and allows efficient retrieval of map features within the area of a tile.

# Technical Details #

It shares much of its codebase with the [MapnikRenderer](MapnikRenderer.md). Where the MapnikRenderer would fetch a tile from disk, the QTileRenderer draws the tile on the fly.

Drawing tiles and displaying them is used instead of drawing directly to the screen as it allows the slow vector drawing operations to be done infrequently and the tiles to be cached for subsequent refreshes.

For each map feature the preprocessor decides which openstreetmap tiles it falls within. Any feature which falls within more than one zoom-level 13 tile is split at the zoom-level 13 tile boundaries. Map features are then ordered by the [quadtile](http://wiki.openstreetmap.org/wiki/QuadTiles) of the projected coordinate of their first node, and written to the database. Retrieving data for a tile of zoom level <=13 involves seeking to the correct portion of the database (using an index for speed), and reading consecutive map features until one is read which does not fall in the current tile. For zoom levels >13 the data must be read for the level 13 tile that the smaller tile falls within to ensure all roads which cross the tile are loaded.

Drawing is carried out using the agg graphics library (which is embedded in the code to reduce dependencies), and a series of drawing rules which can be found at the top of tile-write.cpp.

## Settings ##

The main configuration variable currently is the .osm file to read the map data from. Additionally there's a file called rendering.qrr which contains some details how features should look like at different zoom levels.

## Work to do ##

Text is currently drawn for placenames only, but not for streets.

## Screenshots ##

| ![http://monav.googlecode.com/svn/wiki/images/screenshots-0.3/qtilerenderer-placenames.png](http://monav.googlecode.com/svn/wiki/images/screenshots-0.3/qtilerenderer-placenames.png) |
|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|