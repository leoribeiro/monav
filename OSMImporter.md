# Introduction #

Imports [OSM XML](http://wiki.openstreetmap.org/wiki/Data_Primitives) files as well [PBF](http://wiki.openstreetmap.org/wiki/PBF_Format) files.

# Details #

The plugin tries to import as much data as possible from the OpenStreetMap file. Since many data schemes are convoluted or fuzzy expect some slight errors when importing.

The plugin imports:
  * ways:
    * all ways with a highway tag specified in the speed profile
    * `oneway` tag: `1, true, yes, 0, false, no, -1`
    * `junction` - `roundabout` sets oneway tag and overwrites highway type with `junction`
    * `highway` - `motorway` / `motorway_link` sets oneway tag
    * `maxspeed` tag if formatted correctly: `"40", "40 kmh", "40kmh", "40 km/h", "40km/h", "40", "40 mph", "40mph"`
    * it is determined whether a way is inside a city via:
      * if a bounding polygon is specified as a single way it is used
      * otherwise all ways within a radius from the city node, smaller places overwrite larger ones:
        * city: 10000m
        * town: 5000m
        * village: 1000m
        * hamlet: 300m
    * the name of a street is determined for two purposes:
      * address lookup: the `name` / `name:XXX` tag is used if available
      * route descriptions / driving instruction: `ref` is used if available, otherwise `name` / `name:XXX` is used.
    * `access` tag is interpreted via the official access tree:
      * access
        * foot
        * ski
        * inline\_skates
        * ice\_skates
        * climbing
        * hiking
        * horse
        * vehicle
          * bicycle
          * carriage
          * wheelchair
          * motor\_vehicle
            * motorcycle
            * moped
            * mofa
            * motorcar
              * hov
            * caravan
            * psv
              * bus
              * taxi
            * snowmobile
            * agricultural
            * forestry
            * emergency
            * hazmat
  * nodes:
    * latitude, longitude, id and name
    * all places with a place type in { city, town, village, hamlet, suburb }
    * population statistics for each place
    * traffic signal nodes

## Settings ##

![http://monav.googlecode.com/svn/wiki/images/screenshots-0.3/preprocessor-8.png](http://monav.googlecode.com/svn/wiki/images/screenshots-0.3/preprocessor-8.png)

  * The input .osm or .osm.bz2 XML file or .pbf file has to be specified
  * A speed profile has to be specified
  * Alternatively a custom speed profile can be created
  * The set of imported languages can be changed. For each node and way the list is traversed from top to bottom and the first available tag is used as a name.