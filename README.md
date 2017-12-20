# Abandoned

**This project is no longer maintained in favor to npm based distribution of [OpenLayers as es2015 modules](https://www.npmjs.com/package/ol)**

## Openlayers Compiler

Docker image for compiling custom build of [Openlayers library](https://github.com/openlayers/openlayers).

## Usage

**TL;DR**

- create configuration file
- build the image
- run docker image

### More detail

Please read [this guide](https://openlayers.org/en/latest/doc/tutorials/custom-builds.html) to write your own openlayers custom build.

#### Write Configuration File

Save it as ``json`` file (e.g ``ol-custom.json``). Example configuration :

```json
{
  "exports": [
    "ol.Map",
    "ol.View",
    "ol.control.defaults",
    "ol.layer.Tile",
    "ol.source.OSM"
  ],
  "compile": {
    "externs": [
      "externs/bingmaps.js",
      "externs/closure-compiler.js",
      "externs/geojson.js",
      "externs/oli.js",
      "externs/olx.js",
      "externs/proj4js.js",
      "externs/tilejson.js",
      "externs/topojson.js"
    ],
    "define": [
      "ol.DEBUG=false"
    ],
    "extra_annotation_name": [
      "api", "observable"
    ],
    "compilation_level": "ADVANCED",
    "manage_closure_dependencies": true
  }
}
```

#### Build Docker Image

```bash
docker build --rm --tag your-image-name:your-tag .
```

Example
```bash
docker build --rm --tag ol-compiler:latest .
```

#### Run Docker Image
```bash
docker run --rm \
  --user $(id -u):$(id -g) \
  --volume $(pwd):/build \
  your-image-name:your-tag <config-file.json> <output-file.js>
```

Example
```bash
docker run --rm \
  --user $(id -u):$(id -g) \
  --volume $(pwd):/build \
  ol-compiler:latest ol-custom.json ol-custom.js
```

### Disclaimer

This Dockerfile is written by [herloct](https://gist.github.com/herloct/58cfa7f8de397f70d481322b002f0238).
