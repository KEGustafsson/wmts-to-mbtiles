
# WMTS to MBTiles utility

NodeJS utility to fetch map tiles from WTMS service to [MBTiles](https://github.com/mapbox/mbtiles-spec) format.

## Usage
```
Usage: wmts-to-mbtiles [options]

  Options:

    -h, --help          output usage information
    --layers            List WMTS service layers
    --layer [id]        Get layer
    --output [mbtiles]  Output file
    --zoom [zoom]       Zoom level
    --input [url]       WMTS service URL
    --bbox [w s e n]    Latitude and longitude values, eg. "23.411 59.731 26.850 60.562"
```

Defaults:
```
url: https://julkinen.vayla.fi/rasteripalvelu/service/wmts
layer: liikennevirasto:Rannikkokartat public
zoom: 10
```

### Example

Fetch default layer from `liikennevirasto.fi` and output `test.mbtiles`:

    wmts-to-mbtiles --output test.mbtiles

Fetch smaller area:

    wmts-to-mbtiles --zoom 15 --bbox "23.411 59.731 26.850 60.562" --output test.mbtiles

Helper for defining the bbox: http://boundingbox.klokantech.com/

List layers in `{layer id} :: {layer name}` format:

    wmts-to-mbtiles --layers

### Finnish coastal nautical charts:

Check out https://github.com/vokkim/rannikkokartat-mbtiles

### Preview result

Install [mbview](https://github.com/mapbox/mbview):

    npm install -g mbview

Get a [Mapbox access token](https://www.mapbox.com/help/create-api-access-token/) for the basemap and `export MAPBOX_ACCESS_TOKEN=...`

Run `mbview`:
  
    mbview --port 4999 test.mbtiles

## Generate zoom levels

1. Install [GDAL](http://www.gdal.org/)
 - Use docker-compose.yml to get GDAL
 - mbtiles-folder bind to docker

2. Use [gdaladdo](http://www.gdal.org/gdaladdo.html) to generate zoom levels for existing mbtiles file:
    
    gdaladdo -r cubic test.mbtiles 2 4 8 16 32 64 128

Use `cubic` sampling for better results.

## License

MIT
