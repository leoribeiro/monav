# Introduction #

The MapnikRenderer uses Mapnik, pgsql and postgis to precompute all tiles necessary to paint the area covered by the data. This means the user has to set up a functional pgsql database to use the [Preprocesor](MoNavPreprocessor.md).

## Note ##

This plugin needs **a lot** of storage space for large areas and is most likely the limiting factor when it comes to deploying the data set to a mobile platform. These platforms often support only <2GB files. Should strange errors occur, try a smaller data set first.

# Details #

First of all, a functional pgsql database populated with OpenStreetMap data has to be created by the user, e.g. by following the official guide: [OpenStreetMap:Mapnik](http://wiki.openstreetmap.org/wiki/Mapnik). Next, a mapnik style sheet has to be created, including valid pointers to coastline data and symbols. This is also covered in the official guide.

The tiles are stored within a file per zoom level. A simple array structure is used as an index.

Whenever the map is to be painted, the necessary tiles are fetched from a memory LRU cache. If the cache does not contain the tile, it is fetched from the tile file. The route overlay, edge highlights, target and source indicators, as well as POIs are painted on top of the tiles.

As the actual painting is done using a QPainter, one can easily switch the rendering engine, e.g.: Raster, OpenGL as described in http://doc.qt.nokia.com/4.6/qapplication.html#setGraphicsSystem

## Settings ##

![http://monav.googlecode.com/svn/wiki/images/MRSettings1.png](http://monav.googlecode.com/svn/wiki/images/MRSettings1.png)

  * Specify a directory containing the [DeJaVu](http://dejavu-fonts.org/wiki/Main_Page) font
  * Specify the mapnik directory containing its input plugins
  * Specify the mapnik theme file created by following the official guide [OpenStreetMap:Mapnik](http://wiki.openstreetmap.org/wiki/Mapnik)

![http://monav.googlecode.com/svn/wiki/images/MRSettings2.png](http://monav.googlecode.com/svn/wiki/images/MRSettings2.png)

  * Choose the desired zoom levels. It is advisable to omit some to allow for quicker zooming.

  * Each zoom level is twice the size of the previous zoom level. For a conversion from pixel to meter consult the [OpenStreetMap wiki](http://wiki.openstreetmap.org/wiki/Zoom_levels).

  * The whole world is rendered down to the specified zoom level. This avoids awkward 1-tile zoom levels.

  * Choose an extra margin around the data set that is also rendered.

![http://monav.googlecode.com/svn/wiki/images/MRSettings3.png](http://monav.googlecode.com/svn/wiki/images/MRSettings3.png)

  * Choose a tile size ( 256x256 Pixel recommended )

  * Choose a metatile size _k_. A metatile will contain _k_ times _k_ tiles. Each rendering thread renders a meta tile and divides it into tiles. Rendering a larger amount of tiles at once is faster, but needs more RAM. Try to adjust this value for your machine and remember to save some memory for the pqsql database.

  * Choose a margin for each metatile. This is necessary for mapnik to allow labels across metatile boundaries. A larger value is more likely to avoid display glitches. 128 pixels are recommended.

![http://monav.googlecode.com/svn/wiki/images/MRSettings4.png](http://monav.googlecode.com/svn/wiki/images/MRSettings4.png)

  * The tiles can be compressed by reducing the color space to 256 colors. Recomended.
  * [PNGCrush](http://pmt.sourceforge.net/pngcrush/) can be used for every tile to further reduce tile size. This takes up a huge amount of time as pngcrush is started for each tile. Be sure to provide pngcrush. Not recomended.
  * Tiles containing no routeable edges are removed. As these tiles often do not use much space, this saves only some storage space. Recommended if the data area contains vast stretches of emptiness, otherwise not.

## Screenshots ##

| ![http://monav.googlecode.com/svn/wiki/images/RouteView.png](http://monav.googlecode.com/svn/wiki/images/RouteView.png) | ![http://monav.googlecode.com/svn/wiki/images/MapRoute.png](http://monav.googlecode.com/svn/wiki/images/MapRoute.png) | ![http://monav.googlecode.com/svn/wiki/images/Map.png](http://monav.googlecode.com/svn/wiki/images/Map.png) |
|:------------------------------------------------------------------------------------------------------------------------|:----------------------------------------------------------------------------------------------------------------------|:------------------------------------------------------------------------------------------------------------|