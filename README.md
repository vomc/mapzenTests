# mapzenTests
Running the Amman map style on heroku since MapZen is shutting down
https://mapzen.com/blog/migration/

From their docs

To run a map for a city or a region with no network dependencies:

Save `mapzen.js / tangram.js, index.html` and `scene.yaml` file in a directory.
Extract a pyramid of tiles for area of interest using tilepack and save them in that same directory. (Note you don’t need to go beyond z15 tiles as they contain all the data in higher (>= 16) tiles, and Tangram overzooms.)
To download tiles from our hosted services before shutdown:

https://github.com/tilezen/tilepacks MAPZEN_API_KEY=mapzen-xxxxxx tilepack -122.51489 37.70808 -122.35698 37.83239 10 15 sf_mvt_10_15 --tile-size 512

Size and download speeds makes this viable for a city and perhaps a region. The example above generates a 30MB pyramid of MVT tiles, or 138MB of topojson, for San Francisco. For GeoJSON, SF is 67MB at z14, and 130MB at z15.

Serve tiles via a web server (localhost or hosted).
Create a scene file for Tangram. Note you will need to override the mapzen source in the scene file if you are importing a basemap.
sources:
    mapzen:
        type: MVT
        url:  localhost:8000/sf_mvt_10_15/all/{z}/{x}/{y}.mvt
        tile_size: 512
        max_zoom: 15

