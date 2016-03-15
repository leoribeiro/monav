# Introduction #

The preprocessor performs the preprocessing phase for each plugin and writes the necessary data to a specified output directory.

The preprocessor comes in two shapes: a console version as well as a GUI version.

# Details #

A single MoNav map package consists of several modules, at least one module for each category:
  1. Routing Module: ( [Router](Router.md) + [GPS Lookup](GPSLookup.md) )
  1. Rendering Module: ( [Renderer](Renderer.md) )
  1. Address Lookup Module: ( [Address Lookup](AddressLookup.md) )

The user can switch between modules on-the-fly, therefore it makes sense to bundle different modules into a single map package, e.g. bicycle and motorcar routing.

## GUI ##

![http://monav.googlecode.com/svn/wiki/images/screenshots-0.3/preprocessor-1.png](http://monav.googlecode.com/svn/wiki/images/screenshots-0.3/preprocessor-1.png)

You can compile a map package using only the GUI tool. However, if you want to generate huge sets of map packages you should consider using the console version and automate the whole process.

![http://monav.googlecode.com/svn/wiki/images/screenshots-0.3/preprocessor-2.png](http://monav.googlecode.com/svn/wiki/images/screenshots-0.3/preprocessor-2.png)

First of all you have to specify the input file. This file will be passed to the importer plugin you will choose later on. Currently [OSM XML](http://wiki.openstreetmap.org/wiki/Data_Primitives) files as well as [PBF](http://wiki.openstreetmap.org/wiki/PBF_Format) files are supported. PBF files have the advantage of being parsed ten times faster. Therefore you should choose the PBF format if possible.

The output directory will contain the map package. It has to exist and should be empty. You can set the name of the map package, i.e. the name of the city / country / continent. If you desire you can limit the amount of threads used during the data processing.

The packaging option packages every module into a MoNavMapModule file. Currently only the RoutingDaemon support unpacking those, the MoNavClient currently cannot handle them.

You also have the option to save and load the settings. This is especially useful if you want to use a specific set of options from the console as you can just specify the settings file to be used.

![http://monav.googlecode.com/svn/wiki/images/screenshots-0.3/preprocessor-3.png](http://monav.googlecode.com/svn/wiki/images/screenshots-0.3/preprocessor-3.png)

Here you can choose which plugins to use for each type of module. Also, you can set a name for each module, which will be later displayed to the user. Be sure to also set every plugin's settings before proceeding further.

Most of the time you will just want to process all modules used for the MoNavClient. Just press the "Build All" button and you are done. If you want to generate the routing module for the RoutingDaemon press the "Build Daemon Data" button. If you know what you are doing you can also build single modules using one of the "Preprocess" buttons. Just be sure, that the Importer has finished its preprocessing before you start any of the other modules.

## Console ##

Most plugins offer their full set of settings also on the console. However, for those that do not you have to create a settings file using the GUI version of the preprocessor. You can then use this setting file with the console version.

Currently the console version supports the following settings:

### Global ###
|**Short Command**|**Verbose Command**|**Description**|**Type**|
|:----------------|:------------------|:--------------|:-------|
|-i               |--input            |input file     |filename|
|-o               |--output           |output directory|directory|
|-n               |--name             |map package name|string  |
|-p               |--plugins          |lists plugins  |        |
|-pi              |--importer         |importer plugin|plugin name|
|-pro             |--router           |router plugin  |plugin name|
|-pg              |--gps-lookup       |gps lookup plugin|plugin name|
|-pre             |--renderer         |renderer plugin|plugin name|
|-pa              |--address-lookup   |address lookup plugin|plugin name|
|-di              |--do-importing     |runs importer  |        |
|-dro             |--do-routing       |creates routing module|module name|
|-dre             |--do-rendering     |creates rendering module|module name|
|-da              |--do-address-lookup|creates address lookup module|module name|
|-dc              |--do-config        |writes main map config file|
|-dd              |--do-del-tmp       |deletes temporary files|        |
|-m               |--do-package       |packages modules|        |
|-mb              |--module-block-size|block size used for packaged map modules|integer |
|-md              |--module-dictionary-size|block size used for packaged map modules|integer |
|-l               |--log              |writes log to file|filename|
|-s               |--settings         |use settings file|settings filename|
|-v               |--verbose          |verbose logging|        |
|-t               |--threads          |number of threads|integer |
|-h               |--help             |displays help page|

A typical run of the console version producing a fill map package look something like:
```
./monav-preprocessor -s=settings.ini -i=germany.osm.pbf -o=germany -n=Deutschland -pi="OSM Importer" -pro="Contraction Hierarchies" -pg="GPS Grid" -pre="OSM Renderer" -pa="Unicode Tournament Trie" -di -dro=Motorcar -dre=Online -da=Normal -dc -dd -v
```

### Plugin Settings ###
Many plugins also provide console commands to set some or all of their settings instead of reading them from the settings file:

#### Mapnik Renderer ####
|**Short Command**|**Verbose Command**|**Description**|**Type**|
|:----------------|:------------------|:--------------|:-------|
|                 |--mapnik-theme     |mapnik theme file|filename|

#### Contraction Hierarchies ####
|**Short Command**|**Verbose Command**|**Description**|**Type**|
|:----------------|:------------------|:--------------|:-------|
|                 |--block-size       |sets block size of compressed graph to 2^x|integer > 7|

#### Qtile Renderer ####
|**Short Command**|**Verbose Command**|**Description**|**Type**|
|:----------------|:------------------|:--------------|:-------|
|                 |--qtile-input      |osm/osm.pbf input file|filename|
|                 |--qtile-rendering-rules|rendering rules file|filename|

#### OpenStreetMap Importer ####
|**Short Command**|**Verbose Command**|**Description**|**Type**|
|:----------------|:------------------|:--------------|:-------|
|                 |--profile          |build in speed profile|speed profile name|
|                 |--profile-file     |read speed profile from file|speed profile filename|
|                 |--list-profiles    |lists build in speed profiles|
|                 |--add-language     |adds a language to the language list|name[:XXX]|


## Things that can ( and will ) go wrong ##
  * The application may crash. Since this software is still in its beta phase, this will happen sometimes. Apart from bugs, this can happen if:
    * You ran out of RAM: Happens often for larger data sets. Consult [MoNav](MoNav.md) and the plugin's pages for pointers on how much RAM is needed.
    * You did not set up your system for the plugin, e.g.: The MapnikRenderer requires a postgrseql database and correct stylesheets, fonts, coastlines and input plugins.
  * You get an error message. Hopefully this error message helps you solve the problem.
  * You did not compile the application properly.
  * Some plugins are missing.
If you encountered a bug feel free to create an issue on the [bugtracker](http://code.google.com/p/monav/issues/list).