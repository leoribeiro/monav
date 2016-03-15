# Introduction #

The OSMRenderer fetches the map directly from the OpenStreetMap server and thus needs no preprocessing. However, it cannot run on the client without an Internet connection.


# Details #

It shares most of its codebase with the [MapnikRenderer](MapnikRenderer.md), differing only in the method of fetching the tiles: While the MapnikRenderer fetches the tiles from a precomputed file, the OSMRenderer fetches them from the OpenStreetMap server.

In addition to this a 50MB disk cache is used as well as a memory cache.

## Settings ##

![http://monav.googlecode.com/svn/wiki/images/OSMRSettings.png](http://monav.googlecode.com/svn/wiki/images/OSMRSettings.png)

Choose the desired zoom levels. It is advisable to omit some to allow for quicker zooming.

Each zoom level is twice the size of the previous zoom level. For a conversion from pixel to meter consult the [OpenStreetMap wiki](http://wiki.openstreetmap.org/wiki/Zoom_levels).

## Screenshots ##

| ![http://monav.googlecode.com/svn/wiki/images/RouteView.png](http://monav.googlecode.com/svn/wiki/images/RouteView.png) | ![http://monav.googlecode.com/svn/wiki/images/MapRoute.png](http://monav.googlecode.com/svn/wiki/images/MapRoute.png) | ![http://monav.googlecode.com/svn/wiki/images/Map.png](http://monav.googlecode.com/svn/wiki/images/Map.png) |
|:------------------------------------------------------------------------------------------------------------------------|:----------------------------------------------------------------------------------------------------------------------|:------------------------------------------------------------------------------------------------------------|