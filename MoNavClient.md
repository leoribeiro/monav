# Overview #

The client application is the one that end users usually notice as being MoNav. It makes use of the data preprocessed by the [Preprocessor](MoNavPreprocessor.md)]. This data is required to display maps, search for addresses, and to compute routes.

Initially, the client application only uses 3MB cache. It is advised to increase this in the settings to achieve better performance.

# Map Packages #

Preprocessed map packages are available for download from [monav.openstreetmap.de](http://monav.openstreetmap.de). Download, extract and place one or more packages in a dedicated directory somewhere on your machine where enough space is left.

At the very first startup, the client application will show a dialog where the user needs to select the directory containing the map packages:

![http://monav.googlecode.com/svn/wiki/images/screenshots-0.3/datadirectory.png](http://monav.googlecode.com/svn/wiki/images/screenshots-0.3/datadirectory.png)

Select the package to use during a session from the world map displayed:

![http://monav.googlecode.com/svn/wiki/images/screenshots-0.3/mapchooserworldmap.png](http://monav.googlecode.com/svn/wiki/images/screenshots-0.3/mapchooserworldmap.png)

In case the map view is inconvenient, switch it off using the dedicated button and select the package from the list displayed instead:

![http://monav.googlecode.com/svn/wiki/images/screenshots-0.3/mapchooserlist.png](http://monav.googlecode.com/svn/wiki/images/screenshots-0.3/mapchooserlist.png)

## Main Window ##

After selecting the map package, MoNav will display its main window:

![http://monav.googlecode.com/svn/wiki/images/screenshots-0.3/mainwindowmapview.png](http://monav.googlecode.com/svn/wiki/images/screenshots-0.3/mainwindowmapview.png)

On the right hand side, the user finds two zoom button to zoom in and out. On the left hand side, the user finds two buttons to set the source and target for calculating routes. On the top edge a multimode button allows the user to either finish source and target selection, or to set MoNav into routing mode. It will then provide printed route instructions. On the bottom edge, the user can manage bookmarks, pan the map to certain locations, and configure various aspects of MoNav to his likings.

### Basic Routing ###

To set the source, choose the arrow button on the left hand side of the screen. From the appearing menu, choose the method to set the source. This basically means to click on the map, to choose one of the bookmarks, to choose an address, or to link MoNav to the current GPS location, which is especially useful for mobile devices. In case you have chosen to click on the map to create a route, leave the source selection mode by clicking on the multi mode button on the top edge of the screen.

To set the target, choose the red circle button on the left hand side of the screen. It works the same way as the source selection button, except the the current GPS location cannot be linked to the target. On the other hand, this menu hosts two buttons to add via points. Click on them to make additional via points appear between the source and target button. In case you have chosen to click on the map to create a route, leave the target selection by clicking on the multimode button on the top edge of the screen.

At each click on the map, MoNav will automatically create a new route. On mobile devices, MoNav will recompute the route each time it gets a new position information from the GPS subsystem of the device. Here's a bike route from Karlsruhe to Rostock in routing mode, while displaying turn instructions:

![http://monav.googlecode.com/svn/wiki/images/screenshots-0.3/mainwindowbikeroute.png](http://monav.googlecode.com/svn/wiki/images/screenshots-0.3/mainwindowbikeroute.png)


### Address search ###

MoNav provides fast address search, filtering the results while you type. The address search can be used to set the source, the target, or routepoints:

| ![http://monav.googlecode.com/svn/wiki/images/screenshots-0.3/client-addresssearch-praha.png](http://monav.googlecode.com/svn/wiki/images/screenshots-0.3/client-addresssearch-praha.png) |
|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|

MoNav currently does not support searching for house numbers or zip codes.

In case MoNav finds more than one entry for the place name selected, it will display a map where you can toggle through the results using the two arrow buttons. If you found the correct target, select it via the button labeled as »Choose City«:

| ![http://monav.googlecode.com/svn/wiki/images/screenshots-0.3/client-addresssearch-place-selection.png](http://monav.googlecode.com/svn/wiki/images/screenshots-0.3/client-addresssearch-place-selection.png) |
|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|

Searching for the street works the same way, providing a live search while you type. After selecting a street, MoNav will display it highlighted. You can still click on the map to set the target selector to the desired location:

| ![http://monav.googlecode.com/svn/wiki/images/screenshots-0.3/client-addresssearch-street-selection.png](http://monav.googlecode.com/svn/wiki/images/screenshots-0.3/client-addresssearch-street-selection.png) |
|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|

## Bookmarks ##

Bookmarks are used to save your individual points of interest, maybe your home location, locations of your friends and the like.Bookmarks are available for selecting the source, the target, routepoints, and from the goto-menu. Additionally, there's a dedicated button in the main window to open the bookmarks dialog:

| ![http://monav.googlecode.com/svn/wiki/images/screenshots-0.3/client-bookmarks-dialog.png](http://monav.googlecode.com/svn/wiki/images/screenshots-0.3/client-bookmarks-dialog.png) |
|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|

In this dialog, you can add new bookmarks using the source and target. Bookmarks can be deleted and chosen from the list of saved bookmarks. Press select to leave the dialog and to set the bookmark as source, target or map center, depending on the context from which you opened this dialog.

## Settings ##

The settings menu provides several sections to configure MoNav to your likings. The most important ones are the settings concerning the map packages, the map modules, and the general settings:

| ![http://monav.googlecode.com/svn/wiki/images/screenshots-0.3/client-settingsmenu.png](http://monav.googlecode.com/svn/wiki/images/screenshots-0.3/client-settingsmenu.png) |
|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|

### Map Packages ###

The map packages dialog will allow you to select the main map repository as described above.

### Map Modules ###

This option allows you to select the modules to use from the chosen mpa package. Some map packages may only provide one option. Others may provide a selection for car, bike, and pedestrian routing, an option to switch between offline vector map rendering and online map tiles from the openstreetmap server, or options concerning the address lookup:

| ![http://monav.googlecode.com/svn/wiki/images/screenshots-0.3/client-mapmodules-selection.png](http://monav.googlecode.com/svn/wiki/images/screenshots-0.3/client-mapmodules-selection.png) |
|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|

### General Settings ###

This dialog provides several pages, hosting settings concerning the user interface, the routing, and track logging.

#### GUI ####

On computers with high resolution screens, e.g. smart phones, the user might want to set the map magnification to a value greater than 1. This will effectively use more pixels on the screen to display one pixel of the map image, so the map gets more readable.

The icon size can be adjusted so the user interface is either easier to use or leaves more space left for displaying the map.

On desktop machines, it is recommended to use traditional popup menus. On mobile devices with a touch screen, it is recommended to use overlay menus.

| ![http://monav.googlecode.com/svn/wiki/images/screenshots-0.3/client-settings-gui.png](http://monav.googlecode.com/svn/wiki/images/screenshots-0.3/client-settings-gui.png) |
|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|

#### Routing ####

While MoNav provides turn instructions, it usually rotates the map automatically. This might be unwanted, e.g. when using online tiles where text labels will also show rotated, or people who prefer maps which show north up:

| ![http://monav.googlecode.com/svn/wiki/images/screenshots-0.3/client-settings-routing.png](http://monav.googlecode.com/svn/wiki/images/screenshots-0.3/client-settings-routing.png) |
|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|

#### Logging ####

MoNav can record your trips to a GPX trackklog. This feature can be enabled or disabled. A path where the tracklog file should be placed can be selected, and the tracklog can be cleared:

| ![http://monav.googlecode.com/svn/wiki/images/screenshots-0.3/client-settings-logging.png](http://monav.googlecode.com/svn/wiki/images/screenshots-0.3/client-settings-logging.png) |
|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|

A recorded tracklog will be displayed in red colour on top of the map.