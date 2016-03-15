## Plugins ##
MoNav uses several plugins:
  * [Importer](Importer.md) - IImporter
  * [Router](Router.md) - IRouter
  * [Renderer](Renderer.md) - IRenderer
  * [GPS Lookup](GPSLookup.md) - IGPSLookup
  * [Address Lookup](AddressLookup.md) - IAddressLookup

Additionally each plugin has to support the IPreprocessor interface to precompute its data.

## Available Plugins ##

Currently available plugins are:
  * Importer - [OSMImporter](OSMImporter.md)
  * Router - [ContractionHierarchies](ContractionHierarchies.md)
  * Renderer - [MapnikRenderer](MapnikRenderer.md)
  * Renderer - [OSMRenderer](OSMRenderer.md)
  * Renderer - [QTileRenderer](QTileRenderer.md)
  * GPS Lookup - [GPSGrid](GPSGrid.md)
  * Address Lookup - [UnicodeTournamentTrie](UnicodeTournamentTrie.md)