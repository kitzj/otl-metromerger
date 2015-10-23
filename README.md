# otl-metromerger
Simulate the merger (or redistricting) of smaller polygon areas into larger regions, with Leaflet choropleth map framework for On The Line book (http://OnTheLine.trincoll.edu)

## Demo
http://jackdougherty.github.io/otl-metromerger

## iframe shortcode for OnTheLine book
[iframe src="http://jackdougherty.github.io/otl-metromerger" width="100%" height=520]

## To Do
- insert data source, year, and link (possibly on same line as "export results" and make sure that it also appears in exported output)
- start other versions: a School District merger tool, possibly with CT only data layer, or EdBuild national data layer?
- future redesign to display both indiv and merged data inside info window, perhaps in 2-row table with headings, to unify display and remove redundant labels


## Steps to construct this
1) Begin with Leaflet choropleth tutorial at http://leafletjs.com/examples/choropleth.html

2) Create simplified geoJson layer of Connecticut town boundaries
- Download town boundaries shapefile from UConn MAGIC http://magic.libraries.uconn.edu
- Simplify the polygon shapes to reduce size in geoJson format with this general approach http://chimera.labs.oreilly.com/books/1230000000345/ch12.html#_simplify_the_shapes
- Use MapShaper web tool (http://www.mapshaper.org/) to reduce size without changing too much detail. In this case, I reduced Connecticut boundaries down to 1.5%, around 100k.
- Export "shapefile - polygons", then copy and rename new .shp and .shx files into new folder with original .dbf (to retain data) and original .prj (projection) files

3) Join spreadsheet town data to the new simplified polygon shapefile
- in GIS application (such as ArcGIS or QGIS), load the new simplified polygon shapefile and spreadsheet data
- join data to shapefile, then export > save as new shapefile in new layer, and open attributes to delete unneeded columns
- create a new folder with four files (.shp, .shx, .dbf, .prj) and zip folder for next step

4) Convert new joined shapefile (simplified boundaries + data) into js format to use in Leaflet map
- Use ogre to ogre web client (http://ogre.adc4gis.com/) to convert zipped shapefile to geojson
- Copy and paste the geojson output into a new file, and modify into json this way:
- At top of new file, declare contents as a variable by adding this text:
```
var data =
```
- At the bottom of the new file, add a semicolon (;)
- Rename file suffix as .js, place inside local directory, and upload in the Leaflet HTML index template

5) See code comments in the Leaflet index.html template

## Credits
- Thanks to the creator of the Leaflet Interactive Choropleth Map tutorial (http://leafletjs.com/examples/choropleth.html)
- Thanks to @alvinschang at CT Mirror for creating functions to display info window data, based on examples such as http://projects.ctmirror.org/content/2014/05/raceSchools/
- Thanks to @erose for helping me with the JavaScript logic
- Thanks to @nav10003 Natalia Vorotyntseva at UConn MAGIC (http://magic.lib.uconn.edu) for code to toggle on/off polygons, display results for multiple regions, and export results
