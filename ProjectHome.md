MoNav is a Desktop / Mobile application that offers state-of-the-art fast and exact routing with OpenStreetMap Data.

## News ##

  * 23.4.2011: Version 0.3 has been released:
    * Highlights:
      * UI Overhaul, take a look at the [Screenshots](#Screenshots.md)
      * Offline vector renderer: [QTileRenderer](QTileRenderer.md)
      * [PBF](http://wiki.openstreetmap.org/wiki/PBF_Format) support: 10 times faster OpenStreetMap data parsing!
      * Better handling of map data and map modules: It is now very easy to switch between routing ( motorcar, bicycle, pedestrian ) and rendering modes ( online, offline vector... ).
      * Full Maemo support
      * Track logging
      * Console version of the preprocessor
      * Improved import of OpenStreetMap data: surface, smoothness, barriers, ...
    * Downloads available [here](http://monav.openstreetmap.de/)

## Project Details ##

In contrast to most commercial and open-source routing applications, MoNav offers exact routing without heuristic assumptions and with very little computational work. Its routing core is based on [Contraction Hierarchies](ContractionHierarchies.md)

The application is divided into two parts: The [MoNav Preprocessor](MoNavPreprocessor.md) transforms the raw OpenStreetMap data into file formats usable by the [MoNav Client](MoNavClient.md) application. The preprocessing is often time consuming and requires larger amounts of memory, as well as a x86-64 OS. The client application on the other hand has very few requirements and can even run on mobile devices.

Additionally a routing daemon is available to act as a background route server for other applications. The SVN version of [Marble](http://edu.kde.org/marble/) already supports the routing daemon as a backend.

MoNav is based on a diploma [thesis](http://code.google.com/p/monav/downloads/detail?name=thesis.pdf&can=2&q=) by Christian Vetter.

## Project Information ##

  * [Downloads](Downloads.md)
  * [Plugins](Plugins.md)
  * [Compile Guide](CompileGuide.md)
  * [MoNav Preprocessor](MoNavPreprocessor.md)
  * [MoNav Client](MoNavClient.md)
  * [MoNav Routing Daemon](MoNavRoutingDaemon.md)

## System Requirements ##

### Preprocessing ###
  * Linux OS
  * RAM and disk usage is based on the graph size, choice of plugins, and speed profile, e.g.:
    * Germany ~1GB RAM, 8GB free disc space
    * Europe 6GB RAM, 27GB free disc space
    * Planet 20GB RAM, 200GB free disc space

### Client ###
  * Any OS supported by Qt ( http://doc.qt.nokia.com/4.6/supported-platforms.html ), e.g.:
    * Windows
    * Windows Mobile
    * Linux
    * Embedded Linux
    * Maemo
    * Symbian
  * 10MB RAM
  * Disk usage is based on the graph size, choice of plugins, and speed profile, e.g.:
    * Germany 570MB + renderer data
    * Europe 3.5GB + renderer data
    * Planet 12GB + renderer data

## Screenshots ##

![http://monav.googlecode.com/svn/wiki/images/screenshots-0.3/client-route-bike.png](http://monav.googlecode.com/svn/wiki/images/screenshots-0.3/client-route-bike.png)

![http://monav.googlecode.com/svn/wiki/images/screenshots-0.3/client-route-luxembourg-szczecin.png](http://monav.googlecode.com/svn/wiki/images/screenshots-0.3/client-route-luxembourg-szczecin.png)

![http://monav.googlecode.com/svn/wiki/images/screenshots-0.3/client-addresssearch-praha.png](http://monav.googlecode.com/svn/wiki/images/screenshots-0.3/client-addresssearch-praha.png)

![http://monav.googlecode.com/svn/wiki/images/RouteDescriptionList.png](http://monav.googlecode.com/svn/wiki/images/RouteDescriptionList.png)

![http://monav.googlecode.com/svn/wiki/images/screenshots-0.3/client-settingsmenu.png](http://monav.googlecode.com/svn/wiki/images/screenshots-0.3/client-settingsmenu.png)

![http://monav.googlecode.com/svn/wiki/images/screenshots-0.3/mapchooserworldmap.png](http://monav.googlecode.com/svn/wiki/images/screenshots-0.3/mapchooserworldmap.png)

![http://monav.googlecode.com/svn/wiki/images/screenshots-0.3/mainwindowbikeroute.png](http://monav.googlecode.com/svn/wiki/images/screenshots-0.3/mainwindowbikeroute.png)

## License ##

All map data displayed in screenshots or available as downloads is licensed as CC-BY-SA by OpenStreetMap and contributors,