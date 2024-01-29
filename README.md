# otl-metromerger
Simulate the merger (or redistricting) of smaller polygon areas into larger regions, with Leaflet thematic hover map

## Link
https://ontheline.github.io/otl-metromerger/index.html

## Shortcode to embed in http://OnTheLine.trincoll.edu
```
<iframe src="https://ontheline.github.io/otl-metromerger/index.html" width="100%" height=520></iframe>
```

## To Do
- update data sources from CT Open Data, Municipal Fiscal Indicators 2021 https://data.ct.gov/Local-Government/Municipal-Fiscal-Indicators-Economic-and-Grand-Lis/jrwx-mxhm/about_data
  - Town
  - Population 2021 (from Census ACS)
  - Income per capita 2021 (from Census ACS)
  - Equalized Net Grand List (ENGL) as "taxable property" (from CT OPM)
- update to newer Leaflet hosted CDN https://leafletjs.com/download.html
- update to newer jQuery hosted CDN https://releases.jquery.com
- redesign code: simplify from `data.js` to `data.geojson` format, as we do in nearly all other OnTheLine leaflet maps
- add GA code
- rewrite all README instructions
- Create index-frame.html with caption, sources, credits
- Create better solution to display source data. Currently, source data downloadable via a hard-coded link (data.csv) to GitHub Pages
- Future redesign to display both indiv and merged data inside info window, perhaps in 2-row table with headings, to unify display and remove redundant labels


## Steps to construct this

Simplify instructions below: To join new data to the existing Connecticut towns geojson file, use http://mapshaper.org command line tools to jump over steps 2-3-4. See http://www.datavizforall.org/shape/mapshaper/index.html

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
