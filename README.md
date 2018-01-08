# mapzenTests
Running an offline mapzen styled map since Mapzen is shutting down
https://mapzen.com/blog/migration/

Should work offline and display this: (note: using default `scene.yaml` file)

![screenshot](https://raw.githubusercontent.com/vomc/mapzenTests/master/Screen%20Shot%202018-01-08%20at%203.08.10%20PM.png)


## How to setup

Clone the repo and run this on localhost:999 via `sudo python -m SimpleHTTPServer 999` and it should work. Note that we are just using the `scene.yaml` file here, not the `refill-style.yaml` just yet. 

## How to generate your own tiles using tilepack

You will need python3 on your machine and then follow the setup from here: 

https://github.com/tilezen/tilepacks

Once you have that installed inside a virtual env, first activate it:

`source env/bin/activate`

Then run the command like this (use your own MAPZEN key):

`$ MAPZEN_API_KEY=mapzen-xxxxxx tilepack -122.51489 37.70808 -122.35698 37.83239 10 15 sf_mvt_10_15 --tile-size 512`

This will download tiles for San Francisco (note that the bounds are specified in reverse for some reason and you start with the bottom left corner, then the top right). This will generate a .zip file called `sf_mvt_10_15.zip`, make sure you move that into this repository and then unzip it.

Inside `scene.yaml`:

`sources:
  mapzen:
    type: MVT
    url:  /sf_mvt_10_15/all/{z}/{x}/{y}.mvt
    tile_size: 512
    max_zoom: 15`

